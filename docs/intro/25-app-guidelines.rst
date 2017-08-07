Application guidelines
======================

We will define and design our core components, views, functions and features
based on Cosmoz standards, reusability and our own vision of our product future and scope.


Automation and efficiency
~~~~~~~~~~~~~~~~~~~~~~~~~

Always design with automation in mind.
Assume that an automatic process is in place and that users only will be interested in deviations.
To handle deviations, see if there's a way to do it with :term:`assisted automation`.
If not, see if there's a possiblity to do mass-updates to handle more than one deviation at a time.
As a last resort, handle deviations one by one.


AI, machine learning, user teaching
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

At any time a repeatable action is performed, we should consider asking the user to create a rule.
Instead of separating normal application actions and administration, a lot of things can be created from proper contexts.


Simplicity
~~~~~~~~~~

The user interface should be simple and straigh-forward enough to explain itself.
The more manuals, wizards, tooltips and training we need, the bigger we fail.


Specificity
~~~~~~~~~~~

Views should be as specific as possible to make actions as straight-forward as possible to carry out.
Also, this makes mobile view design easier when less components need to fit.


Device agnostic
~~~~~~~~~~~~~~~

Not only should it work on all modern web platforms and devices,
but we will also not limit functionality in any way because of the device used.

100% Cosmoz - everywhere.


Customizability
~~~~~~~~~~~~~~~

To enable full customizability for customers, we will create customer-specific views to 
cater to their exact and specific needs.
This will ensure that we never compromise neither core Cosmoz features and design nor customer experience and efficiency.


Challenging
~~~~~~~~~~~ 

We should never fall into old habits but challenge ourselves to see where we can improve our workflows, UI, UX, etc.


Performant
~~~~~~~~~~

We will never accept bad performance, not for backend processer and not for UI responsiveness.
Use the platform to get closer to the metal and enable a performant experience for low-end devices.
Use best practices for lazy loading, perceived performance, service workers, etc.


Exact UI state
~~~~~~~~~~~~~~

We can not assume things like:

    | "This request will finish before the user notices."

We can not blame user phone network latency even if the user goes into airplane mode.
The UI should handle any environment and inform the user accordingly.
If a request is slow, we will inform the user with progress bars, spinners or text before the user gets frustrated.
Also, when performing actions we will not enable the user to spam any action, so any such interactive elements should be disabled accordingly.