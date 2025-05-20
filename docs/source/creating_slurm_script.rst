Creating a SLURM Script
========================================

In this section, we will guide you step-by-step on creating and running a SLURM script. Once you’ve evaluated the available computing resources, you are ready to write a script that integrates your resource requests, module loads, and job commands.

Step 1: Create the Script File
---------------------------------
Open your favorite text editor and create a new file—commonly named ``job_script.sh``. This file will serve as the blueprint for your job submission.

Step 2: Write the SLURM Script
-------------------------------
Every SLURM script begins with a bash shebang, followed by a series of ``#SBATCH`` directives that specify resource allocations. Below is an example:

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
- ``--job-name`` sets a label for your job, making it easier to locate in the queue.
- ``--output`` and ``--error`` capture the job's output and error messages, which can be vital for debugging.
- ``--partition`` selects the appropriate subset of nodes, ensuring your job is run on the intended hardware.
- ``--time`` defines the maximum runtime, helping the scheduler manage job durations.
- ``--nodes`` and ``--ntasks-per-node`` let you fine-tune the scope of resource allocation.

Step 3: Submit the Job
------------------------
After saving the script, submit the job to the SLURM scheduler with the following command:

.. code-block:: bash

   sbatch job_script.sh

SLURM will return a job ID upon submission. This identifier is essential for tracking the job’s status.

Step 4: Monitor Your Job
-------------------------
You can monitor the status and progress of your job using several commands:
- **``squeue``**: Lists all jobs in the queue along with their current state.
- **``scontrol show job <job_id>``**: Provides detailed info about a specific job.
- **``sacct``**: Displays accounting information for jobs, including resource usage, which helps in performance tuning.

Step 5: Review Output and Logs
-------------------------------
Once your job completes, check the ``example_output.log`` and ``example_error.log`` files. These logs offer insights into job performance and help diagnose any issues that may have arisen.

**Maximizing Efficiency and Fair Resource Use**

Before submitting your script, consider whether your application truly requires specialized resources such as GPUs. GPUs can dramatically accelerate tasks that benefit from parallel processing, but they are limited. By accurately assessing your job’s needs, you help maximize resource utilization without creating system bottlenecks. Optimizing your script ensures that the allocated resources are fully utilized during job execution while maintaining a fair computing environment for all users.

By following these steps, you'll create a robust SLURM script that makes efficient use of your HPC system's resources. Regularly reviewing and refining your script based on logged performance data will also help ensure that you remain both efficient and considerate of other users.