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
