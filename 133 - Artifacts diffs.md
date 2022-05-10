What are the differences between __Build Artifacts__ and __Pipelines Artifacts__ in Azure Pipelines, and how do they compare to __Azure Artifact__?

With Azure DevOps using similar names for different things, there is quite some confusion between them. And in fact I’ve received many comments and questions about them on my videos about Azure Pipelines... but today we are going to answer these questions once and for all. Let’s dive into it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube WWCmEUCt3Cc %}

[Link to the video: https://youtu.be/WWCmEUCt3Cc](https://youtu.be/WWCmEUCt3Cc)

If you rather prefer reading, well... let's just continue :)

### A Word About Artifacts

So, what are the differences? We will go through them one by one, see what they are used for, and at the end we’ll have a quick recap and some recommendations on what to use when. But first, we need to understand what an artifact is, at least in the context of Azure DevOps.

Using a simplification, an artifact is __any kind of file__ or files that your build produces, or that you may want to reuse in another build, another job of your build, or a deployment or release pipeline.

For example, the compiled DLLs that you have as result of your CI can be stored in an artifact to be then deployed by another job. Same thing for the _dist_ folder of a Node.js application. Or, let’s suppose you want to save some output of one of your pipeline task to then download it and review it later... well, you can package that in an artifact as well. 

Now that we know what artifacts are, let’s see how they differ. 

### Build Artifacts

Build Artifacts have been in Azure DevOps for a long time and are the __built-in artifact storage mechanism__ for Azure Pipelines. 

They can be used in both the Classic Build Pipelines, the one created using the UI, as well as the newer YAML Pipelines.

[IMAGE 01]

Build Artifacts are published via the `Publish Build Artifacts` task and can be downloaded with the `Download Build Artifact` task. And when you publish them, you can instruct the task to either push the content up to the Azure DevOps cloud or serve, or to copy the files to a local file share instead.

Build Artifacts can be consumed from other jobs in the same Pipeline, and from other Pipelines.

[IMAGE 02]

Additionally, Build Pipelines can be used if you want to consume your artifact from a Release Pipeline triggered by the build completion.

And you can always download your artifacts from the Build run status page.

[IMAGE 03]

And as you can see in the image above, you can explore the content of your artifact directly in the UI.

### Pipeline Artifacts

Alright, let’s talk about **Pipelines Artifacts** now.

These are the __newer version__, if you will, of Build Artifacts, and as such they can be used only from within the YAML Pipelines.

One of the main benefits of Pipeline Artifacts is that they can __dramatically reduce the time__ it takes to upload and download the artifacts because of the way the files are both uploaded and stored. And this is especially true for large artifacts.

Until fairly recently, Pipelines Artifacts couldn’t be used in Classic Release Pipelines, or from other Pipelines, but now that limitation is gone so their usage is very similar to Build Artifacts.

[IMAGE 04]

To publish the Pipelines Artifacts you can use the `Publish Pipeline Artifact` task and you can download them using the `Download Pipeline Artifact` task.

[IMAGE 05]

Alternatively, since this feature is only available in the YAML Pipelines, you can use the `publish` keyword and the `download` keyword, which are just the abbreviation for the whole tasks.

And if you publish a Pipeline Artifacts, and you want to use it in a deployment job in the same pipeline, you don’t even have to add the download task because Azure Pipelines will download them automatically.

### Build vs Pipeline Artifacts

There are few more differences in publishing and downloading the artifacts between Build and Pipeline Artifacts.

[IMAGE 06]

The publish tasks are virtually identical, with the only differences being that in the Publish Build Artifact task here on the left you can optionally choose to further include your artifact in a Tar file, while this is not present on the right on the Publish Pipeline Artifact Task. This one, instead, allows you to add some custom properties to the artifact. They must be in JSON format, all keys having the prefix `user-`

It gets more interesting if we look at the Download tasks

[IMAGE 07]

As you can see in this side by side view, when you download a a Build Artifact (on the left) you can choose if you want to download the whole thing, or just some specific file from the artifact. You can also set some parallelization settings and other parameters. When downloading a Pipeline Artifact, instead, you don’t have that option, as you can see here on the right hand side of the image.

And if we switch the task to download from a different pipeline or run, instead of from the current one, we have one more difference.

[IMAGE 08]

Aside from a different positioning of the fields, you can see that when you download a Pipeline Artifact you can choose to do so even if the pipeline run you are targeting has failed

And that basically covers everything there is to say about Build and Pipeline Artifacts. If you have noticed, I kept comparing the two... but I haven’t mentioned Azure Artifacts yet. Why? Well, because it is a __completely different thing__.

### What About Azure Artifacts?

So Azure Artifacts... as I was saying it is pretty different from Build and Pipeline Artifacts. Despite the similar name, it’s a __different service which serves a different purpose__.

Both Build and Pipeline Artifacts are very generic, you can save whatever you want in them, and what Azure DevOps does is just packaging the files in a zip archive and saving it somewhere. Azure Artifacts, instead, is a __typed package repository__.

[IMAGE 09]

It supports multiple package types such as NuGet, npm, Python, Maven, and Universal Packages... you can basically see it as an alternative to Artifactory, Nexus, GitHub Packages, and services like that.

You may have seen that Azure Artifacts also supports Universal Packages, and although that is somewhat similar to the other types of artifact we have seen before, it is conceptually different.

You would use Universal Packages when you want to create an artifact with a lifetime independent of the pipeline that created it. In fact both Build and Pipeline Artifacts are always tied to the Pipelines that created them. As we have seen, you can download Pipeline Artifacts after a pipeline has completed via the artifacts UI - but if you want something that really exists independent of pipeline you would go for Universal Packages.

Another big difference is about the pricing. Whether you use Build Artifacts or Pipeline Artifacts, you will not have to pay a single cent for them, no matter how many files you store or how big they are. Azure Artifacts, on the other hand, is billed by size.

[IMAGE 10]

You have a free grant of 2 Gb for each organization, but once you reach the maximum storage limit, you can no longer upload new artifacts and will need to either delete some of your existing artifacts, or [set up billing](https://docs.microsoft.com/en-us/azure/devops/organizations/billing/set-up-billing-for-your-organization-vs?view=azure-devops)  to increase your storage limit.

So, let’s recap and see my recommendations.

[BROLL 11]

Build Artifacts are the older type of artifacts and can be used in both Classic and YAML Pipelines. They are fairly slow to upload and download, they are tied to a specific Pipeline run and they can be used to trigger a deployment, via Release Pipelines.

Finally, Build Artifacts cannot be shared, you can use them for storing anything you want, and you don’t pay for the space you use.

Pipeline Artifacts, on the other hand, are newer and faster, but they can be used only in YAML Pipelines. They are also tied to a specific Pipeline run, they trigger CD in both Multistage Pipelines and Release Pipelines, and cannot be shared. Likewise, they can be used to store anything and they are free.

Finally, Azure Artifact is a completely different service. Packages stored in Azure Artifacts can be used in both Classic and YAML Pipeline, and their upload and download are as fast as with Pipelines Artifacts because they share the same underlying technology.

Being a different service, Azure Artifacts are independent from the Pipelines which have publish them, but like the other types can be used to trigger CD.

Finally, they are the only type of artifact that can be shared with developers even cross-organization, but they can be only typed packages and, last but not least, you get 2gb of space for free but after that it’s a paid service.

### Recommendations

How would I recommend you use the different types of artifacts?

Use __Build Artifacts__ only if you are using Classic Build Pipelines. There is really no other reason to use them, since they are the older and slower flavor of artifacts.

Use __Pipelines Artifacts__ if you are on YAML Pipelines, and you don’t need to share the result of your CI with other teams.

Finally, __Azure Artifacts__ enables developers to share their code efficiently and manage all their packages from one place. Use Azure Artifacts if you need to share packages within the same team, across organizations, or even publicly.

### Conclusions

Let me know in the comments below if you still have any more questions about Build Artifacts, Pipeline Artifacts, and Azure Artifacts and I will try my best to answer them.

Also, check out [this video](https://youtu.be/3cGtA__dKUc) with all you need to know about the differences between Classic Pipelines and YAML Pipelines.

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

{% youtube WWCmEUCt3Cc %}