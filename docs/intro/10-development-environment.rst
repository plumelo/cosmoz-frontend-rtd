Development Environment
-----------------------

`Visual Studio Code (vscode) <https://code.visualstudio.com/>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A code editor developed by Microsoft, freely available to download and use, even in Linux OS:es.

`Extensions to vscode <https://marketplace.visualstudio.com/>`_

Follow the installation instructions for each of them below to install them in vscode.

* `ESLint <https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint>`_ - Integrates ESLint into VS Code
         
* `polymer-ide <https://marketplace.visualstudio.com/items?itemName=polymer.polymer-ide>`_ - Provides linting, autocompletion, and more for web components

`NodeJS <https://nodejs.org/en/download/>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Note to Debian and other similar Linux based OS developers: the NodeJS version in the OS repos are outdated
(for Debian Stable anyway…). Follow the instructions at https://nodejs.org/en/download/package-manager/
to get an updated version of NodeJS.

NPM install of Gulp (web server), bower (package manager), Polymer (library)::

    $ sudo npm install -g gulp bower polymer-cli

.. todo:: Replace bower with yarn

.. todo:: Drop dependency for ``gulp``, use ``polymer build`` / ``polymer serve``


.. _git-setup:

`Git <https://git-scm.com/downloads>`_
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Debian/Ubuntu::

    $ sudo apt-get install git

Time
~~~~

Make sure the time is correctly set on your computer as it is used when committing and it will be noted in git log.

Debian/Ubuntu::

    $ sudo apt-get install ntp
    $ sudo ntpq -p