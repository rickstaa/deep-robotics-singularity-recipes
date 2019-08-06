.. _doc_dev:

.. _deep_robotics: https://github.com/rickstaa/deep_robotics_singularity_recipes/

Release documentation
===================================

Building
--------------------------
Building `deep_robotics`_ 's documentation requires `sphinx <http://www.sphinx-doc.org/en/master>`_
and a few plugins.

To install the required dependencies, go to the ``panda_autograsp``
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
Release a new version
==================================

Before releasing a new version, you have to bump the version
and update the changelog. This is done using the `bumpversion <https://github.com/peritus/bumpversion>`_ python
package and the `auto-changelog <https://github.com/CookPete/auto-changelog>`_ npm package.
The bumpversion package can be installed using the ``pip install .[dev]``
command inside the main repository folder. The auto-changelog package
installation instructions can be found
`here <https://github.com/CookPete/auto-changelog>`_.

Using these packages, you can release a new version using the
following commands:

.. code-block:: bash

    bumpversion patch
    auto-changelog

.. note:: To be able to run these command you first have to commit all your changes.
