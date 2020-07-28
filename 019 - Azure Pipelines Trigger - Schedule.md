We all know how to enable our Builds as CI Pipelines, and our Releases as CD Pipelines. No big deal there.

But sometimes it is necessary or just helpful to run some pipeline at defined intervals, or in a scheduled manner.

Let's see how, with the help of Azure Pipelines Schedule trigger.

### Intro

This is the second post in the series about Azure Pipelines Triggers.

In the previous post, we have seen how to kick off our release pipelines every time a new container image is pushed to a registry.

Today instead we are going in a quite different direction, we are going to talk about Scheduling the executions of our pipelines using the Schedule trigger.

Once again I'll focus first on the Classic Release Pipelines, using the UI, and then on the YAML Pipelines. Stay with me until the end because the behaviour of the two is quite different.
Finally I will also show you how to check when your scheduled pipelines will run next.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much ___more complete___ than this post.

{% youtube RlZ31mAS_DA %}

If you rather prefer reading, well... let's just continue :) 

### Classic Build Pipelines

Let's start with the Classic Build. Go to your Pipeline page, then _Edit_, _Triggers_, _Schedule_.

![Classic Builds](https://dev-to-uploads.s3.amazonaws.com/i/db24m4gmgzpvs8280pzt.png)

Here you can select the __days__ and __time__ when you want to run the build.

You can also make the scheduled pipeline run only if either the source code or the pipeline has changed between the previous execution and the scheduled one.

If your repository is Azure Repos Git, GitHub, or Other Git, then you can also specify branches to include in and exclude from the build.
And you can use __wildcards__, just type the branch specification (for example, features/modules/*) and then press Enter.

And this is basically it for the Classic build. Let's talk about the Classic Release pipelines now.

### Classic Release Pipelines

Let's go to _Releases_, _Edit_ and this time use the _Schedule_ button

![Classic Release](https://dev-to-uploads.s3.amazonaws.com/i/7kckzlty0owwk6qqpml2.png)

This will open a very __familiar__ panel where we can set all the settings we need for the schedule:

![Classic Releases](https://dev-to-uploads.s3.amazonaws.com/i/b0fss4rai3m68r9mzdp6.png)

And remember that the time is expressed in __24 hours__.

As you can see, scheduling Builds and Releases using the Classic editor is super easy and intuitive.

Alright, let's see now how to achieve the same with the Multistage YAML Pipelines.

### YAML Pipelines

There are 2 ways to schedule a YAML Pipeline: using the _settings UI_ and using the _YAML syntax_.

But we need to be careful, because ___scheduled triggers defined using the pipeline settings UI take precedence over YAML ones___.

If your YAML pipeline has both YAML scheduled triggers and UI-defined scheduled triggers, only the UI defined scheduled triggers are run. To run the YAML defined scheduled triggers in your YAML pipeline, you must remove the scheduled triggers defined in the pipeline setting UI. Once all UI scheduled triggers are removed, a push must be made in order for the YAML scheduled triggers to start running.

Let's take a look at the triggers from the __setting UI__ first.

Once again, just go to your Pipeline edit page, then click on the _ellipses_ and select _triggers_

![Settings UI](https://dev-to-uploads.s3.amazonaws.com/i/uteiin5jddroy77rkzoa.png)

Easy right? And the Ui is identical to the Classic Pipelines one... with of course the "_inconvenient_" of the override.

But let's talk about __YAML__.

First of all, if you want to run your pipeline by ONLY using scheduled triggers, you must disable PR and continuous integration triggers.

The easiest way to do so is using:

```yaml
trigger: none
```

Next we need to add the ___schedules___. For example:

```yaml
schedules:
- cron: "0 0 * * *"
  displayName: Daily midnight build
  branches:
    include:
    - master
    - releases/*
    exclude:
    - releases/old/*

- cron: "0 */6 * * *"
  displayName: Every 6 hours build
  branches:
    include:
    - releases/*
  always: true
```

In this case I have 2 schedules.

As you can see, the trigger uses the ___CRON___ syntax.

If you are not familiar with the CRON syntax, here you have something for your reference.

![CRON](https://dev-to-uploads.s3.amazonaws.com/i/g57nfp1o7999j8bp4972.png)

It's basically a numerical way to express time and dates for scheduling purposes.

It starts with minutes, then hours, days, months and days of weeks.

And for each field, apart from the values you can see here. you can also use wildcards like star to match every possible value or intervals.

Going back to the schedules, there are some things you __need to keep in mind__.

First, you __must__ use the "___include___" keyword. In the Classic Pipelines you can omit that, and the engine will take the whole content of the repo. With the YAML Pipelines, it won't work. The "exclude" part is instead optional.

Second, by default the Classic Pipelines will execute anyway, no matter what, unless you optionally enable the "Only schedule builds if the source or pipeline has changed" checkbox. With YAML, instead, you __need to manually tell Azure Pipelines that you want to always execute the Pipeline even tho something hasn't changed__, and you do so using the "_always: true_" statement. Basically Classic and YAML Pipelines behave the opposite one another.

Lastly, __the time in the YAML Pipelines is expressed in UTC time zone__ and it is not possible to change time zone.

This is super flexible, way more than the UI.

### Limitations

Keep in mind that there are certain limits on how often you can schedule a pipeline to run, put in place to prevent misuse of Azure Pipelines resources.  

At the time of writing this post, the limit is around 1000 runs per pipeline per week.

### Scheduled Runs

Before we close, I want to mention there is a way to check when your scheduled Pipelines will run next.

Just go to your Pipeline page, click on the Pipeline you want to check, click on the _ellipses_ and the select _Scheduled Runs_

![Scheduled Runs](https://dev-to-uploads.s3.amazonaws.com/i/2t0p7ktg3dxbhuuyph0u.png)

### Conclusion

Alright, that's it for today.

Let me know in the comment section below what you use or plan to use the scheduled pipelines for.

### References and Links

- [Video with full explanation and examples about the Schedule trigger](https://youtu.be/RlZ31mAS_DA)
- [All the other videos in the Azure Pipelines Triggers series](https://youtu.be/FHnPJ8FBjLM)