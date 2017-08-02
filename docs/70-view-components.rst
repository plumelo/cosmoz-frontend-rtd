View components
===============

cz-\* components are not intended for open source publishing but
cosmoz-\* components are.

.. _cz-apicall::

cz-apicall
----------

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

Sometimes though, we might want to handle/mangle the data received
before forwarding to another component, and the best way to describe
this is to call the computing method at the input for the other
component, example:

.. code-block:: html

    <cz-apicall ... data="{{ supplierListData }}"></cz-apicall>
    <cosmoz-omnitable data="[[ _getSuppliers(supplierListData) ]] ...>...</cosmoz-omnitable>

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

.. _cosmoz-bottom-bar-view:

cosmoz-bottom-bar-view
----------------------

Meant to be a placeholder for a view, to provide a bottom bar with
actions whenever the user is scrolling up or reach the bottom.

https://github.com/Neovici/cosmoz-bottom-bar

.. todo:: link wc.org docs

.. _cosmoz-data-nav:

cosmoz-data-nav
---------------

Meant to navigate a list of objects..

.. todo:: Documentation

.. todo:: Move to public github

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

cosmoz-tab-cards
~~~~~~~~~~~~~~~~

Placeholder for tab-cards.

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

.. todo:: Move to public github

cz-history
----------

.. todo:: Documentation