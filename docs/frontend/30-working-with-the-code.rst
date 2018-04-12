Working with the code
=====================

Dependency management
---------------------

Management of dependencies for the frontend are mostly the same approach as for
public elements.

.. seealso::

    * :ref:`dependency-management`

Start the editor
----------------

Open the recommended editor :ref:`vscode`. Then open the repository root
directory by using the menus:

    :menuselection:`File --> Open Folder… --> Find cosmoz3-frontend folder --> OK`

Set the backend
---------------

The default backend for development is the alpha backend. The frontend can to be
configured to use an different backend by setting it in the configuration file
in the repository.

    .. seealso:: :ref:`backend-config`

Start the web server
--------------------

The frontend runs on a local web server powered by yarn. To start it you
need to go to the repository root directory and then run the following::

    $ yarn start

The start of yarn will also open the default web browser when the server is
ready and point it to http://localhost:3000 where the frontend is available.

Login in to alpha and beta
--------------------------

Login using the alpha or beta backend using Google authentication directly
through the local frontend is currently not possible due to invalid origin for
the sign in process. Trying to login that way results in sign errors.

To login, do instead visit https://alpha.cosmoz.com for alpha or
https://beta.cosmoz.com for beta and use the Google sign in there, then go back
to http://localhost:3000 and reload the page. You should now be logged in
because both uses the same backend.

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

``parameter`` and ``value`` are parameters passed to the page.

There may also be a query parameter besides ``cpl`` named ``backendBaseUri``
that overrides the property with the same name defined in the
:file:`app/cz.config.js` file.

.. seealso::
    * :ref:`url-view-structure`

Linting in Visual Studio Code
-----------------------------

Linting in :ref:`vscode` is available from several sources: ESLint and Polymer
IDE extensions. Both of these should automatically lint the code.

Single JS files are not lintable alone
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

HTML and JS are mostly separated. Therefore can't Polymer IDE lint the JS-file
by itself, only through the HTML file.

This is because the JS-file doesn't have any reference to the importing
HTML-file. There is a high priority issue for this opened in the
polymer-analyzer at the Polymer repository to address this, `issue number 224
<https://github.com/Polymer/polymer-analyzer/issues/224>`_.

Linting the JS-file will result in a lot of unknown polymer behavior false
errors.

The workaround for this is not to lint or trust the linting results the JS files
alone but rather lint the HTML files related to the JS files instead.

Linting with Polymer
--------------------

Polymer linting is also available from the command line using ``polymer lint``.

Linting HTML and JS files together
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

You may lint HTML files which will also lint the related JS files.

To do this, make sure you stand in the repository root. This makes sure it uses
:file:`polymer.json` and also that it will be able to resolve all dependency
imports.

To lint a view, core file and so on, do this when standing in the repository
root::

    $ polymer lint app/views/<path/to/view file>.html

.. _private_component_docs:

Linting with ESLint
-------------------

ESLint linting is also availble from the command line.

To lint some selected relevant directories of the repository, go to the root of
it and run::

    $ node_modules/.bin/eslint --ext .js,.html app/views/ app/scripts/ app/polymer/

Local documentation for private components
------------------------------------------

The private components are located in ``app/polymer`` under the repository root
directory. There is a simple, crude way to access the component documentation
for these when ``gulp serve`` server is running:

    http://localhost:3000/polymer/<component name>/index.html

These components should be documented the same way as the public repository
:ref:`public_repo_documentation`.

.. todo::
    Create a basic listing/catalog of the elements we have.

    Make sure ``gulp serve`` serves ``index.html`` for any directory.

    Or preferably implement something like
    https://github.com/Polymer/polymer-element-catalog.

System documentation
--------------------

Working with the frontend documentation (this documentation).

Install dependencies
~~~~~~~~~~~~~~~~~~~~

Dependencies for the documentation are installed using the pip package manager.

The required documentation dependencies are currently:

- `Sphinx <http://www.sphinx-doc.org/en/master/>`_ - a Python documentation generator

- `sphinx-autobuild <https://pypi.python.org/pypi/sphinx-autobuild>`_ - a script to automatically rebuild the documentation

- `Read the Docs Sphinx Theme <https://github.com/rtfd/sphinx_rtd_theme/blob/master/README.rst>`_ - the Sphinx theme for the documentation

To install pip and the dependencies, do the following:

Debian / Ubuntu::

    $ sudo apt install python-pip
    $ sudo pip install sphinx sphinx-autobuild sphinx_rtd_theme

Get the source
~~~~~~~~~~~~~~

To get the source you can clone it from the GitHub repository and then enter the
directory that is created by the cloning process::

    $ git clone https://github.com/Neovici/cosmoz-frontend-rtd
    $ cd cosmoz-frontend-rtd/docs

Start the web server
~~~~~~~~~~~~~~~~~~~~

In order to get the local copy of the documentation up and running you need to
use ``sphinx-autobuild`` to build it and start the web server::

    $ sphinx-autobuild . _build_html

Documentation should be available and reload automatically upon change at
http://localhost:8000.

For more information about setting up the documentation you may look at the
`Installing Sphinx <http://www.sphinx-doc.org/en/master/usage/installation.html>`_
page at Sphinx documentation and the `Getting started
<https://docs.readthedocs.io/en/latest/getting_started.html>`_ page in the Read
the Docs documentation.

Writing documentation
~~~~~~~~~~~~~~~~~~~~~

Documentation is written in the ``reStructuredText`` format. Information about
this format is available in the `Sphinx documentation
<http://www.sphinx-doc.org/en/master/rest.html>`_.


The documentation is hosted by Read the Docs, which has a `documentation
<https://docs.readthedocs.io/en/latest/index.html>`_ itself.

Submitting changes
~~~~~~~~~~~~~~~~~~

Contributions to the documentation are encouraged and should be done in branches
followed by a `pull request
<https://help.github.com/articles/creating-a-pull-request/>`_. For more details
about this, please see :ref:`github-submitting-changes` for public elements
:ref:`github-git`.