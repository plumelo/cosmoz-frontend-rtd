``cz-application``
==================

.. _cosmoz-page-router:

cosmoz-page-router
------------------

``cosmoz-page-router`` is in responsible for showing different views
within itself based on the current route activated. It support different
kind of views like inline templates, etc.

:ref:`cz-application` controls the behavior of ``cosmoz-page-router`` very much and
reacts to a lot of different events emitted by ``cosmoz-page-router``.

The two elements in combination handles

-  Ad-hoc routing (no need to register all used URLs)
-  State change (URL changed in browser address bar)

   -  :ref:`cz-application` might intercept some URL-changes to redirect based on paths, usernames or whatever

-  Route loading / fetching

   -  :ref:`cz-application` will use ``moduleInfo`` to show this (with a delay)

-  Import errors info / template not found info
-  View behavior enrichment
-  Setting application view title based on view title property
-  Vulcanized views

.. _url-view-structure:

URL / View structure
--------------------

Currently, we use client-side hash URLs.

If the user/client navigates to ``#!/purchase/invoices/attest-queue``

1. ``cosmoz-page-router`` will try to fetch ``urlPrefix + ‘/purchase/invoices/attest-queue’ + fileSuffix`` with an HTML import.

   a. ``urlPrefix`` is set to ``views`` for cosmoz3-frontend and ``fileSuffix`` is left as default ``.html`` for now, resulting in ``views/purchase/invoices/attest-queue.html``

   b. if vulcanized, this will be overridden as ``views/cz-views.vulcanized.html`` for all views

2. Once loaded, ``cosmoz-page-router`` will try to create an element with that name, ``/`` replaced with ``-``, resulting in ``purchase-invoices-attest-queue``

   .. warning:: Don’t name view elements/URLs with capital letters - use ``attest-queue``, not ``attestQueue``

3. Once imported and attached, it will be activated through standard ``ready()`` function or through ``activate()`` function to support persisted
   views

.. _cz-mainmenu:

cz-mainmenu
-----------

If a menu entry is needed, add it to ``polymer/cz-mainmenu/cz-mainmenu-menus.js``.

Optionally, add a required function needed for it to be displayed.

.. _cosmoz-viewinfo:

cosmoz-viewinfo
---------------

cosmoz-viewinfo provides a convenience object with “view info”, which
will convey if we’re rendering for mobile, tablet or desktop.
(``viewInfo.mobile``, ``viewInfo.tablet`` and ``viewInfo.desktop`` boolean
properties).

An important difference to the usual responsiveness approaches is that
this is measured from the ``cosmoz-viewinfo`` (singleton) element and not
from the window size, so hiding the left or right drawer will affect the
available space for the view without resizing the window.

To be able to use this convenience object, the component or view must
use the ``Cosmoz.ViewInfoBehavior`` behavior.

The ``cz`` namespace
--------------------------------------

Even though the ``cz`` namespace gets less and less relevant, it will
probably never get completely removed.

Therefore, it’s implemented as a shared object by using the
``cz.behaviors.Template`` behavior in a component or view. This allows the
component or view to observe or bind to any cz.\* property.

.. note::
      When using this behavior, the global ``cz`` is available as ``this.cz``,
      which is the preferred way to use it and might enable dropping the global completely.

Important paths:

-  ``cz.boot`` - boot information from backend after login
-  ``cz.options`` - frontend/backend URLs

Translations
------------

Translations are handled by the cosmoz-i18next component, which is a
component wrapper and translation behavior for the i18next library.

.. _cosmoz-i18next:

cosmoz-i18next
~~~~~~~~~~~~~~

Should be a singleton component (right now in :ref:`cz-start`) to interface the i18next library.

See https://github.com/Neovici/cosmoz-i18next

``Cosmoz.TranslatableBehavior``
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Behavior used by any component/view needing translations.

This provides gettext-like functions to translate and also an observed t
object in case language changes and text needs to be re-rendered.


Theming
-------

Web Components and Shadow DOM solve the issue of unwanted theming
because of non-unique CSS classes or IDs, but present an issue at the
same time with theming of components.

Polymer has presented a solution to this with custom properties where
elements can expose properties to be themed, or elements within the
component to apply mixins to, see official documentation at:

      https://www.polymer-project.org/1.0/docs/devguide/styling.html

Custom properties
~~~~~~~~~~~~~~~~~

As far as Cosmoz component theming goes, we should never hard code any
colors into the components themselves, but rather use descriptive custom
properties that begin with the component name.

The component should primarily honor this property but should also try
pick a suitable, as generic as possible, secondary property.

For example, for cosmoz-bottom-bar, the background color of the
component could be specified with::

      background-color: var(--cosmoz-bottom-bar-background-color, --primary-background-color);

See https://www.polymer-project.org/1.0/docs/devguide/styling.html#custom-css-properties

Custom element styling
~~~~~~~~~~~~~~~~~~~~~~

But, the more traditional way of theming elements also applies to custom
elements and should be the more straight-forward way of theming.

Things like::

      cosmoz-bottom-bar {
            background-color: red;
      }

      cosmoz-bottom-bar.bluetype {
            background-color: blue;
      }

This is preferable when component design allows it. It should also
override any custom properties?

However, it would only work within the parent custom element, such as
our views, since these kind of rules can’t penetrate down through custom
component encapsulated DOM structures.

.. warning:: ``/deep/`` and ``::shadow`` should not be used

Themes
~~~~~~

In the ``app/themes`` directory there are different themes that can be
loaded, taken from https://polymerthemes.com.

These themes should really be split up - custom properties value
definitions can be put here, but custom element styling like above
should be put into the shared-styles shared styling.

Right now, a ``cosmoz3-base`` theme is always imported with base theming.

.. warning:: When changing themes in profile-page, a theme can not be loaded twice without reloading the app. 