---
title: Azure ARM Deployment of Docker
layout: default
description: deploy a docker container to a VM via ARM deployment template
copyright: copyright &copy; 2017 Jeff Gabriel
---
## {{page.title}}

While all the excitement may rightly be around what can be done with containers in a managed cluster deployment like Kubernetes or Swarm, sometimes you don't need a cluster. Sometimes you just want to use a container by itself, deployed to its own VM. And just because you want this unexciting buzzword-free deployment doesn't mean you shouldn't have some fun automating it.

Lately I've found lots of reasons to use Docker on individual VMs. First, I can work out the configuration locally without ever using a VM. I've been doing this a lot with our development tools suite like with our git server, our private package repo, our sonarqube server, and even our Jira and Confluence servers. Second, if I build out the image and deployed containers properly, I can kill a mis-behaving image very easily and start over without missing a beat. This is not theoretical - I've done it several times; including with a portion of our consumer facing production application.  Finally, though not exhaustively, building the environment into containers is a habit I want our organization to form so that we think about and prepare more of our applications this way. If we deploy containers to single VMs, we're just as ready to deploy to a managed cluster should the need arise. We continue to find reasons to include containers in all parts of our environment.

Enough about the motivation, let's look at how I've been doing this with Azure ARM templates. The full example source is over at <a href="https://github.com/jeffgabriel/ARMBasedDockerDeploy">GitHub</a> if you just want to get right into it.

For this example we're deploying a Redis server with the base <a href="https://hub.docker.com/_/redis/" target="_blank">Redis docker image</a> with the <a href="https://hub.docker.com/_/alpine/" target="_blank">Alpine</a> tag. <a href="https://alpinelinux.org/" target="_blank">Alpine</a>[*](#gliderlabs) is a very small (5MB) linux variant based on BusyBox and I use these variants whenever offered because I often store my own custom images and space savings is cost savings.  If you want to startup the Redis server on your local system (given that you have the Docker runtime available) simply execute the following command:

```shell
docker run --name redis -p 6379:6379 -d redis:3.2-alpine
```
I'll leave you to explore the <a href="https://docs.docker.com/engine/reference/run/">run command docs</a> if you want details, but you now have a redis server running locally and ready to respond on localhost at port 6379.

### The Azure Environment
A lot of what goes into an ARM template is there to get an environment up inside a resource group on Azure. If you're not familiar yet with Azure and ARM, you may want to start with the following first:
- <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template">https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template</a>
- <a href="https://docs.microsoft.com/en-us/azure/virtual-machines/linux/">https://docs.microsoft.com/en-us/azure/virtual-machines/linux/</a>

If you have a look at <a href="https://github.com/jeffgabriel/ARMBasedDockerDeploy/blob/master/DeployRedis-template.json" target="_blank">the template</a> you'll want to focus on the two extensions I have added to the virtual machine.

#### Docker Extension
The Docker extension simply installs Docker on the VM. You can pass parameters to setup your docker container and in particular setup variables and files to help with compose operations. These are helpful but I have found that I need to run the custom script anyhow in most cases so I ignore this capability, but your experience may vary.
#### Custom Script Extension
The custom script extension will download files from either public or private sources and then execute a command. I use the custom script to not only run the initial docker but also to setup the system daemon and install log rotation configuration. In production deployments there is usually a need to pull down an image from a private repo and potentially modify the system configuration to enable storage for a permanent volume such as with database containers.
### Running the ARM Deployment[**](#secrets)
All of the files you need to run the deployment are in the referenced git repo. Executing the powershell script *DeployRedis.ps1* will generate a resource group or use an existing one. You'll need to update the subscriptionid to your own, and login to Azure first. You're then ready to execute a deployment based on the *DeployRedis-template.json* ARM template. I recommend that you also change the name of the resource group and either change the passwords in the template itself or pass in new values to override the defaults.

Once you execute the script you'll be able to connect to your public IP over SSH[***](#sshaccess). This template does not configure the redis port to be open in the attached NSG. You can find the public DNS name by browsing in the Azure portal or by executing the following (chaning rg name if you changed during deploy):
```powershell
$publicIp = Get-AzureRmPublicIpAddress `
-ResourceGroupName 'redis-sample-rg' `
-Name 'redis-server-pip'
$publicIp.DnsSettings.Fqdn
```
#### Debugging
If you get the VM to deploy but still get errors from the custom scripts module, these errors returned may seem unhelpful.  If you're having trouble figuring out what went wrong then SSH to the VM and see if there is something more helpful in the console output:
```shell
sudo -i
cat /var/lib/waagent/custom-script/download/0/stderr
```
Also note that any command you execute which writes to stderr will cause the extension to report failure. If you have something which does this in your script then send the output of that command somewhere else.
#### Resources and Further Reading
- <a href="https://docs.microsoft.com/en-us/azure/virtual-machines/linux/extensions-customscript" target="_blank">Custom Script Extension documentation</a>
- <a name="gliderlabs">*</a> When I am writing my own image I like to use the Gliderlabs Alpine base image instead of the official package.
- <a name="secrets">**</a>I've removed a couple of complicating factors by removing secrets. I normally use the Azure KeyVault to store an SSH key, a password to a private image repository, and any other passwords used in the custom scripts. I left a sample secrets reference in the parameters file but suggest you take a look at <a href="https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-keyvault-parameter" target="_blank">the documentation</a> for more details. You can see a simple implementation with a <a href="https://github.com/Azure/azure-quickstart-templates/blob/master/marketplace-samples/simple-Linux-VM/Simple-Linux-VM-sshPublicKey.json" target="_blank">SSH key here</a>.
- <a name="sshaccess">***</a> You'll want to tighten up the public NSG if you run the sample config so that your SSH port access is only allowed from your own IP.
