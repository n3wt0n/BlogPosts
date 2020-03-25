GitHub Actions has been released in General Availability in November 2019, and since then the service has seen an incredible growth, making it the second most popular CI tool on GitHub, for both private and public repos.

It has many Starter Template for a lot of different languages, such as .Net Core, Python, Java, Docker, and many more. But unfortunately there is no out of the box Starter Template for the Full .Net Framework.

Nevertheless, today we are going to create a CI workflow for a .NET Framework application, using GitHub Actions.

But before deep diving into the code, let me take a step back and talk a little bit about Actions, because it is much more than a CI system. 

### About GitHub Actions

In fact, it is a very powerful automation engine where actions, defined in YAML files, allow you to trigger workflow processed on any GitHub event, such as code commits, creation of Pull Requests or new GitHub Releases, and more.

To create the workflow you use the Actions, which basically are individual tasks, that you can combine to create jobs and customize your workflow. You can create your own actions, and use and customize actions shared by the GitHub community.

And actually for creating a CI workflow for a .NET Framework project, we have to use both "official" GitHub Actions and community ones.

If you want to know more about GitHub Actions you can take a look [here](https://help.github.com/en/actions)

### Let's do this

Here you have the video with the whole explanation, and of course the end to end creation of the CI with Actions for a .NET Framework Asp.net MVC application.

{% youtube g8tdrB3kbDU %}

### Closing

If you have used before other CI systems, like for example Azure Pipelines, you need to "clear your mind" and start afresh, because the syntax and the logic here, even tho they seem alike, are quite different.

Let me know in the comments what you think about GitHub Actions, and if you have encountered any problem or issue in creating CI workflows, especially for the Full .Net Framework.