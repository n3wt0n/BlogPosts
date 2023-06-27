Do you want to build your application with GitHub Actions, but the standard agents are not powerful enough for your needs and at the same time you don’t want to use self hosted runners?

Well, GitHub has just released the Larger Runners feature and it is exactly what you need.

Let’s take a look at it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube lTAkB7P1qV0 %}

[Link to the video: https://youtu.be/lTAkB7P1qV0](https://youtu.be/lTAkB7P1qV0)

If you rather prefer reading, well... let's just continue :)

### About Action Runners

As I’ve mentioned in the intro, today we are going to take a look at the GitHub Larger Runners. We will see them in action (_no pun intended_) in a moment, but I think is important to have a bit of context around GitHub Actions runner first. Feel free to skip to the the next part if you know already everything about GitHub Actions.

First of all, runners are basically the machines that execute jobs in a GitHub Actions workflow.

![Runner into screen](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rtdycxlrfobl3c08ncob.png)

For example, a runner can clone your repository locally, install testing software, and then run commands that evaluate your code.

GitHub provides runners that they maintain and you can use to run your jobs. Each GitHub-hosted runner is a new virtual machine hosted by GitHub with the runner application and other tools preinstalled, and is available with Ubuntu Linux, Windows, or macOS.

When you use a __GitHub-hosted runner__, machine maintenance and upgrades are __taken care of__ for you.

Until now they only had a single size of these runners, with 2 cores and 7Gb of ram for the windows and linux runners, and 3 cores and 14gb of ram for MacOs.

And this meant that if your application needed more resources to be built or tested, you had to __install your own runners__, on your own hardware or cloud of choice. While this is not necessarily a huge problem, it comes with 2 downsides:

- First, you need to take care of the installation and upgrade of all the needed tools and libraries yourself,
- and second your own hosted runners are not ephemeral, meaning that all the files, temporary folders, etc from the previous completed jobs are still on the machine.

And this is where the new GitHub Larger runners come into play. 

### The Larger Runners

We now have the option of allocating __a lot more resources__ to our runners, up to 64 cores and 256 gb of ram, while having them still hosted and __managed by GitHub directly__! Which means tools installation, maintenance, etc, are all already done. And, the runners are __ephemeral__.

There are a couple of other _somewhat minor_ differences between standard hosted runners and larger runners,  you can check them out all here [on the official documentation](https://docs.github.com/en/actions/using-github-hosted-runners/about-larger-runners#additional-features-for-larger-runners).

### Create Larger Runners

So, how can we __enable and use the Larger Runners__?

> [Check the demo section of the video to see this in action](https://youtu.be/lTAkB7P1qV0?t=151)

From your organization home page, go to `Settings`, scroll down to `Actions`, and click on `Runners`. Here you have the list of runners already associated to your org.

![List of Runners](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oxu9q081sehzxezusp3l.png)

Next, click on the `New Runner` button, and pick `New GitHub-hoster runner`.

This takes you to the creation page.

![New Runner form](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wknvxmitdpodqau8rlj7.png)

You can give it a name, select Ubuntu Linux or Windows Server as OS (_MacOS will be available soon_), and select the size: from 4 cores 16gb of ram all the way to 64 cores and 256gb of ram.

You can set a maximum concurrency, which means how many runners can be createad and run at the same time.

![Public IP on Actions Runners](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cqqo6yxuevyqjpuwbsxq.png)

And, if you are on GitHub Enterprise, you can even assign a unique static public IP range for these runners.

Click `Create Runner` and you are done.

### Use Larger Runners

> [Check the demo section of the video to see this in action](https://youtu.be/lTAkB7P1qV0?t=203)

The creation was super easy, but how to use the new runners? It’s no different on how you normally use any other runner.

Just edit your workflow YAML file and in the `runs-on` field use the name of the runner you have created.

![Using Larger Runners](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rah7sndj1v1ymofpw6rl.png)

In my case, using "a lot of imagination" I called it _mynewrunner_ so that is what I am going to use.

From now on, my workflow will use the new larger runner. Not difficult, right?

### Pricing and Availability

Another important thing is pricing.

Compared to standard GitHub-hosted runners, larger runners are __billed differently__. Larger runners are only billed at the per-minute rate for the amount of time workflows are executed on them. There is no cost associated with creating a larger runner that is not being used by a workflow.

Also, larger runners are __not eligible for the use of entitlement minutes__ on private repositories. For both private and public repositories, when larger runners are in use, they will always be billed at the per-minute rate.

Last but not least, availability. Larger runners are available for organizations and enterprises using the __GitHub Team or GitHub Enterprise Cloud__ plans.

### Conclusions

Let me know in the comments below what you think about the Larger runners, if you are using or going to use them, and for what specific application or requirement.

Also, check out [this video](https://youtu.be/msCWg2F4sck) in which I cover all the [automation capabilities of GitHub Actions](https://youtu.be/msCWg2F4sck).

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

{% youtube lTAkB7P1qV0 %}