What happened in the DevOps Space in 2021? Yep, It's that time of the year... These are the Top 10 DevOps-related news of 2021!

### Intro

This post is the last one I will publish in 2021. In fact I will take a short break and I will publish the next post (and video) next year ;)

Alright, these are my __top 10 news of this year__, but if you have any other news that you want to share or that you think is more important please let me know in the comment section below, I'd love to hear your opinion.

Also, the news are not in any specific order. If one comes before another it doesn't mean it's more important or anything.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube 2R1nSOBBMuw %}

[Link to the video: https://youtu.be/2R1nSOBBMuw](https://youtu.be/2R1nSOBBMuw)

If you rather prefer reading, well... let's just continue :)

### General DevOps State in 2021

> [Watch this part here](https://youtu.be/2R1nSOBBMuw?t=50)

As a general comment, this year has been great for DevOps tools, but not __so much for DevOps Adoption__ at higher level.

The DORA's report for 2021, in fact, shows Modest DevOps Gains in comparison to 2019.

![DORA](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/phmvwhjknhezrzlpz9j1.png)

There has been only a 6% increase in the number of Elite Performers in the last 2 years, even tho the high performer grew about 17%. Not bad of course, but could be better. Not sure if the growth has been slowed down because of the pandemic, but all the analysts were expecting bigger numbers.

![DORA SRE](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3m6x7dbp2wvmq2vhftkn.png)

What is interesting in my opinion is the number of organizations that are reportedly using SRE practices, about 52% of the respondent to the study, even tho only the 10% of the elite performers reported to have implemented the totality of the practices. There is a lot of room for growth.

### 1. GitHub CEO Change

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=100)

Alright, let's jump to the first news, which is pretty recent and came quite unexpected. I'm talking about GitHub CEO Nat Friedman stepping down from the role.

In an internal post, subsequently published also on GitHub's blog on November 3, Nat in fact announced that he was stepping down as CEO of GitHub after more than 3 years of service.

![GitHub Stats](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k1k2falepc7invcyav0e.png)

In the same post, Nat Friedman also announced the latest figure about GitHub usage: 73 million of active developers, and about 84% of Fortune 500.

And the same day the company announced the new CEO, again with a post on the public Blog. Thomas Dohmke, who was previously Chief Product Officer.

![GitHub New CEO](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dkv4lldu9ano9zcxu33g.png)

Thomas has joined GitHub in 2018 together with Nat, and has been in charge of some very important programs like the GitHub Archive, Dependabot, Codespaces, Copilot and even the NPM acquisition.

![GitHub Statement](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i0h1l0q1capwqf16vw5q.png)

In the post, Thomas assured that GitHub will remain an independent outfit within Microsoft and that it will retain its developer-first values, distinctive spirit, and open extensibility, while supporting developers in their choice of any language, license, tool, platform, or cloud.

Well, good to know that. Who knows what GitHub will have for us in the coming months.

### 2. GitHub Actions OIDC Support for Passwordless Authentication to Cloud

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=168)

And still talking about GitHub, time for a more technical news. During GitHub Universe 2021 in October, it has been announced that GitHub Actions will now support OpenID Connect as authentication method to connect to Cloud resources.

The usage of OpenID Connect, OIDC, solves a long standing problem afflicting all the major CI/CD platforms.

![CI CD Credentianls](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/me2wmuebrq7okx010rte.png)

CI/CD workflows are often designed to access a cloud provider in order to deploy software or use the cloud's services.
To access these resources, the workflow will supply credentials, such as a passwords or tokens, to the cloud provider. These credentials are usually stored as a secret, and the workflow presents this secret to the cloud provider every time it runs.

But using hardcoded secrets requires you to create credentials in the cloud provider and then duplicate them in GitHub as a secret. With OIDC, you can take a different approach, configuring your workflow to request a short-lived access token directly from the cloud provider.

![OIDC Flow](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0h53k311zjif1ptsu6r2.jpg)

Your cloud provider also needs to support OIDC on their end of course, and you must configure a trust relationship that controls which workflows are able to request the access tokens.

[Other benefits of OIDC are that permissions can be made more granular by configuring conditions for issuing tokens, and that tokens are only valid for a single workflow run, and then automatically expire. This increase security and remove the needs for credentials rotation.

Providers that currently support OIDC include AWS, Azure, GCP, and HashiCorp Vault, and more will be added over time.

### 3. Snyk Extends Tools Portfolio to Drive DevSecOps Adoption

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=269)

Ok, enough talking about GitHub, let's move to the 3rd news and we will still be talking about Security.

During its online annual conference in October, Snyk, one of the leading companies focusing on DevSecOps, announced a massive expansion of their Tools Portfolio.

Snyk Code has added support for support for C++, C#, Elixir, Ruby, PHP and Go.

Snyk Open Source has been extended to provide native integration with Atlassian BitBucket and AWS CodePipeline platforms, while tightening the integrations with DigitalOcean and HashiCorp. Support for package managers Yarn 2 and Poetry has been added, alongside integration with a C++ scanning tool from FossilID

The Snyk Container platform is now integrated with the open source Trivy container scanning tools and with Snyk’s vulnerability database in addition to adding support for container registries such as Quay, GitHub Container Registry, GitLab, Google Artifact Registry and Harbor.

The Snyk infrastructure-as-code platform now also makes it possible to detect configuration issues in Kubernetes manifests in Terraform code in a way that is compatible with cloud platforms from AWS, Azure and GCP.

And finally, Snyk launched both a new free developer security education program, dubbed Snyk Learn, through which developers can attain and measure their level of DevSecOps expertise and Snyk Impact, an effort to foster collaboration among developers involving a wide range of socio-economic issues.

If you want to know more about Snyk and the tools they provide, check out the [complete review I made about their toolset](https://youtu.be/hXiJJUTiLEw)).

### 4. Chaos Engineering With Azure Chaos Studio

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=362)

Next up, a very interesting news about Azure. During Ignite 2021 Microsoft has in fact announced the public preview of Azure Chaos Studio.

As the name hints, with Chaos Studio you can practice chaos engineering, because it enables you to orchestrate fault injection on your Azure resources in a safe and controlled way.

Chaos Studio is a fully-managed service, so it doesn’t require you to do any management or maintenance of the service, and of course it is deeply integrated into Azure, leveraging ARM templates, Azure Policy, Application Insights and Azure AD for RBAC

It uses a fault library that cover several Azure services and replicates real-world scenarios: you can run faults in sequence and/or in parallel, add time delays, and group target resources across regions.

It does even allow to easily stop an experiment and roll back the fault being injected to avoid having more impact to an environment than originally intended.

Chaos Engineering is not always easy to do, and it is especially difficult to do it right (aka without taking down the whole production), so this service is extremely interesting for me and I can't wait to try it out. If you are interested too, consider subscribing because I will soon have a video about this.

### 5. AWS Announced DevOps Guru

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=423)

But Azure is not the only cloud provider that has announced something major in the DevOps space this year. AWS, in fact  announced during their re:Invent conference a new tool called DevOps Guru which should help operations find issues that could be having an impact on an application performance.

![AWS DevOps Guru](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i8d6o1nwjh0wlw1ebu3j.png)

The way it works is that it collects and analyzes data from application metrics, logs, and events to identify behavior that deviates from normal operational patterns.

When it finds a problem, the service can send an SMS, Slack message or other communication to the team and provides recommendations on how to fix the problem as quickly as possible.

![AWS DevOps Guru Stats](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/td3f751rwmcchm3toqj6.png)

This service gives AWS a product that would be competing with companies like Sumo Logic, DataDog or Splunk by providing deep operational insight on problems that could impact your applications.

### 6. Salesforce Makes DevOps for Salesforce

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=482)

Next news is about Salesforce... Now, I know what you are thinking... "Really? Talking about Salesforce in the Top 10 DevOps news for 2021?" Well, it does sound strange, but I think they've actually got something here...

At its online conference  in June, Salesforce  unveiled a DevOps Center pilot that provides a portal through which organizations can track and manage changes to Salesforce applications, including work items and pipelines that should be fully configurable.

In addition, Salesforce added Salesforce Functions to enable developers to deploy code in a serverless environment, using any code... or so they said.

They have also announced a new unified command line interface (CLI) for all its applications, which allows you to work with and automate all of Salesforce and Heroku at the same time, including the new Functions. Also because the only way you have to create those functions is via the CLI.

Finally, Salesforce added an Einstein Automate tool that employs machine learning algorithms to both integrate data and automate workflows.

I've never been a huge fan of Salesforce and Salesforce development in particular, but I think adding more DevOps components and services to the platform is a good thing. What do you think? Let me know in the comments below.

### 7. Docker Desktop No Longer Free

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=566)

In a blog post on the 31st of August, Docker's CEO announced that the use of Docker Desktop in large businesses now requires a Pro, Team, or Business paid subscription. And Large businesses for them means companies with 250 or more employees, or annual revenues higher than $10m.

As part of this announcement, the company has also updated their plans and pricing.

![Docker Pricing](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t3enoatkk645zxun48ns.png)

Docker has renamed its Free plan to "Personal", and while there are no changes to the $5/month Pro and $7/month Teams subscriptions, a new $21/month Business subscription has been created adding features such as centralized management, single sign-on, and enhanced security.

As I've said before in my opinion this news made more noise than necessary, and this is for 2 reasons. First of all, there has been no change in the Docker Engine itself and the Docker CLI, those are still free.

Second, most of the Docker workloads, especially on bigger companies, run on Linux machines, while Docker Desktop supports only Windows and MacOS... so again, not a big deal if you ask me.

### 8. GitLab Removed Its 'Starter' Tier

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=655)

Next up, let's talk about GitLab. At the beginning of the year, in fact, GitLab announced that it would get rid of their cheapest plan.

![GitLab Blog](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fn0sltnl4ez9yedxtygo.png)

In a blog post, GitLab's cofounder and CEO Sid Sijbrandij announced that they were phasing out the Bronze/Starter tier because, and I quote "_The Bronze/Starter tier does not meet the hurdle rate that GitLab expects from a tier_"

![GitLab Reason](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/h66rjfss0ktx07icimr9.png)

In other words, GitLab decided it was not making enough money on the $4.00 user/month subscription.

The effect of the change is that any features in Bronze that are not in the free tier have been moved up to Premium tier, which is almost 5 times more expensive that the Starter tier was.

Luckily the free tier, which in terms of total users is the most popular plan on GitLab, will remain in place, but it only comes with limited CI/CD credits and doesn’t include any support options.

### 9. Jira's Negative Year

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=711)

And still on the negative side, but I promise this is the last bad news, I want to talk about Jira. This is not much of a news, rather a market trend, but 2021 has seen a lot of negative comments and feedback targeting the platform. And I mean a lot.

So much so that someone has even created an entire website dedicated to this, called "_Why Jira Sucks_", which at the time of recording lists the 31 biggest complains Jira users have.

There has even been a video campaign on YouTube in which Jira was personified as an employee of a company and an HR representative was trying to fire them listing all the problems and downsides they have... I have to said that was quite funny to watch, but I felt bad for Atlassian...

![Jira Twitter](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1da8p2wyqe6dmttx9cbf.png)

And the situation on twitter isn't better, with countless tweets of angry and frustrated users that use the platform to express their thoughts.

![Jira Meme](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qp9hzz8xx3jf76hgvaj0.png)

I hope the recent move of Atlassian to basically deprecate the on-prem installations of their products, including Jira, and move the users to their cloud offering will allow them bring more innovation to the platform and fix the problems they have.

### 10. HashiCorp and Terraform Wins

> [Watch this news here](https://youtu.be/2R1nSOBBMuw?t=780)

Alright, last one for this year. And this is about HashiCorp, the maker of Terraform, Vault, and Consul, just to name a few things.

This year has been a great year for HashiCorp.

![HashiCorp Microsoft Partner of the Year](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/avm7t2qm5zdvt0qwdlr3.png)

Not only they have been recognized as the Winner of 2021 Microsoft Open Source Software on Azure Partner of the Year, but also been named #4 on the 2021 Forbes Cloud 100 List.

![HashiCorp Cloud 100](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3k7d6vftqbh5l67o9k9y.png)

Anyway, that was not the news... the news is that in June HashiCorp released the much awaited version 1.0 of Terraform, the de-facto standard multicloud IaC solution.

The GA of version 1.0 of course brings a ton of improvements to the system, including an improved experience for both usage and upgrade, and better interoperability, scalability, and stability.

And with this milestone, Terraform Cloud now has the ability to run checks for third-party Integrations, to enforce security, compliance, and cost management best practices.

### Conclusions

Alright, these were the TOP 10 DevOps Related news of 2021 for me. As I said before, let me know in the comment section below if I've missed something you consider important.

With this, I wish you all a prosperous new year, I hope 2022 will bring you joy.

Once again, thanks for your support to the channel, __all this wouldn't be possible if not for you. You all made my year.__

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

{% youtube 2R1nSOBBMuw %}