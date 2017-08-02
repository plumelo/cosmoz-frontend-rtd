.. _github-git:

GitHub and Git
--------------

Basic git usage
~~~~~~~~~~~~~~~

http://rogerdudler.github.io/git-guide/

Repository configuration
~~~~~~~~~~~~~~~~~~~~~~~~

For each component repository::

    $ git config pull.rebase true
    $ git config user.name "Firstname Lastname"
    $ git config user.email "your.name@domain.tld"

.. note:: These settings can be made machine-wide by adding the ``--global`` option.

Submitting changes
~~~~~~~~~~~~~~~~~~

Use `whatever model <https://help.github.com/articles/about-collaborative-development-models/>`_ you have access to and
feel comfortable with, but make sure to use a `Pull Request <https://help.github.com/articles/about-pull-requests/>`_
approach unless otherwise instructed.

GitHub 2FA setup
~~~~~~~~~~~~~~~~

Be sure to activate two-factor authentication for GitHub:

    https://help.github.com/articles/securing-your-account-with-two-factor-authentication-2fa/

.netrc
~~~~~~

To avoid entering password when pushing to GitHub, use a `.netrc` file.

Set it up with GPG encryption:

    https://bryanwweber.com/writing/personal/2016/01/01/how-to-set-up-an-encrypted-.netrc-file-with-gpg-for-github-2fa-access/

.. seealso::

    :ref:`git-setup`