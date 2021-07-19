Ever had the need to restrict some users to just specific projects in Azure DevOps? Today I'm gonna show you how to do that.

### Intro

Today we talk about a new feature that has been released recently in Azure DevOps and that allows you to limit the user visibility and collaboration to specific projects. I'm talking about the _Limit user visibility and collaboration to specific projects_ Preview Feature

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube yftHyHW32fM %}

[Link to the video: https://youtu.be/yftHyHW32fM](https://youtu.be/yftHyHW32fM)

If you rather prefer reading, well... let's just continue :)

### The Problem

By default, users added to an organization __can view all organization metadata and settings__.

![Org Settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mcr9xpetxtinq23bdxcd.png)

This includes viewing the list of users in the organization, list of projects, __billing details__, usage data, and anything that's accessible through the organization settings.

![Users Selection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ep2oko4gjf66i1o6vzuf.png)

This includes viewing the list of users in the organization, list of projects, billing details, usage data, and anything that's accessible through the organization settings.

This is because people pickers provide support for searching __all users and groups added to Azure AD__, not just those users and groups added to your project

And until now there was no effective way to change this behavior. As I said, ___until now___ :)

### The Solution

To restrict users from this information, you can enable the "___Limit user visibility and collaboration to specific projects___" preview feature for your organization. 

![Feature Enabled](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/95vkcb5jlsbvzjuhkfhe.png)

Once enabled, the _Project-Scoped Users_ group, which is an organization-level security group, will be added to your Azure DevOps organization. It can be found by navigating to the Organization `Settings -> Permissions`

When you add Users and groups to this new group, they will see a banner stating that the administrator has limited their visibility.

![Banner](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kxmh5kg8gr8tw8pps9to.png)

After that, they will have two limitations. 

![Limited Org Settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5oeq01rj10x5kuc976ao.png)

When accessing the Organization Settings, most of the items will be hidden. 

And about the people selection, the people-picker search will be limited to only the AAD Users that have been added to the project the user is scoped to.

![Limited User Selection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w18dcw01ffali918cr33.png)

And this applies also to the tagging of users in Work Items and Comments.

### Conclusions

__Comment down below__ and let me know if this new feature solves any issue you had in the past with user management.

Also, checkout [this video](https://youtu.be/nrYSu_046cw), where I talk about how to properly secure and Azure DevOps Organization.

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

{% youtube yftHyHW32fM %}