GitHub Advanced Security now supports the ability to analyze your code for vulnerabilities __from third-party CI pipelines__, while previously, instead, this capability was available exclusively with GitHub Actions.

In this post (and video) I will show you how to use Code Scanning to scan a GitHub Repository from an Azure DevOps pipeline using the YAML editor. 

### Intro

Alright, as I've mentioned before, rather than leveraging the native GitHub Actions workflow with the standard “_Set Up Workflow_” experience, today we are going to use an Azure DevOps Pipeline to scan the Code we have in our GitHub repo.

Let's take a look at the steps we would need to perform to integrate GitHub Advanced Security for Code Scanning with Azure DevOps:

![Steps](https://dev-to-uploads.s3.amazonaws.com/i/v6ttrbguv629jq21lrcg.png)

Since the Azure Pipelines Agent I am using is ephemeral, because I'm using the Hosted Agents, I'll have to install the CodeQl package __on each pipeline execution__. If you are using a self hosted agent instead consider pre-installing the package to save time and compute resources.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube ZgR90vWpBQw %}

([Link to the video: https://youtu.be/ZgR90vWpBQw](https://youtu.be/ZgR90vWpBQw))

If you rather prefer reading, well... let's just continue :)

### Download CodeQL

First thing we have to do, as we have seen in the list of steps, is to Download the latest CodeQL dependencies on my agent.

```yaml
- script: |
    wget https://github.com/github/codeql-action/releases/latest/download/codeql-runner-linux
    chmod +x codeql-runner-linux
  displayName: 'Get latest CodeQL package. Install on Agent.'
```

Since this Pipeline runs on Linux, using wget and targeting the latest Linux release I can download all necessary files to my directory. I also change permissions for the downloaded file before I run it.

### Authorizing CodeQL

Next, we need to give that pipeline __full access to our repo__. To do so, we need to create a GitHub Personal Access Token. ([see how](https://www.youtube.com/watch?v=ZgR90vWpBQw&t=172s)).

> For private repositories the token must have the whole `repo` scope. For public repos, instead, the token needs only the `public_repo` and `repo:security_events` scopes.

Then we need to save the PAT as a variable in the Pipeline. Remember to __set it as a secret__. For security sake, I'd recommend you using Azure KeyVault, save the PAT there and reference it into Azure Pipelines.

Now that we have the GitHub Personal Access Token saved in Azure Pipelines, we can initialize CodeQL.

### Initialize CodeQL

Let's initialize the CodeQL Executable and create a CodeQL database for the language detected.

Once again we need to add a script step to our workflow:

```yaml
- script: |
    ./codeql-runner-linux init \
    --repository YOUR_REPO_NAME \
    --github-url https://github.com \
    --github-auth $GITHUB_PAT \
    --config-file .github/codeql/codeql-config.yml 
  displayName: 'Initialize CodeQL Executable and create a CodeQL database'
```

Replace the `YOUR_REPO_NAME` placeholder with the whole name of the repo you want to scan, for example "_n3wt0n/myrepo_"

Also, the `$GITHUB_PAT` is the name of the variable where I've saved the PAT.

If you want to __analyze a compiled language__ like .Net, Java and so on, remember to __execute the build AFTER the CodeQL Init step but BEFORE the Analyze step__.

In fact the init step will create a script for you that you have to execute before building your code in order for CodeQL to be able to monitor the build as well.

### Analyze the repo

Finally, I want to populate the CodeQL runner databases, analyze them, and upload the results to GitHub.

Let's add the final script

```yaml
- script: |
    ./codeql-runner-linux analyze \
	--repository YOUR_REPO_NAME \
	--github-url https://github.com \
	--github-auth $GITHUB_PAT \
	--commit $(Build.SourceVersion) \
	--ref $(Build.SourceBranch)
  displayName: 'Populate the CodeQL runner databases, analyze them, and upload the results to GitHub.'
```

Once again, replace the `YOUR_REPO_NAME` placeholder with the whole name of the repo you want to scan.

Here we also have 2 more parameters:

- __--commit__: this is the SHA of the commit you want to scan
- __--ref__: this is the ___fully qualified ref name of the branch___ you want to scan (_i.e. refs/heads/master_)

In my case I retrieve both parameters from variables, which is an approach I would recommend.

### Conclusion

And that is basically it.

You can now run the Pipelines and, if successful, you should be able to navigate back to your GitHub repository security tab under code scanning to view the results of your scan.

[Check the video for the full explanation and demo](https://youtu.be/ZgR90vWpBQw)

Let me know in the comment section below what you think about this experience. For me, it would of course be even better if we could have native Azure Pipelines tasks instead of having to write shell scripts, but for the time being this work pretty well as well.
