With the newly released Manual Validation task you can pause a YAML pipeline mid-stage. This allows you to perform manual or offline activities and then resume (or reject) the run. 

### Intro

As I've mentioned, you can use this new task in a YAML pipeline to pause a run within a stage, typically to perform some manual actions or validations, and then resume/reject the run.

This is especially useful in scenarios where you want to pause a pipeline and validate configuration settings, build package, etc. before moving on to a long-running, compute-intensive job.

When the Manual validation task is activated during a pipeline, it displays a message bar containing a link that opens the Manual validation dialog containing the instructions. After carrying out the manual steps, the administrator or user can choose to resume the run or reject it.

### Demo

Let's see this in action. We will cover how to configure Azure Pipelines to use it and how to use it.

Here you have __the video with the whole demo and explanation__.

{% youtube sfb3d100JPo %}

[Link to the video: https://youtu.be/sfb3d100JPo](https://youtu.be/sfb3d100JPo)

### Limitations

Remember that, as I've mentioned in the video, you can use this new approach only in an agentless job of a YAML pipeline. If like in my example you have other jobs already, you would need to add a job with pool: server to make this work.

### Conclusions

I wanna know what you think about this feature, so let me know in the comment section below.

Also, check [this video over here](https://youtu.be/3cGtA__dKUc), where I talk about the differences between Classic and YAML pipelines for both Build and Release.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube sfb3d100JPo %}