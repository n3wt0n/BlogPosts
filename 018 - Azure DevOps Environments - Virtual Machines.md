Azure Pipelines is a great tool for doing Continuous Integration and Continuous Deployment and thanks to Multi Stage Pipelines we can finally have build, test, and release directly expressed in source code.

Recently they have also introduced the concept of "Environments", which belongs to the release process.

In the previous articles of this series we've looked at the Environments in general, and then we've gone deeper into it and explored the integration between environments and Kubernetes clusters.

Today, instead, we will focus on how we can connect our __Virtual Machines__ to Azure DevOps environments and take advantage of it. _Because we all know that among all the fun and cooler stuff, Virtual Machines are here to stay._

### Video

This time I do not have the _written version of the explanation_, because it is just much better to see this in action.

In this video I will show you first how to set everything up, and then what advantags we have in using Environments with VMs.

Enjoy the watch!

{% youtube zBr7cl6ASMQ %}

### Conclusion

Alright, this is how to use the Azure DevOps Environments with Virtual Machines and how amazing and usefult it is working this way.

As you've seen, super easy to set up and it generates the setup script for you. And remember, the PAT used expires after 3 hours, so you'd have to generate the script again if you haven't used it yet.

And the reolling deployment is super useful!

Let me know in the comment section below what do you think and how you deploy to your VMs.