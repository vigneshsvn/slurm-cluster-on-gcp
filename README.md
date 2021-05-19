# Deploy an Auto-Scaling HPC Cluster with Slurm on Google Cloud Platform using Marketplace

This tutorial shows how to deploy a auto-scaling Slurm cluster on Google Cloud Platform using Marketplace. 

## About Slurm

Slurm is one of the leading workload managers for HPC clusters around the world. Slurm provides an open-source, fault-tolerant, and highly-scalable workload management and job scheduling system for small and large Linux clusters. Slurm requires no kernel modifications for its operation and is relatively self-contained. As a cluster workload manager, Slurm has three key functions:

<ol>
<li>It allocates exclusive or non-exclusive access to resources (compute nodes) to users for some duration of time so they can perform work.</li>

<li>It provides a framework for starting, executing, and monitoring work (normally a parallel job) on the set of allocated nodes.</li>

<li>It arbitrates contention for resources by managing a queue of pending work.</li>
</ol>
<br>

![Basic architectural diagram of a stand-alone Slurm Cluster in Google Cloud](/assets/images/0.png)
Basic architectural diagram of a stand-alone Slurm Cluster in Google Cloud. Ref: [Codelabs](https://codelabs.developers.google.com/codelabs/hpc-slurm-on-gcp/img/a739730a41acff0a.png).

<br>

> Learn More About Slurm at [Slurm Overview](https://slurm.schedmd.com/overview.html).

<br>
## What you'll learn
<ul>
<li>How to deploy the Slurm Cluster using Marketplace</li>
<li>How to run a job using Slurm</li>
<li>How to query cluster information and monitor running jobs in Slurm</li>
<li>How to autoscale nodes to accommodate specific job parameters and requirements</li>
</ul>

## Prerequisites
<ul>
<li>Google Cloud Platform Account and a Project with Billing</li>
<li>Basic Linux Experience</li>
</ul>

<br>
## Deploying the Slurm Cluster using Marketplace

From the dropdown select the project where you want to deploy the Slurm Cluster

![Select the project](/assets/images/1.png)
<img src="/assets/images/1.png" alt="Select the project"  width="800" height="200" />