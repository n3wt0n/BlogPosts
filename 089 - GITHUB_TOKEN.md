Today I'm gonna tell you everything about the __GITHUB_TOKEN__ in GitHub Actions. You will learn what it is, __how it works__, how to __customize__ its behavior, and how to limit or __change its permissions__.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube jEK07KPEjnY %}

[Link to the video: https://youtu.be/jEK07KPEjnY](https://youtu.be/jEK07KPEjnY)

If you rather prefer reading, well... let's just continue :)

### What is GITHUB_TOKEN

Let's start with what the GITHUB_TOKEN is in GitHub Actions and how it works.

The GITHUB_TOKEN is a __special access token__ that you can use to authenticate on behalf of GitHub Actions. GitHub __automatically creates__ a GITHUB_TOKEN secret for you to use in your workflow, and you can use it to authenticate in a workflow run.

The way this works is that when you enable GitHub Actions in a repository, __GitHub installs a GitHub App__ on that. The GITHUB_TOKEN secret is basically a GitHub App installation access token.

Before each job begins, GitHub fetches an installation access token for the job from that GitHub App. Since the App has access to a single repo, the __token's permissions are limited to the repository__ that contains your workflow. And to make it even more secure, the token expires when the job is finished.

Hope the mechanism is now clearer. Let's quickly see how to use a GITHUB_TOKEN

### Use GitHub Token

There are 2 ways to use the token: from _secrets_ and from the _context_.

```yaml
      - uses: actions/labeler@v2
        with:
          repo-token: ${{ secrets.GITHUB_TOKEN }}
```

In this first example we use the `secrets.GITHUB_TOKEN` to consume it. As mentioned, the secret is automatically generated so you can just use it straight away.

```yaml
      - name: Create a Release
        id: create_release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ github.token }}
```

Here instead we use the GitHub context, which contains the token. Note that the two are equivalent.

### Personal Access Token vs GITHUB_TOKEN

If you are thinking _"why should I use the GITHUB_TOKEN instead of my normal PAT?", remember that a Personal Access Token is always available, so if someone is able to steal that PAT they can potentially do some harm.

The GITHUB_TOKEN instead expires just right after the job is over. So even if someone is able to steal it (which is _almost impossible_), they basically can't do anything wrong.

### Default Permissions

By Default, the GITHUB_TOKEN has a quite comprehensive list of permissions assigned to it.

![Permissions Table](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dhcu0oezj5gcrqbqh0ch.png)

This table shows the permissions granted to the GITHUB_TOKEN by default. Good thing is that people with admin permissions to an enterprise, organization, or repository can set the default __permissions to be either permissive or restricted__. 

### The Permissions UI

So, let's see how we can ___change the permissions___ of the GITHUB_TOKEN to make it even more secure.

Just go to your repository or organization ___Settings___, then click on ___Actions___.

![Permissions UI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/omcns15otneci0mmzmrj.png)

In here you can change the permissions assigned to your token by choosing `Read and Write` (which allows you to access the content and make changes) or `Read-only`.

That is super quick to do, but on the other hand pretty limited. What if I want to assign permissions in a more granular way?

### Granular permissions via YAML

You can use the `permissions` key in the __YAML workflow__ file to modify permissions for the GITHUB_TOKEN for an entire workflow or for individual jobs.

```yaml
permissions:
  contents: write
  pull-requests: write 
  issues: read
  packages: none
```

And you can use all the permissions that are listed in the table above. Additionally, as you can see below, it supports _intellisense_ if you do it in the GitHub interface directly:

![Intellisense](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/29trk400g443p1j2qeyn.png)

> When the permissions key is used, all unspecified permissions are set to no access, with the exception of the metadata scope, which always gets read access.

You can personalize the token permissions either at Job level, or at whole workflow level (or actually both):

```yaml
[...]
permissions:
  contents: write
  pull-requests: write  

jobs:
  job1:
    runs-on: ubuntu-latest

    steps:
      [...]

  job2:   
    runs-on: ubuntu-latest  
    permissions:
      issues: write
    steps:
    [...]
```

### Conclusions

Hope you have now a better understanding about the GITHUB_TOKEN, what it does and how we can set its permissions properly. Let me know in the comment section below if you have any other questions about it.

Also, check out [this video](https://youtu.be/SzrETQdGzBM) where I talk about creating Personal Access Tokens in GitHub.

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

{% youtube jEK07KPEjnY %}