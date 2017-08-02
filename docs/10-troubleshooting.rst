Troubleshooting
===============

.. topic:: Logged out on page reload and console says error 401 all the time

    Symptom: You are logged out every time you reload the page, a little
    wait too long or clicks somewhere in the interface where a request is
    issued. The page reloads and you are back to login page.

    Possible cause: Your browser rejects the very important session storage
    cookie “cz3demowebapp-beta.azurewebsites.net”.

    Affects: Chromium, Google Chrome (also Safari?)

    Solution for Chromium: Check your cookie settings in the address bar -
    cookie icon there, go to “Show cookies and other website data…”, then
    “Blocked” tab, look for the cookie
    “cz3demowebapp-beta.azurewebsites.net” and remove it from the list by
    marking it and clicking “Allow”. You then need to close the popup dialog
    and reload the page.