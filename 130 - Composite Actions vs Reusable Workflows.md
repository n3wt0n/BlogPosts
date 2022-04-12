With GitHub offering both ___Composite Actions___ and __Reusable Workflows__, I’ve seen a lot of people having doubts about what they should use, and in fact I often have someone asking me: _what is the difference between Reusable Workflows and Composite Actions_?

In the past __the difference was very clear__, because Composite Actions allowed to only use bash scripts in them. But now that we have the possibility to __use other actions__ as steps in the Composite Actions, as I explain in [this video](https://youtu.be/4lH_7b5lmjo), the difference is more subtle.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube xa9gYSCf8q0 %}

[Link to the video: https://youtu.be/xa9gYSCf8q0](https://youtu.be/xa9gYSCf8q0)

If you rather prefer reading, well... let's just continue :)

### General

First of all, let me say that if you want to have a deep dive in either one of these features I’d highly recommend to check the specific videos I made about them, you can find them [here (Composite Actions)](https://youtu.be/4lH_7b5lmjo) and [here (Reusable Workflows)](https://youtu.be/lRypYtmbKMs). To summarize, I would say that Composite Actions are intended to be more isolated and generic, while Reusable Workflows are more feature rich and appeal to slightly more specific scenarios.

In general, I would say __80% of the time you can probably use either one__. But 20% of the time, you’ll need to use one or the other.

I’ve identified __6 main differences__ between those 2 flavors of GitHub Actions, and we will go through each one of those right now.

### Difference 1: Nesting

The first one is about nesting. Composite Actions can be nested __up to 10 layers__. This means you can create a Composite Action that has another Composite Action as one of its steps, and so on so forth until the 10th level.

Reusable Workflows, on the other hand, __cannot call another reusable workflow__, you can’t chain them. Using another terminology which may be more familiar to users of other CI systems, you cannot have a template which refers to another template.

### Difference 2: Secrets

The second big difference is about Secrets. Composite Actions __cannot use secrets__, not from the workflow nor as parameter. And this, as you can imagine, could be a fairly big limit.

![Secrets in Reusable Workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g79raymqlpi73zzpsfcw.png)

Reusable Workflows instead __can consume secrets__, although you have to pass them to the workflow via parameter, as you can see in the image above.

This, together with the next difference, makes the Reusable Workflows way more flexible.

### Difference 3: Conditionals

Third difference is that Reusable Workflows can use the __if conditionals__.

![Conditionals](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/gy27xbwg9ic6jj8l814q.png)

This means that the execution of parts of the template can be controlled by some conditions, like you would do in a normal workflow.

This behavior unfortunately is not present in the Composite Actions, where you can __only have a flat list of steps__ and no control over their execution.

### Difference 4: Storage

The fourth main difference I’ve identified is about storing them.

![Reusable Workflows Storage](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sd2e84p9rju060w9mu0r.png)

Reusable Workflows can be stored in your repo as __normal YAML__ actions files, in the `.github/workflows` folder. Or you can create a __centralized repository__ to store multiple Reusable Workflows.

![Composite Actions Storage](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4m6culjlyg89njm2t9i1.png)

Each Composite Actions definition, on the other hand, requires its own repository, which must be public, and a metadata file. And if you want to execute script from a file, then you’ll also need the script file in the same repo.

### Difference 5: Jobs

The fifth difference is about multiple jobs. As we have said before, Composite Actions allow you to only have a flat list of steps. Therefore, you __cannot have multiple jobs__ in a single Composite Action

![No Job on Composite Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kzwfpxtjtmzwbkvq0w9i.png)

In fact, a Composite Action doesn’t specify a `job` keyword, but uses `runs` instead, and can only be consumed from within a job in the caller repository.

Because of this, you can see a Composite Action basically like any other action you have on the marketplace. 

The story is different, however, for Reusable Workflows.

![Job on Reusable Workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/2x4cgmbbogykcor2y4eq.png)

They do __define jobs__ inside them, and because of that you can have as many jobs as you want in a single Reusable Workflow.

![Multiple Jobs on Reusable Workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6gel01gutqr6k74z4tcj.png)

And since they do use jobs, and you have to specify where the job will run, we can take this a little further: ___if your job needs to run on a specific runner or machine, you need to use Reusable Workflows___.

### Difference 6: Logging

The sixth and last difference between Reusable Workflows and Composite Actions is something I think is __pretty important__ but often overlooked. I’m talking about logging.

![Rich Logs on Reusable Workflows](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0uhefkcht5a3bf6xdsne.png)

With Reusable workflows you have a __very rich log__ of what is happening, and every single job and step is logged independently in real time.

![Sipmle Log on Composite Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0y4c2rpyyftd0scnilty.png)

Using Composite Actions, instead, all you have is a __single log__ of a single step... even if it contains multiple steps.

### Conclusions

Because of all we have seen, Reusable Workflows make it simpler to spin up new repositories and projects and immediately start using automation and CI/CD workflows with GitHub Actions that you know will work. Composite Actions, on the other hand, allow you to pack multiple tasks and operations in a single step, to be reused inside a job.

Hope this clarifies once and for all the differences between those 2 powerful features of GitHub Actions. But let me know in the comments below if you have other questions about them that this article/video wasn’t able to answer.

Also, check out [this video](https://youtu.be/lRypYtmbKMs), in which I show how to build and use Reusable Workflows.

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

{% youtube xa9gYSCf8q0 %}