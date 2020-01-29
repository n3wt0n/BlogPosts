When you use containers for your application, one of the things you need to think about is how to move (aka promote) the container images you generate across different environments.

In this series, I will explore different ways to do so... with the help of __Azure DevOps__

### Intro

In the first article of the series we explored the "Base Registry" approach to promote a Container image across different environments.  
And we got rid of the additional registry and we used a Build Artifact in the second part.  

In this third and final part we will use the same approach as the second one, but using 100% the __YAML Pipelines__ (or, more appropriately, the ___Multi-stage Pipelines___).

### Before starting

While the Multi-stage Pipeline editor should be already the default experience at the time of writing, if you can't see it be sure to have it enabled in the preview features.

In this article I will use some YAML code snippet to go through the example.  
You can [download the complete YAML Pipeline definition file here]().

### Building the image

As in the last article, we will start with building the application and creating our container image from it, with all we need for our application to function properly.

We will again use the _"Artifact way"_

As you can see, I not only create the image, but I "Save it" and then I pusblish it as a Build Artifact.  

> Build Artifacts are stored into Azure DevOps services directly, or you can even select your own fileshare for them. I normally use the service because it is free and it doesn't require any maintenance.

The __"Save image"__ step uses the _docker save_ command to export the container image we have just created into a .tar file.

![Save Image](https://thepracticaldev.s3.amazonaws.com/i/4z683v6nfbxyc6voqgqw.png)

The _save_ command is not directly embedded in the v2 of the Docker task, so we need to manually type the command name, and insert the image name in the arguments box.  
I have defined variables for the names so I can reuse them across the different environments.

Also, note that I have to specify the output for the command, and I use the _$(build.artifactstagingdirectory)_ system variable to store the exported image in the folder the Azure DevOps service uses as base path.

As soon as I have my image saved in a "normal file" I then can use it as a Build Artifact. To do so, I have to perform a __Publish Artifact__ step:

![Publish Artifact](https://thepracticaldev.s3.amazonaws.com/i/s9ami6x4ksxwmrc1dqfs.png)

Nothing too difficult here. This step just take thes content of the _$(build.artifactstagingdirectory)_ folder, zips it and makes it available to a Release Pipeline.

Notice that I selected "Azure Pipelines" as publish location for my artifact: this allows me to use the service storage instead of a custom file share.

### Let's Release

Ok, now we have our container image, and we have created a Build Artifact with it.

We are going to create a __Release Pipeline__ which will use the Build Artifact as input, and will use it to deploy to the different environments.

![Artifact](https://thepracticaldev.s3.amazonaws.com/i/q6fuxwhi13h4z6djgzdb.png)

To do so, simply click on the "_Add an artifact_" button (after creating a new release pipeline), and select "_Build_". Select the _Build Pipeline_ we just created before, and you're ready to go.  
Also, be sure to enable the __Continuous Delivery__ flag so this release pipeline can run every time a new container image is pushed to the registry.

Now, as in the previous example we have three different environments: Dev, Test, and Prod. First thing to do is to create three _Stages_ in the Pipeline.

Then let's edit the _Dev_ stage. We need to:

* Load the image from the .tar file in the Build Artifact
* Change it's name so it can be pushed to the Dev registry
* Push it to the Dev registry

![The steps](https://thepracticaldev.s3.amazonaws.com/i/uc37uxtguzvafr0wpg1a.png)

The main part is, obviously, the first step: we need to __restore the image from the .tar__ file we created in the build. Adain, a little trick is necessary.
The _load_ command, in fact, is not directly embedded in the v2 of the Docker task.

![Load the image from the artifact](https://thepracticaldev.s3.amazonaws.com/i/tsr17dqx156bvow3kfca.png)

So we need to manually type _load_ as command name, and fill in the parametersin the arguments box.

Note that the input path uses the _$(System.DefaultWorkingDirectory)_ system variable: it represents the folder where the Build Artifacts are stored for the Release Pipelines. The full path is composed by the base directory, the name of the Artifact we have chosen, "drop" (or anything else you defined in the Build Ppipeline's Publish Artifact step) and finally the name of the file. Once again, I have defined variables for the names so I can reuse them across the different environments.

Next we need to __tag__ the image differently, to add the name of the registry. This is because if you have to push an image to a certain registry, you need the image full name as "_registryName/ImageName_", where _registryName_ is the full qualified domain in case of anything different from Docker Hub (for Azure Container Registry, it would be something like _myregistryname.azurecr.io_

Again, the _tag_ command is not embedded in the v2 of the task so we need to use the arguments box. The use of variables is optional but I recommend it, it just makes everything easier to automate and templatize.

![Tag with new registry](https://thepracticaldev.s3.amazonaws.com/i/xcna32cixv6zp48aen0z.png)

Differently from the previous case we analyzed, in this case we can not only tag the image as "latest" but, as in the image above, tag it with a __reference of the Build process__ (in my case I use BuildId). This is possible because the Release Pipeline is triggered directly from a Build Pipeline (or anyway it references it) so we have all the Build information available.

Last step, we need to __push the image__ to the new registry.

![And push it](https://thepracticaldev.s3.amazonaws.com/i/bglztae2mfn44yh0rlk6.png)

This time, the _push_ command is fully supported so no need for the custom arguments!

As for the previous step, also in here we can reference some Build variables.

And we are done for Dev!

Now we can replicate the same process to the other environments, just changing the source and target registries.

Ideally when pushing to the environment-specific registry you should have a mechanism to notify your target host service (App Service, AKS, Container Instances, etc) of the new image so the deployment can be executed.

And of course you probably want to set some _Release Gates_ or _Approvals_ for deploying to Test and Prod.

### Conclusion

This process is not widely used, mostly because people don't know about it, but it is definitely my favorite:

* You have __1:1 mapping between build and release__
  * this means that __the image you build and the one you deploy are for sure the same__.
* You __can directly reference the Build number__, or any other parameter that comes from the Build, because you CI and your CD pipelines are directly related.
* You have __full traceability__

In the next article we will explore how to achieve the same, but using the new YAML MultiStage pipeline.

Stay tuned!
