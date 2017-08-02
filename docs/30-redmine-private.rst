.. _private-redmine:

Working with the frontend code
==============================

Getting started with the code
-----------------------------

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

-  Install project development tools (ESLint, gulp plugins, etc)::

    $ npm install

.. todo:: yarn

-  Install frontend dependencies into the directory::

    $ bower install

.. todo:: yarn

-  Run frontend development web server Gulp::

    $ gulp serve

.. note::
    ``polymer serve`` almost works when run in ``app/`` folder in repo.

    .. todo::

        - Google Auth (invalid origin)

        - Default hash-URL (because of folder path?)


-  Open project in Visual Studio Code::

:menuselection:`File --> Open Folder… --> Find cosmoz3-frontend folder --> OK`

-  Make sure ``app/cz.config.js`` points to the right backend and has the right ``googleClientId`` for Google sign-in

-  Visit http://localhost:3000

-  Get busy! :)

Repository work
---------------

Mostly the same as :ref:`public-github`.

Git
---

Create a feature branch and push to Redmine for review.

Deployment
~~~~~~~~~~

``master`` branch will be deployed to https://staging.cosmoz.com on successful build on :ref:`jenkins`

``beta`` branch will be deployed to https://beta.cosmoz.com on successful build on :ref:`jenkins`

``prod`` branch will be deployed to https://app.cosmoz.com on successful build on :ref:`jenkins`

Merges and cherry-picks to ``beta`` and ``prod`` branches are done manually according to instance deployment schedules.

.. todo:: Pull requests

.. seealso::
    :ref:`github-git`

Documentation
-------------

Working with the documentation (this)::

    $ sudo apt install python-pip
    $ sudo pip install sphinx sphinx-autobuild sphinx_rtd_theme

.. seealso:: 

    https://docs.readthedocs.io/en/latest/getting_started.html

    http://sphinx-doc.org/latest/install.html

How to write docs:

    https://docs.readthedocs.io/en/latest/index.html

    http://www.sphinx-doc.org/en/stable/rest.html

Github repo

    https://github.com/Neovici/cosmoz-frontend-rtd

.. todo:: How to update docs (PR-flow)

.. todo:: https://github.com/Polymer/polymer-element-catalog

Application build and deployment
--------------------------------

.. todo:: Polymer build

.. todo:: CI/CD with git

.. _jenkins::

Jenkins
~~~~~~~

.. todo:: Explain jenkins pipeline