If like many other people you are confused about the below settings of the Classic Release Pipelines in Azure DevOps, look no further. Today we are going to clarify this ___once and for all___.

![Setting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4jo3pm5q9dm5kve17ha2.png)

In this article I'm going to cover these __5 infamous confusing settings__ of Azure Pipelines:

- Report deployment status to the repository host
- Report deployment status to Work
- Report deployment status to Boards
- Report deployment status to Jira
- Enable the deployment status badge

Today's topic has been highly requested through the comments on my videos and posts, and on some of the social media platforms I'm in. And by the way if you are not following me, go below and check the __links to my platforms__.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube EHbPpQNoBvI %}

[Link to the video: https://youtu.be/EHbPpQNoBvI](https://youtu.be/EHbPpQNoBvI)

If you rather prefer reading, well... let's just continue :)

### Where?

First off, let's see where to find them.

Just go to your _Classic Release Pipelines_, and open a Pipeline.

Click on _Edit_, then _Options_, and finally _Integrations_. And here you have those 5 infamous options.

Ok, with that out of the way, let's go deep now in every single setting.

### Report deployment status to the repository host

If your sources are in an Azure Repos Git repository in your project, this option displays a badge on the Azure Repos pages. 

![Report deployment status to the repository host](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zweiehthn448sgrwcvub.png)

The badge indicates where the specific commit got deployed and whether the deployment is passing or failing.

![Badge Details](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/eiqyig80mr4ghz7dfq5x.png)

This as you can imagine can be helpful to have a snapshot of your deployment status directly in the repo.

> Watch the [video here](https://youtu.be/EHbPpQNoBvI) for a __full demo__ of this setting (starts at minute [1:41](https://youtu.be/EHbPpQNoBvI?t=101))

Let's see the next two options, which are probably the most confusing ones because at a first glance they seem to be basically the same. But, in fact, they are fairly different.

### Report deployment status to Work

The _Report deployment status to Work_ allows you link the Release runs (with the status) to your Work Items in the "Links" section:

![Report deployment status to Work](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j4wnb466rsuzcikffwmz.png)

It can be beneficial for reporting purposes, or if you export your Work Items in other formats. However, I would not recommend using this one (_see the next options_) because it doesn't offer an immediate visualization in the work item itself

> Watch the [video here](https://youtu.be/EHbPpQNoBvI) for a  __full demo__ of this setting (starts at minute [3:39](https://youtu.be/EHbPpQNoBvI?t=219))

### Report deployment status to Boards

This setting is similar to the previous one, but it offers a much better and clearer UI. In fact, Deployments are linked to the Work Items in the __Deployments Section__:

![Report deployment status to Boards](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kh0pie7afe742y6max10.png)

Not only, clicking on each deployment box you can gather __more information__ on the deployment itself.

When you enable this option, you'd have to map your custom deployment stages to predefined ones (Development, Staging, Test, Production, Unmapped).

> Watch the [video here](https://youtu.be/EHbPpQNoBvI) for a  __full demo__ of this setting (starts at minute [5:46](https://youtu.be/EHbPpQNoBvI?t=346))

Hope the difference between those 2 options is clearer now. I think both can be useful, depending on your work style.

### Report deployment status to Jira

Finally, let's check the remaining 2 options.

This _Report deployment status to Jira_ option is similar to the previous one, and in fact the same mapping applies. However, as the name says, the link is done with cards in Jira rather than with work items in Azure Boards

> Watch the [video here](https://youtu.be/EHbPpQNoBvI) for a  __full demo__ of this setting (starts at minute [8:29](https://youtu.be/EHbPpQNoBvI?t=509))

### Enable the deployment status badge

Finally, the easier one. What this setting does is providing a link for each Release stage selected.

![Enable the deployment status badge](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5rr48zlkff9t4v26tb6a.png)

Each link, in return, represents a badge like this one which can be added to your Readme.md files in GitHub, a website or basically anywhere you want to have a visualization of the status of your deployment:

![Badge](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/an1pv60v3bh4avs0g89x.png)

> Watch the [video here](https://youtu.be/EHbPpQNoBvI) for a  __full demo__ of this setting (starts at minute [9:13](https://youtu.be/EHbPpQNoBvI?t=553))

### Conclusions

Now the Release Pipelines in Azure DevOps don't have secrets for us... well there's actually more to cover, but I will leave that to another post/video.

Let me know in the comment section below if this explanation was good, and if you have now a better understanding of the platform.

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

{% youtube EHbPpQNoBvI %}