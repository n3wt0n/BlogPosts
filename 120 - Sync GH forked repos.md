Keeping your forked repo in sync with the upstream one is something tedious, and to do it usually we have to use the command line and some git command. 

But today I have for you __3 ways you can make that simpler__ and much less time consuming, and even synchronize them __automatically__!

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube VOakLctEC2Q %}

[Link to the video: https://youtu.be/VOakLctEC2Q](https://youtu.be/VOakLctEC2Q)

If you rather prefer reading, well... let's just continue :)

### 1. Sync from the UI

Right, so the first way you can easily synchronize your forked repo is using the feature GitHub has made recently available __directly in the UI__.

You can just go to the main page of your repo, in the Code Section, and next to the indicator that says if your branch is ahead or behind the source repo, you now have this "Fetch Upstream" button.

[IMAGE 01]

Clicking on that you have the possibility to __compare__ the changes made in the source repo with the ones made in your forked repo, and also to __automatically fetch and merge__ them into your repo.

If the changes from the upstream repository cause conflicts, GitHub will prompt you to create a pull request to resolve the conflicts.

> [Watch the whole demo here](https://youtu.be/VOakLctEC2Q?t=26)

### 2. The new API

Next method I have for you to synchronize your forked repo with the upstream one requires a little more setup, but then it will allow you to keep the repos in sync __automatically__. I'm talking about using the new GitHub `merge-upstream` API. This way is much more flexible than the previous one. 

Using the API, in fact, you can start the synchronization from many different platforms: your CLI, an application you develop to apply governance to your repos, and so on so forth. And as such it will also enable you to automate the whole process, for example using a cron job or a scheduled operation.

For this example I'm gonna use `curl` to invoke the API.

First thing to notice is that this will be a __POST__ operation:

```bash
curl \
  -X POST 
```

Then, we'd need to specify the _GitHub APIs version_ we are targeting, in this case let's use the v3. You need to pass that in a header:

```bash
  -H "Accept: application/vnd.github.v3+json"
```

Next, __authorization__. The `merge-upstream` API requires authentication, of course otherwise everyone would be able to merge somebody else's repos :)

```bash
  -H "Authorization: token YOUR_GITHUB_PAT"
```

Since GitHub is deprecating the use of username and password for API authentication, I'm using a Personal Access Token instead. And this needs to be passed as a header as well.

To know more about how you can authenticate to the GitHub's APIs, check [this link](https://docs.github.com/en/rest/guides/getting-started-with-the-rest-api#authentication).

And [check this out](https://youtu.be/SzrETQdGzBM) to know how to create a PAT in GitHub.

Then we need to pass the __url of the API__: 

```bash
https://api.github.com/repos/USER_OR_ORG/REPO_NAME/merge-upstream
```

It is pretty self-explanatory, you just need the name of your forked repo, and the username or organization name that owns it.

Last step, we need to tell GitHub what __branch__ we want to synchronize with the upstream repo:

```bash
  -d '{"branch":"main"}'
```

In this example I'm telling the API I want to sync the `main` branch but you can specify any branch which is present in both the upstream and the forked repos.

This is how the complete API call looks when invoked using `curl`, using my user account `n3wt0n` and the repo `openhack-devops-team` which I've forked a while back from Microsoft:

```bash
curl \
  -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token PAT_REMOVED_FOR_SECURITY_REASONS" \
  https://api.github.com/repos/n3wt0n/openhack-devops-team/merge-upstream \
  -d '{"branch":"main"}'
```

If everything goes well, and the sync is __successful__, we will see a message like `Status: 200 OK` with a response which will give you all the details of the operation:

```json
{
  "message": "Successfully fetched and fast-forwarded from upstream defunkt:main",
  "merge_type": "fast-forward",
  "base_branch": "defunkt:main"
}
```

If instead there are __conflicts__, the API will return `Status: 409 Conflict` and you will need to solve the conflicts manually before merge.

> [Watch the whole demo here](https://youtu.be/VOakLctEC2Q?t=64)

### 3. Using GitHub Actions

The final method I have for you behind the scenes still uses the new API we have just seen, but it __abstracts__ it to the user making it much easier to use and to automate. So much so that I can say this is my favorite one, also because __it uses GitHub Actions__. 

There are just a few actions that allow you to sync your forked repos, but [this one](https://github.com/marketplace/actions/sync-and-merge-upstream-repository-with-your-current-repository) from [dabreadman](https://github.com/dabreadman) is my favorite because it allows you to use __GITHUB_TOKEN__ rather than your PAT.

The action is __fully configurable__ but the most important parts are the following ones:

```yaml
- name: Sync and merge upstream repository with your current repository
  uses: dabreadman/sync-upstream-repo@v1.0.0.b
  with:
    # URL of gitHub public upstream repo
    upstream_repo: "https://github.com/actions/starter-workflows.git"
    # Branch to merge from upstream (defaults to downstream branch)
    upstream_branch: main
    # Branch to merge into downstream
    downstream_branch: master
    # GitHub Bot token
    token: ${{ secrets.GITHUB_TOKEN }}
```

The actions fields are self-explanatory. The minimum information you need to pass to the action is the original (upstream) repo url you want to sync from, the branch in your forked repo you want to sync to, and the token.

In my case I like to have this run on a schedule, so my repo should be always in sync with the upstream one (unless there are conflicts):

```yaml
on:
  workflow_dispatch:
  schedule: 
  - cron: "0 13 * * 1"
```

I think it should be now clearer why this is my favorite way to sync a forked repo, and also why it's usually my recommendation.  

> [Watch the whole demo here](https://youtu.be/VOakLctEC2Q?t=428)

### Conclusions

Of course if you have to sync just once in a while, using the UI is more than enough. And if you have complex requirements for busy repos or custom apps the API is the way to go. 

But this last one using GitHub Actions is for me __the sweet spot__.

Let me know in the comment section below __how you synchronize your forked repos__ to their upstreams, and if are going to change now that we have this other options.

Also, you may want to check out [this video here](https://youtu.be/msCWg2F4sck), where I talk about using GitHub Actions to __automate everything__.

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

{% youtube VOakLctEC2Q %}