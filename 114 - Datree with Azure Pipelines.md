In this third article dedicated to ___Datree___ we will explore how to use the tool with Azure Pipelines to validate and secure our Kubernetes deployments.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube aM7EVflmEt4 %}

[Link to the video: https://youtu.be/aM7EVflmEt4](https://youtu.be/aM7EVflmEt4). The part about ___Azure Pipelines___ starts at minute [16:33](https://youtu.be/aM7EVflmEt4?t=993)

If you rather prefer reading, well... let's just continue :)

### The Basics

While I will not cover how to install and use the service in general (_check the video and the first article of this series if you want to know more about it_), there are few things worth remembering and that will be useful later on in this article:

- Datree is a __CLI__ tool, which works on Linux, MacOS and Windows
- The Centralized Policy Management uses a __Token__ as _connection_ between the scans and the account

### Datree in Azure Pipelines

Alright, let's do this. First thing we have to do, as we would in a local environment, is to __install the CLI__

```yaml
- script: curl https://get.datree.io | /bin/bash
  displayName: 'Install Datree'
```

In this case the pipeline is running on Linux, so I can use the bash script for installing it.

This step will take only few seconds to execute.

> This is necessary if you are using the _Microsoft Hosted Agents_. If you are instead on _Self-hosted Agents_ you can install the CLI directly on the agent machine so you can skip this step. However, you'd need to manually take care of updating the CLI

Next, we can __invoke the validation__ command:

```yaml
- script: datree test ~/.datree/k8s-demo.yaml
  env:
    DATREE_TOKEN: $(DATREE_TOKEN)
  displayName: 'Run the datree scan'
```

As you can see, nothing different from what we would normally do.

Since we don't have access to the config file in our CI environment, we need to __pass the Token as environment variable__. Best practice is to save it as a protected variable in Pipelines, and retrieve it using `$(YOUR_SECRET_NAME)`

> In the example above the Token is passed as environment variable directly in the task to minimize exposure. If you have multiple scans in the same workflow, you can also add it as job, stage, or pipeline environment variable.

And this is basically all you need.

So the __full pipeline__ will look like this:

```yaml
# Pipeline to show Datree scan

trigger:
  - main

pool:
  vmImage: ubuntu-latest

steps:
- script: curl https://get.datree.io | /bin/bash
  displayName: 'Install Datree'

- script: datree test ~/.datree/k8s-demo.yaml
  env:
    DATREE_TOKEN: $(DATREE_TOKEN)
  displayName: 'Run the datree scan'

```

Of course you can also integrate this into your own CI or PR validation pipelines rather than keeping it separate if you wish so.

### Execution and Results

First thing to notice is that, as Ive said before, the __installation step is very quick__.

![Installation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jln3krt0kink37mfs8ye.png)

This is why it is probably a good idea to leave it there even on Self-hosted agents so you don't have to worry about updating it.

![Execution](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ju4vviy66ne9uiupxmt2.png)

And the validation scan is also very quick.

Second thing to notice is that by design __if a validation fails it will break the build/run__. This is to ensure the enforcement of the policies and best practices.

Finally, let's take a look at the results.

![Results](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nt7fy319ele9srkhlkqv.png)

As you can see, the __output is exactly the same__ as when executing the CLI on any local environment, or anywhere else for what batters, keeping the experience very consistent.

### Offer

__Datree is free__ to use up to 1000 scans per month, and you can pay for more scans and enhanced support. However...

![A Month for Free](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d21dd4pybgm67x8js18f.png)

___You can get 1 month of the Premium plan for FREE is you use this link___: [https://app.datree.io/?utm_source=coder-dave&medium=youtube](https://app.datree.io/?utm_source=coder-dave&medium=youtube)

### Conclusions

So, what do you think about Datree? Is it something you will adopt as part of your workflow? Let me know in the comment section below, I'd really like to know it.

You may also want to watch [this video](https://youtu.be/4Oa5HneTuKs) in which show you how to deploy to Kubernetes in Azure Pipelines starting from scratch.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
📧 [Newsletter](https://coderdave.io/newsletter)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube aM7EVflmEt4 %}