While I've covered the basics of the Composite Run Steps Actions in this other [post](https://dev.to/n3wt0n/github-composite-actions-nest-actions-within-actions-3e5l) and [video](https://youtu.be/OqJyrZUUGTw), _and therefore I will not go too in depth in those here_, today I will show you one of the most important new features in GitHub Actions in the last 6 months, at least in my opinion: __The possibility to use other Actions in a Composite Action__.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube 4lH_7b5lmjo %}

[Link to the video: https://youtu.be/4lH_7b5lmjo](https://youtu.be/4lH_7b5lmjo)

If you rather prefer reading, well... let's just continue :)

### The Problem and The Solution

Until now, Composite Actions could use only scripts, either inline in the YAML or in separate files. And this of course was pretty limiting.

But now they can instead __reference other Actions as well__, making them the de-facto __equivalent of templates__ in Azure Pipelines, Jenkins, and so on so forth.

And of course this also makes it easy to reduce duplication in your workflows, and it is perfect for repetitive tasks.

### The Scenario

Alright, let's see how we can create Composite Actions that use other Actions, and how to use them. For this example, I wanted to create __something actually useful__. I decided to go with templatizing the Build and Push of a Docker image, which is something I do all the time in my workflows, and represent a __recurrent set of tasks__.

### Create a Composite Action with Actions

First think we have to do is creating an `action.yml` file in the root of a public repo, which will become the "_source_" for our Composite Action.

Next, we can add some metadata.

```yaml
name: "Publish to Docker"
description: "Build a container image and Pushes it to Docker registry"
```

These two lines just add a name and the description, so we know what our Action does.

Next, we need some inputs. We'd need for example the Docker registry username and password, the image name, tags, etc.

```yaml
inputs:
  registry_username:
    description: "Username for image registry"
    required: true
  registry_password:
    description: "Password for image registry"
    required: true
  image_name:
    description: "Name of the image to push"
    required: true
  tag: 
    description: "How to tag the image. Default: latest" 
```

As you can see we can set the inputs as required, or leave them optional (as the tag).

Last part before we can add the actual task, we need to let GitHub know this is a metadata file for composite actions:

```yaml
runs:
  using: "composite"
  steps:
```

### Add the tasks

Alright, we are ready to add our task. How? Well, exactly in the same way you'd do in a normal Actions workflow:

```yaml

      - name: Setup BuildX
        uses: docker/setup-buildx-action@v1

      - name: Login to the Registry
        uses: docker/login-action@v1
        with:
          username: ${{inputs.registry_username}}
          password: ${{inputs.registry_password}}
      
      - name: Set the tag
        shell: bash
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
          tags: ${{inputs.registry_username}}/${{inputs.image_name}}:${{env.final_tag}}
```

The only difference is that you'd need to add the Actions references (_for example `uses: docker/setup-buildx-action@v1`_) manually because there is no marketplace pane on the right side of the screen like you'd have in the Actions workflow.

> ℹ️ Suggestion: if you don't remember all the Actions names, you can compose your tasks in the normal workflow editor, and then copy them over into the Composite Action

Another thing worth noting in the YAML is how you use the value of the inputs: `${{ inputs.image_name }}`

And that's basically all you need to do for creating a Composite Action that uses Actions in it. Just commit and you're good to go.

> 👀 Check out the [n3wt0n/CompositeAction repo](https://github.com/n3wt0n/CompositeAction) to see the whole YAML

### Use the Composite Action in your Workflow

Let's see now how to use our action in a normal workflow.

All you have to do is referencing that Composite Action using the username (or organization account) and the name of the repo:

```yaml
- name: Build and Push the image
  uses: n3wt0n/CompositeAction@main
  with:
    registry_username: ${{secrets.REGISTRY_USERNAME}}
    registry_password: ${{secrets.REGISTRY_PASSWORD}}
    image_name: my-awesome-app
    tag: $GITHUB_RUN_NUMBER
```

In the YAML above, in the `uses` you can see that I reference my Composite Action using my __account name__ (`n3wt0n`), and the __repo name__ (`CompositeAction`). Plus, I need to use a __version__. In this case I used `main`, which means that my workflow will always use the latest version of the Composite Action available on the main branch. If you want to have a ___static version___ instead, you'd have to __create a tag on your repo__ and use that instead of the branch name to version your Composite Action.

Lastly, as you can see you can pass your input values using the `with` keyword

> 👀 Check out the [n3wt0n/ActionsTest repo](https://github.com/n3wt0n/ActionsTest/blob/main/.github/workflows/compositeActionUse.yml) to see the whole YAML

### The Log

Last thing worth mentioning is how the whole thing is printed out in the logs.

![Logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nrhgv9r43fia6vy8paqu.png)

As you can see, we have the `Build and Push the image` task (which is how I called the step that uses my Composite Action) but __we don't have the details of the steps in the Composite Action itself__.

We have however the logs of the steps in the actual log:

![Logs Expanded](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qu6v4r22ixuun8k77m6u.png)

### Conclusions

As you can see, this new capability of the Composite Actions is very useful for __simplifying repetitive tasks__ and to make sure everything needed is included in your workflow with just a single reference.

As I've mentioned before this feature is for me one of the best new additions to GitHub Actions in the past few months. Do you agree with me? Let me know in the comments below.

![Roadmap](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w7iqa30qs1qhk4i5rn76.png)

I also think that when it would be possible to use custom actions from internal and private repositories, which is a feature that is actually planned for the last quarter of this year, as you can see here on the GitHub's public roadmap, this will be even more powerful. Let me know in the comment section below how do you use or plan to use the Composite Actions.

You may also want to watch [this video](https://youtu.be/OqJyrZUUGTw), in which I talk about all the basics of the Composite Run Steps Actions.


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

{% youtube 4lH_7b5lmjo %}