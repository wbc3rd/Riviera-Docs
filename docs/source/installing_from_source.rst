Installing Software from Source in Home Directory
=================================================

Many HPC systems do not grant administrative privileges, which means you must install software and any essential packages locally. There are several reliable approaches to set up your personal software environment while ensuring that your workflows remain reproducible and isolated.

Downloading and Installing from Source
--------------------------------------
When installing software from source in your home directory, follow this general pattern to ensure proper orgnaization and functionality.

1. **Create a source directory and navigate to it:**
    
    .. code-block:: bash

        mkdir -p ~/src 
        cd ~/src

2. **Download the source code using wget:**
    
    .. code-block:: bash 

       wget http://example.com/software-1.0.tar.gz

3. **Extract the archive:**

    .. code-block:: bash

        tar -xzf software-1.0.tar.gz 
        cd software-1.0

4. **Configure the installation to your home directory:

    .. code-block:: bash 

        ./configure --prefix=$HOME

5. **Compile and install the software:** 

    .. code-block:: bash 
        
        make 
        make install

6. **Update your PATH** to use the newly installed Python:

    .. code-block:: bash

      export PATH=$HOME/lib/bin:$PATH

Look at installing Python from source to see an example 

Summary
-------
This section outlined strategies for installing software from source on HPC systems without administrative access. By downloading source code with wget, configuring installations to use your home directory, and properly setting up your environment variables, you ensure that your personal computing environment is both flexible and reproducible while maintaining isolation from system-wide installations.


