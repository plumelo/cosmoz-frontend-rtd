Different types of views
------------------------

Cosmoz has a few generic types of views that are recurring:


.. _view_type_core:

"\*-core"-type views
~~~~~~~~~~~~~~~~~~~~

A "core" type view is intended to be reused by other views.
It is basically a complete view except that:

- It doesn't fetch its own "main" data
- It doesn't set the ``title`` property
- It doesn't depend on the ``params`` property object

.. note::

    For example, ``purchase-invoices-view-core`` expects the ``invoice``
    property to be set by "someone", whereas the ``purchase-invoices-view`` implementation
    finds out the ``id`` from ``params.id``, fetches the invoice and feeds it to ``purchase-invoices-view-core``.

“Add”-type views
~~~~~~~~~~~~~~~~

“List”-type views
~~~~~~~~~~~~~~~~~

.. _view_type_list_queue:

“List-queue”-type views
~~~~~~~~~~~~~~~~~~~~~~~

A "list-queue" view typically uses :ref:`cosmoz-data-nav` to combine the ``list-core`` view and the ``view-core`` view to make a queue-type behavior with browsable items.
It is usually implemented as a ``list-queue-core`` view for the object-type, which in turn is reused wherever the list-queue behavior for the object type is needed.

Breakdown:

- list-queue - implementation
    - :ref:`cz-apicall` - fetch list data
    - set title
    - list-queue-core
        - mediator between list-core and data-nav/view-core
        - :ref:`cz-apicall` - will fetch object details when requested
        - :ref:`cosmoz-tabs`
            - cosmoz-tab
                - list-core - provide a re-sorted/filtered/grouped version of the list through :ref:`cosmoz-omnitable`
            - cosmoz-tab
                - :ref:`cosmoz-data-nav` - consume user-reorganized version
                    - template
                        - view-core

“View/edit”-type views
~~~~~~~~~~~~~~~~~~~~~~
