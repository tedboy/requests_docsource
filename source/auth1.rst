Basic Authentication
--------------------

Many web services that require authentication accept HTTP Basic Auth. This is
the simplest kind, and Requests supports it straight out of the box.

Making requests with HTTP Basic Auth is very simple::

    >>> from requests.auth import HTTPBasicAuth
    >>> requests.get('https://api.github.com/user', auth=HTTPBasicAuth('user', 'pass'))
    <Response [200]>

In fact, HTTP Basic Auth is so common that Requests provides a handy shorthand
for using it::

    >>> requests.get('https://api.github.com/user', auth=('user', 'pass'))
    <Response [200]>

Providing the credentials in a tuple like this is exactly the same as the
``HTTPBasicAuth`` example above.


netrc Authentication
~~~~~~~~~~~~~~~~~~~~

If no authentication method is given with the ``auth`` argument, Requests will
attempt to get the authentication credentials for the URL's hostname from the
user's netrc file. The netrc file overrides raw HTTP authentication headers
set with `headers=`.

If credentials for the hostname are found, the request is sent with HTTP Basic
Auth.
