Securing on Organization in Azure DevOps is a __pretty important__ thing to do. 

Today I'm gonna show you exactly how you can do it using tools like security policies, multi-factor authentication, and much more.

### Intro

I've decided to make this post because working with many companies and organizations I've noticed that often the security of development tools and environments is not the priority.

But the question is: ___how can you keep safe your production if you don't take care of all the previous stages and environments___? And anyway often tools like Azure DevOps and Azure Pipelines are accessing production in some form, especially for deployment... so, better keep everything safe and secure, right?

There are many tools we can use to __secure our Azure DevOps organization__. I will try to cover most of them here but let me know in the comment section below if you have any other use case or scenario you would like me to cover, or if you are using a tool or technique I haven't mentioned.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube nrYSu_046cw %}

[Link to the video: https://youtu.be/nrYSu_046cw](https://youtu.be/nrYSu_046cw)

If you rather prefer reading, well... let's just continue :)

### Connect to AAD

First thing you want to do  in your Azure DevOps organization is __connecting your Azure DevOps organization with your Azure AD tenant__. This, as we will see, brings so many advantages to the table. Benefits like strong ___identity governance___, ___MFA___ (Multi Factor Authentication), ___access policies___, etc.

> Watch the [video](https://youtu.be/nrYSu_046cw) to see how to connect AzDO to AAD

![Connect AAD](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/62fst8im0fx8w1p0bfe2.png)

Note that you need to do that with an account that has the __proper permissions__ in your Azure AD. 

Also, if you have already other users in your Azure DevOps organization that don't belong to the Azure AD tenant you have chosen, they will temporarily loose access to the organization. You can eventually __map them back__ to other users or __invite them__ to your Azure AD.

Alright, now that your Azure DevOps organization is connected to Azure AD, let's see what we can do with it.

### Dynamic User Access

First cool thing is the Dynamic User Access. Let's say you have some groups in Azure AD where all your developers are. You can __dynamically add access__ for azure DevOps project using the Azure AD group rule.

Just go to _Users_ under your organization settings, then click on _Group Rules_, and _Add a group rule_.

![Group Rules](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/w8r2w9o5n591x7gups88.png)

Search for the group you have in Azure AD, select the Access Level you want to Grant, and the projects you want to grant it to.

That's it, now __every AD user in that group will be able to access__ the projects you've selected, with the access level you've set.

You can always add or remove projects, and the AD administrators can manage these accesses without using the Azure DevOps settings, directly from Azure AD.

There is more to say about this, we are just scratching the surface here, so let me know in the comments section below if you want to see this explored more in depth.

### Conditional Access Policies

Probably the most useful thing you can do thanks to Azure Active Directory, and I promise that after this one we will move to something that doesn't require AAD, aside from a bonus one at the end, is enabling the __Conditional Access Policy Validation__. 

You can find this setting under the "_Policies_" menu inside "_Organization Settings_".

When you enable it, you'll be able to enforce all the policies you have in AAD.

![AAD access policies](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ivahd1s9qxrxyetoss3v.png)

Things like allowing the connection to Azure DevOps only from __specific IP Addresses__, or __authorized computers__, and so forth.

### More Policies

We've just seen the Policies page when enabling the conditional access from AAD, but there's more to it. As you can see, the __available policies you can enable vary__ whether you have your organization connected to AAD or not, but there are some common ones.

![Policies AAD vs No AAD](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/pz8xntx4r2mp7jwuwtlo.png)

The first one, the __Alternate Credentials__ for authentication, shouldn't be actually there anymore. Will go away very soon, so disable it straight away and __use Personal Access Tokens instead.__ If you want to know how to create a PAT in Azure DevOps, I have [a post](https://dev.to/n3wt0n/how-to-create-a-personal-access-token-azure-devops-2fm7) and [a video that explains just that](https://youtu.be/o1rrrVKzc-o).

The second policy is to enable 3rd party Apps to connect to Azure DevOps using __OAuth__.

![OAuth Policy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4hq3be8tuyn8gtnem4fc.png)

It's enabled by default, but you can turn it off if you don't plan to use any third-party application. __I wouldn't recommend it__ though, because most like you will use applications that need OAuth.

Next one is similar, but it cover __SSH authentication__.

![SSH Policy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/z4ytdr1bokamnwwqv3hq.png)

Again this is enabled by default, and as the name says it enables Azure DevOps to __generate encryption keys__ for using with Linux, macOS, and Windows running Git for Windows. I would not recommend turning this off either.

Finally, here we have the __Allow public projects__ policy. 

![Public Projects Policy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xipone2qvf2wmxkaqnex.png)

As the name says, when enabled it give the possibility to the users to __create public projects__. It is disabled by default, because ___public projects are visible to anyone___ who has a link to them. Enable this only if you want to have your code publicly available.

### Organization Permissions

Final topic I want to talk about today is fine tuning your Organization permissions. Azure DevOps has __great and rich permission management system__.

> Watch the [video](https://youtu.be/nrYSu_046cw) to see this in action

Going to the "_Permissions_" menu in the _Organization settings_, you can __fine tune all the permissions__ if they don't meet your company policies or they don't suit your needs. In here you can manage the policies for __Groups and Users separately__.

Working on __Groups__, you can set the permissions for each part of the service. For example, the Group that is supposed to work only on CI\CD won't need access to the creation of Processes for Azure Boards, so you can remove that. You can add members to a group, and change its __general settings__.

When working on __Users__, instead, you can really fine tune all their permissions. Let's say you have a user that needs to be able to __perform some additional operations__, either extemporary or as part of his duty. You can easily access their profile and enable them on the permissions needed. This will __override__ the permissions the user has as part of the groups they are in.

### Disable Organization Creation

Ok, almost done. But as promised, a __bonus policy__ for you.

Working with a lot of clients, I've noticed that there is a tendency where __all the company departments create new organizations__ in Azure DevOps, and IT department can’t control the security settings and who has rights to access the source code.

Thanks to the Azure AD integration, however, __we have a solution__.

In the _Azure Active Directory_ page under _Organization Settings_, in fact, we have this __Restricting organization creation toggle__.

![Org Creation Policy](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xq655y5ly6vzi7su639c.png)

When Enabled, creation of new Organizations for users in your AAD will be disabled. Only users in the ___Azure DevOps Administrator___ group and users you add to the "_Allow list_" will be able to create new orgs.

> If you don't see the toggle in your settings, make sure the user you have logged in into Azure DevOps with is added to the "_Azure DevOps administrators group_" in your Azure AD. By default no user is.


### Conclusions

Alright, that's it for today.

Let me know in the comment section below if you've found this guide useful, if you use any other technique to secure Azure DevOps, and if there is any area you would like for me to go deeper into.

You may also want to watch [this video here](https://youtu.be/o1rrrVKzc-o), where I explain how to create the Personal Access Tokens.

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

{% youtube nrYSu_046cw %}