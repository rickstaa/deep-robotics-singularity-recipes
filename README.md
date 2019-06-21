# Deep Robotics singularity recipe repository (v0.0.5)

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/3134)


This repository contains the singularity recipes I use for my robotics projects. The recipes in this repository can also be found on [www.singularity-hub.org](https://www.singularity-hub.org)

## Recipe overview
This repository contains both public and private recipe files. The private recipe files can only be built with the right permissions. To obtain the right permissions to a private recipe contact me at [github.com/rickstaa](https://www.github.com/rickstaa).

### Public recipes

- **tensorflow-gpu-miniconda3-ros_kinetic-xenial.def**
- **panda-tensorflow-gpu-miniconda3-ros_kinetic-xenial.def**


#### tensorflow-gpu-miniconda3-ros_kinetic-xenial.def

- [Latest stable tensorflow release](https://www.tensorflow.org)
- [Jupyter notebook](https://jupyter.org/)
- [ROS kinetic](https://wiki.ros.org/kinetic)
- [Miniconda3](https://docs.conda.io/en/latest/miniconda.html)
- [conda tensorflow-gpu](https://anaconda.org/anaconda/tensorflow-gpu)

#### panda-tensorflow-gpu-miniconda3-ros_kinetic-xenial.def
This recipe sets up a [UBUNTU 16.04 (xenial)](https://wiki.ubuntu.com/XenialXerus) container with the following packages installed in it:

- [Latest stable tensorflow release](https://www.tensorflow.org)
- [Jupyter notebook](https://jupyter.org/)
- [ROS kinetic](https://wiki.ros.org/kinetic)
- [Miniconda3](https://docs.conda.io/en/latest/miniconda.html)
- [conda tensorflow-gpu](https://anaconda.org/anaconda/tensorflow-gpu)
- [libfranka](https://github.com/frankaemika/libfranka)
- [panda_simulation package](https://github.com/rickstaa/panda_simulation)

### Private recipes

#### panda-autograsp-tensorflow-gpu-miniconda3-ros_kinetic-xenial
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
Singularity is a free, cross-platform and open-source computer program that performs operating-system-level virtualisation also known as [containerization](https://en.wikipedia.org/wiki/OS-level_virtualisation) One of the main uses of Singularity is to bring containers and reproducibility to scientific computing and the high-performance computing (HPC) world. The Singularity installation instructions can be found in the [the singularity documentation](https://www.sylabs.io/docs/).

### Container build instructions
The containers in this repository can be pulled directly from the [singularity-hub](https://www.singularity-hub.org). To build the container you can, therefore, use the following command.

```
sudo singularity build <CONTAINER_NAME>.simg shub://rickstaa/deep-robotics-singularity-recipes:<RECIPE_NAME>
```

### Container run instructions

After the container is built you can use the singularity `shell`, `start` and `run` commands to interact with the container. You are advised to use the `run` command since this also sources a `.singularity_bashrc` file that is present in each of the containers. This file can be used as a `.bashrc` file. You can run the singularity container using one of the following `run` commands:

- **With Nvidia GPU:** `$ singularity run --nv <YOUR_CONTAINER_NAME>`
- **Without Nvidia GPU:** `$ singularity run <YOUR_CONTAINER_NAME>`

Additionally, you can also add the `--writable` parameter to the `run command` to receive write permissions.

### Tensorflow-gpu use instructions
The tensorflow-gpu package is present in the `tf-gpu` conda enviroment. This enviroment can be loaded running the `conda activate tf-gpu` command.

## Additional documentation

### Add a visual code IDE to the singularity container

Visual studio code can be added to the singularity container in order to enable easy code debugging. This is done as follows:

1. Run your container using the `sudo singularity run --writable <YOUR_CONTAINER_NAME>`
2. Install visual code or visual code-insiders using the following bash commands:

```
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install code # or code-insiders
```

3. Bind the /run directory to use visual code from within the container this can be done by running the singularity containg with the `sudo singularity run -B /run --writable <YOUR_CONTAINER_NAME>` command.

### Add the right permissions
If you also want to access the files in the container folder without having to use the root user you can change the `<YOUR_CONTAINER_NAME>` folder permissions as follows:

1. Change the group owner to your user group

 ```
 sudo chgrp -R <YOUR_USER_NAME> ./<YOUR_CONTAINER_NAME>
 ```

2. Give your user group *read and write* access to the <YOUR_CONTAINER_NAME> folder.

```
sudo chmod -R g+rwx  ./<YOUR_CONTAINER_NAME>
```

5. If successful the lock above the folder now disappeared.
