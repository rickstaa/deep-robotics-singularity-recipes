Additional instructions
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

#. Run your container using the ``sudo singularity run --writable <YOUR_CONTAINER_NAME>``
#. Install visual code or visual code-insiders using the following bash commands:

.. code-block:: bash

   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo install -o root -g root -m 644 microsoft.gpg /etc/apt/trusted.gpg.d/
   sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
   sudo apt-get install apt-transport-https
   sudo apt-get update
   sudo apt-get install code # or code-insiders
