View components
===============

Components used in Cosmoz views.


.. _cz-apicall:

cz-apicall
----------

http://localhost:3000/polymer/cz-apicall/index.html#cz-apicall

Basically a wrapper for ``iron-ajax``, apart from a few things:

-  Centrally configurable defaults, such as

   -  Content-type

   -  Client timeout

   -  Response default (json)

   -  auto (request)

-  URL basepath set to ``cz.options.backendBaseUri``
-  Automatic loading message handling

   -  With moduleInfo

Data mangling with cz-apicall
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Normally, the API should be designed so that we can bind the data
property of the ``cz-apicall`` instance as input for another component, like
:ref:`cosmoz-omnitable`.

Even though it should be avoided, we might sometimes want to handle/mangle the data received
before forwarding to another component, and the best way to describe
this is to call the computing method at the input for the other
component, example:

.. code-block:: html

    <cz-apicall data="{{ supplierListData }}"></cz-apicall>
    <cosmoz-omnitable data="[[ _getSuppliers(supplierListData) ]]"></cosmoz-omnitable>

This will reduce the need of a computed property which would mean “one
more logic step to follow” and also highlight that the data property for
:ref:`cosmoz-omnitable` is one way since any updates from :ref:`cosmoz-omnitable` will
be lost.

API call parameters
~~~~~~~~~~~~~~~~~~~

``myItemsOnly`` (bool)
^^^^^^^^^^^^^^^^^^^^^^

``myItemsOnly`` is a generic parameter that should be sent whenever the
:term:`Swagger` API documentation mentions MyItemsOnly in Implementation Notes.

The value to send is the value of ``cz.state.myItemsOnly``, controlled by
the toggle in the right menu.

This should be present as an argument to the computing function of the
API call parameters.

``pathLocator`` (string)
^^^^^^^^^^^^^^^^^^^^^^^^

``pathLocator`` should be sent for any API call requesting it.

The value to send is the value of ``cz.state.currentLocationPath``,
controlled by the treenode navigator in the right menu.

This should be present as an argument to the computing function of the
API call parameters.

Sample:

.. code-block:: html

    <cz-apicall
        api="api/supplier-invoices/for-approval"
        needs-params
        params="[[ _computeSupplierInvoiceParams(cz.state.currentLocationPath, cz.state.myItemsOnly) ]]"
        loading-message="[[ _('Fetching invoices list', t) ]]"
        data="{{ supplierInvoices }}">
    </cz-apicall>

.. code-block:: js

    _computeSupplierInvoiceParams: function (pathLocator, myItemsOnly) {
        return {
            approvableByMe: true,
            myItemsOnly: myItemsOnly,
            pathLocator: pathLocator,
            recursive: true
        };
    },

Explanation

-  ``needs-params`` makes sure that the call will not be executed before
   ``params`` is something else than ``undefined``

   -  ``_computeSupplierInvoiceParams()`` must run

-  The compute method ``_computeSupplierInvoiceParams()`` will not be run
   until all parameters are something else than undefined

   -  The ``cz.state`` properties must be defined

-  When ``params`` changes, the api-call will be executed again, refreshing
   the data, and re-rendering any part of the view that uses it
-  ``params`` will change when the user selects another branch in the right
   menu, or toggles the prioritization of own items

.. note::

    By default, ``cz-apicall`` will fire as soon as it's ready, which likely isn't the intent.
    
    For ``GET``-requests (and some ``POST``), this usually implies setting ``params`` first, and to make it fire when ``params``
    are set, use the ``needs-params`` property. (Recommended approach)
    
    For other ``POST`` calls that might require user input and should be triggered on a specific event, use
    ``no-auto`` and manually call ``generateRequest()`` on the element when it should be fired, much like ``iron-ajax``.


.. _cz-apicall-batch:

cz-apicall-batch
----------------

http://localhost:3000/polymer/cz-apicall/index.html#cz-apicall-batch


.. _cosmoz-bottom-bar:

cosmoz-bottom-bar
-----------------

https://www.webcomponents.org/element/neovici/cosmoz-bottom-bar/elements/cosmoz-bottom-bar


.. _cosmoz-bottom-bar-view:

cosmoz-bottom-bar-view
----------------------

https://www.webcomponents.org/element/neovici/cosmoz-bottom-bar/elements/cosmoz-bottom-bar-view


.. _cosmoz-data-nav:

cosmoz-data-nav
---------------

http://localhost:3000/polymer/cosmoz-data-nav/index.html

.. todo:: Move to public github

.. seealso:: :ref:`view_type_list_queue`

.. _cosmoz-tabs:

cosmoz-tabs
-----------

Component to provide information in different sections, for desktop
views in tabs and for mobile views as cards.

.. todo:: Documentation

.. todo:: Move to public github

cosmoz-tabs
~~~~~~~~~~~

Main component, meant as a placeholder for the different tabs.

cosmoz-tab
~~~~~~~~~~

Will in desktop mode represent a tab, and in mobile mode represent a
card, unless it contains a cosmoz-tab-cards element.

.. _cosmoz-tab-card:

cosmoz-tab-card
~~~~~~~~~~~~~~~

Will be a fixed-width card on desktop to enable multiple cards
horizontally.

Will be a card on mobile.

``row`` class
~~~~~~~~~~~~~

The shared CSS class ``row`` should be used for divs in :ref:`cosmoz-tab-card`
components to provide key/value rows.

.. _cosmoz-omnitable:

cosmoz-omnitable
----------------

Responsive, flexible data grid / table solution for listing/sorting/filtering/grouping data.

https://github.com/Neovici/cosmoz-omnitable

.. todo:: Documentation

cz-history
----------

.. todo:: Documentation