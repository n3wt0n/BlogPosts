GitHub Container Registry improves how we handle containers within GitHub. Let's see what it is, how it works, and if it is better than Docker Hub.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube WjzA9dfk5w4 %}

[Link to the video: https://youtu.be/WjzA9dfk5w4](https://youtu.be/WjzA9dfk5w4)

If you rather prefer reading, well... let's just continue :)

### GitHub Container Registry?

The GitHub Container Registry (___GHCR___) is a redesigned, __enhanced version of GitHub Packages__. It not only __replaces the Packages Docker__ service, but also it represents a fundamental shift in how GitHub will provide packages to its customers, because Packages are now tied to organizations and accounts instead of repos. 

And in the case of the Container Registry, it also has its own url: _ghcr.io_.

GHCR also represents a step toward a __Cloud Native approach__ to CI/CD workflows. This service is in fact built from the latest docker distribution and offers OCI compatible storage.

### How To Push an Image?

Pushing a container image to the GitHub Container Registry is super easy and __straight forward__.

You just __authenticate__ using your GitHub Username and a PAT with the write packages scope (watch [this video](https://youtu.be/SzrETQdGzBM) to see how to create a PAT in GitHub), for example with Docker Login, and push the container as you would normally do.

You just have to __tag the image__ with the format `ghcr.io/OWNER/IMAGE_NAME:version`, where _OWNER_ is the name of your user or the organization.

And if you are doing it in __GitHub Actions__ it's even easier.

```yaml
- name: Log into GitHub Container Registry
  run: echo "${{ secrets.GITHUB_TOKEN }}" | docker login https://ghcr.io -u ${{ github.actor }} --password-stdin

- name: Push image to GitHub Container Registry
  run: |
    IMAGE_ID=ghcr.io/${{ github.repository_owner }}/MyBeautifulContainer:123        
    docker push $IMAGE_ID
```

You can in fact use the `GITHUB_TOKEN` environment variable instead of your PAT, `github.actor` to automatically retrieve the current user running the workflow, and `github.repository_owner` to automatically get the user or organization this container belongs to.

### Better than Docker Hub?

Is it better than Docker Hub? You tell me.

You can link GHCR to a repo, so you can __get the Readme directly__ as description for that image.

And you also have __granular control__ of the permissions. You can __restrict the usage__ of the container image only to some of your repos or your organization's repos, and you can also manage the __permissions for individual users or teams__.

Finally, you can __change the visibility__ of the container image between private and public.

So yes, ___for me___ it is better than Docker Hub. Adn the fact that it is already directly into GitHub makes it even easier to use.

### Final Considerations

Note that the Container registry is currently in __public beta and may be subject to changes__. It is free for public images, while for private images Container Registry is free during the beta, and as part of GitHub Packages will follow the same pricing model when generally available.

Also, remember that to use the Container registry, you __must enable the feature preview__. Just go to your profile settings and access the Feature Preview submenu.

### Conclusions

What do you think of the GitHub Container Registry? Are you using it?
Let me know in the comment section below.

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

{% youtube WjzA9dfk5w4 %}