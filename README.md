# Deploy an Auto-Scaling HPC Cluster with Slurm on Google Cloud Platform using Marketplace

This tutorial shows how to deploy an auto-scaling Slurm cluster on Google Cloud Platform using Marketplace. 

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

1. From the dropdown select the project where you want to deploy the Slurm Cluster. 
<br>

![SchedMD-Slurm-GCP](/assets/images/1.png)

<br>
2. From the Navigation menu click on the Marketplace.

![SchedMD-Slurm-GCP](/assets/images/2.png)

<br>
3. In the search for **SchedMD-Slurm-GCP**.
<br><br>

![SchedMD-Slurm-GCP](/assets/images/3.png)

<br>
4. From the search you will see the below result. 
<br><br>

![SchedMD-Slurm-GCP](/assets/images/4.png)

<br>
5. Click on the **Schedmd-Slurm-GCP** from the result and Click **Launch**. 
<br><br>

![SchedMD-Slurm-GCP](/assets/images/5.png)

<br>
6. Some of the options provide defaults, others require input. 

<ul>
<li>Enter the Deployment name, Cluster name.</li>
<li>Select the Zone and Network interface where Slurm Cluster has to deployed.</li>
</ul>
<br>

![SchedMD-Slurm-GCP](/assets/images/6.png)

<br>
7. Configure Slurm Controller: 
<ul>
<li>Under Machine family section, Choose the <strong>Machine family</strong> as required.</li>
<li>Choose the <strong>Machine type</strong> as required.</li>
<li>Click on <strong>MORE</strong> and then Choose the <strong>Boot Disk Type</strong> and <strong>Size</strong> required. </li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/7.png)

<br>
8. Configure Slurm Login:
<ul>
<li>Click on SHOW SLUM LOGIN OPTIONS</li>
<li>Under Machine family section, Choose the <strong>Machine family</strong> as required.</li>
<li>Choose the <strong>Machine type</strong> as required.</li>
<li>Choose the <strong>Boot Disk Type</strong> and <strong>Size</strong> required. </li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/8.png)

<br>
9. Configure Slurm Compute Partition:
<ul>
<li>Enter the <strong>Name</strong> of the partition 1.</li>
<li>Set the <strong>Maximum Instance Count</strong>.</li>
<li>Set the <strong>Number of Static nodes to create</strong> initially.</li>
<li>Under Machine family section, Choose the <strong>COMPUTE-OPTIMISED</strong> Tab. Strongly recommend choosing a <strong>compute-optimized instances</strong>. 
<li>Choose the <strong>Machine type</strong> as required.</li>
<li>Click on <strong>MORE</strong> and then Choose the <strong>Boot Disk Type</strong> and <strong>Size</strong> required. </li>
</ul>

> To learn why compute optimized instances, read [Use compute-optimized instances](https://cloud.google.com/solutions/best-practices-for-using-mpi-on-compute-engine#use_compute-optimized_instances).

![SchedMD-Slurm-GCP](/assets/images/9.png)

<br>
10. Adding additional Partition
<ul>
<li>By default, one partition is enabled. Check the box “Enable partition” under the “Slurm Compute Partition” sections to configure more partitions.</li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/10.png)

<br>
11. <strong> When complete, click “Deploy”. </strong>
