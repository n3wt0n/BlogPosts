If you want to create a new __GitHub Personal Access Token__ but you don't know where to start, this article is for you!

### Intro

Today we talk about GitHub Personal Access Tokens, PATs, and how to create them.

Personal access tokens (PATs) are an alternative to using passwords for authentication to GitHub when using the GitHub APIs, the command line, or any integration really.

Although their creation is pretty straight forward, most people either don't know where to start or, as it happens to me all the time 😅, just forget about it...

Let's do it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube SzrETQdGzBM %}

([Link to the video: https://youtu.be/SzrETQdGzBM](https://youtu.be/SzrETQdGzBM))

If you rather prefer reading, well... let's just continue :)

### Create a PAT

To create a PAT, just go to your profile menu in the upper right corner > _Settings_ > _Developer Settings_ > and finally click on _Personal Access Tokens_.

[IMAGE 01]

Here you have the list of all the PATs you've created, together with the date you last used them.

Now just click on the _Generate new token_ button, select the __Scope__, click _Generate Token_ and you're done.

[IMAGE 02]

> __IMPORTANT__: after generating a token, you will see the token itself. Be sure to copy this value because it will __disappear__ as soon as you leave or refresh the page and you will ___never___ be able to retrieve it again.

### Authorize a PAT for SSO

If you want to use a PAT to access resources owned by an __organization that uses SAML SSO__, you must authorize the PAT. 


> Final note: As a security precaution, GitHub __automatically removes__ personal access tokens that haven't been used in a year.

### Announcement

Before closing, I have an __announcement__ to make, which I'm very excited about. I've finally launched my [__Patreon page__](https://patreon.com/CoderDave). You can get __exclusive content__, both posts and videos that are not posted anywhere else. You can influence the content of this blog and my YouTube channel, you can have live chats and Q&A with me. But the coolest part is that __you can have a 1:1 consultation with me__ to talk about anything DevOps, GitHub or Azure DevOps.

Visit my Patreon page to see the options available, just go to [patreon.com/CoderDave](https://patreon.com/CoderDave).

### Conclusions

Now you should be able to create any PAT you need in GitHub. Let me know in the comment section below if you have any questions about this.
