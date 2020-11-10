Branch protection is part of a powerful set of configuration options that give repository administrators the ability to enforce security policies by preventing accidental branch deletions, enforcing code reviews, and requiring successful automated checks before pull requests can be merged.

These options offer an effective way to __increase code quality without obstructing effective collaboration__. Finding the right combination of settings to achieve the desired effect is very important.

Let's explore the best practices to help you maintain a healthy codebase without impairing collaboration. You will learn when and how to use required status checks, branch restrictions, required reviews and more.

### Intro

Today we are going to talk about the __best practices around branch protection and branch policies__, what I'll cover can and should be easily adapted to any Git SCM.

In fact I've already published [a video where I show how to enable branch protection in both Azure DevOps and GitHub](https://youtu.be/Y6YUHG8Es-Y).

I'm gonna group the best practices into 4 main categories:

- Branch protection
- Branch restrictions
- Required status checks
- Required pull request reviews

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation and demo, which to be fair is much ___more complete___ than this post.

{% youtube gUJ52Shwtm0 %}

([Link to the video: https://youtu.be/gUJ52Shwtm0](https://youtu.be/gUJ52Shwtm0))

If you rather prefer reading, well... let's just continue :)

### Why doing Branch Protection?

Before going into the details, __why is branch protection important__ for both Open Source projects and organization?

Collaborators with write access to a repository have __complete write permissions on all its files and history__. 

While this is good for collaboration and innersouce, it’s not always desirable: for example, somebody may accidentally delete an important branch or overwrite its commit history by force pushing incompatible changes.

Another common scenario is a collaborator introducing bugs by adding work that hasn’t been tested.

Branch protection and branch policies offer a number of tools to achieve collaboration while helping you keep your __repositories in good shape__ and __avoiding unnecessary obstructions__ in your development workflow.

### Branch Protection

Let's talk about the first category: branch protection.

You can protect any branch in any repository and by enabling this setting you will ensure that:

- the __branch cannot be deleted__, either accidentally or intentionally
- the branch commit history __cannot be overwritten__ with an alternate set of changes (force push)

These are the Best Practices:

![Branch Protection BP](https://dev-to-uploads.s3.amazonaws.com/i/09kcugb35zq2xzyxzqw1.png)

[Check this video for the whole Best Practices details: https://youtu.be/gUJ52Shwtm0](https://youtu.be/gUJ52Shwtm0)

Please note that collaborators with write permissions pushing commits to the top of a protected branch, either directly or by merging pull requests without merge conflicts __will remain unaffected__ by this setting. That’s because merging a pull request is in fact equivalent to pushing its commits to the target branch.

### Branch Restrictions

Next stop: Branch restrictions

It’s possible to restrict the teams or individuals who can push to a branch at all by enabling the option "_Restrict who can push to this branch_" and specifying their names on the list.

By default, all collaborators who have been granted write permissions to the repository are able to push to the protected branch. By explicitly specifying permitted collaborators, __you will narrow down the list of existing collaborators who can push to the branch__.

It’s important to understand the __implications__ of using this option especially in conjunction with the others.

By enabling this setting you can prevent a user from pushing commits to a branch while still allowing them to open pull requests. And again this will prevent them from being able to merge their own pull requests and therefore only the users in the list will be able to do that.

The best practices in this case are the following.

![Branch Restrictions BP](https://dev-to-uploads.s3.amazonaws.com/i/clmp0d8xcy3f3uwhxcpe.png)

[Check this video for the whole Best Practices details: https://youtu.be/gUJ52Shwtm0](https://youtu.be/gUJ52Shwtm0)

As a side note, Branch restriction is a type of branch protection that is __available for public and private repositories__ owned by organizations in ___GitHub Team, GitHub Enterprise Cloud, and GitHub Enterprise Server___.

### Required Status Check

Next one is Requiring status checks to pass before merging.

If you test your code with a continuous integration system that sends build statues back to your SCM, like for example using GitHub Actions, you can __avoid broken code by requiring one ore more status checks to pass__ on a branch before allowing pull requests to be merged.

A very common scenario is enabling branch protection on the main branch turning on "_Require status checks to pass before merging_".

You can also make sure that checks are ran against the __latest state of the target branch__ of a Pull Request. If the code on the target branch has changed since a pull request has been opened, a message will appear to indicate that those changes need to be merged upstream into the pull request branch before merging. Once the changes are integrated a new build will be triggered and the status checks __will update to reflect the latest state__.

The best practices in this case are pretty straight forward.

![Required Checks BP](https://dev-to-uploads.s3.amazonaws.com/i/zt7gzgatob8frddb9upl.png)

[Check this video for the whole Best Practices details: https://youtu.be/gUJ52Shwtm0](https://youtu.be/gUJ52Shwtm0)

### Required Pull Request Reviews

Lastly, let's talk about requiring pull request reviews before merging.

Code reviews are a __critical part__ of any development workflow. You can require at least one review and approval by checking the "_Require pull request reviews before merging_" checkbox. This option alone is very useful and when used in conjunction with required status checks it provides teams certain “collaboration guardrails” to help with __writing better code while maintaining high levels of productivity__.

In fact, when you enable this setting you will ensure that __no pull request can be merged without at least one approved review__ and prevent collaborators from pushing directly to the branch (and merging their own pull requests).

Pull request authors must either respond to requested changes, or dismiss a review, if they are not restricted from doing so by the "_Restrict who can dismiss pull request reviews_" option.

Some SCMs, including __GitHub__, have an advanced tool that makes code reviews even better: __Code Owners__. Repository administrators can define exactly which people and teams need to review projects using the _CODEOWNERS_ file. This new feature automatically assigns reviewers based on Code Owners when a pull request changes any owned files, using the same syntax as the _.gitignore_ file.

For Pull Request reviews, the best practices include:

![Code Reviews BP](https://dev-to-uploads.s3.amazonaws.com/i/tj548auve61n3bwkxth5.png)

[Check this video for the whole Best Practices details: https://youtu.be/gUJ52Shwtm0](https://youtu.be/gUJ52Shwtm0)

### Conclusion

Alright, that's it for today.

Let me know in the comment section below what you think about those best practices, if you follow them already or if you have any other recommendation.
