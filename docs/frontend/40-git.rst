Git
---

Create a feature branch and push to Redmine for review.

.. _git-deployment:

Deployment
~~~~~~~~~~

``master`` branch will be deployed to https://staging.cosmoz.com on successful build on :ref:`jenkins`

``beta`` branch will be deployed to https://beta.cosmoz.com on successful build on :ref:`jenkins`

``prod`` branch will be deployed to https://app.cosmoz.com on successful build on :ref:`jenkins`

Merges and cherry-picks to ``beta`` and ``prod`` branches are done manually according to instance deployment schedules.

.. todo:: Pull requests

.. seealso::
    :ref:`github-git`