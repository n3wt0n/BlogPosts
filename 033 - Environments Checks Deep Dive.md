After talking about Azure DevOps Environments in general and then looking into the specific implementations for Azure Virtual Machines and for Kubernetes Clusters, it is now time for a deep dive into Checks and Gates.

Let's take a look at all the Checks and Gates available in an Azure DevOps Environments and see how we can use them for deployment control!

### Intro

I want tp talk about all the Gates and Checks available in Azure DevOps Environments for __controlling the release process__. 

This post is part of the series dedicated to the Azure DevOps Environments, series in which I've already covered the Pipelines environments in general, as well as the specific implementations for Virtual Machines and Kubernetes cluster.

Today instead we will go through __all the Checks__ that we can configure inside an Environment (_at least all the ones available at the time of writing_) and we'll see how we can use them to orchestrate our deployments.

### The Checks

There are currently __9 different types of check__ available in Azure Pipelines Environments:

![Checks](https://dev-to-uploads.s3.amazonaws.com/i/7kce5mqkfzj0gtdnr5ts.png)

To enable a check, we need to go in an Environment and click on "_Approvals and Checks_" on the ellipses menu on the upper right

### The Video

Right, let's jump now into Azure DevOps and analyze all the checks, how to use them, and what benefits they provide.

Enjoy the watch!

{% youtube FbXKpo6oEyg  %}

([Link to the video: https://youtu.be/FbXKpo6oEyg](https://youtu.be/FbXKpo6oEyg))

### Few Notes

#### Approvals

This is probably the most used one. Just add the people or group you want to ask approval for a specific stage, and they will receive the notification.

🔮▶ [Demo about Approvals](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=126s).

#### Branch control

The check requires the __branch names to be fully qualified__. Make sure the format for branch name is `ref/heads/<branch name>`

🔮▶ [Demo about Branch control](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=246s).

#### Business Hours

I've cover this previously in  [this other video](https://youtu.be/MjkmKeEGOyc). This check basically allows you to define __deployment windows__ and so your stages will run only during those windows.

🔮▶ [Demo about Business Hours](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=347s).

#### Evaluate artifact

With this check you can evaluate artifact(s) to be deployed to an environment against custom policies.  
Remember that currently this works only with _container image artifacts_.

🔮▶ [Demo about Evaluate artifact](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=446s).

When you run a pipeline, as usual the execution of that run pauses before entering a stage that uses the environment and the specified policy is evaluated against the available image metadata.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/dpj12puyeoe5lxfj9ho1.png)

The check passes when all the policies are successfully evaluated against the artifact

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/hhzu7mln9cq95btjvdid.png)

You can also see the complete logs of the policy checks from the pipeline view.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/ns6ywpeopz8lwt7u5bj0.png)

If any of the policy fails, instead, the whole check fails and the stage is marked failed as well.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/xjkqqofie5r98qnwzkqa.png)

Again, you can also see the complete logs of the policy checks and the ones which failed from the pipeline view. 

#### Exclusive Lock

This is pretty interesting.

You can ensure that only a __single run deploys__ to an environment at a time. By choosing the "Exclusive lock" check on an environment, only one run will proceed. Subsequent runs which want to deploy to that environment will be paused. Once the run with the exclusive lock completes, the latest run will proceed. __Any intermediate runs will be canceled__.

🔮▶ [Demo about Exclusive Lock](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=613s).

#### Invoke Azure Functions 

In case the Azure Function executes for more than 1 minute, you'll need to use the Callback completion event instead of the API Response one. API Response completion option is supported for requests that complete __within 60 seconds__.

🔮▶ [Demo about Invoke Azure Functions](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=668s).

#### Invoke REST API

This is very similar to the previous one, with the difference that the URL and the authentication is defined in the __Service Connection__ rather than in the check itself.

🔮▶ [Demo about Invoke REST API](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=887s).

#### Query Azure Monitor alerts

I want to spend a moment talking about this one because I think the documentation is a little misleading.

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/cmibym9bd87hpa7l59i9.png)

If we read the part here highlighted in yellow, in fact, it says that  "_Query Azure Monitor Alerts helps you observe Azure Monitor and ensure no alerts are raised for the application __AFTER A DEPLOYMENT__ _"

Reading this may lead you to think that this check is executed _AFTER_ the stage runs, while in reality __it is still a PRE-Deployment check__.

What you can do for being sure the application you have just deployed is working correctly is then deploying it in a stage, and then add another stage which just target the environment that contains this check. Not super streamlined, but it works.

🔮▶ [Demo about Query Azure Monitor alerts](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=990s).

#### Required template

With this check, you can enforce pipelines to __use a specific YAML template__. When this check is in place, a pipeline will fail if it doesn't extend from the referenced template.

🔮▶ [Demo about Required template](https://www.youtube.com/watch?v=FbXKpo6oEyg&t=1128s).

### Conclusion

We now have a quite good understanding of how we can control our deployments with Azure Pipelines and the checks embedded into Environments.

Let me know in the comment section below if you have any questions about them.