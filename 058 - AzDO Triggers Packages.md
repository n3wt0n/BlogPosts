Ever wanted to have an Azure Pipelines run starting when a new version of a GitHub Package gets released?

This is exactly what we are going to do today!

### Intro

Today I have for you another post in the Azure Pipelines Triggers series, this is the 3rd one and it is about triggering an Azure Pipelines execution when a new GitHub Package version gets released.

For this we will use the ___Packages___ type of resource available in the __YAML Pipelines__.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube 99g1QA_74Z0 %}

([Link to the video: https://youtu.be/99g1QA_74Z0](https://youtu.be/99g1QA_74Z0))

If you rather prefer reading, well... let's just continue :)

### Why Packages Triggers?

So, why would you want to do this? _I'm glad you've asked_.

For example, this can be very useful when __your application depends on a package__ and you want to make sure it still works with the new version of the package. So you start some CI and test work.

In general, there are many scenarios that you can think of where it makes sense __triggering a CI or even a CD pipeline__ when a new version of a package is created.

### Enable the Trigger

As I've mention before, to achieve this we can use the YAML Resources. You can in fact __consume NuGet and npm GitHub packages__ as a resource in YAML Pipelines, and enable __automated pipeline triggers__ when a new package version gets released.

This is the YAML snippet we need in our Pipeline:

```yaml
resources:
  packages:
    - package: myPackageName
      type: NPM
      connection: n3wt0nPAT
      name: HelloNode/hellonodepkg
      trigger: true
```

> Watch the [video here](https://youtu.be/99g1QA_74Z0) for the full explanation of this snippet

This will give our pipelines access to the "_hellonodepkg_" package of the "_HelloNode_" repository in GitHub, and call it "_myPackageName_".

You can specify the type (currently only _npm_ or _NuGet_), and you can also target a specific version with:

```yaml
version: 1.2.3
```

If you don't specify the version, and in the snippet above, then it defaults to `latest`

Note that the `connection` must use a __Personal Access Token__ (PAT) for it to work.

And that's basically all you need.

### Download the package

Remember that by default __packages will not be automatically downloaded__ into your jobs.  To download a package, you have to use the `getPackage` task:

```yaml
- getPackage: myPackageName
```

As you can see, you use the same name you assigned to the package in the resources section.

> Watch the [video here](https://youtu.be/99g1QA_74Z0) for the full demo of this in action

### Announcement

Before closing, I have an __announcement__ to make, which I'm very excited about. I've finally launched my [__Patreon page__](https://patreon.com/CoderDave). You can get __exclusive content__, both posts and videos that are not posted anywhere else. You can influence the content of this blog and my YouTube channel, you can have live chats and Q&A with me. But the coolest part is that __you can have a 1:1 consultation with me__ to talk about anything DevOps, GitHub or Azure DevOps.

Visit my Patreon page to see the options available, just go to [patreon.com/CoderDave](https://patreon.com/CoderDave).

### Conclusions

Alright, that's it for today.

Let me know in the comment section below if you think this is useful. And don't forget to check the other posts and videos in the Azure Pipelines Triggers series!
