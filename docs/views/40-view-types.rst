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

.. todo:: Document

“List”-type views
~~~~~~~~~~~~~~~~~

.. todo:: Document

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

Data flow
*********

    `To easier understand the flow, it is described from the "supplier invoice" list-queue.
    So in the front-end, these list-core, list-queue, list-queue-core and view-core views are 
    actually prefixed with "purchase-invoices-", but this is left out for brevity.`

.. code-block:: html

    <list-queue>
        <cz-apicall data="{{ supplierInvoices }}">

``<list-queue>`` fetches ``supplierInvoices`` with :ref:`cz-apicall`, which uses and API that returns headers only

.. todo:: Make APIs return "detail lacking details" ?

.. note:: Other implementations can use complete, invoice object lists

.. code-block:: html

    <list-queue>
        <list-queue-core supplier-invoices="[[ _headersToInvoices(supplierInvoices) ]]">

Since ``<list-queue-core>`` needs to support mixed lists of headers and full details (different backend systems),
``<list-queue>`` converts the invoice headers from the API response to complete invoice objects with only a header

.. code-block:: html

    <list-queue-core>
        <list-core invoice-list="[[ _computeInvoiceHeaderList(supplierInvoices) ]]">

``<list-queue-core>`` then converts the invoice list back to an invoice header list since ``<list-core>`` only needs that

.. todo:: Update list-core to expect "full" invoice detail objects?

.. code-block:: html

    <list-core>
        <cosmoz-omnitable data="[[ invoiceList ]]"
            sorted-filtered-grouped-items="{{ visibleGroupedInvoices }}"
            selected-items="{{ selectedInvoices }}">

``<list-core>`` then exposes the invoice list in a :ref:`cosmoz-omnitable` where the user can sort, filter, group and select invoices
in the list. The results are published in ``visibleGroupedInvoices`` and ``selectedInvoices`` (not used yet)

.. code-block:: html

    <list-queue-core>
        <list-core visible-grouped-invoices="{{ visibleGroupedInvoiceHeaders }}">``

.. code-block:: js

    // list-queue-core
    visibleInvoices: {
        type: Array,
        computed: '_computeVisibleInvoices(visibleGroupedInvoiceHeaders)'
    }

``<list-queue-core>`` then flattens the grouped list to maintain the filtering and sorting and creates a new list of complete invoices
mapped with ``supplierInvoices``

.. note:: In implementations other than ``<list-queue>`` (like ``<list-queue-approval>``), ``supplierInvoices`` can contain both headers and full invoice objects so this step
    could extract some full invoice objects.

.. code-block:: html

    <list-queue-core>
        <cosmoz-data-nav
            items="[[ _getItems(visibleInvoices) ]]"
            id-list="[[ _getIdList(visibleInvoices) ]]">
 
:ref:`cosmoz-data-nav` gets two lists, one (optional) with ``items`` (where some items may be ``undefined`` to signal that they're missing/not fetched).
The other (optional) is ``idList`` which contains a corresponding list, but with just (unique) item ids in each post.
If :ref:`cosmoz-data-nav` finds an ``undefined`` item, it will fire a ``need-data`` event to signal that it needs data for the corresponding id in ``idList``:

.. code-block:: html

     <list-queue-core>
        <cz-apicall params="[[ _invoiceDetailsParams ]]" on-response="updateQueue">
        <cosmoz-data-nav id="dataNav" on-need-data="triggerDetailFetch">

.. code-block:: js

    // list-queue-core
    triggerDetailFetch: function (event, detail) {
        this._invoiceDetailsParams = {
            id: detail.id
        };
    },
    updateQueue: function (event, detail) {
        var response = detail.response,
            id = this.get(this._idPath, response);

        this._itemCache[id] = response;

        this.$.dataNav.fire('object-details-fetched', {
            id: id,
            object: response
        });
    }

1. The user navigates the :ref:`cosmoz-data-nav` items, which realizes it is missing an item 
2. :ref:`cosmoz-data-nav` fires a ``need-data`` event for the id
3. In ``<list-queue-core>``, the event sets new params for :ref:`cz-apicall` to fetch details, with triggers an :term:`XHR`
4. When :ref:`cz-apicall` finishes

    a) the detail info is saved to an ``_itemCache``
    b) list-queue-core fires an ``object-details-fetched`` event back to :ref:`cosmoz-data-nav` with detail info

.. note::

    The data-binding chain will keep its state intact, so any change anywhere in it will cause the dependant bindings 
    to update. For example, sorting the :ref:`cosmoz-omnitable` will feed a completely new list to :ref:`cosmoz-data-nav`.
    This creates mainly two issues:

        1. :ref:`cosmoz-data-nav` will (likely) request details for the first three items every time the user sorts, groups
        or filters the list, even though they maybe the same as before the action.
        For this reason, the ``_itemCache`` will cache details until another ``supplierInvoices`` list is fed to list-queue-core.
        
        2. Even with the cache, the :ref:`cosmoz-data-nav` can easily lose its index of the queue if the list is updated, when
        it needs to re-render the list and automatically ends up at index 1. This can be very frustrating for users if they were
        working somewhere a bit into the list.

        .. todo::

            How do we solve this best? Semi-persistent queue index? Handle array mutations?

“View/edit”-type views
~~~~~~~~~~~~~~~~~~~~~~

.. todo:: Document
