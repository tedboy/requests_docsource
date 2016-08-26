New Forms of Authentication
---------------------------

If you can't find a good implementation of the form of authentication you
want, you can implement it yourself. Requests makes it easy to add your own
forms of authentication.

To do so, subclass :class:`AuthBase <requests.auth.AuthBase>` and implement the
``__call__()`` method::

    >>> import requests
    >>> class MyAuth(requests.auth.AuthBase):
    ...     def __call__(self, r):
    ...         # Implement my authentication
    ...         return r
    ...
    >>> url = 'http://httpbin.org/get'
    >>> requests.get(url, auth=MyAuth())
    <Response [200]>

When an authentication handler is attached to a request,
it is called during request setup. The ``__call__`` method must therefore do
whatever is required to make the authentication work. Some forms of
authentication will additionally add hooks to provide further functionality.

Further examples can be found under the `Requests organization`_ and in the
``auth.py`` file.

.. _OAuth: http://oauth.net/
.. _requests_oauthlib: https://github.com/requests/requests-oauthlib
.. _Kerberos: https://github.com/requests/requests-kerberos
.. _NTLM: https://github.com/requests/requests-ntlm
.. _Requests organization: https://github.com/requests
