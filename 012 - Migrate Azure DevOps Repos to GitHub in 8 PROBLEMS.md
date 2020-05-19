Migrating your Git repository from Azure DevOps Repos to GitHub should be easy. But it is not always like that.

We need to take care of Authentication, Clone, Branches, Tags, History... and much more... 

In this video we will takle all this problems and we will succesfully migrate our repo to GitHub (__including full history, branches and tags__)!

Don't worry if you are not overly familiar with Git and it's command line, I will try to be as clear as possible.

And stay with me until the end for a bonus content.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much more complete than this post.

{% youtube SR0L6czMr1A %}

If you rather prefer reading, well... let's just continue :) 

### Problem 1: How to get the code from Azure DevOps

This is fairly easy to do, you just need to have the URL of the repository you want to move over to GitHub. And you need to have access to that repo of course.

The URL is something like in this format:

```
https://dev.azure.com/ORGANIZATION/PROJECT/_git/REPONAME.git
```

To retrieve that, just head over your project repo and you can use the Clone button there.

Now that we have the URL, we can clone the code.

### Problem 2: How to authenticate to your Azure DevOps Git Repo

There are different ways to do so.

You could use the same credentials you use to authenticate to Azure DevOps portal itself, but this would open a browser windows for you to insert username and password. 

If you have to migrate only one repo than I guess this is fine, but if you want to perform multiple migrations, or you are on a machine that it is nor yours you may not want this.

Another option is to genereate new Git Credentials (_in the Clone dialog we used before the get the URL_), and use those instead. Again, not very suitable if you want to automate migrations, also because the credentials may vary from repo to repo.

The way I prefer doing this is with a PAT, __Personal Access Token__. which basically replace both username and password.

To create a PAT simply access your Azure DevOps portal, go to the small icon with the user image next to your picture, and click on Personal Access Tokens.

Here you can create a new Token, and assign specific permissions to it. For the scope of Git Repo migration we'd just need the "Read" permission under "Code".

So now we are ready to get the code.

### Problem 3: How to clone a repository using a PAT?

This is rather easy, just prepend the PAT to the "dev.azure.com" in your url, like this.

```PowerShell
$AzDOPAT = 'PeRsOnAl_AcCeSs_ToKeN_fOr_AzUrE_dEvOpS'
$AzDOOrg = 'ORGANIZATION_NAME'
$AzDOPrj = 'SOURCE_PROJECT_NAME'
$AzDORepo = 'SOURCE_REPOSITORY_NAME'

git clone https://$AzDOPAT@dev.azure.com/$AzDOOrg/$AzDOPrj/_git/$AzDORepo .
```

In this case I use variables to make it more re-usable, but I think you get the general meaning.

Ok, now we have the code, at least

### Problem 4: How to clone all the rest (branches, Tags, etc)?

We could actually do it manually, but let's instead use the git command that does it for us:

```PowerShell
git clone --mirror https://$AzDOPAT@dev.azure.com/$AzDOOrg/$AzDOPrj/_git/$AzDORepo .
```

This is almost the same command we used before, with the exception of the ___--mirror___ flag.

What this does is cloning the repo in a "special state" called mirroring which copies every object in it.

Indeed, the result of that command looks pretty different than the original repo.

Cool, now we have everything we need: code, branches, tags...

### Problem 5: How to link it to the GitHub destination repository?

The cloned repo now only has the reference to the source repository in Azure DevOps. It's called origin.

We need to add another remote repo, which will be the one in GitHub.

First of all we need the URL for GitHub, which is in this format:

```
https://github.com/USERNAME/REPONAME.git
```

or

```
https://github.com/ORGANIZATION/REPONAME.git
```

And this is for both Public and Private repositories, no differences.

Next we need to add this as a new remote.

```PowerShell
$GHUser = 'GITHUB_USERNAME'
$GHRepo = 'GITHUB_TARGET_REPOSITORY_NAME'

git remote add GHorigin "https://github.com/$GHUser/$GHRepo.git"
```

To do so we can use the "git remote add" command.

It needs a name for it, in my case i decided to call it "GHorigin", but it can be anything you want.

And we need to pass to it the GitHub URL we got before.

Again, here I'm using variables to compose the URL but you can pass it directly.

### Problem 6: How to push all the objects to the target repo?

As in one of the previous steps, we could push code, branches, tags, etc, separately with different commands.

But once again, git comes in help:

```PowerShell
$GHPAT = 'pErSoNaL_aCcEsS_tOkEn_FoR_gItHuB'
$GHUser = 'GITHUB_USERNAME'
$GHRepo = 'GITHUB_TARGET_REPOSITORY_NAME'

git push --mirror GHorigin

git push --mirror "https://$GHPAT@github.com/$GHUser/$GHRepo.git"
```

In fact the "--mirror" switch cannot only be applied to the "git clone" command as we have seen before, but that can be applied also to the "git push" as you can see here.

If you have the GitHub credentials stored in your machine, or you want to insert them interactively then you can use the first command and push to the new origin, which in my case is this _GHorigin_.

If instead you want to do this more programmatically, or you don't want to save your credentials, you can use the second command which uses the Personal Access Token instead.

### Problem 7: How to get a Personal Access Token in GitHub?

To create a PAT in GitHub, go to the Settings, then Developer Settings, and finally Personal Access Tokens.

Here you can Generate a new PAT. For migration purposes, we need to assign it proper permissions.

If your repository is public, then select just "_public_repo_". If, instead, you want to push to a private repository, you'd need to select the whole "repo" section.

When you have your PAT, you can use it in that command.

We are almost done, just one more thing.

### Problem 8: This leaves the local repo in an "unusable state"

That's right, the "_git clone --mirror_", as we have seen, clones the repository in its "RAW" format, which then cannot be used as a normal working copy.

If you want to migrate the repo AND then use it as a working copy, I got you covered.

In fact I have created the [Azure DevOps To GitHub Repo Migrator - GitHub Repository](https://github.com/n3wt0n/AzureDevOpsToGitHubRepoMigrator) which contains a few utilities to migrate your Azure DevOps repository to GitHub.

{% github n3wt0n/AzureDevOpsToGitHubRepoMigrator %}

Starting from the Scripts Folder, we have the "migrate-mirror.ps1" script which performs the migration as we have seen before.

But we also have the "migrate.ps1" script which instead migrate the repository and leave it in an "usable" state.

Instead of using the __--mirror__, we clone first the code, then we clone all the remote branches (excluding the HEAD and the master, which we already have)

Then we add the new origin as we have seen before.

After doing that, we push first the code and all the branches with the "--all" switch and then we push the tags using the "--tags" switch

Finally, we remove the source origin and optionally we raname the GitHub origin, which in my case is "GHorigin", to just origin.

And that's it.

In my GitHub repository I've shown there are also some other implementations which allow you to execute your migration in a Docker container, and even run it inside Azure Container Instances. 

Take a look at the video at the top of this post ([here for simpler reference](https://youtu.be/SR0L6czMr1A)) to see those examples more in depth.

### References and Links

- [Github repo with all the examples](https://github.com/n3wt0n/AzureDevOpsToGitHubRepoMigrator)
- [Video with all the explanation and examples](https://youtu.be/SR0L6czMr1A)