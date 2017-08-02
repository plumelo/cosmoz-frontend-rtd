View loading / switching
========================

View lifecycle events / aspects
-------------------------------

-  ``created()`` callback - called the first time the view is imported and
   created
-  ``ready()``, ``attached()`` callbacks - called everytime a view is injected
   (non-persisted, visited and revisited)
-  ``activate()`` callback - called everytime a view is visited, revisited,
   refreshed, persisted or not

View loading timeline
---------------------

1. State / client URL changes
2. :ref:`cosmoz-page-router` finds the route

   a. If route doesn’t exist, it is created ad-hoc

   b. If it is active already, jump to “activate” with new params

3. Fade out current view
4. :ref:`cosmoz-page-router` loads the route element

   a. If route element is not available/imported, fetch the import

      i. Also includes any non deduped, not loaded dependencies

   b. If import fetching takes > 300ms, display loading view message

   c. ``created()`` callback

5. :ref:`cosmoz-page-router` injects the element
6. The element template definition will trigger any ``auto`` :ref:`cz-apicall` elements

   a. If data fetching takes > 300ms, display loading message

7. Polymer/Web component lifecycle callbacks triggered

   a. (first load) ``ready()``

   b. (with non-persisted views) ``attached()``

8. Cosmoz view lifecycle callbacks triggered

   a. (only callback for persisted or refreshed views) ``activate()``

9. UNSPECIFIED EVENT - trigger fade-in of new view

View setup / activation
-----------------------

When views are loaded, any component-generic lifecycle callbacks will be
run, see https://www.polymer-project.org/1.0/docs/devguide/registering-elements.html#lifecycle-callbacks

The way right now to do any view setup on load is to just create a
``ready()`` callback with setup code. However, we plan to support persisted
views, and in those cases the ``ready()`` will only be run once, whereas
some kind of view-activation code needs to be run when re-visiting those
views.

To resolve this issue, :ref:`cz-application` injects the
``cz.behaviors.TemplateViewCommonBehavior`` to all views loaded, which calls
an ``activate()`` callback when activating a view.

So setup should be split up into ``ready()`` for one-time setup needs and
``activate()`` for every-load time things.