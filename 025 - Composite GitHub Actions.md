When working on CICD, we want to execute a variety of scripts and commands in different languages and shells in a single Action and map those outputs to the GitHub Actions workflow.

We also want to reuse parts of our workflows into other workflows.

Those 2 things are __historically very difficult__ to do in GitHub actions. Well, despair not, today I'm showing you how to do just that, using a new GitHub Actions type that has just been released: __composite run steps__.

### About Composite Run Steps Actions

So, first things first: _What is a composite run steps action_?

A composite run steps action allows you to ___combine multiple workflow run steps within one action___. For example, you can use this feature to __bundle__ together multiple run commands into an action, and then have a workflow that executes the bundled commands a single step using that action.

In simple words, it is a feature that enables you to ___nest actions within actions___.

_Why would you want to do it_?

The most common reason is that you create a sort of __template__ action and then you can reuse it anywhere you need. Another very common one is when you have multiple project and all of them need to follow the same steps in the CICD workflow.

Using the Composite Run Steps you can now write that part once, save it somewhere and use it in any of your actions. And if you need to change that, maybe adding a new step or changing some parameters, you'll __change it once__ in the central location and the change will apply to all the workflows that use it.

### The Video

If you are a __visual learner__, simply prefer to watch and listen instead of reading, or you want to see this in action, here you have the video with the whole explanation.

I'd encourage you to watch it because, to be fair, it is ___much more complete than this post___.

{% youtube OqJyrZUUGTw %}

If you rather prefer reading, well... let's just continue :)

### Supported Properties

For each run step in a composite action, these are the properties that are currently supported:

```yaml
name  
id  
run  
env  
shell  
working-directory  
```

In addition, mapping _input_ and _outputs_ throughout the action are also supported.

### The metadata

First of all, you need to create a __metadata file__.

I prefer creating a new repository to host my composite run steps action, because I like to keep things organized and this also optimize the reusability.  
But you can save the composited actions also in the local repository and reference them from there.

You have to create a file named ___action.yml___ or ___action.yaml___. Other file names are __not__ supported.

The file could look like this:

```yaml
name: 'File Copy'
description: 'Pretends to copy some files and return the number of files copied'
inputs:
  destinationFolder:  # path
    description: 'The folder to copy the files to'
    required: true
    default: '~'
outputs:
  copied-files: 
    description: "Number of files copied"
    value: ${{ steps.random-number-generator.outputs.filesNo }}
runs:
  using: "composite"
  steps: 
    - run: ${{ github.action_path }}/ExecuteSomething.sh
      shell: bash
    - id: random-number-generator
      run: echo "::set-output name=filesNo::$(echo $RANDOM)"
      shell: bash
    - run: ${{ github.action_path }}/CopyFiles.sh
      shell: bash
```

In this file, the properties _name_, _description_, and _runs_ are mandatory.

The _input_ and _outputs_ sections, instead, are optional and are the way we can mut input and outputs from and to the using workflow.

The YAML is quite self explanatory, I just want to point out the `using: "composite"` part because it's what makes this work.

> Check the [video with the full explanation](https://youtu.be/OqJyrZUUGTw) to understand what all the parts in the YAML mean.

Save, commit, and push to the repo.

### Tag time

Before we can use this _"snippet"_ into our actions, we need to __create a Tag and a Release__ for our repo.

You can use whatever tag you like, but this is what will identify your Composite Run Steps, so choose something meaningful.

For this example I'd go with ___v1___

![Alt Text](https://dev-to-uploads.s3.amazonaws.com/i/no3r0n9kgfzqhklq939u.png)

Ok, now we have everything we need. Let's create a composite action.

### Use it in the Composite Run Steps Action

Let's go to Actions, and create a new workflow. Something like this:

```yaml
# This is an example of using Composite Run Steps Actions

name: Composite Example

on: [workflow_dispatch]

jobs:
  copy_files_job:
    runs-on: ubuntu-latest
    name: A job that copy files
    steps:
    - uses: actions/checkout@v2
    - id: myCompositeAction
      uses: n3wt0n/CompositeActionsArchive@v1 
      with:
        destinationFolder: '/whatever/folder'
    - run: echo Files copied ${{ steps.myCompositeAction.outputs.copied-files }} 
      shell: bash

```

As you can see, this is a __normal__ GitHub action. I'm using a ___manual trigger___ ([check this video if you are not familiar with Manually Triggering GH Actions](https://youtu.be/uNYDgUBClYY)), but it can use any trigger you want.

The interesting part is the one in the middle:

```yaml
- id: myCompositeAction
      uses: n3wt0n/CompositeActionsArchive@v1 
      with:
        destinationFolder: '/whatever/folder'
```

As you can see, we are _using_ our metadata file referencing it with the syntax `"account/repo@tag"`.

More or less what you would do when using an Action from the Marketplace.

We are also passing some params as __input__ (using the ___with:___ clause) and we are getting the __output__ out of it (with the usual context, in the form `steps.YOUR_STEP_ID.outputs.YOUR_PARAM_NAME`)

> Once again, check the [video with the full explanation](https://youtu.be/OqJyrZUUGTw) to understand what all the parts in the YAML mean.

And you're basically done!

Not bad right? Making slices of GitHub Actions workflows reusable is a __real game changer__.

### Unsupported features

Some notes.

Since at the time of writing this feature has been released very recently, there are few things which are __not yet supported__. Those include setting conditionals, continue-on-error, timeouts and uses. Although the team is already working on most of those features.

Another thing that is not supported is using secrets on individual steps within a composite action.

Of course, you can still use all of those attributes in workflows that use a composite run steps action.

### Conclusion

Alright, that's it for today. I will have another post and another video when the composite run steps actions will be more mature and gain more of the missing features, so subscribe to [my YouTube channel](https://www.youtube.com/CoderDave?sub_confirmation=1) and stay tuned so you'll not miss them.

Let me know in the comment section below what you think about this new feature, and if you have any question about it.

### References and Links

- [Video with the full explanation about GitHub Composite Actions](https://youtu.be/OqJyrZUUGTw)
- [GitHub Actions Showcase](https://youtu.be/msCWg2F4sck)
- [Video on GitHub Actions for .Net Framework](https://youtu.be/g8tdrB3kbDU)