Development environment
=======================

The frontend development environment consists of various parts of software
working together.

Various operating systems are supported - Debian, Ubuntu and Windows. The
used software is free of charge and it's possible to locally run only open
source software if you like to.

Things marked with an asterisk (*) are required.

Google Chrome / Chromium *
--------------------------

Google Chrome is the target web
browser, but Chromium works just as good as an open source alternative.

Google Chrome *
~~~~~~~~~~~~~~~

Debian / Ubuntu / Windows:
    Get it from the official `Google Chrome download page <https://www.google.se/chrome/>`_ and install it.

Chromium *
~~~~~~~~~~

Debian/Ubuntu:
    ``$ sudo apt-get install chromium``

Windows:
    Get it from the `Chromium download page <https://chromium.woolyss.com/download/>`_ and install it.

.. _vscode:

`Visual Studio Code (vscode) <https://code.visualstudio.com/>`_ with `extensions <https://marketplace.visualstudio.com/>`_ *
----------------------------------------------------------------------------------------------------------------------------

A code editor developed by Microsoft for most common platforms, even in Linux
based operating systems, enhanced by some required extensions.

Follow the installation instructions for the editor itself and the extensions
in the links below to get them too.

Debian / Ubuntu / Windows:
    * `Visual Studio Code <https://code.visualstudio.com/>`_ * - The editor itself

    * `ESLint <https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint>`_ * - Integrates ESLint into VS Code

    * `polymer-ide <https://marketplace.visualstudio.com/items?itemName=polymer.polymer-ide>`_ * - Provides linting, autocompletion, and more for web components

    * `Marketplace <https://marketplace.visualstudio.com/>`_ - For the inspired to find more extensions

`NodeJS <https://nodejs.org/en/download/>`_ *
---------------------------------------------

An open source server framework running on JavaScript, It runs the frontend and
comes with the NPM package manager used to install additional required packages.

Version 8 and above of NodeJS is required.

Debian / Ubuntu:
    .. note::
        Debian and other similar Linux based operating system developers: the
        NodeJS version in the OS repository is outdated (for Debian Stable at
        least).

    Follow the instructions on the `Installing Node.js via package manager <https://nodejs.org/en/download/package-manager/>`_ page to get an updated version of NodeJS.

Windows:
    Download the installer from the official `NodeJS download page <https://nodejs.org/en/download/>`_ and and run it.

.. _yarn-setup:

NPM *
-------

NPM is the package manager for JavaScript and the world’s largest software registry.
Because ``yarn`` is used as the main package manager but we need a ``package-lock.json`` file for analysis and audit
we create that file by using a package.json script:
    ``"sync-npm": "rm -f package-lock.json && npm shrinkwrap && mv npm-shrinkwrap.json package-lock.json"``

The ``sync-npm`` command should be called on ``postinstall`` to update the file when ``yarn.lock`` changes:
    ``"postinstall": "other/commands && yarn sync-npm"``

Starting with version 6 ``npm audit`` will list security vulnerabilities found in the currently installed packages.
Simply running ``npm audit`` will show insecure packages with their dependency tree and if possible a way to fix them.
Most of the time to fix a security issue we will need an update from the top level packages used.

More info about this feature can be found `here <https://docs.npmjs.com/getting-started/running-a-security-audit>`_.

Bower *
-------

Bower is a front-end package manager. It is needed and installed through NPM.

Debian / Ubuntu:
    ``$ sudo npm install -g bower``

Windows:
    ``npm install -g bower``

.. todo:: Replace bower with yarn.

.. todo:: Don't use ``sudo`` with npm.

Yarn *
------

Yarn is a package manager for JavaScript that is also used to run the frontend.
It is required to run the frontend and it needs NodeJS.

The following instructions are a summary, for more detailed information please
see the official `installation instructions at Yarn <https://yarnpkg.com/en/docs/install>`_.

**Debian / Ubuntu**::

    curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
    echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
    sudo apt-get update && sudo apt-get install yarn

Windows:
    `Download <https://yarnpkg.com/en/docs/install>`_ and run the installer from Yarn.

.. _git-setup:

`Git <https://git-scm.com/downloads>`_ *
----------------------------------------

Git is the distributed version control system to manage the frontend code
repositories.

Windows:
    Download the installer from the `official Git page <https://git-scm.com/downloads>`_ and run it.

Debian / Ubuntu:
    ``$ sudo apt-get install git``

Time
----

Make sure the time is correctly set on your computer as it is used when
committing code and it will be noted in git log.

Debian / Ubuntu:
    .. note::
        The recommended and following instructions will install ntpq, the
        standard NTP query program, and query time servers. This will in
        addition also keep the date and time updated automatically. If this is
        not what you want, then you may manually `adjust the
        time <https://wiki.debian.org/DateTime>`_ of the system.

    ``$ sudo apt-get install ntp``

    ``$ sudo ntpq -p``

Windows:
    Go to the control panel and adjust date and time, it is also recommended to
    `enable synchronization with a time server <https://www.windowscentral.com/how-manage-time-servers-windows-10>`_ to keep it correct.

Optional software
-----------------

Meld
~~~~

A a visual diff and merge tool targeted at developers. Useful to compare
file differences and similarities.

Debian / Ubuntu:
    ``$ sudo apt-get install meld``

Windows:
    Download it from the official `Meld page <http://meldmerge.org/>`_ and run
    the installer.

ModHeaders
~~~~~~~~~~

A Google Chrome / Chromium extension enabling the possibility to show
the output of available-values API calls presented in the web browser
console by modifying HTTP headers sent to the server.

Google Chrome / Chromium:
    Get the extension from the `Chrome Web Store <https://chrome.google.com/webstore/detail/modheader/idgpnmonknjnojddfkpgkljpfnnfcklj>`_

    Then click on the icon next to the address bar, then the plus (+)
    and add:

        Request header

            Name: ``Accept``

            Value: ``application/json``

        Filter

            Name: ``URL Pattern``

            Value: ``*cosmoz*available*``

Slack standalone application
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Slack is a cloud-based set of proprietary team collaboration tools and
services used for collaboration. You can access it through the web, or
via an standalone application if you like. The following instructions
install that.

Download the installer from the
`official Slack page <https://slack.com/downloads>`_.

Debian / Ubuntu:
    ``dpkg -i <downloaded file name>``

Windows:
    Run the downloaded installer file.
