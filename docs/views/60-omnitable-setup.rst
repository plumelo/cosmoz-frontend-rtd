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

cosmoz-omnitable-column-amount
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type for money amounts, including currency symbol.

cosmoz-omnitable-column-autocomplete
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

cosmoz-omnitable-column-boolean
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type for boolean values, displays as yes or no.

cosmoz-omnitable-column-date
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type for date only display. Follows user locale format.

cosmoz-omnitable-column-datetime
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type for both date and time display. Follows user locale format.

cosmoz-omnitable-column-list
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type to display a dashed vertical list within the column itself.

cosmoz-omnitable-column-list-horizontal
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type to display a horizontal list within the column itself.

cosmoz-omnitable-column-number
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type to display numbers - integer, float values and so on.

cosmoz-omnitable-column-time
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Column type to display times. Follows user locale format.

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

Sorting and grouping
~~~~~~~~~~~~~~~~~~~~

Sorting in omnitable can be set by the user selecting what column to sort on in the bottom controls of the table, or by presetting it in the code using the ``sort-by`` attribute in the ``cosmoz-omnitable`` tag. This attribute takes the column name attribute as value.

The same goes for grouping, it can also be set by the user in the bottom of the table and also be set by presetting it using the ``group-on``.

Results / local mode
~~~~~~~~~~~~~~~~~~~~