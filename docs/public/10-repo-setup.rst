Repository setup
================

Creating a repository
---------------------

Public elements need to have their own repositories on GitHub.

Make sure to create it under the https://github.com/Neovici organization.

.. _github-readme:

Required files in a public element repository
----------------------------------------------

:file:`README.md`
~~~~~~~~~~~~~~~~~
This file should contain badges for GitHub, information about what the element does, how
to install it, how to use it, an inline demo for Webcomponents.org and so on.

Badges
	Badges are small informational signs that appear when the file is
	displayed on GitHub, showing status for various services. Start the file
	by adding these.

	.. note:: Badge URLs suggested here need to be adjusted for the relevant repo.

	Travis-CI
		This badge shows the element build status for Travis-CI.

		.. code-block:: text

			[![Build Status](https://travis-ci.org/Neovici/cosmoz-bottom-bar.svg?branch=master)](https://travis-ci.org/Neovici/cosmoz-bottom-bar)

	Webcomponents.org
		This badge shows the element publication status on Webcomponents.org.

		.. code-block:: text

			[![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/Neovici/cosmoz-bottom-bar)

Inline demo
	There need to be an inline demo included in the file, used by
	:ref:`webcomponents-org`.

	.. _eslintrc-json:

:file:`.eslintrc.json`
~~~~~~~~~~~~~~~~~~~~~~

This file holds data for ESLint validation.

.. code-block:: json

	{
		"env": {
			"browser": true,
			"es6": true
		},
		"extends": "eslint:recommended",
		"globals": {
			"Cosmoz": false,
			"CustomElements": false,
			"HTMLImports": false,
			"Polymer": false,
			"WeakMap": false
		},
		"plugins": [
			"html"
		],
		"rules": {
			"accessor-pairs": "warn",
			"array-bracket-spacing": [
				"error",
				"never"
			],
			"arrow-parens": [
				"error",
				"as-needed"
			],
			"arrow-spacing": [
				"error",
				{
					"before": true,
					"after": true
				}
			],
			"brace-style": "error",
			"camelcase": "error",
			"comma-spacing": [
				"error",
				{
					"after": true
				}
			],
			"comma-style": [
				"error",
				"last"
			],
			"curly": [
				"error",
				"all"
			],
			"eqeqeq": [
				"error",
				"smart"
			],
			"guard-for-in": "error",
			"indent": [
				"error",
				"tab"
			],
			"key-spacing": [
				"error",
				{
					"afterColon": true,
					"beforeColon": false
				}
			],
			"keyword-spacing": [
				"error",
				{
					"before": true
				}
			],
			"no-console": "off",
			"no-else-return": "error",
			"no-empty": "error",
			"no-empty-function": "error",
			"no-eval": "error",
			"no-extra-bind": "error",
			"no-extra-parens": "error",
			"no-invalid-this": "error",
			"no-labels": "error",
			"no-lone-blocks": "error",
			"no-lonely-if": "error",
			"no-loop-func": "error",
			"no-new": "error",
			"no-param-reassign": "error",
			"no-self-compare": "error",
			"no-trailing-spaces": "error",
			"no-unused-expressions": "error",
			"no-unused-vars": "warn",
			"no-use-before-define": "error",
			"no-useless-call": "error",
			"no-useless-concat": "error",
			"one-var": "error",
			"one-var-declaration-per-line": [
				"error",
				"always"
			],
			"quotes": [
				"error",
				"single"
			],
			"radix": "error",
			"semi": [
				"error",
				"always"
			],
			"space-before-blocks": [
				"error",
				"always"
			],
			"space-before-function-paren": [
				"error",
				{
					"anonymous": "always",
					"named": "never"
				}
			],
			"space-in-parens": "error",
			"space-infix-ops": "error",
			"valid-jsdoc": "warn"
		}
	}

.. _github-license:

License
-------

Open Source Cosmoz components use the Apache-2.0 license.

This should be set or present in the files noted below.

:file:`.bower.json`
~~~~~~~~~~~~~~~~~~~

The Bower package manager configuration, add a license property with as the value set to the Apache 2.0 license. to this file.

Ommit the ``{`` and ``}`` if the file already has these.

.. code-block:: json

	{
		"license": "Apache-2.0"
	}

:file:`.package.json`
~~~~~~~~~~~~~~~~~~~~~

The NPM package manager configuration, add a license property with as the value set to the Apache 2.0 license. to this file.

Ommit the ``{`` and ``}`` if the file already has these.

.. code-block:: json

	{
		"license": "Apache-2.0"
	}

:file:`LICENSE / LICENSE.md`
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

This file should contain the  `Apache 2.0 License <https://www.apache.org/licenses/LICENSE-2.0.txt>`_ in plain text format.

License comment
~~~~~~~~~~~~~~~

Finally, all applicable files should have the following notice enclosed in the appropriate comment syntax for the file format::

	Copyright 2017-2018 Neovici

	Licensed under the Apache License, Version 2.0 (the "License");
	you may not use this file except in compliance with the License.
	You may obtain a copy of the License at

		http://www.apache.org/licenses/LICENSE-2.0

	Unless required by applicable law or agreed to in writing, software
	distributed under the License is distributed on an "AS IS" BASIS,
	WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
	See the License for the specific language governing permissions and
	limitations under the License.

Integrations
------------

There are some integrations needed to be done for the element to make various
services push information about element changes to Slack.

Travis-CI + Slack
~~~~~~~~~~~~~~~~~

Travis-CI and Slack integration enables build notifications for the element
directly in Slack.

In the repository, run::

    $ travis encrypt "<1password-devops-password>" --add notifications.slack

.. note::
    Make sure that the organisation is ``Neovici`` and not ``neovici`` (case
    insensitive!) for the repo slug (the URL-friendly name of the repository).

GitHub + Slack
~~~~~~~~~~~~~~

GitHub and Slack integration enables repository change notifications directly
in Slack.

Adjust GitHub integration at https://neovici.slack.com/apps/manage, add repo.

.. _cosmoz-elements:

The Cosmoz elements collection
------------------------------

Add the element to the `cosmoz-elements <https://github.com/Neovici/cosmoz-elements>`_ collection.

Also, some files that are common between all elements can be hosted here.

.. todo:: What files? CONTRIBUTING?

.. todo:: Publish collection to webcomponents.org.