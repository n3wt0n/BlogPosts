It is very common to __ask for approval__ during a release pipeline, especially when deploying to important environments like QA, Production, etc..

Azure Pipelines offers the Approval feature to do so, and it comes in 2 flavors: ___Pre-deployment___ and ___Post-deployment___ approvals.

But what is the difference between those 2 methods? And why it matters?

Let's discover it together.

### Intro

Today we talk about _Release flow control using approvals_, and more specifically about the different behavior that the Pre-deployment and the Post-deployment approvals have when using Azure Pipelines.

First of all, I should say that this applies to the __Classic Release experience only__, because with the Multistage YAML Pipelines you can define only some "generic" approvals at environment level and those are de-facto pre-deployment approvals. I made a [video about Azure Pipelines Environments](https://youtu.be/gN4j65w7wIM) where I also cover the approvals for YAML Pipelines, I encourage you to check it out if you are into YAML Pipelines.

Alright, so you are using the Classic Release Pipelines and wanna ask for Approval. Should you use the pre- or the post-deployment approval? What are the differences between those 2?

### The Video

To answer these questions and show you how to set and work with those kind of approvals, I created an example and I've gone through that in the video below.

Enjoy the watch!

{% youtube UvuiswLWSeo %}

### Conclusion

As you have seen, the behavior between the 2 is pretty different.

What do you think?  

Let me know in the comment section below if you prefer using the Pre or the Post deployment approvals and why.

### References and Links

- [Examples and explanation about Pre- and Post-deployment approvals](https://youtu.be/UvuiswLWSeo)
- [Approvals for YAML Pipelines, as part of Environments](https://youtu.be/gN4j65w7wIM)