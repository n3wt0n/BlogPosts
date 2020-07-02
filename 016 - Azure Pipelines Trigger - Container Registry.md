As you probably know, Azure Pipelines supports __many types of triggers__, and sometimes it may be a little confusing. 

This is why I've decided to create this mini-series dedicated to Triggers. And today we are going to talk about the __Container Registry trigger__, which allows to you run a Pipeline every time a new container image is pushed to __Azure Container Registry__ and __Docker Hub__.

### Classic vs YAML

I'll focus first on the __Classic__ Release Pipelines, using the UI, because setting up the trigger is easier and it supports both the _Azure Container Registry_ and _Docker Hub_.

For the Multistage __YAML__ Pipelines, instead, we can achieve ___almost the same___ using the YAML triggers, but the trigger is currently available only if you're using Azure Container Registry. It is not available for Docker Hub. But stay with me until the end because ___I have a workaround for you for triggering from Docker Hub___.

To be able to trigger a Pipeline run whenever a new container image is pushed to your registry, we need to use a Resource. If you are not familiar with Resources, they are basically anything used by a pipeline that lives outside the pipeline.

Those can be other pipelines, repositories, packages and of course containers images.

### The Video

Enjoy the watch!

{% youtube FHnPJ8FBjLM %}

### Conclusion

I think that this is pretty cool, especially now that a lot of developers have their applications containerized.

And being able to trigger also from Docker Hub, as I've shown, it is pretty handy.

What do you think? How do you trigger your deployments of container images?

### References and Links

- [Video on Pipelines Environments](https://youtu.be/gN4j65w7wIM)
- [Video on Pipelines Environments for Kubernetes](https://youtu.be/qBO5-xINmSs)