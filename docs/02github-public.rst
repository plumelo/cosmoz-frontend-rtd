Public Cosmoz elements on GitHub
================================

Creating a repository
---------------------

Be sure to create it under the https://github.com/Neovici organization

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

-  Make sure to install all dependencies for the *actual component(s)* in the repo

   Not demo/dev dependencies, see :ref:`github-demo-dev-dependencies`.

-  Make sure to remove any dependencies not needed
-  Install new dependencies with ``bower install --save org/package#^v1.0.0``

-  Run ``bower update`` periodically to update the dependencies to the latest version


.. _github-demo-dev-dependencies:

Installing demo/dev dependencies
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For any components/dependencies only needed for demo/dev, follow the
above but install with ``bower install --save-dev org/package#^v1.0.0``

Bower link
~~~~~~~~~~

If developing two components that depend on each other, to avoid pushing
commits and running bower update all the time, use ``bower link``.

Example
^^^^^^^

cosmoz-omnitable depends on cosmoz-autocomplete for filtering, but
cosmoz-autocomplete property change notification somehow doesn’t work in
that context and needs to be tested, debugged and fixed with both
components in parallel::

    $ cd cosmoz-autocomplete
    $ bower link
    $ cd ../cosmoz-omnitable
    $ bower link cosmoz-autocomplete

Now the ``cosmoz-omnitable/bower_components/cosmoz-autocomplete`` will be
linked to the local cosmoz-autocomplete repo, causing any changes to be
available in cosmoz-omnitable instantly.

.. note::

    This will cause the linked component to not update with ``bower update``,
    instead a ``git pull`` is needed in that repo.

    When a link is no longer needed, you should therefore ``bower uninstall
    <dependency-package>`` before running ``bower update`` to make sure all
    dependencies are updated properly.

Development
-----------

Run ``polymer serve`` in the component directory to serve up that component in a small web server locally.

Testing
-------

https://www.polymer-project.org/1.0/tools/tests.html

.. todo:: Document how we approach testing

WCT
~~~

Web component tester

https://github.com/Polymer/web-component-tester

.. todo:: Document

WCT-Sauce
~~~~~~~~~

Sauce Labs support for web-component-tester

https://github.com/Polymer/wct-sauce

.. todo:: Document

Documentation
-------------

See official Polymer documentation for guidelines on how to document methods, properties, etc: https://www.polymer-project.org/1.0/tools/documentation.html

.. todo:: Add info on documentation, see :ref:`webcomponents-org`.

Git
---

.. seealso::

    :ref:`git-setup`

.. todo:: GitHub 2FA setup

    https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/

.. todo:: ``.netrc`` config

Travis-CI
---------

.. todo:: Document

    https://youtu.be/afy_EEq_4Go

    https://www.jamiestarke.com/2015/06/10/continuous-integration-polymer-web-component-tester-travis-ci/

To enable integration setup::

    $ sudo apt install ruby ruby-dev
    $ sudo gem install travis

Integrations
------------

Travis-CI + Slack
~~~~~~~~~~~~~~~~~

In the repo, run::

    $ travis encrypt "<1password-devops-password>" --add notifications.slack

.. note::
    Make sure that the organisation is ``Neovici`` and not ``neovici`` (case
    insensitive!) for the repo slug (the URL-friendly name of the repository).

GitHub + Slack
~~~~~~~~~~~~~~

Adjust GitHub integration, add repo


.. _webcomponents-org:

Webcomponents.org
-----------------

.. todo:: Apache 2.0 license

.. todo:: Inline-demo

.. todo:: Docs