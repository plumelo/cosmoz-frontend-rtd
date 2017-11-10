Repository setup
----------------

-  Make sure you have the ``Developer`` role in the ``Cosmoz 3`` project in Redmine

    If not, make an `Access Request <https://redmine.neovici.se/projects/access-requests/issues/new>`_

-  Check out the code from the repository::

    $ git clone https://username@git.neovici.se/development/cosmoz3/frontend.git cosmoz3-frontend
    $ cd cosmoz3-frontend

* Add commit-hook, to make sure you include Redmine issue number or NOREF tags.
  This will abort if they are missing in your commit messages.

Create the file ``.git/hooks/commit-msg`` with the following content:

.. code-block:: bash

    #!/bin/sh
    # regex to validate in commit msg
    commit_regex='(merge|NOREF|refs #|fixes #)'
    error_msg="Aborting commit. Your commit message is missing either a fixes #1234, refs #1234 or NOREF"
    if ! grep -iqE "$commit_regex" "$1"; then
        echo "$error_msg" >&2
        exit 1
    fi

* Optionally, add pre-commit hook, to check for invalid root commits and to
  show ESLint and Polymer Lint results with an option to abort the commit.

Create the file ``.git/hooks/pre-commit`` with the following content:

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

-  Install project development tools (ESLint, gulp plugins, etc)::

    $ npm install

.. todo:: ``yarn install`` (seems to work, faster)

-  Install frontend dependencies into the directory::

    $ bower install

.. todo:: ``polymer install`` ? (Currently wraps bower, seems to work)
