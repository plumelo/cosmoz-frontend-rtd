Coding guidelines
-----------------

Always try to develop components in as much isolation as possible and
try to put different demo scenarios into the demo to test different
contexts at the same time.

.. todo:: ESLint info

Indentation
~~~~~~~~~~~

Tabs.

Polymer data binding
~~~~~~~~~~~~~~~~~~~~

Data bindings should be written with spaces::

    [[\_(“Text”, t)]]

instead of::

    [[ \_(“Text”, t) ]]