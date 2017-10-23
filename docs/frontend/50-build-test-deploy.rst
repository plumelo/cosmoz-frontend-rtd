Continuous integration and continuous deployment
================================================

Application is setup for CI/CD with Travis at https://travis-ci.com/Neovici/cosmoz-frontend.

Continus integration
--------------------

A travis build is triggered when any the following occurs:

* a commit is pushed to branches master or demo
* a pull request is submitted
* a tag matching the following regexp /^v\d+\.\d+(\.\d+)?(-\S*)?$/, for example v3.0.1,  is pushed
* a tag is merged to branch prod

The build steps are the following:

#. install

   This step will install npm packages used for the build by using ``yarn install``.

   When npm packages have been installed, yarn will run ``polymer install``.

#. before_script

   This step will run eslint on the frontend sources.

#. script

   This step will run the build script.

   Depending on the branch, tag or PR being built, the script will determine the suitable build environment.

#. deploy

   Depending on the branch or tag being built, automatic deployment will occur. See below.

Continus deployment
-------------------

A travis build will be automatically deployed to the following environment:

* staging: for builds triggered by a commit to master branch
* demo: for builds triggered by a commit to demo branch 
* beta: for builds triggered by a tag matching the version regexp/
* prod: for build triggered by a tag being merged to prod.

Building and deploying the beta environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Manually
""""""""

::

    git tag -a vX.Y.Z -m "Version description"
    git push origin vX.Y.Z

The tag name must be a valid semantic version number prefixed with the 'v' letter.
Any other tag will not be built and deployed by Travis.

You may also use ``git push --follow-tags`` instead of specifying the tag name.

From the github web interface
"""""""""""""""""""""""""""""

Go the the github "new release" page at https://github.com/Neovici/cosmoz-frontend/releases/new

.. image:: github-beta-release.png

Fill the fields, ensuring the tag name follows the vX.Y.Z pattern, then click on "Publish release".

Building and and deploying the prod environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The production environment is built and deployed when a tag is merged to the prod branch.

If there are other commits than the merge commit, the build will fail and no deployment will be made.

Manually
""""""""

::

    git checkout prod
    git merge vX.Y.Z
    git push origin

From the github web interface
"""""""""""""""""""""""""""""

TODO: is it possible ?