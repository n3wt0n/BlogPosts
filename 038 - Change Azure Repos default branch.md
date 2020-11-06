Azure Repos now offers a __customizable default branch name for Git__ which can be set per project or per organization.

Today we talk about the default branch name in Azure Repos and how to change it. Let's see how.

### Video

If you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube zoTnQRyt6pM %}

([Link to the video: https://youtu.be/zoTnQRyt6pM](https://youtu.be/zoTnQRyt6pM))

If you rather prefer reading, well... let's just continue :)

### Intro

To change the default branch name for new repositories you have 2 options: you can do it either at project-level or at organization-level.

#### Change at Project Level

To change it at project level, you need to go into `Project Settings > Repositories > Settings`

![Prj level settings](https://dev-to-uploads.s3.amazonaws.com/i/kgowngnncnrghru7tuzh.png)

Remember that this will set the new default branch name __only on newly created repos inside this project__.

If you want to __change the default branch for an existing repo__, just go to:

`Repos > Branches > Create o select a branch > ... > Set as default`

[Watch the video for the full example](https://www.youtube.com/watch?v=zoTnQRyt6pM&t=60s)

This is good, but if you have many projects in your Azure DevOps organization it will take you forever to change this. This is where the new org-level settings comes in help.

#### Change at Organization Level

To change the default branch name for new repositories at org level go into `Org Settings > Repositories > Settings`

![Org level settings](https://dev-to-uploads.s3.amazonaws.com/i/ildptlk95jsp4kubyn13.png)

Now __all your new repos__ will have the default branch name as you set here.

You can still change the name at project level if you want, and that will override the setting at organization-level.

[Watch the video for the full example](https://www.youtube.com/watch?v=zoTnQRyt6pM&t=120s)

### Conclusion

Let me know in the comment section below what is your default branch name of choice.