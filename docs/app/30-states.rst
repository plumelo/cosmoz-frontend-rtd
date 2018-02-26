Application states
==================

App state
---------

.. todo:: Service workers

.. todo:: local storage

.. todo:: user settings

URL app state
-------------

The app state can be controlled by different parts of the URL in different ways.
Consider:

``https://app.cosmoz.com/?cpl=1.18.19#!/purchase/invoices/list-queue#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate``

Query params
^^^^^^^^^^^^
Query params can control the loaded app state and is persistent during the session unless intentionally changed.

``?cpl=1.18.19`` above will stick in the URL while navigating around the app, and will be part of any links opened in new windows but is not guaranteed
to be the same across windows or sessions. (This example sets the node path so if the user changes node it will be same same while navigating and persist across
page reloads.

Hash (bang) params
^^^^^^^^^^^^^^^^^^
Next part is the hash params ``#!/purchase/invoices/list-queue`` which contains the view to load.
This is the part (and anything after it) that we update when switching views and is not sent to the server hosting the frontend app.

Hash hash params
^^^^^^^^^^^^^^^^
Next is that hash hash params that configures a state for the specific view loaded ``#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate``
This tracks the state of activated/selected tabs and how omnitables are configured in terms of grouping, sorting, filtering.
This is to maintain a view-state across reloads and can also act as a user-configured state for bookmarks.

Important is to make sure any hash hash params making use of this doesn't conflict with other "namespaces" so right now the params are pretty excessively long.

.. todo:: Find nice algorithm to shorten hash hash param keys while still making them (somewhat) readable.