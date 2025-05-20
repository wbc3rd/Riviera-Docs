Data Transfer and File Management
=====================================

Working efficiently with data on an HPC system not only streamlines your workflow but also ensures that you remain within your allocated storage quotas. Many HPC environments separate long-term home storage from fast, temporary scratch storage. Understanding this structure will help you manage large datasets and avoid clutter in your home directory.

Using SCP for File Transfers
-----------------------------
Secure Copy (SCP) is a command-line utility that leverages SSH to transfer files between your local machine and the HPC system. For example, to copy a file from your local system to the HPC:

.. code-block:: bash

   scp /path/to/local/file.txt username@hpc.cluster:/path/to/destination/

Similarly, to retrieve a file from the system:

.. code-block:: bash

   scp username@hpc.cluster:/path/to/file.txt /path/to/local/destination/

Using rsync for Efficient Synchronization
-------------------------------------------
When dealing with large directories or when you need to update files incrementally, ``rsync`` is an excellent tool. It transfers only the differences between the source and the destination, making the process faster and reducing bandwidth usage. For instance:

.. code-block:: bash

   rsync -avh /path/to/local/directory/ username@hpc.cluster:/path/to/destination/

This command preserves file permissions and provides detailed output during transfer. Adjust the options as needed to suit your workflow.

Using SFTP for Interactive Transfers
--------------------------------------
If you prefer an interactive session to manage files, the SFTP (Secure File Transfer Protocol) client is a viable option. To initiate an SFTP session, run:

.. code-block:: bash

   sftp username@hpc.cluster

Once connected, you can use commands such as ``get``, ``put``, ``ls``, and ``cd`` to navigate the directories and transfer files. Type ``help`` at the SFTP prompt to see a list of available commands.

Managing Your Storage
---------------------
HPC systems often provide distinguished spaces such as a home directory for permanent storage and a scratch directory for temporary or large data files. The home directory usually comes with storage quotas, so it is best practice to utilize the scratch space for large datasets, intermediate results, or temporary files. Always refer to your system's documentation regarding file storage policies, cleanup procedures, and backup recommendations to ensure efficient use of the available resources.

**Additional Resources**
-------------------------
For a demonstration of creating and running a SLURM script, check out the `YouTube tutorial on SLURM scripts <https://youtu.be/F03HWqmFbK4?si=jXWDhgM2Wy8I7cpN>`_.
Summary
-------
This section has guided you through the essential tools for data transfer—namely SCP, rsync, and SFTP—and provided insights on managing storage on an HPC system. Efficient file management keeps your projects organized, ensures optimal performance, and helps maintain a fair computing environment for all users.