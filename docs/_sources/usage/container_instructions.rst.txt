Container build instructions
==================================

The containers in this repository can be pulled directly from
the `singularity-hub <https://www.singularity-hub.org>`_ container
registry as follows:

.. code-block:: bash

    build <CONTAINER_NAME>.simg shub://rickstaa/panda_autograsp:ros-kinetic-cuda10-xenial

It can also be built from the recipe file using the following command:

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
You are advised to use the ``run`` command since this also sources
a ``.singularity_bashrc`` file that is present in each of the containers.
This file can be used as a ``.bashrc`` file. You can run the singularity
container using one of the following ``run`` commands:

- **With Nvidia GPU:** ``$ singularity run --nv <YOUR_CONTAINER_NAME>``
- **Without Nvidia GPU:** ``$ singularity run <YOUR_CONTAINER_NAME>``

.. note:: Additionally, you can also add the ``--writable`` parameter to the ``run command`` to receive write permissions.
