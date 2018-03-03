View overview
=============

Views are really just custom elements named after their URL, as
described in :ref:`url-view-structure` above.

Any view-generic behavior or function should be implemented in a common
Template/View behavior or maybe enriched (like somethings are today) by
the :ref:`cosmoz-page-router`.


.. _view-imports:

View imports
------------

All views should import the ``views/imports.html`` file which, in turn,
imports the most common things needed for a view.


View Behaviors
~~~~~~~~~~~~~~

``Cosmoz.CommonBehaviors``

.. todo:: Document view behaviors