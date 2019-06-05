# Deep Robotics singularity recipe repository

















the panda_auto_grasp package

[![https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg](https://www.singularity-hub.org/static/img/hosted-singularity--hub-%23e32929.svg)](https://singularity-hub.org/collections/2876)

This repository contains the singularity recipes which can be used to run the [panda_autograsp](https://github.com/rickstaa/panda_autograsp) ROS package. This package adds a nubmer of autonomous robot grasping solutions to the Emika Franka robots. This package can be used to automatically grasp a number of objects using the Emika Franka Panda robot. This can be done both in simulations and on the real robots. Since this package is still under development it is currently set to private. These recipe files in this repository can be used to create a singularity container in which all the packages and libraries that are needed to run the `panda_autograsp` package are set up correctly. This repository currently contains the following recipe files:

- **panda_kinetic_xenial.def**: Recipe file that sets up the right environment and installs the dependencies that are needed to run the [panda_autograsp](https://github.com/rickstaa/panda_autograsp) ROS package. It, however, doesn't install the `panda_autograsp` package itself.
- **panda_autograsp_kinetic.def**: Recipe file that does everything the **panda_kinetic_xenial.def** recipe file does but also installs and builds the [panda_autograsp](https://github.com/rickstaa/panda_autograsp) ROS package.

## How to use

### Singularity installation
Singularity is a free, cross-platform and open-source computer program that performs operating-system-level virtualisation also known as [containerization]https://en.wikipedia.org/wiki/OS-level_virtualisation) One of the main uses of Singularity is to bring containers and reproducibility to scientific computing and the high-performance computing (HPC) world. The Singularity installation instructions can be found in the [the singularity documentation](https://www.sylabs.io/docs/).

### Container build instructions

#### panda_kinetic_xenial.def
This container can be pulled directly from the [singularity-hub](https://www.singularity-hub.org) repository. To build the container you can, therefore, use the following command. 

```
sudo singularity build panda_autograsp_singularity_recipes.simg shub://rickstaa/panda_autograsp_singularity_recipes
```

:warning: Keep in mind that this container doesn't yet contain the `panda_autograsp` repository. When using the **panda_kinetic_xenial.def** recipe you therefore still have to clone and build the [panda_autograsp](https://github.com/rickstaa/panda_autograsp) catkin workspace.

#### panda_autograsp_kinetic.def
As the `panda_autograsp` ROS package is still under development, the **panda_autograsp_kinetic.def** slarity recipe cannot yet be uploaded to the [singularity-hub](https://www.singularity-hub.org). When using the **panda_autograsp_kinetic.def** recipe file you therefore currently have to build the singularity container using the `panda_autograsp_kinetic.def` recipe file present in this repository. To do this follow the steps below:

1. Download the `panda_autograsp_kinetic.def` file and place it in the folder in which you want to build the singularity container.
2. You can build the singularity container using one of the following `build` commands:

    - **Normal singularity container:** `$sudo singularity build <YOUR_IMAGE_NAME> panda_autograsp_kinetic.def`
    - **Development container:** `$sudo singularity build --sandbox <YOUR_IMAGE_NAME> panda_autograsp_kinetic.def`

:warning: As two of the repositories that are contained in this container are private you will be asked for your GitHub credentials two times at the start of the building process.

### Container run instructions

Now the container is built you can use the singularity `shell`, `start` and `run` commands to interact with the container. You are advised to use the `run` command since this also sources the catkin workspace. You can run the singularity container using one of the following `run` commands:

- **With Nvidia GPU:** `$ singularity run --nv <YOUR_IMAGE_NAME>`
- **Without Nvidia GPU:** `$ singularity run <YOUR_IMAGE_NAME>`

Additionally, you can also add the `--writable` parameter to the `run command` to receive write permissions.

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

3. Downoad the visual studio code tar.gz

```
curl -L "https://go.microsoft.com/fwlink/?LinkId=723968" > vscode-insiders.tar.gz
tar xzf vscode-stable.tar.gz
```

4. Go into the newly created VSCode-linux-x64 folder and create a `data` folder.

```
mkdir data
```

5. Now exit the shell and change the container permissions as described below. When the right permissions are set you can run the program using the `/VSCode-linux-x64/bin/code-insiders` command. This command can also be added as a alias to the `.singularity_bashrc` file which is sourced while loading the container.

### Additional permissions
If you also want to access the files in the container folder without having to use the root user you can change the `<YOUR_IMAGE_NAME>` folder permissions as follows:

1. Change the group owner to your user group

 ```
 sudo chgrp <YOUR_USER_NAME> ./<YOUR_IMAGE_NAME>
 ```

2. Give your user group *read and write* access to the <YOUR_IMAGE_NAME> folder.

    ```
    sudo chmod -R g+rwx  ./<YOUR_IMAGE_NAME>
    ```
    
5. If successful the lock above the folder now disappeared.

## Recipe file description

### Panda_kinetic_xenial.def
he container build by this recipe file contains the followin main packages:
- [ROS kinetic](https://wiki.ros.org/kinetic)
- [The libfranka library](https://frankaemika.github.io/docs/libfranka.html)
- Gazebo 7.0.0
- [Libfreenect2 library](https://github.com/OpenKinect/libfreenect2)

### Panda_autograsp_kinetic.def

The container build by this recipe file contains the followin main packages:

- [ROS kinetic](https://wiki.ros.org/kinetic)
- [The libfranka library](https://frankaemika.github.io/docs/libfranka.html)
- Gazebo 7.0.0
- [Libfreenect2 library](https://github.com/OpenKinect/libfreenect2)
- [The Moveit ros kinetic package](https://wiki.ros.org/moveit)
- A modified version of the [franka_ros](https://github.com/rickstaa/franka_ros/tree/0501ab556476bec15a57c739f9403eeac00459e8) ROS package.
- A modified version of the [moveit_tutorials](https://github.com/ros-planning/moveit_tutorials/tree/65af8798d8ad9ac0cc10416f451136b56d910115) ROS package.
- A modified version of the [panda_simulation](https://github.com/rickstaa/panda_simulation/tree/432b97bfdd48df5e180e533786a195900fcf4519) ROS package that was created by [@erdalpekel](https://github.com/erdalpekel/panda_simulation).
- A modified version of the [panda_movit_config](https://github.com/rickstaa/panda_moveit_config/tree/fb18126bda38d47cb30a4c144ead4c02c257914f) ROS package that was also created by [@erdalpekel](https://github.com/erdalpekel/panda_moveit_config).
- The [panda_autograsp](https://github.com/rickstaa/panda_autograsp/tree/fd6901d0cf2fb11556d3560e00224b866d9a4cfc) ROS package that was created by [@me](https://github.com/rickstaa/panda_autograsp/tree/kinetic-devel).
- The [GQCNN](https://github.com/BerkeleyAutomation/gqcnn) [@BerkleyAutomation](https://github.com/BerkeleyAutomation).
- The [autolab_core](https://github.com/rickstaa/autolab_core) [@BerkleyAutomation](https://github.com/BerkeleyAutomation).
- The [perception](https://github.com/rickstaa/perception) [@BerkleyAutomation](https://github.com/BerkeleyAutomation).
