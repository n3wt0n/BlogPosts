I’ve recently sent [a poll](https://www.youtube.com/post/Ugkxa3QvgM58EMcArTwu5qaN4HICgcqHLOw0) on my [YouTube channel](https://www.youtube.com/channel/UCtiFg7r8WBBzC6xo-tfEYFw) community tab, asking where people store their IaC, Infrastructure as Code.

![Poll](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ueqk8hd8dj7c60xilkye.png)

With my surprise, more than half of the people said that they __always__ store their IaC scripts and their application code in __separate repos__.

In this article I will discuss those results, and tell you __how and where I store my Infra as Code__ files, and why I think __you should do the same__ as well.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube Ub76JGoXzKI %}

[Link to the video: https://youtu.be/Ub76JGoXzKI](https://youtu.be/Ub76JGoXzKI)

If you rather prefer reading, well... let's just continue :)

### About IaC

As I’ve mentioned in the intro, today we talk about how to store your IaC, Infrastructure as Code, which is the way to __describe, create and manage your resources__ using some definition language. 

If you are not very familiar with it, and __want to know more__, I’d recommend you to check out the video I made about what IaC is and why using it. You can [find it here](https://youtu.be/fE4gY-SydKo)

### How I Store My Infra as Code

Alright, enough of that. How do I store my Infra as Code? Well, it depends.

I can say I do it __both ways__, I would have picked the option in the middle, in my poll above. And the reason for this is very easy to explain: it depends on __what the IaC script or model I’m writing is for__.

I tend in fact to split my IaC into __two parts__: foundational infrastructure and app-related one.

### Foundational Infrastructure

Foundational infrastructure comprises of all the pieces that are __not directly related to a specific app__ or service, but are instead more general and perhaps shared between different applications. Examples of this could be some Virtual Networks used by multiple services, storage accounts for storing logs, or Kubernetes clusters.

![Infra Repo](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1no1imc93z95kofdlvpj.png)

Since those are __independent__ from the software parts, I store them in a __separate centralized repository__. As you can see in the image above, I have different __folders for different environments__, and in each I have the resources. 

![Dev IaC](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/x07jwzck5frimmywa89c.png)

As I’ve mentioned, you can see I define here the AKS Kubernetes clusters, the networking resources, etc.

And as you have probably noticed, I use Terraform for my IaC. And I like to __separate my resources into modules__. 

![Terraform Modules on GitHub](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9hnc9ci08o3lebxq29l4.png)

I store their code in separate repositories in GitHub, and publish them to the HashiCorp cloud, on my private registry, together with the Terraform state.

![Terraform Modules Registry](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5dr6uza694uwaltbtmna.png)

Let me know in the comments if you want to know more about how I structure my Terraform IaC modules and files.

### App-related Infrastructure

Alright that was about the shared foundational infrastructure. So what about the other piece of IaC I've mentioned? The one related to the applications? Well, as you have probably already figured, I store it __together with the application code__, in the same repo.

![Application Repo with IaC](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wz599349shsttorus2hi.png)

As you can see here, I have my application code but I also have this ARM Template folder in the root of the repo, in which I have the __IaC scripts for this particular piece of software__.

In this case this was ARM but I do the same for Terraform, which, as I've mentioned, is my IaC provider of choice.

I store this way all the Infra as Code that provisions and manages resource only __related to a specific application__. That could be an App Service Web App where my web application runs, a Virtual Machine that hosts a server-management tool, or an API Management solution that provides the gateway for my application’s APIs... and of course the list can be endless, but you got the point.

### Why The Double Approach

Not only do I store my IaC it this way, but I usually recommend this to the teams and companies I work with. Storing your Infrastructure as Code with this "_double approach_" gives a __lot of flexibility__. For example, you could have a centralized infra management team taking care of all the shared infrastructure which provides the foundation of your environments, while leaving the apps specific bits to the app developers who know exactly what their software needs.

### Conclusions

Let me know in the comments below how you store your Infrastructure as Code and what you think about my approach.

Also, check out this video in which I go through the [reasons why you should use Infrastructure as Code](https://youtu.be/fE4gY-SydKo).

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

{% youtube Ub76JGoXzKI %}