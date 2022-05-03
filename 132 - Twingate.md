When moving to the cloud, and in fast-paced DevOps environments, __securely connecting__ to your private networks can be very challenging. 

And if you and your team want to be able to do it from any device (_PCs, phones, tablets, etc_) in an easy way, while keep a __Zero Trust approach__, and without a very complex VPN solution.... Well, I’d normally say "_good luck_" 🤣

Today however I have for you __a solution to that__. A service which lets you create a __secure network__ between your servers, computers, and cloud instances, even when separated by firewalls or subnets, and that just works. Oh, and you can start with it for __free__! Let’s talk about __Twingate__.

> Try out Twingate today and start securely accessing your private resources: https://geni.us/twingate

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube JsQ6xNSOVqk %}

[Link to the video: https://youtu.be/JsQ6xNSOVqk](https://youtu.be/JsQ6xNSOVqk)

If you rather prefer reading, well... let's just continue :)

### Why Twingate And Not a VPN?

Let’s firstly see why we would want to use a Zero-Trust Networking solution like Twingate over a normal VPN. And for me, it is down to 4 main pillars: 
- Security
- Performance
- Maintainability
- User Experience.

#### Security

Let’s start with Security. With normal VPNs, user access is usually granted to the __entire network__ that the VPN secures, and access to specific applications need to be managed with __complex routing changes__ or by the applications themselves.

![Security Principles](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/7kqdr2wbejewg81s7gh0.png)

Twingate, instead, allows you to __control access granularly__ at the application level, not the network level. The access is granted on a per application basis.

Moreover, access to a specific resource can be based on a wide variety of factors, including an identity authenticated by a third party __SSO__ or identity provider using __MFA__, the user’s physical __location__, time of day, __device__, and other contextual data.

Finally, Twingate provides __comprehensive logging__ in a single centralized view, making monitoring way easier.

#### Performance

Let’s talk now about Performance. If you’ve ever used a VPN, you know that in most cases that comes with a degradation of performance. Not with Twingate, this service in fact uses something called "__Smart Routing__" that promises to have no impact on user performance or latency. And it works on 3 levels.

![Smart Routing](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8c0cbmoqnhshbrtwz47z.png)

First one is __Resource-level Split Tunneling__. With a normal VPN solution, unless you have complex rules in place, all traffic is sent to the VPN gateway, and flows through it. 

![Split Tunneling](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/npqgg3osd1st3foc7dod.png)

With Twingate instead, only the traffic that needs to go to the private endpoint is sent through the service, meaning that all your "_non-private_ traffic" is not affected.

We then have the NAT Traversal. Traditional VPN clients are relatively __limited__. They relay information to a VPN server, and it is the job of that server and other network infrastructure to process authorization requests and manage traffic routing. This is known to cause increased latency.

![NAT Traversal](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/zceaqv6y5upot7apa71f.png)

Twingate pushes these processing activities to the __network edge__ by making its clients __intelligent__, and creating peer-to-peer connections between clients and resources to minimize latency.

![QUIC Multiplexing](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/sfuukfrueoi1njaod4de.png)

The final point about performance has to do with how the traffic is managed. Instead of using single-plexing, which basically queues the traffic in a single stream and therefore causes performance degradation, Twingate delivers concurrent data streams by __multiplexing them over a single connection__.

In general, Twingate is able to __improve connectivity performances__ to private resources, and reduce corporate network congestion and bandwidth usage.

#### Deployment and Maintainability

I mentioned before that another point I consider an advantage of Twingate over traditional VPN solutions is about Deployment and Maintainability.

We will see in a moment how __quick and easy__ it is to deploy Twingate (and this is something you don’t usually get with a traditional VPN), but it doesn’t stop there.

![Twingate Admin Console](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/4yhwqh6xr24fgjzfl52x.jpg)

Twingate provides a __centralized admin console__ which controls access to private resources throughout the organization, regardless of whether they are inside or outside the traditional network.

Additionally, not much maintenance is needed on the connectors you deploy, and the service uses an __API-first approach__ so you can automate the configuration, make it part of your CI/CD and even use Terraform to manage them.

![Twingate CICD](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/uuh1ix1vxpdu1w9m4cik.png)

#### User Experience

I don’t think I need to add much else to what we have seen so far to see why the __user experience for both admins and end users is better__ than a traditional VPN.

### Twingate Architecture

Before we see this in action, I want to spend a moment talking about the overall service architecture and its components, so later it will be easier to understand the steps we are taking.

Twingate relies on four components: 

- Controller
- Clients
- Connectors
- Relays.

![Twingate Architecture](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/vl5855ujq95yxxc6invf.png)

The ___Controller___ is the central coordination component for Twingate. It's a multi-tenant component that stores configuration changes via the Admin console, registers Connectors, and issues signed authorizations to Clients making connection requests amongst other responsibilities.

The ___Client___ is installed onto user devices and acts as a combined authentication and authorization proxy for user requests for private Resources. The Client is where most of the decision-making takes place in a Twingate network deployment, with routing and authorization taking place at the edge within the Client.

The __Connector__ is deployed inside your private network or behind your firewall, and takes care of validating the client connections and ACLs, and performing local DNS resolutions, among other things.

Finally, the __Relay__ is the simplest component in the Twingate architecture. No data or network-identifiable information is stored in the Relay and no data-carrying connections are terminated at the Relay. It basically serves as a registration point for Connectors, and as a connection point for clients.

### Step-by-Step Videos

Alright, enough talking. Let’s see this in action. We will start from scratch, installing the connectors, the client, and see how to use them all together.

1️⃣🎦 [Demo setup overview](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=390s)
2️⃣🎦 [Create a Twingate Network](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=460s)
3️⃣🎦 [Installing the Twingate Connectors](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=508s)
4️⃣🎦 [Add Resources to Twingate](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=725s)
5️⃣🎦 [Twingate Clients Setup](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=809s)
6️⃣🎦 [Connect to Private Resources](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=894s)
7️⃣🎦 [Twingate Security and User Management](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=1022s)
8️⃣🎦 [Integration with Identity Provider (AAD, Okta, etc)](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=1135s)
9️⃣🎦 [Advanced Management: Devices and Policies](https://www.youtube.com/watch?v=JsQ6xNSOVqk&t=1190s)

### Pricing

As I’ve mentioned before, you can start with Twingate __completely for free__! And you can keep it free __forever__ if you don’t need more than 5 users or more than 2 remote networks.

![Twingate Pricing](https://dev-to-uploads.s3.amazonaws.com/uploads/articles/ibvic7rv3m30dcuia7gp.png)

However, with the free tier you will miss out on the most innovative and useful features. If you want to have resource-level access policies or integrate with your identity provider, for example, or if you need to have it rolled out to more users, more devices, or more remote networks... then you’ll have to go to one of their [paid plans](https://geni.us/twingate).

And as you have seen that can be even for unlimited users, devices, and remote networks... But remember to __factor in the cost of your deployed connectors__ as well, as we have seen before.

> Try out Twingate today and start securely accessing your private resources: https://geni.us/twingate

### Conclusions

There is so much more about the service we could explore, like for example use Twingate to __remotely connect to a NAS__, using it as an access control mechanisms for Staging Environments, even use it for __securing SaaS applications__... let me know in the comments below if you wanna see more about it and I’ll try and make another article/video about Twingate.

So, what do I think about this service? I do like it and I think it is on __a whole new level__ if compared to standard VPN solutions. 

One thing I’d love to see implemented is some sort of __automated provisioning of the connectors__, with Twingate using the cloud provider APIs to deploy it for you. This may not apply to more enterprise level users, where we normally prefer having more control over the deployments, but I think smaller users could benefit from something like that.

Let me know in the comments below what your thoughts are about Twingate, and if you will consider using it instead of a normal VPN... or if you are already using it or some other Zero Trust Networking solution.

Finally, check out [this video](https://youtu.be/KaoPQLyWq_g) in which I talk about DevSecOps and how to do it properly.

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

{% youtube JsQ6xNSOVqk %}