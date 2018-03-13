Working with the code
=====================

Dependency management
---------------------

Management of dependencies are mostly the same approach as for public elements:

.. seealso::

    * :ref:`dependency-management`

Start the editor
----------------

Open the recommended editor :ref:`vscode`. Then open the repository root
directory by using the menus:

    :menuselection:`File --> Open Folder… --> Find cosmoz3-frontend folder --> OK`

Set the backend
---------------

The frontend needs to be configured to use the correct backend. This is done in a
configuration file in the repository:

:file:`app/cz.config.js`

Open this file and verify that the ``backendBaseUri`` property points to the
right backend and that ``googleClientId`` has the right value for Google
sign-in.

Start the web server
--------------------

The frontend runs on a local web server powered by gulp toolkit. To start it you
need to go to the repository root directory and then run the following::

    $ gulp serve

.. note::
    ``polymer serve`` almost works when run in ``app/`` folder in repo.

This will also open the default web browser when the server is ready and point
it to http://localhost:3000/.

Login in to beta
----------------

Login using the beta backend using Google authentication directly through
the local frontend is currently not possible due to invalid origin for the
sign in process.

To login, do instead visit https://beta.cosmoz.com/ and use the Google sign in
there, then go back to http://localhost:3000/ and reload the page. You should
now be logged in because both uses the same backend.

URL format
----------

The URL usually consists of the following::

    http://localhost:3000/?cpl=<current path locator>#!/<view path>#<parameter 1>=<value 1>&<parameter 2>=<value 2>...

``current path locator`` refers to the path locator currently used in the
frontend, the branch in the organization tree selected in the branch selector in
the bottom right of the page.

``view path`` is the directory path of the current view that is being displayed.
This path is the same as ``app/views/<view path>`` in the repository root
directory.

``parameter`` and ``value`` are GET parameters passed to the page.

There may also be a parameter besides ``cpl`` named ``backendBaseUri`` that
overrides the property with the same name defined in the
:file:`app/cz.config.js` file.

Linting
-------

Both ESLint and Polymer IDE should automatically lint the code in :ref:`vscode`.

Single JS files are not lintable
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HTML and JS are mostly separated. Therefore can't Polymer-IDE :ref:`vscode` lint
the JS-file by itself, only through the HTML file.

This is because the JS-file doesn't have any reference to the importing
HTML-file. There is a high priority issue for this opened in the
polymer-analyzer at the Polymer repository to address this:

https://github.com/Polymer/polymer-analyzer/issues/224

Linting the JS-file will result in a lot of "unknown polymer behavior" errors.

The workaround for this is not to lint or trust the linting results the JS files
alone buth rather lint the HTML file related to the JS file instead.

Linting HTML and JS files together
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You may lint HTML files which will also lint the related JS files using
``polymer lint``.

To do this, make sure you stand in the repository root. This makes sure it uses
:file:`polymer.json` and also that it will be able to resolve all dependency
imports::

To lint a view, core file and so on, do this when standing in the repository
root::

    $ polymer lint app/views/<path to view file>.html

.. _private_component_docs:

Local documentation for private components
------------------------------------------

There is a simple, crude way to access the component documentation,
for example for ``cz-apicall`` when running the ``gulp serve`` server:

    http://localhost:3000/polymer/cz-apicall/index.html

These should be documented the same way as the public repository
:ref:`public_repo_documentation`.


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