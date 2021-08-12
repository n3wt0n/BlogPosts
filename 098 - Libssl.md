Have you ever encountered this error when trying to build a dotnet core application in GitHub Actions and Azure Pipelines, or when trying to use .NET Core on Linux?

![Error](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fhc0ujgsdom3z0gcf137.png)

Today I'm gonna tell you why the "`No usable version of the libssl was found`" error happens and show you how to solve it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube EbEzgxLi8YY %}

[Link to the video: https://youtu.be/EbEzgxLi8YY](https://youtu.be/EbEzgxLi8YY)

If you rather prefer reading, well... let's just continue :)

### Why The Error Happens

So first think first, let me tell you why this happens.

.NET Core, among the other things, relies on some __OpenSSL libraries__.

![OpenSSL](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k8muob51x4cdhjj4aiv5.png)

OpenSSL is one of the __most common__ cryptographic libraries used on Linux, and it has multiple versions. Version 1.0 is kind of old, but still heavily used, while 1.1 is the __newer version__ that was _relatively recently released_.  

The problem is that __versions 1.0 and 1.1 are not compatible__. An application that expects 1.0 __cannot__ build against 1.1, nor run against it.

Many Linux distributions are starting to make __OpenSSL 1.1 the new default__ instead of the version 1.0

And here is the problem: ___.NET Core 2.1, and all earlier versions, only support OpenSSL 1.0___.

### How to Solve it

So, how can we fix this? __We have 2 ways__.

#### Upgrade .NET Core version

The simplest one would be to upgrade to a __most recent version__ of .NET Core.

And I'm not talking about major upgrades, you don't need to go all the way to .NET 5.

![OpenSSL .NET Core 2.1](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o15wewlth5f3trj2gg3n.png)

Luckily for us, the .NET team has __updated .NET Core 2.1 to support the version 1.1__ of OpenSSL.

All you need to do is make sure that you are using the __latest minor build of .NET Core 2.1__, which at the time of writing is the _2.1.28_ which has an SDK version of _2.1.816_. And of course

And doing this in Actions or Pipelines is very simple. Just __change the version of .NET Core in the Setup task__ and you are done.

#### Install the Older Version

If for any reason it is not possible for you to use the newer version of .NET Core, there is still one more thing you can do.

Even tho as I've said before Many Linux distributions are starting to make OpenSSL 1.1 the new default, most of them __still have a package for 1.0__. 

So you just need to __find and install that__. 

On CentOS and Fedora for example it's called `compact-openssl10`. For openSUSE, instead, it's `libopenssl1_0_0`. Finally, for Ubuntu and Debian we have the `libssl-dev`.

After installing the older version of the library, __.NET Core will find it__, pick it up and use it automatically.

And this of course can be done locally on your machine, but also on the CI agents in Azure Pipelines and GitHub Actions, __simply using a `script` task or action__.

### Conclusions

Let me know in the comment section below if you have any more questions about fixing this problem.

Also, check out [this video](https://youtu.be/g8tdrB3kbDU) in which I show how to use GitHub Actions with the .NET Framework.

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

{% youtube EbEzgxLi8YY %}
