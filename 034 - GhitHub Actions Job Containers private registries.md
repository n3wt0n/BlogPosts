Today we are talking about a very __new feature__ for GitHub Actions: Job and service containers from __private registries__. 

What does that mean? Let's discover it together.

### Video

If you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube S5eZ0YOLJDc %}

([Link to the video: https://youtu.be/S5eZ0YOLJDc](https://youtu.be/S5eZ0YOLJDc))

If you rather prefer reading, well... let's just continue :) 

### What are Job Containers and Service Containers?

First off, what are job containers and service containers?

Job containers allow you to provide the __environment and tools__ that your workflow needs, they are a great way to ensure your dependencies are always exactly met and __under your control__. 

Similarly, service containers provide a way to stand up __additional networked services__ that your workflow may need to build or test against, like a database, an API, and so forth.

### The old way

Previously you may have had a workflow like this:

```yaml
name: JobContainers

on: [workflow_dispatch]

jobs:
  build:
    runs-on: ubuntu-latest
    services:
      redis: redis:latest
    container: alpine:3
    steps:
    - run: ./build.sh
```

In the workflow we have both the service container (a _redis_ image under _services_) and the job container (an _alpine_ image under _container_), and as you can see both images comes from a __public container registry__.

Unfortunately ___there has not been a way to consume these containers from private registries___, or more generally if pulling them required you be logged in. Until now!

### The new way!

With the new feature, in fact, you can just provide the username and password in a new __credentials__ property as you would if you were running docker login.

```yaml
name: JobContainers Private reg

on: [workflow_dispatch]

jobs:
  private:
    runs-on: ubuntu-latest
    services:
      redis: 
        image: ghcr.io/n3wt0n/modified-redis
        credentials:
          username: n3wt0n
          password: ${{ secrets.GHCR_TOKEN }}
    container:
      image: ghcr.io/n3wt0n/modified-alpine
      credentials:
        username: n3wt0n
        password: ${{ secrets.GHCR_TOKEN }}
    steps:
    - run: echo secret!
```

As you can see above, we now have this now `credentials` property that allows us to specify the credentials to authenticate to __any private registry__.

In that example I'm using the new GitHub Container Registry, but in fact that would work for any registry which requires authentication: Private Docker Hub, Azure Container Registry, etc... you name it...

Easy right?

### Conclusion

Let me know in the comment section below what you think of this new feature. I personally think it's a __great addition to GitHub Actions__ that finally opens so many new scenarios.

Once again, [watch the video on YouTube](https://youtu.be/S5eZ0YOLJDc) to see this live with the whole explanation.