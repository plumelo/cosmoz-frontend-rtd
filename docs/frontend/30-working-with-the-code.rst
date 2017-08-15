Working with the code
=====================

Mostly the same approach as for public elements:

.. seealso::

    * :ref:`dependency-management`

Documentation
-------------

-  Run frontend development web server Gulp::

    $ gulp serve

.. note::
    ``polymer serve`` almost works when run in ``app/`` folder in repo.

    .. todo::

        - Google Auth (invalid origin)

        - Default hash-URL (because of folder path?)

-  Open project in :ref:`vscode`:

:menuselection:`File --> Open Folder… --> Find cosmoz3-frontend folder --> OK`

-  Make sure ``app/cz.config.js`` points to the right backend and has the right ``googleClientId`` for Google sign-in

-  The local frontend should now be running at http://localhost:3000



Working with the documentation (this).

Install sphinx + autobuild + rtd theme::

    $ sudo apt install python-pip
    $ sudo pip install sphinx sphinx-autobuild sphinx_rtd_theme

Get the source::

    $ git clone https://github.com/Neovici/cosmoz-frontend-rtd
    $ cd cosmoz-frontend-rtd/docs

.. seealso:: 

    https://docs.readthedocs.io/en/latest/getting_started.html

    http://sphinx-doc.org/latest/install.html

Writing docs
~~~~~~~~~~~~

.. seealso::

    https://docs.readthedocs.io/en/latest/index.html

    http://www.sphinx-doc.org/en/stable/rest.html

Submitting changes
~~~~~~~~~~~~~~~~~~

See :ref:`github-submitting-changes` for public elements' :ref:`github-git`

Internal component documentation catalog
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. todo:: https://github.com/Polymer/polymer-element-catalog