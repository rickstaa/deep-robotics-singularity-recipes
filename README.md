# Deep Robotics singularity recipe repository

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/2876)

This repository contains the singularity recipes I use for my robotics projects. The recipes in this repository can also be found on [www.singularity-hub.org](https://www.singularity-hub.org)

## Recipe overview
This repository contains both public and private recipe files. The private recipe files can only be built with the right permissions. To obtain the right permissions to a private recipe contact me at [github.com/rickstaa](https://www.github.com/rickstaa).

### Public recipes

- **panda-ros_kinetic-miniconda3-tensorflow_gpu**

#### panda-ros_kinetic-miniconda3-tensorflow_gpu
This recipe sets up a [UBUNTU 16.04 (xenial)](https://wiki.ubuntu.com/XenialXerus) container with the following packages installed in it:

- [Latest stable tensorflow release](https://www.tensorflow.org)
- [Jupyter notebook](https://jupyter.org/)
- [ROS kinetic](https://wiki.ros.org/kinetic)
- [Miniconda3](https://docs.conda.io/en/latest/miniconda.html)
- [conda tensorflow-gpu](https://anaconda.org/anaconda/tensorflow-gpu)
- [libfranka](https://github.com/frankaemika/libfranka)
- [panda_simulation package](https://github.com/rickstaa/panda_simulation)
- [libfreenect2](https://github.com/OpenKinect/libfreenect2)

### Private recipes

#### panda-autograsp-ros_kinetic
This recipe sets up a [UBUNTU 16.04 (xenial)](https://wiki.ubuntu.com/XenialXerus) container with the following packages installed in it:

- [Latest stable tensorflow release](https://www.tensorflow.org)
- [Jupyter notebook](https://jupyter.org/)
- [ROS kinetic](https://wiki.ros.org/kinetic)
- [Miniconda3](https://docs.conda.io/en/latest/miniconda.html)
- [conda tensorflow-gpu](https://anaconda.org/anaconda/tensorflow-gpu)
- [libfranka](https://github.com/frankaemika/libfranka)
- [panda_autograsp package](https://github.com/rickstaa/panda_autograsp_ws)
- [libfreenect2](https://github.com/OpenKinect/libfreenect2)

## How to use

### Singularity installation
Singularity is a free, cross-platform and open-source computer program that performs operating-system-level virtualisation also known as [containerization]https://en.wikipedia.org/wiki/OS-level_virtualisation) One of the main uses of Singularity is to bring containers and reproducibility to scientific computing and the high-performance computing (HPC) world. The Singularity installation instructions can be found in the [the singularity documentation](https://www.sylabs.io/docs/).

### Container build instructions
The containers in this repository can be pulled directly from the [singularity-hub](https://www.singularity-hub.org). To build the container you can, therefore, use the following command.

```
sudo singularity build <CONTAINER_NAME>.simg shub://rickstaa/deep-robotics-singularity-recipes:<RECIPE_NAME>
```

### Container run instructions

After the container is built you can use the singularity `shell`, `start` and `run` commands to interact with the container. You are advised to use the `run` command since this also sources a `.singularity_bashrc` file that is present in each of the containers. This file can be used as a `.bashrc` file. You can run the singularity container using one of the following `run` commands:

- **With Nvidia GPU:** `$ singularity run --nv <YOUR_IMAGE_NAME>`
- **Without Nvidia GPU:** `$ singularity run <YOUR_IMAGE_NAME>`

Additionally, you can also add the `--writable` parameter to the `run command` to receive write permissions.

## Additional documentation

### Add a visual code IDE to the singularity image

Visual studio code can be added to the singularity container in order to enable easy code debugging. This is done as follows:

1. Run the container as a sudo user using the `--writable` tag

```
sudo singularity run --nv --writable <SINGULARITY_CONTAINER>
```

2. Cd to the root folder.

```
cd /
```

3. Download the visual studio code tar.gz

```
curl -L "https://go.microsoft.com/fwlink/?LinkId=723968" > vscode-insiders.tar.gz
tar xzf vscode-stable.tar.gz
```

4. Go into the newly created VSCode-Linux-x64 folder and create a `data` folder.

```
mkdir data
```

5. Now exit the shell and change the container permissions as described below. When the right permissions are set you can run the program using the `/VSCode-Linux-x64/bin/code-insiders` command. This command can also be added as an alias to the `.singularity_bashrc` file which is sourced while loading the container.

### Add the right permissions
If you also want to access the files in the container folder without having to use the root user you can change the `<YOUR_IMAGE_NAME>` folder permissions as follows:

1. Change the group owner to your user group

 ```
 sudo chgrp -R <YOUR_USER_NAME> ./<YOUR_IMAGE_NAME>
 ```

2. Give your user group *read and write* access to the <YOUR_IMAGE_NAME> folder.

```
sudo chmod -R g+rwx  ./<YOUR_IMAGE_NAME>
```

5. If successful the lock above the folder now disappeared.
