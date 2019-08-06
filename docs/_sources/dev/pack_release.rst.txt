.. _pack_release:

Release package
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

    $ bumpversion patch
    $ auto-changelog

.. note:: To be able to run these command you first have to commit all your changes.
