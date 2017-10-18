Repository setup
================

Creating a repository
---------------------

Be sure to create it under the https://github.com/Neovici organization


.. _github-readme:

:file:`README.md`
-----------------

Badges
~~~~~~

Travis-CI::

    [![Build Status](https://travis-ci.org/Neovici/cosmoz-bottom-bar.svg?branch=master)](https://travis-ci.org/Neovici/cosmoz-bottom-bar)

Webcomponents.org::

    [![Published on webcomponents.org](https://img.shields.io/badge/webcomponents.org-published-blue.svg)](https://www.webcomponents.org/element/Neovici/cosmoz-bottom-bar)

.. note:: Badge URLs needs to be adjusted for the relevant repo.

Inline demo
~~~~~~~~~~~

For :ref:`webcomponents-org`

.. _eslintrc-json:

:file:`.eslintrc.json`
----------------------

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
				{ "before": true, "after": true }
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

This should be set/present in:

* ``bower.json``
* ``package.json``

Also, a ``LICENSE`` file containing the Apache 2.0 License should be present in the repository root.

Finally, all applicable files should have the following notice enclosed in the appropriate comment syntax for the file format::

    Copyright 2017 Neovici

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

Travis-CI + Slack
~~~~~~~~~~~~~~~~~

In the repo, run::

    $ travis encrypt "<1password-devops-password>" --add notifications.slack

.. note::
    Make sure that the organisation is ``Neovici`` and not ``neovici`` (case
    insensitive!) for the repo slug (the URL-friendly name of the repository).

GitHub + Slack
~~~~~~~~~~~~~~

Adjust GitHub integration at https://neovici.slack.com/apps/manage, add repo


.. _cosmoz-elements:

cosmoz-elements
---------------

https://github.com/Neovici/cosmoz-elements

Add the element to the ``cosmoz-elements`` collection.

Also, some files that are common between all elements can be hosted here.

.. todo:: What files? CONTRIBUTING?

.. todo:: publish collection to wc.org
