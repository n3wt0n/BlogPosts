Today we talk about a new feature of GitHub that not many people know about, the __AutoLink References__. I will show you how to __automatically add links to external resources__ like JIRA issues and Zendesk tickets into your GitHub issues, pull requests, etc. using custom tags.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube ZoXiA_WyNzc %}

[Link to the video: https://youtu.be/ZoXiA_WyNzc](https://youtu.be/ZoXiA_WyNzc)

If you rather prefer reading, well... let's just continue :)

### Autolinks?

You probably know that GitHub automatically creates links when a standard URL is typed or pasted into an issue or any other markdown field, and that it also creates links to other pull requests, Issues, and commits when you use the proper notation, like the # for referencing an issue.

What you probably don't know is that __you can create your own shortcuts__ and automatic link creation for external resources.

If you use an external tool to track user-reported tickets, for example, you can __reference a ticket number in the pull request__ you open to fix the issue. And this works basically with anything that is reachable via URL. 

### Create Autolink References

Let me show you how to do this.

![Setting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hjth4jab791zqq3vvmnh.png)

First, we need to go to _Setting_, and where you have the _Autolink References_.

When there, you have a "_Add Autolink Reference_" button that, as the name says, lets you add a new one.

![New Autolink](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/awnj3f2mta5cq8gc1j1k.png)

In the form you have to specify 2 things:

- the prefix, or keyword, you wanna use
- the link to your service

> __Note__: the link must contain the variable `<num>` which will be replaced at runtime with the ID you are going to specify.

For example, in my case I want to link some Discord channel to my issues, so the configuration will look something like this:

![New Autolink filled in](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5pknoxf7lsosau1ruz2z.png)

### How to use them

> Take a look at the [video of the demo](https://youtu.be/ZoXiA_WyNzc) to see this in action

Now it's time to use our new autolink reference. As I've mentioned before, __you can use it in any field__ that accepts markdown... but it is certainly most effective when used in Issues and PRs.

Just type your prefix, followed by the id of the resources (page, ticket, issue, etc...) you are going to reference. For my Discord example, something like this:

![Issue](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/36t2972xbtt0u8y3jbnt.png)

When the issue is saved, the __Autolink Reference does its magic__ and "transforms" the shortcut in a full link as you can see here:

![Transformed](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v6m6ao64cnuv0qa07a03.png)

### Limitations and Notes

Cool right?

One thing you need to be aware of is that the ID of the resources you are trying to link using Autolink References __has to be numeric__. Currently alphanumeric IDs are yet not supported.

Also, it is worth mentioning that Autolinks are available in repositories with GitHub Pro, GitHub Team, GitHub Enterprise Cloud, and GitHub Enterprise Server.

### Conclusions

Let me know in the comment section below what you think of the Autolink references.
For me it's a very cool feature and I can think of hundred different ways I want to use it.

__Like, share and follow me__ 🚀 for more content:

[YouTube](https://www.youtube.com/CoderDave)
[Patreon](https://patreon.com/CoderDave)
[Merch](https://geni.us/cdmerch)
[Facebook page](https://www.facebook.com/CoderDaveYT)
[GitHub](https://github.com/n3wt0n)
[Twitter](https://www.twitter.com/davide.benvegnu)
[LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
[Podcast](https://geni.us/cdpodcast)

{% youtube ZoXiA_WyNzc %}