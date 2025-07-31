Frequently Asked Questions
===========================
.. toggle::
    **Q: How do I request a Riviera account?** 
    
    To request a Riviera account, go to the `Riviera Website <https://www.research.colostate.edu/dsri/hpc-riviera/>`_ and fill out the access survey located at the bottom of the page.
    
    **Who can access the Riviera cluster?** 
    
    Access to Riviera is open to all Colorado State University (CSU) researchers and students. Whether you’re a faculty member leading a large research project, a graduate student developing machine learning models, or an undergraduate student exploring data science, you are eligible to use the Riviera cluster. This is provided that your work aligns with academic or research objectives. Access is managed by the Data Science Research Institute and must agree to the HPC usage policies. 
    
    **What compute resources does Riviera offer?**
    
    Riviera provides state-of-the-art computational capabilities tailored to the needs of modern research, particularly in AI and bioinformatics. Key hardware resources include:  
    
    - GPU Compute Nodes with 2x AMD EPYC 7763 64-Core processors and 4x NVIDIA A100 80GB per node with 500GB of memory available per node optimized for AI/ML workflows, deep learning training, and accelerated computing. 
    - CPU Compute Nodes with 2x AMD EPYC 7763 64-Core processors with 500GB of memory available per node. 
    - High-Memory CPU Compute Nodes with 2x AMD EPYC 7763 64-Core CPUs with hyperthreading enabled and 2TB of memory available per node for memory-intensive tasks such as genome assembly, large-scale simulations, or in-memory data processing. 
    - 35 total nodes.  
    - 2944 total CPU cores. 
    - 3PB of total storage. 

**How do I cite Riviera?** 

If you are using or have used Riviera as part of published work, special talk, or other publishing materials, please acknowledge Riviera support in your research. This will help us to continue to support CSU research as well as highlight work done on the HPC. Here are a couple of example citations: 

“This work was supported in part by Colorado State University through high-performance computer time and resources provided by the Data Science Research Institute.”  

“Portions of this work were performed on the Colorado State University Data Science Research Institute high performance computer Riviera.” 

**How can I request troubleshooting help or schedule a HPC consultation?**

If you need assistance, you can take advantage of a few support options. Contact dsri_riviera_help@colostate.edu for support and troubleshooting about the Riviera cluster. You can request an HPC consultation by `filling out the form <https://www.research.colostate.edu/dsri/hpc-riviera/>`_ to discuss your project needs, optimize performance, or plan resource allocations. Riviera is supported by a Documentation Website that provides quick-start guides, SBATCH script examples, software module help, and have useful links to the `DSRI YouTube channel <https://www.youtube.com/@DataScienceResearchInstitute>`_ for more information about the Riviera cluster. 

**How much data can I store in my home directory?**

Riviera supports up to 500GB of storage in your home directory. Please contact dsri_riviera_help@colostate.edu for more information or concerns. 

**How do I request interactive time?**

See `Running Interactively <https://riviera-docs.readthedocs.io/en/latest/slurm.html#running-interactively>`_ in the `Slurm Overview <https://riviera-docs.readthedocs.io/en/latest/slurm.html#>`_ for information on running interactively.

**How can I transfer data from my local computer to the cluster?** 

See `Data Transfer and File Management <https://riviera-docs.readthedocs.io/en/latest/data_transfer.html>`_ for information on how to transfer data on and off of the cluster.

**How do I access scratch space on the riviera cluster?**

It is possible to view the available file systems and storage capacities by running ``df -h`` while running interactively on the node you want to use. From there you can transfer data to the local scratch space (``/local``) on the node you are using with the ``mv`` or ``cp`` commands and direct your programs to use those directories for file storage.

**How do I install Miniconda?**

Download miniconda using wget to download Miniconda installer from the Anaconda repository: 

.. code-block:: bash

  wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh 

Make the installer executable: 

.. code-block:: bash

  chmod u+x Miniconda3-latest-Linux-x86_64.sh 

Run it: 

.. code-block:: bash

  ./Miniconda3-latest-Linux-x86_64.sh 

Follow the installation prompts: 

- Press Enter to continue with installation 
- Scroll through and accept the license terms 
- Confirm the installation location (default: /nfs/home/username/miniconda3) 
- Say yes when asked to initialize conda in your shell profile 

Activate conda: 

.. code-block:: bash

  source ~/.bashrc 

You should now see (base) in your command prompt, indicating conda is active. 
