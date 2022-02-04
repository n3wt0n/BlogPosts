Do you want to protect your GitHub Actions so they are not public?

GitHub has finally released a new feature that allows __sharing custom GitHub Actions privately__ only within an organization. You don’t need to have them in a public repo anymore.

Let’s see how!

### The Problem

As you probably know, until now when you created a custom GitHub Action you had to store them in a __Public Repo__ to be able to use them.

![Public Repo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d8t6btvau99019ppi2sr.png)

This means that __anybody on the internet__ could see your Actions and use or copy them. And while this is not necessarily a problem, and in fact promotes Open Source, it is a limitation in the cases in which you or your company has some kind of IP in those Actions, or simply want to keep them private to avoid security issues or other problems.

### The Solution

And this is where the new feature comes into play: less than a couple of week ago, GitHub has made available the __hosting of Actions in Internal repos__.

![Announcement](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uk5oapo2k97zneeef7v1.png)

And this means that your Action is effectively “Private” since internal repos can be seen only by members of an organization.

There is actually __a catch__ on this being private. In GitHub docs, there is this curious warning that says: “_If you make an internal repository in your enterprise accessible to GitHub Actions workflows in other repositories, outside collaborators on the other repositories can indirectly access the internal repository, even though they do not have direct access to the internal repository_”

![GitHub Warning](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/n3uegilt0opu9hie4hdb.png)

They also mention they can view the logs when the Action is used, but first __I would expect that to be the case__, if I use an Action I should be able to read the logs, and second, it is not clear if that is the only access they have or if there’s anything else they can do as part of what they call “__indirect access__”. I’ve tried this feature and I didn’t seem to be able to access or see the internal repo with an account that didn’t have access to the org, but I think this is worth a deeper investigation.

With that said, let’s see quickly how to enable this.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube _qS9UbbkGa4 %}

[Link to the video: https://youtu.be/_qS9UbbkGa4](https://youtu.be/_qS9UbbkGa4)

If you rather prefer reading, well... let's just continue :)

### Enable Actions in Internal Repos

Alright, first thing you have to do is making sure the repo you want to host your custom Action into is __internal__.

![Internal Repo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gxf2jtp8vq41ds9jh9gw.png)

Just go to the repo _Settings_, scroll down to the Danger Zone, click “_Change Visibility_”, and select “_Make internal_”.

> If you don’t see the Internal option but only Public and Private, make sure the repository you are working on is part of an organization in the ___GitHub Enterprise Cloud___

Next, we need to __enable the access__ to this repo from the GitHub Actions workflows that will reference our custom action.

To do this, still in the _Settings_ section of your repo, find and expand the “_Actions_” tab, and click on “_General_”. Scroll down until you see the “_Access_” section, and here you can find the 2 options the allow to access the repo from workflows in the __same organization__, or even taking it a step forward enabling the sharing to the __whole enterprise__.

![Enable Access to the Repo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xb5njcp3arizualjht5l.png)

And that’s basically it, now you can reference the action stored in that repository from the repos in your organization or enterprise respectively. Just use the usual syntax:

```yaml
owner/repo@version
```

where `owner` is the name of the organization where the repo is hosted.

### Notes

Quick note: the Actions you store in internal repositories can only be used by workflows defined in other __private and internal repositories__, but cannot be used in workflows defined within any public repositories.

Also, at the time of recording this video this feature is still in beta so things may change, and it is __only available for accounts in the GitHub Enterprise Cloud__ as I’ve mentioned before.

### Conclusions

Let me know in the comments below if you are happy that this feature is finally here.

Also, check out [this video](https://youtu.be/lRypYtmbKMs) where I talk about sharing entire workflows in GitHub Actions.

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

{% youtube _qS9UbbkGa4 %}