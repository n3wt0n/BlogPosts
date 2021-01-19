Azure Pipelines has a very useful feature that allows you to __create templates with task you want to share and use them across multiple pipelines__.

In today's post we are going to see ___what___ Templates are, ___why___ they are important and ___how___ we can create and use them.

Let's get into it.

### What?

Templates allow us to __define reusable content__, logic, and parameters, keeping our main pipeline definitions focused on the application. They are also a great way of __sharing common logic in a centralized way__, without duplicating it in many pipelines.

![Sample Template](https://dev-to-uploads.s3.amazonaws.com/i/ufdu7w7o968at343gzsq.png)

Essentially, we can define reusable code in separate templates. 

If you have worked in the past with Task Groups in the Classic Pipelines, YAML Templates are somehow similar but quite more powerful.

We can __include templates within templates__ and define four types of templates: 

![Template Types](https://dev-to-uploads.s3.amazonaws.com/i/c25zte4en19x4xvnmvle.png)

- __Stage template__, to define a set of stages of related jobs
- __Job template__, to define a collection of steps run by an agent
- __Step template__, to define a linear sequence of operations for a job
- __Variable template__, as an alternative to hard coded values or variable groups

Just as a side note, Azure Pipelines currently support a __maximum of 100 separate template files__ in a pipeline, and no more than __20 level of template nesting__. Which I think it is more than enough for a normal use. If you need more than that in a pipeline, it's probably better if you re-architect it.

### Why?

Anyway, why are YAML Templates so important? Well, there are a number of Reasons.

#### Guardrails

First, as guardrails provide boundaries on the roads, templates can be used for the same purpose on a pipeline. In fact we can __use templates to provide alignment__ to architecture, security and development. 

![Required Template](https://dev-to-uploads.s3.amazonaws.com/i/dk2ay6fe9lh8gq7m9utc.png)

Do you have some task or operation you want every pipeline in the project to do? 
Make it part of a template, and enforce a policy to make sure __all the pipelines use that template__. If you wanna know how to enforce that policy, check the [video about the Environment Gates and Checks](https://youtu.be/FbXKpo6oEyg).

#### Consistency and Speed

Other reasons are consistency and speed. Organizing the most common operations in templates, the development of a pipeline will take much less time. 

![Docker params](https://dev-to-uploads.s3.amazonaws.com/i/4zgvkhc3pdehpv7txylt.png)

Let's say that you often build container images for your software, and to do so you have to add many steps to build the image, tag it properly, test it for vulnerabilities and finally push it to a container registry. _That is easily a 4 or 5 steps process that you need to configure every time_.

If instead you save that into a template, you will have to use a __single step in your pipeline__, which is the template, passing it only the parameters that change, like the image name, repo name, etc, making it much faster to write.

Also, by doing so you ensure that all the pipelines which build a container image will be __consistent one another__ because they all use the same template.

And of course this applies to each and every operation you can think of.

#### Centralize editing

Moreover, if you have many pipelines using the same template __changes became very easy to make__.

![Edit](https://dev-to-uploads.s3.amazonaws.com/i/zdxfp67ujpk27wc0xz42.jpeg)

What if you perform some operation in many pipelines and you realize that __you need to change__ a parameter, or maybe the command changed in a new version of a tool? If you are not using templates, you would need to go into each and every pipeline definition and make that change. If instead you are using a template for that operation, you just have to __change that template and all the next pipeline runs will use the modified version__.

#### Simplicity

Finally, using templates allows you to __keep your pipeline definitions simpler__, focusing only on the application-specific tasks and operations.

### How?

Alright, enough talking. Let's actually see how to build a template, and how to use it.

For this, I have created this video that shows step by step how to do that:

> You might want to skip to the demo at around minute [4:00](https://www.youtube.com/watch?v=UQlRITs7veM&t=240s)

{% youtube UQlRITs7veM %}

([Link to the video: https://youtu.be/UQlRITs7veM](https://youtu.be/UQlRITs7veM))

### Conclusions

Alright, I think that's enough for today. This was an _introduction to Azure Pipelines Templates_. In the next posts and videos about this topic we will go more in depth into it, looking at more __complex examples and scenarios__. If you are interested, consider __following me here__ and [subscribing to my channel](https://www.youtube.com/CoderDave?sub_confirmation=1) so you won't miss it.

Let me know in the comment section below what you think about the Azure Pipelines Templates and if you use them already.