Prohibited Actions
===================

Running Code on the Login node
------------------------------
Running code, including creating virtual environments, compiling, and removing large directories should be run on a compute node and not the login node. These tasks can all instead be ran interactively using the ``srun --pty bash`` command which puts a user in a bash environment on the short-cpu partition. Because storage is served up by NFS on Riviera any changes made in your home directory on any partition will be reflected on the user's home directory in all other partitions as well.

Long Running sInteracting Jobs
------------------------------
If a job is going to take an extended period of time (longer than one hour) to run sbatch should be used instead of sinteractive. This allows Slurm to properly allocate resources with an understanding of program runtimes.

Connecting with an IDE
----------------------
IDEs like VSCode, PyCharm, and others should not be used to connect to Riviera. If a user is not comfortable doing all of their work in the terminal using nano or vim then they can edit their files locally in their IDE of choice and transfer those files back to Riviera with SCP or rsync.

Sensitive Data
--------------
Users should not use Riviera for projects that use sensitive data such as HIPAA or FERPA data. Riviera is not set up in a way that complies with the standards that are required for sensitive data and an alternative should instead be found.

Long Term File storage
----------------------
Riviera is not for long term user file storage. As such, users should not permanently store files in their home directory and should instead transfer files off of Riviera back to their local machines when done with their compute. Users should also not use more than 500 GB of space on their home directory.

Improper Resource Usage
-----------------------
Jobs should not use more resources than required and should use those resources efficiently. Resources should be properly requested within slurm.

Sharing Credentials
-------------------
Users should not share credentials with each other. If a group needs access to Riviera each user should have their own login and a group space can be set up.
