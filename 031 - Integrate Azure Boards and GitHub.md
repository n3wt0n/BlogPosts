By connecting Azure Boards with GitHub repositories, you enable linking between GitHub commits, pull requests, and issues to work items. You can use GitHub for software development while using Azure Boards to plan and track your work. 

And today we will see how we can do that.

### Intro

Today we will see how we can connect Azure Boards and GitHub. Doing so you will be able to work on your code using all the good __top notch features GitHub offers__, while managing your __work with Azure Boards__ which, to be completely honest, is much more mature and feature-rich than the GitHub Project Boards.

We will not only see how to integrate the two tools, but also some example of using them together.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much ___more complete___ than this post.

{% youtube 8cPP52fRo_s %}

If you rather prefer reading, well... let's just continue :) 

### Connecting

To __connect Azure Boards to GitHub__ you have 2 options:

- doing it from within Azure Boards or, alternatively,
- install and configure the Azure Boards app from GitHub.

Both methods have been streamlined and support authenticating and operating via the app rather than an individual.

When you make the connection from Azure Boards, the list of GitHub repositories correspond to ones that you allow Azure Boards to access. You can limit which repositories Azure Boards can access overall, and limit what a particular project can access or split the management of work across different Azure Boards projects.

While the steps to make the GitHub-Azure Boards connection are different depending on your starting point, the end result is the same.

#### From Azure DevOps

To initiate the integration from Azure DevOps, just go to the _Project Settings_ > _GitHub Connections_ and click on _Connect your GitHub Account_

![Connect from AzDo](https://dev-to-uploads.s3.amazonaws.com/i/1bbe2n7yer701b4az3jd.png)

Once you do that, you will have to authorize the connection and select the repository(ies) to connect with your Board.

Take a look a [the video](https://youtu.be/8cPP52fRo_s) for a step by step demonstration.

#### From GitHub

If instead you want to initiate the integration from the GitHub Side, the easiest way is to browse the _Marketplace_ for the _Azure Boards app_.

![GH App](https://dev-to-uploads.s3.amazonaws.com/i/vasxromhxc5ndcq08imb.png)

In here just click on _Set up a new plan_ and you will be taken through a similar process than before, where you will have to select the repo(s) you want to connect and this time authenticate with Azure Boards.

Once again, [here you have the step by step explanation](https://youtu.be/8cPP52fRo_s).

### Add the Board status to GitHub

Now that we have the tools connected, let's see what we can do with them.

First thing, you can add Markdown syntax to a GitHub repo README.md file to display the __status of your Kanban board__. You do this by adding the syntax you choose from your Kanban board settings.

![Boards status settings](https://dev-to-uploads.s3.amazonaws.com/i/bcwus62km607s8r0duyk.png)

When you do so, remember to __check__ the _Allow anonymous users to access the status badge_ otherwise nothing will be displayed on GitHub.

Just grab the code in the _Sample Markdown_ field and __paste it on your GitHub README file__. The result will be something like this:

![Badge](https://dev-to-uploads.s3.amazonaws.com/i/7p80v867aakog5uz48n2.png)

### Track the work

Finally, let's see how we can track our work between GitHub commits and PRs and Azure Boards Work Items.

The whole point here is to use the __AB#__ notation in your commit messages, Issues and PRs. Doing so, you will have the __full traceability__ between your work in GitHub and your work items in Azure Boards.

Let's say for example that you have a the work item _465_ in Azure Boards you are working on. After writing the code, you just commit to your GitHub Repo and add "__AB#465__" to your commit message. Now __that commit is linked to your work__ item!

![Commit](https://dev-to-uploads.s3.amazonaws.com/i/s6xslskyv0m3xkbg7mjp.png)

Now, let's say you want to open a Pull Request to have code review, and to merge back to your main branch. Just do it and since the commit is already linked, you will have __the PR linked to your work item(s) as well__!

![PR](https://dev-to-uploads.s3.amazonaws.com/i/3wa6nfyynjvjsodkmx7t.png)

Not only the PR is linked, but it's status is reported as 'Open'

Finally, let's merge the PR into your main branch.

![Merge](https://dev-to-uploads.s3.amazonaws.com/i/dnoi58t90z7zkzmfjwso.png)

Now not only __the merge commit is linked as well__, but also the Pull Request status has been changed to 'Closed'

Cool, right?

[Watch the video here for the full demo](https://youtu.be/8cPP52fRo_s).

### Conclusions

What do you think of this? Do you use or plan to use the Azure Boards and GitHub integration? If not, what do you use to manage your work? 
Let me know in the comment section below.