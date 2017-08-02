.. _public-github:

Public elements
===============

Hosted on `GitHub <https://github.com>`_

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


.. _github-readme:

README.md 
~~~~~~~~~

Badges
^^^^^^

Travis-CI::

    [![Build Status](https://travis-ci.org/Neovici/cosmoz-bottom-bar.svg?branch=master)](https://travis-ci.org/Neovici/cosmoz-bottom-bar)

Webcomponents.org::

    [![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/Neovici/cosmoz-bottom-bar)

.. note:: Badge URLs needs to be adjusted for the relevant repo.

Inline demo
^^^^^^^^^^^

For :ref:`webcomponents-org`

.. _github-license:

License
~~~~~~~

Open Source Cosmoz components use the Apache-2.0 license.

This should be set/present in:

* ``bower.json``
* ``package.json``

Also, a ``LICENSE`` file containing the Apache 2.0 License should be present in the repository root.

Finally, all applicable files should have the following notice enclosed in the appropriate comment syntax for the file format::

    Copyright 2017 Neovici

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

        http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

.. _github-git:

Git
---

Submitting changes
~~~~~~~~~~~~~~~~~~

Use `whatever model <https://help.github.com/articles/about-collaborative-development-models/>`_ you have access to and
feel comfortable with, but make sure to use a `Pull Request <https://help.github.com/articles/about-pull-requests/>`_
approach unless otherwise instructed.

GitHub 2FA setup
~~~~~~~~~~~~~~~~

Be sure to activate two-factor authentication for GitHub:

    https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/

.netrc
~~~~~~

To avoid entering password when pushing to GitHub, use a `.netrc` file.

Set it up with GPG encryption:

    https://bryanwweber.com/writing/personal/2016/01/01/how-to-set-up-an-encrypted-.netrc-file-with-gpg-for-github-2fa-access/

.. seealso::

    :ref:`git-setup`

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

Adjust GitHub integration at https://neovici.slack.com/apps/manage, add repo


.. _cosmoz-elements:

`cosmoz-elements <https://github.com/Neovici/cosmoz-elements>`_
---------------------------------------------------------------

.. todo:: publish

.. _webcomponents-org:

`Webcomponents.org <https://webcomponents.org>`_
------------------------------------------------

All components should aspire to be published at https://webcomponents.org.

See requirements for publishing at https://www.webcomponents.org/publish.

* Configure :ref:`github-license`

* Create a `tagged release <https://help.github.com/articles/about-releases/>`_

* Update the :ref:`github-readme`

Webcomponents.org acts as a way to show-case our components but also maintain updated docs.