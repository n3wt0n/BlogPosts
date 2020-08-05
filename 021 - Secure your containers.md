Securing any environment requires multiple lines of defense, and it's usually pretty complex. And that's no different when it comes to Containers.

Luckily for us, tools like Azure Container Registry and Security Center provide the right features to secure our container end-to-end workflow, quickly and easily.

### Intro

When it comes to containers and container security, there are many things you need to consider.

- How to create the images? 
- Where to store them?
- How to deploy?
- What to take care of after the deployment?

Those are just some of the most commonly asked questions...

I've already talked in some previous posts about _how I like to build my container images_ ([VIDEO](https://youtu.be/VBr-fj44W0E)) and _[how I do deploy them in enterprise scenarios](https://dev.to/n3wt0n/container-image-promotion-across-environments-build-artifact-5887) ([VIDEO](https://youtu.be/tG0O8vsO1LE))_, so I won't cover that here. I highly encourage you to check them out.

What I will cover here, instead, is how to use ___Azure Container Registry___, ___Azure Security Centre___ and ___Azure Policies___ to __secure your containers__ when they leave your controlled environment, if you will.

### Video

If you are a __visual learner__, simply prefer to watch and listen instead of reading, or you want to see this in action, here you have the video with the whole explanation, which to be fair is much more complete than this post.

{% youtube JpEchkDd8O4 %}

If you rather prefer reading, well... let's just continue :)

### About ACR

Azure Container Registry in fact recently announced the general availability of features like ___Azure Private Link___, ___customer-managed keys___, ___dedicated data-endpoints___, and ___Azure Policy definitions___, as well as the ___integration with Azure Security Center___ for the security scan of container images. These features provide tools to secure Azure Container Registry as part of the container end-to-end workflow, and I will focus on those, one by one.

### ACR Customer-managed Keys

First off, let's talk about Customer-Managed keys.

By default, when you store images and other artifacts in an Azure Container Registry, content is automatically encrypted at rest with _Microsoft-managed keys_.

But if you or your organization have stricter compliance needs, or want to be in full control, you can choose customer-managed keys that are __created and maintained in your Azure Key Vault__ instance.

There are few __prerequisites__, first you'd need to create a ___Managed Identity___ for the ACR.

```bash
az identity create \
  --resource-group <resource-group-name> \
  --name <managed-identity-name>
```

Then, you'd need to create a ___KeyVault___, if you don't have one already.

And of course you'd need to enable the Managed identity to access that KeyVault.

Just go to _Access Policies_ > _Add_ > and select your Managed Identity under _Select Principal_

![MI permisisons](https://dev-to-uploads.s3.amazonaws.com/i/dn2unc1mr97km9uvw4gd.png)

You just need the ___Get___, ___Unwrap Key___ and __Wrap Key__ permisisons under _Key permissions_

Lastly on KeyVault, you need to __create a Key__ for securing your ACR.

Just go to the Key section of KeyVault, Select _+ Generate/Import_ and enter a unique name for the key.

And finally now you can __create your container registry__. ([Video with full explanation and examples](https://youtu.be/JpEchkDd8O4))

Select the Premium SKU and, in the Encryption section:

![ACR Creation](https://dev-to-uploads.s3.amazonaws.com/i/46vnm2j2img0etdtchv4.png)

After enabling a customer-managed key in a registry, you can perform the same registry operations that you perform in a registry that's not encrypted with a customer-managed key.

And of course you can __change that key__ down the road.

Just go to _Encryption_ under _Settings_ > _Change Key_ > Select Key > Choose the same one > _Create a key_ > Generate, Create > Save

Of course you can also use another exhisting key, if you want.

There are few __things to note__ here:

1. This feature is available only in the Premium container registry service tier.
2. You can currently enable a customer-managed key only when you create a registry.
3. After enabling a customer-managed key on a registry, you can't disable it.

### Private Links

Let's move now to Private Links.

Container Registry previously had the ability to restrict access using firewall rules. Now, with the introduction of Private Link, the registry endpoints are assigned __private IP addresses__, routing traffic within your virtual network and the service through a Microsoft backbone network.

![Private Links](https://dev-to-uploads.s3.amazonaws.com/i/lg8wzzufszr8ppytesy3.png)

This of course means not only tighter security when accessing the Azure Container Registry directly, for example for pushing images, but also when communicating with other Azure Services which are either in a VNET or that support Private Link, like AKS.

You can set up a private link when you create a registry, or you can add a private link to an existing registry.

To add it to an existing one, go to _Networking_ > _Private Endpoints_ > _+ Private Endpoint_ and follow the wizard to select the Container Registry and the VNet you want to connect to. ([Video with full explanation and examples](https://youtu.be/JpEchkDd8O4))

Now your registry is __accessible only from within that VNET__ and its peered VNETs, if any.

This also means that ___you would need to push your images to the Container Registry from a VM that is in the same Virtual Network___ where the Private Link is configured. But this is not a big deal using Azure DevOps, you can just register a small VM in that VNET as Pipeline Self-hosted agent and you're good to go, as long as you have either the docker CLI or the Azure CLI on that VM of course.

### Dedicated Data Endpoints

As we have seen, Private Link is the most secure way to control network access between clients and the registry as network traffic is limited to the Azure Virtual Network.

If Private Link can't be used, for example because you want to use your container registry with Azure Container Instances which at the time of recording doesn't support Private Link yet, then __dedicated data-endpoints can be enabled to minimize data exfiltration concerns__.

Enabling dedicated data endpoints means you can ___configure firewall rules with fully qualified domain names___ rather than a rule with wildcard for all storage accounts.

You can enable dedicated data-endpoints using the Azure portal or the Microsoft Azure CLI.

Once again, on the portal go to _Networking_ > _Public access_ > _Enable dedicated data endpoint_

![Dedicated data endpoints](https://dev-to-uploads.s3.amazonaws.com/i/76f5rub60fseoeudh6xq.png)

The data endpoint (or endpoints) will appear in the portal.

As you can see, the data endpoints follow a regional pattern:

```PowerShell
<registry-name>.<region>.data.azurecr.io.
```

And the cool part is that if you have a geo-replicated registry, enabling data endpoints creates ___endpoints in all replica regions___. 

### ACR Built-in Policies

Next one is a feature that has been GAed pretty recently and I have to say I quite like it.

I'm talking about the built-in Azure Policy definitions in Azure Container Registry.

In my opinion those policies are __quite important__, because having security capabilities will secure your workflows only if they’re implemented. The Azure built-in policies assure your Azure resources are following the best security practices.

And best of all, there are __no charges__ for using Azure Policy!

All you have to do is going to _Azure Policy_ > _Assignments_ > _Assign Policy_ and then search for _container registries_ in the "Policy Definition" box

![Policies](https://dev-to-uploads.s3.amazonaws.com/i/etq8pk5dip63769onx42.png)

Just click on the one you want to use, and select the __scope__ (whole Subscription or a single Resource Group). And you're done.  
It takes about 30 minutes for the new policies to be applied.

Then you can go to "_Compliance_" to see whether your container registries implement your policies and the best practices or not.

![Compliance](https://dev-to-uploads.s3.amazonaws.com/i/sx5601iw5tud4whtrand.png)

Using Azure Policy, you can ensure that your registries stay compliant with your organization's needs. And this is pretty important.

### Azure Security Center Container Image Scan

Last but not least, let's talk about Security for Container Images.

If you're on Azure Security Center's ___standard tier___, you can add the __Container Registries bundle__. This optional feature brings deeper visibility into the vulnerabilities of the images in your registries and ensures that Security Center is ready to scan images that get pushed to the registry.

Whenever an image is pushed to your registry, Security Center is notified via WebHooks and automatically scans that image.

![Security Center flow](https://dev-to-uploads.s3.amazonaws.com/i/qe51ta9mpso9872c20pw.png)

The image is pulled from the registry and it's run in an __isolated sandbox__ with the Qualys scanner that extracts a list of known vulnerabilities.

Security Center then filters and classifies the findings from the scanner. 

When an image is healthy, Security Center marks it as such, otherwise it generates security recommendations for the issues to be resolved. 

By only notifying when there are problems, Security Center reduces the potential for unwanted informational alerts.

When the scan completes (typically after approximately 2 minutes, but can be up to 15 minutes), findings are available as __Security Center recommendations__ like this one:

![Scan results](https://dev-to-uploads.s3.amazonaws.com/i/hc4rrs8yew39627ee3v0.png)

### Conclusion

Alright, that's it for today. That was a lot of stuff, hope you stayed with me the whole time.

Let me know in the comment section below if you're already using any of these features or, if not, how you take care of your container workflows.

### References and Links

- [Video with full explanation and examples](https://youtu.be/JpEchkDd8O4)
- [How I build container images](https://youtu.be/VBr-fj44W0E)
- [How I deploy my containers](https://youtu.be/tG0O8vsO1LE)