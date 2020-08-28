Pipeline caching can help reduce build time by allowing the outputs or downloaded dependencies from one run to be reused in later runs, reducing or avoiding the cost to recreate or redownload the same files again.

Let's see how to enable and use caching in Azure Pipelines.

### Intro

Hi everybody. Today we talk about how we can reduce the time our Pipelines take to run, using caching.

Caching is especially useful in scenarios where the same dependencies are downloaded over and over at the start of each run. This is often a time consuming process involving hundreds or thousands of network calls.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much ___more complete___ than this post.

{% youtube HfJcN9gWleM %}

If you rather prefer reading, well... let's just continue    :) 

### Why Caching

Why is caching important? If you are on your on-prem machine or dev machine, the build and release processes already have some sort of caching implementation that saves the files or the metadata locally.

However, when it comes to Azure Pipelines Agents, every time a new Pipelines Run starts, you are on an __agent machine that has been created afresh__ just for that run, so nothing is stored there apart from the binaries and services the CICD process needs. This is why you may want to use the cache service.

Remember that caching can be effective at improving build time provided the __time to restore and save the cache is less than the time to produce the output__ again from scratch. Because of this, caching may not be effective in all scenarios and may actually have a negative impact on build time.

### Let's Cache

Caching is added to a pipeline using the ___Cache pipeline task___. This task works like any other task and is added to the steps section of a job.

```yaml
variables:
  solution: '**/WebAppTest.sln'
  NUGET_PACKAGES: $(Pipeline.Workspace)/.nuget/packages
```

```yaml
- task: Cache@2
  inputs:
    key: 'nuget | "$(Agent.OS)" | **/packages.lock.json,!**/bin/**,!**/obj/**'
    restoreKeys: |
       nuget | "$(Agent.OS)"
    path: $(NUGET_PACKAGES)
  displayName: Cache NuGet packages
```

The Cache task has __two required inputs__: _key_ and _path_:

- ___path___ should be set to the directory to populate the cache from (on save) and to store files in (on restore). It can be absolute or relative.
- ___key___ instead should be set to the identifier for the cache you want to restore or save

There is also another parameter, "restore keys", which can be used if you want to query against multiple keys or key prefixes. This is useful to fallback to another key in the case that a key couldn't be found. 

In the example above, I use a __composite key__ with the '_nuget_' string literal, the OS version the agent is running (which comes from a system variable), and finally the content of the '_packages.lock.json_' file. When you specify a file, the engine uses the __hash of the content__ of the file as part of the key so if the content changes, so does the key. I've also specified additional filters so to ignore that file if tit is present in the _bin_ and _obj_ folders.

![Execution](https://dev-to-uploads.s3.amazonaws.com/i/i8yeh2utrwg3fuoxi8u6.png)

When a cache step is encountered during a run, the task will __restore__ the cache based on the provided inputs. If no cache is found, the step completes and the next step in the job is run. After all steps in the job have run and assuming a successful job status, a special "__save cache__" step is automatically injected and run for each "restore cache" step that was not skipped. This step is responsible for saving the cache.

### Skip steps based on cache hit

There are some scenarios in which the successful restoration of the cache should __cause a different set of steps to be run__. For example, a step that installs dependencies can be skipped if the cache was restored. 

```yaml
variables:
  solution: '**/WebAppTest.sln'
  NUGET_PACKAGES: $(Pipeline.Workspace)/.nuget/packages
  CACHE_RESTORED: 'false'
```

```yaml
- task: Cache@2
  inputs:
    key: 'nuget | "$(Agent.OS)" | **/packages.lock.json,!**/bin/**,!**/obj/**'
    restoreKeys: |
       nuget | "$(Agent.OS)"
    path: $(NUGET_PACKAGES)
    cacheHitVar: CACHE_RESTORED
  displayName: Cache NuGet packages

- task: NuGetCommand@2
  inputs:
    restoreSolution: '$(solution)'
  condition: ne(variables.CACHE_RESTORED, 'true')
```

To achieve that, we can use the __cacheHitVar__ param, and pass a variable to it. If there is a cache hit, then that variable value will be changed to _true_.

Then we can use that variable in a __condition__ for the task or step we want to skip.

### Comparison

I've created this comparison table so we can have an overview about the caching performances.

![Comparison](https://dev-to-uploads.s3.amazonaws.com/i/lmp2pic8ubakj5cly937.png)

The __first__ column is the execution with __no cache__.

The __second__ one, instead, is with cache but at first run, which means that there is a __cache miss__. as you can see the overall time is more because not only the dependencies have to be restored as before, but we need to check if the cache exists and, since it doesn't, upload the content and create the cache item.

The __third__ and last column is a __cache hit__. The cache is present, so the dependencies don't have to be downloaded (hence the NuGet Restore step is faster and since the cache doesn't chance there is no time for saving it. And this is faster, even tho for just few seconds because I had just few dependencies in the demo app.

### Conclusion

It is worth noting that caching is currently supported in CI and deployment jobs, but not in classic release jobs.

What do you think of the Azure Pipelines Caching system? Do you use it? Can you see its benefits?
Let me know in the comment section below.

### References and Links

- [Video with full explanation and examples about Pipelines Caching](https://youtu.be/HfJcN9gWleM)
- [Azure Pipelines Triggers series](https://www.youtube.com/playlist?list=PL-HoEl0ZEUlJ72OnulpdyP96rBptxNNOp)
- [Official documentation about Azure Pipelines Caching](https://docs.microsoft.com/en-us/azure/devops/pipelines/release/caching?view=azure-devops)