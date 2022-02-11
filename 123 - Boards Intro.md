With Azure Boards you can plan, track, and discuss work across your teams, connecting everything from idea to release.

Let’s see how we can get started with it.

> ATTENTION: I'm running a __giveaway__ until Tuesday, February 15th 2022. Keep reading to know ___HOW TO WIN___

### Intro

In this article I will cover some general topics around it, but let me know in the comments section below if you want me to go deeper into any of the different areas of Azure Boards because I’m thinking of dedicating a series to this awesome service.

I also want to mention that __Azure Boards is part of Azure DevOps__, therefore it of course works in combination with all the other services in Azure DevOps, but __it can work just as well with other systems__ like for example GitHub, and also in a standalone way.

If you want to see how to __integrate Azure Boards with GitHub__, check out [the video I made about this](https://www.youtube.com/watch?v=8cPP52fRo_s) when you are done with this article.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube Ft1JESBVFX8 %}

[Link to the video: https://youtu.be/Ft1JESBVFX8](https://youtu.be/Ft1JESBVFX8)

If you rather prefer reading, well... let's just continue :)

### What is Azure Boards

So, what is Azure Boards? In simple words, Azure Boards is a tool that allows you to __plan, organize, and track the work__ of your team and your organization in a simple, easy way.

![Boards](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/rnq0f8xfleidkdt8kgl5.jpg)

Azure Boards is interactive and customizable, and provides a rich set of capabilities including native support for Agile, Scrum, and Kanban processes, calendar views, configurable dashboards, and integrated reporting.

![Dashboards](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vv97sckqrmjsscyaim3z.jpg)

And all of this using a simple drag-and-drop interface, directly in the browser.

And on top of that, Azure Boards allows you to filter individual users, export data into calendars, plan sprints and even will let you query for your work items.

### Create a new Project

Alright, let’s see how we can get started and create a new project.

Once you login into Azure DevOps, if you don’t have any other project, you’ll have a prompt that says "_Create a project to get started_". 

![First Project](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9dh7njpr7iu8edxoppjl.png)

If instead other projects are present, you can click on the "_New Project_" button in the top right and the _Create New Project_ dialog will open.

![New Project Popup](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ga0eyazv7g3gzhlt7s39.png)

In either case, here you can specify a name for your project and provide a brief description for it.

You’ll then be given two options on the type of project you can create.

- __Public__ visibility permits users anywhere on the internet to see your board. That word public means exactly that! This is ideal for open-source projects that may need collaborators that are not part of a unified group that requires authentication.
- __Private__ visibility is just that, it allows you to lock your Azure DevOps and only permit those you choose to have access. This is great for your personal projects or smaller projects that do not have a large team within your team.

> Please note that Public projects are disabled by default for security reasons, and can be enabled in the organization's settings.

Clicking on _Advanced_, you can select the type of Source Control you want your project to use, but I will leave this for another time since it is not relevant to Azure Boards.

![Advanced Settings](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bdqakfutlsl6emneewoy.png)

What is very relevant tho is the selection of the process type. As mentioned before, Azure Boards supports a __variety of processes out of the box__: Agile, Basic, CMMI, and Scrum.

In this example you can also see another process, called Custom Scrum. As the name says, this is a custom process type. Azure Boards in fact allows you to __fully customize your processes__ based on your needs.

Once you have picked the process type that is right for you and your team, click on Create and in a few seconds the project will be ready.

> If you want to discover more about the different process templates and how to pick the right one for you, I’d recommend you to check out [this video where I explain exactly that](https://www.youtube.com/watch?v=sEO3eOstiKo).

### Sections

> Check out [this section of the video](https://youtu.be/Ft1JESBVFX8?t=324) for the full demo

Regardless of the process template you’ve selected, __the main sections are the same__: Work items, Boards, Backlogs, Sprints, and Queries.

And everything we will see is __configurable and customizable__!

#### Work Items

__Work Items__ is just a flat list of all the work items you have created, regardless of the type, status, area, etc.  In fact, you can see I have ___Tasks___, ___Product Backlog Items___, ___Features___ and even ___Bugs___ in here. 

![Work Items section](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/1xhsh7i18gzpluyw85em.png)

You can of course filter the list by keywords or by the different fields.

#### Backlogs and Boards

Backlogs and Boards are strictly correlated, in the sense that they show the same work items but in a different representation.

![Boards section](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uosgdjp1r471kf1w9jtb.png)

__Boards__ show Epics, Features, and Backlog Items (in Scrum, or Users Stories if you are using the Agile template) in a Kanban-stye view.

![Backlogs section](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vp2weyqe2jolke2lau8b.png)

While __Backlogs__ show the same but in a hierarchical list view that allows you to navigate the dependencies between the work items, even down to tasks and bugs.

#### Sprints

__Sprints__, on the other side, let you visualize and plan your iterations in a Kanban-like view, for tasks and bugs, still keeping the relationship with their parent backlog items visible (as you can see on the left). 

![Sprints section](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/83db2rkb48j2e2kdjvnt.png)

Here you can move the items via drag-and-drop to track the work done by your team.

#### Queries

Finally, the __Queries__ tab allows you to navigate the data about the work items using either predefined queries or custom ones. You can specify conditions and clauses, and manipulate the data for your own use.

![Queries section](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3qbx041vymrxqv2hp0f0.png)

> Check out [this section of the video](https://youtu.be/Ft1JESBVFX8?t=324) for the full demo

### Create a Work Item

The quick way to create any work item is to go to the _Work Items_ list, click on "_New Work Item_", and select the type of the Work Item we want to create. 

![New Work Item](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w0k09mmql7kkdatdvkfm.png)

This is the easiest, but it is __not the most efficient__. You want in fact to create __hierarchy__ between work items so to track the work properly.

Let’s say for example you want to assign a new task to a developer. That task for sure will be related to a backlog item, which in turn relates to a Feature.

In a scenario like this, what you probably want to do is going to the __Backlogs__ tab, locate and expand the Feature and the Backlog Item your new task will be part of, and here click on the create work item button, the one with the Plus at the left of the list. This will give you the selection of only the work item types you can create at that level.

![New from Backlog](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kxcp0udq8f052eaqa3ro.png)

If I were to click on the plus button near a feature, you would see that it would create a Backlog Item because it is the only work item type that is allowed in a feature.

![New Task](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ndhggxdqovqwq6xql70q.png)

When creating our task, we will need to insert all the information the person will need to execute it, and then we can assign the task to a specific person or leave the team free to pick it up. Finally, we should assign that work item to an iteration, so the team knows when to execute it.

Since I’ve assigned it to the current sprint, I can go to the sprints tab and under my Backlog Item I will now see the new task.

![New Task in Sprint](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5ipx1yjjfzpy3v2hl3x4.png)

And as for the lists and Kanban boards, Teams can __customize these fields__ to ensure specific data is captured. 

### How to Win the Giveaway Prize

All you have to do to participate in the Giveaway is subscribe to [my YouTube channel CoderDave](https://www.youtube.com/CoderDave?sub_confirmation=1), leave a like to the [video related to this article](https://youtu.be/Ft1JESBVFX8), and head over to [coderdave.io/newsletter](https://coderdave.io/newsletter) and join the newsletter for free.

![Giveaway Instructions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fyx4eplitv02o503e05p.png)

The giveaway runs until __Tuesday, February 15th 2022__. After that date, I will randomly select a person from the list of people that have joined the newsletter. The winner will be notified via email and in one of the next videos as well.

And do you want to know what the prize is? A __$50 worth of swag__ from the DEV Shop! I will provide you with a coupon code that you can use on that platform, and please note that shipping is not covered by the coupon.

### Conclusions

Let me know in the comments below if you have any questions about what we have covered in this video, and if you want me to go deeper into any of the sections of Azure Boards. And remember to go to [coderdave.io/newsletter](https://coderdave.io/newsletter) and join so you can participate in the giveaway.

Also, check out [this video](https://www.youtube.com/watch?v=8cPP52fRo_s) in which I explain how to integrate Azure Boards and GitHub to track the work.

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

{% youtube Ft1JESBVFX8 %}