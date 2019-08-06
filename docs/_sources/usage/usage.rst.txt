.. _usage:

Container build instructions
==================================

The containers in this repository can be pulled directly from
the `singularity-hub <https://www.singularity-hub.org>`_ container
registry as follows:

.. code-block:: bash

	build <CONTAINER_NAME>.simg shub://rickstaa/panda_autograsp:ros-kinetic-cuda10-xenial

It can also be build from the recipe file using the following command:

.. code-block:: bash

	sudo singularity <CONTAINER_NAME>.simg shub://rickstaa/panda_autograsp:ros-kinetic-cuda10-xenial

You can also add the ``--sandbox`` argument to build the container
as a writeable folder.

.. warning:: You need root access to build from a recipe file.

Container use instructions
==================================

Run instructions
---------------------------

After the container is built, you can use the singularity ``shell``,
``start`` and ``run`` commands to interact with the container.
You are advised to use the `run` command since this also sources
a ``.singularity_bashrc`` file that is present in each of the containers.
This file can be used as a ``.bashrc`` file. You can run the singularity
container using one of the following `run` commands:

- **With Nvidia GPU:** ``$ singularity run --nv <YOUR_CONTAINER_NAME>``
- **Without Nvidia GPU:** ``$ singularity run <YOUR_CONTAINER_NAME>``

.. note:: Additionally, you can also add the ``--writable`` parameter to the ``run command`` to receive write permissions.

Additional settings and configuration
===========================================

Add additional permissions
--------------------------------

If you did build the singularity container as a writable folder
you can give your user write and read access from outside the singularity
container by:

#. Changing the group owner to your user group.

.. code-block:: bash

	sudo chgrp -R <YOUR_USER_NAME> ./<YOUR_CONTAINER_NAME>

#. Giving your user group _read and write\_ access to the ``<YOUR_CONTAINER_NAME`` folder.

.. code-block:: bash

	sudo chmod -R g+rwx ./<YOUR_CONTAINER_NAME>

Add a visual code IDE to the singularity container
------------------------------------------------------------

Visual studio code can be added to the singularity container in order to enable
easy code debugging. This is done as follows:

#. Run your container using the `sudo singularity run --writable <YOUR_CONTAINER_NAME>`
#. Install visual code or visual code-insiders using the following bash commands:

.. code-block:: bash

	curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
 	sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
 	sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
 	sudo apt-get install apt-transport-https
 	sudo apt-get update
 	sudo apt-get install code # or code-insiders
