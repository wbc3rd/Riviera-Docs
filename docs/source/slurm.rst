Slurm
=====

What is Slurm?
--------------
Slurm is the job scheduling and workload manager system run by Riviera. It enables users to schedule tasks using SBATCH scripts or to run on a compute node interactively. To run an SBATCH script a user executes the command ``sbatch job_script.sh``. To run interactively you execute the command ``srun --partition=short-cpu --pty bash``, short-cpu is the default partition to run on but any partition can be specified depending on the resources needed. Once this command is run you will be running all further commands on the node selected until exiting using the command ``exit``. 

Creating a Slurm SBATCH script
------------------------------

Step 1: Create the SBATCH File
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
All SBATCH files are actually shell script files. To create a new file a user can run ``touch job_script.sh``. This creates an empty file with the name job_script.sh in the current directory. A user can then user nano or vim to edit the file. Alternatively, if a user is not comfortable with using nano or vim to edit files in a terminal they can make the file on their local machine and then once it is ready transfer it over to Riviera with a tool like :ref:`scp<Data Transfer and File Management>`.

Step 2: Write the SBATCH Script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Every Slurm script begins with a bash shebang, a shebang is the characters ``#!`` followed by a path to an interpreter. For SBATCH scripts the interpreter is bash so the shebang is ``#!/bin/bash``.

After the shebang SBATCH scripts contain a series of directives denoted by ``#SBATCH``. These directives function as settings for the particular job. For a list of common SBATCH directives see `SBATCH Directives <https://riviera-docs.readthedocs.io/en/latest/sbatch_directives.html>`_. A very basic example SBATCH script can be seen below, for more SBATCH script examples see `SBatch Use Cases <https://riviera-docs.readthedocs.io/en/latest/sbatch_use_cases.html#>`_.

.. code-block:: bash

   #!/bin/bash
   #SBATCH --job-name=ExampleJob         # Set a descriptive name for your job.
   #SBATCH --output=example_output.log   # Direct standard output to a file.
   #SBATCH --error=example_error.log     # Direct error output to a file.
   #SBATCH --partition=batch             # Specify the partition to use.
   #SBATCH --time=01:00:00               # Maximum run time (hh:mm:ss).
   #SBATCH --nodes=1                     # Number of nodes.
   #SBATCH --ntasks-per-node=16          # Number of tasks per node.

   # Load necessary modules or environment variables.
   module load python/3.8

   # Run your application.
   srun python my_script.py

**Explanation of the Directives:**
* ``--job-name`` sets a label for the job, making it easier to locate in the queue.
* ``--output`` and ``--error`` capture the job's output and error messages and specify the file path that the messages should be written to.
* ``--partition`` selects the appropriate subset of nodes, ensuring a job is run on the intended hardware.
* ``--time`` defines the maximum runtime, helping the scheduler manage job durations and scheduling.
* ``--nodes`` and ``--ntasks-per-node`` helps fine-tune the scope of resource allocation by specifying the number of nodes a job needs and how many tasks each node step will spawn.

Step 3: Submit the Job
^^^^^^^^^^^^^^^^^^^^^^
After saving the script, submit the job to the SLURM scheduler with the following command:

.. code-block:: bash

   sbatch job_script.sh

SLurm will return a job ID upon submission. This identifier is essential for tracking the job's status.

Step 4: Monitor A Job
^^^^^^^^^^^^^^^^^^^^^
A user can monitor the status and progress of your job using several commands:
- ``squeue``: Lists all jobs in the queue along with their current state.
- ``scontrol show job <job_id>``: Provides detailed info about a specific job.
- ``sacct``: Displays accounting information for previously run jobs, including resource usage, which helps in performance tuning.

Step 5: Review Output and Logs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Once a job completes, a user can check the output and error logs as specified in the SBATCH script. These logs can both offer insights on job performance and also give a user some results from their job if they were for instance printing calculation results to the standard output stream (such as with python's ``print()`` function which by default prints to stdout).

Additional Resources
^^^^^^^^^^^^^^^^^^^^
For a demonstration of creating and running a SLURM script, check out the `YouTube tutorial on SLURM scripts <https://youtu.be/bER-Syr9_pI?si=48lMnWvQ_tufdbPJ>`_.

What Computing Resources Are Available?
---------------------------------------

Before creating a SLURM script, it's essential to understand the HPC system's infrastructure and current workload. This knowledge can help decide which node or partition to target and how to request the right resources.

Inspecting Node Status with ``sinfo``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The ``sinfo`` command gives you a quick overview of all partitions and their nodes, along with their status. When a user runs

.. code-block:: bash

   sinfo

they will see columns that typically include partition names, node state (e.g., idle, alloc, down, mix), available CPU cores, and memory. For example, an output might look like this

.. code-block::

   PARTITION  AVAIL  TIMELIMIT   NODES  STATE   NODELIST
   batch      up     7-00:00:00  10     idle    node[01-10]
   gpu        up     3-00:00:00  5      mix     gpu01, gpu02, gpu03, gpu04, gpu05

In this output:
* **idle** nodes are free to run your job.
* **alloc** or **busy** nodes are currently in use.
* **mix** indicates that some resources on the node are allocated while others might still be free.
* **down** means that the node is unavailable for scheduling, possibly due to maintenance or errors.

Obtaining Detailed Node Information with ``scontrol``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For a more in-depth look at individual nodes, a user can use

.. code-block:: bash

   scontrol show nodes

This command displays detailed information for each node, such as memory, CPU count, available features, and current state. This information is invaluable when a job requires a specific hardware or software configuration.

Allocating Resources in an SBATCH Script
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Based on the information gathered from ``sinfo`` and ``scontrol``, a user can fine-tune an SBATCH script. For instance, if they determine that GPU-enabled nodes are available in a "gpu" partition, the script might look like

.. code-block:: bash

   #!/bin/bash
   #SBATCH --job-name=MyGPUJob
   #SBATCH --partition=gpu
   #SBATCH --gres=gpu:1        # Request one GPU
   #SBATCH --time=02:00:00     # Set the job run time to 2 hours
   #SBATCH --nodes=1           # Request one node
   #SBATCH --ntasks=1          # Typically one task for GPU jobs

   # Load necessary modules or set up the environment
   module load cuda

   # Run your application
   srun my_gpu_application

Similarly, if a user notices that a specific partition has more idle nodes and is optimal for CPU-intensive tasks, they can adjust the resource request accordingly

.. code-block:: bash

   #!/bin/bash
   #SBATCH --job-name=MyCPUTask
   #SBATCH --partition=batch
   #SBATCH --time=01:00:00     # Set the job run time to 1 hour
   #SBATCH --nodes=1
   #SBATCH --ntasks-per-node=16

   # Load any necessary modules
   module load python

   # Execute your program
   srun python my_cpu_script.py

Resource Efficiency and Fair Use
--------------------------------
Before submitting a script, consider whether the application truly requires specialized resources such as GPUs. GPUs can dramatically accelerate tasks that benefit from parallel processing, but they are limited. By accurately assessing a job's needs, resource utilization is maximized without creating system bottlenecks. Optimizing a script ensures that the allocated resources are fully utilized during job execution while maintaining a fair computing environment for all users.
