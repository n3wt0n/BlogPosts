I’ve been using GitHub for quite some time, and a long the way I’ve picked up few tricks and discovered some secrets to manage it, push it to its limits, and personalize my experience. I’m sharing a few of my favorites today, and I'm sure there’s something new and helpful for you.

### Intro

Today we talk about GitHub, and how to use it __better, smarter or at least more conveniently__.

As I've mentioned , there are quite a few tips, tricks and "secrets" when it comes to using GitHub, and perhaps not all of those may be known even to hardcore or long term users.

Let's jump into them!

### Secrets, Tips and Tricks

1. Fuzzy Finder
2. Octotree
3. Supported keywords for closing issues
4. SuperLinter
5. Links to Code Snippets
6. Must-have Markdown formatting tips
7. Magic URLs
8. Branches auto deletion

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much ___more complete___ than this post.

{% youtube sGnqVAfnZ6U %}

If you rather prefer reading, well... let's just continue :) 

### Fuzzy Finder

The first one is the "Fuzzy Finder".

Have you ever tried searching for a specific file in a big GitHub repo and just couldn't find it? I had. But this tip is going to help you.

Press __t__ on the keyboard when you are in any repository page to access it and start typing the name of the file you want to find.

Just type few letters to have the finder filtering the files list, and use the arrows to move between the results. Press enter and... voila! super easy to find anything.

Goodbye navigating through directories in a repo.

### Octotree

Speaking of searching for files, let's go with tip number 2.

This is the only one which actually requires something that is not already integrated into GitHub. There is a great browser extension called ___Octotree___, which helps you navigate directories, and open files with a familiar tree-like structure.

You can find it at [https://octotree.io](octotree.io), and it is fully open sourced [on GitHub](https://github.com/ovity/octotree)

Watch [my video here](https://youtu.be/sGnqVAfnZ6U) to see it in action.

___Bonus points___: It works with GitHub Enterprise, and they have the free version!

### Supported keywords for closing issues

Next stop, maybe not a secret but definitely not very well documented.

Let's talk about keywords for closing issues.

As you probably now, when you commit your code you can add a message that automaticaly closes an associated issue. Commonly people use "fix # number", where the number is the issue number.

For example "_fix #12_" to close the issue number 12.

But there are many others you can use. Here is the list:

```bash
fix #12
fixes #12
fixed #12
close #12
closes #12
closed #12
resolve #12
resolves #12
resolved #12
```

Use any of those and the commit closes the issue automatically.

___Bonus tip___: if the commit is in a PR, the issue gets closed at merge.

### SuperLinter

Next one, the SuperLinter.

Setting up a new repository with all the right linters for the different types of code can be time consuming and tedious. So many tools and configurations to choose from and often more than one linter is needed to cover all the languages used.

Not anymore. The Super Linter is a source code repository that is packaged into a Docker container and called by GitHub Actions. This allows for any repository on GitHub.com to call the Super Linter and start utilizing its benefits. You can find more information about it [here](https://github.blog/2020-06-18-introducing-github-super-linter-one-linter-to-rule-them-all/)

Once again, watch [my video here](https://youtu.be/sGnqVAfnZ6U) to go more in-depth into it.

### Links to Code Snippets

Well, this isn’t so much of a secret, but it’s definitely not known by everyone, and occasionally blows minds.

You can ___link to specific lines of code by clicking the line number___ when you’re viewing a file.

By default, the line number (for example, #L1337) is appended to the URL, which will always take you directly to that line.

You can also link to a line number range by holding down SHIFT and selecting the starting and ending lines.

If that file is edited, deleted, or renamed, unfortunately the link will no longer work as expected. However you can press __y__ on the keyboard or click _Copy permalink_ to generate the canonical URL that will always work.

___Added bonus___: If you add a code snippet permalink in a GitHub comment, a nice visualization of the code appears.

I have a very comprehensive example in [my video](https://youtu.be/sGnqVAfnZ6U)

### Must-have Markdown formatting tips

Let's now talk about Markdow.

GitHub Flavored Markdown is great for vanilla formatting of text and basic tables, but sometimes you need to get creative to make it do what you want.

First thing I want to show you is __Keyboard tags__.

You can use `<kbd>` tags to make text appear like a button, which is slightly different from regular backticked text. It’s perfect for documenting things like keyboard shortcuts or game controls in your READMEs/wikis.

Something like this (but in GitHub it renders more nicely):

 `Use <kbd>ALT</kbd>+<kbd>F4</kbd> to make the magic happen!`   
 Use <kbd>ALT</kbd>+<kbd>F4</kbd> to make the magic happen!

Another cool thing __Visualizing hex codes__.

Placing hex colors in backticks renders a tile in that color. I think it’s totally hexcellent!
Something like this (this works only in GitHub):

GitHub contribution graph colors: 

```
`#C6E48B` `#7AC96F` `#249A3C` `#196127` 
```

This is quite cool, but let's see some formatting which is both cool and helpful.

You can __visualize a diff__ using backticks and diff which highlights lines red or green based on the "minus" or "plus" at the beginning of the line.

` ```diff `  
` This line is unchanged. `  
` - This line has been removed `  
` + This instead has been Added `  
` + And this has been added too! `  
` ``` `

```diff
This line is unchanged.
- This line has been removed
+ This instead has been Added
+ And this has been added too!
```

Last but not least about Markdown formatting... did you know you can __add an accordion-like button__ to your comments to make them smaller and, I have to say, pretty cooler? Check this out.

This:

```
<details>
<summary>Click here to see terminal history + debug info</summary>
<pre>
488 cd /opt/LLL/controller/laser/
489 vi LLLSDLaserControl.c
490 make
491 make install
492 ./sanity_check
493 ./configure -o test.cfg
494 vi test.cfg
495 vi ~/last_will_and_testament.txt
496 cat /proc/meminfo
497 ps -a -x -u
498 kill -9 2207
499 kill 2208
500 ps -a -x -u
501 touch /opt/LLL/run/ok
502 LLLSDLaserControl -ok1
```

Renders to this:

<details>
<summary>Click here to see terminal history + debug info</summary>
<pre>
488 cd /opt/LLL/controller/laser/
489 vi LLLSDLaserControl.c
490 make
491 make install
492 ./sanity_check
493 ./configure -o test.cfg
494 vi test.cfg
495 vi ~/last_will_and_testament.txt
496 cat /proc/meminfo
497 ps -a -x -u
498 kill -9 2207
499 kill 2208
500 ps -a -x -u
501 touch /opt/LLL/run/ok
502 LLLSDLaserControl -ok1

### Magic URLs

Next one, let's talk about URLs

Did you know you can get a user or organization’s avatar just by an url?

You can get the avatar of any GitHub user or organization by visiting `https://github.com/<username>.png!`

This for example is mine: [https://github.com/n3wt0n.png](https://github.com/n3wt0n.png).

This is useful for example when you’re building websites or designs that rely on GitHub accounts, like All Contributor’s table view, or Probot’s app catalog.

But that's not all. You can get the __patch or diff of a commit__ or a pull request in the same easy way in your browser:

`https://github.com/<owner>/<repo>/commit/<sha>.diff`
`https://github.com/<owner>/<repo>/commit/<sha>.patch`

And you can do the same with __pull requests__:

`https://github.com/<owner>/<repo>/pull/<id>.diff`
`https://github.com/<owner>/<repo>/pull/<id>.patch`

### Branches auto deletion

Alright, last one for today.

This isn’t a tip so much as a really great feature, but since it’s fairly new I want to highlight it.

In your repository settings, you can enable __Automatically delete head branches__, which deletes the head branch of pull requests that are merged.

Unless you rely on long-lived branches (and you really shouldn't!), this is a quick improvement. You can always restore the deleted branch if you want, so there’s no risk.

Personally, I always delete my branches right away, so why not automate it.

### Conclusion

I hope there’s something new and helpful for you here.

What do you think? Did you already now every one of them?
Do you have any other tip you want to share?

Let me know in the comments.

### References and Links

YouTube video about these Secrets, Tips, and Tricks: [https://youtu.be/sGnqVAfnZ6U](https://youtu.be/sGnqVAfnZ6U)  
Github repo with the examples: [https://github.com/n3wt0n/GitHubSecrets](https://github.com/n3wt0n/GitHubSecrets)  
OctoTree: [http://octotree.io](http://octotree.io)  
SuperLinter: [https://github.com/github/super-linter/](https://github.com/github/super-linter/)
