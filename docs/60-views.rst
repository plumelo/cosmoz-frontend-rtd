Application views
=================

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

View loading / switching
------------------------

View lifecycle events / aspects
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

-  ``created()`` callback - called the first time the view is imported and
   created
-  ``ready()``, ``attached()`` callbacks - called everytime a view is injected
   (non-persisted, visited and revisited)
-  ``activate()`` callback - called everytime a view is visited, revisited,
   refreshed, persisted or not

View loading timeline
~~~~~~~~~~~~~~~~~~~~~

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

Properties
----------

title
~~~~~

If present, :ref:`cz-application` will update the application title with this value.

Since this should be translated, it needs to be computed somehow. 


Example:

.. code-block:: js

    properties: {
        title: {
            type: String,
            computed: '_("Profile", t)'
        }
    },

Shared CSS-styles for views
---------------------------

``app/css/app/shared-styles.html`` contains a few shared styles and helpers to
make views look uniform.

These are recurring styling helpers that are minor
enough to not warrant a complete custom element but big enough to be
shared throughout the application.

To activate them, the view needs a ``<style include="shared-styles"></style>`` tag:

.. code-block:: html

    <dom-module>
        <template>
            <style include="shared-styles"></style>
            …
        </template>
        …
    </dom-module>

.. _page-header:

``page-header``
~~~~~~~~~~~~~~~

A top-level header within a view to display item core values, left
outside the scroller of :ref:`cosmoz-bottom-bar-view`, if present to stay in
view during scroll.

Typical usage
^^^^^^^^^^^^^

.. code-block:: html

    <template>
        <style include="shared-styles"></style>
        <paper-material cross-fade z="1" class="page-header">
            <cz-letterball background-color="#a9aa32" letter="U"></cz-letterball>
            <div>
                <h3>User name</h3>
                <div>
                    <div class="error">Disabled</div>
                </div>
            </div>
        </paper-material>
        <cosmoz-bottom-bar-view class="flex">
            ...

Notable is that this helper structure needs to be exactly like above to
work as expected since it’s based on CSS rules like ``.page-header >
div:first-of-type > div:first-of-type > div:first-of-type``.

The innermost div currently support a complimentary ``error`` class to
highlight errors.

``page-sub-header``
~~~~~~~~~~~~~~~~~~~

Similar to :ref:`page-header`, this sub header allows for two additional
information pieces that are commonly placed within the
:ref:`cosmoz-bottom-bar-view` scroller to disappear as scrolling starts, but is
used in combination with page-header above.

Typical usage
^^^^^^^^^^^^^

.. code-block:: html

    <cosmoz-bottom-bar-view class="flex">
        <div class="cosmoz-bottom-bar-scroll">
            <div class="page-sub-header">
                <div>User text</div>
                <div>User text2</div>
            </div>

Different types of views
------------------------

Cosmoz has a few generic types of views that are recurring:

"\*-core"-type views
~~~~~~~~~~~~~~~~~~~~~~

“View/edit”-type views
~~~~~~~~~~~~~~~~~~~~~~

“List”-type views
~~~~~~~~~~~~~~~~~

“Add”-type views
~~~~~~~~~~~~~~~~

View Behaviors
~~~~~~~~~~~~~~

Cosmoz.CommonBehaviors