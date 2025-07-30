Frequently Asked Questions
===========================
**How do I request a Riviera account?** 

To request a Riviera account, go to the `Riviera Website <https://www.research.colostate.edu/dsri/hpc-riviera/>`_ and fill out the access survey located at the bottom of the page.
**Who can access the riviera cluster?** 

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

To request interactive time on a compute node, use:  

srun - -pty bash 

This allocates an interactive session on a compute node where you can run commands and programs directly. 
