.. _github-git:

GitHub and git
==============

GitHub is a web-based hosting service for version control that hosts the source
code and git is the version control system used on GitHub to track it.

For more information on how to setup git, please refer to the :ref:`git-setup`
chapter.

Basic git usage
---------------

For a simple and fast on guide how to use git you may look at
`git - the simple guide <http://rogerdudler.github.io/git-guide/>`_.

There are also `several graphical frontends <https://git-scm.com/downloads/guis>`_
for git as an alternative to command line interaction.

Configuration of git repositories
---------------------------------

When you have created or cloned a component repository you need to make sure
that the current settings for it are as desired.

For each component repository you need to configure it like this::

    $ git config pull.rebase true
    $ git config user.name "Firstname Lastname"
    $ git config user.email "your.name@domain.tld"

.. note::
    These settings can be made machine-wide by adding the ``--global`` option
    to each of them.

.. _github-submitting-changes:

Enable two-factor authentication setup for GitHub
-------------------------------------------------

Two-factor authentication (2FA) on GitHub is a security process for user
authentication through two combined methods, one that is a password and the
other through an app that is installed on a smartphone device for.

Be sure to activate `two-factor authentication for GitHub
<https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/>`_
as described in the help documentation for it.

Command line two-factor authentication for GitHub
-------------------------------------------------

Two-factor authentication makes the contribution process safer, but it also
means that it is no longer possible to use the regular GitHub password to
login to it at the command line.

It is possible to enable two-factor authentication for this too by creating a
``.netrc`` file.

For more information on how to do this, please see a guide on how to setup `GPG
encryption <https://bryanwweber.com/writing/personal/2016/01/01/how-to-set-up-an-encrypted-netrc-file-with-gpg-for-github-2fa-access/>`_.

Submitting changes to GitHub
----------------------------

Use `whatever development model <https://help.github.com/articles/about-collaborative-development-models/>`_
you have access to and feel comfortable with.

But make sure to use a `Pull Request <https://help.github.com/articles/about-pull-requests/>`_
approach unless instructed otherwise.

In summary, create a branch to commit the changes to, keep it updated by rebases
based on the master branch and when it is ready to merge with the master branch
then make a pull request and assign appropriate reviewers to approve it.