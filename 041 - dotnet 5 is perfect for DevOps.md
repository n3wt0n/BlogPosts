.Net 5 has finally reached the __General Availability__ stage last week during the .Net Conf 2020. But is .Net 5 a good framework for DevOps?

Today I want to talk about it, but from a DevOps and CICD standpoint. Let me show you why I think ___.Net 5 is perfect for DevOps___.

### Intro

If you have been following the me he or on my [YouTube Channel](https://youtube.com/CoderDave) for a while, you've probably noticed that most of my examples and demos which require some code are done in .Net. In fact __I've been a .Net developer for years__ and, although I'm proficient in other langugaes like Java, Ruby and Node.js, __.Net is still my favorite language__. However, I have to say that in the past .Net was not super DevOps-friendly, especially in its .Net Framework flavor.

But after using .Net five for a while, and following it GA release last week, Im now convinced that it is just perfect for DevOps and CICD scenarios.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube -2LcsiXLw88 %}

([Link to the video: https://youtu.be/-2LcsiXLw88](https://youtu.be/-2LcsiXLw88))

If you rather prefer reading, well... let's just continue :)

### What is .Net 5?

Alright, lets jump into the topic. Let me start with a __brief introduction__ of what .Net 5 is. If you already now this, feel free to jump to the next section.

So What is .Net 5?

![Release](https://dev-to-uploads.s3.amazonaws.com/i/i3yy08osc06hd053ybz4.png)

It is a __major release__ of .Net, with a broad set of new features and compelling improvements. It’s actually already in active use by teams at Microsoft and other companies, in production and for performance testing.

Most importantly, .NET 5.0 is the first release in the __.NET unification journey__. .NET 5.0 has been built to enable a much larger group of developers to migrate their .NET Framework code and apps to .NET 5.0. It also includes much of the early work in 5.0 so that Xamarin developers can use the unified .NET platform when .NET 6.0 will be released.

Speaking of which, there will be a major release every year, with .Net 6 coming in November 2021, and of course with minor releases if needed.

![Schedule](https://dev-to-uploads.s3.amazonaws.com/i/2f3w8ew5x4vfhbt0w0v7.png)

It is worth noting that __.Net 5 doesn't replace the .Net Framework__, and in fact .Net Framework 4.x is and will still be supported, and there are no plans to migrate WebForms, WCF and Workflow Foundation to .Net 5 or higher.

Also, __.Net 5 doesn't replace .Net Standard__, it will just not be necessary anymore because there won't be different APIs in different flavors of .Net. New application development can specify the net5.0 target framework moniker for all project types, including class libraries and so sharing code between .NET 5 workloads is simplified. And same would be true for .Net 6 and higher.

Alright, now that we have an overview about .Net 5, let see why I think it's perfect for DevOps and CICD.

### 1. .Net Momentum

First of all, .Net in general is __one of the most used frameworks__.

There are more than 2 million active .Net Core developers and more than 5 millions active .Net Developers, and those people would be able to switch to .Net 5 very easily.

Also, .Net Core, which .Net 5 is the evolution of, is the number 1 __most loved framework__ accordingly to the StackOverflow framework for 2 years in a row.

Furthermore, C# (which is the main language used in both .Net Framework and .Net Core) is the 5th most used language on GitHub.

Lastly, Asp.net Core is the number 1 web application platform by performance in the upcoming TechEmpower Benchmarks

![Momentum](https://dev-to-uploads.s3.amazonaws.com/i/pwpmpw6nq84plr4y8ti5.png)

And this without mentioning the more than 40% of the developers new to .Net are students and that the whole .Net project not only is completely Open Source, but is also one of the projects with the highest velocity.

> Put this all together, and you have something truly great for DevOps. Why? A performant framework which developers love and that is well known by the community. Your teams will be happy using it, and you'll be able to quickly find new developers should you need to expand your teams.

### 2. Performances

Speaking about performances, those have been really improved.

![Performance](https://dev-to-uploads.s3.amazonaws.com/i/t81bi6chuh2wwn0xq73l.png)

Not only .Net 5 is over __30% more performant__ on socket on Linux over .Net Core 3.1, which performances were already pretty good, but also the JSON serialization performance has been improved about 20%.

And for a modern application development, especially when talking about MicroServices, .Net 5 gRPC performance has been improved so much that now it __exceeds the one of Go, C++ and Java__.

While RPS (requests per seconds) are important, they are not everything. Most of the time in fact the __performance of an application__ and ultimately the number of machine cores needed to run it __depends on latency__.

The team did an incredible job about it as well, and worked a ton on the Garbage collector of .Net 5, and now the latency is the lowest ever provided by any .Net Framework and .Net Core version.

> Again, this is great for DevOps and especially for the Ops part: __better performance + less latency means less computing power needed in production__ and hopefully less headaches.

### 3. Compilation Time

And talking about compute, there is also less compute needed for CI. __The compiler in fact is now much more optimized, and offer great performances__.

On the right side of the image here we have a small project, which targets .Net Core 3.1 and it is been built by the compiler that ships with the .Net Core SDK version 3.1.404

On the left side instead we have the exact same project, but I've retargeted it to .Net 5 and it's been built by the compiler that ships with the .Net 5 SDK version 5.0.100

![Build Time](https://dev-to-uploads.s3.amazonaws.com/i/7bzviyjejdgl3spp8zxf.png)

As you can see, __the difference is massive__. The .Net Core 3.1 compiler takes more than 2 and a half second in average to build the solution, while the .Net 5 compiler consistently stay below 0.9 seconds.

And in bigger solutions this difference is even greater.

> Not only it builds faster, but __the resources consumed by the compiler in term of CPU and Ram are lower__.

I think we can all agree that the team did a fantastic job here.

### 4. Container Images

Let's stay in the CICD territory, and let's talk about containers.

Containers are of course one of the most important cloud trends and the __.Net team has been investing significantly__ in them. There are a number of improvements in the lower levels of .Net 5 that make it __perfect to run in containers__, but probably the most visible one is the __optimization of the provided container images__.

As part of .NET 5.0, the team has re-based the SDK image on top of the ASP.NET image instead of _buildpack-deps_ to dramatically reduces the size of the aggregate images you pull in multi-stage build scenarios.

![Containers](https://dev-to-uploads.s3.amazonaws.com/i/nyj31jtv5ykywcu3egpw.png)

As you can see in the image, the SDK image size _has been reduced somewhere between 30 and 65 Mb_. But the biggest improvement is in the runtime image.
If you do this as a multi-stage build, your runtime images will be between 4 and 10kb! And this is possible because all the layers you need are already in the SDK image, so you have them already and therefore you __just download and store the manifest__.

With this change, the Asp.Net pull (for example), will be a no-op, because you will have pulled the Asp.Net layers via the initial sdk pull.

This will allow you to __save up to 40% of the storage__ space for your images. You will see significant size wins for Alpine and Nano Server as well with 5.0, for multi-stage builds.

> Smaller images means not only less storage needed, but also __faster pull and therefore faster startup__ of your containerized image when pulling from scratch.

And if you need to run your containers on Windows, we now have Windows Server Core images, in addition to Nano Server.

### 5. Multiplatform

Which brings me to the next point. .Net Core was already multi platform, but .Net 5 is even more multiplatform... it has __the widest OS support of any .Net version before__.

In fact it runs on:

- Windows 7 SP1, 8.1 and 10, on both x86 and x64 architectures and for the first time ever on __Arm64__
- Windows Server and Windows Server Core 2012 R2 and higher, on both x86 and x64, and Nano Server 1809 and higher on x64
- Linux: all the major distributions including Alpine, CentOS, Debian, RedHat, Suse, Ubuntu and more, mostly on the x64 architecture but in some cases supporting also Arm32 and Arm64
- MacOS, from the version 10.13 onwards, on the x64 architecture

This translate to being able to build a .Net 5 application on __virtually any CI agent__, whether it is hosted or self-hosted, physical or virtual, Windows or Linux. And of course it also means that you'll be able to __deploy your application to any of the abovementioned platforms__, for a total flexibility.

> From a DevOps standpoint it also means __you can choose the platform__ you and your team are more familiar with, and that gives you more performances and reliability.

Also, .Net 5 is already available in both Azure Pipelines and GitHub Actions, so you can build it with no problems.

### 6. Single File Applications

Finally, and still talking about CICD, one of my favorite features: ___Single File Applications___.

Single file applications are published and deployed as a __single file__. The app and sll its dependencies are all included within that file.

Even tho Single File Applications were already a think in .Net Core, their __behavior is completely different__. In .Net Core 3.1, in fact, it packages binaries into a single file for deployment and then unpacks those files to a temporary directory to load and execute them. With .Net 5 instead when the app is run t__he dependencies are loaded directly from that file into memory__ (with no performance penalty). A big improvement.

![SFA](https://dev-to-uploads.s3.amazonaws.com/i/7ofel02h5lulz8kcez1i.png)

You can create a Single File Application using either the command line or tools like Visual Studio. You can also configure the single file publishing directly in the project file.

Remember that in .Net 5.0, single file apps can be either _framework-dependent_ or _self-contained_. Framework-dependent single file apps can be very small, by relying on a globally-installed .NET runtime. Self-contained single-file apps are larger (due to carrying the runtime), but do not require installation of the .NET runtime as an installation pre-step and will just work as a result.

> Why Single File Apps are great for DevOps? Well, your CD will thank you. Having to transfer and publish a single file __is much faster and has much less latency__ than doing so with multiple files. And if you're thinking "I can do the same with a zip file", remember that in .Net 5 Single File applications don't have to be unzipped... so again, __faster and more optimized__.

### Recap

So, to recap... Why is .Net 5 great for DevOps?

![Recap](https://dev-to-uploads.s3.amazonaws.com/i/jzj8sdzvwo61za8bfoc1.png)

The __momentum__ of the .Net frameworks and ecosystem is __great__, and the team worked a lot on __performance improvement__. .Net 5 is the most performant .Net ever.

It is also great for CICD, because of __single file applications__, __smaller container images__, and super __fast build__ time.

Finally, it is truly __multiplatform__, being able to run on Windows, Linux and MacOS, on the x86, x64, __Arm32 and Arm64__ architectures.

Remember to [watch the video for a full-length explanation](https://youtu.be/-2LcsiXLw88).

### Conclusion

Alright, that's it for today. Of Course .Net 5 has many other improvements and awesome features, but the ones we have seen today are for me the most important ones when it comes to DevOps and CICD.

What do you think? Let me know in the comment section below what your favorite features are, and if you agree with me in saying that .Net 5 is perfect for DevOps.
