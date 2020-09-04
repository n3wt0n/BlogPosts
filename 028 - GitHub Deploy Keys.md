Have you ever noticed a menu, deep down inside the GitHub settings, called __Deploy Key__ and wondered what that was for?

Well, today you'll finally know what that is for and how to use it.

### Intro

Today we talk about __GitHub's Deploy Keys.__ What are they for? How to use them? Pros and Cons?

First of all, let's see where we can find them.

![Menu](https://dev-to-uploads.s3.amazonaws.com/i/yzdn6behzbpeyi5ubpx7.png)

In your _repo_, just go to _Settings_, and here you have it: Deploy Keys.

Before adding one, let's talk about what they are.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much ___more complete___ than this post.

{% youtube qx1dHVtpCC0 %}

If you rather prefer reading, well... let's just continue    :) 

### What are the Deploy Keys?

Deploy Keys work in conjunction with something called "_Delivering Deployments_".

The ___Deployments APIs___, in fact, provides the capability to launch your GitHub hosted projects on a server that you own. Combined with the ___Status API___, you'll be able to coordinate your deployments the moment your code is committed on master.

And here is where the Deploy Keys come into the picture.

Because a Deploy Key is __basically an SSH key that grants access to a single repository__. GitHub attaches the public part of the key directly to your repository instead of a personal user account, and the private part of the key remains on your server.

And you can assign them write access so they can perform the same actions as a user with admin access, or a collaborator on a personal repository.

### Create and Assign a Deploy Key

To __create__ a Deploy Key, first thing to do is running the _ssh-keygen_ procedure on the server it is intended for.

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This will create both the private and the public key.

Next, check the `/.ssh/XXX.pub` file inside your home folder to see the public key (where XXX is the name of the file you specified in the previous command) and copy it's content. In my case:

```shell
cat ~/.ssh/githubdeploy.pub
```

Alright, now that we have the key let's go back to GitHub.

Click on the ___Add Deploy Key___ button and fill in the form.

![New Key](https://dev-to-uploads.s3.amazonaws.com/i/73iuxozqylky5ng249rz.png)

By default, the key is __Read Only__, meaning that can only Pull from the repo. If you want it to be enabled for Write Operations, just check the option.

There you go, now your __Deploy Key is added to GitHub__ and can be used to launch your project directly on your server.

Consider watching my [Video with full explanation about GitHub Deploy Keys](https://youtu.be/qx1dHVtpCC0) on YouTube

### PROs and CONs

Finally, let's take a look at the Pros and Cons of this approach.

__PROS:__

- Anyone with access to the repository and server has the ability to deploy the project.
- Users don't have to change their local SSH settings.
- Deploy keys are read-only by default, but you can give them write access when adding them to a repository.

__CONS:__

- Deploy keys only grant access to a single repository. More complex projects may have many repositories to pull to the same server.
- Deploy keys are usually not protected by a passphrase, making the key easily accessible if the server is compromised. 

### Conclusion

What do you think of the GitHub's Deploy Key? Let me know in the comment section below. 

There are other ways to do launch a project on your servers, let me know if you are interested to explore the other ones.

### References and Links

- [Video with full explanation about GitHub Deploy Keys](https://youtu.be/qx1dHVtpCC0)
- [Official GitHub Documentation](https://docs.github.com/en/developers/overview/managing-deploy-keys)