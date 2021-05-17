Application Security in DevOps is important, but often underrated. So much so that someone has created the DevSecOps word for it. But what does shift left mean? And how to shift left on security?

We will see all of these and more today.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube 94AIX5oArIw %}

[Link to the video: https://youtu.be/94AIX5oArIw](https://youtu.be/94AIX5oArIw)

If you rather prefer reading, well... let's just continue :)

### Meaning of "Shift Left"

First, what is the meaning of "shift left".

Shift left is a __principle__ that focuses on executing a practice, implementing a process, or using a tool __as early as possible__ in the development chain.

![SDLC](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/apwql714x4sp91dkfxt3.png)

It is called "shift left" because the software development lifecycle is commonly represented as a __straight line with multiple phases__.

![Security Traditional](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/eikmp98wgfj0i6ltkfo9.png)

Traditionally, companies apply security just after the deployment, which is on the right side of that flow chart. But the better practice is to do so during development itself.

![Shifted Left](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ovew1gxguiljsr9h2thi.png)

As you can see, since the development phase is on the left of the chart, we "pushed" that arrow to the left... hence shift left.

![Complete](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/muv9mn4ug697wxw9o237.png)

Also notice that this doesn't mean you will do security just once, __it should be applied all the way__ from day one of development to after having your application in production.

And we have seen it for security, but __this can and should be applied to other practices__ as well, like for example testing.

### Benefits of Shifting Left on Security

Moving on... let's talk about the benefits of shifting left on security. There are __several benefits__ that can be obtained by adopting a shift left strategy.

#### Automation

First one is a better automation.

It is in fact __much easier to automate__ security testing and scanning when it runs against the source code, rather than running it on a deployed environment. And there are a lot of tools like SAST, DAST, etc which can help.

And automation of course also means __fewer human errors__, increased coverage and ultimately fewer to __no issues in production__.

#### Time

Another benefit is time... if you apply security for the whole time you are developing and testing, then you have __much more time to discover and fix vulnerabilities__.

If you do so just before going to production or, even worse, after deployment... well, you don't have much time to fix problems and also you have little time to scan and find vulnerabilities.

### What About my Security Team

Let's quickly address the elephant in the room. Every time I talk about this with companies and teams, I always get the same question: _what about the security team_? _Should we get rid of it_?

The answer of course is "no"!

While shifting left on security means that security is now a responsibility of the Development team, that doesn't mean it's only on them. __Security teams still play a very important role__.

First of all, all the things like penetration testing, RBAC, etc are still important and __should still be performed__.

Additionally, the development team should follow __guidelines__, __best practices__, and procedures... and who's better in defining them than the security team?

The big difference here is that, as I've mentioned, __application security is not just responsibility of a security team anymore__, everyone shares it. So much so that I don't actually like to talk about Dev, Ops, and Sec teams like different teams anymore, they should __work together as a single team__ from the very beginning of the development effort till the end.

### How to Shift Left on Security

Now that we have that out of the way, there is one last thing I wanna briefly talk about: how can a company shift left on security.

There is __not single way__ of doing so, of course, but there are few __practices that you should implement__ if you wanna do it.

First of all, add security and vulnerability scanning __as early as possible__ in your development lifecycle. Every time you open a Pull Request, there should be a security scan running for it and it should block the PR if vulnerabilities are present. This way, you stop vulnerable code to reach your main branch. Some tools allow you to scan your code even before committing to your repo, and that would be even better.

Second, have the __same scanning in your main CI__, meaning the CI on your main branch, for each push or merge. 

Furthermore, __schedule a scan at a fixed interval__, perhaps weekly, so you can make sure that your codebase is constantly checked even if you do not commit or merge anything, should new vulnerabilities be discovered in the meantime.

Additionally, you should __treat any remediation or security work as part of your normal backlog__, not as extemporary work. I have a [video dedicated to this](https://youtu.be/_COrbeZMF1k), so check it out after you finish watching this post.

Finally, as I've mentioned, have all your __teams working together__. At the end of the day y'all have the same goal. Developers, Operations and Security should __work together day in day out__. This is the only way to have truly secured software and environments.

### Conclusions

Alright, I think I've covered everything... Don't get me wrong, there is much more to talk about, but at least we have covered the basics.

Let me know your thoughts in the comment section below. I would also like to know how you currently do security where you work.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

{% youtube 94AIX5oArIw %}