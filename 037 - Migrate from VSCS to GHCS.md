You may have already heard about this, but __Visual Studio Codespaces will be soon retired__ in favor of GitHub Codespaces. This means we have to migrate to it to continue to use this awesome online development environment.

Today we are going to explore 3 ways to migrate from Visual Studio Codespaces to GitHub Codespaces.

### What is happening?

If you have been using Visual Studio Codespaces before, you've probably received this email.

![The Email](https://dev-to-uploads.s3.amazonaws.com/i/f8l3n3cwif9yoxul64f2.png)

Soon you won't be able to create new Visual Studio Codespaces environments and in February 2021 we will not be able to access the service anymore, and any Codespaces or plans that you created through it will be deleted.

Why is this?

Currently, Azure customers have __two options__ for cloud-hosted development environments — Visual Studio Codespaces and GitHub Codespaces. To streamline and simplify the user experience, __Microsoft and Github are consolidating these services in GitHub Codespaces__, and they'll retire Visual Studio Codespaces on 17 February 2021.

### It's time to migrate

So, __we have to move to GitHub Codespaces__. Today I want to walk you through __3 ways to do so__, 3 ways to migrate from Visual Studio Codespaces to Github Codespaces. 

I will also give you a __timeline__, and few extra information about the whole move.

### Video

If you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube u0J4YQhiiFI %}

([Link to the video: https://youtu.be/u0J4YQhiiFI](https://youtu.be/u0J4YQhiiFI))

If you rather prefer reading, well... let's just continue :)

### The timeline

Let's talk about the timeline first.

![Timeline](https://dev-to-uploads.s3.amazonaws.com/i/w0eofgqd53tac9geep6v.png)

GitHub Codespaces are already available in beta since September 4, so maybe you already have it enabled or, if not, you can __ask for entering the beta__.

Starting on November 20, 2020 we will not be able to create new plans and new environments, and new users won't be able to sing up for the service. At this stage, however, ___existing Codespaces environments will still be working___.

Finally, on February 17, 2021 the service will be retired. This means that you will not be able to access the portal anymore and the __existing environments will be deleted__.

### Why migrating now?

Even though we still have few months to migrate from VS Codespaces to GitHub Codespaces, I'd recommend moving as soon as possible, for 2 reasons:

1. GitHub Codespaces is currently free, since it is in beta, while you are paying for the Visual Studio Codespaces
2. So you have more time to familiarize with the new service, even tho it is very similar, and you can solve any issue you might encounter

Alright, so how can we migrate from Visual Studio Codespaces to GitHub Codespaces?

Let's start by saying that __there isn't a direct way to move Visual Studio Codespaces over to GitHub Codespaces__. You will eventually need to re-create your codespaces once you gain access to the GitHub Codespaces beta.

But we have 3 ways to do it, let's go through each one of these.

### 1 - Everything from scratch

> [WATCH THE FULL EXPLANATION HERE - First way](https://youtu.be/u0J4YQhiiFI)

The first way is obviously from scratch. This is probably the simplest way but also the most time-consuming one.

1. Create your own GitHub repository
2. Manually push all the code there
3. Copy over or re-create all the customization you have (_like dotfiles, containersettings.json, etc_)
4. and then you create the Codespaces environment.

As you can see, this will be quite time consuming.

### 2 - Export and Download

> [WATCH THE FULL EXPLANATION AND EXAMPLES HERE- Second way](https://www.youtube.com/watch?v=u0J4YQhiiFI&t=223s)

The second way we have for moving our Visual Studio Codespaces environment to GitHub is by __exporting and downloading the actual environment__.

You would need __VS Code__ with the Codespaces extension to do this.

In the Codespaces view:

- Login to Codespaces 
- Right Click on the Codespaces environment
- Export Codespaces

Remember that the environment __needs to be suspended__, if it is not VS Code will ask and suspend it before it can proceed.

This will download your __whole Codespaces environment workspace__. And this includes all the customizations you've made, and all the changes you have done to your application that you may not have yet pushed to the remote repository.

In fact if we compare the source repo with the content of the exported Codespaces workspace we can see that __the latter contains files and especially settings and customizations that are not present in the remote repo__.

Now all I have to do is create a new repo, upload (aka push) the files I've just downloaded and my GitHub Codespaces environment will be complete with all the settings and customizations I had before in the Visual Studio Codespaces one.

Cool isn't it?

> [WATCH THE FULL EXPLANATION AND EXAMPLES HERE- Second way](https://www.youtube.com/watch?v=u0J4YQhiiFI&t=223s)

### 3 - Git to the rescue

> [WATCH THE FULL EXPLANATION AND EXAMPLES HERE- Third way](https://www.youtube.com/watch?v=u0J4YQhiiFI&t=353s)

This is somehow similar to the previous one, with the difference that we don't need to download the files and re-upload them to GitHub. __Git can do this for us__.

First, you need to have an empty GitHub repo. It should be __not initialized__ for this to work.

Then, in your Codespaces environment you can access the __Terminal__ and just __add a new origin__ to your workspace:

```bash
git remote add GHorigin https://github.com/USER/REPONAME.git

git push -u GHorigin
```

And that's it.

Since the workspace contains all the customizations and settings, now we have all the files in here, and we can spin up a new Codespaces environment from here.

> [WATCH THE FULL EXPLANATION AND EXAMPLES HERE- Third way](https://www.youtube.com/watch?v=u0J4YQhiiFI&t=353s)

### Common questions

Check [this section of the video for some answer to the most commonly asked questions about this](https://www.youtube.com/watch?v=u0J4YQhiiFI&t=488s)

Those include:

- Are VS Codespaces and GitHub Codespaces at feature parity?
- What about the private preview of Codespaces for Visual Studio?
- Can I use other Git providers?

### Conclusion

Alright, that's it for today.

Will you be migrating to GitHub Codespaces anytime soon?  
Let me know in the comment section below if you can think of any other way to do the migration.