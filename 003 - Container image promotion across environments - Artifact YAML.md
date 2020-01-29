When you use containers for your application, one of the things you need to think about is how to move (aka promote) the container images you generate across different environments.

In this series, I will explore different ways to do so... with the help of __Azure DevOps__

### Intro

In the first article of the series we explored the "Base Registry" approach to promote a Container image across different environments.  
In the second part we got rid of the additional registry and we used a Build Artifact.  

In this third and final part we will use the same approach as the second one, but using 100% the __YAML Pipelines__ (or, more appropriately, the ___Multi-stage Pipelines___).

### Before starting

While the Multi-stage Pipeline editor should be already the default experience at the time of writing, if you can't see it make sure to have it enabled in the preview features.

In this article I will use some YAML code snippet to go through the examples.  
You can [download the complete YAML Pipeline definition file here](https://github.com/n3wt0n/BlogPosts/blob/master/003%20-%20Container%20image%20promotion%20across%20environments%20-%20Artifact%20YAML/Multistage%20Pipeline%20example.yaml).  
If you want to have the FULL definition, which includes all the build steps for a .Net Core application, [you can download it here](https://github.com/n3wt0n/BlogPosts/blob/master/003%20-%20Container%20image%20promotion%20across%20environments%20-%20Artifact%20YAML/Multistage%20Pipeline%20example%20-%20FULL.yaml).

Ok, let's start

### Pipeline structure

As I have mentioned, we are going to use the Multi-stage Pipeline, the YAML-based version. As the name says, we can have multiple _Stages_ inside a single pipeline definition. Each Stage will be delegated to a specific function.

In this example, riding on the previous articles, I'm going to build the application and the image, and deploy to 3 environments (Dev, Uat, and Prod).
Therefore, we are going to use __4 stages__.

```YAML
 stages:
  
   - stage: CI
     displayName: 'CI stage'
     jobs:
     #JOBS HERE
  
  - stage: CDDev
     displayName: 'CD stage for DEV'
     jobs:
     #JOBS HERE

  - stage: CDUat
     displayName: 'CD stage for UAT'
     jobs:
     #JOBS HERE

  - stage: CDProd
     displayName: 'CD stage for PROD'
     jobs:
     #JOBS HERE
```

I'm going to explain later why I have decided to use different stages for different environments instead of one "CD" stage and multiple jobs for the different environments.

### The CI - _aka Building the image_

As in the last article, we will start with building the application and creating our container image from it, with all we need for our application to function properly.

We will again use the _"Artifact way"_ to publish our Image.

To do so, we start including in the _CI Stage_ all the tasks the are responsible for building/compiling/publishing our application:

```YAML
- stage: CI
     displayName: 'CI stage'
     jobs:
     - job: Build
       displayName: 'Build for MyProject'
       steps:
        # Add all the tasks you need to build your project
       - task: WhateverTask@1
         displayName: 'Build MyProject'
         # all the parameters you need
```

When we have that, we need to create the Container Image and, as we did last time, export that in the Tar format:

```YAML
   - task: Docker@2
     displayName: 'Build MyProject image'
     inputs:
       repository: '$(ImageName)'
       command: build
       Dockerfile: MyProject/Dockerfile
       tags: $(Build.BuildId)
  
   - task: Docker@2
     displayName: 'Save image to TAR'
     inputs:
       repository: '$(ImageName)'
       command: save
       arguments: '--output $(build.artifactstagingdirectory)/$(ImageName).image.tar $(ImageName):$(Build.BuildId)'
       addPipelineData: false
```

Those commands are exactly like the ones we used in the previous article, but in their YAML representation.

The __"Save image to TAR"__ step uses the _docker save_ command to export the container image we have just created into a .tar file.
  
I have defined variables for the names so I can reuse them across the different environments.

__Variables__ can be specified inside the YAML or in the UI. In this case I decided to include it into the YAML, therefore I placed this _before_ the stages definition (so they can be accessed from within any of the stages and jobs):

```YAML
   variables:
     ImageName: 'myprojectreportexecutor'
```

Also, note that I have to specify the output for the command, and I use the _$(build.artifactstagingdirectory)_ system variable to store the exported image in the folder the Azure DevOps service uses as base path.

As soon as I have my image saved in a "normal file" I then can use it as an Artifact. In the previous article we used the _Build Artifact_ object, in this example we will instead use the new __Pipeline Artifact__ object (which is available only in the YAML Pipelines, not in the Classic ones). To do so, I have to add a __Publish Pipeline Artifact__ step:

```YAML
  - task: PublishPipelineArtifact@1
    displayName: 'Publishing Image as Pipeline Artifact'
    inputs:
      path: $(build.artifactstagingdirectory)
      artifact: 'ContainerImage'
```

> Pipeline Artifacts are stored into Azure DevOps services directly. Differently from the _Build Artifacts_, at the time of writing it is not possible to select your own fileshare for saving them.  
> More info about the difference between Pipeline and Build Artifacts [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/artifacts/artifacts-overview?view=azure-devops)

Nothing too difficult here. This step just takes the content of the _$(build.artifactstagingdirectory)_ folder, zips it and makes it available to subsequent steps/jobs/stages.

The _artifact_ parameter represent the name you want to give to that file on the system. It is an optional parameter, but I'd advise to always name your artifacts so it will be easier to reference them later on.

### And then the CD - _aka deploy time_

Ok, now we have our container image, and we have created a Pipeline Artifact with it. It's time to fill in the other stages.

Before starting, it's importat to understand few things here.

#### Deployment jobs

In the CI part of our pipeline we used one (or more) _job_.  
A job is a generic "collection of task", and usually it is associated with Continuous Integration. Why? Because every job automatically download the source code from the repo associated with the pipeline.

We don't want our code to be re-dowloaded before each deployment, do we?  
For this reason, Azure Pipelines makes available another type of job, specialized in deployment operations: the __deployment job__.

This particular job not only doesn't download the code from the repo, but it automatically downloads any Pipeline Artifact published in any previous stage!

#### Strategies

Another peculiarity of the deployment jobs is that they support different __deployment strategies__. At the time of writing they are _runOnce_, _rolling_ and _canary_.

I will not cover them all in this post (mode information [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops#deployment-strategies)), we are going to use the _runOnce_ one that, as the name says, executes every step only once.

#### Lifecycle hooks

Every deployment strategy has some "Lifecycle hooks" which basically orchestrate the deployment operations: _preDeploy_, _deploy_, etc (more info [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops#descriptions-of-life-cycle-hooks)).

Again, I'm not going to cover them in details in this post. I will use the _deploy_ hook because it is the only one which actually downloads automatically the artifacts.

#### The deployment steps

Ok, now that we have a much clearer (hopefully) idea about those topics, let's take a look at the top of the deployment stage.

I will focus on the DEV environment, because the other ones will be pretty much the same.

```YAML
   - stage: CDDev
     displayName: 'CD stage for DEV'
     jobs:
     - deployment: Dev
       displayName: 'Deploy to DEV'
       environment: MyProject-DEV
       strategy:
         runOnce:
           deploy:
             steps:
```

As you can see, and as I mention before, here I'm using the _runOnce_ strategy with the _deploy_ hook.

By default, this stage will be executed __only__ if the previous stage (the CI) has been succesful.

Wait a minute. What is that "environment"?  
__Environments__ are another new concept available only in YAML pipelines. They allow you to define and map some actual environment for using them as your deployment targets.

At the time of writing, they support only Kubernetes and Virtual Machines as specific resource, but you can create one with no resources. The reason for doing so is that you will have a full history of any deployment to that specific environment.

Also, you can now require __approvals__ for deploying to a specific environment, and that approvals have to be defined in the environment object.

Now, as in the previous example we have three different environments: Dev, Test, and Prod. First thing to do is to create them in Azure DevOps.

> If you don't manually create the environment in Azure DevOps UI, they will be created automatically the first time the pipeline is executed.

Now that we have the environment ready, we can continue.

First step: we need to __restore the image from the .tar__ file we created in the build.

```YAML
  - task: Docker@2
    displayName: 'Load Image from Tar'
    inputs:
      command: load
      arguments: '--input $(Pipeline.Workspace)/ContainerImage/$(ImageName).image.tar'
```

Note that the input path uses the _$(Pipeline.Workspace)_ system variable: it represents the folder where the Pipeline Artifacts are downloaded. The full path is composed by the base directory, the name of the Artifact we have chosen in the CI Publish Artifact step) and finally the name of the file. Once again, I have defined variables for the names so I can reuse them across the different environments.

Next we need to __tag__ the image differently, to add the name of the registry. This is because if you have to push an image to a certain registry, you need the image full name as "_registryName/ImageName_", where _registryName_ is the full qualified domain in case of anything different from Docker Hub (for Azure Container Registry, it would be something like _myregistryname.azurecr.io_).

```YAML
  - task: Docker@2
    displayName: 'ReTag Image with ACR Name - BuildId'
    inputs:
      containerRegistry: MyProjectACRdev # This comes from the Service Connections
      repository: '$(ImageName)'
      command: tag
      arguments: '$(ImageName):$(Build.BuildId) $(ContainerRegistryNameDev)/$(ImageName):$(Build.BuildId)'
```

The use of variables is optional but once again I recommend it, it just makes everything easier to automate and templatize.

> The _containerRegistry_ parameter value needs to match the name of the Service Connection you defined in the Settings that maps your Azure Container Registry (or any other Docker Registry)

Last step, we need to __push the image__ to the new registry.

```YAML
  - task: Docker@2
    displayName: 'Push Image to ACR'
    inputs:
      containerRegistry: MyProjectACRdev
      repository: '$(ImageName)'
      command: push
      tags: $(Build.BuildId)
```

As for the previous step, also in here we can reference some Build variables.

And we are done for Dev!

Now we can replicate the same process to the other environments, just changing the source and target registries (and of course the environment name in the Stage).

Ideally when pushing to the environment-specific registry you should have a mechanism to notify your target host service (App Service, AKS, Container Instances, etc) of the new image so the deployment can be executed.

One last thing, as I mention before you probably want to set some __Approvals__ for deploying to Uat and Prod. This can be done in the Environments section.

### Multiple Stages vs Single Stage for deployment

As I have mentioned before, I decided to create 4 stages (1 for CI and 3 for CD).  
This has been necessary because I want to use __Approvals__.

In fact, approvals are applied at _Environment_ level, and the approval engine of Azure Pipelines requires that "_the execution of a run pauses before entering a stage that uses the environment. Users configured as approvers must review and approve or reject the deployment._" (from the official documentation [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/approvals?view=azure-devops&tabs=check-pass#approvals))

This means that even thought the Environment parameter belongs to the Deployment Job, it is not that job which will wait for the approval. Instead, the Stage containing that Deployment Job will be the one waiting.

Therefore this also means that if you have multiple Deployment Jobs in a Stage, with each job associated to a different environment, and each environment having its own approval, then you would need to approve all the deployment for having the stage to run, making it useless.

If, instead, you have multiple Stages, one per each environment, everything works great.

### Let's run this

When you run the pipeline, the UI will be sligthly different from what you are used to.

This is the main screen:

![Pipeline execution](https://dev-to-uploads.s3.amazonaws.com/i/9phnlgsatp6mquk6cfcd.png)

This instead is the execution log screen:

![Pipeline execution in logs](https://dev-to-uploads.s3.amazonaws.com/i/h4tz109eaqpudk4zi4ow.png)

I have added an Approval request for both Uat and Prod, so this is what happens when the deployment to Dev is successful:

![Waiting for approval](https://dev-to-uploads.s3.amazonaws.com/i/drwy1jrpjlubp1cyfqys.png)

And this is inside the logs:

![Waiting for approval in logs](https://dev-to-uploads.s3.amazonaws.com/i/2cccjud80xrlhnxsm0so.png)

This is what you see when clicking on the "Review" button:

![Approve or Reject](https://dev-to-uploads.s3.amazonaws.com/i/59vdgzvospjv9p7j379i.png)

You have obviously the chance to Approve or to Reject the deployment. If you reject, nothing will be deployed to that environment and the whole pipeline process will stop.

The approval is customizable, in my case I specified that at lest one of the required approvers must approve in order to continue.

Last but not least, the Environments view:

![Environment with deployments](https://dev-to-uploads.s3.amazonaws.com/i/pil3vfsscvg8u64o3vwv.png)

It's pretty useful because you can have an immediate picture of what is deployed in any environment at any given time.

### Conclusion

This process is not widely used, mostly because people don't know about it, but it is definitely my favorite:

* You have __1:1 mapping between build and release__
  * this means that __the image you build and the one you deploy are for sure the same__.
* You __can directly reference the Build number__, or any other parameter that comes from the Build, because you CI and your CD pipelines are directly related.
* You have __full traceability__

In this article we achieved everything using the new Multi-stage Pipelines experience, which allows to version and protect the YAML files (for example setting up a branch policy).

Of course, if you take a look at the full YAML file, it's pretty long and not very readable. In fact, one of the things the we usually recommend is to use __Templates__ and link them in instead of having everything in the same file.

I will cover this in a new post sometimes soon, but if you want to take a look at it [here is the documentation](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/templates?view=azure-devops)
