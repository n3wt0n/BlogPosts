In the last years the popularity of containers has exploded. Unfortunately, so have their __security risks__.

Most containers available today are vulnerable to __supply chain attacks__, because they can be published with just a simple API key. And if that that key leaks, it’s easy for an attacker to publish a container that __looks legit but actually contains malware__.

One of the best ways to protect users from these kinds of attacks is by __signing the container image__ at creation time so that developers can verify that the one they have received is the real image with the code as it was intended to be. Today we are gonna see how we can sign our container images automatically, and host them in GitHub Container Registry.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube OqZlKbTRWOY %}

[Link to the video: https://youtu.be/OqZlKbTRWOY](https://youtu.be/OqZlKbTRWOY)

If you rather prefer reading, well... let's just continue :)

### About Sigstore and Cosign

So, signing a container image. There are few tools that allow to do so, but one of the most exciting one is __sigstore__.

Sigstore is an open source security project now sponsored by the OpenSSF, the Open Software Security Foundation, which allows developers to securely __build, distribute, and verify signed software artifacts__.

Among the other things, sigstore contains a tool called __cosign__ which allows you to __sign container images__.

[IMAGE 01]

Cosign supports __several types of signing keys__, such as text-based keys, cloud KMS-based keys or even keys generated on hardware tokens, and kubernetes-secrets, which can all be generated directly with the tool itself, and also supports adding __key-value annotations__ to the signature (and we will see this in action in a moment).

And after you sign the image, you need a Container Registry that supports signed images, because not all do, and even the ones that do support signed images may or may not support all the different signatures. Luckily, GitHub Container Registry supports signed images, and supports cosign as well.

But enough talking, let’s see how this works with GitHub Actions and GitHub Container registry.

### Cosign Installation

First thing you need to do is installing cosign to generate the keys.

You can just go to the official GitHub repo, _sigstore/cosign_, click on Releases, and download the version for your operative system.

[IMAGE 02]

Many OSes and platforms are supported, so be sure to pick the right one.

Once you have the version which is right for you, you can just run it. It is also advisable to rename the tool, in my case the executable was called `cosign-windows-amd64.exe` but I’ve renamed to just `cosign` for ease of use.

### Key Generation

Now all you have to do is generate a key. For this example, I will generate a __static text key__ using the `generate-key-pair` command, which requires a password to create the keys. 
The password can be given to the tool via environment variable

```shell
set COSIGN_PASSWORD=123
cosign generate-key-pair
```

or with an interactive prompt

```shell
cosign generate-key-pair
```

> Unfortunately, the latest version available at the moment of recording this video has a bug which makes it crash if you try to use the interactive prompt to provide the password on Windows, as you can see below.

[IMAGE 03]

If you don’t want to create an environment variable, you can use PowerShell and the syntax you see below, with your password piped to the command.

```powershell
"myPassw0rd" | .\cosign.exe generate-key-pari
```

In either case, this will create for you the __private and public key files__ that you can use to sign and validate your container images.

### Cosign Key Generation for GitHub

But we can do better. As I've mentioned before, I want to sign my container images via GitHub Actions, so now I would need to create some secrets in GitHub, and copy those keys to the secret values. But __the tool can do this__ for us directly!

For example, let’s say I want to sign images in the ___n3wt0n/SignedContainers___ repo. I can use the same command to create my keys in GitHub directly:

```bash
export GITHUB_TOKEN=ghp_xyz123

export CONSIGN_PASSWORD=pwd123

./cosign generate-key-pair github://n3wt0n/SignedContainers
```

First thing I need to do is creating an environment variable called GITHUB_TOKEN and its value should be a PAT with __write access__ to your repo. (Check [this video](https://youtu.be/SzrETQdGzBM) to see how to create a PAT in GitHub)

Then, I can use the command we have seen before to generate the key, but this time we pass the repo as input parameter. The syntax as you can see is _github://OWNER/REPONAME_

[IMAGE 04]

As you can see, the secrets containing the password we specified as well as the private and public keys are created in our repo, ready to use.

> Keep in mind that there have been instances in which the secrets were created in GitHub but their values were empty, and therefore the Actions workflow would fail. I’m not sure why that happens, but let me know if that happened to you as well. Anyway, the solution for this is simple, just try and generate the keys again or, if the problem persists, generate the keys locally and copy them manually into your secrets.

### Sign a Container Image with Cosign and GitHub Actions

Alright, now that we have our keys set up, let’s see how we can __sign our images from within a GitHub Actions workflow__.

Let's assume we have a fairly standard Actions workflow which just build a Docker image and pushes it to the GitHub Container Registry (_you can see the whole workflow's YAML below_)

The first thing we have to do is install cosign. For this we can use the pre-built action, just search for cosign and you can find the __cosign installer__. It has a couple of parameters, but they are optional so we don’t need them for now:

```yaml
    - name: cosign-installer
      uses: sigstore/cosign-installer@v2.0.0
```

When we have it, we can use the `cosign sign` command to sign our image:

```yaml
    - name: Sign the published Docker image
      env:
        COSIGN_PASSWORD: ${{ secrets.COSIGN_PASSWORD }}
      run: cosign sign --key cosign.key ${{ env.REGISTRY }}/${{ github.actor }}/${{ env.IMAGE_NAME }}:${{ github.run_id }}
```

It uses the __private key__ for signing, and it needs the cosign password to access it, plus of course we have to specify the __full image name__, with the registry name as well.

As you can see tho, the command __needs they key to be in a file__, while we currently have it on a GitHub secret.

The workaround for that is to __add another task__ before the sign command, which reads the key from the secret and writes it to disk:

```yaml
    - name: Write signing key to disk
      run: 'echo "$KEY" > cosign.key'
      shell: bash
      env:
        KEY: ${{ secrets.COSIGN_PRIVATE_KEY }}
```

___ I don’t much like it___, so I would prefer having a cosign implementation that can read it from the secret directly.

We can now commit and run our workflow. After a few seconds, the process is completed and we can see that our image has been successfully signed.

[IMAGE 05]

As I’ve mentioned the step to write the key on a file to give it to cosign is ___quite a workaround___, and it may pose some security risk especially if you do it on self-hosted runners. Hosted runners are disposed as soon as a Job finishes so it “should” be ok.

In more secure scenarios, like enterprise ones, I would recommend saving those keys in services like Azure KeyVault, Hashicorp Vault, AWS KMS, or similar to avoid this issue. 

[IMAGE 06]

Good thing is that cosign __supports reading the keys__ from those services directly.

> If you want to see the __full YAML of the workflow__, check it out [here on GitHub](https://github.com/n3wt0n/SignedContainers/blob/main/.github/workflows/docker-publish.yml) 

### Verify a Container Image Signature

Anyway, after an image has been signed, we can always verify it using the public key that has been generated together with the private key. You can also share your public key with developers and users of the container image so they can always verify its authenticity.

To __verify the authenticity of the image__, we can use the `cosign verify` command.

```bash
cosign verify --key cosign.pub ghcr.io/n3wt0n/signedcontainer:123
```

We just need to pass to it the public key file, and the name of the image we want to verify, and that’s it.

[IMAGE 07]

If, for comparison, we try to verify an image that hasn’t been signed with our key, we will get this error:

[IMAGE 08]

And this of course will happen also if the image has been changed or modified after we have signed it, so __our users can be safe and trust the image__ if the signature is verified.

### Add Annotation to a Signature

We have said before that cosign also supports__ adding key-value annotations__ to the signature. Let’s see how we can do that. Let’s say that for example I want to sign an image and also add some _author metadata_ to it.

Since I’m running this locally this time, I will need to first login into the container registry.

```bash
docker login -u myuser -p 123 ghcr.io
```

Then, I can use the usual command cosign sign, but this time I use a -a flag, which stands for annotation, to add some key value pairs to my image. 

```bash
cosign sign --key cosign.key -a "author=CoderDave" ghcr.io/n3wt0n/signedcontainer:123
```

In this case I’m adding _author=CoderDave_, but it can be anything and you can __add multiple values__ as well just adding more -a parameters.

After doing that, we can use the `cosign verify` command as we have seen before, and it will __show also the annotation__ I’ve added to my image.

[IMAGE 09]

The annotations feature can be __pretty useful__. For example, if you are running the signing process in GitHub Actions like we have seen before, you may want to add information about your repo, workflow run, etc to your signature to make it more complete.

[IMAGE 10]

### Cosign and GitHub Actions: Starter Workflow

Cosign and its process works fairly well, as we have seen, but __setting it all up is not very immediate__. Well, once again __GitHub made it simpler__ for use to get started.

They have in fact integrated cosign in their starter workflow. Just go to ___Actions___ > __New Workflow__, and pick the “__Publish Docker Container__” starter workflow.

```yaml
[...]

      # Install the cosign tool except on PR
      # https://github.com/sigstore/cosign-installer
      - name: Install cosign
        if: github.event_name != 'pull_request'
        uses: sigstore/cosign-installer@1e95c1de343b5b0c23352d6417ee3e48d5bcd422
        with:
          cosign-release: 'v1.4.0'


    [...]

      # Sign the resulting Docker image digest except on PRs.
      # This will only write to the public Rekor transparency log when the Docker
      # repository is public to avoid leaking data.  If you would like to publish
      # transparency data even for private images, pass --force to cosign below.
      # https://github.com/sigstore/cosign
      - name: Sign the published Docker image
        if: ${{ github.event_name != 'pull_request' }}
        env:
          COSIGN_EXPERIMENTAL: "true"
        # This step uses the identity token to provision an ephemeral certificate
        # against the sigstore community Fulcio instance.
        run: cosign sign ${{ env.REGISTRY }}/${{ env.IMAGE_NAME }}@${{ steps.build-and-push.outputs.digest }}

```

As you can see in the extract above, taken from the actual starter workflow, there is __no key specified__ in there.

This is because Actions supports other 2 tools which are part of sigstore: __Fulcio__, which is a root CA that issues signing certificates from OIDC tokens, as well as __Rekor__, a transparency log for certificates issued by Fulcio.

Thanks to these, you can __sign your container images with the GitHub-provided OIDC token__ in Actions, without provisioning or managing your own private key.

> It is important to note that with this keyless signing process, your username, organization name, repository name, and workflow name will be published to the Rekor public transparency log. This is the right choice for public repositories, but probably not for private repositories. And in fact GitHub has disabled this in private repositories by default to prevent potential leaks.

### Conclusions

What do you think about signing your container images, and especially doing so with cosign, GitHub Actions, and the GitHub Container Registry? Let me know in the comment section below.

Also, check out [this video here](https://youtu.be/9-dt5aMRzVU) in which I have 3 steps for you to make your Docker Image build faster.

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

{% youtube OqZlKbTRWOY %}