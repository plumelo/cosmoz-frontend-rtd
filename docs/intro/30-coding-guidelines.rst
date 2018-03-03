Coding guidelines
-----------------

Always try to develop components in as much isolation as possible and
try to put different demo scenarios into the demo to test different
contexts at the same time.


ESLint
~~~~~~

All code should be linted with ESLint with the settings configured in the :ref:`eslintrc-json`.


JavaScript compatibility
~~~~~~~~~~~~~~~~~~~~~~~~

Current code is written with ES5-compatible features.

ES6 code is written where specific features are available for :ref:`supported-platforms`.

Once the build is upgraded to run `polymer build` and transpile, we will start writing ES6 code.

.. seealso:: :ref:`jenkins` 


Polymer data binding
~~~~~~~~~~~~~~~~~~~~

Data bindings should be written with spaces, instead of::

    [[\_(“Text”, t)]]

do::

    [[ \_(“Text”, t) ]]