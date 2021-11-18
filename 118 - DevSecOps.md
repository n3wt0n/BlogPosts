DevSecOps is something we all keep hearing, and everyone says it is __important__. 

But why is it important? And how can we adopt DevSecOps the right way without penalizing any aspect of our workflow, especially in a Cloud Native scenario?

Let's take a look at the __best practices for DevSecOps__, and DOs and DONTs of this practice.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation__.

{% youtube KaoPQLyWq_g %}

[Link to the video: https://youtu.be/KaoPQLyWq_g](https://youtu.be/KaoPQLyWq_g)

If you rather prefer reading, well... let's just continue :)

### A Word About DevOps Transformation

In my role as DevOps Architect I get to work with the biggest, most important, and most strategic Microsoft and GitHub's clients in Asia and Oceania on their __DevOps Transformations__.

And you know that DevOps is a very broad term. So when I say that I work on the DevOps Transformations, the meaning of that really depends on the client. 

![DevOps](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/utrn3rfhr8ke872z51pn.png)

Some companies want to focus more on technical aspects like CI/CD, branching strategies, testing, automation, etc., while others perhaps prefer taking a more theoretical approach and discuss about processes, methodologies, cultural changes, you name it.

But regardless of the approach, more and more often I work with those companies on the __security aspects of DevOps__, what we usually refer to as __DevSecOps__.

### DevSecOps?

Now, even though DevSecOps is a buzzword that we hear constantly, ___I usually don't call it that way___. The reason is simple: giving it another name makes it feel like it is something optional, something one can decide when and if to adopt. But in reality, it is not exactly like that. Let me explain.

#### No Security

We all know this diagram, the classic DevOps representation. If you look closer though, you will notice that there is no mention of "anything security" in it.

![No Security](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2095cougiwe20suvheu3.png)

This of course is "___no good___".

#### Security as an Afterthought

This is why companies often operate in this way, having security __completely detached__ from anything else, siloed, and pulled in after the fact, usually when the piece of software has already been deployed.

![Security as an Afterthought](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fpc80yrs401tzhzjt5lm.png)

I hope we all agree this is still __not a good practice__.

#### Security but Detached

In fact, other companies too realize that it is not how you should operate, so they __bring security closer__ to the other teams and practices. And they call it DevSecOps.

![Security but Detached](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5kzgklv0xzlevkcmralt.png)

While this is certainly __better than the previous model__, I still have a problem with it. Security is still operating independently, somewhat siloed. They may have more visibility on what is happening during development, testing, deployment, etc., but the __security team has yet full responsibility__ on anything security. And this makes it still not a very good model.

#### Security Everywhere

To make it better, to make our software secure and secured, we have to take this a __step forward__.

Security needs to be __integrated__ in the whole flow, and practiced and applied in every single area, from ideation to coding, from testing to deployment, to monitoring.

![DevSecOps](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mp7cyaayvmwzh14k10tf.png)

__Security everywhere and at any time__: this is the key. So, how do we get there? This is where things start getting interesting, because there are multiple steps you can and eventually have to take to implement this properly.

### Shift Left on Security

One of the first things people usually suggest is to __shift left on security__. This is a great advice, but we need to do it the right way.

![SDLC](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ik48mt1wbqsn99e1ur5q.png)

This is the usual, __legacy starting point__ in which we don't have integrated security, and as I've mentioned before the first thing companies usually do is adding security after deployment.

![Security after deployment](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ymkll1cubmmzuajraen9.png)

And this means pentesting, security scanning, bug hunting, etc. Perhaps all in production.

And don't get me wrong, those things are certainly useful. But finding a security bug in production is not a good thing, it is __way too late__.

![Breach Cost](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8j08kl3xi4630s37c8ql.png)

The cost of fixing bugs and security issues increases every time me "_move right_" to the next stage in the DevOps flow, and if we are not able to catch them in time because we only apply security after deployment, __a breach could be catastrophic__.

![Security at Development](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/a6tyx87ywy55wbj3dct5.png)

For this reason we should shift left on security, starting it while in the development phase. But this is not the arrival point, this is __just the beginning__. As I've mentioned before, we should apply this concept __everywhere__.

![Security Everywhere](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/twoouw1irselsjqih739.png)

This means having __security embedded in each and every phase__ of our iterations. Each phase will require different approaches and tools, but we need to have it there.

To do this, it is just not possible to rely only on a central isolated security team. We need a __change in the paradigm__.

### Security as Responsibility

Security has to become a __responsibility of every person__ involved.

![Security for Everyone](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oeb3g9oo3w5svrgefgmv.png)

Product Owners and PMs have to think about the features with security in minds, Developers have to implement those features respecting the security indications, best practices, and guidelines, testers have to test not only for functionality but also for security... and so on so forth, you got the point.

### What About Security Team?

Let's quickly address the elephant in the room. Every time I talk about this with companies and teams, I always get the same question: ___what about the security team? Should we get rid of it?___

The answer of course is "__no__"!

While shifting left on security means that security is now a __responsibility for everyone__, that doesn't mean it's only on them. __Security teams still play a very important role__.

First of all, all the things like penetration testing, RBAC, etc. are still important and should still be performed. 

Additionally, as I've mentioned the development team should follow guidelines, best practices, and procedures... and who's better in __defining them__ than the security team?

![Siloed Security](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jwaavpiusp3b4xhtempr.png)

Security teams have to __pivot their role__ from being the only security-related touch point, to being a __security-focused team helping and supporting__ all the other functions.

![Supportive Security](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oaea5mp9bxdnvpzb30zc.png)

And as always in DevOps, with the ultimate goal of having a big __cross-functional cross-discipline team__ rather then separated teams.

![Integrated Security](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uvif7bb78tbanx9cywak.png)

And by the way this is even more important in a Cloud-first development model, because while it is true that you delegate part of the security to the cloud provider, on the other hand your development and deployment frequency will most likely greatly increase. So __you need to "do security" faster__, and this model will help you scale.

### DevSecOps Practice

Alright, let's talk about some more __concrete practices__ you can adopt for securing your DevOps. (_Noted as I didn't mention DevSecOps?_ 😉 )

#### Security Work in the Backlog

First thing I always recommend is __treating the Security work as if it were normal work__. This means including it in the Backlog, and work on it during the normal sprints or iterations.

![Security Backlog](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/p3sxy1l9erg1xxhd720q.png)

This will help your development team especially at the beginning, because they will __get more familiar__ with the security and technical debt remediation, and they won't have any excuse not to work on those tasks since they are part of the sprint.

Of course, if there is any security incident or bug that needs to be remediated immediately, that will have an exception. But in general, __this should be the rule__.

#### Security Throughout the Process

And once you have it in your work management software as backlog, then you should carry it through your whole process.

![Security Process](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/u6qtu7uhiawggqtagwuh.png)

- Every time you open a Pull Request, there should be a __security scan__ running for it and it should block the PR if vulnerabilities are present. This way, you stop vulnerable code to reach your default branch.
- Then, have the same __scanning in your main CI__, meaning the CI on your default branch, for each push or merge.
- Furthermore, __schedule a scan__ at a fixed interval, perhaps weekly, so you can make sure that your codebase is constantly checked even if you do not commit or merge anything, should new vulnerabilities be discovered in the mean time.
- Finally, __deploy only if all the security tests have passed__, and __deploy across multiple stages__ with gates in place to further test for security and vulnerabilities, aside from proper functionality.

Enabling __progressive exposure__ like I've just described will allow you to identify and fix security vulnerabilities as quickly as possible, and even roll back or roll forward much more easily if you have to.

#### Assume Breach

And speaking of identifying vulnerabilities, there is one __mindset change__ that can help you with that: ___assuming breaches___. There are different ways to do it, but today I want to tell you how we've addressed that in the Microsoft Engineering group working on Azure DevOps.

![Red Blue war games](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vjpdcxjolxvpjisr8oup.png)

As many companies, we started with classic __Red/Blue war games__ to the learn attacks and practice responses. 

But over time we've ended up __eliminating the Blue team__ and shifting even this part left. Which means that now is the engineering team that directly that takes care of it.

![Shift Left](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/85hwmfbcetwdmou14i00.png)

And this approach has helped us __preventing some of the most common issues__ like vulnerabilities in Open Source dependencies, secret leaks, credential theft, and other.

### DevSecOps Everywhere

Let's now quickly take a look back at the general definition of DevOps. The definition that in my opinion best represent DevOps is this one from Donovan Brown:

> DevOps is the union of people, processes, and products to enable continuous delivery of value to your end users.

People, Processes and Products are __the pillars of DevOps__. And so, to have the maximum benefits and results out of DevSecOps, we need to find and apply techniques to each of those 3 pillars.

![DevSecOps Pillars](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/75t96p6l0a2js1ynj279.png)

For once, let's start with the products, which can also be referred to as technologies or tools. There are many things that you can do on this pillar, and some are very dependent on your specific technological landscape. But others are __universal__.

For example, automating as much as possible will take the human error out of the equation. Also, using Infrastructure as code and Config as Code will ensure you reproducibility and security in the configuration as well. Of course, the usage of tools like Static Code Analysis and Application Security Testing, both Static and Dynamic, as soon as possible in the development cycle helps in identifying issues as quickly as possible. And this is especially true if you run those tests in the Pull Request phase. And same considerations apply for other scan types like Credential Scanning or scanning for known vulnerabilities, either in code patterns or dependencies.

But tools alone are not enough, __you need to have Processes__ in place to support this. And those processes can be complex like Secure Development Lifecycle, Thread Modeling and the Red/Blue team exercises, just to name a few, or simpler things like adopting code reviews across the whole organization (of course in this case with emphasis on the security of the code), limiting access to production (which should be virtually non-existing for non-automated tools), adopting progressive exposure as I've mentioned before, and of course doing regular security assessments.

But once again this is not enough. You can have the best tools in the market, and the best processes defined... but __if your people won't use those tools or follow those processes, you won't be successful__.

And for the People, all starts with the __education__: to let the teams embrace a security first mindset, to always assume breach and try to prevent it, and even for more basic things like protecting credentials, whether we are talking about some external service or environment credentials.

People are, as always in DevOps, the __most important part of the equation__. So remember to invest in your people, in your teams, in your company culture.

### Selecting DevSecOps Tools

People are important also when it comes to the selection of the tools. It is incredibly important to find the right __tools that fit your processes and that your people would actually want to use__.

You need for example to find tools that are __Developer friendly__, and that means easy to use, fast, and reliable. If something requires a lot of effort or time to be used or run, then nobody will use it. And if it takes too long to execute, then your builds and CIs will slow down, impacting your cadence.

Another thing you should look into is having tools that can be __used both locally and in a CI system__. This way, the developers can run those tools on their machines, since they are fast (as we said before), before even committing the code to the remote branches and opening their Pull Requests

And since we are talking about security tools, the tools you use __must have a very low false positive rate__. You don't want to waste your time investigating hundreds of false positives. Plus, if you have real issues or vulnerabilities they would be buried under many non-issues and that may make the whole process flawed.

#### Cloud Native and Containers

If you develop in containers, remember to have in place both __application scanning and container image scanning__. This way you can ensure that there are no vulnerabilities in your hidden dependencies, meaning the dependencies that you inherit from the Container Base image itself, and that all the policies are respected. 

![Container Image Scan](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9ul5uidrqa0bqn1khybz.png)

If the container registry you use has an embedded security scanning capability, it is usually a good starting point. But you would still want to have your images scanned __as early as possible__ in your chain.

And still talking about containers, there is something which is very often overlooked: I'm talking about __Kubernetes best practices validation and enforcement__.

There are just a few tools out there to do this (I personally usually use Datree, as I explain in [this video here](https://youtu.be/aM7EVflmEt4)) , but in my opinion it is an __extremely important area__.

The whole concept is to __prevent security issues in production__ by preventing Kubernetes misconfigurations from reaching production. And of course you can do this manually via Code Review, for example, but code reviews are time consuming and, most importantly, they are error prone. If you can automate things like Kubernetes schema validation, and the enforcement of best practices and policies over your Kubernetes manifests, then you will make sure that you can just focus on your application bits.

And, once again, ideally you should find a tool that does this kind of validations in every scenario, including local development environments, and that does it __very quickly and reliably__ to maximize the benefits. (and this is one of the reasons why I use Datree 😉 )

### Recap

Alright, let's wrap this up and let's just recap what we've seen:

- Security is not just for security people, or security teams. It should be everyone's responsibility.
- Apply security everywhere, in every step of your software production flow, and as early and as frequently as possible. This will maximize your chances to identify and solve security issues fast.
- Consider the 3 pillars of DevOps, People, Processes, and Products, and identify areas of improvement in each of them when it comes to security. They are all important, and you need to have solutions for each and every of them.
- Choose the tools that people would want to actually use: fast, easy to use, and reliable.

And finally, __DevSecOps should just be DevOps__. Security should always be embedded in DevOps... so, make it so and you'll soon see the benefits.

### Conclusions

I hope you've found this valuable. Please feel free to reach out to me if you have any questions, just comment down below or check my contacts in the next section.

Also, let me know what you think about my guidelines for an efficient DevSecOps adoption.

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

{% youtube KaoPQLyWq_g %}