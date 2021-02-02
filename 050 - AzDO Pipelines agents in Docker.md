If you want to use an Azure Pipelines Self Hosted agents, you have some different options. But only few of them allow you to be __truly flexible and scalable__. 

In this post we will see how to run the Azure Pipelines Agents in __Docker__, so you can take advantage of orchestrators like Kubernetes, Azure Container Instances, and many more.

Let's get into it.

### Intro

Today I wanna show you how you can __run your Azure Pipelines agents in Docker__ so you can then take advantage of orchestrators like Kubernetes, Azure Container Instances, and others to make your CI CD agents truly scalable and flexible.

I will walk you through a __complete container example__.

### Video

As usual, if you are a __visual learner__, or simply prefer to watch and listen instead of reading, here you have __the video with the whole explanation and demo__, which to be fair is much ___more complete___ than this post.

{% youtube rO-VKProMp8 %}

([Link to the video: https://youtu.be/rO-VKProMp8](https://youtu.be/rO-VKProMp8))

If you rather prefer reading, well... let's just continue :)

### Supported Platforms

First things first: Let's talk about the __supported platforms__.

![Platforms](https://dev-to-uploads.s3.amazonaws.com/i/jtw2me1z7ks24fo0w8iu.png)

The good news is that __both Windows and Linux are supported__ as container hosts. If your CICD process requires tools that are platform specific there is no problem.

### Prerequisites

Second thing, prerequisites. On Windows you would need to remember to __enable Hyper-V__, which is disabled by default, while on Linux it just works.

Of course you would need to __have Docker installed__ on both platforms, and that could be either _Docker Community Edition_ or _Docker Enterprise Edition_.

### Container Image Creation

Alright, let see now how to __create a basic image__. The process is slightly different between Windows and Linux, so I will cover both.

I will start with Windows, but you can skip to the Linux section if you want.

#### Windows

> [Click here to check the video and see this explained in much __greater details__.](https://www.youtube.com/watch?v=rO-VKProMp8&t=89s) 

To create a container image for Windows you need a __Docker file__, of course.

```docker
FROM mcr.microsoft.com/windows/servercore:ltsc2019

WORKDIR /azp

COPY start.ps1 .

CMD powershell .\start.ps1
```

We derive from the Server Core image, which __contains already all the dependencies__ we need.

Next we need to download the __PowerShell script__ Microsoft provides ([here](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#create-and-build-the-dockerfile)):

```powershell
if (-not (Test-Path Env:AZP_URL)) {
  Write-Error "error: missing AZP_URL environment variable"
  exit 1
}

if (-not (Test-Path Env:AZP_TOKEN_FILE)) {
  if (-not (Test-Path Env:AZP_TOKEN)) {
    Write-Error "error: missing AZP_TOKEN environment variable"
    exit 1
  }

  $Env:AZP_TOKEN_FILE = "\azp\.token"
  $Env:AZP_TOKEN | Out-File -FilePath $Env:AZP_TOKEN_FILE
}

Remove-Item Env:AZP_TOKEN

if ($Env:AZP_WORK -and -not (Test-Path Env:AZP_WORK)) {
  New-Item $Env:AZP_WORK -ItemType directory | Out-Null
}

New-Item "\azp\agent" -ItemType directory | Out-Null

# Let the agent ignore the token env variables
$Env:VSO_AGENT_IGNORE = "AZP_TOKEN,AZP_TOKEN_FILE"

Set-Location agent

Write-Host "1. Determining matching Azure Pipelines agent..." -ForegroundColor Cyan

$base64AuthInfo = [Convert]::ToBase64String([Text.Encoding]::ASCII.GetBytes(":$(Get-Content ${Env:AZP_TOKEN_FILE})"))
$package = Invoke-RestMethod -Headers @{Authorization=("Basic $base64AuthInfo")} "$(${Env:AZP_URL})/_apis/distributedtask/packages/agent?platform=win-x64&`$top=1"
$packageUrl = $package[0].Value.downloadUrl

Write-Host $packageUrl

Write-Host "2. Downloading and installing Azure Pipelines agent..." -ForegroundColor Cyan

$wc = New-Object System.Net.WebClient
$wc.DownloadFile($packageUrl, "$(Get-Location)\agent.zip")

Expand-Archive -Path "agent.zip" -DestinationPath "\azp\agent"

try
{
  Write-Host "3. Configuring Azure Pipelines agent..." -ForegroundColor Cyan

  .\config.cmd --unattended `
    --agent "$(if (Test-Path Env:AZP_AGENT_NAME) { ${Env:AZP_AGENT_NAME} } else { ${Env:computername} })" `
    --url "$(${Env:AZP_URL})" `
    --auth PAT `
    --token "$(Get-Content ${Env:AZP_TOKEN_FILE})" `
    --pool "$(if (Test-Path Env:AZP_POOL) { ${Env:AZP_POOL} } else { 'Default' })" `
    --work "$(if (Test-Path Env:AZP_WORK) { ${Env:AZP_WORK} } else { '_work' })" `
    --replace

  Write-Host "4. Running Azure Pipelines agent..." -ForegroundColor Cyan

  .\run.cmd
}
finally
{
  Write-Host "Cleanup. Removing Azure Pipelines agent..." -ForegroundColor Cyan

  .\config.cmd remove --unattended `
    --auth PAT `
    --token "$(Get-Content ${Env:AZP_TOKEN_FILE})"
}
```

This script checks the environment, create some folders and __install and configure the agent__.

If you want a __fresh agent container__ for every pipeline job, pass the `--once` flag to the run command. You must also use a container orchestration system, like Kubernetes or Azure Container Instances, to make sure you __start new copies of the container__ when the work completes.

Finally, let's just create the image:

```cmd
docker build -t dockeragentwin:latest -f Dockerfile.windows .
```

Once again, you may want to [check the video and see this explained in much __greater details__.](https://www.youtube.com/watch?v=rO-VKProMp8&t=89s) 

#### Linux

> [Click here to check the video and see this explained in much __greater details__.](https://www.youtube.com/watch?v=rO-VKProMp8&t=207s) 

For Linux, the __Dockerfile looks a little different__:

```docker
FROM ubuntu:18.04

# To make it easier for build and release pipelines to run apt-get,
# configure apt to not require confirmation (assume the -y argument by default)
ENV DEBIAN_FRONTEND=noninteractive
RUN echo "APT::Get::Assume-Yes \"true\";" > /etc/apt/apt.conf.d/90assumeyes

RUN apt-get update \
&& apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        jq \
        git \
        iputils-ping \
        libcurl4 \
        libicu60 \
        libunwind8 \
        netcat \
        libssl1.0

WORKDIR /azp

COPY ./start.sh .
RUN chmod +x start.sh

CMD ["./start.sh"]
```

The main differences here are that we use a Linux base image, and that we need to __install the dependencies__ manually using `apt-get`.

Then we need the startup script as well, but this time is a __bash script__ (also provided by Microsoft [here](https://docs.microsoft.com/en-us/azure/devops/pipelines/agents/docker?view=azure-devops#create-and-build-the-dockerfile-1))

```bash
#!/bin/bash
set -e

if [ -z "$AZP_URL" ]; then
  echo 1>&2 "error: missing AZP_URL environment variable"
  exit 1
fi

if [ -z "$AZP_TOKEN_FILE" ]; then
  if [ -z "$AZP_TOKEN" ]; then
    echo 1>&2 "error: missing AZP_TOKEN environment variable"
    exit 1
  fi

  AZP_TOKEN_FILE=/azp/.token
  echo -n $AZP_TOKEN > "$AZP_TOKEN_FILE"
fi

unset AZP_TOKEN

if [ -n "$AZP_WORK" ]; then
  mkdir -p "$AZP_WORK"
fi

rm -rf /azp/agent
mkdir /azp/agent
cd /azp/agent

export AGENT_ALLOW_RUNASROOT="1"

cleanup() {
  if [ -e config.sh ]; then
    print_header "Cleanup. Removing Azure Pipelines agent..."

    ./config.sh remove --unattended \
      --auth PAT \
      --token $(cat "$AZP_TOKEN_FILE")
  fi
}

print_header() {
  lightcyan='\033[1;36m'
  nocolor='\033[0m'
  echo -e "${lightcyan}$1${nocolor}"
}

# Let the agent ignore the token env variables
export VSO_AGENT_IGNORE=AZP_TOKEN,AZP_TOKEN_FILE

print_header "1. Determining matching Azure Pipelines agent..."

AZP_AGENT_RESPONSE=$(curl -LsS \
  -u user:$(cat "$AZP_TOKEN_FILE") \
  -H 'Accept:application/json;api-version=3.0-preview' \
  "$AZP_URL/_apis/distributedtask/packages/agent?platform=linux-x64")

if echo "$AZP_AGENT_RESPONSE" | jq . >/dev/null 2>&1; then
  AZP_AGENTPACKAGE_URL=$(echo "$AZP_AGENT_RESPONSE" \
    | jq -r '.value | map([.version.major,.version.minor,.version.patch,.downloadUrl]) | sort | .[length-1] | .[3]')
fi

if [ -z "$AZP_AGENTPACKAGE_URL" -o "$AZP_AGENTPACKAGE_URL" == "null" ]; then
  echo 1>&2 "error: could not determine a matching Azure Pipelines agent - check that account '$AZP_URL' is correct and the token is valid for that account"
  exit 1
fi

print_header "2. Downloading and installing Azure Pipelines agent..."

curl -LsS $AZP_AGENTPACKAGE_URL | tar -xz & wait $!

source ./env.sh

print_header "3. Configuring Azure Pipelines agent..."

./config.sh --unattended \
  --agent "${AZP_AGENT_NAME:-$(hostname)}" \
  --url "$AZP_URL" \
  --auth PAT \
  --token $(cat "$AZP_TOKEN_FILE") \
  --pool "${AZP_POOL:-Default}" \
  --work "${AZP_WORK:-_work}" \
  --replace \
  --acceptTeeEula & wait $!

print_header "4. Running Azure Pipelines agent..."

trap 'cleanup; exit 130' INT
trap 'cleanup; exit 143' TERM

# To be aware of TERM and INT signals call run.sh
# Running it with the --once flag at the end will shut down the agent after the build is executed
./run.sh & wait $!
```

Although it looks different, this script does exactly the same things of the Windows one: prepare the system, and install and configure the agent.

Let's build the image:

```sh
docker build -t dockeragentlin:latest -f Dockerfile.linux .
```

Once again, if you want a fresh agent container for every pipeline job, pass the `--once` flag to the run command.

Remember to [check the video and see this explained in much __greater details__.](https://www.youtube.com/watch?v=rO-VKProMp8&t=207s) 

### Run the container

That was not too bad right? And the fact that, as we have seen, __Microsoft provides the full script for both platforms__ makes it even easier.

> If you are interested in how you can Drastically improve you Docker Build Performance, I have a [video which talks just about that](https://youtu.be/9-dt5aMRzVU).

To __run the container__, of course we can use the `docker run` command:

```cmd
docker run -e AZP_URL=<Azure DevOps instance> -e AZP_TOKEN=<PAT token> -e AZP_AGENT_NAME=<Agent name> dockeragentlin:latest
```

As you've probably noticed, there are some __environment variables__ we can use to control the execution. Needless to say, those works in both a local Docker instance as well as any orchestrator.

![Environment Variables](https://dev-to-uploads.s3.amazonaws.com/i/1mervh1doqgx0rbnzfhs.png)

We can use the ___AZP_URL___ variable to specify the URL of the instance of Azure DevOps we want to connect to. This parameter, as you may imagine, is __required__.

We also need to pass the ___AZP_TOKEN___ variable and its value must be a __Personal Access Token__ with the Read and Manage Agent Pools scope that is valid on the instance of Azure DevOps we are connecting to.

The other 3 variables are instead __optional__.

- ___AZP_AGENT_NAME___ lets you set a name for the agent and it defaults to the container hostname
- ___AZP_POOL___ is used to specify the Agent Pool that you want that specific agent to be part of
- And finally ___AZP_WORK___ lets you cange the working directory of the agent, which by default is __work_.

### Extend the basic image

At this point we have a __fully working basic build agent__. 

You can of course __extend the Dockerfile__ to include additional tools and their dependencies, or build your own container by using this one as a base layer. 

Just make sure that __the start script is called and it is the last command in the Dockerfile__, and ensure that any of the derivative containers don't remove any of the dependencies of the original one.

### The agent in Azure DevOps

Check out [this section of the video](https://www.youtube.com/watch?v=rO-VKProMp8&t=452s) to see how a __new agent appears__ in Azure DevOps.

### Important Notes

Before we close, just a few notes.

First of all, as we have seen before, __the startup script installs the agents every time__ the image is run from scratch. If you want the startup to be quicker, you can consider installing the agent as part of your docker image creation instead.

Also, remember that each agent __automatically updates__ itself when it runs a task that requires a newer version of the agent.

Second thing to note is that in order to __use Docker from within a Docker container__, you have to _bind-mount_ the Docker socket.

![Warning](https://dev-to-uploads.s3.amazonaws.com/i/fz14cevz0ndjr0g3mrz8.png)

As this very noticeable warning message on the official documentation site says, remember that doing so it is __not recommended__ because it has serious security implications. The code inside the container can inf cat run as root on your Docker host.

Lastly, if you are trying to run this on Windows and you experience an error like the one below, you need to install _Git Bash_ by downloading and installing __git-scm__.

![Error](https://dev-to-uploads.s3.amazonaws.com/i/0cubx3zlr88ic1s0thc1.png)

### Conclusions

Alright, that's it for today. Now you can take those container images and run them in __any orchestration of your choice__, to have a truly flexible and scalable CICD platform with Azure Pipelines.

Let me know in the comment section below what you think about this, and if you'd like me to make a follow-up post/video on this showing how to deploy the containerized Azure Pipeline agents to Kubernetes.

{% youtube rO-VKProMp8 %}