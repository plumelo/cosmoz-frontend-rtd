Git
===

.. _git-deployment:

.. seealso::
    Public elements - :ref:`github-git`

Pull Requests (PRs)
~~~~~~~~~~~~~~~~~~~

.. seealso:: https://help.github.com/articles/proposing-changes-to-your-work-with-pull-requests/

Pull Requests are the most efficient way to safely review and merge code.
To create a Pull Request, create a new branch (based off ``master``)::

    $ git checkout master
    $ git pull
    $ git checkout -b my-feature

Develop the feature and push the branch to GitHub::

    $ git push --set-upstream origin my-feature

Then head to https://github.com/Neovici/cosmoz-frontend/branches/yours and find your newly created branch,
and press the :guilabel:`New pull request` button.
Make sure the PR base is the ``master`` branch and describe the PR in the form.
Assign yourself the PR, and if known, assign one or more reviewers, labels and projects.
Press :guilabel:`Create pull request`.

.. seealso:: https://help.github.com/articles/creating-a-pull-request/


PR scope
--------

Try to keep a PR centered around one specific issue and don't solve multiple issues in the same PR.
The goal is to make the PRs as easy as possible to approve and merge, and avoid big, complex PRs that never get merged,
or eventually get merged despite issues becuase the PR-reviewal process gets too drawn out.
Also, the bigger a PR is, the longer it takes to re-review after requested changes are carried out.

When doing indentation changes, *never* combine this with code changes since it will be impossible to review.

When the code *touches* a code block or line that doesn't conform to coding style guidelines, use the opportunity
to adjust that/those lines. (ES6 arrow functions instead of ``function () {}.bind(this)`` for example.)
It could also include adjacent lines that will be included in the diff output.
This does *not* mean to find all occurrences in the file and replacing those.

Reviewing a PR
--------------

When reviewing a PR, as a guideline, consider the following for the new code:

* Is the code readable? If not, the preferred approach is to refactor it to be self-documenting, otherwise add comments.
* Is it performant?
* Does it conform to coding style guidelines?
* What kind of WCT tests could/should be designed around this?
* Are there any related scenarios that could be affected by this? This should be tested out.

.. todo:: More guidelines

.. note::
  On the "Conversation" tab of the PR, next to the merge-button, there are instructions on
  how to check out and test the PR locally with the CLI.

.. seealso::
  https://help.github.com/articles/about-pull-request-reviews/
  https://help.github.com/articles/reviewing-proposed-changes-in-a-pull-request/

Merging a PR
------------

If you are the only, or last, reviewer of a PR, you should also merge the PR.

:guilabel:`Rebase and merge` will add the commits directly on master.
This is a good starting point and should be used for any PR only containing one commit.
If there are more than one commit, they should make sense to have in the commit history individually.

:guilabel:`Squash and merge` will squash all commits into one.
This is a good approach for a PR that contains detail changes or a minor feature but has
grown in number of commits, maybe due to number of requested changes during review.
If it feels like the commits mostly reference the same thing and the individual commits would
add more noise than traceability to the git history, this would be a good candidate.

:guilabel:`Create a merge commit` will create a merge commit along with all the commits in the PR.
This is the default git behavior and makes sense if the PR is a bigger feature with several parts,
so they should be kept together as they affect the same feature, but they also make sense individually.

Deployment and branches
~~~~~~~~~~~~~~~~~~~~~~~


Artifacts / binaries
--------------------

Once the build promotion pipeline (integration -> alpha -> beta -> prod) has started, we
need a way to guarantee consistent builds across environments.

.. todo:: Define a way to do this - copy integration build output files to different environments?

   .. seealso:: yarn lock - https://yarnpkg.com/lang/en/docs/yarn-lock/

``master`` branch
-----------------

``master`` branch will get all updates indended to reach the production environment.
This should be done by creating a branch and a PR for code that is intended for next production release.

Commits added to the master branch will build, and on success, deploy to Cosmoz integration environment.
If integration tests succeed, the build will be promoted to the Alpha environment (https://alpha.cosmoz.com)
for Q/A and testing.

Once a release-ready state has been reached in Alpha, a tag is created for the release.
New tags will automatically be built and deployed to Beta environment (https://beta.cosmoz.com) which 
enables customer testing.

.. todo:: Lock down ``master`` branch for direct commits ?

``prod`` branch
---------------

During the next scheduled production release, unless reviewed beta-version has been rejected.
The beta-reviewed version/tag is merged to the prod branch and pushed, which causes a build and deploy
to Production environment (https://app.cosmoz.com).

``next`` branch
---------------

If a PR is experimental enough in nature to require testing that might not be completed in time for
production release, the branch of the PR should be merged to the ``next`` branch instead, which will
deploy individually to the experimental Next environment for thorough testing.
Changes to the PR will require additional merges of the source branch to next, and once the feature
is approved, the PR can be merged as well.