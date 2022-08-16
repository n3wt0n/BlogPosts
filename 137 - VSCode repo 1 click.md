Do you have some code in VSCode and want to take it to GitHub, without having to write a single command in the CLI? Today I’m gonna show you how to do that, how to publish your code to a new GitHub repo, all from VSCode.

### Introduction

I already have [an article](https://dev.to/n3wt0n/how-to-use-github-with-visual-studio-code-1p7d) and [a video](https://youtu.be/aUhl3B6ZweQ) talking about how to use VSCode with GitHub, but, as someone has pointed out:

![Comment from YouTube](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c1cg1ycata4mbt6tgbt4.png)

That content assumed you already had your code on GitHub. But what if you don’t? Let’s do it now.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube shP-3p-2m6g %}

[Link to the video: https://youtu.be/shP-3p-2m6g](https://youtu.be/shP-3p-2m6g)

If you rather prefer reading, well... let's just continue :)

### Just one prerequisite

Everything you need to create a new repository in GitHub from VSCode is already present in Visual Studio Code itself. The only thing you need to make sure to do before hand is logging in into VSCode with your GitHub user.

Your VSCode should look like this:

![VSCode Login](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u33ajdq8t07erwlx511s.png)

Of course with your username, not mine 😇

If it is not like this, click on _Sign In (GitHub)_ and you are good to go.

### Create the repo

Now that we know we are logged in, creating the repository in GitHub is very easy.

Just click on the ___Git - Source Control___ icon  

![SCM VSCode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3hib6o52sbjyqi7tv79v.png)

And this will prompt you to either _Initialize Repository_ or ___Publish to GitHub___

![New Repo Choice](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nul29cn3pnahgbj9mymj.png)

The first option does only execute the _git init_ command, so it does technically create a repository for you but only on the local machine. If you want to have your repo in GitHub, instead, use __Publish to GitHub__. This will do for you the repo initialization as well, but will also create a new repo in GitHub and push the code to it.

![Repo Type Selection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p5fjq3evupg7wy481v1a.png)

When you click on _Publish to GitHub_, VSCode will ask you what name you want your new repo to have (defaults to the name of the root folder of your project) and you can choose whether you want your new repo to be private or public.

Last thing you can do is select what files or folders you want to include in your repo (the default is everything, so if that's what you want to do you can just skip this step).

![Repo File Selection](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t7z0o9ipmomgwa8sijdn.png)

And after that, VSCode will do its magic, create the repo for you in GitHub, set it as the origin on the local folder, and push the code.

![Completed](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t3zzctr91ahbaphxzl3g.png)

### Conclusions

Cool right? And you know what would be even cooler? If you could hit the like buttons on the side :)

Jokes aside, now that your code is on GitHub, go and check [this other video](https://youtu.be/aUhl3B6ZweQ) I’ve mentioned before to see how you can manage it directly from VSCode as well.

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

{% youtube shP-3p-2m6g %}