Installing R and Libraries
==========================

Using Conda to Install R
------------------------

An Anaconda virtual environment should be used to install R on Riviera. If Anaconda has not been installed yet a user can `follow the instructions to install it <https://riviera-docs.readthedocs.io/en/latest/setting_up_anaconda.html#installing-anaconda>`_.

Once Anaconda has been installed, a new virtual environment needs to be created with r installed in it and then activated.

.. code-block:: bash

  conda create --name r-env r-base r-essentials 

  conda activate r-env

Now a conda environment with R installed is available. More R packages are available to be installed with conda, with a full list of available packages `here <https://repo.anaconda.com/pkgs/r/>`_. The packages can be installed in an environment with:

.. code-block:: bash

  conda install package_name

Finally, conda can be deactivated with:

.. code-block:: bash
   
  conda deactivate


