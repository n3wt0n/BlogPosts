Today we talk about security in GitHub, and specifically about how to properly use and configure GitHub Actions Secrets. 

This article is part of a new GitHub Security Hardening series, so stay tuned for new articles about this topic.

Also, if you are new to GitHub Actions, I recommend you to check the [intro video I made](https://youtu.be/msCWg2F4sck) about the topic, there I cover all you can do with GitHub Actions.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation__.

{% youtube 2yHRq7aWDKM %}

[Link to the video: https://youtu.be/2yHRq7aWDKM](https://youtu.be/2yHRq7aWDKM)

If you rather prefer reading, well... let's just continue :)

### Let's Talk About Secrets

We hopefully all agree that sensitive values should __never be stored as plain text__ in workflow files, but rather as secrets.

Secrets can be configured at the enterprise, organization, repository, or environment level, allowing you to store sensitive information in GitHub, as I explained in [this video](https://youtu.be/tXv_npAP90k).

Storing these secrets is not a problem as everything is safely managed by GitHub. They are even __encrypted on the client side__ before reaching GitHub! However, using them can be problematic.

To help prevent accidental leakages, in fact, GitHub redacts any secrets that appear in run logs and replace their values with stars (`***`).

![GitHub replaces secrets with stars in logs](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/iouqofcln97s8ud850zz.png)

This redaction looks for __exact matches__ of any configured secrets, as well as __common encodings__ of the values, like for example Base64. There are however multiple ways in which a secret value can be transformed, and because of that this redaction is not 100% guaranteed.

As a result, there are some things we can proactively do, and good practices we should follow, to help ensure secrets are redacted and to limit other risks associated with secrets.

### Don't Use Structured Data

First of all, if possible __don’t use structured data as a secret__. Using structured data can cause secret redaction within logs to fail, as redaction relies on identifying an exact match of the secret value. 

![Structured vs Unstructured secrets](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3cqbd32o9etuqaqa9ydp.png)

For example, avoid using a blob of JSON, XML, YAML, or similar as secret value, this significantly reduces the probability that the secrets will be properly redacted. 
Instead, create __individual secrets for each sensitive value__.

Again, this is not always possible, but doing so greatly reduce risks.

### Register ALL Secrets

Another important step is to register all secrets used within workflows. If a secret is used to generate another sensitive value within a workflow, that __generated value should be formally registered as a secret__. This ensures that the value will be redacted if it ever appears in the logs.

![Use Secrets in GitHub Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/jki32zzmdu47kukw5f9h.png)

For example, when using a private key to generate a signed JWT for accessing a web API, it's important to register that JWT as a secret. Otherwise, the JWT won't be redacted if it ever enters the log output.

It's important to note that registering secrets also applies to __any sort of transformation or encoding__. If your secret is transformed in any way (for example with Base64 or URL encoding), be sure to register the new value as a secret as well.

Let me know in the comments down below if you like me to produce an article and/or a video on how to register anything as a secret in GitHub Actions.

### Audit How Secrets Are Handled

In addition, it is important to audit how secrets are handled. This involves reviewing how secrets are used to ensure they are being handled properly. 

To do this, you can review the source code of the repository executing the workflow and check any actions used in the workflow. For example, make sure that secrets are not sent to unintended hosts or explicitly printed to log output.

![Source Code of a GitHub Action handling secrets](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/l4uk0vn58u2ka0ss2lr9.png)

After testing valid and invalid inputs, view the run logs for your workflow and confirm that secrets are properly redacted or not shown. It is not always clear how a command or tool you are invoking will send errors to `STDOUT` and `STDERR`, and secrets may end up in error logs. Therefore, it is good practice to manually review the workflow logs to ensure that secrets are properly handled.

### Use Minimally Scoped Credentials

Next, it’s a good practice, and not only for GitHub Actions Secrets, using __credentials that are minimally scoped__.

Ensure that the credentials used in workflows have the minimum privileges required. Keep in mind that any user with write access to your repository also has read access to all the secrets configured in it.

![Setting the proper permissions for the GITHUB_TOKEN](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/el6vnletkksxtb461i09.png)

Actions can access the `GITHUB_TOKEN` from the `github.token` context and you should ensure that this token is only granted the minimum required permissions. It is good security practice to set the default permission for `GITHUB_TOKEN` to read access only for repository contents. 
The permissions can then be increased for individual jobs within the workflow file, as required.

### Audit and Rotate Registered Secrets

Another thing we should all do when working with secrets is to __audit and rotate__ registered secrets. 

For example, we can periodically review the registered secrets to confirm they are still required and remove those that are no longer needed. I personally set this as a recurrent task for my team so every months we have a review of all secrets.

![Security audit task in Jira](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/59oiwzb0ibn3figgkfh9.png)

We should also __rotate secrets periodically__ to reduce the window of time during which a compromised secret is valid.

### Require Approval for Accessing Secrets

And final good practice, consider requiring __review for access to secrets__.

Not everyone may be aware of this, but you can use required reviewers to protect environment secrets. A workflow job cannot access environment secrets until a reviewer grants approval. 

![Secrets access with approval in GitHub Actions](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/mmx2xpyomlkryjez62bi.png)

This is of course only available in GitHub Enterprise or on public repositories, but it is something __you should definitely do__ if you can.

### Conclusions

Let me know in the comments below if you have any other tip and best practices when working with GitHub Secrets. 

Also, check out [this video](https://youtu.be/tXv_npAP90k), in which I explain how to properly store Secrets in GitHub.

__Like, share and follow me__ 🚀 for more content:

🆘 [Get Help With DevOps](https://geni.us/cdconsult)
📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
📧 [Newsletter](https://coderdave.io/newsletter)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)
💖 [Patreon](https://patreon.com/CoderDave)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube 2yHRq7aWDKM %}