Azure Pipelines is a great tool for doing Continuous Integration and Continuous Deployment and thanks to Multi Stage Pipelines we can finally have build, test, and release directly expressed in source code.

Recently they have also introduced the concept of "Environments", which belongs to the release process.

In the previous article of this series we've looked at the Environments in general.

Today, instead, we will go deeper into it and we will explore the integration between environments and __Kubernetes__ clusters.

In fact, the Kubernetes resource is the first that has been made available in Azure DevOps Environments and it's the one which provides the most features.

Let's see first what we can do with it and then how to set this up.

### Video

If you are a __visual learner__ or simply prefer to watch and listen instead of reading, here you have the video with the whole explanation, which to be fair is much more complete than this post.

{% youtube qBO5-xINmSs %}

If you rather prefer reading, well... let's just continue :)

### Deployments

When you click on the environment, you have 2 separate tabs: Resources and Deployments.

The Deployments tab has the same content we've seen in the previous post about Environments in general, so I won't spend much time about it.

Just real quick, in here you can see __what has been deployed and when__.

![What and where](https://dev-to-uploads.s3.amazonaws.com/i/yeu5euw2lme0718yp80w.png)

For example here I can see that this deployment came from the _deploy_ job of the _K8S_CICD_ Pipelines, ran on May 25.

Also, if I go inside, I can see what changes are included (and I have visibility down to the single file diffs):

![Changes](https://dev-to-uploads.s3.amazonaws.com/i/tpce3z7c8oiemzunec7g.png)

and that all of this was initially planned in the linked work items, here for example a bug and a task:

![Bug and Task](https://dev-to-uploads.s3.amazonaws.com/i/216ahknmmcblzhadw21e.png)

Thanks to the __complete integration__ of all the parts of Azure Devops, we have full traceability from Work management to deployments, and everything in between.

But as we have seen in the previous article, this comes with any kind of Environment, not only with the Kubernetes ones. So let's see what is unique about this one.

### Resources

Back in the Environment page, the Resources tab is where the magic happens.

In fact here I can basically explore the ___content___ of my Kubernetes cluster!

Again, we have two tabs here: Workloads and Services.

Workloads lists the __Deployments__ with their __Replica Sets__:

![Workloads](https://dev-to-uploads.s3.amazonaws.com/i/c8hmft6wa7tukho87zen.png)

You can drill into the Replica Set to see its details and the __Pods__ it's running on:

![Replica Sets](https://dev-to-uploads.s3.amazonaws.com/i/3rk3gyazl3gpwxpua9a6.png)

Note that here you can see not only the image associated with this deployment, but also its label and selectors (if any).

Finally, drilling into a pod, you can see its full details:

![Pod](https://dev-to-uploads.s3.amazonaws.com/i/8o0ktigh885j7k2oxoq1.png)

But that's not all, you can go even deeper. In fact, we can see the __Logs__ the Pod is producing:

![Logs](https://dev-to-uploads.s3.amazonaws.com/i/vryv37jl2b3sgm2oygjf.png)

and even the full __YAML__ of the Pod coming directly from K8S!

![YAML](https://dev-to-uploads.s3.amazonaws.com/i/igw8gbaaf7k8emzwgy0p.png)

If you are curious about the YAML content, this is what you get:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver-7f6cf4c486-4mtcj
  generateName: webserver-7f6cf4c486-
  namespace: default
  selfLink: /api/v1/namespaces/default/pods/webserver-7f6cf4c486-4mtcj
  uid: 536bafd1-9d45-44d3-b674-3e0d91345d1c
  resourceVersion: '899183'
  creationTimestamp: '2020-05-19T06:17:44Z'
  labels:
    app: nginx
    pod-template-hash: 7f6cf4c486
  annotations:
    azure-pipelines/jobName: '"Deploy"'
    azure-pipelines/org: 'https://dev.azure.com/dbtek/'
    azure-pipelines/pipeline: '"K8S_CICD"'
    azure-pipelines/pipelineId: '"65"'
    azure-pipelines/project: AKSEnvironmentDemo
    azure-pipelines/run: '20200525.1'
    azure-pipelines/runuri: 'https://dev.azure.com/dbtek/AKSEnvironmentDemo/_build/results?buildId=1058'
    cni.projectcalico.org/podIP: 10.244.1.9/32
  ownerReferences:
    - apiVersion: apps/v1
      kind: ReplicaSet
      name: webserver-7f6cf4c486
      uid: 1daf0d4e-5daf-4926-a4ee-42c735fb0071
      controller: true
      blockOwnerDeletion: true
spec:
  volumes:
    - name: default-token-mcfjv
      secret:
        secretName: default-token-mcfjv
        defaultMode: 420
  containers:
    - name: nginx
      image: 'nginx:1.17.10'
      ports:
        - containerPort: 80
          protocol: TCP
      resources: {}
      volumeMounts:
        - name: default-token-mcfjv
          readOnly: true
          mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      terminationMessagePath: /dev/termination-log
      terminationMessagePolicy: File
      imagePullPolicy: IfNotPresent
  restartPolicy: Always
  terminationGracePeriodSeconds: 30
  dnsPolicy: ClusterFirst
  serviceAccountName: default
  serviceAccount: default
  nodeName: aks-agentpool-17828392-vmss000002
  securityContext: {}
  schedulerName: default-scheduler
  tolerations:
    - key: node.kubernetes.io/not-ready
      operator: Exists
      effect: NoExecute
      tolerationSeconds: 300
    - key: node.kubernetes.io/unreachable
      operator: Exists
      effect: NoExecute
      tolerationSeconds: 300
  priority: 0
  enableServiceLinks: true
status:
  phase: Running
  conditions:
    - type: Initialized
      status: 'True'
      lastProbeTime: null
      lastTransitionTime: '2020-05-19T06:17:44Z'
    - type: Ready
      status: 'True'
      lastProbeTime: null
      lastTransitionTime: '2020-05-19T06:17:56Z'
    - type: ContainersReady
      status: 'True'
      lastProbeTime: null
      lastTransitionTime: '2020-05-19T06:17:56Z'
    - type: PodScheduled
      status: 'True'
      lastProbeTime: null
      lastTransitionTime: '2020-05-19T06:17:44Z'
  hostIP: 10.240.0.6
  podIP: 10.244.1.9
  podIPs:
    - ip: 10.244.1.9
  startTime: '2020-05-19T06:17:44Z'
  containerStatuses:
    - name: nginx
      state:
        running:
          startedAt: '2020-05-19T06:17:56Z'
      lastState: {}
      ready: true
      restartCount: 0
      image: 'nginx:1.17.10'
      imageID: >-
        docker-pullable://nginx@sha256:30dfa439718a17baafefadf16c5e7c9d0a1cde97b4fd84f63b69e13513be7097
      containerID: >-
        docker://6c8ebc8692033d4a0e92fe247fa4970ed77d664876cf42a7b8f5bad012eb2c68
      started: true
  qosClass: BestEffort
```

I love it, it's so useful and having everything in one tool allows you to focus much more!

Now that we have explored what we can do with it, let's see how to create a new Environment for Kubernetes in Azure Pipelines.

### Create a Kubernetes environment

First of all, needless to say, you need to have a Kubernetes cluster. I always use AKS in Azure because is a managed service and I don't have to pay for the master nodes ;)

And using AKS is also much easier linking the cluster with Azure DevOps.

First of all, let's go to the Environments section under Pipelines, and click "_New Environment_".

Let's give the environment a name and select "_Kubernetes_" as type of Resource.

Here you can set whether you want to use AKS or any other Kubernetes cluster. If you go for a Generic Kubernetes, then you'll need to input all the parameters manually and set up your cluster so it is reachable from Azure DevOps.

But if you select AKS, you'll get prompted with the selection directly.

Just pick the Azure Subscription and the cluster, and select the namespace you want to link. In fact, ___each resource maps to a specific Namespace in your cluster___.

If you already have an environment linked to your _default_ namespace, you can create a new one.

For this post I decided to call the new Environment _Secondary_ and to create a new namespaces called _app2ns_.

> This of course works if the account with which you're accessing Azure Devops has the proper permissions in your Azure subscription.

![New Environment](https://dev-to-uploads.s3.amazonaws.com/i/8js1g58vv4x2eorhvsk1.png)

And that's it! Of course, since we've just created it, it is completely empty.

Now all we have to do is using this environment in a ___Deployment job___ of a pipeline to have all the goodness we've seen before.

### Let's use it in a Pipeline

As mentioned, you need to have a pipeline which uses a [Deployment Job](https://docs.microsoft.com/en-us/azure/devops/pipelines/process/deployment-jobs?view=azure-devops), not a "normal one".

Then add the environment to it. The format to use is "_EnvironmentName dot Namespace_". In my case, this is _Secondary.app2namespace_

This is the snippet:

```yaml
- stage: CD
  displayName: CD Stage
  dependsOn: CI
  jobs:
  
  - deployment: deploy
    displayName: Deploy
    environment: Secondary.app2namespace
    strategy: 
      runOnce:
        deploy:
          steps: 

          - task: KubernetesManifest@0
            inputs:
              action: 'deploy'
              manifests: '$(Pipeline.Workspace)/YAML Files/k8s/App2.yaml'
```

The beauty of this, looking down at the task which actually perform the deployment, is that __we do not need to specify any service connection, credentials__, or anything else.  
The reason for this is that the ___Pipelines engine will take everything it needs from the Environment directly___.

If you then make a change at your code, this will start the whole process of CI CD, and bring together all the componentes: code, work items, build and deployment.

### Conclusion

Cool right? I mean, there are cooler things than this but they are all in the outside world... like, the real world... you know what I mean :D

Alright, this is how to use the Azure DevOps Environments for Kubernetes and how amazing and useful it is working this way.

### Examples

Take a look at my [video on YoutTube here](https://youtu.be/qBO5-xINmSs) to see how to create, manage, and use the Environments for Kubernetes in Azure DevOps.