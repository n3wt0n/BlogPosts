Today we talk about how to __use GitHub in VS Code__, and I have __3 ways__ for you to do so. Actually 4, I have a __bonus one for you at the end__ so make sure you'll stick around for it.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube aUhl3B6ZweQ %}

([Link to the video: https://youtu.be/aUhl3B6ZweQ](https://youtu.be/aUhl3B6ZweQ))

If you rather prefer reading, well... let's just continue :)

### Source Code

> Watch the demo for this [in this section of the video](https://www.youtube.com/watch?v=aUhl3B6ZweQ&t=40s)

The first way to use GitHub in VSCode is, as you probable can imagine, the __source control part.__

To use GitHub in VSCode as Source Control you don't need to install any external component. When you open it you can already __Clone__ a repository and then click on "Clone from GitHub". When you do so it will ask for logging in and after you've done it you'll have a list of all the repositories you have the rights to work on.

Just pick one, choose the local folder where you want the code to be stored and you're done.

After changing the code, you can go to the Source Control icon in the menu to stage and commit your code locally. Remember to add a commit message! And when you're ready to save the changes to GitHub, just click on the Push button and your new code will be uploaded to GitHub.

Ok, this was straight forward. Let's move to the next one...

### Pull Requests

> Watch the demo for this [in this section of the video](https://www.youtube.com/watch?v=aUhl3B6ZweQ&t=80s)

...which is __Managing your Pull Requests in GitHub from within VS Code__.

For this one, we need to install the ___GitHub Pull Requests and Issues___ extension.

To do so, just head over the Extension tab in the menu bar, and just search for GitHub. I recommend using the official one as you can see here.

After you've installed it, just head over the new icon that appears in the menu.

Here you will see all the Pull Requests of the project you're working on.

You can also create a new PR, just selecting the target branch, setting the Title and that's it. This creates a new Pull Request and of course then you will be able to edit it as well.

If instead you want to work on PRs that are already open, you can __search__ them in the different categories.

Just select one, and you can see it's description page, and review each file in it.

After reviewing it, you can add your comments to it, and request changes, approve it, or close it.

Finally, if everything is ok, you can merge it back to your main branch. 

Also this was really easy to do, I think __the PR experience for GitHub in VSCode is pretty cool__. It might not be as powerful as the one in GitHub's web interface, but it is pretty close.

### Issues

> Watch the demo for this [in this section of the video](https://www.youtube.com/watch?v=aUhl3B6ZweQ&t=145s)

Alright, next one is __managing issues from within VSCode__.

To manage Issues, you need the __same extension__ we have seen before, as well as the same menu tab.

In here you can see all the issues that are assigned to you and created in the repo you are working on .

You can create an issue as well, just click on the plus sign and fill in the fields. If you have custom issues templates those will appear here and you'll be able to use them instead.

After creation, you will have 2 options. You can either use the globe icon to open the issue on the web, unfortunately it is not yet possible to manage or edit the issue directly in VSCode, Or you can use the arrow icon.

This will automatically assign the issue to you, and in fact you see it under "_My Issues_".

This function will also automatically assign the issue to the next code commit.
If you want to avoid that, you can use the square box icon. The issue will still be assigned to you but won't be associated to the commit.

### Bonus: CodeSpaces

> Watch the demo for this [in this section of the video](https://www.youtube.com/watch?v=aUhl3B6ZweQ&t=210s)

Those were the 3 ways we have right now to work with GitHub from VSCode. But as I promised, I have a bonus one for you! We can __manage and use our GitHub CodeSpaces__ from VSCode.

To use GitHub CodeSpaces from VSCode, first we need to have the proper extension installed. Go to the extension menu, and search for CodeSpaces. Here you find the Github CodeSpaces one that you can install.

This will add a new item to the Remote Explorer tab. You can head to it, and choose "Github CodeSpaces" from the dropdown menu.

Here you will be able to see your existing CodeSpaces or create a new one.

To create a new one, click on the plus, select the repository in which you want to create it, pick the branch, and select the size of the new CodeSpaces environment.

If you want to connect to an existing one, instead, just click on it and use the "plug" icon.

This will start and load the CodeSpaces Environment and let you manage it as you would normally do on the web interface.

Lastly, you can either disconnect from an environment, or stop it entirely, from within the Remote Explorer tab as well.

If you wanna know more about GitHub CodeSpaces, I have an entire [series of videos about them you can check out](https://youtube.com/playlist?list=PL-HoEl0ZEUlKDm-ws2KQP8np-4Km7MSda).

### Conclusions

Let me know in the comment section below how you use GitHub with VSCode, or... VSCode with GitHub... Do you do something I haven't shown? Do you know any other way to use GitHub in VSCode? Comment down below and share it with all of us.

{% youtube aUhl3B6ZweQ %}