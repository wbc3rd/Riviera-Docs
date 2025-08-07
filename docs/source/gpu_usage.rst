GPU Usage Guidelines
====================

The Riviera HPC cluster provides access to GPU resources for computationally intensive tasks such as deep learning, large-scale simulations, and data processing. This page outlines the proper usage of GPUs, how to request them and best practices.

When to Use a GPU
-----------------

- If your application uses CUDA, OpenCL, or GPU-accelerated libraries.
- If you are training large machine learning models.
- If you need significantly faster matrix operations or rendering performance.
- If your software documentation explicitly mention GPU support.

Requesting a GPU in Slurm 
-------------------------

To use a GPU in a job, you must request it in your Slurm job script:

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
   srun my_gpu_application.py

Available GPU Resources
-----------------------

- **2 AMD EPYC 7763 64-Core Processor** without hyperthreading GPU-enabled
- **4 NVIDIA A100 80GB Graphic cards**

Monitoring GPU Usage
--------------------

Use the ``nvidia-smi`` tool within your job to monitor GPU activity:

.. code-block:: bash

    srun --partition=short-gpu --pty bash
    nvidia-smi

Best Practices
--------------

- Test your code on CPUs first.
- Run batch jobs instead of interactive GPU sessions.
- Release GPUs as soon as your job is done. 
- Store model checkpoints periodically (see `Checkpointing <https://riviera-docs.readthedocs.io/en/latest/checkpoint_jobs.html>`_).

Dos and Don't
-------------

.. list-table:: GPU Usage Dos and Don't
    :header-rows: 1
    :widths: 40 60

    * - Do
      - Don't 
    * - Request GPUs only when needed
      - Run CPU-only jobs on GPU nodes
    * - Monitoure GPU usuage with `nvidia-smi`
      - Compile software on GPU nodes
    * - Use `--gres=gpu:N` or `--partition=short-gpu` in Slurm scripts
      - Leave jobs idle on GPU nodes
    * - Use time limits appropriatley
      - Request more GPUs than necessary

When Code is not Using GPU Effectively
--------------------------------------
- GPU utilization is consistently below 50%
- High CPU usage with low GPU usage
- More time spent in memory transfer than computation
- Sequential operations that could be parallelized
- Algorithm not suited for GPU architecture (highly branching, irregular memory access)
