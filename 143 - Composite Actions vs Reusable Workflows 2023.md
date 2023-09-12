Understanding the differences between Composite Actions and Reusable Workflows in GitHub Actions can be more complex than you think… especially after the latest changes GitHub made.

But hey, I’m here for you. Let’s find out together what those 2 features have in common, what the differences are, and when you should use one instead of the other.

### Into

I’ve already written an [article](https://dev.to/n3wt0n/composite-actions-vs-reusable-workflows-what-is-the-difference-github-actions-11kd) and made a [video](https://youtu.be/4lH_7b5lmjo) on this subject before, however that was almost 1 and a half years ago and, as many pointed out in the comments , GitHub has substantially changed the featureset since… so it’s time for an updated comparison.

Btw if you want to have a deep dive into either Composite Actions or Reusable Workflows, be sure to check the in-depth videos I made about them ([here](https://youtu.be/4lH_7b5lmjo) and [here](https://youtu.be/lRypYtmbKMs)).

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation__.

{% youtube zc19mR3O4a4 %}

[Link to the video: https://youtu.be/zc19mR3O4a4](https://youtu.be/zc19mR3O4a4)

If you rather prefer reading, well... let's just continue :)

### About Composite Actins and Reusable Workflows

In general, __Reusable Workflows__ are a way to avoid duplication as you can reuse the same workflow in multiple other workflows, and perhaps create a library of proven and effective workflows that can be centrally maintained.

__Composite Actions__, instead, allows you to combine multiple steps within one action. For example, you can use this feature to bundle together multiple run commands into an action, and then have a workflow that executes the bundled commands as a single step using that action.

And this brings me to the first difference between the 2: Visibility and Logging.

### 1. Visibility and Logging

I think this point is __pretty important__ but often overlooked. 

With Reusable Workflows you have a __very rich log__ of what is happening, and every single job and step is logged independently in real time as you can see below:

![Reusable Workflows Logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zxl2e30bs806z7myo098.png)

This specific workflow has 2 jobs in it, and each job is logged together with its steps. All clear and organized.

![Composite Actions Logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kgtnwp0ligtx0auwj1qo.png)

This is not the case, however, with Composite Actions. As we have just seen, Composite Actions are a way to _group_ multiple steps in one… this also means that when executing that step you don’t have visibility on all of the parts.

![Multiple Jobs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kl7hrc3amerl4orjrd5x.png)

All you have is a __single log__ of a single step... even if it contains multiple steps.

### 2. Jobs

Another difference, which is the __biggest difference__ in my opinion, is about Jobs.

As we have said before, Composite Actions allow you to only have a flat list of steps. Therefore, you __cannot have multiple jobs__ in a single Composite Action. 

In fact, a Composite Action doesn’t even specify a `job` keyword, but uses `runs` instead, and can only be consumed from within a job in the caller repository.

![No Jobs in Composite Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jslsko9fkfy33way3daw.png)

Because of this, you can see a Composite Action basically like any other action you have on the marketplace.

The story is different, however, for Reusable Workflows.

They do __define jobs__ inside them, and because of that you can have as many jobs as you want in a single Reusable Workflow.

![Jobs in Reusable Workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/r8jrmt9jj5dxbkltayt8.png)

And since they do use jobs, and you have to specify where the job will run, we can take this a little further: if your job needs to run on a specific runner or machine, you need to use Reusable Workflows.

### 3. Calling them

Next, and actually last, difference between Composite Actions and Reusable Workflows is __how you call them__, and this tightly relates to what we have seen previously.

Reusable workflows are called __directly within a job definition__, and not from within a job step. 

![Calling a Reusable Workflow](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/05civa9bq8gjxxrkvnev.png)

You cannot, therefore, use `GITHUB_ENV` to pass values to job steps in the caller workflow. And, more importantly, you cannot add additional steps to the job which calls the reusable workflow.

Composite Actions, instead, can exclusively be called and used as a step in a job, which also means there could be (and that is usually the case) other steps in the job before and or after the Composite Action.

![Calling a Composite Action](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8fvmk8ct8ow9b7vrbybh.png)

Make sure to keep this difference in mind when designing your Actions Workflows.

### Conclusions

There used to be many more differences between Composite Actions and Reusable Workflow, but as of recording this video, the only ones still standing are the 3 differences we have just seen.

So, to recap, Reusable Workflows make it simpler to spin up new repositories and projects and immediately start using automation and CI/CD workflows with GitHub Actions that you know will work, and to reduce code duplication. 

Composite Actions, on the other hand, allow you to pack multiple tasks and operations in a single step, to be reused inside a job.

Let me know in the comments below if you noticed any other point in which those 2 features differ, and if you prefer using Composite Actions, or Reusable Workflows… or both 😉

Also, check out [this video](https://youtu.be/lTAkB7P1qV0), in which I talk about the new GitHub Actions Larger Runners and how to use them.

__Like, share and follow me__ 🚀 for more content:

🆘 [Get Help With DevOps](https://geni.us/cdconsult)
📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
📧 [Newsletter](https://coderdave.io/newsletter)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)
💖 [Patreon](https://patreon.com/CoderDave)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube zc19mR3O4a4 %}