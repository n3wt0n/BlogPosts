Civo Kubernetes Cloud has become quite popular lately, everyone seems to use it... especially because it promises to be cheap and fast, and with a good developer-friendly experience.

So, I decided to give it a try, and see what it is actually like. I've tried it for you, so you don't have to 😉

### TLDR

After trying it, there are __many things I liked__ but I also had some __issues__ and other things I didn't like.

In the video __I cover every point extensively__, with examples, and I give my opinion and general comments on the service. But if you want a quick overview, here you have it.

#### Things I Like

- It is very cheap
  - You can start as low as 5$ a month
  - Generally less than half cost when compared with other cloud providers
- You get 250$ for free to start with
- It is pretty fast: 
  - The provisioning of a cluster takes about 2 minutes 
  - Deletion and deprovisioning are basically immediate
- Application Marketplace (easy to install anything without Helm charts or scripts)
- They try to appeal to non-experts and make them learn.
  - Academy: lot of courses around Kubernetes, operations and management
  - KubeQuest: quests and tasks to complete to progress in the challenge
- They now also have VMs, not just K8s
- Support is quite fast
- Community oriented: docs, tutorial, feedback

#### Things I Don't Like

- The Documentation all over the place
  - While it is nice that it leverages the community, it also makes it chaotic
  - There are multiple different versions of the same topics. For example, there are 3 versions of a "_start with terraform_" tutorial (and one is wrong)
- After signing up, I had to wait for several hours for the account to be "verified" before being able to do anything (including creating clusters)
- The Terraform provider
    - As mentioned, there are at least 3 different versions in docs/tutorials
    - The documentation on the official Terraform registry website is incomplete
    - All the issues I had with my clusters were due to the terraform provider
- It is not as user friendly as other clouds, for Operations (Out-of-the box there are no metrics, no logs, no dashboard...)
- It is not mentioned anywhere of how they ensure HA and SLAs
- They have a quota system for resources, which could be a limit

### Video

If you want to know more about Civo, and my analysis of everything I liked and didn't like, check out the video I made:

{% youtube N6IEysLIx6c %}

[Link to the video: https://youtu.be/N6IEysLIx6c](https://youtu.be/N6IEysLIx6c)

### Conclusions

In general, it is not a bad service. It is really fast and really cheap, and offers a good value for the cost. I will personally use it for development purposes, but wouldn't recommend it (at least at this stage) for production workloads.

Let me know in the comments below if you have already tried Civo and what do you think about it, or if you are going to try it out.

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

{% youtube N6IEysLIx6c %}