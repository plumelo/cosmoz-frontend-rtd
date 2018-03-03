Versions and releases
=====================

To create a release on GitHub, see https://help.github.com/articles/creating-releases/

We use the common ``v1.2.3`` `semantic versioning <http://semver.org>`_ syntax.

When making a release, be sure to provide a QA/Testing level of information about the changes.

The easiest way to compile the list of changes (commits) is to go to the ``/releases`` page of a component, like https://github.com/Neovici/cosmoz-bottom-bar/releases
and look at the latest release. Beneath it, a line of information will show such as::

     nomego released this 19 days ago · 36 commits to master since this release

The number of commits will be a link to a page comparing the latest release tag with the master branch, listing all commits, such as::

    https://github.com/Neovici/cosmoz-bottom-bar/compare/v0.9.2...master

From this page, given that commit messages (titles) have been well written, it should be easy to summarize the development efforts made.

For a new release, the release title can be a major feature summary, a codename, or other fitting text.

The description should contain the major and minor changes listed, summarized from the commits made.

Changes driving versions
------------------------

Major = “breaking changes” – Increment MAJOR version when you have removed or changed a feature, and dependent modules will have to modified to be compatible with the new version.

Minor = “new feature” – Increment MINOR version when you have added a feature, but the module is backwards compatible.
This will be the effect of any (combination of) change(s) that is not safe to go directly to prod.

Patch = “bugfix” – Increment PATCH version when you have fixed a problem, but not broken or changed anything else.
Immediately ready for prod.

Cosmoz frontend will depend on a "caret range" for components (``^1.2.3``), automatically updating PATCH version changes on redeploys.

Version milestones
------------------

=======  =========
Version  Guideline
=======  =========
1.0      First stable version, Polymer 1.x support
1.20     Polymer 2-hybrid
1.40     Published to WebComponents.org
2.0      Polymer 2.x (1.x deprecated)
3.0      Polymer 3.x support
=======  =========