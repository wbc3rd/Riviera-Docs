Checkpointing Jobs
==================

Checkpointing is the process of periodically saving a job’s progress by capturing its current state or key values. This allows a job to resume from the last saved point instead of starting over in the event of an interruption.

Checkpoint Usage
----------------
Checkpoints are useful for recovering from:

- Hardware or node failures
- Exceptions that occur after a job step
- Reaching the job’s time limit
- Job preemption mid-execution (to avoid repeating completed work)

They can also be used for:

- Debugging purposes
- Monitoring the internal state of a running program

Implementing Checkpoints
------------------------
Checkpointing can be implemented in several ways:

- **Language-level support:** Some programming languages offer built-in features to save a program’s state when it is paused or preempted, allowing it to resume later. However, these features typically do not support recovery from full job failures or crashes.
- **Workflow management tools:** Tools like Snakemake and Nextflow support checkpointing by organizing job steps into a Directed Acyclic Graph (DAG). Checkpoints can be assigned to specific nodes within the graph, enabling partial progress to be saved and resumed efficiently.
- **Manual checkpointing:** In a do-it-yourself (DIY) approach, users can periodically write important data or intermediate results to a file at key stages of the job. This manual method provides flexibility and is especially useful when no automated checkpointing support is available.

SRUN Checkpointing Options
--------------------------
``srun`` provides several options to support checkpoint and restart functionality for job steps:

- ``--checkpoint``: Sets the time interval for automatically creating checkpoint images during a job step. By default, no checkpoints are created. Valid formats for this interval include:

  - ``"minutes"``

  - ``"minutes:seconds"``

  - ``"hours:minutes:seconds"``

  - ``"days-hours"``

  - ``"days-hours:minutes"``

  - ``"days-hours:minutes:seconds"``

- ``--checkpoint-dir``: Specifies the directory where checkpoint files for the job step will be saved. If not set, the current working directory is used by default. Checkpoint files are named as follows:

  - For entire jobs: ``<job_id>.ckpt``

  - For specific job steps: ``<job_id>.<step_id>.ckpt``

- ``--restart-dir``: Indicates the directory from which checkpoint files should be read when restarting a job step.

Each of these options also has a corresponding environment variable:

- ``SLURM_CHECKPOINT`` = ``--checkpoint``
- ``SLURM_CHECKPOINT_DIR`` = ``--checkpoint-dir``
- ``SLURM_RESTART_DIR`` = ``--restart-dir``

In addition, the variable ``SLURM_SRUN_CR_SOCKET`` is used internally to allow job step logic to communicate with the ``srun_cr`` command.

SBATCH Checkpointing Options
----------------------------
``sbatch`` supports checkpoint and restart functionality through the following options:

- ``--checkpoint``: Defines the interval for creating periodic checkpoints of a batch job. By default, no checkpoints are created. Valid time formats include:

  - ``"minutes"``
  - ``"minutes:seconds"``
  - ``"hours:minutes:seconds"``
  - ``"days-hours"``
  - ``"days-hours:minutes"``
  - ``"days-hours:minutes:seconds"``

- ``--checkpoint-dir``: Specifies the directory where checkpoint image files for the batch job will be stored. If not provided, the default is the current working directory. Checkpoint files follow this naming format:
  
  - For full jobs: ``<job_id>.ckpt``
  - For job steps: ``<job_id>.<step_id>.ckpt``

Environment variables can be used in place of the command-line options:

- ``SLURM_CHECKPOINT`` is equivalent to ``--checkpoint``
- ``SLURM_CHECKPOINT_DIR`` is equivalent to ``--checkpoint-dir``

SCONTROL
--------
``scontrol`` is used to initiate checkpoint and restart requests.

Create a Checkpoint
___________________

.. code-block:: bash

   scontrol checkpoint create <jobid> [ImageDir=<dir>] [MaxWait=<seconds>]

- Requests a checkpoint for the specified job.
- If only a job ID is provided, all associated job steps will be checkpointed.
- If the job ID corresponds to a batch job, the entire job is checkpointed. This includes the batch shell and all running tasks from all job steps.
- The task launch command must propagate the checkpoint request to any tasks it initiates.
- ``ImageDir`` specifies the directory where checkpoint image files will be saved. If provided, this overrides any ``--checkpoint-dir`` setting used at job submission.
- ``MaxWait`` sets the maximum duration (in seconds) allowed for the checkpoint operation. If the checkpoint is not completed within this time, the request is considered failed.

.. code-block:: bash

   scontrol checkpoint create <jobid.stepid> [ImageDir=<dir>] [MaxWait=<seconds>]

- Requests a checkpoint for a specific job step only.

Restart from a Checkpoint
_________________________

.. code-block:: bash

   scontrol checkpoint restart <jobid> [ImageDir=<dir>] [StickToNodes]

- Restarts a previously checkpointed batch job.
- ``ImageDir`` specifies the location of the checkpoint image files to restore from.
- ``StickToNodes`` ensures the job restarts on the same nodes it was originally checkpointed on.
