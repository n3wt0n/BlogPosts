> This article is part of [#ServerlessSeptember](https://aka.ms/ServerlessSeptember2020). You'll find other helpful articles, detailed tutorials, and videos in this all-things-Serverless content collection. New articles from community members and cloud advocates are published every week from Monday to Thursday through September. 
>  
> Find out more about how Microsoft Azure enables your Serverless functions at [https://docs.microsoft.com/azure/azure-functions/](https://docs.microsoft.com/azure/azure-functions/?WT.mc_id=servsept20-devto-cxaall). 

### Intro

In this post I want to show you how serverless could be beneficial even in the enterprise context.

To do so, I will tell you a __real story__ of a real enterprise I've helped creating an ___EIP___, enterprise integration platform, which is ___completely Serverless___.

### Some Context

The need of this enterprise was very similar to many other realities around the globe.

They had __dozens of different systems__ that needed to communicate with one another, and they wanted to do so in a reliable, simple but yet inexpensive manner.

Of course, as you would expect, the landscape of those systems is very __heterogeneous__: 

- some platform have APIs, some haven't
- on some system you need to connect directly on the database
- some of the systems are hosted on-prem, while some others are hosted in Azure

### Requisites

Since they had to create it from scratch, the company also wanted their yet-to-be-born EIP to fulfill a series of requisites that sound pretty reasonable. The EIP had to:

- Connect all the systems using some sort of __standardized approach__
- Allow __both synchronous and asynchronous__ communication
- __Handle unpredictable load__ peaks, as well as scale down on the _no load moment_
- Be __reliable__
- Ensure __consistency__
- Had little or __reduced maintenance cost__ and overhead
- Everything should be managed via __CI/CD__

Each of those points is fair, but the challenge was to __achieve them all within the same platform__.

Luckily for them (and for us), __Azure has all we need for achieving those goals__.

### The Solution (v1)

We decided to create the entire EIP using these 4 services:

- Azure Functions
- Logic Apps
- Service Bus
- API Management

All of them can __automatically scale__ based on load or custom metrics, to help handling load and reduce cost.

After a few architectural sessions, and some implementation, this is what we came out with:

[IMAGE 01]

As you can see, there are __2 main flows__: the ___API___ flow and the ___Message Queue___ one.

Let's start with the __APIs__. The main component here is __API Management__; all the APIs (for all the services that have APIs...) are masked and exposed by this service, for __both on-Azure and on-prem__ (thanks to the VNet integration).

This allows for standardizing the APIs methods, verbs and request/response objects since APIM can easily _translate_ them for us.

If no APIs are available for a certain operation and to ensure the async support, we also implemented the __Message Queue flow__.

One (_or more_) __Azure Functions__ have been developed for each system, and they respond to that very system events. They take the payload of that an event and __push a message into Service Bus__.

But that's not enough, because remember that ___we want to achieve standardization___. For this reason, each Azure Functions massage the data of the payload and __create a message in a standard format__ and only then they write to Service Bus.

And since the message at this point has a standard format and properties, it can easily be picked up from a __Logic App__ that orchestrate the response process. Once again, we have multiple Logic Apps for multiple systems, and depending on the destination system and the message content they may invoke some APIs, write to the DB, and what not. Of course, each set of Logic Apps has a subscription only to the appropriate messages.

This was already a __good solution__, but not a perfect one. In fact:

- __async communication was not always provided__ (especially when invoking APIs directly)
- the system __wasn't able to handle the online/offline__ status of the services (for example during maintenance or update windows)
- there was __no way for the users to interact manually__ with the EIP

### The Better Solution (v2)

For the above reasons, we decided to expand the v1 into the v2 of the EIP:

[IMAGE 2]

The ___foundations of the v2 are the same___, but we introduced some more "components".

First of all, we decided to create some __Online/Offline handlers__, using once again Azure Functions. Those are very useful, especially when the systems are interacting with the APIs, because they allow for handling any problems during communication. If a system is not reachable because it's down for maintenance, or there is a network problem, or yet a transient error occurs, these handlers __compose a new message__ and save it into Service Bus. Each message has a property which indicates if it's an "_original_" message or, like in this case, a "_retry_". If it is in fact a retry, there is also a "_retry times_" property which is incremented every time. To avoid flooding the system with retries, a configurable retry threshold is in place and if the number of retries is reached for a specific message, the message is discarded (aka put in a specific _errors queue_) and a high priority alert is generated.

Also, we've created a Web App (which once again publish messages to the MQ via an Azure Function) to __allow users to send messages into the EIP__, targeting predefined operations in specific systems. This, as you can see in the diagram, __follows the same patterns and principles__ of the other flows and systems.

### Does this fulfill all the requirements?

In one word: ___yes___!

- Everything used is __Serverless__, so has very little maintenance, management cost/effort, and scales up and down pretty easily
- The Combination of Azure Functions and Logic Apps, together with Service Bus, allows to create a __fully sync/async platform__
- The messages and format used have been __standardized__, and so are the _APIs_ thanks to API Management
- The online/offline handlers ensure __reliability__ at application level, while Azure (and the services SLAs) does so at platform level
- All the code (including Functions and Logic Apps) is stored into, and validated and deployed with Azure DevOps, achieving __full CI/CD__

We also went beyond what the initial requirements were:

- Quotas were implemented into API Management to __prevent accidental DoS__
- API Management also help controlling the execution and the security of the APIs, which some systems didn't have in place
- The __entire EIP is under monitoring__, thanks to Azure Monitor and Application Insights

### Some Gotchas...

Although this is an almost perfect EIP (at least it is for us), there are some small notes and gotchas worth sharing.

- Azure Functions in Consumption mode doesn't support VNet integration
  - You need to use other hosting plans (i.e. Premium, Dedicated, etc) if you want to connect to on-prem
- CI/CD for LogicApps is not exactly fun
  - LogicApp workflow definition language must be manually parametrized
  - Then ARM Template can be grabbed, but
  - ARM Template must be manually modified to set parameters value
- There is no _Azure Functions Specific_ build and deploy task in Azure DevOps
  - You need to use the Asp.Net Core task
  - Depending on your configuration, you may need to use [customized deployments settings](https://github.com/projectkudu/kudu/wiki/Customizing-deployments)

### Let's hang out

Follow me:

- YouTube: [CoderDave](https://youtube.com/CoderDave)
- GitHub: [@n3wt0n](https://github.com/n3wt0n)
- Twitter: [@davidebenvegnu](https://twitter.com/davidebenvegnu)
- LinkedIn: [davidebenvegnu](https://www.linkedin.com/in/davidebenvegnu)
- Website: [http://www.davidebenvegnu.com](http://www.davidebenvegnu.com)
