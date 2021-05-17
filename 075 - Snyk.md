Ensuring __application security is extremely important__. But usually it's also pretty tedious and definitely not fun.

The tools we use are usually __slow and not very accurate__, and this leads to not using them properly.

Notice that I've said "usually", because I think I've found the __solution__ for it. Or, better, __Snyk has found it__.

Let's dive into it.

> 🌏Check out Snyk at [http://snyk.co/coderdave](http://snyk.co/coderdave)

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__.

> I would __highly recommend__ you to watch the video because is much ___more complete___ than this post, and in there you can see all the products in action.

{% youtube 94AIX5oArIw %}

[Link to the video: https://youtu.be/94AIX5oArIw](https://youtu.be/94AIX5oArIw)

If you rather prefer reading, well... let's just continue :)

### Current Challenges for DevSecOps

To better understand where to position Snyk, we need to take a look at the __current issues we face__. 

There are __many tools__ out there that take care of the different phases of application security, but as I've mentioned in the intro they are __usually pretty slow and not very accurate__. 

And this is a __problem__. In the DevSecOps realm, in fact, you want to __shift left on security__, meaning that you want your code to be scanned and made secure as soon as possible in the development cycle. If the tool you're using is too slow, then it will __waste you precious time during development__ or in the CI for Pull Requests.

Similarly, if the results of the tool are not accurate, for example it returns __too many false positive__ or even worse, if the tool regularly misses potential vulnerabilities, your confidence in the tool itself will decrease.

Because of those aspects, you may end up __not using the tools at all__, exposing your code and application to __greater risks__.

### Snyk is Different

So, what makes Snyk different? First of all, their __philosophy__.

![Snyk](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3l7tl2wf8ruoyepyfnxb.png)

They have a __unique combination__ of developer-first tooling and best in class security depth which enable developers and companies to easily build security into their continuous development process.

And I want to empathize the "___developer-first___" bit. Snyk tools are built for developers from developers. This means they try and solve all the common adoption blockers we have seen before.

Second thing that makes Snyk different is that they provide a comprehensive end to end platform, which they call Cloud Native Application Security platform, which includes basically almost all you need for making your code secure.

This platform includes in fact:

- ___Open Source Security,___  that automatically finds, prioritizes and fixed vulnerabilities in open source dependencies
- ___Code Security___, which we'll explore more in depth later
- ___Container Security___, to find and automatically fix vulnerabilities in your containers
- ___Infrastructure as Code Security___, that focused on issues and vulnerabilities on Terraform and Kubernetes definitions

### Snyk Open Source and Infrastructure as Code

As I've mentioned, we will go in depth into their new Snyk Code a little later in the video, but I want to quickly see what these other tools can do and how they work.

Check out the video for the demo:

{% youtube 94AIX5oArIw %}

> [Demo for this starts at minute 2:52](https://youtu.be/94AIX5oArIw?t=172)

### Snyk Code

Alright, next I wanna talk about the star of the show: __Snyk Code__.

Snyk Code is a Static Application Security Testing tool (__SAST__), but unlike other SASTs in the market which are designed primarily to test applications post-development, Snyk Code is been developed with a __Developers-first approach__, and this means that not only if provides a very user-friendly experience and integration with Dev tools, it is also pretty fast with __near real-time scan results__, and has a __high accuracy__.

It can be all of this because it even __integrates into your IDEs__ like Visual Studio, VSCode, Eclipse and many others (more on this later) and it's __powered by machine learning and AI__. The Snyk Code AI engine learns from millions of open-source commits, and is paired with known issues from Snyk’s Security Intelligence database, creating a continually growing code security knowledge-base.

But enough talking, let's see this in action. We'll see it first on a more "traditional" approach, and the we will push it to its limits.

Check out the video for the demo:

{% youtube 94AIX5oArIw %}

> [Demo for this starts at minute 8:45](https://youtu.be/94AIX5oArIw?t=525)

In the demo I cover:

- Snyk Code Intro at [minute 7:41](https://youtu.be/94AIX5oArIw?t=461)
- Snyk Code Demo at [minute 8:45](https://youtu.be/94AIX5oArIw?t=525)
- Snyk Code for Java at [minute 11:05](https://youtu.be/94AIX5oArIw?t=665)
- Snyk Code for Python at [minute 11:28](https://youtu.be/94AIX5oArIw?t=688)
- Snyk CLI at [minute 12:19](https://youtu.be/94AIX5oArIw?t=739)
- Snyk with GitHub Actions at [minute 15:05](https://youtu.be/94AIX5oArIw?t=905)
- Snyk with Azure Pipelines at [minute 17:23](https://youtu.be/94AIX5oArIw?t=1043)

### Conclusions

Alright, I think that's more than enough for today.

As we have seen, Snyk has a __very comprehensive portfolio of tools__ we can use to secure our code and applications. And __Snyk Code is a very powerful__ addition to the suite. 

I really love we can use it in a more traditional way by adding our repos to it as projects, but also that we can take it a step forward and use it as part of our continuous integration process.

And I think you probably agree with me that its best feature is to be able to __scan the code real time__ so we can shift left on security very easily and integrate it as part of our development workflow, even before committing to our repo.

Let me know in the comment section below what your thoughts are.

> 🌏Check out Snyk at [http://snyk.co/coderdave](http://snyk.co/coderdave)

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