In this post I'm going to show you how to disable a repository in Azure DevOps and prevent users from accessing its contents.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube G_um1mm7LiM %}

[Link to the video: https://youtu.be/G_um1mm7LiM](https://youtu.be/G_um1mm7LiM)

If you rather prefer reading, well... let's just continue :)

### Why Disabling Repos?

Before we talk about how to disable a repo, why would you want to do it?

Well, for example you may want to disable a repository because you found a secret in it. Or a third-party scanning tool found the repository to be out of compliance.

In such cases, you may want to temporarily disable the repository while you work to resolve the issue.

### How to Disable a Repo in Azure DevOps

Let's see now how to disable a repo. It is very easy.

Just go to the `Project Settings`, scroll down to the `Repositories` section and enter it, then click on the specific repo you want to Disable. In the settings, you have the `Disable Repo` switch

![Disable a Repo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h6jn7q4mtcrydlfl29z0.png)

When a repo is disabled, it still shows up in the list of repos, however no one can access or update its content.

And you would also see a message saying that the repo has been disabled when they try to access it in the Azure Repos UI.

![Disabled Message](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u8kwc99oklp2828z7090.png)

And of course after the necessary mitigation steps have been taken, disabled repositories can be re-enabled using the same setting.

> Final note: you can disable a repository only if you are either admin or owner, or you have the Delete repository permissions.

### Conclusions

Let me know in the comment section below if you think this is useful and if you've ever been in a situation in which you could have disabled a repo.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube G_um1mm7LiM %}