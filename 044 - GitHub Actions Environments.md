The features everyone was waiting for in GitHub Actions are finally here: __Environments and Manual Approvals__.

This is gonna be fun.

### Intro

Today we talk about Environments and Manual approvals in GitHub Actions. These long-awaited features have been announced at GitHub Universe 2020 couple of weeks ago and finally __released just a few days ago__, on the 15th of December to be precise.

In this video we are going to see how to enable them and how to use them to control our deployment flow. We can finally say that Actions have proper Continuous Deployment capabilities.

If you want to have an overview of everything you can do with GitHub Actions, I highly encourage you to watch the video I made on the subject after you are done with this post, you can find it [here](https://youtu.be/msCWg2F4sck)

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube w_37LDOy4sI %}

([Link to the video: https://youtu.be/w_37LDOy4sI](https://youtu.be/w_37LDOy4sI))

If you rather prefer reading, well... let's just continue :)

### Why Environments?

So first off, why do we talk about Environments and Manual Approval together.

Well, Manual approvals are actually __built on top of Environments__.

And they are __just one of the features__ Environments offer to prevent unauthorized deployments, preserve secrets, track changes and much more.

For these reasons we will talk about all we can do with the Environments. But first, let's see how to enable this feature.

### Enabling Environments and Availability

To do so, just go to the _repository Settings_, and then you have this new _Environments_ section.

Click on it, and here you can create a new Environment.

Give it a name, click on _Configure_ environment, and here you have it.

> Check [this section of the video](https://www.youtube.com/watch?v=w_37LDOy4sI&t=101s) for a demo about enabling environments in your repo.

To configure an environment in a ___user repository___ you must be the __repository owner__. To configure an environment in a repo that belongs to an ___organization___, instead, you must have __admin access__.

Also note that you will be able to create and use Environments __only on public repos or if you are part of a GitHub Enterprise Cloud__ organization. Environments and all their features, including manual approvals, are not currently supported in "normal" private repos and in the Pro and Teams plans. If you go to settings on those repos and plans, in fact, the Environment menu tab simply won't show up.

### Environment Settings

Right, let's go and see what we have in the Environment configuration.

First section is the __Environment Protection Rules__

![Protection Rules](https://dev-to-uploads.s3.amazonaws.com/i/xane291kij549ixainpj.png)

The Environment protection rules can currently be used to configure manual approvals and timeouts, and perhaps more settings will come in the future.

The manual approvals, as the name says, allow you to specify __up to 6 people or teams__ that will be notified for a deployment and will need to approve it for it to continue.

To be in te "Approvers" list you __only need Read Access__ to the repository, and that allows you to have people who can approve deployments that don't necessarily have the ability to alter code.

There is currently no way to specify a minimum number of reviewers, meaning that if just one person approve it, that deployment will continue.

The second setting, instead, is the __Wait Timer__. This is useful if you want your __deployment to be delayed__ of a certain number of minutes after the jobs is triggered. And this works with and without approvals.

We then have the __Secrets section__. 

![Secrets](https://dev-to-uploads.s3.amazonaws.com/i/0kudpivmhdjry2aj6eik.png)

Secrets are __encrypted__ environment variables. They are accessible only by GitHub Actions in the context of ___this environment___.

GitHub already has the Secrets management at repo level, but anybody with write access to a repo can alter those secrets. They cannot see them (_because as you probably know after saving them they can be retrieved only by the Actions in the workflows_), but they can change them and use them in any workflow.

For this reason, we now have Environment level secrets. The job that does the deployment doesn't get access to these secrets until after the approval, if any, and this protect these secrets from unauthorized access.

If you want to know more about secrets, and also how __secrets with the same name__ between Environments and Repo level work, [check this section of the video](https://www.youtube.com/watch?v=w_37LDOy4sI&t=254s).

### Use Environments in an Action Workflow

Let's see how we can actually use all of that in an Actions Workflow. It is pretty easy.

```yaml
  DeployDev:
    name: Deploy to Dev 
    runs-on: ubuntu-latest
    environment: 
      name: YOUR_ENVIRONMENT_NAME
      url: URL_OF_THE_DEPLOYMENT
    steps:
      - name: Deploy
        run: echo I am deploying! 
```

This is all you need to do! Just add the `environment` section to your job and reference the environment __by name__.

The `url` parameter is optional and can be either a _string literal_ or a value coming from an __output parameter__ of a step in the job (this is useful for example if your deployed app changes URL every time and you know it only after deploying it).

Everything that has been configured on that environment, including __approvals__, __timers__ and __secrets__ will be automatically applied to that job.

If an approval is required, all the users/teams in the Approvers list will receive a __notification__ on Screen, by Email, and on the GitHub Notifications. Soon those will also be integrated into the Mobile App and Slack.

### An Example

> Check [this section of the video](https://www.youtube.com/watch?v=w_37LDOy4sI&t=523s) for the __demo__ about this example

Let's say you want to:

- Deploy to Dev only when you are in a Pull Request
- Deploy to Staging only when you commit or merge into main
- Deploy to Production only after Staging, with an Approval

To do this, you would need first to __create three environments__, add the approvers to the Production one, then setup your Action Workflow like this:

```yaml
name: CI + CD

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

jobs:
  Build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - name: Compile
        run: echo Hello, world!
    
  DeployDev:
    name: Deploy to Dev 
    if: github.event_name == 'pull_request'
    needs: [Build]
    runs-on: ubuntu-latest
    environment: 
      name: Development
      url: 'http://dev.myapp.com'
    steps:
      - name: Deploy
        run: echo I am deploying! 
    
  DeployStaging:
    name: Deploy to Staging 
    if: github.event.ref == 'refs/heads/main'
    needs: [Build]
    runs-on: ubuntu-latest
    environment: 
      name: Staging
      url: 'http://test.myapp.com'
    steps:
      - name: Deploy
        run: echo I am deploying! 
            
  DeployProd:
    name: Deploy to Production 
    needs: [DeployStaging]
    runs-on: ubuntu-latest
    environment: 
      name: Production
      url: 'http://www.myapp.com'
    steps:
      - name: Deploy
        run: echo I am deploying! 
```

As you can see, everything revolves around the `environment` definition.

> Check [this section of the video](https://www.youtube.com/watch?v=w_37LDOy4sI&t=523s) for a more __in-depth demo and explanation__ about this example.

Is in cases like this one that the new __Visual Graph of GitHub Actions shines__

### Visualization

This new feature gives you a much better way to visualize __how your workflow is progressing__.

In the previous example, when you are coming from a Pull Request the workflow takes the _Deploy to Dev_ branch:

![PR flow](https://dev-to-uploads.s3.amazonaws.com/i/ocilynn1gwabiprr0b12.png)

As you can see, this is very clear from the new visualization, as well as it is clear that the __Staging + Production branch has been skipped__.

If instead we are committing into main, the other branch of the workflow is activated:

![Prod approval](https://dev-to-uploads.s3.amazonaws.com/i/yhh60ggt5ennpfzuv56w.png)

As you can see, it deploys to Staging and then __it waits for approval__ on Production.

And when an approver clicks on the _Review Deployment_ button, they have a chance to either __Reject__ or __Approve__ the deployment, and to leave a comment.

![Review](https://dev-to-uploads.s3.amazonaws.com/i/39he7r5ppkzqujvstz68.png)

Super easy to setup and manage.

And as you can see, it also shows the __deployment url__ on the environment box for easy access to your application. This comes from the `url` param previously defined in the `environment` section for that deployment.

> Watch the visualization [demo and explanation here](https://www.youtube.com/watch?v=w_37LDOy4sI&t=570s)

### Tracking and Auditing

__Everything that happens in an environment is audited__. In fact, Environments track the history of your deployments. And so you have the ability to see exactly what has been deployed to a specific environment (and that will soon include also work items, issues, and so on), who did it and when.

In fact, you if you to the _Code_ page on your repo, the main page, and scroll down you will find the __environments list__ on the right column:

![Environments list](https://dev-to-uploads.s3.amazonaws.com/i/os94dwj2c00srdyk5q0u.png)

If you click on a single environment you will see the __Activity Log__ for that specific environment, while if you click on the section title you will have __comprehensive status__ of all the environments.

![Tracking](https://dev-to-uploads.s3.amazonaws.com/i/akjnc4px42rabcfty5b4.png)

Here you can see two main things.

On the top part you have the __status of each environment__ which includes the last deployment, together with the branch and commit deployed. The _view deployment_ button will take you to the `url` that has been previously defined in the `environment` section for that deployment. This is __super useful__ because you can see immediately what you have deployed in that moment in each and every environment.

On the bottom, instead, you have the __activity log__ for all environments, including approved and rejected deployments, and of course that can be filtered by environment as well.

> Once again, I'd recommend you to [take a look at the demo of this here](https://www.youtube.com/watch?v=w_37LDOy4sI&t=692s) for a more comprehensive explanation.

### Conclusion

Alright, that's it for today.

Let me know in the comment section below what you think about these new features, if you'd like to have something different, and if you plan to use them in your projects.

I'd appreciate if you would take a look at the video about this (you can find it on YouTube at this link: [https://youtu.be/w_37LDOy4sI](https://youtu.be/w_37LDOy4sI)), leave a like and perhaps subscribe to my channel. It is about DevOps, especially with GitHub and Azure DevOps.
