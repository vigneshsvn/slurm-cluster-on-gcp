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

![SchedMD-Slurm-GCP](/assets/images/1.png)

<br>

2. From the Navigation menu click on the Marketplace.

![SchedMD-Slurm-GCP](/assets/images/2.png)

<br>

3. In the search for **SchedMD-Slurm-GCP**.

![SchedMD-Slurm-GCP](/assets/images/3.png)

<br>

4. From the search you will see the below result. 

![SchedMD-Slurm-GCP](/assets/images/4.png)

<br>

5. Click on the **Schedmd-Slurm-GCP** from the result and Click **Launch**. 

![SchedMD-Slurm-GCP](/assets/images/5.png)

<br>

6. Some of the options provide defaults, others require input. 

<ul>
<li>Enter the Deployment name, Cluster name.</li>
<li>Select the Zone and Network interface where Slurm Cluster has to deployed.</li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/6.png)

7. Configure Slurm Controller: 
<ul>
<li>Under Machine family section, Choose the <strong>Machine family</strong> as required.</li>
<li>Choose the <strong>Machine type</strong> as required.</li>
<li>Click on <strong>MORE</strong> and then Choose the <strong>Boot Disk Type</strong> and <strong>Size</strong> required. </li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/7.png)

8. Configure Slurm Login:
<ul>
<li>Click on SHOW SLUM LOGIN OPTIONS</li>
<li>Under Machine family section, Choose the <strong>Machine family</strong> as required.</li>
<li>Choose the <strong>Machine type</strong> as required.</li>
<li>Choose the <strong>Boot Disk Type</strong> and <strong>Size</strong> required. </li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/8.png)

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

10. Adding additional Partition
<ul>
<li>By default, one partition is enabled. Check the box “Enable partition” under the “Slurm Compute Partition” sections to configure more partitions.</li>
</ul>

![SchedMD-Slurm-GCP](/assets/images/10.png)

11. When complete, click <strong>Deploy</strong>.

<br>

12. When the deployment is complete, you should see a check box saying deployment completed.

![SchedMD-Slurm-GCP](/assets/images/11.png)

<br>

## Run a job using Slurm

1. SSH to the Login node by clicking the <strong>SSH TO SLURM LOGIN NODE</strong> button.

<br>

2. Execute the <strong>sinfo</strong> command to view the status of our cluster's resources. You can see our <strong>10 nodes</strong>, dictated by the debug partition's <strong>"max_node_count" of 10</strong>, are marked as "idle~" (the node is in an idle and non-allocated mode, ready to be spun up).

<img src="/assets/images/12.png" alt="SchedMD-Slurm-GCP" width="1000" height="750" />

<br>
<br>

3. Next, execute the <strong>squeue</strong> command to view the status of our cluster's queue. We don't have any jobs running, so the contents of this command are empty.

```shell
JOBID PARTITION     NAME     USER ST       TIME  NODES NODELIST(REASON)
```

> <br> <strong>Note:</strong> The Slurm commands "srun" and "sbatch" are used to run jobs that are put into the queue. "srun" runs parallel jobs, and can be used as a wrapper for mpirun. "sbatch" is used to submit a batch job to slurm, and can call srun once or many times in different configurations. "sbatch" can take batch scripts, or can be used with the –wrap option to run the entire job from the command line.
<br>

4. Run a Slurm Job and Scale the Cluster

Create file <strong>example.sh</strong> using the below command

```shell
cat > example.sh << EOF 
#!/bin/bash
srun hostname
EOF
```

Type <strong>ls</strong> to check the file is created. then run the following command to execute the batch job.

```shell
sbatch --nodes=2 example.sh
```

You will get an <strong>output</strong> like 

```shell
Submitted batch job 2
```

To view the job queue, type <strong>squeue</strong>

You will likely see the job you executed listed like below:

```shell
JOBID PARTITION                               NAME      USER ST       TIME  NODES   NODELIST(REASON)
    2     p1 slurm-test-cluster-compute-[0-1] username  R             0:10      2   gslurm-test-cluster-compute-0-[0-1]
```

<br>

5. View the new compute nodes added on the Console.

![SchedMD-Slurm-GCP](/assets/images/13.png)


> <strong>Note:</strong> <br>
<strong>sbatch</strong> is the Slurm command which runs Slurm batch scripts. [More Info](https://slurm.schedmd.com/sbatch.html).<br>
<strong>srun</strong> is the Slurm command which runs commands in parallel. [More Info](https://slurm.schedmd.com/srun.html).<br>
<strong>squeue</strong> is the Slurm queue monitoring command line tool. It lists all running jobs, and the resources they are associated with. [More Info](https://slurm.schedmd.com/squeue.html).<br>
<strong>sinfo</strong> is the Slurm command which lists the information about the Slurm cluster. This lists the Slurm partition, availability, time limit, and current state of the nodes in the cluster. [More Info](https://slurm.schedmd.com/sinfo.html).
<br>

## Congratulations, you've run a job and scaled up your Slurm cluster on Google Cloud Platform! 

You can use this model to run any variety of jobs, and it scales to hundreds of instances in minutes by simply requesting the nodes in Slurm

> <br> NOTE: syslog and all Slurm logs can be viewed in GCP Console's Logs Viewer.
<br>

## Support
Slurm Troubleshooting Guide: https://slurm.schedmd.com/troubleshoot.html 
