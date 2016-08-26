.. _custom-auth:

Custom Authentication
---------------------

Requests allows you to use specify your own authentication mechanism.

Any callable which is passed as the ``auth`` argument to a request method will
have the opportunity to modify the request before it is dispatched.

Authentication implementations are subclasses of :class:`AuthBase <requests.auth.AuthBase>`,
and are easy to define. Requests provides two common authentication scheme
implementations in ``requests.auth``: :class:`HTTPBasicAuth <requests.auth.HTTPBasicAuth>` and
:class:`HTTPDigestAuth <requests.auth.HTTPDigestAuth>`.

Let's pretend that we have a web service that will only respond if the
``X-Pizza`` header is set to a password value. Unlikely, but just go with it.

::

    from requests.auth import AuthBase

    class PizzaAuth(AuthBase):
        """Attaches HTTP Pizza Authentication to the given Request object."""
        def __init__(self, username):
            # setup any auth-related data here
            self.username = username

        def __call__(self, r):
            # modify and return the request
            r.headers['X-Pizza'] = self.username
            return r

Then, we can make a request using our Pizza Auth::

    >>> requests.get('http://pizzabin.org/admin', auth=PizzaAuth('kenneth'))
    <Response [200]>