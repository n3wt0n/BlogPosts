When you use containers for your application, one of the things you need to think about is how to move (aka promote) the container images you generate across different environments.

In this series, I will explore different ways to do so... with the help of __Azure DevOps__

### Intro

In this article, the first of the series, we will explore the simplest and most used  way (at least in my experience) to promote a Container image across different environments.

We will use a non-environment-specific registry as a base repo, and we will push the image to this registry during the _build_ phase. Then, we will take the image and push it to some environment-specific registries in the _release_ phases as we move forward.

### The Build

As step "zero", we want to create our container image with all we need for our application to function properly. I will not focus on the image creation at this time.

> There are two ways to "install" your code onto a container image: a multi-step Dockerfile which compiles your code AND create the image, or compiling the application outside the container and then simply install it into the image.

> While the first approach ensures (in theory) even more immutability, the build process is often way less verbose and more difficult to tune.

> I personally prefer using the CI capabilities of Azure DevOps to build the application and then create the image with the result. Let me know if you are interested in this approach so I can write another post about it.

Whatever your approach is, you will at the end have your container image created.

Now what?

As I've mentioned before, we need to __push it to an environment-neutral container registry__. Even tho we could do this in the release process as well, I normally consider this as part of the build, simply because you want your build process to give you something usable. In our case, usable means having the image ready to be processed, therefore we'd need to have it in the registry.

![Build pipeline](https://thepracticaldev.s3.amazonaws.com/i/dep497a2ddeemmmx4t4z.png)

As you can see, I simply create the image and then I push it to the registry.  
Actually Azure DevOps has a task that can combine both operation, called __buildAndPush__, but for clarity I prefer keeping the two commands separated.

### Let's Release

Ok, now we have our container image, and we have pushed it to the general container registry.

The temptation here would be to pull the image from that very registry and ship it to our server. NO, we won't do that. Instead, we are going to create a __Release Pipeline__ which will use the container registry as input.

![Artifact](https://thepracticaldev.s3.amazonaws.com/i/1x104e0relbanj459d49.png)

To do so, simply click on the "_Add an artifact_" button (after creating a new release pipeline), and select "_Azure Container Registry_" (or _Docker Hub_, if you want to use that). Just few parameters to set, and you're ready to go.  
Also, be sure to enable the __Continuous Delivery__ flag so this release pipeline can run every time a new container image is pushed to the registry.

![Push it](https://thepracticaldev.s3.amazonaws.com/i/af5m9slc1kafln26ust7.png)

Now, let's talk about the next steps. Let's say you have three different environments: Dev, Test, and Prod. First thing to do is to create three _Stages_ in the Pipeline.

![Stages](https://thepracticaldev.s3.amazonaws.com/i/87nkrz8pkgd3pvuiu4nz.png)

Then let's edit the _Dev_ stage. We need to:

* Pull the image from the generic registry
* Change it's name so it can be pushed to the Dev registry
* Push it to the Dev registry

![The 3 steps](https://thepracticaldev.s3.amazonaws.com/i/2tjyxwqapq24ztdm0anx.png)

To __pull__ the image from the generic container registry we need to do a little trick. The _pull_ command, in fact, is not directly embedded in the v2 of the Docker task.

![Pull the image from the Base Container](https://thepracticaldev.s3.amazonaws.com/i/7y4v2oul9amixeu0vaur.png)

So we need to manually type _pull_ as command name, and insert the registry name and the image name in the arguments box.  
I have defined variables for the names so I can reuse them across the different environments.

Next we need to __tag__ the image differently, to change the name of the registry. This is because if you have to push an image to a certain registry, you need the image full name as "_registryName/ImageName_", where _registryName_ is the full qualified domain in case of anything different from Docker Hub (for Azure Container Registry, it would be something like _myregistryname.azurecr.io_

![Tag with new registry](https://thepracticaldev.s3.amazonaws.com/i/bwbhgd279m0eaxkftyah.png)

Again, the _tag_ command is not embedded in the v2 of the task so we need to use the arguments box. The use of variables is optional but I recommend it, it just makes everything easier to automate and templatize.

Last step, we need to push the image to the new registry.

![And push it](https://thepracticaldev.s3.amazonaws.com/i/f4mekboh3z8lile7vuly.png)

This time, the _push_ command is fully supported so no need for the custom arguments!

And we are done for Dev! 

Now we can replicate the same process to the other environments, just changing the source and target registries.

Ideally when pushing to the environment-specific registry you should have a mechanism to notify your target host service (App Service, AKS, Container Instances, etc) of the new image so the deployment can be executed.

And of course you probably want to set some _Release Gates_ or _Approvals_ for deploying to Test and Prod.

### Conclusion

This process is probably the most used, however it is not my favorite.  
First of all, you need more registries than environments.  
Second, and probably more important, __it doesn't ensure 1:1 mapping between build and release__. And this means that __the image you build and the one you deploy might not be the same__.

If someone does any change to the images in the _generic registry_, then you will in fact end up having deployed a different version than the one your CI pipeline generated.

Another issue here is that you __cannot directly reference the Build number__, or any other parameter that comes from the Build, because you CI and your CD pipelines are not directly related. This may not be a problem for everyone, but I like to version my images using the BuildId. So this won't work for me.

This is why in the next article of the series we will explore another approach, using the Build Artifact capabilities of Azure DevOps to get a fully immutable image to be promoted across environments.

Stay tuned!