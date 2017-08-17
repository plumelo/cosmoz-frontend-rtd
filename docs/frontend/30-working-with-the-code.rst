Working with the code
=====================

Mostly the same approach as for public elements:

.. seealso::

    * :ref:`dependency-management`


-  Run frontend development web server Gulp::

    $ gulp serve

.. note::
    ``polymer serve`` almost works when run in ``app/`` folder in repo.

    .. todo::

        - Google Auth (invalid origin)

        - Default hash-URL (because of folder path?)

-  Open project in :ref:`vscode`:

:menuselection:`File --> Open Folder… --> Find cosmoz3-frontend folder --> OK`

-  Make sure :file:`app/cz.config.js` points to the right backend and has the right ``googleClientId`` for Google sign-in

-  The local frontend should now be running at http://localhost:3000


Linting
-------

Both ESLint and Polymer IDE should automatically lint the code in :ref:`vscode`.

.. note::

    Since we (mostly) separate HTML and JS, Polymer-IDE in :ref:`vscode` can't lint the JS-file by itself, only through the HTML file.
    This is because the JS-file doesn't have any reference to the importing HTML-file, high prio case here:
    https://github.com/Polymer/polymer-analyzer/issues/224

    Linting the JS-file will result in a lot of "unknown polymer behavior" errors.

.. note::

    If you want to run ``polymer lint`` manually on a file in the source, be sure to run the command from the repo root.
    This makes sure it uses :file:`polymer.json` and also that it will be able to resolve all imports::

        $ polymer lint app/views/purchase/invoices/view-core.html

.. _private_component_docs:

Documentation for private components
------------------------------------

For now there's a simple, crude way to access the component documentation,
for example for ``cz-apicall`` when running the ``gulp serve`` server:

    http://localhost:3000/polymer/cz-apicall/index.html

These should be documented the same way as the public repo :ref:`public_repo_documentation`.


.. todo::

    - Create a basic listing/catalog of the elements we have

    - Make sure ``gulp serve`` serves ``index.html`` for any directory

    or, preferably:

    - Implement (something like) https://github.com/Polymer/polymer-element-catalog


System documentation
--------------------

Working with the documentation (this).

Install sphinx + autobuild + rtd theme::

    $ sudo apt install python-pip
    $ sudo pip install sphinx sphinx-autobuild sphinx_rtd_theme

Get the source::

    $ git clone https://github.com/Neovici/cosmoz-frontend-rtd
    $ cd cosmoz-frontend-rtd/docs

Auto-build and view::

    $ sphinx-autobuild . _build_html

Documentation should be available and auto-reload upon change at http://localhost:8000

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
