GitHub has just introduced the ability to set an __optional expiration date on personal access tokens__ (PATs). Users are now able to choose an expiration from a set of preset values, or specify a custom expiration date using a calendar drop-down.

Let's take a look at this new feature!

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube f7t7cJp2v00 %}

[Link to the video: https://youtu.be/f7t7cJp2v00](https://youtu.be/f7t7cJp2v00)

If you rather prefer reading, well... let's just continue :)

### The Problem

Personal Access Tokens, or PATs, provide users with a quick way to create OAuth access tokens which they can use instead of passwords to make API calls or use services.

However, until now PATs __didn't offer an expiration option__, meaning they exist until they are manually disabled. Long-lived tokens can create __large security implications__ if they leak. 

Now this new optional expiration date increases both user's and organization's ability to secure how their data is accessed.

### Set the Expiration Date

To set the expiration date to a PAT just go to the _PAT creation_, under `Your Profile > Settings > Developer Setting > Personal Access Tokens`, and in here after clicking on the "_Generate new token_" button you'll have, among the other things, the new "Expiration" drop down.

![Dropdown](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/wiwv0jp0v0fmofmhaenk.png)

Here you can select any of the pre-defined options, between 7 and 90 days, or insert a custom expiration date.

![Dropdown values](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/t09q1uvq2jahcpb21xc7.png)

There is still the possibility to have non-expiring tokens, as you can see, but it is __highly not recommended__ since, as I've mentioned before, that could represent a security issue in case the tokens leak.

It is also possible to update existing tokens, adding the expiration date... however, that requires the re-generation of the token key.

### Conclusions

Let me know in the comment section below what do you think about this feature. And if you are new to Personal Access Tokens in Github, I highly encourage you to checkout [this post](https://dev.to/n3wt0n/how-to-create-a-personal-access-token-pg7) or [this video](https://youtu.be/SzrETQdGzBM) where I explain everything you need to know about them.

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

{% youtube f7t7cJp2v00 %}