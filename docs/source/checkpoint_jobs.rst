Checkpointing Jobs
==================

Checkpointing is the process of periodically saving a job’s progress by capturing its current state or key values. This allows a job to resume from the last saved point instead of starting over in the event of an interruption. This is a crucial feature for long-running computational tasks, especially in High-performance Computing(HPC) environments.

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

Quick Start Guide
-----------------

Check if Your Software Already Supports Checkpointing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

- **Machine Leraning:** TensorFlow ``tf.keras.callbacks.ModelCheckpoint``, Pytorch ``torch.save/load``
- **Molecular Dynammics:** GROMACS (``-cpi`` flag), LAMMPS (``restart`` command)
- **Computational Chemistry:** Gaussian (``.chk`` files), NWChem(``restart`` keyword)

Simple Manual Checkpointing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
If your software does not have bult-in checkpointing, here's a minimal example:

.. tabs:: python
    .. code-block:: python
        import pickle
        import os

        def save_checkpoint(data, filename="checkpoint.pkl"):
            """Save current progress"""
            with open(filename + ".tmp", 'wb') as f:
                pickle.dump(data, f)
            os.rename(filename + ".tmp", filename)  
            print(f"Checkpoint saved: {filename}")

        def load_checkpoint(filename="checkpoint.pkl"):
            """Load previous progress"""
            if os.path.exists(filename):
                with open(filename, 'rb') as f:
                    return pickle.load(f)
            return None
        def main():
            # Try to load previous progress
             progress = load_checkpoint()
    
            if progress:
                print("Resuming from checkpoint...")
                start_i = progress['step']
                results = progress['results']
            else:
                print("Starting fresh...")
                start_i = 0
                results = []
    
            # Main computation loop
            for i in range(start_i, 1000):
                result = compute_something(i)
                results.append(result)
        
            # Save checkpoint every 100 steps
            if i % 100 == 0:
                checkpoint_data = {
                    'step': i + 1,
                    'results': results
                }
                save_checkpoint(checkpoint_data)

        def compute_something(i):
            # Your actual computation
            return i ** 2

SLURM job Script with Checkpointing
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. tabs:: python
    .. code-block:: python
        #!/bin/bash
        #SBATCH --job-name=my_checkpointed_job
        #SBATCH --time=02:00:00
        #SBATCH --mem=4GB
        #SBATCH --output=job_%j.out

        # Load any modules you need
        module load python/3.8

        # Run your checkpointed program
        python my_checkpointed_program.py

        # Check if job finished or was interrupted
        if [ $? -eq 0 ]; then
            echo "Job completed successfully"
        else
            echo "Job was interrupted - checkpoint should allow restart"