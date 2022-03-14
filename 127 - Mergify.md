### The Problem

Merging code into a branch could be a __really time consuming__ task, especially on big projects with many developers, or anyway when you have a big number of Pull Requests that have to be __reviewed, approved, and merged__ in the correct order.

And it’s not just the merge itself... for each pull request you have to decide who the reviewers are, assign the labels, perhaps rebase your branches to the most updated version that was merged in the meantime, and __much more__.

Wouldn’t be nice if we could have a __free automation tool__ which works with any CI, integrates natively with GitHub, and can do for us all the things I’ve just mentioned?

Well, today __I have that very tool__ for you. Let’s talk about it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube jb9wnpqNzEo %}

[Link to the video: https://youtu.be/jb9wnpqNzEo](https://youtu.be/jb9wnpqNzEo)

If you rather prefer reading, well... let's just continue :)

### The Solution: Mergify

What I have for you today is the review of a tool that promises to __revolutionize the way we work with our Pull Requests__ and we do the merges: __Mergify__!

![Mergify](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/scgus7agdk6brjbzhlsz.png)

Mergify is a tool that helps prioritizing, queuing and automatically merging your pull requests, and which can also rebase and update your branches, while commenting, labeling, assigning and closing your pull requests.

If it sounds __really powerful__ it’s because it is.

I know what you're thinking: can’t I do some of these things in GitHub directly? Well, __yes and no__. 

As we will see in a minute, GitHub does have some of same the features that Mergify has, but you need to either activate them manually, or they are __not as powerful__ and complete as the ones in Mergify. Plus, there are many other features that are simply __not present in GitHub__, at least at the time of writing this. You’ll soon see what I mean.

### Mergify Onboarding

Let’s start with quickly seeing how to setup the tool the first time you use it.

All you have to do is going to [mergify.com](https://www.mergify.com/?utm_source=sponsor&utm_medium=social&utm_campaign=CoderDave) and click on sign up. You will then need to insert you GitHub username and password, __Mergify in fact uses the GitHub authentication__, and you’re in. 

To interact with GitHub, Mergify requires the __installation of a GitHub App__. 

![Mergify GitHub App](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d1nzhp8oyfbxfl00brr3.png)

As always happens when installing GitHub Apps, you can __pick and choose the organizations and accounts__ where you want to install the app, and then you can choose if you want it to access all your __repos in that organization__ or only the hand-selected ones.

And when it is done, you’ll be redirected to the Mergify Dashboard where a message will welcome you saying the setup of Mergify on your account is completed, and that to fully utilize the service you should __create a config file__ in the root directory of your repositories with the rules that you want to apply. We will see how to do all of this in just a moment, but let’s go back to the dashboard and see what we have here out of the box.

### Mergify Dashboard

As you can see the dashboard is quite minimalistic.

![Mergify Dashboard](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nn32o61ufeqwf94gtcop.png)

On the left hand side, we have the selection of the __account or organization__ we want to work on. It shows the organizations/accounts where we have installed the app, but we can always add more organizations.

Then we have the __list of repositories__ currently visible to Mergify in the selected account. We can pick the repo we want to work on using the dropdown list, and we can add additional repos if we have enabled only a subset of repositories in the App.

Next is the Application Keys menu, where, as the name says, we can create __API keys__ to be used for integration with other tools that require API access.

We then have the billing section, which we will explore later on when we talk about pricing, and the Usage section, which shows you the __active users__ in your selected repos. It is important to note that, for Mergify, they count __every user that have write access to your repos as a seat__.

We will take a look at the different plans later on, but don’t worry... they do have a __free forever plan__. 

> 🤑 If you decide you like to tool and you want to subscribe to their paid plans, you can use the coupon code `CODERDAVE22` to get __2 months for free for any offer__.

### Initial Configuration and Config Editor

Let’s get now into the beefier stuff about Mergify and let’s configure the first set of rules.

> 🎦 Check out [this part of the video](https://youtu.be/jb9wnpqNzEo?t=282) for a __full demo__.

Mergify relies on a configuration file called `.mergify.yml` in the root of your repo. We can create this from scratch or we can use the `Config Editor` in the UI.

![Mergify Config Editor](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xyjh756jv9kyvmcv3lnn.png)

Just select the repo you want to work on, click on the Config Editor Tab, and there you are with the first default rule.

Let's take a closer look at it:

```yaml
pull_request_rules:
  - name: Automatic merge on approval
    conditions:
      - "#approved-reviews-by>=1"
    actions:
      merge:
        method: merge
```

As you can probably see, the rule is very simple. It will just wait for a PR to be approved from at least 1 reviewer, and then automatically merge it.

Analyzing the YAML we can see the general structure of it. First off, this is a _Pull Request Rule_ (we will see later that there can be different types of rules), it has __name__ (which can be anything we want), some __conditions__ and some __actions__. As you probably thought already, __the actions are executed when the conditions are verified__.

Also you've probably noticed the `#` character in front of the condition. That is part of the _Mergify grammar_ and it means __number__. If we were to use `approved-reviews-by` instead (without #) we would have the list of reviewers.

### Test Your Configuration

One thing I love about Mergify is that it allows you to __test the configuration__ before even creating the config file.

![Config Test](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bae5t8sxwrx4m9p8s21z.png)

Just write in the textbox the number of the PR in that repo which you want to test your configuration rules against, and see the result!

In the example above, you can see that the summary says ___1 potential rule___. This means that the rule we have tested can potentially be applied to that pull request if the conditions apply. This is because the condition specify that the PR must be approved, while it is currently not.

If I were to change the condition to 0 (this wouldn't make sense in practice, but for demo purposes...) and re-test the rule:

![Config test matches](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1jpluepytf52izrhmmba.png)

The rule would be marked as "matching" because all the conditions.

When you are ready to __push your config to the repo__, you can just click on the _Create a pull request with this configuration_ button and... well, I think the button text is descriptive enough :)

> ℹ️ Please note that if a configuration is pushed to a repo and some rules matches already, the actions will be executed immediately

### More Pull Request Rules

Of course, we can write much more complex rules.

```yaml
pull_request_rules:
  - name: Automatic merge on approval PRs targeting README.md
    conditions:
      - "#approved-reviews-by>=1"
      - files=README.md
    actions:
      merge:
        method: merge
```

The rule above, for example, will execute on all and only the PRs that are approved and target the `README.md` file.

As you've probably noticed, by default all the conditions have to match for the actions to be executed. So, what if we want one or the other?

```yaml
pull_request_rules:
  - name: Automatic merge
    conditions:
      - or:
        - "#approved-reviews-by>=1"
        - files=README.md
    actions:
      merge:
        method: merge
```

I can use a "modifier", like you see above, to add an `or` condition to the rule. The rule will now work on all PR that are either approved or target the README.md file.

And in fact, if we try and validate the rule, we can see that the summary looks a little different.

![Any of](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7ro3xymowctoiygjhf9y.png)

You can in fact see that now we have the ___any of___ clause there. And of course we can __nest__ and __combine__ those conditions. Let take a look at this rule:

```yaml
pull_request_rules:
  - name: Automatic merge with and and or
    conditions:
      - and:
        - "#approved-reviews-by>=1"
        - or:
            - files=README.md
            - "#files=1"
    actions:
      merge:
        method: merge
```

What will it do? It will automatically merge all the PRs that are approved and target either a README.md file or target only 1 file (whatever it is).

### Multiple Rules and Multiple Actions

All we have seen so far included a single rule and a single action in that rule. Config files tho can get much more interesting. We can have multiple rules, and each can have multiple actions.

> 🎦 Check out [this part of the video](https://youtu.be/jb9wnpqNzEo?t=694) for a __full demo__.

```yaml
pull_request_rules:
  - name: Automatic merge on approval
    conditions:
      - or:
          - files=README.md
          - "#files=1"
    actions:
      merge:
        method: merge

  - name: Assign to n3wt0n if YAML and label as Enhancement
    conditions:
      - files~=\.yml
      - -closed
    actions:
      assign:
        add_users:
          - n3wt0n
      label:
        add:
          - enhancement
```

Let's analyze this example. First off, we have __two Pull Request rules__. The first one is the same we had before, the second one is a little more interesting.

On the conditions part, we want to target all the PRs that target `.yml` files (this is what the `files~=\.yml` means) and that are __not closed__ (the `-` in front of a condition is equivalent to `not`).

On the actions side, instead, you can see we have __two actions__: `assign` and `label`.

Just as recap, what the rule does is assigning the PR to the user specified and labeling it, for all the PRs targeting YAML files and that are not closed.

![GitHub Labels and Assign](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/q8x8s675aul683qnv7ms.png)

And you can see it executing in the screenshot above.

### Mergify Manual Command

Not bad right, and we’ve __just scratched the surface__ of what this tool can do.

Mergify also exposes a set of __Commands__ that you can trigger by commenting on the pull request.

> 🎦 Check out [this part of the video](https://youtu.be/jb9wnpqNzEo?t=694) for a __full demo__.

You can see the list of those commands on the [Commands page in the docs](https://docs.mergify.com/commands/), but what they do is basically run some action directly without leveraging the rule system.

At the time of writing this article, the available commands are:

- rebase
- update
- backport
- copy
- squash
- refresh

To __execute a command__ all you need to is tagging the mergify bot in the Pull Request comment section and specify a command.

For example, if I want to __update the branch__ associated with a pull request to include all the changes that have been made in the main branch, I will comment this:

```
@Mergifyio update
```

and Mergify will take care of the rest.


![Update Command](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/a9cu8vbdkujmhn2x3ice.png)

### What Else?

Ok enough talking about Pull Request rules... let’s see what other actions and rules we can add to our configuration File.

First thing to mention is that there are 4 main sections of the configuration file: 
- Pull Request Rules 
- Queue Rules -
- Command Restrictions 
- Defaults

And you can have config files with all four of them or as little as just one of them... And anything in between.

We have talked about __Pull Request Rules__ until now. As the name says, they apply to pull requests. You can use them to govern how and when your merges will happen. As we have seen before, those rules need to have a name, some conditions, and some actions to be executed.

#### Command Restrictions

Command Restrictions are... well, as the name says, they allow you to put restrictions on the commands that you can execute via the Mergify bot by commenting on the PRs.

```yaml
commands_restrictions:
  backport:
    conditions:
    - base=main
```

For example, the rule above limits the execution of the `backport` command for pull requests coming from the main branch.

#### Defaults

The __Defaults__ section is used to define default configuration values for actions run by pull request rules and by commands. If the options are defined in `pull_request_rules` they are used, otherwise, the values set in `defaults` are used.

For example, the following configuration

```yaml
defaults:
  actions:
    comment:
      bot_account: Autobot

pull_request_rules:
  - name: comment with default
    conditions:
      - label=comment
    actions:
      comment:
        message: I 💙 Mergify
```

and this one

```yaml
pull_request_rules:
  - name: comment with default
    conditions:
      - label=comment
    actions:
      comment:
        message: I 💙 Mergify
        bot_account: Autobot
```

will produce the same results.

#### Queue Rules

To understand Queue Rules we need first to understand what merge queues are and what problem they solve.

### Merge Queues and The Problem

Imagine that you have repository, you make some changes and you open a PR

![Queue Status 1](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kevppc2qvt8ejrrr02m4.png)

You PR is valid so the CI and all the test pass.

While the pull request is open, another commit is pushed to `main` either directly or from another pull request.

![Queue Status 2](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ik2jqjidgtrwkbp32v07.png)

The tests are run against the main branch by the CI, and they pass as well.

The pull request is still marked as valid by the continuous integration system since it did not change. As there is no code conflict, the pull request is considered as mergeable by GitHub.

![Queue Status 3](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3jmoa303wmcv730yy2lm.png)

When you merge the PR, however, it is possible that the pull request that was once working breaks the main branch. The stalled pull request might introduce regression or breakages into the production system.

Using a merge queue __solves that issue__ by updating any pull request that is not up-to-date with its base branch before being merged. That forces the continuous integration system to retest the pull request with the new code from its base branch.

![Queue Status 4](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/l5pjy252u3thfea6vbct.png)

If a merge queue were being used in the previous example, Mergify would automatically merge the `main` in the base branch. The continuous integration system would have rerun and marked the pull request as failing the test, removing it from the merge queue altogether.

Mergify Queues provide this, but we can even take this a step forward, for example __batching the merges of multiple PRs__ in the correct order, etc.

When multiple pull requests are mergeable, they are scheduled to be merged sequentially, and are updated on top of each other. The pull request branch update is only done when the pull request is ready to be merged by the engine, for example when all conditions are validated.

![Parallel Queue](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/undxpw6inqeavieqlfzh.png)

That means that when a first pull request has been merged, and the second one is outdated like you can see in this image, Mergify will make sure the pull request #2 is updated with the latest tip of the base branch before merging

![Parallel Queue Result](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rwbjyft6hs8875ycyqhp.png)

With this, there's no way to merge a broken pull request into the base branch.

### Queue Rules

Now that we have seen this in theory, let’s see how to configure and use merge queues in Mergify.

> 🎦 Check out [this part of the video](https://www.youtube.com/watch?v=jb9wnpqNzEo&t=1100s) for a __full demo__.

Let's start with a simple example. This set of rules gives us the ability to enqueue our PR merges based on conditions.

```yaml
queue_rules:
  - name: CoderDave_queue
    conditions:
      - check-success=My CI Job

pull_request_rules:
  - name: Merge using the merge queue
    conditions:
      - base=main
      - "#approved-reviews-by>=2"
      - check-success=My CI Job
    actions:
      queue:
        name: CoderDave_queue
```

On the upper part we have the queue definition, and the condition for auto-merge (in this case the success of the _My CI Job_). Then we have a rule with the action of type `queue`: this will send to the queue all the PRs that match the conditions.

This gives you a general idea of how this works: you need to define queues and have conditions to decide which PRs to enqueue.

Let's take a look at another, more complex example of a Queue Rule.

```yaml
queue_rules:
  - name: urgent
    conditions:
      - check-success=My CI Job

  - name: default
    conditions:
      - check-success=My CI Job

pull_request_rules:
  - name: move to urgent queue when 2 reviews and label urgent
    conditions:
      - base=main
      - "#approved-reviews-by>=2"
      - label=urgent
    actions:
      queue:
        name: urgent

  - name: merge using the merge queue
    conditions:
      - base=main
      - "#approved-reviews-by>=2"
      - check-success=My CI Job
      - label!=urgent
    actions:
      queue:
        name: default
```

In this case we have __two queues__: urgent and default.

The concept here is to be able to enqueue PRs base on their priority (for example _hotfixes_ vs _features_), based on their label. If a PR is labeled as _urgent_ then it will be sent to the _urgent_ queue, otherwise it will be sent to the other queue. In this case, the urgent PRs will be merged more quickly because, if you look at the rule, they require the CI to pass only while in the queue. The normal PRs, instead, need the CI to be successful also as prerequisite for them to be enqueued.

Finally, let's talk about another feature that is part of the Queue Rules, and that makes __Mergify offering quite appealing__. I'm talking about the __Speculative Checks__.

If your continuous integration system takes __a long time__ to validate the enqueued pull requests, it might be interesting to enable speculative checks. This will allow Mergify to __trigger multiple runs of the CI in parallel__. In the following example, by setting the `speculative_checks` option to 2, Mergify will create up to 2 new pull requests to check if the first three enqueued pull requests are mergeable.

```yaml
ueue_rules:
  - name: default
    speculative_checks: 2
    conditions:
      - check-success=My CI Job

pull_request_rules:
  - name: merge using the merge queue and speculative checks
    conditions:
      - base=main
      - "#approved-reviews-by>=2"
      - check-success=Travis CI - Pull Request
    actions:
      queue:
        name: default
```

Multiple pull requests can be checked within one speculative check by settings `batch_size`.

For example, by `settings speculative_checks: 2` and `batch_size: 3`, Mergify will create two pull requests: a first one to check if the first three enqueued pull requests are mergeable, and a second one to check the three next enqueued pull requests.

```yaml
queue_rules:
  - name: default
    speculative_checks: 2
    batch_size: 2
    conditions:
      - check-success=Travis CI - Pull Request

pull_request_rules:
  - name: merge using the merge queue and speculative checks
    conditions:
      - base=main
      - "#approved-reviews-by>=2"
      - check-success=Travis CI - Pull Request
    actions:
      queue:
        name: default
```

At this point, I should mention that both the multiple queues and speculative checks features are not present in the free plan, they are part of the paid plans.

> ℹ️ It is also important to note that, in general, a PR will be automatically removed from a queue if the conditions don't match anymore. For example, if one of the conditions is that the PR must be approved and someone removes the approval, that PR will be taken off the queue (if it has not been already merged, of course)

### Pricing and Save Some Money

Finally, let’s talk about prices and how you can save some money on Mergify.

As I’ve mentioned before, they do have a __forever free plan__ you can use for your repositories, and that covers the use on public repos with unlimited actions and rules, and even basic merge queues.

If you want more, like using Mergify on private repos, advanced queue features, batch merge or even having a dedicated bot account to act on your behalf, you can subscribe to one of their [paid plans](https://mergify.com/pricing?utm_source=sponsor&utm_medium=social&utm_campaign=CoderDave). And as I’ve mentioned before, if you want to get __2 months off__ any of their paid plans you can use the code `CODERDAVE22` (all uppercase) at purchase. But be quick because this is valid __only for the first 50 people__ who will use it.

### Mergify Startup Program

And if you are part of a startup it gets even better, because you can get __up to $21,000 value of Mergify services, free of charge__.

![Mergify Startup Program](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w2977lw6w0vmkt7e7osd.png)

The company has in fact launched their startup program, a 12-month partnership between new ventures and Mergify which gives access to __all Mergify features for free__.

If you want to apply to it, you can do it from their [Startup Program page](https://mergify.io/startup?utm_source=sponsor&utm_medium=social&utm_campaign=CoderDave) (link in the description below) or email them at [startup@mergify.io](mailto:startup@mergify.io).

### Conclusions

Let me know in the comments below what you think about Mergify and if you’ve had a chance to use it already.

Also, check out [this video](https://youtu.be/lSnbOtw4izI), in which I explain how to properly manage Pull Requests in GitHub.

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

{% youtube jb9wnpqNzEo %}