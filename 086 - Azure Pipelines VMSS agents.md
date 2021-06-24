Today we are going to cover everything you need to know about the Scale Set Agents in Azure Pipelines, and how to use them to make your builds more elastic and flexible.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube 3oILIG4i71g %}

[Link to the video: https://youtu.be/3oILIG4i71g](https://youtu.be/3oILIG4i71g)

If you rather prefer reading, well... let's just continue :)

### Intro

So, Scale Set Agents in Azure Pipelines.

As the name says those are agents that you can install and run in Azure Virtual Machine Scale Sets, or VMSS.

As such, they can be scaled horizontally automatically, to make your build faster, more elastic, and eventually more flexible.

But Dave, I hear you asking, why would I bother to install my self-host agent in VMSS rather than using the Azure DevOps hosted agents instead? Can't I achieve the same flexibility just adding more hosted agents?

The answers to these questions are not so obvious. Let me explain.

### Why Scale Set Agents?

First of all, unlike Microsoft-hosted agents, you have flexibility over the size and the image of the machines on which agents run. When you use the hosted agents in fact, you depend on what Azure DevOps provides for you.

What if you need more resources, like more CPU power or RAM for the operations you have to perform? Or what if you need to install some software or library in order to build your application?

On the hosted agents you can't quite do it, can you?

And apart from that, there may be situations in which even if you are ok with what the hosted agents provide you can use them because of the environment you operate in.

Perhaps you depend on services or servers that are in a private network and therefore not reachable from internet. Or yet you may want to restrict network connectivity of agent machines and allow them to reach only approved sites.

In all of these scenarios you could install the normal self-hosted agents and scale them manually. But as we will see in a moment the Scale Set Agents are a much better solution.

Of course, this is if you are in Azure or you have an Azure Subscription. Let me know in the comment section below if you use other providers like GCP or AWS and would like to see how to scale your agents of those platforms as well.

Alright, let's see now how to set Scale Set Agents up.

### Create a Virtual Machine Scale Set with Proper Configuration

First thing to do is, of course, to create a VMSS cluster that Pipelines can use.

The virtual machine scale set must have the Azure's autoscaling disabled so that Azure Pipelines can determine how to perform scaling based on number of incoming pipeline jobs.

To do it, you can use this script from Azure CLI:

```bash
az vmss create \
--name YOUR_POOL_NAME \
--resource-group RES_GROUP \
--image UbuntuLTS \
--vm-sku Standard_D2_v3 \
--storage-sku StandardSSD_LRS \
--authentication-type SSH \
--instance-count 2 \
--disable-overprovision \
--upgrade-policy-mode manual \
--single-placement-group false \
--platform-fault-domain-count 1 \
--load-balancer ""
```

To make sure this works properly, remember that `--disable-overprovision` and `--upgrade-policy-mode manual` are required.

About `--load-balancer ""`, Azure Pipelines doesn't require a load balancer to route jobs to the agents in the scale set agent pool, but configuring a load balancer is one way to get an IP address for your scale set agents that you could use for firewall rules.

In the example I've created the scale set with a standard image, but most likely you would want to use an image with all the tools you need already installed. Good news, since this is a normal VMSS you can use any image you want.

And the same is true for updating an image, you can use the usual tools and commands for upgrading your images and when done all the new agents will be created with the new image. Let me know in the comment section below if you want me to create a video to explain how to work with Azure Virtual Machine Scale Set

### Create an Agent Pool for Scale Set in Azure DevOps

Alright, now that we have the Scale Set properly set, it's time to create an Agents Pool in Azure DevOps.

To do so, just go to the Project (or Organization) settings, then Agent Pools, and then click on "Add Pool"

![Agent Pool](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/kxuov76uxmttnsj2a9nw.png)

In there, select ___Azure virtual machine scale set__ for the pool type. Then select the Azure subscription that contains the scale set, choose _Authorize_, and choose the desired virtual machine scale set from that subscription. If you have an existing service connection you can choose that from the list instead of the subscription.

There are there a number of options you can specify, which will influence how your Scale Set Agents will be scaled in and out. Check [this section of the video](https://youtu.be/3oILIG4i71g?t=316) for a full explanation of those setting

> To configure a scale set agent pool, you must have either __Owner__ or __User Access Administrator__ permissions on the Azure selected subscription. If you have one of these permissions but get an error when you choose Authorize, it could be due to the fact that your user has only guest permission in the directory, or that it is not authorized to add applications in the directory. Either way, talk to your AAD admin.

Please note that the only service connection currently supported is using ARM with a service principal key. If you try to use an ARM service connection based either on a certificate credential or a Managed Identity, the process will fail with an error like this one:

`Invalid Service Endpoint with Id <guid> and Scope <guid>`

### Use an Agent from the Scale Set Agent Pool

Using a scale set agent pool is similar to any other agent pool. You can use it in classic build, release, or YAML pipelines. 

#### Classic Build Pipelines

Just change the pool in the Run options:

![Classic Build](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/nq31hieqhunx3r0mqph3.png)

#### Classic Release Pipelines

Change the pool in the Agent options:

![Classic Release](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8c1a8p3803jqgfzf08cb.png)

#### YAML Pipelines

Change the YAML section in the Pipeline, Stage, or Job:

![YAML](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/86mxloigkndvdv2y16f5.png)

User permissions, pipeline permissions, approvals, and all other checks work the same way as in any other agent pool.

### Scaling in and out

Ok, last thing I want to talk about is how Azure Pipelines manage the scale set and the agents in it. First, some theory.

Azure Pipelines samples the state of the agents in the pool and virtual machines in the scale set every 5 minutes. The decision to scale in or out is based on the number of idle agents at that time. Fairly enough, an agent is considered idle if it is online and is not running a job.

When needed, Azure Pipelines performs a scale out operation if either of the following conditions is satisfied:

- The number of idle agents is lower than the number of standby agents you specify
- There are pipeline jobs waiting in the queue and no agents is in the idle state

If one of these conditions is met, Azure Pipelines grows the number of VMs incrementally.

Talking about scaling in, instead, Azure Pipelines scales in the agents when the number of idle agents exceeds the standby count for more than 30 minutes.

![Delay](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/yld9gst5ydc1xg3s23t2.png)

> To see a __Complete Demo__ of scaling agents in and out, check [this section of the video](https://youtu.be/3oILIG4i71g?t=608)

### Limitations

At the time of writing, if you create a VMSS using Linux only Ubuntu is supported as OS for the Scale Set Agents. RedHad and Debian are not supported.

And if you are using Windows 10 client, it does not support running the pipeline agent as a local user and therefore the agent cannot interact with the UI. The agent will run as Local Service instead.

### Conclusions

Let me know in the comments below if you are using or going to use the Scale Set agents in Azure Pipelines and what kind of problem they solve for you.

You may also want to watch [this video here](https://youtu.be/rO-VKProMp8), in which I explain how to containerize your Azure Pipelines Agents for more flexibility.

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

{% youtube 3oILIG4i71g %}