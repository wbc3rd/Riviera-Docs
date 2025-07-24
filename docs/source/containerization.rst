Containerization
=================

What is a container?
--------------------
A container packages up code, all of its dependencies, and its runtime environment so that it can be run on various machines/environments. This means each container has its own filesystem, libraries, os and environment variables. 

Containers are primarily used to isolate an application, ensure consistent execution across different environments and systems, or to make use of a different operating system. They are analogous to Python Virtual environments, but rather than python-level isolation, containers provide system-level isolation.

Singularity
-----------
`Singularity <https://docs.sylabs.io/guides/3.5/user-guide/introduction.html>`_ is the container system used on HPC Riviera. At a user level it functions similarly to Docker but it does not require root access to run and therefore is much safer to run on a multi user HPC system such as Riviera. Additionally, Singularity functions better with scheduling and resource management systems like Slurm because it does not start up a daemon like Docker does, it instead runs the container processes as child processes allowing Slurm to properly allocate resources to it.

Using Images from Docker Hub
----------------------------
Despite not being docker, Singularity is able to pull images from docker hub and even convert docker images to the Singularity .sif format to run. Pulling images from Docker Hub is the easiest workflow for Singularity. To pull the latest ubuntu image from Docker Hub and then execute a command on it, or run a .sh bash script we do the following: 

.. code-block:: bash

    [username@login001]$ module load slurm
    [username@login001]$ module load singularity
    [username@login001]$ srun --pty bash
    bash-4.4$ singularity pull docker://ubuntu
    bash-4.4$ singularity exec ubuntu_latest.sif <command>
    bash-4.4$ exit

Binding files to a Singularity Image
------------------------------------
Because a container is isolated from the host OS, io and external files are also isolated and must be bound/mounted to the container manually with the --bind flag. When binding files the path to the local files comes before the colon : and the path to the where the files will be bound inside of the container comes after. If multiple files/directories need to be bound they can be separated by a comma, and if the path is the same locally and in the container only one path is necessary.

.. code-block:: bash

    bash-4.4$ singularity exec --bind <local_path>:<target_path> my_container.sif <command>

Building images with Dockerfiles
--------------------------------

A Very Simple Image
^^^^^^^^^^^^^^^^^^^
It is also possible to build our own image with a dockerfile. If we wanted to build a single use dockerfile that always runs the same python file we can.

**Dockerfile**

.. code-block:: dockerfile

    # A base image to build off of, in this case Ubuntu
    FROM ubuntu:latest

    # Sets the working directory inside of the container
    WORKDIR /usr/src/app

    # Copies application files from host to container
    COPY . .

    # Installs dependencies in the container
    RUN apt-get update && apt-get install -y \
        python3 \
        python3-pip

    # Set the default command to execute when the container starts
    CMD ["python3", "test.py"]

**test.py**

.. code-block:: python

    def main():
        print("Hello, Docker!")

    if __name__ == "__main__":
        main()

Now that we have a basic Dockerfile set up we can build the docker image with docker and then save it in a form that Singularity will be able to work with. To do that we need docker running on our local machines, Docker Desktop is the easiest way to have docker running locally. From there we can build the image with docker and then save it as a tar archive, which Singularity will be able to work with to build a compatible image.

.. code-block:: bash

    $ cd BasicImage/
    $ docker build -t basicimage .
    $ docker save basicimage -o basicimage.tar

We now have everything we need to run this docker image with singularity on Riviera, so now all we need to do is transfer our image archive and python script over.

.. code-block:: bash

    $ scp basicimage.tar test.py username@riviera.colostate.edu:~/your_directory

Now that it is transferred over we need to ssh into Riviera and we can run the container with singularity. When running with singularity we first build the image into a .sif file targeting the docker archive .tar file we just transferred over. We can then run the container making sure that the python file is in the current directory.

.. code-block:: bash

    [username@login001]$ cd your_directory/
    [username@login001]$ module load slurm
    [username@login001]$ module load singularity
    [username@login001]$ srun --pty bash
    bash-4.4$ singularity build basicimage.sif docker-archive://basicimage.tar
    bash-4.4$ singularity run basicimage.sif
    Hello, Docker!
    bash-4.4$ exit

A Slightly More Advanced Image
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Here is an example of building a more advanced container for use with PyTorch. This image is notable because we do not specify a a command but instead an entrypoint. This allows us to change what python file we execute with the container.

**Dockerfile**

.. code-block:: dockerfile   

    FROM nvidia/cuda:12.2.2-devel-ubuntu22.04

    # Prevents interactive prompts
    ENV DEBIAN_FRONTEND=noninteractive
    # Install system dependencies
    RUN apt-get update && \
        apt-get install -y \
            git \
            python3-pip \
            python3-dev \
            python3-opencv \
            libglib2.0-0

    COPY . .

    RUN python3 -m pip install -r requirements.txt
    RUN python3 -m pip install --upgrade pip
    RUN pip3 install torch torchvision torchaudio -f https://download.pytorch.org/whl/cu118/torch_stable.html

    # Set the working directory
    WORKDIR /app

    # Set the entrypoint
    ENTRYPOINT [ "python3" ]

Now that we have our dockerfile we can build our pytorch container and transfer it over to Riviera. Due to the size of the base nvidia container and the libraries being installed this will take some time. This can also all be sped up by carefully selecting the files that need to be installed and using a lighter weight image like the rocky linux one from nvidia for cuda.

.. code-block:: bash

    $ cd PyTorch/
    $ docker build -t pytorchimage .
    $ docker save pytorchimage -o pytorchimage.tar
    $ scp pytorchimage.tar your_username@riviera.colostate.edu:~/your_directory

Now that our container archive is transferred over we can build it with singularity. Due to the size of the container building it with singularity will overrun the default tmp directory on Riviera, so we will need to specify a new temp directory to use before building such as ~/tmp.

.. code-block:: bash

    [username@login001]$ mkdir temp_directory
    [username@login001]$ export TMPDIR=~/temp_directory
    [username@login001]$ cd your_directory/
    [username@login001]$ module load slurm
    [username@login001]$ module load singularity
    [username@login001]$ srun --pty bash
    bash-4.4$ singularity build pytorchimage.sif docker-archive://pytorchimage.tar
    bash-4.4$ exit

We have now built our pytorch container with singularity. To run it we need to load our cuda modules and make sure that we tell singularity to use nvidia GPUs with the --nv flag. We also need to make sure to be in a partition with GPUs when we run this container with pytorch. We will also need to pass the container a python file to run. As an example we can run it with a very simple pytorch test file to make sure we see the GPUs properly.

**pytorch-cuda.py**

.. code-block:: python

    import torch
    import torch.nn as nn

    model = nn.Linear(10, 1)
    input_data = torch.rand(100, 10)

    device = torch.device(torch.accelerator.current_accelerator())
    model.to(device)
    input_data = input_data.to(device)

    output = model(input_data)
    print(f"Output tensor device: {output.device}")

.. code-block:: bash

    [username@login001]$ module load cuda12.2/blas
    [username@login001]$ module load cuda12.2/fft
    [username@login001]$ module load cuda12.2/toolkit
    [username@login001]$ srun --pty --partition=short-gpu bash
    bash-4.4$ singularity run --nv pytorchimage.sif pytorch-cuda.py
    Output tensor device: cuda:0
    bash-4.4$ exit
