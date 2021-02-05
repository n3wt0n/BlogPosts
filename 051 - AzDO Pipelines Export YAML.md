Let's say you have been working on a Classic Pipeline in Azure DevOps, and now you would like to __convert it to YAML__. Or perhaps you just want to learn the YAML Pipelines syntax referencing an existing Classic one.

Today we are gonna do just that, using the new __Export to YAML feature__.

### Intro

Today we talk about the __new Export to YAML feature of Azure Pipelines__. This is the feature which helps you migrate designer pipelines to YAML.

You may want to read this post even if you have already used the "View YAML" feature that existed before, because __this new feature is much better__!

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube PD0JHHw0Or4 %}

([Link to the video: https://youtu.be/PD0JHHw0Or4](https://youtu.be/PD0JHHw0Or4))

If you rather prefer reading, well... let's just continue :)

### It is more complete!

The new version is more correct and __covers more Classic Build features__.

The previous version of this feature worked on __a job or step at a time__. This was not only very time consuming, you had to click on each step and get the YAML, but also __not very accurate__.

The differences were typically __subtle, small, and hard to spot__.

The new experience takes a different tactic. It’s implemented in the platform, reusing existing Classic and YAML pipeline infrastructure to make sure __the resulting YAML is correct__.

### How to use it

> You may want to [watch the video with the demo here](https://youtu.be/PD0JHHw0Or4)

To use the new Export to YAML, you don't need to go editing the pipeline but __just click on it__.

Then you can just select the "___Export to YAML___" item from the ellipses menu.

This will __download the whole pipeline converted in a YAML__ file that you can then edit and use to create a YAML Pipeline.

No more time consuming operations. Just one click and you have the full YAML. Isn't it cool?

### Supported Features

In addition to being more correct, __the new version covers more__ Classic pipeline features. 

The new system knows how to handle every feature listed here:

![Feature list](https://dev-to-uploads.s3.amazonaws.com/i/fussj48kc6vy8d9se7kj.png)

### Unsupported Features

There are only __2 features that are not supported__.

If you have __UI variables__ in your Classic pipeline, those won't be exported but they will be mentioned by name in the comments to remind you that you need to configure them in your new YAML pipeline definition.

The other unsupported one is the __cron timezone translation__.  Cron schedules in YAML are expressed in UTC, while Classic schedules are in the organization’s timezone.
Converting a cron expression to a different timezone is almost impossible. ___Believe me, I've tried___.

### Conclusion

I hope you enjoy the new, more correct and more complete “Export to YAML”. Let me know in the comment section below what your thoughts are, I think it is very useful.

Check the video below to see this in action:

{% youtube PD0JHHw0Or4 %}