Omnitable setup
===============

.. todo: Add omnitable background

Column defintions
-----------------

Naming
~~~~~~

Make sure each ``name`` is unique, it will be used for sorting/grouping
among other things and should be (close enough to) something backend understands for BE-sorting, etc.

Data types
~~~~~~~~~~

cosmoz-omnitable-column
^^^^^^^^^^^^^^^^^^^^^^^
Freetext search, will locally match any row *containing* the written letters.

.. note:: 

    OTS - This should be used for data like article numbers, invoice numbers, order numbers,
    order identifiers, descriptions, etc for OTS to avoid requesting huge lists of suggestions.

cosmoz-omnitable-column-autocomplete
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^




Sizing
~~~~~~

- Flex
- Flex 0
- overflow
- minWidth

Folding priority
~~~~~~~~~~~~~~~~

Omnitable search (OTS)
----------------------

Available values
~~~~~~~~~~~~~~~~

Filtering / querying setup
~~~~~~~~~~~~~~~~~~~~~~~~~~

Sorting
~~~~~~~

Results / local mode
~~~~~~~~~~~~~~~~~~~~