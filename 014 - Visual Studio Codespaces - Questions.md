I've recently made a [video about Codespaces](https://youtu.be/rg0VHA_YZUI) where I went and took a look at what they are and how to use them.

After that video, I've received a lot of questions about __Visual Studio Codespaces__ and __GitHub Codespaces__, so I've decided to put them all together and answer them. Here we have the 7 most common questions I've received about Codespaces.

These are the questions I will be answering to:

1. Are Visual Studio CodeSpaces and GitHub Codespaces the same thing?
2. How much RAM does the browser version consume?
3. Does it work offline?
4. Does it support only GitHub hosted repos?
5. Does it support Visual Studio or only VSCode?
6. Can I customize it or it is fixed out of the box?
7. Can I use custom machines as Codespaces host?

If you have any other questions you want answered, leave me a comment in the section below and I will try my best to answer it.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much more complete than this post.

{% youtube -xCA_7IX2rw %}

If you rather prefer reading, well... let's just continue :)

### Q1. Are Visual Studio CodeSpaces and GitHub Codespaces the same thing?

They are actually very very similar, but somehow a little different.

The two platform are based on the same technology, which, if I was to over simplify it, is just ___VS Code running on Linux___.

One thing that is immediately obvious, even tho I'd say is pretty minor, is the different __theme__.

![GitHub Codespaces theme](https://dev-to-uploads.s3.amazonaws.com/i/zftdzsswcwoi8ky9bo9g.png)

The online browser experience of GitHub Codespaces always starts with the _white GitHub theme_ as we can see here.

![Visual Studio Codespaces theme](https://dev-to-uploads.s3.amazonaws.com/i/v2hwyfo25an14kidn2od.png)

On the other hand the default theme of Visual Studio Codespaces is the _Default Dark+ of VSCode_.

Another difference is that, if you are using Visual Studio Codespaces, before creating an Codespaces Environment you need to create or select a __Plan__, which maps to one of your Azure Subscriptions.

For GitHub, instead, the process is more seamless. You just click on the Code button, and then "Open with Codespaces". If you do not already have a codespace associated with that repo, then GitHub creates one for you and that's it. Nothing else to do on your side.

That also means that, at least at the time of writing this post, you ___cannot choose the size of your environment with GitHub Codespaces___. With VS Codespaces, instead, you can select the size of the machine hosting your environment at creation time and then change it, if you need to, at any point in time for the entire lifespan of your environment.

I think this will change when GitHub Codespaces will be released in GA, but I haven't seen any document or information about it.

Last thing I want to mention is that, for some strange reason, it seems like the "__Terminal__" of GitHub Codespace doesn't allow you do paste anything, wheter you try to use CTRL-V (or Command-V on Mac) or the mouse right click... simply nothing happens.

This instead __works perfectly__ on Visual Studio Codespaces. I guess they will fix this at some point.

### Q2. How much RAM does the browser version consume?

This is a question I've received a lot, and it totally makes sense. Codespaces have been positioned like "_do your coding form anywhere and any device_". And for the any device part, it means even iPad or other tablets, which usually have a limited amount of resources.

Well, good news, since all the computing and elaboration happes on the servers side, __your client doesn't need to be very powerful__. In fact, as we will see in a second, any decent tablet will do.

I've done some tests with Edge and Chrome, opening and working with a NodeJS application and an Aspnet Core one.

I opened only one tab, the one with VS Codespaces, so to be sure nothing else impacted the test.

![Edge Ram](https://dev-to-uploads.s3.amazonaws.com/i/t7nauwoatee4skvvbl99.png)

The maximum utilization across all the tests in __Edge__ was about __375 Mb__ (note that on my system, before opening Codespaces, Edge was consuming about 200 Mb of RAM, so I'd said Codespaces had a max overhead of about 150 Mb).

![Chrome Ram](https://dev-to-uploads.s3.amazonaws.com/i/8j5lozz9qcwn2u657osc.png)

On __Chrome__ instead the max memory usage was about __420 Mb__, with an "empty" Chrome using about 180 Mb, so an overhead of about 240 Mb.

> At the time of writing, __Firefox is not supported in GitHub Codespaces__ and there are some small __limitations__ when using __Safari__ in both Visual Studio Codespaces and GitHub Codespaces which may prevent you to have the full set of features using that browser.

### Q3. Does it work offline?

We need to break this down in 2 different parts: the browser editor, and connecting VS Code to Codespaces.

Of course, if you start already in an offline situation, like let's say on a plane, you won't be able to use either ones.

But what happens if you are working already using Codespaces and the connection stops working?

For testing this scenario, I started working on the laptop with the network connected via cable and the wifi disabled. Then, I've unplugged the network cable and see what happened.

Let's start with the __browser experience__.

![Browser reconnection](https://dev-to-uploads.s3.amazonaws.com/i/kwz0woz3jxk7ugkzsp4p.png)

As you can see here, as soon as I have unplugged the network cable, the application detects it and tries to reconnect to the server.

If you try to "Reload the window" that will fail too and everything will stop working.

But if you click on "Dismiss" you are able to continue _working_. And for working I mean you are able to do some editing, only on the files you have already open, but nothing else.

__No intellisense. And most importantly no file save__.

You can navigate on other tabs, but you cannot do much in there because everything happens on the server.

The debugger seems to be starting, but again that is not happening because as we've said that would require the server to be connected.

So yeah, it doesn't kick you out but __not really usable__.

And what about using __VSCode connected to a codespace__?

![VSCode reconnection](https://dev-to-uploads.s3.amazonaws.com/i/zsyop4kfpa9mgfj0s704.png)

Again, when I unplug the network cable the software catch that, even tho with a little more delay, and prompt for reconnection.

If you decide to go ahead anyway, __same as before__: no other files can be open, no debug, no nothing.

And again, this makes totally sense. All the files are in the cloud, I do not have it on my machine, the intellisense lives in there not on my local VSCode, compilation and debug as well, and so on and so forth.

So, to answer the question, does Visual Studio Codespaces work offline? __I'm afraid it doesn't__. Oh, and same thing for GitHub Codespaces as well, since the technology is the same.

### Q4. Does it support only GitHub hosted repos?

_Yes and no_.

Visual Studio Codespaces's environments can be initialized with a Git repository during creation, either from the UI in both Browser and VSCode, or using a  _devcontainer.json_ file (more on this later).

What this does is just cloning automatically the code from that repository and prepare your environment with that code.
And yes, that Git repository, at the time of writing at least, can be only from GitHub. No other Git provider is currently supported, but work to improve and extend the support for additional hosting providers is ongoing.

But then, when the Codespace environment is created, it support any Git repository.

In fact __you can clone and work with Azure Repo or any other Git hosting provider__ as long as it is reachable from your environment. And this of course works also for Private Git repos.

So, as I said, yes and no. Only GitHub is supported for the initialization, and anyway that is optional, and then you can use any Git provider of choice when in a Codespace.

### Q5. Does Codespaces support Visual Studio or only VSCode?

The version of Codespaces that is currently available supports only VS Code, but there is already a private preview you can sign in for which supports Visual Studio 2019. ([you can sign up here](https://visualstudio.microsoft.com/vs/private-preview/))

However, as far as I know, __the browser experience will still be supported only for a VS Code-like experience__. Which means that you will be able to use Codespaces for Visual Studio 2019 only via a client connection.

After you enable the Connect to Visual Studio Codespaces preview feature you will see a new Connect to a Codespace button in the Start Window and a new Connect to a Codespace command under the File menu.

The Visual Studio client will allow you to create and manage your Codespaces through a guided experience, and of course work on your projects.

Features in Visual Studio generally work the same in a Codespace as they do while working in a local environment. You can edit code, build the application and debug using the same menus, toolbars and shortcuts. Not all Visual Studio features have been enabled work in a Codespace, yet. Features that aren't yet supported in a Codespace will not appear in the UI when connected to Codespace or will appear with an indicator that they are not yet supported.

As for the VS Code experience, when connecting your Visual Studio client to a Codespace all the code, compilation, debugging etc will happen in the cloud, so that enables you to basically have a full VS experience even on computers with low memory or CPU capacity.

> 2 Notes:
>  
> - First, please note that when using Visual Studio 2019 you won't be able to connect to a Codespace running Linux.
> - Second, at the time of recording this video Codespaces are not supported by Visual Studio for Mac yet. The team is working on updating the client, but for the time being if you're on Mac you'd need to use VS Code.

### Q6. Can I customize it or it is fixed out of the box?

Visual Studio Codespaces and GitHub Codespaces are __quite customizable__, and there are few ways to do so. I will not go too much in depth on this, but let me know in the comment section below if you are interested in this so I will try to make new article/video about how to customize your Codespaces.

First and easiest way to customize a Codespace is to use __VSCode extensions__. Since a Codespace is in effect VS Code running remotely, it is compatible with any VS Code extension and works in broadly the same way as it would on your desktop.

If that is not enough, Codespace environments are fully __customizable on a per project basis__. Customization is accomplished by including a ___devcontainer.json___ file in the project's repository.

![DevContainer.json](https://dev-to-uploads.s3.amazonaws.com/i/tcrl3ngoq9oe765lqto0.png)

In this file, you can for example change specific Linux settings, automatically install tools, runtimes and frameworks, open specific ports, setting environment variable, configure editor settings and so on so forth.

One of the properties of the _devcontainer.json_ file allows you to specify a __dockerfile or a container image__ from which Codespaces will create your environment. When a _devcontainer.json_ file isn't included, which is the defaule, or when the image or dockerFile properties are not specified, a general container is provided which contains a big list of runtimes and SDKs.

Last but not least, Codespaces's environments are fully __personalizable on a per user basis__. This is done by referencing a "_dotfiles repo_" at environment creation time.

Dotfiles are files whose filename begins with a dot (.) and they typically contain configuration information for an application. Common examples would be .gitignore and .editorconfig

For Codespaces, you can configure dotfiles in few different ways.

![dotfiles at creation](https://dev-to-uploads.s3.amazonaws.com/i/dji5e7xi2pdkvc4d4reo.png)

In Visual Studio Codespaces, you can link a repo where you have stored your dotfiles to the Codespace at creation as we see here (and this works only with Visual Studio Codespaces, since there is currently no creation UI for the GitHub Codespaces)

You can achieve the same with GitHub Codespace is you have a __public repository named__ ___dotfiles___ in your account.

Remember that this works only with public repos, private _dotfiles_ repositories are not currently supported.

Another way is to associate your dotfiles after environment creation.

![dorfiles after creation](https://dev-to-uploads.s3.amazonaws.com/i/t5k4qfjc1899n68adpns.png)

To do so, just go to the settings, Extensions, Visual Studio Codespaces, and scroll down until you see the dotfiles seciton.

Same things for GitHub Codespaces.

### Q7. Can I use custom machines as Codespaces host?

You sure can. By default, Codespaces provisions fully managed environments that run in Azure. These environments are backed by the full power of Azure (they are always available, quick to create, scalable, etc). 

However, you can also __register your own physical or virtualized environment__ to your Codespaces Plan, and that can be on a dedicated computer, a VM in Azure or anywhere else, or even a laptop if you want.

To register a self-hosted machine, you can use VS Code directly or you can do it via CLI. The only requirement for that target machine is that is must be running VS Code or Visual Studio 2019 on it.

And doing so you will still have access to most of the benefits of Codespaces (for example the use of the browser-based editor) while leveraging your existing infrastructure and customized machines. This is especially useful if your project has some very specific dependency that cannot be installed in the normal hosted version.

### Conclusion

Alright, I think that's enough for today. A lot of info :D.

As I said before, if you still have a question leave me a comment below and I'll try my best to answer it.

And watch the [video about Codespaces Q&A here](https://youtu.be/-xCA_7IX2rw), or take a look at the [Codespaces - First Look here](https://youtu.be/rg0VHA_YZUI)
