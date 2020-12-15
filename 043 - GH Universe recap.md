GitHub held their __flagship event__, GitHub Universe 2020, just a couple of days ago and boy it was full of surprises! 

In this post, I will go through all the major announcements and new features presented during the event together with some more information about them.

This is all you need to know about GitHub Universe 2020.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube ZOkwHxJj1oI %}

([Link to the video: https://youtu.be/ZOkwHxJj1oI](https://youtu.be/ZOkwHxJj1oI))

If you rather prefer reading, well... let's just continue :)

Alright, let's jump into the announcements.

### Dark Mode

The first one I wanna talk about is the new Dark Mode. Yes, you've read it right... GitHub finally has its own __official Dark Theme__.

![Dark Mode](https://dev-to-uploads.s3.amazonaws.com/i/zj8t8zp89xcu7b0qkyp3.png)

With this new Dark Mode, which is available in Public Beta, you will be able to change the appearance of your GitHub interface to, as the name says, a darker version

Since the Dark Mode is still in beta, not every section of GitHub is covered by this update. If you want to know more about this, you can take a look at the [video I published recently about it](https://youtu.be/-MoCoijGRAY).

### Discussions

Next one, Discussions.

This is something that has been ___announced a while back___, and it's been in private beta with some large Open Source contributors until now, but now it's __finally released in Public Beta__ for all the Public Repos.

![Discussions](https://dev-to-uploads.s3.amazonaws.com/i/wm477lwy9yd3scivmmmf.png)

Using Discussions instead of Issues, you can have open ended, threaded conversations and discussions. One way to think about it's as a "Stack Overflow type thing", but it's much, much more than that. And it's really a place for software communities on GitHub.

It's great for QA and for __building knowledge__. It is also great for community managers to be able to manage conversations about where the code is going for example, or what features should happen, and, in general, all the other things that really don't belong in issues.

Super excited about this to be finally available in all the public repos. Remember, at this stage this __will not be available in GHEC or on Private Repos__.

### GitHub Actions - Workflow Visualization

Next we are going to talk about a couple of very cool new features around GitHub Actions.

First one, is the __Workflow Visualization__.

Essentially what this is, it provides you a visual graph of how the workflow is progressing in real time.

![Actions Visualization](https://dev-to-uploads.s3.amazonaws.com/i/mcu58krj8oebk4ixw70n.png)

While Actions previously did that with a __live logging__ and you could see all of the code and everything run through (_and by the way that will of course still be available_), this is a little simpler and can also help you identify things that are working in parallel.

There is a summary view to let you easily understand more complex workflows and make it a little easier to see how things are progressing.

And of course, this is __all within the GitHub experience itself__. So it means that you and your developers don't actually ever have to leave, it's easier for you to navigate to your source code or anything else that is within GitHub as well.

![Actions Visualization 2](https://dev-to-uploads.s3.amazonaws.com/i/xzvdv99pzmjz09nv9d0y.png)

And as you can see on the right side of the image, as things start deploying, you can start navigating to the deployment URLs as well. This will open that up for you so __you can see your staging environment__, or wherever else you are deploying, as you go through this

This is a very cool feature. I will soon have a whole video about this so if you are interested you may want to consider subscribing to my [YouTube Channel](https://youtube.com/CoderDave) not to miss that video.

### GitHub Actions - Manual Approvals

And talking about cool new features of GitHub Actions, we will __finally have manual approvals__! This is a feature that has been long requested and basically every organization I talked to wanted this feature to be available so to be able to control the deployment workflow.

![Actions Approval](https://dev-to-uploads.s3.amazonaws.com/i/xibxnljxh4v869tbzunj.png)

So first off, manual approvals are exactly what you think they are: __this features allows either a person or a team to require their approval__ to move a particular deployment workflow forward.

And this is really helpful for teams which have specific ___security or compliance requirements___, but in general for everyone who whishes to have more control over deployment to specific environments.

And not only it gives you control over the deployment, but __everything is audited__ so you will be able to know at any moment what happened, when it happened and who did it.

This new feature will be available only for public repos and in GitHub Enterprise Cloud, __unfortunately private repos in for example the Teams plan won't receive this__.

Once again, stay tuned because I'm planning to make a video about this on my [YouTube Channel](https://youtube.com/CoderDave).

### PR Auto-merge

Another pretty cool new feature, even tho it's somehow minor, it the ability to __automatically merge a Pull Request__ into the base branch.

![PR Auto merge](https://dev-to-uploads.s3.amazonaws.com/i/92q4sc42iyh5ejt4yf0b.png)

Right now when you submit a pull request on GitHub you often have to spend a lot of time waiting for approval, status checks to complete, etc. And then you gotta remember to check back in so that you can actually have the code merged. And if you forget to do that, or if you wait a day or two, sometimes even other changes come in and you have to redo your pull request.

This new feature basically __lets the developer submit a pull request to a code base and mark it to be automatically merged in__ when approved and all the checks have passed.

Of course this is totally optional, but it is a significant time savings and improving experience. And there is a way for repo admins or org admins to disable it if they don't want their PRs to be automatically merged.

### Dependency Review

Let's now change page, and talk a little about ___security___. The first new feature in this category is the Dependency Review.

This new feature, released in beta for the Enterprise Cloud, will automatically __scan your dependencies during a Pull Request__ to detect if any change has been made or any vulnerable or out of date components have been added as part of that PR.

![Dependency Review](https://dev-to-uploads.s3.amazonaws.com/i/8jaqlhag4g1od1q5bcf5.png)

This is super important because currently developers find out about security issues in open source post-merge today, so it is basically an "after the fact" alert. With this instead everything is shifted left and teams will be able to __identify those vulnerabilities as soon as possible__ in the dev flow.

And cool fact: GitHub, with this feature, is the ___first entity in the market___ to provide a native proactive approach for this concept.

### Code Scanning GA

And still talking about security, a quick word on Code Scanning.

Code Scanning is the foundation of the Code Scanning Alert feature, which allows you to detect vulnerability and security issues in your code.

The team did a __terrific job in optimization__, and in fact now the time Code Scanning takes to scan the repo is about 54% lower than before. And also the startup time is greatly reduced.

![Code Scanning GA](https://dev-to-uploads.s3.amazonaws.com/i/yv85ciqtba4zm9whftp9.png)

Moreover, Code Scanning has been in beta for a while and now it is finally released in GA for GHEC and will also be part of the upcoming GHES 3.0

Speaking of which...

### GitHub Enterprise Server 3.0

Let's say welcome to GHES 3.0

This version will be launching on December 16th 2020 and will bring a __ton of innovation__ in the Server space.

![GHES 3](https://dev-to-uploads.s3.amazonaws.com/i/apyytzf2y50x4j024cuc.png)

In fact, it will __ship with all everyone using GitHub Server was waiting for__: Actions, Packages and even Advanced Security. In fact, as we have seen a minute ago, Code Scanning will be included in the GHES 3.0 as well as Secret Scanning.

And as I've said in the [video I made about the new features of the GitHub Mobile App](https://youtu.be/FnUnYC_b8sE), __GitHub for Mobile__ is finally available for GitHub Enterprise Server as well!

### Sponsor for Companies

Lastly, let's talk about Sponsor for Companies.

This will be an opportunity for GitHub's enterprise customers to start __contributing to the projects__ that matter to them.

GitHub has launched this at Universe with some really big names showing some great momentum behind this initiative from companies who have contributed significant dollars to open source to ensure those projects stay healthy and are able to support them over time.

And so sponsors for companies is a __great opportunity for organizations__ to ensure that they can engage securely and they can support those organizations that they depend on

I'm really excited about this, as I see it both as an opportunity to help open source community, but also as an __opportunity to help boost the software supply chain__.

### Conclusion

Alright, that's it for today.

Those were all the most important announcements and new features presented by GitHub at their flagship event GitHub Universe last week. As you have seen, we have some quite cool features coming, __especially for Actions, Security, and the overall development community__.

Let me know in the comment section below what you think about those announcements, and what is your one favorite new feature.

And check out the [video about this on my YouTube Channel: CoderDave](https://youtu.be/ZOkwHxJj1oI)

{% youtube ZOkwHxJj1oI %}
