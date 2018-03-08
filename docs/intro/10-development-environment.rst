Development environment
-----------------------

The frontend development environment consists of various parts of software
working together.

Various operating systems are supported - Debian, Ubuntu and Windows. The
used software is free of charge and it's possible to locally run only open
source software if you like to.

Things marked with an asterisk (*) are required.

Before you start
    In Linux based operating systems (Debian / Ubuntu) you need to open a
    terminal window (or switch to a TTY) to run the commands presented here.
    There are various ways to do this and they differ between Linux operating
    system variants. Try ``Ctrl + Alt + T`` or look it up for your specific
    operating system version.

    In Windows you need to open a console window instead. One way to do it is
    push ``Win + R`` key and type ``cli``. Another is to browse the menus and
    find the console window program.

    The terminal / console window plays a big part of the frontend development,
    so get yourself familiar with it if you have not used it before.

    All commands should be followed by an ``Enter / Return`` key to run them.
    Exclude the ``$`` in the beginning of each line, it's just there to show
    that it is a command.

Google Chrome / Chromium *
~~~~~~~~~~~~~~~~~~~~~~~~~~

Google Chrome is a freeware web browser developed by Google. Chromium is an
open-source Web browser project started by Google, to provide the source code
for the proprietary Google Chrome browser. Google Chrome is the target web
browser, but Chromium works just as good as an open source alternative.

    Google Chrome *
        The major web browser.

        Debian / Ubuntu / Windows:
            Get it from the official `download page <https://www.google.se/chrome/>`_ and install it.

    Chromium *
        If you want an open source alternative.

        Debian/Ubuntu:
            ``$ sudo apt-get install chromium``

        Windows:
            Get it from the `download page <https://chromium.woolyss.com/download/>`_ and install it.

.. _vscode:

`Visual Studio Code (vscode) <https://code.visualstudio.com/>`_ with `extensions <https://marketplace.visualstudio.com/>`_ *
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A code editor developed by Microsoft, freely available to download and use for
the most common platforms, even in Linux based operating systems, enhanced by
some required extensions.

Follow the installation instructions for the editor itself and the extensions
in the links below to get them too.

Debian / Ubuntu / Windows:
    * `Visual Studio Code <https://code.visualstudio.com/>`_ * - The editor itself

    * `ESLint <https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint>`_ * - Integrates ESLint into VS Code

    * `polymer-ide <https://marketplace.visualstudio.com/items?itemName=polymer.polymer-ide>`_ * - Provides linting, autocompletion, and more for web components

    * `Marketplace <https://marketplace.visualstudio.com/>`_ - For the inspired to find more extensions

`NodeJS <https://nodejs.org/en/download/>`_ *
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

An open source server framework, it's free, runs on various platforms and uses
JavaScript. It's used to run the frontend and comes with the NPM package manager
used to install some additional required packages.

Debian / Ubuntu:
    .. note::
        Debian and other similar Linux based operating system developers: the
        NodeJS version in the OS repository is outdated (for Debian Stable at
        least).

    Follow the instructions on the `Installing Node.js via package manager <https://nodejs.org/en/download/package-manager/>`_ page to get an updated version of NodeJS.

Windows:
    Download the installer from the official `download page <https://nodejs.org/en/download/>`_ and and run it.

Gulp, Bower and Polymer *
~~~~~~~~~~~~~~~~~~~~~~~~~

Gulp is a toolkit for automating painful or time-consuming tasks in your
development workflow, Bower is a front-end package manager and Polymer CLI is
the official command line tool for Polymer projects and Web Components. They
are all needed and installed through NPM.

Debian / Ubuntu:
    ``$ sudo npm install -g gulp bower polymer-cli``

Windows:
    ``npm install -g gulp bower polymer-cli``


.. todo:: Replace bower with yarn.

.. todo:: Drop dependency for ``gulp``, use ``polymer build`` / ``polymer serve``.

.. todo:: Don't use ``sudo`` with npm.

.. _git-setup:

`Git <https://git-scm.com/downloads>`_ *
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Git is a distributed version control system, used to manage the frontend code
repositories.

Windows:
    Download the installer from the `official page <https://git-scm.com/downloads>`_ and run it.

Debian / Ubuntu:
    ``$ sudo apt-get install git``

Time
~~~~

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
~~~~~~~~~~~~~~~~~

    Meld
        A a visual diff and merge tool targeted at developers. Useful to compare
        file differences and similarities.

        Debian / Ubuntu:
            ``$ sudo apt-get install meld``

        Windows:
            `Download <http://meldmerge.org/>`_ and run the installer.

    ModHeaders
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
        Slack is a cloud-based set of proprietary team collaboration tools and
        services used for collaboration. You can access it through the web, or
        via an standalone application if you like. The following instructions
        install that.

        Download the installer from the
        `official page <https://slack.com/downloads>`_.

        Debian / Ubuntu:
            ``dpkg -i <downloaded file name>``

        Windows:
            Run the downloaded installer file.