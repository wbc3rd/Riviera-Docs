SBATCH Directives
=================

Here are some common SBATCH directives seen on Riviera:

``--job-name=<name>`` 
    Sets the name of a job which can allow for finding the job in a queue.
``--output=<path>`` 
    Sets the file path for the standard output stream so a user can access the data printed to it once the job has completed.
``--error=<path>`` 
    Sets the file path for the standard error stream so a user can access the data printed to it once the job has completed.
``--partition=<partition>`` 
    Informs Slurm that the job needs to execute on a particular partition. The default partition for this on Riviera is ``short-cpu``.
``--time=<time>`` 
    Sets the maximum runtime for a job. The possible acceptable formats for time are "minutes", "minutes:seconds", "hours:minutes:seconds", "days-hours", "days-hours:minutes", and "days-hours:minutes:seconds".
``--ntasks=<number>`` 
    Sets the maximum number of tasks that each step of the job will take. The default is one per node, but ``--cpus-per-task`` will change the default.
``--cpus-per-task=<number>`` 
    Informs Slurm that each task will require _number_ of CPUS per task. Otherwise Slurm will just try to assign one CPU to each task.
``--array=<indices>``
    Submits a job array, which is multiple instances of the same job without a need to communicate between the jobs. For more on how to set up job arrays see `Job Arrays in SBATCH Use Cases <https://riviera-docs.readthedocs.io/en/latest/sbatch_use_cases.html>`_.
``--mem=<size>``
    Specifies the memory requirement per node. By default the units are in megabytes, but different units can be specified using the suffix [K\|M\|G\|T]. ``--mem`` is mutually exclusive with ``--mem-per-cpu`` and ``--mem-per-gpu``.
``--mem-per-cpu=<size>``
    Specifies the memory requirement per usable allocated CPU. By default the units are in megabytes, but different units can be specified using the suffix [K\|M\|G\|T]. ``--mem-per-cpu`` is mutually exclusive with ``--mem`` and ``--mem-per-gpu``.
``--mem-per-gpu=<size>``
    Specifies the memory requirement per usable allocated CPU. By default the units are in megabytes, but different units can be specified using the suffix [K\|M\|G\|T]. ``--mem-per-gpu`` is mutually exclusive with ``--mem`` and ``--mem-per-cpu``.
``--nodes=<minnodes>[-maxnodes]``
    Requests that a minimum number of _minnodes_ be allocated to the job. A maximum node count may also be specified with _maxnodes_. IF only one number is supplied this is taken as both the minimum and maximum. 

For more SBATCH directives see the `Official Slurm documentation <https://slurm.schedmd.com/sbatch.html>`_.`