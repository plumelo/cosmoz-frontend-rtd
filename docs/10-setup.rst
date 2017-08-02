Introduction
============

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

Repository configuration
^^^^^^^^^^^^^^^^^^^^^^^^

For each component repository::

    $ git config pull.rebase true
    $ git config user.name "Firstname Lastname"
    $ git config user.email "your.name@domain.tld"

.. note:: These settings can be made machine-wide by adding the ``--global`` option.

Basic Usage
^^^^^^^^^^^

.. todo:: Link to generic git guide for common tasks

.. todo:: Git flow info (Github? Gitflow? Neovici? PRs?)

Fetch changes from remote repo
""""""""""""""""""""""""""""""

Get the latest changes from remote repo, be ready with your username and password::

    $ git pull or git fetch

Checking your current work progress and log, show what files you have changed::

    $ git status

Red files are not staged for commit, green are.

Show your current changes (difference), push q to quit this::

    $ git diff

Pay attention to red square characters/long red bars they show mixed tabs and spaces, please correct before committing.
Tab characters are used in favour of spaces.

Show the commit log, push q to quit this::

    $ git log

Publishing to remote repo
"""""""""""""""""""""""""

Add files to commit::

    $ git add <files you want to commit>

Commit the changes::

    $ git commit -m “What changes you have made. Refs #issue-number”

Push the changes to the remote repo, be ready with your username and password::

    $ git push

Get latest changes::

    $ git pull

Creating versions
"""""""""""""""""

This could be done through the GitHub web, or with git cli::

    $ git tag 1.0
    $ git push --tags

Time
~~~~

Make sure the time is correctly set on your computer as it is used when committing and it will be noted in git log.

Debian/Ubuntu::

    $ sudo apt-get install ntp
    $ sudo ntpq -p

Element separation
------------------

Element names starting with ``cosmoz-`` are :ref:`public-github` (:ref:`cosmoz-elements`) hosted at GitHub.

Element names starting with ``cz-`` are available when :ref:`private-redmine`.

Coding guidelines
-----------------

Always try to develop components in as much isolation as possible and
try to put different demo scenarios into the demo to test different
contexts at the same time.

.. todo:: ESLint info

Indentation
~~~~~~~~~~~

Tabs.

Polymer data binding
~~~~~~~~~~~~~~~~~~~~

Data bindings should be written with spaces::

    [[\_(“Text”, t)]]

instead of::

    [[ \_(“Text”, t) ]]