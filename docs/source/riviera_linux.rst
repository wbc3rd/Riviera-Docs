Riviera Structure
================

Operating System
----------------
Riviera currently runs `Rocky Linux 8.8 <https://rockylinux.org/>`_ (Green Obsidian). 

Workload management
-------------------
Riviera uses Slurm for workload management. The basic layout of Riviera as seen by Slurm is:

* Node: A compute resource.
    * Riviera has normal nodes, high memory nodes, and gpu nodes.
* Partition: A set of possible nodes a job runs on. (Nodes can belong to multiple partitions).
    * A partition functions as a queue where job that have been requested get scheduled. 
    * Partitions have constraints such as job size and job time limit.
* Job: An allocation of compute resources to a user for a period of time.
    * Jobs contain Job Steps which contain Job Tasks.
* Job steps: A set of actions within a job.
    * A job has one or more steps associated with it.
    * Jobs created with ``sbatch`` have one implicit step, the Bash script itself
* Job Task: A set of actions within a job step.
    * Each job step creates one or more job tasks associated with it. 
    * Job tasks are actions run sequentially or concurrently created by a Job step.
    * The majority of jobs will not need to have more than one job task per step, it is typically only used with MPI.

For more on Slurm itself see `Slurm <slurm>`_.

File Management
---------------
Riviera uses NFS to serve user's home directories to whatever partition a user is connected to. User's home directories have a default of 1000 GB of available storage but users should not plan to use more than 500 GB of it except for as scratch space when a program is running. Users should also not use their available home directory storage as permanent storage for any programs or data and should instead transfer files on and off of Riviera as needed. User's home directories may have old files cleaned up off of them periodically so nothing important should be kept exclusively there.

Riviera does not currently have scratch space for users to work in, and users are instead directed to use their home directory as scratch space unless they have high speed requirements. If a user has high speed requirements for storage they can reach out to the Riviera team to be instructed on how to use high speed storage local to each node as scratch space.

Compute Nodes
-------------

Riviera has three main types of compute nodes, CPU compute nodes, high memory CPU compute nodes, and GPU compute nodes. 

* The CPU compute nodes are for users who do not have jobs that will take up a substantial amount of memory, need GPU compute resources, or need hyperthreading enabled.
    * Each CPU compute node has 2 AMD EPYC 7763 64-Core Processors without hyperthreading enabled and approximately 500 GB of total available memory. 
* The high memory compute nodes are for users who have jobs that do not use a GPU but need a lot of memory resources allocated to them or need hyperthreading enabled on the CPU.
    * Each high memory compute node has two AMD EPYC 7763 64-Core Processors with hyperthreading enabled and approximately 2000 GB of total available memory. 
* The GPU compute nodes are for users who have jobs that need access to GPU resources.
    * Each GPU compute node has 2 AMD EPYC 7763 64-Core Processors without hyperthreading enabled, four Nvidia A100 80GB graphics cards, and approximately 500 GB of total available memory. 
    
Each compute node type also has three different partition options that affect run length:
* short where the maximum job length is 2 hours.
* day-long where the maximum job length is 24 hours.
* week-long where the maximum job length is 7 days.

Modules
-------
Modules are packages preloaded onto Riviera for any user to use without needing to install from source. To view a list of available modules you can run the command ``module av``. To view a list of modules you have loaded you can run the command ``module list``. In order to do any sort of computing on the cluster you will need to load the slurm module. To load the module (or any other module) run the command ``module load slurm``. To unload a module you can run the command ``module unload module_name``, and to unload all modules you can run ``module purge``.

