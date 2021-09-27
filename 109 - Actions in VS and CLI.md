Today I'm going to show you two very easy ways to create your GitHub __Actions CI__ Workflow for .NET Applications, __without writing a single line of YAML__.

### Intro

Getting started with GitHub Actions may not be always easy. Especially when the alternatives for deployment are so easy (like the right-click publish in Visual Studio, for example). What if we could create our CI workflows with Actions in the same way?

Btw, I'd be curious to know how you create your GitHub Actions workflow. Let me know in the comment section below if you do it directly in the GitHub UI, or in VSCode perhaps with some extension, or however else you do it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube N2ELIqLWz0k %}

[Link to the video: https://youtu.be/N2ELIqLWz0k](https://youtu.be/N2ELIqLWz0k)

If you rather prefer reading, well... let's just continue :)

### The Tools

The first tool we are going to take a look at is __integrated in Visual Studio__, so it works on Windows, while the second one requires the __use of the CLI__ and therefore can be used in MacOS and Linux as well.

Let's jump into VS.

#### From Visual Studio

Doing it from Visual Studio is pretty straight forward.

![Deployment Type](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o9zzkq0tc5qqzdg00zwa.png)

Just right-click on the __Project Name__, select ___Publish__, choose your deployment target, and then you have the new ___Deployment Type__ selection.

You can either deploy directly, as usual, or create a YAML file for the GitHub Actions CI/CD.

After confirmation, Visual Studio will take care of the rest and create the YAML file for you in the `.github/workflows` folder, named as your deployment target.

![YAML Generated](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oefpiafjskopdjgtccqm.png)

As you can see in the image, the workflow takes care of both CI and CD for your application

> If you are on Visual Studio 2019 and you don't see the deployment type selection, make sure the feature is enabled. Go to _Tools > Options > Environment > Preview Features_ and make sure the ___GitHub Actions support in Publish___ is checked.

#### From The CLI

As I've said, the second way I have for you to generate a GitHub Actions Workflow without writing the YAML is using the __dotnet CLI__.

[Tim Heuer](https://timheuer.com) has in fact created an __awesome template__ that generates the workflow files for GitHub Actions from the CLI.

First thing, we need to __install the template__:

```bash
dotnet new -i TimHeuer.GitHubActions.Templates
```

This will add the feature we want to use. Then just execute

```bash
dotnet new workflow
```

in the root folder of your project and you are done.

What you’ll get is a straightforward GitHub Actions workflow to __build and test__ your .NET application. Keep in mind this is a starting point. It’s not going to do everything you might want, but it’s a solid base to build from.

### Conclusions

Cool right? Let me know down below what you think about this, and as I've said before also how you usually create your Actions workflows.

Also, speaking of GitHub Actions, checkout [this video](https://youtu.be/4lH_7b5lmjo), where I talk about creating and using templates.

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

{% youtube N2ELIqLWz0k %}