Application states
==================

App state
---------

.. todo:: Service workers.

.. todo:: Local storage.

.. todo:: User settings.

URL app state
-------------

The app state can be controlled by different parts of the URL in different ways.
It can be described as::

	https://<environment>.cosmoz.com/?<query parameters>#!/<hash (bang) parameters>#<hash hash parameters>

Consider this URL for example::

	https://app.cosmoz.com/?cpl=1.18.19#!/purchase/invoices/list-queue#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

Environment
^^^^^^^^^^^

The environment subdomain part (``app`` in the example) of the URL defines what
environment to use. This stick in the URL during the whole visit. There are
several to choose from:

* ``app`` - Production environment
* ``beta`` - Beta environment, used for development
* ``staging`` - Environment for staging, deprecated more or less

During development, make sure that the frontend configuration does not use the
production environment unless intended.

Query parameters
^^^^^^^^^^^^^^^^
Query parameters can control the loaded app state and is persistent during the
session unless intentionally changed.

``?cpl=1.18.19`` above will stick in the URL while navigating around the app,
and will be part of any links opened in new windows but is not guaranteed
to be the same across windows or sessions. (This example sets the node path so
if the user changes node it will be same same while navigating and persist
across page reloads.

Hash (bang) parameters
^^^^^^^^^^^^^^^^^^^^^^
hash parameters - ``#!/purchase/invoices/list-queue`` - contains the view to
load. This is the part (and anything after it) that is updated when switching
views and is not sent to the server hosting the frontend app.

Hash hash parameters
^^^^^^^^^^^^^^^^
Next is that hash hash parameters that configures a state for the specific view loaded::

	#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

This tracks the state of activated/selected tabs and how omnitables are
configured in terms of grouping, sorting, filtering.

This is to maintain a view-state across reloads and can also act as a
user-configured state for bookmarks.

Important is to make sure any hash hash parameters making use of this doesn't
conflict with other "namespaces" so right now the parameters are pretty
excessively long.

.. todo:: Find a suitable algorithm to shorten hash hash parameter keys while still making them (somewhat) readable.