There are many DevOps myths circulating in the developer community. This is no surprise, given the popularity of the DevOps concept in recent years.

Today I'm gonna debunk those myths once and for all so you can really understand what DevOps is about and how to do it correctly.

### Intro

As you probably know, the DevOps methodology can have __significant positive effects__ for organizations when properly implemented, as I've discussed in [this video over here](https://youtu.be/OxDtADXeyv8).

But to do it properly, it is necessary to recognize what DevOps really represents. And that’s why I wanted to make this article/video.

Let's jump right into the first myth.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation__, which is  ___more complete___ than this post.

{% youtube XXX %}

[Link to the video: XXX](XXX)

If you rather prefer reading, well... let's just continue :)

### Myth 1: DevOps is the same as CI/CD

Or to say it differently, "If I do CI/CD I do DevOps".

This is one of the __biggest misconceptions__ about DevOps, and unfortunately there are a lot of people thinking that DevOps is the same thing as CI/CD. 

The truth is that while continuous integration and delivery are some key components, DevOps adoption focuses also on the __culture__ and responsibility in a __team__. It emphasizes the need for everyone on the team to take part in each other’s tasks. This improves __collaboration and communication__ in the team.

On the other hand, CI/CD enables this culture with software and tools that emphasize automation. You can see them as __a mean to an end__.

### Myth 2: DevOps is all about tools

Conversations about DevOps are often very focused around which tools a company is using. They then turn into philosophical battles about what are the best tools. Instead, we should be communicating about the bigger picture, the __business value DevOps brings__ to your company.

DevOps means __focusing on culture, mindset__, and how individuals work together. Tools are important, but only after addressing people and processes. In fact, you should be choosing __the right tools for your processes__, and not changing your processes to adapt them to the tools.

In general, many studies have in fact shown that the main factors in successfully implementing DevOps are the right culture, the right processes, AND the right tools. Tools should always come last.

### Myth 3: I can use the same processes for all my projects

While this might be true in some contexts, it is usually not...

You can and __should reuse some processes__, especially around people interactions and collaboration, but the more __"technical processes" may change__ between different projects or even may need to be different.

For example, let's talk about environment promotion. You may have projects that only need two to three environments. For example, development, test, and production environments with frequent deployments. Another project may require more environments because it has multiple stages in the software delivery cycle. Or have more or less frequent deployments.

Another example could be around approvals. Maybe a project needs to go through different approval at various stages, so your processes should account for that. But it is also possible that another project in your organization doesn't require the same approvals, or perhaps needs no approval at all.

Different projects, different requirements and needs, different processes.

### Myth 4: I can do in my organization what Microsoft/Amazon/Google/Netflix do

Many world-famous companies have adopted DevOps for its benefits and its flexibility. Looking at the successes of these companies, we of course appreciate their achievements. We do this without realizing their context and the steps they have taken to be successful.

One thing is for sure: these organizations chose and built the tools and processes that worked best for them at the time. This does not necessarily mean that we have to follow these organizations. Plus, __what they've done won't magically work for our business either__.

We need to learn from them and find new ways to innovate and grow. Explore and find the right processes and tools that define our problem space. What will __bring success to our business__ in particular? This is what DevOps is.

As I've mentioned in the previous myth, different projects may require different processes and tools. And it is of course even more evident between different companies or organizations.

### Myth 5:  I can create a DevOps team and I'm done implementing DevOps

This is something I see happening many times and given the amount of replies I had when I posted this on Twitter means that I'm not the only one. (Btw [follow me on Twitter](https://twitter.com/davidebenvegnu) if you aren't yet).

Back to the myth, what I see happening all the time, especially in big organization, is that they create a new team, they hire a bunch of DevOps engineers, __they call it "DevOps team" and they think their done__.

The problem there is that if you're not willing to change your processes and your culture, creating a DevOps team won't help at all. DevOps is about collaboration, every person and team in the organization should "do DevOps". __Barriers and silos need to be removed__ for this to work. Otherwise, you are just creating more silos...

There is an exception to this, and it is when the newly created DevOps team is in fact in charge to spread the DevOps principles throughout the organization. Basically, a DevOps Center of Excellence. But this anyway is not the end, __it is just the starting point__.

### Myth 6: If I do DevOps, I don't need IT Operations anymore

If you think about it, you already know the answer. Of course __you still need to perform tasks usually associated to IT Operations__! And the Operations team still has its own place.

But __with DevOps the responsibilities shift__. In a "_properly adopted_" DevOps model, Software Engineers should also take care of the deployment. Maybe they are not the ones "pressing the deploy button", but they are the ones who should __understand__ how the application is __operated in production__, and the ones who have to create __deployment procedures and scripts__. Who better than them would know how to do it?

Also, in many DevOps-mature organizations, Developers and Software engineers share the on-call duties with Operations for solving live site incidents.

In this scenario, __IT Operations duties shift__ more towards the care and maintenance of the __live site__: things like scaling, optimizations, etc.

### Myth 7: Automation removes all bottlenecks

Automation is one of the biggest advantages of DevOps. But __this is not a quick fix__ that will solve all of your problems.

A continuous delivery process allows teams to quickly deploy new features, and also quickly get the feedback they need. This of course means that you have to guarantee the quality of the product. In addition, you should take care of its proper operation and performance when scaling, for example. You also need to ensure smooth production deployments.

Automating your CI / CD pipelines helps eliminate bottlenecks between code validation and deployment. But this is only one step in the software delivery process. Unless the __developers and testers work together as a single team__, you won't be able to solve all of your issues. It is likely that you will only move the bottlenecks somewhere else.

### Myth 8: DevOps requires Agile

The truth is that DevOps and Agile can be either complementary or competitive, or even not related at all.

The notions of working with small, incremental changes is common to both Agile and DevOps. However, organizations that embrace Agile are focused on __optimization of the development end of the pipeline__, and may struggle with DevOps, which emphasizes engineering of end-to-end process optimizations.

I've also seen organization being fairly __successful at DevOps while not doing Agile__ at all, working with Waterfall methodologies. It is quite rare, but not impossible.

### Myth 9: DevOps applies only to web applications

This is simply not true. __DevOps can be applied to any kind of software development__: Databases, Backends, Desktop software, Embedded software, IoT, and much more.

In fact, the same principles can be applied and are applied also outside of the software world, like for example __hardware development__. Remember that the legacy of DevOps for how we know it today comes from factory floors optimization.

The examples of DevOps you can find around are mostly based on Web Applications or platforms because Web Development is one of the __most common__ types of software development, and also because it is where you can see the effects of DevOps more quickly. But that doesn't mean that DevOps and its principles cannot be used in other kind of projects.

### Myth 10: I have to apply DevOps to any software product, service or application

The fact that you can do DevOps basically everywhere, doesn't actually mean that you have to.

DevOps brings benefits in many circumstances, but __in some cases you may not want to or be able to afford the changes__ in the people, process, and technology needed for DevOps.

For example, applications that rarely change may not justify the cost of DevOps changes.

In general, the guideline here is: __assess your processes__ and culture and see if it makes sense to change. Usually the answer is yes, but there may be instances in which the cost or the effort outweigh the benefits. If you have __ROI__ from adopting DevOps (and that usually comes in the form of higher velocity, higher quality, and reduced time-to-market) then go for it.

### Conclusions

Alright, ___10 myths busted___. I think it is enough for today.

Let me know in the comment section below what you think about what I've covered in this video and about my "answers" to those myths. Let me also know if you have any questions around this topic and DevOps in general.

You may also want to [watch this video](https://youtu.be/OxDtADXeyv8), where I talk about the Benefits of adopting DevOps.

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

{% youtube XXX %}