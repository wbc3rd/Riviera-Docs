Open OnDemand
=================

What is Open OnDemand?
----------------------- 
Open OnDemand (OOD) is a web portal for accessing and using Riviera's computing resources. It gives a graphical interface to services that Riviera offers that would otherwise require using command line tools to access.

Accessing Open OnDemand
-----------------------
Open OnDemand is accessed by going to `https://riviera.colostate.edu <https://riviera.colostate.edu>`_ in any browser. When accessing that page, users will first be met by a screen saying that their connection is not secure. This screen occurs because Riviera is currently self signing its HTTPS certificate and can be safely ignored. Past that screen the website will prompt for a username and password, these are the same credentials used when accessing Riviera via SSH.

Using Open OnDemand
------------------- 
Once signed in, users will be met with a landing page and a number of possible navigation items on the top bar, these actions are how a user uses OOD to interact with Riviera. 

Files
^^^^^
The "Files" navigation item leads users to a GUI interface for navigating Riviera's file system. Possible actions from within this GUI include creating new files and directories, uploading files to Riviera, downloading files from Riviera, moving and copying files, and opening a terminal in OOD within the current directory.

Jobs
^^^^
The "Jobs" navigation item gives users access to 3 items, Active Jobs, Job Composer, and Project Manager.

Active Jobs
~~~~~~~~~~~
The "Active Jobs" item leads users to a page that shows all active jobs on riviera as well as some basic information about each job. It also gives users the ability to filter jobs to get more granular information.

Job Composer 
~~~~~~~~~~~~
The OOD Job Composer is where users go to create new slurm jobs to submit onto the cluster. It gives a GUI interface for creating and editing jobs as well as submitting them. 

To create a job a user selects New Job and either creates a job from the default template, a specified template, a specific path on the file system, or an existing job. Once a new job is created users then have the ability to change various basic parameters of the job and edit the submit script called ``main_job.sh`` by default. There is a built-in text editor within OOD that allows for editing of job scripts and any code that a user may want to upload to Riviera for a job to execute. 

Once a job is fully set up and the user is back on the Job Composer main page they can then select their job and click submit to submit it to the job queue. After it has finished executing they can view Folder Contents for their job's main script directory to see any files they set their job up to create. 

Project Manager
~~~~~~~~~~~~~~~
The project manager gives users a persistent workspace for organizing files and work related to a particular project. Within projects there are two main tools for interacting with the compute resources of a cluster, Launchers and Workflows.

Launchers provide a convenient way for users to configure and submit jobs from within an OOD project. Each launcher defines the script to run and also include other parameters required by jobs. Launchers are particularly useful for tasks that need to be run repeatedly or shared as part of a project as a launcher only needs to be configured once before using it to submit new instances of a job as needed. 

Workflows are tools that allow multiple launchers within an OOD project to be organized into a sequence of related jobs. Workflows allow dependencies to be defined between launchers to control when each job runs. Workflows are useful for multi-stage workloads where the output of one job is required by another while keeping each job as a single task that is not requesting more resources than necessary.

Clusters
^^^^^^^^
The "Clusters" navigation item gives users access to the module browser, Riviera Shell Access, and System Status pages.

Module Browser
~~~~~~~~~~~~~~
The Module Browser page is not currently set up but will allow users to view available modules on Riviera.

Riviera Shell Access
~~~~~~~~~~~~~~~~~~~~
Riviera shell access gives users access to a shell within their browser. From that shell they can interact with the cluster exactly how they would if they were accessing Riviera through SSH. 

System Status
~~~~~~~~~~~~~
System status gives an overview of what resources are currently in use on Riviera. It gives node, CPU core, and GPU level insights as well as how many jobs are actively running or queued. 

Interactive Apps
^^^^^^^^^^^^^^^^
The Interactive Apps navigation item gives users access to either a virtual desktop or Jupyter Notebook instance on a development node on Riviera. There are currently two development nodes, one dedicated to development that does not need a GPU called Compute Development and the other dedicated to GPU compute called GPU Development. On GPU Development a user has access to up to 2 A100 GPUs, and on both Compute and GPU Development a user has access to up to 16 CPU cores and up to 64 GB of system memory. 

Interactive apps on Riviera are only designed to be used for development. As such, users are asked to be courteous to the other users on Riviera who may want access to these interactive apps by only requesting the resources required for the task they are performing and by logging off of their instance when not in use. Doing so will allow everyone access to these tools and will keep the wait for resources down. 

Riviera desktop
~~~~~~~~~~~~~~~
Riviera Desktop gives users access to a GUI desktop on Riviera, from which they can perform tasks like they would on any other Linux desktop.

Jupyter Notebook
~~~~~~~~~~~~~~~~
Users are able to launch Jupyter Notebook instances on either development node to have access to some of Riviera's compute resources within the interactive Jupyter Notebook format. Once connected, Jupyter is used just like it is used on a local system within JupyterLab.

My Interactive Sessions
~~~~~~~~~~~~~~~~~~~~~~~
The "My Interactive Sessions" navigation items gives users access to their running interactive sessions and another location to launch the interactive apps from. 
