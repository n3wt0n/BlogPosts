We all know and I think can agree that __DevOps is good for Application Development__. 

But is DevOps a workable goal for IoT development?  ___Do we really need DevOps in IoT___?

Let's go over the challenges and some possible solutions for IoT DevOps, and see why I think DevOps is good for IoT as well.

### Intro

Today I want to talk about two topics that you don't normally see discussed together: __DevOps__ and __IoT__.

We all know that DevOps can bring many benefits to organizations adopting it (I have a [whole video about it](https://youtu.be/OxDtADXeyv8)) but when it comes to applying DevOps in the IoT space those benefits may not be immediately evident or, perhaps, __we need to look at them from another angle__. 

And I would argue that most of the time they are even __more important__ than doing it on normal applications... _more about this later_.

Let me also say that even tho there are many different "_kinds_" of Internet of Things, if you will, from tiny sensors which perform a single task autonomously, to complex appliances. For the sake of this post, I will try to keep this ___as general as possible___ talking about things that can apply to any kind of IoT development.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have the video, which to be fair is much ___more complete___ than this post.

{% youtube LPNMlP165v4 %}

([Link to the video: https://youtu.be/LPNMlP165v4](https://youtu.be/LPNMlP165v4))

If you rather prefer reading, well... let's just continue :)

### The Challenges

Alright, so... do we really need DevOps in IoT devices development?

#### Consumer IoT

From the consumer side of things, we are living in an age when customers test a device first, usually utilizing the product for their needs through its mobile app, and give feedback on the missing features directly to the developers. That is the only way for the developer teams to understand what the customers really want and how their device performs.

And think about wearables or personal assistants as well.

In those scenarios, how do you make sure you deliver the __right quality__ to your end users?  
And how do you __improve the experience__ if there is any gap or problem?  

These are just few of the challenges IoT developers face. And it gets even more complex when we talk about industrial IoT.

#### Industrial IoT

We now have millions if not billions of devices, from small autonomous sensors, to boards attached to other existing device to make them smarter, and all those devices __help controlling many aspects__ of the processes which bring products and services through a production line. 

Whether we are talking about controlling a factory floor, monitoring a cold cell for food storage, or tracking a shipping in real time... __That's all done through IoT Devices__.

Remember, those devices may be in __difficult locations__, and they are absolutely __essentials__ for the production lines and the businesses they have been created for.

__As an IoT developer, you need to make sure the device, its firmware, and its software are working properly and have the quality and reliability the client expects before they are installed.__

Perhaps even more importantly, you need to make sure your devices are __secure and secured__, so to avoid any possible __data breach and security issue__.

You also need to be able to __react as quickly as possible__ in case of incidents, because the economical impact of a bug, a malfunction, or a security breach is potentially huge.

This is probably where DevOps can have the most impact.

### The Solutions

Alright, enough talking about the challenges. Let's see how __DevOps can help when dealing with IoT__.

If you are familiar with DevOps, you probably already have some ideas on how to tackle the challenges I've just described. I would categorize them into 4 areas:

- Quality
- Security
- Responsiveness
- Monitoring

#### Quality

Talking about quality, we need to make sure the end product we have is __reliable__, works well, and virtually __bug free__. It could be difficult updating the firmware remotely, or at least quite inconvenient for the user. And of course as we all know this is an area where DevOps really helps.

![Feedback Loop](https://dev-to-uploads.s3.amazonaws.com/i/sz97saabkztshh21rk3n.png)

In fact, through the __Feedback Loop__ that is proper of DevOps, we can and should iterate during the development of both the IoT software, which can be the firmware and any control application, and the hardware to ensure their quality is up to our standards.

Yes, you've read it right. We __should apply DevOps to the Hardware development__ as well, or at least its core concepts.

If we talk about the __firmware__, it is basically just a piece of software and as such it can be, and should be I would say, version controlled. And then everything can be reviewed through pull requests and code review, tested automatically, and even deployed to either device emulators and even physical devices.

And if we talk about __hardware__, of course we cannot use the same tools but we can basically __proceed through revisions and apply the same concepts__ of review, testing, and improving.

#### Security

And this is tightly related to the second point, Security.

We all know that security is important in any application, but as I've mentioned before, __security is even more important in IoT__.

Once again this applies to both hardware and software.

Because of its __connected nature__, an attacker could leverage a security vulnerability remotely to __breach a network perimeter__.

If this happens in a consumer environment it is bad because it could lead to the __theft of personal information__, but if it happens in a corporate or industrial environment, where __business trade secrets are stolen__, it could potentially be even worse.

Luckily, with DevOps and __Shifting left on security__, which basically means embedding security early in the development process, and testing for vulnerabilities as soon as possible, you can prevent that.

Alright, at this point we should have a batch of devices with good quality hardware and software, and which have been properly tested for bug and security. We ship it to the factories or to retailers, and our clients start to use them.

How do we know if everything works correctly?  
This is where __monitoring__ comes into the picture.  

#### Monitoring

Thanks to the __telemetry__, we should be able to understand how our devices are functioning, if there is anything wrong and if we can __enhance anything__.

Monitoring is a __crucial part of DevOps__, and for IoT the only difference is that this feature may be either part of the software or the hardware. We should __always collect telemetry and monitoring data__, consider the results in our feedback loop, and __learn__ from them.

Of course there may be cases in which collecting real time telemetry is either not possible, like in some highly protected or regulated industries, or not practical. In those scenarios we should either have a ___local-only telemetry collection___, that then can be sanitized and analyzed, or try to collect the monitoring data at ___given intervals___.

This is important because __monitoring impacts our responsiveness__, which is the last of my points.

#### Responsiveness

In case of failure, malfunction, bug or breach we want to __be able to react as quickly as possible__ and to minimize the impact for the client or user.

Of course if it is a hardware failure, the only thing we can do is replacing the faulty device, but at least we can identify the problem as soon as possible thanks to the monitoring.

If instead the problem is on the software, we should have some __process__ in place to identify the problem, after the telemetry and the monitoring alerted us, fix it, get it tested and __get it deployed back to the device__.

This is similar to what we would do in a normal application, but this is where it gets ___complex___. We would need to deploy the changes to hundreds, thousands, or potentially even millions of affected devices.

Once again, DevOps can help us. We should __build an effective CI\CD pipeline__ that builds and tests the firmware or the control software, and then creates a packaged version for deployment.

![Remote Update](https://dev-to-uploads.s3.amazonaws.com/i/argcvusic4340eaw5ymt.png)

At this point, we should probably rely on some __IoT management platform__, like for example the Azure IoT Suite, that takes care of the __update of device firmware over the air__, remotely.

Our CI CD Pipelines should just __upload__ the new software package to the IoT management platform and __kick off the remote deployment__.

And when it is done, and the new telemetry starts to come in... our job is __complete__, hopefully successfully!

### Conclusions

Alright, I think that's it for today. Let me know in the comment section below what you think about DevOps for IoT, if you are already doing it or if you have other challenges that I haven't mentioned here.

Also, let me know if you would like me to do some other videos about DevOps for IoT but more in practice, to see what this would mean when working on real devices.

Once again, check the [whole video here](https://youtu.be/LPNMlP165v4), which is more interesting :)