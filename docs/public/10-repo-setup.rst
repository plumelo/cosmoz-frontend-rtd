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
            "browser": true
        },
        "extends": "eslint:recommended",
        "rules": {
            "accessor-pairs": 1,
            "brace-style": 2,
            "camelcase": 2,
            "eqeqeq": 2,
            "guard-for-in": 2,
            "indent": [
                2,
                "tab"
            ],
            "no-console": 0,
            "no-else-return": 2,
            "no-empty": 2,
            "no-empty-function": 2,
            "no-eval": 2,
            "no-extra-bind": 2,
            "no-extra-parens": 2,
            "no-invalid-this": 2,
            "no-labels": 2,
            "no-lone-blocks": 2,
            "no-lonely-if": 2,
            "no-loop-func": 2,
            "no-new": 2,
            "no-param-reassign": 2,
            "no-self-compare": 2,
            "no-trailing-spaces": 2,
            "no-unused-expressions": 2,
            "no-unused-vars": 1,
            "no-use-before-define": 2,
            "no-useless-call": 2,
            "no-useless-concat": 2,
            "one-var": 2,
            "one-var-declaration-per-line": [
                2,
                "always"
            ],
            "quotes": [
                2,
                "single"
            ],
            "radix": 2,
            "semi": [
                2,
                "always"
            ],
            "space-before-function-paren": [
                2,
                {
                    "anonymous": "always",
                    "named": "never"
                }
            ],
            "space-in-parens": 2,
            "valid-jsdoc": 1
        },
        "plugins": [
            "html"
        ],
        "globals": {
            "CustomElements": false,
            "HTMLImports": false,
            "Polymer": false,
            "WeakMap": false
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

`cosmoz-elements <https://github.com/Neovici/cosmoz-elements>`_
---------------------------------------------------------------

Add the element to the ``cosmoz-elements`` collection.

Also, some files that are common between all elements can be hosted here.

.. todo:: What files? CONTRIBUTING?

.. todo:: publish collection to wc.org
