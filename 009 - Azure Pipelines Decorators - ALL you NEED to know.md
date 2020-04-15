In Azure DevOps, Pipelines Decorators allow you to execute a series of predefined steps for your CI/CD workflows in your organization. They are essentially a section of the YAML file that will be executed for every pipeline.

Let's see what they are, how they work, hot to build and publish them and how to use them.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, and of course the end to end examples of Pipelines Decorators

{% youtube 1l-UAjdrSsM %}

If you rather prefer reading, well... let's just continue :) 

### About Azure Pipelines

I think we all know Azure Pipelines, the service in Azure DevOps that you can use to automatically build, test and deploy your applications. It works with just about any language or project type.

We can categorize the Pipelines in 2 main categories: 
- Build (or CI)
- Release (or CD).

And also remember that they come in 2 different flavors. We have the __Classic Pipelines__, the one you create and manage using the visual editor, and the __YAML Pipelines__, the proper name would be _Multistage pipelines_, that you create and manage using YAML files.

This distinction will be important in a moment.

To work in pipelines, you just create Job and add a series of Tasks to it for all the operations you want to perform. 

You want to build your Java application? Add the build task. 
Test your dotnet core project? Add the dotnet test task.
Scan your code for vulnerabilities? Add one of the many first and third party tasks.
Deploy your microservices to Kubernetes? Add the specific task.
And so on.

But what if you want all of your pipelines to mandatory execute some tasks, withouth anyone being able to "skip" them?

Pipelines Decorators are the answer.

### Pipelines Decorators

In fact, Pipelines Decorators allow for adding steps to the beginning and/or end of every job. This is different than adding steps to a single definition because it applies to __all pipelines in an organization__.

The tasks defined in a Pipeline Decorators are automatically injected to all your pipelines, and of course you can control that with some conditions.

Since there are 2 main kinds of Pipelines, as we have seen before, there are also 2 types of Pipelines Decorators: 
- Build Decorators
- Release Decorators

The _Build Decorators_ apply to Classic Build Pipelines and to the newer YAML Mulstistage Pipelines.

The _Release Decorators_, instead, apply ONLY to the Classic Release Pipelines.

Easy, right? But, wait a minute...

YAML Pipelines can be used for deployment as well, so how does this work?

Well, actually ___the "Build" Pipeline decorator type applies to the Deployment Jobs of the YAML Pipelines as well___.

I know, this is a bit confusing, but the reason for that is that the YAML Pipelines evolved from the Classic Build ones and therefore they share the same extensibility point.

So, out of the box, when you create a Build Pipeline Decorator it will apply to both the Normal Jobs, which are usually used for CI, as well as the Deployment Jobs. You can change that behaviour using some conditionals, and I will show you in a minute how we can do that.

Another thing you need to decide, when creating your Decorator, is when its tasks have to be injected into the Pipelines.  
You can have it injected at the beginning of the Pipeline, before all the other tasks. Or at the end of it, after all the other tasks. Or even both before and after all the tasks. It is up to you.

### But how can we create a Pipeline Decorator?

Decorators depends on 2 main files.  
The main file is a __YAML file__, where you actually write your tasks like in a normal YAML Pipeline.

The second file is a __JSON file__ that contains all the properties and specifications for your Decorator, like what it targets (Build or Release) and when to inject the tasks.

Decorators use the normal Azure DevOps extensibility points, which means you need to package them as Extensions.

After that, you have to upload this extension into the Marketplace and share it with your Azure DevOps organization. Remember that only private extensions can contain Decorators.

Finally you will have to install the Extension in your organization and, when completed, the Decorators will automatically be injected in all your Pipelines.

### Some Examples

This is the GitHub repo I created for showing how Decorators work. 
I have some basic examples there as well as some more advanced ones. Take a look at it to better understand how to create and use a Decorator.

{% github n3wt0n/AzurePipelinesDecoratorSamples %}

As I mentioned before we have the Build Decorators and the Release Decorators, and for each we can have Pre, Post, and Pre and Post decorators.

As you can imagine, the Pre ones injects at the beginning of the Pipeline while the Post ones at the end.

Each decorator has a _YAML file_ where we define the tasks to be injected, and a _JSON file_ here that contains the manifest of the Decorator.

We also have the _package.json_ and the _package-lock.json_ for each of them because as I've mentioned we need to package the Decorator into an Azure DevOps extension, and that relies on some Node.js components.

Take a look at the video at the top of this post ([here for simpler reference](https://youtu.be/1l-UAjdrSsM)) to see those examples more in depth.

### References and Links

- [Github repo with all the examples](https://github.com/n3wt0n/AzurePipelinesDecoratorSamples)
- Official Documentation about Azure Pipelines Decorators:
  - [Basic](https://docs.microsoft.com/en-us/azure/devops/extend/develop/add-pipeline-decorator?view=azure-devops)
  - [Advanced](https://docs.microsoft.com/en-us/azure/devops/extend/develop/pipeline-decorator-context?view=azure-devops)
- [Video with all the explanation and examples](https://youtu.be/1l-UAjdrSsM)