.. _dependency-management:

Dependency management
---------------------

-  Be sure to specify versions like ``^1.0.0`` and not ``~1.1.3``
-  If depending on master, spell it out

    ``org/package#master`` instead of ``org/package``, ``org/package#\*`` or ``org/package#``

-  If you have specifically tested with version 1.2.3, write ``^1.2.3`` to document that, even if ``^1.0.0`` will install the same version
-  Any public components/repos can only depend on publically available
   components

Installing/updating component dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  Make sure to install all dependencies for the *actual component(s)* in the repo, do not confuse with :ref:`github-demo-dev-dependencies`.

-  Make sure to remove any dependencies not needed
-  Install new dependencies with ``bower install --save org/package#^v1.0.0``

-  Run ``bower update`` periodically to update the dependencies to the latest version

.. todo:: yarn


.. _github-demo-dev-dependencies:

Installing demo/dev dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any components/dependencies only needed for demo/dev, follow the
above but install with ``bower install --save-dev org/package#^v1.0.0``

Bower link
~~~~~~~~~~

If developing two components that depend on each other, to avoid pushing
commits and running bower update all the time, use ``bower link``.

.. todo:: use yarn link

Example
^^^^^^^

:ref:`cosmoz-omnitable` depends on :ref:`cosmoz-autocomplete` for filtering, but
:ref:`cosmoz-autocomplete` property change notification somehow doesn’t work in
that context and needs to be tested, debugged and fixed with both
components in parallel::

    $ cd cosmoz-autocomplete
    $ bower link
    $ cd ../cosmoz-omnitable
    $ bower link cosmoz-autocomplete

Now the ``cosmoz-omnitable/bower_components/cosmoz-autocomplete`` will be
linked to the local :ref:`cosmoz-autocomplete` repo, causing any changes to be
available in :ref:`cosmoz-omnitable` instantly.

.. note::

    This will cause the linked component to not update with ``bower update``,
    instead a ``git pull`` is needed in that repo.

    When a link is no longer needed, you should therefore ``bower uninstall
    <dependency-package>`` before running ``bower update`` to make sure all
    dependencies are updated properly.