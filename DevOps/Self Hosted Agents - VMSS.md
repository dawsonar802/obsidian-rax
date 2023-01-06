---
created: 2023-01-06 09:42
date: 2023-01-06
tags: 
---
#azure #vmss #ado #selfhosted #agent 


# Overview 
Azure virtual machine scale set agents, hereafter referred to as scale set agents, are a form of self-hosted agents that can be autoscaled to meet your demands. This elasticity reduces your need to run dedicated agents all the time. Unlike Microsoft-hosted agents, you have flexibility over the size and the image of machines on which agents run.

## When to use VMSS Agents
-   You don't want to run dedicated agents around the clock. You want to de-provision agent machines that are not being used to run jobs.
-   You run untrusted code in your pipeline and want to re-image agent machines after each job.
-   You want to simplify periodically updating the base image for your agents.

# Setup (basic)
1. Provision a VMSS instance in Azure
2. Complete the outlined steps for setting up the pool [here](https://learn.microsoft.com/en-us/azure/devops/pipelines/agents/scale-set-agents?view=azure-devops#create-the-scale-set-agent-pool)
3. 