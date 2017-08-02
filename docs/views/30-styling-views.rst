Styling views
-------------

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