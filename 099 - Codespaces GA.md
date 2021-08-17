GitHub has just released __Codespaces in GA__, meaning that now it is __available for everyone__ (well, ___almost everyone___, more on this later) and it's feature complete.

In this article we will see how it works, what has been changed from the beta version, and all the new available features. And there are __a lot of them__. 

At the end, we will answer the question that many people have: __is GitHub Codespaces worth it__ or should you continue developing as you've done until now?

### Intro

I'm very excited because I've been waiting for this moment for a long time: GitHub Codespaces is finally GA!

![Tweet](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/achxk434w2qcaig27h45.png)

If you've been following this blog or [my YouTube channel](https://youtube.com/CoderDave) for a while you probably already know that I've covered Codespaces in the past quite a few times already (see this [YouTube Playlist](https://youtube.com/playlist?list=PL-HoEl0ZEUlKDm-ws2KQP8np-4Km7MSda)), but always on the __beta version__. 

Today I want to uncover with you all the feature that Codespaces has now that the GA version is available and see if and how the service has improved.

We will cover:

- What the Codespaces service is
- Availability
- The new creation experience
- Codespaces management
- Usage and new features
- Pricing and billing

And at the end we will answer the question we all have: ___is it worthy___?

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube Car0QZ_YbxQ %}

[Link to the video: https://youtu.be/Car0QZ_YbxQ](https://youtu.be/Car0QZ_YbxQ)

If you rather prefer reading, well... let's just continue :)

### What is GitHub Codespaces

So, real quick, what is GitHub Codespaces?

Codespaces is a service that allow you to create and use __cloud developer environments__ backed by high performance Compute.

Behind the scenes it uses full __VSCode__, including  editor, terminal, debugger, version control, settings sync, and the entire ecosystem of extensions. You can even you GitHub Copilot.

![Codespaces](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qf29hs1x03ec4jchvraz.png)

Codespaces works directly in the browser, or you can connect from your PC via a local VSCode instance.

New environments can be spun up in just seconds, and use __up to 32 cores and 64 Gb of ram__.

Codespaces environments are great because they can be __customized and standardized__ with runtimes, hardware specs, extensions, and settings on a user bases and on a __repository bases__. This means that all the people working on a repository can have the __exact same settings and requirements installed__, in just seconds.

### Availability

Ok, now we know what Codespaces does. Before we go further, let me address one thing: ___the availability___.

In the opening I've mentioned that Codespaces is now in GA and therefore it's ___available to everyone___. Unfortunately, __it is not exactly like that__.

Codespaces is in fact __available for organizations__ on either a __Team__ plan or GitHub __Enterprise Cloud__.

![Announcement](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d99mi3xnk5s6mxqq8q7t.png)

So, what about the users that are NOT in organizations or that don't have those plans?

![Individual Users](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zn5rsdksy9bnsr4703fo.png)

Users that are already in the beta of Codespaces will retain access to it. But it is unclear if new users could access the beta. In general, __seems like Codespaces will not be available to "normal" users__, at least for now.

There is however __another cool thing that is now available to everyone__, including the free users, and I will cover that in the next article/video... Consider following me here on Dev.to and subscribing to [my YouTube channel](https://youtube.com/CoderDave) if you aren't already, you don't wanna miss that video.

### How to Enable Codespaces

Alright, with that out of the way... Let's see how to enable Codespaces.

Just go to your _Organization Settings_, scroll down to _Codespaces_ and here you have it.

![Enable Codespaces](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rygddkc8db1kbi8u0kx5.png)

Here you can enable it for everyone, disable it, or enable Codespaces only for selected users.

If you see the same message as in the image above, don't despair... GitHub is rolling out Codespaces gradually so you may have to wait just a few more days.

> Watch [this section of the video](https://youtu.be/Car0QZ_YbxQ?t=206) for a full demo of this

### Creation of Codespaces Environments

Now that we have Codespaces enabled, let's see how it works and if the creation experience is any different from what it used to be before.

Just go to any of your repos and click on the "_Code < >_" button.

![Creation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9l39dbv9bzwtqkjawjsh.png)

Here you have the new __Codespaces__ tab, in which you can create a new Codespaces Environment.

If you are in an Organization with Codespaces enabled, you will be asked to select the size of your environment:

![Environment Size Selection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hw03tg05ps8by6iwm0qf.png)

You can pick any size from the minimum of 2 cores, 4 Gb of RAM, and 32 Gb of disk space all the way to the beefier configuration which has 32 corse, 64 Gb of RAM and 128 Gb of disk space (_Please note that the 32c/64gb configuration is not generally available, you'd need to contact GitHub support/sales to have it enabled on your Organization_)

If instead you are in the beta access program, the system will __default__ to the configuration with 4 cores, 8 Gb of Ram and 32 Gb of disk space, and you won't be able to change it.

Apart from that, everything else is the same between the above 2 scenarios.

And best of all, __the creation of an environment is WAY faster__ than it used to be, now your Codespaces environment is up and running in just __seconds__!

> Watch [this section of the video](https://youtu.be/Car0QZ_YbxQ?t=259) for a full demo of this

### Codespaces Management

You have now 2 ways to manage your Codespaces environments.

The first and more immediate one is to go back to your repository, click again on "_Code < >_" and access your environment from there.

![Access](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/db9wg47ceci1t1f348kq.png)

There is not much you can currently do from here, just click to access the Codespaces interface.

The other thing you can do, and which gives you __full access to the management__, is either clicking on ___Manage all__ in the same section or go to _Profile_ > _Your Codespaces_

![My Codespaces Menu](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jtiu0dpxmk5jbno299hs.png)

This will take you to the __Codespaces Management page__ in which you can create a new Codespaces environment, access an existing one, open it in VSCode, export the changes made to a branch (_in case you have changes that haven't been committed nor pushed yet_), change the size of your environment, and finally delete an unused one.

![Management](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/x9daxuadw4ixawcxiehh.png)

> Watch [this section of the video](https://youtu.be/Car0QZ_YbxQ?t=479) for a full demo of this

### Usage and New Features

Right, let's see if Codespaces is any different while using it and explore the new features that have been introduced.

> Watch [this section of the video](https://youtu.be/Car0QZ_YbxQ?t=572) for a full demo of this

### Pricing and Billing

Let's now talk about pricing.

Codespaces is __free to use__ for all organizations on a GitHub Team or GitHub Enterprise Cloud plan __until September 10, 2021__.

![Free](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lwzkxexutxsphkh1nw6m.png)

Also, Individual accounts which are part of __the beta access are not currently billed__ for Codespaces usage.

After September 10, existing Codespaces environments __will be billed for their active compute usage, and for the storage__.

![Codespaces Prices](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/73neza6la1sxt95bb8d6.png)

At the time of writing this video, these above are the prices the different Codespaces units will be billed. For your references, prices are shown in US Dollars.

Remember that you will be billed for the __CPU usage only when your Codespaces environments are active__ (_aka not in the Sleeping state_), and they will be billed by the minute. For the storage, instead, __the space used will be billed for regardless of the state__ of your environment.

Last thing I want to mention about the billing is that after September 10 you will need to __setup a Spending Limit __on your organization to be able to use Codespaces.

![Spending Limit](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qicfayiox3442vu29oe1.png)

By default, organizations will have a Codespaces __spending limit of $0__, which prevents new Codespaces from being created or existing Codespaces from being opened.

Remember to change that, or your users won't be happy 😁

### Is GitHub Codespaces Worth It?

Alright, it's now time to answer the __big question__ we have asked at the beginning: with all we have seen and talked about, ___is GitHub Codespaces worthy or should I keep working the old way?___

My verdict is: __it is worthy__. We all know that Reconfiguring code editors, IDEs, environments, and installing dependencies suck, and require a lot of time and effort. GitHub Codespaces offers a full cloud development environment, helping you __get started quickly__ without cloning, installing dependencies, or tweaking configurations.

Is GitHub Codespaces for everyone? Probably not. There are still frameworks and application types that are not fully supported.

In General, though, I'd encourage you to look into it, __evaluate it for yourself__, and start thinking about all the ways this service can help you, your team, and your organization being __more productive__.

### Conclusions

Alright, that's it for today.

Let me know in the comment section below your thoughts about the GA of Codespaces, and __if you have any questions__.

As I've mentioned, consider following/subscribing if you want to know more about Codespaces because I will have soon other articles and videos about this service and specific use cases.

You may also want to watch [this video](https://youtu.be/q0wHjFXZe6I), in which I explore using GitHub Codespaces from an iPad.

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

{% youtube Car0QZ_YbxQ %}