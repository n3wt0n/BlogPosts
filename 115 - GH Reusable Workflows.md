Thanks to the new GitHub Actions feature called "___Reusable Workflows___" you can now reference an existing workflow with a single line of configuration rather than copying and pasting from one workflow to another.

Basically __GitHub Actions Templates on steroids__!

### What Are Reusable Workflows

So, Reusable Workflows in GitHub Actions. Thanks to this feature you can now reference an entire Actions workflow in another workflow, like if it were a single action.

This new feature builds on top of the Composite Actions introduced a while back. If you don't know what Composite Actions are, check [this post](https://dev.to/n3wt0n/github-composite-actions-nest-actions-within-actions-3e5l) or [this video](https://youtu.be/4lH_7b5lmjo), but in short they are __one or more steps packaged together__ which can be then referenced in an Actions workflows by a single line.

Reusable Workflows extend this concept, allowing you to __reference an entire workflow in another one__. If Composite Actions can be thought of as Templates, Reusable Workflows is on another new level.

Right, let's see how to create a reusable workflow.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube lRypYtmbKMs %}

[Link to the video: https://youtu.be/lRypYtmbKMs](https://youtu.be/lRypYtmbKMs)

If you rather prefer reading, well... let's just continue :)

### Create a Reusable Workflow

Reusable workflows are _normal_ Actions YAML files, and as such they have to reside in the `.github/workflows` folder in the root of a repo.

The only particular thing they have to have is a _special trigger_:

```yaml
on:
  workflow_call:
```

The workflow file can also have different triggers, but to make it reusable one of those must be the `workflow_call`.

You can also __pass data__ to a reusable workflow, via the trigger __parameters__ which can be of 2 types:

- inputs
- secrets

The __inputs__ are used to pass _normal_ data (aka not sensitive information):

```yaml
    inputs:
      image_name:
        required: true
        type: string
      tag: 
        type: string
```

In the example above, where I want to use a reusable workflow as template to build and push a Docker Image to a registry, we can see that we have 2 inputs of type `string`, with one required and one not required.

> Note: if a required input has not been passed to the reusable workflow, it will fail 

Other available types are `boolean` and `number`.

The __secrets__, instead, as the name says, are used to pass secret values to the workflow:

```yaml
    secrets:
      registry_username:
        required: true
      registry_password:
        required: true
``` 

In this case you can see that there is no `type`, every secret is treated as string.

Finally, you can use those parameters in your workflow by using `{{inputs.NAME_OF_THE_INPUT}}` and `{{secrets.NAME_OF_THE_SECRET}}`.

So, in the abovementioned example where I want to use a reusable workflow to build and push a Docker image to a registry, the reusable workflow will look something like this:

```yaml
name: Create and Publish Docker Image

on:
  workflow_call:
    inputs:
      image_name:
        required: true
        type: string
      tag: 
        type: string
    secrets:
      registry_username:
        required: true
      registry_password:
        required: true

jobs:
  build:
    runs-on: ubuntu-latest

    steps:      
      - uses: actions/checkout@v2
      
      - name: Setup BuildX
        uses: docker/setup-buildx-action@v1

      - name: Login to the Registry
        uses: docker/login-action@v1
        with:
          username: ${{secrets.registry_username}}
          password: ${{secrets.registry_password}}
      
      - name: Set the tag
        run: |
          if [ -z "${{inputs.tag}}" ]
          then
            echo "final_tag=latest" >> $GITHUB_ENV
          else
            echo "final_tag=${{inputs.tag}}" >> $GITHUB_ENV
          fi
      
      - name: Build and Push the Image
        uses: docker/build-push-action@v2
        with:
          context: .
          push: true
          tags: ${{secrets.registry_username}}/${{inputs.image_name}}:${{env.final_tag}}
          
          
  do-something-else:
    runs-on: ubuntu-latest

    steps:
    - run: echo "Hello"
```

Also note that __reusable workflows can have multiple jobs__, as you can see in the example (where the `do-something-else` does nothing, but it is to show it off)

Easy right? One thing to keep in mind is that if the reusable workflow has other triggers apart from the `workflow_call` you may want to make sure it doesn't accidentally run multiple times.

Now that we have our reusable workflow, let's see how to use it in another workflow. And stay with me until the end because I will talk about the __limitations__ of reusable workflows and when they can be useful.

### Using a Reusable Workflow

Now that we have our reusable workflow ready, it is time to use it in another workflow.

To do so, just __add it directly in a job__ of your workflow with this syntax:

```yaml
 job_name:
    uses: USER_OR_ORG_NAME/REPO_NAME/.github/workflows/REUSABLE_WORKFLOW_FILE.yml@TAG_OR_BRANCH
```

Let's analyse this:

1. You create a job with no steps
2. You don't add a `runs-on` clause, because it is contained in the reusable workflow
3. You reference it as `uses` passing:

  - the name of the user or organization that owns the repo where the reusable workflow is stored
  - the repo name
  - the base folder
  - the name of the reusable workflow yaml file
  - and the tag or the branch where the file is store (if you haven't created a tag/version for it)

In my real example above, this is how I'd reference it in a job called _docker_:

```yaml
  docker:
    uses: n3wt0n/ReusableWorkflow/.github/workflows/buildAndPublishDockerImage.yml@main
```

Now of course we have to pass the parameters. Let's start with the __inputs__:

```yaml
    with:
      image_name: my-awesome-app
      tag: $GITHUB_RUN_NUMBER
```

As you can see, we just use the `with` clause, and we specify the name of the inputs.

> Needless to say, the names have to be the same as the ones in the reusable workflow definition.

For the secrets, instead, we use a new `secrets` section:

```yaml
    secrets:
      registry_username: ${{secrets.REGISTRY_USERNAME}}
      registry_password: ${{secrets.REGISTRY_PASSWORD}}
```

And this is it. So the complete example would look like this (you can find it [here](https://github.com/n3wt0n/ActionsTest/blob/main/.github/workflows/reusableWorkflowsUser.yml)):

```yaml
# This is a basic workflow to showcase the use of Reusable Workflows

name: Reusable Workflow user

on:
  workflow_dispatch:

jobs:
  do-it:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v2

      - name: Run a one-line script
        run: echo Hello, world!

  docker:
    uses: n3wt0n/ReusableWorkflow/.github/workflows/buildAndPublishDockerImage.yml@main
    with:
      image_name: my-awesome-app
      tag: $GITHUB_RUN_NUMBER
    secrets:
      registry_username: ${{secrets.REGISTRY_USERNAME}}
      registry_password: ${{secrets.REGISTRY_PASSWORD}}
```

Once again, as you can see the caller workflow can have multiple jobs as well.

If we run the workflow, this is what we get:

![Workflow run](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gklfn5vy2mklzhhcjbs1.png)

You can see in the image that we have the logs for the `do-it` job that is present in the caller, and then for both the jobs in the reusable workflow.
Since those 2 jobs _are run_ within the `docker` job in the caller workflow, they are referenced in the log as `docker / build` and `docker /do-something-else`.

But apart from that, the logs are complete:

![Logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/onltrx96m0d3fxlpffe4.png)

We get __the full details__ of everything that has happened.

### Limitations and Caveats

So, let's start with a few __notes__. First, remember that the Reusable Workflows are currently in __beta__, so things might change by the time they go GA.

Second, for a workflow to be able to use it, a reusable workflow must be stored in the same repo as the call, or in a public repo, or yet in an internal repo with settings that allow it to be accessed.

![Repo access settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/hw795lt2gzplxe64bfrp.png)

Let's talk now about __limitations__. As direct result of what we have just said, reusable workflows stored in a private repository can be used only by other workflows in the same repo.

Also, Reusable workflows __cannot call and consume other Reusable workflows__.

Finally, and this is big one you need to remember, environment variables set at workflow level in the caller workflow are __not passed to the reusable workflow__. So if you need use any of those variables in the reusable workflow, you'll have to pass them to the workflow via the parameters as I've shown above.

### Conclusions

__Reusing workflows avoids duplication__. This makes workflows easier to maintain and allows you to create new workflows more quickly by building on the work of others, just as you do with actions. 

Workflow reuse also promotes __best practices__ by helping you to use workflows that are well designed, have already been tested, and have been proved to be effective. Your organization can build up a library of reusable workflows that can be __centrally maintained__.

Let me know in the comment section below what you think about these new reusable workflows, if and how you plan to use them, and if there is any feature that you think is missing.

You may also want to watch [this video](https://youtu.be/4lH_7b5lmjo) where I talk about the Composite Actions as templates.

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

{% youtube lRypYtmbKMs %}