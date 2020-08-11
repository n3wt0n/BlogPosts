Codespace environments, on both Visual Studio Codespaces and GitHub Codespaces, are fully customizable on a per project basis and a per user basis.

Let's see how to customize them using devcontainer, dotfiles, and custom container images.

### Intro

Today we are once again talking about Codespaces.
I already have [a post](https://dev.to/n3wt0n/visual-studio-github-codespaces-questions-answered-5ge7) and 2 videos on this topic, a [First Look video](https://youtu.be/rg0VHA_YZUI) where I explore Visual Studio Codespaces and another one where I [answer the most common questions](https://youtu.be/-xCA_7IX2rw) about both Visual Studio Codespaces and GitHub Codespace. I highly encourage you to check those videos as well after you're done with this post.

Today, instead, we will go ___deeper into Codespaces___, we are in fact going to explore how we can __customize the environments__ based on our needs.

Everything I will talk about works on both __Visual Studio Codespaces__ and __GitHub Codespaces__.

There are __3 main ways__ to customize and personalize a Codespaces environment:

- dot files
- devcontainer.json
- custom container image

We are going through all of them.

### The Video

If you are a __visual learner__, simply prefer to watch and listen instead of reading, or you want to see this in action, here you have the video with the whole explanation, which to be fair is much more complete than this post.

{% youtube MpwK2O9RBaM %}

If you rather prefer reading, well... let's just continue :)

### DotFiles

Let's start with DotFiles.

What are DotFiles and how to use them with Codespaces? I've already covered this in my previous post, but here you have a summary.

Dotfiles are files whose filename begins with a dot (.) and they typically contain configuration information for an application. Common examples would be .gitignore and .editorconfig

For Codespaces, you can configure dotfiles in few different ways.

![dotfiles at creation](https://dev-to-uploads.s3.amazonaws.com/i/dji5e7xi2pdkvc4d4reo.png)

In Visual Studio Codespaces, you can link a repo where you have stored your dotfiles to the Codespace at creation as we see here (and this works only with Visual Studio Codespaces, since there is currently no creation UI for the GitHub Codespaces)

You can achieve the same with GitHub Codespace is you have a __public repository named__ ___dotfiles___ in your account.

Remember that this works only with public repos, private _dotfiles_ repositories are not currently supported.

Another way is to associate your dotfiles after environment creation.

![dotfiles after creation](https://dev-to-uploads.s3.amazonaws.com/i/t5k4qfjc1899n68adpns.png)

To do so, just go to the settings, Extensions, Visual Studio Codespaces, and scroll down until you see the dotfiles section.

I will not go more in depth into how to make dotfiles, there are already plenty of examples on GitHub, post here on Dev and videos on YouTube, just search for dotfiles and you'll find everything you need.

One final note on this. Using dotfiles is referred to as "___per user basis customization___" because, especially if you are on GitHub Codespace, those settings will be applied to all of your environments, every time you create a new one, but that will be __only for you__, other people creating their Codespaces environments on the same projects won't be affected by your dotfiles.

### devcontainer.json

Let's move to the next way to customize your Codespaces environments: the devcontainer.json file.

Differently from the previous one, using _devcontainer.json_ file is a __per-project basis customization__.

You can set up a default configuration for every new codespace for a repository to ensure that all the contributors have the tools and settings they need, and that will __apply to everyone creating a Codespaces environment for that repository__.

The _devcontainer.json_ file can be placed in one of two places in a repository:  

- In the repo root, prefixed with a dot: _{repository-root}/.devcontainer.json_
- Inside a _.devcontainer_ folder , without the "dot" at the beginning of the file name: _{repository-root}/.devcontainer/devcontainer.json_

Oh, and those files support JSON with Comments (__jsonc__)!

Let's take a look at the structure of the file:

```jsonc
{
    // Open port 3000 by default
    "appPort": 3000,
    //"forwardPorts": [1, 2, 3],

    // Install needed extensions
    "extensions": [
      "ms-dotnettools.csharp",
      "ms-azuretools.vscode-azurefunctions",
      "ms-vscode.azure-account",
      "wakatime.vscode-wakatime",
      "davidanson.vscode-markdownlint",
      "github.vscode-pull-request-github",
      "johnpapa.vscode-peacock"
    ],
  
    // Adds VS Code settings.json values into the environment.
    "settings": {
      "peacock.remoteColor": "#0078D7"
    },
  
    // Run Bash script in .devcontainer directory
    "postCreateCommand": "/bin/bash ./.devcontainer/post-create.sh > ~/post-create.log",
  }
```

The settings are quite self-explanatory. You can even execute some _post create_ scripts to further personalize your environment.

Check [the video here](https://youtu.be/MpwK2O9RBaM) for a __full explanation of this file properties__.

Pretty cool right? So every time someone needs to create a new codespaces environment on that repo, they will have __everything they need already configured__!

### Custom Container Image

Last way to customize a Codespaces environment: using a custom container for bootstrapping it.

This is, as you can imagine, the most flexible way to customize your environment, but of course the one which requires the most work.

Using a custom container actually builds on top of the devcontainer.json file method.  
In fact, there is another section of that file that we haven't seen yet which allows to configure the custom container and its properties.

```jsonc
    //CUSTOM CONTAINER SECTION
    "name": "Codespaces",
    "dockerFile": "customImage.dockerfile",
    //image: "repo/image:tag"
    "remoteUser": "codespace",
    "workspaceMount": "source=${localWorkspaceFolder},target=/home/codespace/workspace,type=bind,consistency=cached",
    "workspaceFolder": "/home/codespace/workspace",
    "runArgs": [ "--cap-add=SYS_PTRACE", "--security-opt", "seccomp=unconfined" ],
```

When that section doesn't contain any configuration value, a container with a default image is provided.

![Default image](https://dev-to-uploads.s3.amazonaws.com/i/hlqvl67v5dmi1pe6ywbk.png)

The default image has a number of tools and SDKs installed, including the most popular frameworks like _.Net Core_, _Python_, _Java_, _Node.js_ and many more.

Your custom container, instead, can contain everything and anything you want. This is of course very useful if you are using a framework or SDK that is not present in the standard image, or if you have to install a specific package.

There are of course some set of __prerequisites__ that your custom container must fulfill in order to work with Codespaces.

- The first set is the one from ___VS Code Remote Server___, which basically includes installing Docker, VSCode, and the Remote Development extension pack. [official docs here](https://bit.ly/31ekWJn)
- The second one, instead, is the set of prerequisites for ___Live Share___. Those depends on the Linux distro you use, but are usually just a _few libraries_. [official docs here](https://bit.ly/2DkNWXV)

As long as your image fulfills both of those, you're good to go.

What I'd recommend, at least at the beginning, is to use the __standard CodeSpaces image__ as base image for your own custom one, and then build on top of that (mcr.microsoft.com/vscode/devcontainers/universal:linux)

Once again, [take a look at the video here](https://youtu.be/MpwK2O9RBaM) to __see this in action__.

Cool, isn't it?

One thing to notice is that it is __important__ to keep an eye on the logs on screen whenever you use a new Container image. If anything goes wrong for any reason, in fact, the problem is logged but after just few seconds the screen will just report a generic "Codespaces has failed". If you were not paying attention to the scrolling logs, _you won't be able to understand what happened_ because there is no way, or at least I couldn't find any, to retrieve the creation logs after the fact. 

### Conclusion

Alright, that's it for today.

As I've mentioned at the beginning of this video, those things ___work for both Visual Studio Codespaces and GitHub Codespaces___, since they are basically the same service.

Let me know in the comment section below what you think about these personalization and customization capabilities Codespaces have, and what you are using Visual Studio Codespaces or GitHub Codespaces for.

### References and Links

- [Examples and explanation on Visual Studio Codespaces and GitHub Codespaces customization](https://youtu.be/MpwK2O9RBaM)
- [Visual Studio Codespaces First Look](https://youtu.be/rg0VHA_YZUI)
- [GitHub Codespaces Questions Answered](https://youtu.be/-xCA_7IX2rw)