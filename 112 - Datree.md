Starting with Kubernetes is relatively easy. What is hard is __doing it the right way__, applying all the best practices, and __preventing misconfigurations to affect the security and reliability of your production__ environments.

Luckily, there is a tool that not only can do it for us, but it is also __powerful__, really easy to use, and you can start with it for free! ___Datree___.

Today I'm going to tell you everything about it: how to install it, what it can do for us, __how to use it__ locally and in our CI systems, and of course why we would want to use it.

### About Shifting Left

If you've been following this blog or the [YouTube Channel](https://youtube.com/CoderDave) for a while, you know that I'm a big proponent of the __shift-left strategy__. 

![Shift Left](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/m2y0gteybc93ucnw9set.png)

Whether it is testing, security, or validation, I believe we should do it __as soon as possible in the development workflow__.

When it comes to __validation and security__, however, there are just a handful of tools that are really designed with that "shif-left" in mind. And if we talk about Kubernetes-specific tools, then you can count them on the fingers of one hand.

Today we talk about one of those tools, which promises to be the __one-stop-shop for Kubernetes and Helm configuration and best practices validation__. And boy it delivers!

### About Datree

The tool I'm talking about is called ___Datree___. It's a CLI-based tool which works on Windows, Linux, and MacOS, and it is __Open Source__.

{% github datreeio/datree no-readme %}

Datree can do several things for us, and we will explore them in just a second, but the key point for me is that __it works just the same on a local development environment, in any CI system, and anywhere else__.

It can even be configured as a pre-commit git hook, allowing us to truly shift the Kubernetes validation left. (Take a look [here](https://hub.datree.io/git-hooks) for references on this)

At the time of writing, Datree uses __some 30 predefined rules and policies based on best practices__, but it allows you to customize those rules and, in the very near future, even define new custom rules to fit all your needs.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube aM7EVflmEt4 %}

[Link to the video: https://youtu.be/aM7EVflmEt4](https://youtu.be/aM7EVflmEt4)

If you rather prefer reading, well... let's just continue :)

### Installing Datree

> Demo for this section in the video starts at [minute 2:04](https://youtu.be/aM7EVflmEt4?t=124)

Alright, enough talking, let's install it and see it in action.

If you are on __Linux or MacOS__, you can just execute this command:

```bash
curl https://get.datree.io | /bin/bash
```

In __Windows__ instead, you can use PowerShell:

```powershell
iwr -useb https://get.datree.io/windows_install.ps1 | iex
```

There are also options to run this in __Docker__, or using __Homebrew__ (see [here](https://hub.datree.io/))

As you can see, the installation is really quick, just one command, and it is also very fast.

There is one more step we should do for a proper configuration, but will see that in just a second. Let's first try and use the tool.

### First Scan with Datree

> Demo for this section in the video starts at [minute 3:05](https://youtu.be/aM7EVflmEt4?t=185)

To start a scan with Datree, you use the `datree test` command, passing the file(s) you want to scan:

```powershell
datree test myk8smanifest.yml
```

After just a few seconds, the tool will get you the output:

![Scan Output](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bt3t0posuoceugmpmb9b.png)

As you can see the tool does multiple things:

- it validates the YAML, to make sure everything is ok (_so it is basically also a YAML linter)
- it validates the Kubernetes-specific schema against a predefined version
- it checks the manifest against the policies

At the bottom there is a _summary table_ that also contains a link with a `cliId`, or token:

![Scan Summary](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/6q5mmu3ea5zhanp9ykgm.png)

A new token is generated __every time you execute the very first scan__ on a new system.

If you click on the link, the login page will show up and you have the choice to login (create a new account) using you GitHub or Google account.

After logging in, the Datree Dashboard appears.

![Datree Dashboard](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ieh0k3q8195tinzu5p55.png)

This is the __Centralized Policy Management__ dashboard, which is one of the key points of the service. In here you can see the rules that are applied to the scans (_by default 21 over 30_) and for each rule you can have additional information clicking on the `i` button.

![Rule info](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/i3c3vbhanoex9wzzyxwf.png)

This will take you to the documentation page relative to that rule, where you can find the complete information about it.

The interface is pretty minimal, but I appreciate it because __it contains all and only the information you need__ and therefore it is not confusing.

### Kubernetes Schema Version

> Demo for this section in the video starts at [minute 5:46](https://youtu.be/aM7EVflmEt4?t=185)

As mentioned before, Datree validates your manifests for a specific predefined version of the Kubernetes schema. There are 2 ways to change the version.

#### Via the Settings

The first way is to go to the settings (using the user icon in the upper right and selecting _settings_).

![Change Kubernetes schema version](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/tcizens9cly21bjmub5u.png)

Here you have the dropdown for the version selection, from v1.15.0 to the latest one.

Be careful with this setting, though, because __changing the version here will change it for each and every scan__ you perform with Datree.

#### Via the CLI

If you want to perform a one-off scan against a specific Kubernetes schema version, instead, you can override the value in _settings_ using the `--schema-version` __CLI flag__:

```powershell
datree test --schema-version 1.20.0 myk8smanifest.yml
```

This, for example, will run the schema validation against the version 1.20.0 of Kubernetes schema, no matter what the default selected version is.

### Configuring Datree

> Demo for this section in the video starts at [minute 6:44](https://youtu.be/aM7EVflmEt4?t=404)

As I've mentioned before, there is a __simple configuration change__ that we should make. But I wanted to show you the tool without doing that first, because __it just works__. Really easy and quick setup indeed.

The configuration I'm talking about is the Token. Before I said that Datree generates a new token every time you run the first validation on a new system. I've also said that the centralized policy management is of the key features of the service. But how can we centrally manage the policies and assign them to all our users and system if the token changes every time?

Well, the answer is the __Account Token__!

![Account Token](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/d9l13726hd0b8cjg996u.png)

If you go again in the _settings_ you will notice that you have a __Token__ field. Just copy the value of the Token, and replace it in the __Datree configuration file__ in your system. You can find the file with this path: `~/.datree/config.yaml`

Once this is done, you can start managing your policies and rule effectively.

Also, thanks to the token, every time you run a validation with Datree you will see it in the History:

![Datree History](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xpexkb3738ulxuxtxol6.png)

In here you not only have recorded all your scans, but also __the results__.

### Policy Management

> Demo for this section in the video starts at [minute 8:35](https://youtu.be/aM7EVflmEt4?t=515)

Alright, let's finally talk about the __Centralized Policy Management__ :)

With the token in place, we can use the dashboard to the fullest. We can of course ___enable___ and ___disable___ the rules, using the toggle next to the rule's name. As soon as you do it and re-scan your manifest files, you'll see the new rules being taken in consideration. The changes are __automatically propagated__ to all the clients that use the same token.

You can also customize the output message of the rules.

![Edit Custom Message](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5lsrculxercc41qozu3v.png)

This is very useful if you want to give additional information to your user regarding a specific exception or how to solve it.

![Custom Message Output](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sf3kn2hmpy7de0fp4qjj.png)

Again, the changes are automatically propagated so you will see the new message __as soon as you execute a new validation__ scan.

This is already pretty cool by itself because it assures you have __uniformity across environments__. But it is not all, __we can do more__.

We can in fact __create multiple set of rules__, or _policies_ using the Datree naming.

![Multiple Policies](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/knv61bkjo1e3347wr65l.png)

The creation is done directly from the UI, just click on the "_Create Policy +" button, give it a name, and start enabling the rules you want. You can also __clone an existing policy__ and customize it, as well as deleting existing policies.

Once you have a new policy created, you can use it for your validation instead of the default policy using the `--policy` flag:

```powershell
datree test --policy MyNewPolicyName manifest.yaml
```

About __deleting a policy__, remember that if you try to use a policy that doesn't exist anymore Datree won't fall back to the default one, will give you an error message.

### Policy as Code

> Demo for this section in the video starts at [minute 11:29](https://www.youtube.com/watch?v=aM7EVflmEt4&t=689s)

There is one more thing about policies and rule I want to show you. It's been ___very recently introduced___ in the product, and it will make all of you code-enthusiast very happy: __Policy as Code__.

As we have seen, by default Datree uses the UI to manage policies and rules. If we want to use _Policy as Code_, we have to enable it.

![Policy as Code Setting](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/03dlmexbwkm2bs0gcxw8.png)

Remember that once the _Policy as Code_ mode is enabled, the only way to change the policies in your account is by __publishing a YAML configuration file__ (`policies.yaml`) with the defined policies.

We can either create a policy file from scratch or, as I'd recommend, __download the default file and customize it__.

The Policy file, as you can see in an extract below, is just a normal yaml file that contains the definition of the rules, and other metadata for the policy:

```yaml
apiVersion: v1
policies:
  - name: Default
    isDefault: true
    rules:
      - identifier: CONTAINERS_MISSING_IMAGE_VALUE_VERSION
        messageOnFailure: Incorrect value for key `image` - specify an image version to avoid unpleasant "version surprises" in the future
      - identifier: CONTAINERS_MISSING_MEMORY_REQUEST_KEY
        messageOnFailure: Missing property object `requests.memory` - value should be within the accepted boundaries recommended by the organization
      - identifier: CONTAINERS_MISSING_MEMORY_LIMIT_KEY
        messageOnFailure: Missing property object `limits.memory` - value should be within the accepted boundaries recommended by the organization
    [...]
```

You can __disable a rule__ by commenting the line with `#`

```yaml
    [...]
      # - identifier: CONTAINERS_MISSING_IMAGE_VALUE_VERSION
      #   messageOnFailure: Incorrect value for key `image` - specify an image version to avoid unpleasant "version surprises" in the future
      - identifier: CONTAINERS_MISSING_MEMORY_REQUEST_KEY
        messageOnFailure: Missing property object `requests.memory` - value should be within the accepted boundaries recommended by the organization
    [...]
```

And once again you can __change the output message__ by editing the `messageOnFailure` field.

You can also __create one or more new policies__, simply copy/paste the same structure, change the name, set the default, and you are done.

```yaml
apiVersion: v1
policies:
  - name: Default
    isDefault: true
    rules:
      # - identifier: CONTAINERS_MISSING_IMAGE_VALUE_VERSION
      #   messageOnFailure: Incorrect value for key `image` - specify an image version to avoid unpleasant "version surprises" in the future
      - identifier: CONTAINERS_MISSING_MEMORY_REQUEST_KEY
        messageOnFailure: Missing property object `requests.memory` - value should be within the accepted boundaries recommended by the organization
    [...]
  - name: AnotherPolicy
    isDefault: false
    rules:
      - identifier: CONTAINERS_MISSING_IMAGE_VALUE_VERSION
        messageOnFailure: Incorrect value for key `image` - specify an image version to avoid unpleasant "version surprises" in the future
      # - identifier: CONTAINERS_MISSING_MEMORY_REQUEST_KEY
      #   messageOnFailure: Missing property object `requests.memory` - value should be within the accepted boundaries recommended by the organization
    [...]
```

Once you are satisfied with your policy file, it's time to __make it available__ to the service by publishing it.

```powershell
datree publish policyfile.yaml
```

Once a new policy configuration file is published, it will __override the existing policies__ set up in your account.

That's it, now you can start using your new policies as we have seen before.

Using Policy as Code is super interesting, because then as we do with any normal source code and the different "_as code_" models like IaC, CaC, etc, we can __version__ them, store them in our source control platform, and even __use Pull Requests, Code Review, etc__ to make sure they are exactly as we want them to be and to keep them __under control__.

### Datree for Helm

> Demo for this section in the video starts at [minute 18:04](https://www.youtube.com/watch?v=aM7EVflmEt4&t=1084s)

So far we talked about validating Kubernetes manifests. Datree, however, supports also the __validation of Helm charts__!

Datree provides a __Helm plugin__, so the validation can be run directly from the Helm CLI.

```powershell
helm plugin install https://github.com/datreeio/helm-datree
```

Once installed using the command above, you can just run the `helm datree test` command passing the folder containing your helm charts as a parameter.

After the scan is completed, you'll have the __same results__ as you do running the datree CLI directly.

### Datree Pricing

Cool right? I have one more thing for you: let's talk about pricing.

As I've said before, __Datree is free to start with__... and actually it's __totally free to use for a number of scenarios__. You get in fact __1000 free policy scans__ per month, every month, and it doesn't matter if you scan a single file or a hundred... __one "datree test" execution counts as one policy scan__.

If you need more than 1000 scans per month, there are paid options.

![Datree Plans](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/3ezzubclo3yxaie8lky7.png)

You can get __2000 policy scans a month and additional support__ with the Pro Plan, and __customizable amount of policy scans__ and dedicated support with the Enterprise Plan.

![A Month for Free](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/fiej4wn4mfwlpr8fy4nx.png)

Even better, you can get 1 month of the Premium plan for FREE is you use this link: [https://app.datree.io/?utm_source=coder-dave&medium=youtube](https://app.datree.io/?utm_source=coder-dave&medium=youtube)

### Conclusions

So, what do you think about Datree? Is it something you will adopt as part of your workflow? Let me know in the comment section below, I'd really like to know it.

You may also want to watch [this video](https://youtu.be/4Oa5HneTuKs) in which show you how to deploy to Kubernetes in Azure Pipelines starting from scratch.

__Like, share and follow me__ 🚀 for more content:

📽 [YouTube](https://www.youtube.com/CoderDave)
☕ [Buy me a coffee](https://buymeacoffee.com/CoderDave)
💖 [Patreon](https://patreon.com/CoderDave)
📧 [Newsletter](https://coderdave.io/newsletter)
🌐 [CoderDave.io Website](https://coderdave.io)
👕 [Merch](https://geni.us/cdmerch)
👦🏻 [Facebook page](https://www.facebook.com/CoderDaveYT)
🐱‍💻 [GitHub](https://github.com/n3wt0n)
👲🏻 [Twitter](https://www.twitter.com/davide.benvegnu)
👴🏻 [LinkedIn](https://www.linkedin.com/in/davidebenvegnu/)
🔉 [Podcast](https://geni.us/cdpodcast)

<a href="https://www.buymeacoffee.com/CoderDave" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 30px !important; width: 108px !important;" ></a>

{% youtube aM7EVflmEt4 %}