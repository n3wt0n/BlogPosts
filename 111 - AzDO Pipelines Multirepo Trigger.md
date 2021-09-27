Did you know you can specify multiple repositories in one Azure DevOps YAML Pipeline and cause it to trigger by updates to any of the repositories? Let me show you how

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube XXX %}

[Link to the video: XXX](XXX)

If you rather prefer reading, well... let's just continue :)

### Step 1: Basic Pipeline

Let's start from a very simple pipeline definition:

```yaml
trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- checkout: self

- script: dir $(Build.SourcesDirectory)
```

Nothing much to see here, just a pipeline that uses it's own repo and prints out the content after checkout

### Step 2: Add More Repos

Let's now make it a little more interesting, adding some additional repos to it. We will use the `resources` section for it.

```yaml
resources:
  repositories:
  - repository: tools
    type: git
    name: MyProject/tools
    ref: main
```

In this case we are adding a repository named ___tools___ that belongs to the Azure DevOps Project ___MyProject___ and we tell Azure Pipelines to "consider" the branch ___main___ (_I'll explain in a moment what I mean by that_) and to use ___tools___ as reference name for it.

We can also __reference a GitHub repository__:

```yaml
  - repository: MyGitHubRepo
    type: github
    endpoint: MyGitHubServiceConnection
    name: MyGitHubOrgOrUser/MyGitHubRepo
    ref: releases/123
```

Pretty similar to the other example, but to connect to GitHub we had to specify the __service connection__ name (in the _endpoint_ parameter). Note that here the ___reference name___ is _MyGitRepo_

Finally, we can also add repositories in __another Azure DevOps Organization__, in a similar way:

```yaml
  - repository: MyOtherAzureReposGitRepository 
    endpoint: OtherOrgAzureReposGitServiceConnection
    type: git
    name: OtherProject/MyAzureReposGitRepo
```

We need to use the __service connection__ as well, because we are going to connect to another organization. Note that in this case we haven't specified the branch (which is indeed optional).

### Step 3: The Triggers

At this point we have all our repositories referenced in the workflow, but the pipeline still triggers only on the local repo:

```yaml
trigger:
- main
```

If we want it to be triggered also from another repo, we can add a trigger section to the repository definition:

```yaml
  - repository: tools
    type: git
    name: MyProject/tools
    ref: main
    trigger:
    - dev
    - release
```

For example, with the above snippet our pipeline will be triggered every time a change occurs in wither the _dev_ or the _release_ branches of our _tools_ repo.

What about the _main_ branch specified above too, you ask? well, that is not for the triggers... (_I know, confusing... keep reading and you'll know ;)_ )

> At the time of writing, triggers work only for additional repositories in Azure DevOps, in the same organization where the Pipeline is defined. GitHub repos and other repos defined as resources cannot be used for triggering.

### Step 4: Using The Code

We now have our pipelines that is triggered by multiple repos. It's very likely that you would want to also use the code for those additional repos, right?

```yaml
- checkout: MyGitHubRepo
- checkout: tools
- checkout: MyOtherAzureReposGitRepository
```

Just add the checkout then. As you can see, we use the _reference name_ we've specified in the resources section to let the `checkout` step know what we want it to do.

And here is finally where the branch in the `ref` parameter comes into play, because it is __the branch that will be checked out__:

| Repo | Branch Checkout |
| -- | -- | -- |
| self | _default branch_ |
| tools | main |
| MyGitRepo | releases/123 |
| MyAzureReposGitRepo | _default branch_ |

> If you don't specify a path in the checkout step, Azure Pipelines will use the name of the repository to create the folder, not the repository value which is used to reference the repository in the checkout step.

### All Together

With all we have added, our pipeline will now look like this:

```yaml
resources:
  repositories:
  - repository: tools
    type: git
    name: MyProject/tools
    ref: main
    trigger:
    - main
    - release

  - repository: MyGitHubRepo
    type: github
    endpoint: MyGitHubServiceConnection
    name: MyGitHubOrgOrUser/MyGitHubRepo
    ref: releases/123
    
  - repository: MyOtherAzureReposGitRepository 
    endpoint: OtherOrgAzureReposGitServiceConnection
    type: git
    name: OtherProject/MyAzureReposGitRepo

trigger:
- main

pool:
  vmImage: 'ubuntu-latest'

steps:
- checkout: self
- checkout: MyGitHubRepo
- checkout: tools
- checkout: MyOtherAzureReposGitRepository

- script: dir $(Build.SourcesDirectory)
```

You can try it out and you'll see (thanks to the last step) that all the code from the 4 repos is there for you to be used 

### Conclusions

This feature is useful, for example, if you want to __consume a tool or a library__ from a different repository and you want to run tests for your application whenever the tool or library is updated.

It is also good if you keep your __YAML file in a separate repository__ from the application code and you want to trigger the pipeline every time an update is pushed to the application repository.

Let me know in the comment section below how you think this feature can relate to your processes.

Also, checkout [this video](https://youtu.be/hJsMq35KAMk), where I talk about how to Run a job next in Azure Pipelines

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

{% youtube XXX %}