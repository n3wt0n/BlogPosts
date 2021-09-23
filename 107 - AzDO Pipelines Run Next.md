Have you ever had a bugfix which you needed to deploy right this minute but had to wait behind other CI and PR jobs? 

Today I'm going to show you how to bump the priority of a queued job so it could be executed as soon as possible.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube hJsMq35KAMk %}

[Link to the video: https://youtu.be/hJsMq35KAMk](https://youtu.be/hJsMq35KAMk)

If you rather prefer reading, well... let's just continue :)

### Let's Do It

So, how can we decide what job will run next in our Azure Pipelines?

Let's say you have a bunch of jobs and Pipelines run in the queue

![Queued Runs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ltdz6vma911ssezu9a6i.png)

They will each have their own spot in the queue, depending on how many agents you have, the degree of parallelism, etc.

To __run a job next___, aka make it jump the queue, just click on one of the queued items, then on the __Job__ you want to run.

![Job Details](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/klegjymaaqnjbmzhwg62.png)

In the Job Detail Page you'll see its status in the queue (8th, in the image above) and you'll have a __Run Next__ button.

Click on it, and _magically_:

![Job Bumped](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/dmo0xnexzf89gzlg2ytc.png)

That job has been bumped 1st in the queue (and the Run Next button has disappeared).

> You need to have the "Manage" permission on the pool, and this typically means pool administrators, to be able to see the new "Run next" button on the job details page.

### Conclusions

Easy right? And __super effective__ too.

This works with both the YAML Pipelines and the Classic Pipelines. Of course you'll still need available parallelism and a suitable agent to be able to run ___that job___ next.

What do you think of this feature? As I've mentioned before I think it is __pretty useful__ if you need to have something "jumping the queue". Let me know in the comment section below what your thoughts are.

Also, checkout [this video](https://youtu.be/VaEFosTY7FU) where I talk about how to avoid the most common __DevOps mistakes__.

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

{% youtube hJsMq35KAMk %}