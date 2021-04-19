GitHub lets you save your secrets, like credentials, keys, etc., and use them in GitHub Actions.

Let's see _how Secrets work in GitHub and how to manage them_.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube tXv_npAP90k %}

[Link to the video: https://youtu.be/tXv_npAP90k](https://youtu.be/tXv_npAP90k)

If you rather prefer reading, well... let's just continue :)

### Secrets Levels

First thing we have to say is that there are 3 levels of secrets you can use in GitHub. Secrets at Organization Level, at Repository Level, and inside GitHub Actions Environments.

![Secrets](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z0cl5truopcb8acyu5vw.png)

#### Organization Secrets

The organization secrets allow you to __share secrets__ to different repositories without the need of duplicating them. They can also be scoped to specific repositories or used in all of them. Remember that they aren't available in the free plan.

#### Repository Secrets

Repository secrets, instead, as the name says are __scoped to single repo__. They can be used to override the organization-defined secrets, when using the same name, and are available on the free plan.

#### Environment Secrets

Finally, the Environments Secrets. They are scoped to a __specific environment_, and can override both Organization and repo secrets. They are available on the free plan, but only for public repos.

### Secrets Hierarchy

Feature wise, those three levels are __equivalent__, but they have a different hierarchy and precedence.

Organization secrets are of course defined at the highest level, then we have the repository secrets underneath, and finally the environment secrets, since environments are defined inside a repo.

When the GitHub Actions engine needs to access those secrets, it will __first look into environments__. If there is no environment secret defined with that name, it will __fall back to the repository secrets__ and use those ones. And again, if there is no secret with that name, GitHub Actions will __fall back again to the organization secrets__, if you are in a context withing an organization.

If no secret with the given name is found in any of the secrets stores, then you'll get an error.

### Create, Update and Manage Secrets

Let's quickly see now how to create, update, and manage those secrets.

▶ Check the [demo section of the video](https://youtu.be/tXv_npAP90k?t=122)

Once again, remember that once the secret has been saved, it __will not be possible to retrieve its value manually__ via UI or APIs. Only the GitHub Actions engine will be able to consume it.

### Conclusions

Let me know in the comment section below how you manage your secrets and if you want me to cover the integration with 3rd party secrets providers like Azure KeyVault.

Also, you may want to check out [this video](https://youtu.be/w_37LDOy4sI) which talks about GitHub Actions Environments in detail.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

{% youtube tXv_npAP90k %}