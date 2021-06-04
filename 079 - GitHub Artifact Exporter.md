Today I'm going to show you how you can easily export Issue, Releases, Milestone, Commit History and more from GitHub, using the GitHub Artifact Exporter.

### Intro

GitHub Artifact Exporter provides a CLI and a simple GUI for exporting GitHub Issues and related comments based on a date range, and it supports GitHub’s full search syntax, allowing you to filter results based on your search parameters.

![GUI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ngg6abxr9gnkqt6r5qff.png)

The CLI also supports exporting:

- Commits
- Milestones,
- Projects
- Pull requests, including comments
- Releases

![CLI](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/bz6a62uf32fujqrsnml1.png)

And you can export all of that in different formats: JSON, JSON lines, CSV, and Jira-formatted CSV. And of course if you export in CSV, it means that you can open it in Excel. Cool right?

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube xYIJLQB1YF4 %}

[Link to the video: https://youtu.be/xYIJLQB1YF4](https://youtu.be/xYIJLQB1YF4)

If you rather prefer reading, well... let's just continue :)

### Prerequisites

There are few prerequisites to run the exporter.

#### Lerna

First of all it is a lerna project, so you need to have lerna installed. If you don't know what lerna is don't worry because I didn't even know it existed until I started looking into the exporter project. Apparently it's a tool for managing JavaScript projects split within multiple repos and packages.

All you need to do is install lerna via npm and then use it to build and run the project as directed from the instructions in the repository.

```bash
npm install -g lerna
```

Yes, you've heard it right... The GitHub Artifact Exporter comes with the sources and you have to build it yourself. We will do it in a moment, and you can find the link to the repo in the video description.

#### GitHub PAT

Second prerequisite is to generate a Personal Access Token with the "read packages" scope so you can pull from GitHub Package Registry.

### Installation

Alright, let's quickly see how to install the tool... or better, build it since it comes with the source code :)

First think we need is the code. Head to the [official repo](https://github.com/github/github-artifact-exporter) and, download the package in the release.

#### GUI

To install the GUI, we need to execute the lerna commands to build the whole thing:

```bash
lerna exec npm install
lerna link
lerna bootstrap
```

#### CLI

The step above builds also the CLI part, and in fact you can go into the `/packages/cli/bin` folder and there you will find the _cmd_ executable for it.

But you can also install the CLI standalone using:

```bash
npm install @github/github-artifact-exporter-cli
```

### Usage

Alright, now that we have it installed let's see how to use it.

For this, check the [video here](https://youtu.be/xYIJLQB1YF4) for the explanation and the demo. (The demo starts at minute [3:40](https://youtu.be/xYIJLQB1YF4?t=220)

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

{% youtube xYIJLQB1YF4 %}