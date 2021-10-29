GitHub's __flagship event__, GitHub Universe 2021, has just closed its virtual doors after 2 days packed of information, announcements, and releases.

In this video I'm gonna go through all the announcements and new features you need to know from the event

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demos__, which to be fair is much ___more complete___ than this post.

{% youtube HJYpzyUsjKc %}

[Link to the video: https://youtu.be/HJYpzyUsjKc](https://youtu.be/HJYpzyUsjKc)

If you rather prefer reading, well... Let's dive straight into the first couple of announcements.

### New Projects

Let's start with the new Projects. GitHub has announced this a while back as part as the _Issues revamp_ that contained also the new Issues Forms, Task lists, etc. But differently from those features, which went live publicly, the new Projects where kept under private beta.

Now this feature graduates from private beta to __public beta__, and as such it will be __available to everyone__.

![New Projects](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/j82j82abidg4a5oipk5k.png)

Built like a spreadsheet, the new projects tables give you a __live canvas__ to filter, sort, and group issues, pull requests, and cards.

You can also extend issues with __custom fields__ with support for text, number, date, and single-select types; filter, sort, and group by any field; and instantly switch between project tables and boards.

![Boards](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v2tsqvj1qtjr9m5f18yd.png)

Differently from the limited beta, in which the new projects were available only for selected organization, with this announcement __Projects will be available for everyone__, including individual users, and it is now possible to also create __public projects__ (before they were only private).

#### Project Automation

And there is also a new __automation__ capability embedded into the new Projects. Before this, to automate a project board and the related issues you had to rely on GitHub Actions.

![Projects Automation](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/c253mahv8xzaz5e1x8b8.png)

Now instead users will be able to simply turn on automation that helps them keep their project boards up-to-date without needing any manual intervention.

#### Cumulative Flow Diagrams

And finally, still talking about issues and projects, GitHub is introducing CFDs - __cumulative flow diagrams__ - into the projects experience.

![Cumulative Flow Diagram](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9t384nws3eybewdxam3z.png)

Thanks to this, users will be able to __visualize__ progress, remaining work, and throughput of a specific project

It is unclear when the chart will be available to everyone, but I can't wait to have it and use it and see what other reports and charts will be available in the future.

### Command Palette

Alright, second announcement that I want to talk about is the Public Beta for the __Command Palette__.

![Command Palette](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gl2juw0njy1tscvceurf.gif)

The Command Palette is a new GitHub surface designed to improve how users navigate around GitHub and execute time saving commands. You can quickly jump to your organizations and repositories, and search within them for pull requests, issues, projects, files, and more. 

You can access the Command Palette using `ctrl + k` on Windows or `command + k` on Mac, and just start typing.

![Command Mode](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7l08njubsp9f1i1h6ldo.png)

And if you then press `>` (greater than) you enter the "___command mode___", where you can execute commands to optimize your workflows, all without lifting your hands from the keyboard.

What do you think of this? ___I love it___, it's really cool. Let me know in the comment below your thoughts.

### New Releases

Next up, let's talk about Releases, because two improvements to the release process on GitHub are generally available. A redesigned UI, and automatically generated release notes.

![Releases UI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hi410kqrn82tbrrxhli6.png)

The __Releases UI refresh__ gives more clarity into what’s included in a given release and recognition for contributors in the community. GitHub has also made pagination significantly better and introduced new search functionality.

![Releases Comparison](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7d4d37ai6m89dt78szt6.png)

And we now have a handy comparison feature right in the UI, to be able to compare 2 releases.

#### Automatically Generated Release Notes

But it is not all, because as I've already mentioned we now also have the possibility to __automatically generate release notes__.

![Automatic Release Notes](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/lp5pcqll3xmkq0xrnuge.png)

This provides an automated alternative to manually writing release notes for your GitHub releases. With automatically generated release notes, you can __quickly generate an overview of the contents of a release__. You can also __customize__ your automated release notes, using labels to create custom categories to organize pull requests you want to include, and exclude certain labels and users from appearing in the output.

You can also customize the automatically generated release notes by creating a template for them. 

![Releases YAML Template](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cveccfzi92mrs8jx3829.png)

This template is a YAML file, as you can see above, which must be called `release.yml` and placed in the `.github` folder in the root of your repo.

### Codespaces

Next series of announcements are about Codespaces. Some are somewhat __minor__, like the support for Codespaces from the __GitHub CLI__ to help integrate Codespaces with user workflows, or the availability (in beta) of __REST APIs to manage Codespaces__. 

I called those minor features, even though I'm sure a lot of users and sysadmins will rejoice for having them, because the next ones I will talk about are even more exciting.

#### Devcontainer Feature Composition

First, the __Devcontainer features__. The name may not be very exciting, but this is huge.

![Codespaces DevContainer](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0oxbs05hn0vn4nkraqjx.png)

To customize your Codespaces experience and include custom tools and other configuration you had to create a `devcontainer.json` file and edit it, perhaps adding different container images and post creation scripts. Which frankly is not the best in terms of user experience. Now, instead, this feature enables users to more easily __install common tools to their devcontainers__ instead of having to manually script the installation in their _Dockerfiles_ or _postCreate_ scripts.

![Feature Composition](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/v6l1k66awtmbvas03v78.png)

Just add a template devcontainer definition through the `Add development container configuration files…` workflow in Codespaces and you will see the new feature selection, which change and depend on the previous selections.

![Features YAML](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/oy37zw64p0a3mhjpyvce.png)

The selected features will be added to a new `features` section of the `devcontainer.json` file and the Codespaces engine will take care of them for you.

This is super cool, but there's more: Codespaces users can use the Copilot technical preview

#### Copilot 4 Codespaces

Until now, only users that have been accepted into the private beta were able to use Copilot. Now instead __all Codespaces users can use Copilot__ by installing the Copilot extension in VS Code without having to apply to the Copilot technical preview waiting list.

### Copilot

And speaking of Copilot, we do have some announcements for this service as well.

GitHub in fact announced the support for __more languages__, including Java, __support for additional IDEs__ thanks to the plugin for the JetBrains editors (like _Pycharm_, _IntelliJ_, _WebStorm_, and more), and an enhanced OpenAI model that makes the service __even more accurate__ than it was before.

![Copilot JetBrain Plugin](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/836itv7aw098btesr20u.png)

### Custom Repository Roles

Next announcement will make organization admins happy. GitHub has indeed announced that we now get __Custom Repository Roles__.

![Custom Repo Roles](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vuums8k2ax84ipx46tws.gif)

The Custom Repository Roles feature allows organization admins to __create custom permission levels__ that can be applied to teams, organization members, and outside collaborators. They must inherit from one of the predefined roles but can extend them because you can pick and choose the permissions you want. Custom Repo Roles apply to all repositories in an organization.

![Change Repo Default Role](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wf43z6q241psslfnu7af.png)

And once you have the custom roles, it is even possible to assign one of those as __default role for a repo__.

### Pull Request Merge Queue

Ok, last one. This is an improvement to the Pull Request experience, especially when working on big projects or __busy branches__. It is called __Pull Request Merge Queue__.

![Merge Queue](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xrrj8kqp1045o4mthpj2.png)

Once a pull request has passed all its usual required checks and approvals, instead of the developer trying to merge the pull request (which can turn into a race with other developers --- all trying to avoid the dreaded "your branch is out of date, please update" also triggering a new round of CI checks), the developer simply adds the pull request to the merge queue. The queue then creates a temporary branch with that pull request and the pull requests ahead of it in the queue and triggers CI. Once CI passes, the pull request is merged by fast-forwarding the main branch.

This feature is in a private beta access for organization accounts at the moment, but I hope this will be soon open to more accounts because it's a really good feature for big projects and busy branches.

### Conclusions

Alright, that's it for today. So what do you think of this year's GitHub Universe and of these new features and announcements? Let me know in the comment section below, and also __let me know which is your favorite announcement__.

And if you are into new features, you may also want to watch [this video](https://youtu.be/lRypYtmbKMs), in which I cover the recently announced Reusable Workflows in GitHub Actions.

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

{% youtube HJYpzyUsjKc %}