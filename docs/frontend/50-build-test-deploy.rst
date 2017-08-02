Application deployment
----------------------

Application is setup for :term:`CI`/:term:`CD` through :ref:`jenkins`.

This is managed through git :ref:`git-deployment`.


.. _jenkins:

Jenkins
~~~~~~~

Jenkins is responsible for building our different git branches.

Pipeline setup is to:

#. bower install
#. gulp

    #. vulcanize

#. run tests
#. deploy on success

.. todo:: Review Pipeline

.. todo::

    ``polymer build``

        With ES6 transpiling - Google Closure?

    ``polymer test``