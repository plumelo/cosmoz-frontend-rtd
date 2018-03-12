Repository setup
================

Get Developer role
------------------

Redmine is a web-based project management and issue tracking tool used to track
the project.

To get access, create an `Access Request
<https://redmine.neovici.se/projects/access-requests/issues/new>`_ and request a
``Developer`` role in the ``Cosmoz 3`` project.

Get the code
------------

Choose a directory to work in. Then check out the code from the repository at
GitHub and go to the repository root directory that gets created during the
repository cloning process::

    $ git clone https://username@git.neovici.se/development/cosmoz3/frontend.git cosmoz3-frontend
    $ cd cosmoz3-frontend

Add a commit hook
-----------------

To make sure you include Redmine issue number or a ``NOREF`` tag in the commit
messages you need to add a commit hook to your working copy of the repository.
This will automatically abort commits if they are missing the required
information.

:file:`.git/hooks/commit-msg`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create this file  with the following content:

.. code-block:: bash

    #!/bin/sh
    # regex to validate in commit msg
    commit_regex='(merge|NOREF|refs #|fixes #)'
    error_msg="Aborting commit. Your commit message is missing either a fixes #1234, refs #1234 or NOREF"
    if ! grep -iqE "$commit_regex" "$1"; then
        echo "$error_msg" >&2
        exit 1
    fi

.. note::
    Tip. It is possible to edit the last commit message as long as it has not
    been pushed remote by running ``git commit --amend``. This way you can add
    issue number afterwards.

Add a pre-commit hook
---------------------

Optionally, add pre-commit hook to you working copy of the repository to check
for invalid root commits and to show ESLint and Polymer Lint results with an
option to abort the commit.

:file:`.git/hooks/pre-commit`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Create this file with the following content:

.. code-block:: bash

    #!/bin/bash

    if [ "$(id -u)" = "0" ]; then
        echo "Root commits are not allowed, because this affects file permissions."
        exit 1
    fi

    echo '--- ESLint report ---';
    node_modules/.bin/eslint --ext .js,.html app/views/ app/scripts/ app/polymer/
	if [ $? -ne 0 ]; then
		echo "ESLint must pass to allow commit."
		exit 1;
	fi

    echo '--- Polymer Lint report ---';
    polymer lint

    echo '---';

    # read user input, assigns stdin to keyboard
    # because stdin inside git hook is not available

    exec < /dev/tty

    while true; do
        read -p "Continue commit? (Y/y)" yn
        case $yn in
            [Yy] ) exit 0;; # commit accepted - return 0
            [Nn] ) exit 1;; # commit cancelled - return 1
            * ) echo "Answer y or n for yes or no.";;
        esac
    done

Install development tools
-------------------------

To install project development tools (ESLint, gulp plugins, etc), do the
following standing in the repository root directory::

    $ npm install

.. todo:: ``yarn install`` (seems to work, faster)

Install dependencies
--------------------

Install frontend dependencies into the root of the repository directory::

    $ bower install

.. todo:: ``polymer install`` ? (Currently wraps bower, seems to work)
