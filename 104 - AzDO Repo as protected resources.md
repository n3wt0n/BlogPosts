In Azure DevOps, you can add __checks and pipeline permissions to your repository__, to have more control on what pipelines can and cannot do with your code.

And today I'm gonna show you how to do it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube a7k-mAjTbas %}

[Link to the video: https://youtu.be/a7k-mAjTbas](https://youtu.be/a7k-mAjTbas)

If you rather prefer reading, well... let's just continue :)

### Why Protect a Repo?

Today we talk about using Repos as protected resources in YAML Pipelines to have a more granular level of security on them.

So, first things first... why would you even want to use this feature? Let me give you an example.

It is fairly common having __multiple repositories in an Azure DevOps project__, for example to host many sub-projects, and each repository may have one or more pipelines. In this scenario, by default the Pipelines can __access the code on every and each repository__ in the Team project. You may want however to __control which pipelines can access which repositories__. 

![Repos Diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rggr2oisoutp0afbvsja.png)

For example, let's say you have two repositories A and B in the same project and two pipelines X and Y that normally build these repositories. 

![Access Diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8hw2b6a3hi2d99ydsbac.png)

You may want to prevent pipeline Y from accessing repository A. In general, you want the contributors of A to control which pipelines they want to provide access to.

As a contributor of repo A, you can add checks and pipeline permissions to your repository. Let's see how to do this.

### How To Do It

To access those settings, navigate to the ___Project Settings___, select __Repositories__, and then the repo you want to add checks to. 

![AApprovals and Checks menu](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/une84rrrvpzwio9liqu7.png)

You will notice a new menu called "__Approvals and Checks__" in the ellipses, where you can configure any of the approvals and checks like you have on Service Connections, Environments, etc.

![Checks](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i6mklxh1nihpzc1n4bx0.png)

And, Under the "___Security___" tab, you can manage the list of users, pipelines, and even branches and tags that can access the repository.

![Pipelines Permissions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3jh80q4cdd6kxrgq8tcw.png)

Anytime a YAML pipeline uses a repository, the Azure Pipelines infrastructure verifies and ensures that all the checks and permissions are satisfied.

> Remember that these permissions and checks are applicable __only to YAML pipelines__. Classic pipelines do not recognize these new features.

### Conclusions

Hope this was helpful, let me know in the comment section below if you have any question and what are your scenarios for using this feature.

Also, check out [this video here](https://youtu.be/G_um1mm7LiM), where I talk about How to disable a repository in Azure Repos and why you may do it.

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

{% youtube a7k-mAjTbas %}