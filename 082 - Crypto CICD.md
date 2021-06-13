We all know that crypto mining is negatively impacting many things in the world. And now it's ruining something else in a way no one has seen coming. This is why mining crypto currencies is killing every free CI / CD platform.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video__, which to be fair is much ___more complete___ than this post.

{% youtube 9TOJqJSHVvI %}

[Link to the video: https://youtu.be/9TOJqJSHVvI](https://youtu.be/9TOJqJSHVvI)

If you rather prefer reading, well... let's just continue :)

### Intro

Today I have to talk about something I'd prefer not to, but unfortunately this is happening, and it's happening hard. So let's talk about crypto mining and its deleterious effect on free CI/CD platform.

### A Work on Mining

We all know crypto mining, the process in which transactions for various forms of cryptocurrency are verified and added to the blockchain digital ledger, using the computing power of computers or graphics card, and for which miners are rewarded with crypto currencies directly.

We probably all know that this is affecting many aspects of our current time. For example, the current and past generation of graphics cards are so good and fast for mining that it's basically impossible to buy a graphics card right now, or if you find one the price is crazy. All the supply is basically taken up by miners, and few very lucky gamers.

### How Does Mining Cryptocurrencies Affect CI Platforms

Ok, but how does this affect the CI/CD platforms? I'm glad you asked.

Due to the lack of availability of graphics cards, and the constantly increasing number of miners thanks to the rise in value of cryptocurrencies, miners have started trying to find alternative ways for mining. 

They first started using Cloud services but quickly realized that the cost for always running large instances was higher than the gain they were able to get. And this is when they started looking at the free CI providers. 

Hosted Build agents are fairly powerful, having to take care of compilation etc., and most platforms have a free tier, especially for public repositories. Powerful machines for free, a miner's dream come true.

And this is exactly the problem. They have started writing script, pushing them to public repositories, and take advantage of those free CI agents to run their mining software. And as the different providers started blocking those attempts, miners adapted and started writing fairly complex software and scripts to "mask" the real reasons why they were using the repos and CI agents.

### An Example

There are countless examples, but here is one just to make you understand the gravity of the problem. There was a user on GitHub who created a simple repo, which seemed a legit one at a first look.

In the repo this user had the definition for 5 different CI providers, including GitHub Actions, CircleCI, TravisCI and others, and all were configured in automatic CI. The user had roughly 1 commit every hour, which in turn kicked off all 5 of those CI... and the script that was run was in fact a crypto miner. You can imagine how much resources that user alone has consumed.

### The Effects

And in fact, if you have noticed your hosted CI agent being slower than usual or picking up jobs with a greater delay most likely it's because of this. And not only on free CI, but also on paid CI platforms... because the resources are the same. But if the problem was just some slowness, we wouldn't be here talking about this.

The problem is much bigger. So much so that basically all the CI providers have stopped offering free tiers or, in the best cases, they've implemented great limitations on the services.

### Industry Reactions

#### Azure DevOps

Microsoft is not providing anymore free concurrent CI for their Azure Pipelines for new organizations. If the users want them, they need to request for them and provide additional information to verify they are eligible.

![Azure DevOps](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7bvey4m7t1qwh6416hkq.png)

#### TravisCI

TravisCI is taking it a step further, completely removing the free tier, and giving to existing users a trial with an amount of free credits. When the credits are exhausted, if a user wants to keep using CI then they will have to buy a paid plan.

![TravisCI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pf0t2rpdy1m04u37q10g.png)

#### GitLab

GitLab, takes a different approach. 

First, they require new users to verify their account adding a credit card to their account before they can start using the hosted CI agents. Existing users are not currently required to insert a credit card number, but they may be in future.

![GitLab](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3uvmwqbmbqr9uxnctdb8.png)

Second, they are removing the unlimited free minutes that were previously assigned to public projects, and setting a limit to 400 free minutes instead.

![GitLab](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/awd6anryw7uruvpzgn73.png)

#### CircleCI

Circle CI has never had a completely free plan, but only a free grant of 2500 credits per month. 

While they haven't change that, at least not yet, they 've published an article saying that they have a whole team, and I quote, "_of security experts, operations engineers, data scientists, and developers whose ongoing work comprises spotting and eradicating abuse of our platform_".

![CircleCI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ukvd2c7ob6km6y8t0mzd.png)

This of course is a huge cost for the company, and if things will continue like this they will need to find a way to get the money back... you make of this what you want.

#### GitHub Actions

Finally, GitHub Actions is the only provider that I'm aware of which has still a completely free unlimited use of their CI and has not changed that.

However, they did mention in a post on their public blog that the Actions teams have spent thousands of hours fighting against miners. As in the CircleCI case, this comes at a cost. Having engineering teams focusing on fighting miners most likely means they have less time to focus on improving and developing the service.

![GitHub Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dvbrq7spynqd9y9qbutr.png)

And they are also saying that they are rolling out features and improvements to help maintainer of Open Source projects having a better control of their CI when it comes to Pull Requests and Forks.

![GitHub Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wxso1qf2n9gi3nccqjov.png)

And I could continue for long, because similar things are happening from each and every CI provider.

### The Solution?

Is there anything we can do to avoid this? Unfortunately, I'm afraid the answer is no.

Providers can do their best to enforce terms of service and take other measures, but as long as it's profitable and untraceable to make such attacks, miners will continue to become more sophisticated and circumvent measures.

The only hope is for crypto networks to fully disable the current computation-based mining as a way to earn new coins, switching entirely to a proof-of-stake (POS) validation model. It sounds impossible, but it is actually already happening. Ethereum in fact recently announced they will do exactly that.

### Conclusions

Let me know in the comment section below what you think about this sensitive topic.

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

{% youtube 9TOJqJSHVvI %}