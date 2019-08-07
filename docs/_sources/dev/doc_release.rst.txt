.. _doc_release:

.. _deep_robotics: https://github.com/rickstaa/deep_robotics_singularity_recipes/

Release documentation
===================================

Building
--------------------------
Building `deep_robotics`_ 's documentation requires `sphinx <http://www.sphinx-doc.org/en/master>`_
and a few plugins.

To install the required dependencies, go to the ``deep_robotics_singularity_recipes``
directory and run ::

    $ pip install .[docs]

Then, go to the ``docsrc`` directory and run ``make html``
to build the documentation. This command will generate
a set of web pages inside the ``docsrc/_build`` directory.

Deploying
---------------------------
To deploy documentation to the Github Pages site for the repository,
simply run the ``make gh-pages`` command inside the ``panda_autograsp/docsrc``
directory.
