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

	https://<environment subdomain>.cosmoz.com/?<query parameters>#!/<hash (bang) parameters>#<hash hash parameters>

Example::

	https://app.cosmoz.com/?cpl=1.18.19#!/purchase/invoices/list-queue#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

Environment subdomain
^^^^^^^^^^^^^^^^^^^^^

The environment subdomain part of the URL defines what environment to use. This
will stick in the URL during navigation and there are some to choose from:

* ``app`` - Production environment (used in the example)
* ``beta`` - Beta environment, for development
* ``demo`` - Demo environment, for demos
* ``staging`` - Staging environment, for development

Please note that the ``<environment subdomain>.cosmoz.com`` is replaced with
``localhost:3000`` during frontend development because the frontend then runs
locally. The backend does not however, so it is important to set the desired one
in ``app/cz.config.js`` using the ``backendBaseUri`` parameter.

Query parameters
^^^^^^^^^^^^^^^^
Query parameters can control the loaded app state and is
persistent during the session unless intentionally changed.

They stick in the URL while navigating around the app, and will be part of any
links opened in new windows but is not guaranteed to be the same across windows
or sessions.

The example - ``?cpl=1.18.19`` - sets the node path so if the user changes node
it will be same same while navigating and persist across page reloads.

Hash (bang) parameters
^^^^^^^^^^^^^^^^^^^^^^
Hash (bang) parameters defines the view to load. This is the part (and anything
after it) that is updated when switching views and is not sent to the server
hosting the frontend app. It is almost the same as the source path located under
the ``app/views`` directory in the repository root directory, only excluding
``.html`` at the end.

The parameter in the example - ``#!/purchase/invoices/list-queue`` - loads the
"Open invoices" view.

Hash hash parameters
^^^^^^^^^^^^^^^^^^^^
Hash has parameters configure states for the specific view that is loaded. This
is to maintain a view-state across reloads and can also act as a user-configured
state for bookmarks.

The given example tracks the state of activated/selected tabs and how omnitables
are configured in terms of grouping, sorting and filtering::

	#invoices-list-queue-core-tab=queue&invoices-list-core-table-groupOn&invoices-list-core-table-sortOn=dueDate

The ``hash-param`` attribute of :ref:`cosmoz-omnitable` and :ref:`cosmoz-tabs`
components specify how to name the hash hash parameter for these components,
which except for this naming handle the parameter reading and writing
themselves.

It is important is to make sure that any hash hash parameter making use of this
does not conflict with hash hash parameters in other views, therefore are the
naming of these excessively long at the moment as they not only tell the name of
the parameter but also in which view path they are located.

.. todo:: Find a suitable algorithm to shorten hash hash parameter keys while
          still making them (somewhat) readable.