Installing Python and Packages
==============================

Many HPC systems do not grant administrative privileges, which means you must install Python and any essential packages locally. There are several reliable approaches to set up your personal Python environment while ensuring that your workflows remain reproducible and isolated.

Using a Virtual Environment
-----------------------------
A virtual environment creates a self-contained directory that includes its own copy of the Python interpreter and all necessary packages. This method is highly recommended because it does not interfere with the system-wide Python installation and keeps dependencies organized.

1. **Create the virtual environment**:
   
   .. code-block:: bash

      python3 -m venv myenv

2. **Activate the environment**:

   .. code-block:: bash

      source myenv/bin/activate

3. **Install the required packages**:

   .. code-block:: bash

      pip install numpy pandas scikit-learn

4. **Deactivate the environment** when done:

   .. code-block:: bash

      deactivate

Using pip with the ``--user`` Option
--------------------------------------
If you prefer not to use a virtual environment, you can install Python packages into your user directory using the ``--user`` flag. This method installs packages in a directory (typically ``~/.local/lib`` and executables in ``~/.local/bin``) that does not require administrative access.

For example:

.. code-block:: bash

   pip install --user numpy pandas scikit-learn

Make sure the user-level binary directory is in your ``PATH`` by adding the following line to your shell configuration file (e.g., ``.bashrc`` or ``.zshrc``):

.. code-block:: bash

   export PATH=$HOME/.local/bin:$PATH

Installing Python from Source (if Necessary)
---------------------------------------------
If the Python version available on your system does not meet your requirements, you can compile Python from source and install it in your home directory.

1. **Download and extract the source code**:

   .. code-block:: bash

      wget https://www.python.org/ftp/python/3.9.7/Python-3.9.7.tgz
      tar -xf Python-3.9.7.tgz
      cd Python-3.9.7

2. **Configure the installation to a custom local directory**:

   .. code-block:: bash

      ./configure --prefix=$HOME/python3.9

3. **Compile and install Python**:

   .. code-block:: bash

      make
      make install

4. **Update your PATH** to use the newly installed Python:

   .. code-block:: bash

      export PATH=$HOME/python3.9/bin:$PATH

By installing Python locally—either through virtual environments, the ``--user`` flag, or from source—you gain full control of your software stack without interfering with the system setup. This approach not only maximizes resource efficiency but also ensures that your projects can manage their dependencies independently.

Summary
-------
This section outlined several strategies for installing Python and packages on an HPC system without administrative access. By using virtual environments, pip's ``--user`` installation, or compiling Python from source, you ensure that your personal computing environment is both flexible and reproducible.