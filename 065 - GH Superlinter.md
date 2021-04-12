GitHub Super Linter allows you to lint almost any code with just a single component. Today I'm going to show you how it works, how to set it up and use it for your code.

### Intro

To me, __GitHub Super Linter is the ultimate linter__, because it allows you to lint almost any kind of code, with a minimal setup.

If you don't know __what a linter is__ and why you should use one, I'd highly recommend you to check out the [previous post](https://dev.to/n3wt0n/what-is-a-linter-and-why-you-should-use-one-linters-explained-hbc) or the [video](https://youtu.be/HDQXWr5TOnI) I've published on the subject.

### What is GitHub Super Linter?

So, first things first... what is the GitHub Super Linter?

GitHub Super Linter __is not just a linter__, it's a very special one. In fact, the Super Linter is __a source code repository that is packaged into a Docker container__ and called by GitHub Actions. This allows for any repository on GitHub.com to call the Super Linter and start utilizing its benefits.

And it doesn't end here. In fact GitHub Super Linter is unique, __it supports many languages__. Usually a linter is developed specifically for a Language, but the Super Linter supports almost every programming and scripting language you can think of. Whether you are using C#, Groovy, Kotlin, Python, GO, JavaScript or even IaC languages like Ansible, Terraform, or ARM, or yet XML, JSON and YAML... this linter has you covered.

![GitHub Super Linter](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fgns60fn8vjkqcejyhv7.png)

To add on this, the end goal of this tool is to:

- Prevent broken code from being uploaded to the default branch (Usually master or main)
- Help establish coding best practices across multiple languages
- Build guidelines for code layout and format
- Automate the process to help streamline code reviews

### How does GitHub Super Linter work?

So, how does this work, you ask. Well, __it's pretty easy actually__. 

When you’ve set your repository to start running this action, any time you open a pull request, it __will start linting the code__ and return via the Status API. It will let you know if any of your code changes passed successfully, or, if __any errors were detected__, where they are, and what they are. This allows you to go back to your branch, fix any issues, and create a new push to the pull request. At that point, the Super Linter will run again and __validate the updated code__ and repeat the process.

You can configure your [__branch protection rules__](https://youtu.be/gUJ52Shwtm0) to make sure all code must pass before being able to merge as an additional measure.

### How to set up the Super Linter

To show how to set up and use the Super Linter, I created a video in which I have a __full demo__:

{% youtube BCrtoZ04L1Y %}

[Link to the video: https://youtu.be/BCrtoZ04L1Y](https://youtu.be/BCrtoZ04L1Y)

> [Click here to jump directly to the demo part](https://youtu.be/BCrtoZ04L1Y?t=175s)

### Customizations for the GitHub Super Linter

Now that we have our Super Linter set up, let's see how we can customize it.

We are going to analyze the use of Environment Variables, template rules files, and using your own rules files.

#### Environment Variables

> [Click here to jump directly to the demo part for the Environment Variables](https://youtu.be/BCrtoZ04L1Y?t=455s)

#### Template Rules and Custom Rules

Let's move to the rules. You can use the GitHub Super-Linter __with or without your own personal rules sets__. This allows for greater flexibility for each individual code base. 

To __use template rules files__ provided by GitHub, you can copy any or all template rules files from the _Templates_ folder of the Super Linter repo into the folder `.github/linters/` of your repository.

If your repository does not have rules files, the Super Linter will anyway __fall back to the defaults rules__ contained in the TEMPLATES folder.

You can of course use those templates as base to develop __your own ruleset__. And as we have seen before, you can use the Environment variables to tell the Super Linter __where your custom rules files are__, if you prefer saving them in a different folder.

#### Other Customizations

There’s __a ton of other customizations__ with flags and templates that can help you customize the Super Linter to your individual repository. Just follow the detailed directions at the [Super Linter repository](https://github.com/github/super-linter) and the [Super Linter wiki](https://github.com/github/super-linter/wiki).

### Conclusions

It is also possible to __use the GitHub Super Linter outside of GitHub__, for example in Azure, Azure DevOps, GitLab and even locally on your machine. Let me know in the comment section below if you want me to make another post or video showing how to do this.

Let me also know what you think about the GitHub Super Linter, I truly love it and I'm using it basically in every repo I have.

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

{% youtube BCrtoZ04L1Y %}