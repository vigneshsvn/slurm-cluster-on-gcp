# Deploying a Slurm cluster on Google Cloud Platform using Marketplace

This tutorial shows how to deploy a Slurm cluster on Compute Engine. 
<br>

## About Slurm

Slurm is one of the leading workload managers for HPC clusters around the world. Slurm provides an open-source, fault-tolerant, and highly-scalable workload management and job scheduling system for small and large Linux clusters. Slurm requires no kernel modifications for its operation and is relatively self-contained. As a cluster workload manager, Slurm has three key functions:
<br>

![Basic architectural diagram of a stand-alone Slurm Cluster in Google Cloud](/assets/images/0.png)

<br>


Basic architectural diagram of a stand-alone Slurm Cluster in Google Cloud. Ref: [Codelabs](https://codelabs.developers.google.com/codelabs/hpc-slurm-on-gcp/img/a739730a41acff0a.png).


<ol>
<li>It allocates exclusive or non-exclusive access to resources (compute nodes) to users for some duration of time so they can perform work.</li>

<li>It provides a framework for starting, executing, and monitoring work (normally a parallel job) on the set of allocated nodes.</li>

<li>It arbitrates contention for resources by managing a queue of pending work.</li>
</ol>

https://codelabs.developers.google.com/codelabs/hpc-slurm-on-gcp/img/a739730a41acff0a.png