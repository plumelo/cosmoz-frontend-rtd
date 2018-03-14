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

Example::

	https://app.cosmoz.com/?cpl=1.18.19#!/purchase/invoices/list-queue#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

Environment
^^^^^^^^^^^

The environment subdomain part - ``app`` - of the URL defines what
environment to use. This will stick in the URL during navigation and there are
some to choose from:

* ``app`` - Production environment
* ``beta`` - Beta environment, for development
* ``demo`` - Demo environment, for demos
* ``staging`` - Staging environment, for development

Query parameters
^^^^^^^^^^^^^^^^
Query parameters - ``?cpl=1.18.19`` - can control the loaded app state and is
persistent during the session unless intentionally changed.

They stick in the URL while navigating around the app, and will be part of any
links opened in new windows but is not guaranteed to be the same across windows
or sessions. The example sets the node path so if the user changes node it
will be same same while navigating and persist across page reloads.

Hash (bang) parameters
^^^^^^^^^^^^^^^^^^^^^^
Hash (bang) parameters - ``#!/purchase/invoices/list-queue`` - defines the view to
load. This is the part (and anything after it) that is updated when switching
views and is not sent to the server hosting the frontend app. It is almost the
same as the source path located under the ``app/views`` directory in the
repository root directory, only excluding ``.html`` at the end.

Hash hash parameters
^^^^^^^^^^^^^^^^^^^^
Hash has parameters configures states for the specific view loaded::

	#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

This for example tracks the state of activated/selected tabs and how omnitables
are configured in terms of grouping, sorting and filtering.

This is to maintain a view-state across reloads and can also act as a
user-configured state for bookmarks.

It is important is to make sure that any hash hash parameters making use of this
does not conflict with other "namespaces", therefore are these parameters
excessively long at the moment.

.. todo:: Find a suitable algorithm to shorten hash hash parameter keys while still making them (somewhat) readable.