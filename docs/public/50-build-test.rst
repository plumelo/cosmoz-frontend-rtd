Automatic testing and building
==============================

Travis-CI
---------

Travis-CI is a service that allows running unit tests. It's presented by a
little badge in the GitHub repository that tells the build status.

To begin the installation of it, start by installing Ruby including header files
which also will install RubyGems package manager (``gem``). Then install
Travis-CI using RubyGems.

Debian / Ubuntu:

    .. note::
        Please notice that the **gem** package manager and not
        **apt** is used to install Travis-CI. Using apt results in that a completely
        different and not related software gets installed. Make sure you use gem for
        this installation.

    Install Ruby followed by Travis-CI::

        $ sudo apt install ruby ruby-dev
        $ sudo gem install travis

Windows:

    .. note::
        Windows Vista or later is required to install the required version of
        Ruby. It does not work to install older versions of Ruby to get around
        this because Travis-CI requires a recent version.

    Visit the `Ruby installer webpage <https://rubyinstaller.org/>`_ and
    download the suggested version (in bold). Then run the installer.

    In the installation wizard check *Use UTF-8 as default external encoding*.

    At the end of the setup wizard you can choose to *Run ridk install to
    install MSYS2 and development toolchain.* This is optional and not
    neccessary for Travis-CI, uncheck it if you want to save time and disk
    space.

    Open a command window and run::

        gem install travis

    Accept firewall message.

.. todo:: Document

    https://www.jamiestarke.com/2015/06/10/continuous-integration-polymer-web-component-tester-travis-ci/

Travis-CI + Sauce Labs
----------------------

Sauce Labs allows testing on multiple browsers in different virtual machines.
This integration between Travis-CI and Sauce labs allows testing components on
multiple browsers.

.. note::
    There is a `Youtube video <https://www.youtube.com/watch?v=afy_EEq_4Go>`_
    describing the installation procedure mentioned here.

Setting up a Travis-CI account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go to `Travis-CI <https://travis-ci.org/>`_ webpage and create a Travis-CI by
signing in with the GitHub credentials.

Login and then go to the account name in the top right and go down to
``Accounts``. Go down in the list of repositories and enable the repository for
the desired component by clicking on the button to the left of it.

This links Travis-CI to the GitHub repository, so when contents are pushed to
GitHub, then GitHub will communicate with Travis-CI.

Setting up a Sauce Labs account
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Go to `Sauce Labs Open Sauce <https://saucelabs.com/open-source>`_ webpage and
create an account there too.

After creating an account you will be presented with a dashboard page. Go down
to the right, and click on your account name, then go to user settings. On the
bottom of the page is a access key. Note it.

Sauce Labs web browser settings file
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To find out settings for what browsers to test go to the `Sauce Labs
documentation <https://wiki.saucelabs.com/display/DOCS/Test+Configuration+Options#TestConfigurationOptions-RequiredSeleniumTestConfigurationSettings>`_.

Go to the `web components tester
<https://github.com/Polymer/web-component-tester#plugins>`_ website and down to
the Plugins section.

Web components tester is shipped with a Sauce Labs plugin. Copy the example JSON
there and paste it into a new file named ``wct.conf.json`` in the root of the
repository.

Fill in the ``browsers`` section with the selected browsers from the Sauce Labs
documentation earlier mentioned.

Travis-CI settings file
~~~~~~~~~~~~~~~~~~~~~~~

Go to the `Polymer Tools - Travis <https://github.com/googlearchive/tools/tree/master/travis>`_
webpage and download ``sample_travis_with_sauce.yml``, save it as ``travis.yml``
in the root of the repository.

Open the file and note the following lines - edit them if necessary:

- The ``addons`` section tells Travis-CI what browsers to install locally.
- The ``before-script`` contain commands that are going to run before the test
  itself, these prepare the virtual machine.
- The ``script`` section runs the test, using ``xvfb-run wct`` which runs the
  web component tester locally on Travis-CI. These will test the browsers
  locally installed in the ``addons`` section earlier mentioned.

When testing in Travis-CI only local browsers should be used. To enable that,
edit this line::

    - xvfb-run wct

so it looks like this::

    - xvfb-run wct --skip-plugin sauce

For the opposite when testing against Sauce Labs, then only the list of browsers
defined in the configuration should be used. Therefore edit the if section::

    - if [ "${TRAVIS_PULL_REQUEST}" = "false" ]; then wct -s 'default'; fi

so it looks like this::

    - if [ "${TRAVIS_PULL_REQUEST}" = "false" ]; then wct --skip-plugin-local; fi

Open a terminal and run this to install the Travis-CI gem::

	$ gem install travis

Then run this to set the username and access key in the ``travis.yml`` file::

	$ travis encrypt SAUCE_USERNAME=<sauce labs username> --add
	$ travis encrypt SAUCE_ACCESS_KEY=<sauce labs access key> --add

Open the ``travis.yml`` if you like to and verify that they are there.

Test the tests
~~~~~~~~~~~~~~

Make a first commit and push to initialize the integration::

	$ git add .
	$ git commit -m "Adding Travis-CI support."
	$ git push

Go back to Travis-CI webpage to display the output of the test. First comes the
local browsers, and in a little while the browsers tested on Sauce Labs.