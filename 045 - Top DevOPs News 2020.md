It's that time of the year, time for a summary. This will be the __Top 5 DevOps-related news of 2020__!

### Intro

This post is the last one I will publish in 2020. In fact I will take a short break and I will publish the next post (and video) on 12 January 2021.

Alright, let's go into the news. These are my Top 5 news of this year, but if you have any other news that you want to share or that you think is more important please let me know in the comment section below, I'd love to hear your opinion.

Also, the news are not in any specific order. If one comes before another it doesn't mean it's more important or anything.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video, which to be fair is much ___more complete___ than this post.

{% youtube 3cBF7I8ecMc %}

([Link to the video: https://youtu.be/3cBF7I8ecMc](https://youtu.be/3cBF7I8ecMc))

If you rather prefer reading, well... let's just continue :)

### 1. Environment Support in GitHub Actions

The first one I want to talk about is something very recent, but in my opinion very impactful in the DevOps community.

I'm talking about the new __GitHub Actions Environments and Manual Approval__.

Even tho at the first glance this may not seem like a big news, __I think it's actually huge__.

![Environments](https://dev-to-uploads.s3.amazonaws.com/i/wotluu1aw1ahowyao2go.png)

This feature, announced during GitHub Universe 2020 just few weeks ago, marks the official entrance of GitHub Actions in the __enterprise CD world__.

Of course you could deploy using Actions even before this new feature, but it was more oriented to small projects. Now instead you can fulfill the most basic requirement of any Enterprise and I'd say also of most of the "real world" project: ___being able to control the deployment flow___.

![Visualization](https://dev-to-uploads.s3.amazonaws.com/i/0hqekuain5ci9eub0kb3.png)

And that is not all, in fact thanks to Environments all the operations around deploys and releases are __tracked and audited__, so now you are actually able to see at any point in time what was deployed, from who and when.

The support of Environments and Approval in GitHub Actions is an important step forward in the maturity of the platform, making it a very strong potential competitor to other systems. And if you think that even before that Actions was the most popular CI platform on GitHub... well, it says something.

> For a __deep dive__ into GitHub Actions Environments and Approvals, check [this video I made](https://youtu.be/w_37LDOy4sI)

### 2. Kubernetes dropping Docker Support

Second news in my Top 5 is something that made a lot of noise when has been announced.

I'm referring to Kubernetes dropping Docker support from the version 1.22.

The news wasn’t actually a big surprise, for the people near Kubernetes, because the Kubernetes development team had been planning and preparing this step for __about three years__.

However, as I said before, and as you've probably seen as well, this caused a ___mediatic earthquake___. And I think it's mostly because not everyone has actually understood what this announcement means.

First of all Kubernetes will continue to run Docker images because they are __fully compatible with the OCI__ (Open Container Initiative), which Kubernetes supports. Actually Docker was one of the entities which launched the OCI back in 2015.  

![OCI](https://dev-to-uploads.s3.amazonaws.com/i/6a36ep2cvt48i55weh1u.png)

So regardless how Kubernetes runs its container clusters, __Docker images will be able to run on Kubernetes clusters just like they did until now__. 

And because of that, end users will likely __not notice any difference__ at all in how they use their clusters.

Cluster admins, on the other hand, most likely will need to lay hands on their clusters and change the configuration, but once again this should not be seen as a catastrophic operation.

![K8S tweet](https://dev-to-uploads.s3.amazonaws.com/i/3fu6cgh9rrwonuo1fqvl.png)

I don't want to go too deep into the technical reasons why this is happening, but what Kubernetes actually wants to achieve is to remove the need to install Docker and recommend more lightweight alternatives. As Docker includes various tools and APIs to allow you to run containers and a lot of other stuff that Kubernetes doesn't really need.

So yes, Kubernetes is dropping Docker support, but __there is no reason to panic__ because as I've said, for most of us will be business as usual.

### 3. Atlassian Discontinuing All Their Server Products (Including Jira and BitBucket)

Right, into the next one. When talking about news __it's not always good news__, and in fact this isn't.

I don't know if you've heard this, but __Atlassian is discontinuing ALL their server products__ (including Jira, BitBucket and Confluence) as part of their program "journey to the Cloud", as they call it.

![Atlassian Deprecation](https://dev-to-uploads.s3.amazonaws.com/i/00yryr3diixs7qdvh95c.png)

This means that Atlassian will __stop selling new Server licenses__ for all their products starting February 2, 2021. And that will be followed by a __complete end of support of all their server products__, for both bug fixes and most importantly security fixes, in 2024.

What this means, in practice, is that you will either have to migrate to their cloud offering or continue using an unsupported product at your risk.

Atlassian did say, to be fair, that they will, and I quote, "_augment their Datacenter products_" but I've not been able to find any information about what this means.

So if you are an Atlassian user and you're using their server products I'd encourage you to __plan a migration__, either to their cloud platform or, if that is not an option for you, to some other provider that offers server products like for example GitHub Enterprise Server or Azure DevOps Server.

### 4. GitHub Makes Private Repositories FREE for Unlimited Users

Next stop, I wanna talk again about GitHub but this is not a recent news.

In fact Github announced this back in April: __private repositories are available to all GitHub accounts for free__, for an unlimited number of collaborators, and the reduction of the license cost for Pro and Team plans.

Previously, if your organization wanted to use GitHub for private development, you had to subscribe to one of the paid plans. But now that comes actually __free of charge__.

![GitHub free](https://dev-to-uploads.s3.amazonaws.com/i/vto46l7qi5n8oklh9evz.png)

Teams who need advanced features (like code owners), enterprise features (like SAML), or personalized support do still need to upgrade to a paid plan,  however, the cost of a paid Team plan has been reduced to $4 per user/month from $9 per user/month. 

This was an __amazing news__ back in April, and still is, in my opinion.

I think the limitation of private repos on GitHub has always been an adoption blocker and now that it is removed many more developers and teams have and will join the platform, contribute to opensource and __adopt innersource__ as part of their set of practices

Thanks, GitHub.

### 5. Massively Increased DevOps Adoption

The last news in my Top 5 is actually not really a news but more __a trend__. In fact 2020 has seen a __massive increase of the DevOps adoption across the board__. I don't know if it is because of the ongoing pandemic or because this year marked a milestone in companies maturity, but yet that happened.

I had a many discussions with teams wanting to start adopting DevOps in their organizations or wanting to take a step forward in that area, and so have my colleagues.

![DevOps Institute](https://dev-to-uploads.s3.amazonaws.com/i/8akn7dcqucgoa1ic69c5.png)

If we take a look at the [DevOps Survey](https://devopsinstitute.com/thought-leadership/upskilling-2020/) for 2020 presented by the DevOps Institute, we can see that DevOps Adoption has grown __substantially__, and so have Agile and SRE Adoption

And let's take a look at the GitHub's [State of the Octoverse](https://octoverse.github.com/) report.

![State of the Octoverse](https://dev-to-uploads.s3.amazonaws.com/i/m59an93tt2apobww9bl4.png)

This year has seen an __incredible spike in new repository creation__. 

In May, over 40% more repositories were created compared to last year, and since then, roughly 25% more open source repositories have been created compared to the same time period last year.

![State of the Octoverse DEV](https://dev-to-uploads.s3.amazonaws.com/i/ryllmnj33l7nhcmoqobw.png)

Moreover, if we talk about development,  we can see that there's been a __huge increase in both code push volume and number of Pull Requests__ compared to 2019.

And this is true also for the security side of DevOps.

![Security](https://dev-to-uploads.s3.amazonaws.com/i/g53raqrwnawb23e2mvtb.png)

According to the [State of DevOps Report 2020](https://puppet.com/resources/report/2020-state-of-devops-report/), the level of __Security integration in 2020 is higher than it was in 2019__, especially in the levels 3 and 4.

### Conclusion

Alright, these were the TOP 5 DevOps Related news of 2020 for me. As I said before, let me know in the comment section below if I've missed something you consider important.

With this, I wish you all a prosperous new year, I hope 2021 will bring you joy.

Once again, thanks for your support to this blog and the [YouTube channel](https://youtube.com/CoderDave), all this wouldn't be possible if not for you. 

__You all made my year__.