.. _session-objects:

Session Objects
---------------

The Session object allows you to persist certain parameters across
requests. It also persists cookies across all requests made from the
Session instance, and will use ``urllib3``'s `connection pooling`_. So if
you're making several requests to the same host, the underlying TCP
connection will be reused, which can result in a significant performance
increase (see `HTTP persistent connection`_).

A Session object has all the methods of the main Requests API.

Let's persist some cookies across requests::

    s = requests.Session()

    s.get('http://httpbin.org/cookies/set/sessioncookie/123456789')
    r = s.get('http://httpbin.org/cookies')

    print(r.text)
    # '{"cookies": {"sessioncookie": "123456789"}}'


Sessions can also be used to provide default data to the request methods. This
is done by providing data to the properties on a Session object::

    s = requests.Session()
    s.auth = ('user', 'pass')
    s.headers.update({'x-test': 'true'})

    # both 'x-test' and 'x-test2' are sent
    s.get('http://httpbin.org/headers', headers={'x-test2': 'true'})


Any dictionaries that you pass to a request method will be merged with the
session-level values that are set. The method-level parameters override session
parameters.

Note, however, that method-level parameters will *not* be persisted across
requests, even if using a session. This example will only send the cookies
with the first request, but not the second::

    s = requests.Session()

    r = s.get('http://httpbin.org/cookies', cookies={'from-my': 'browser'})
    print(r.text)
    # '{"cookies": {"from-my": "browser"}}'

    r = s.get('http://httpbin.org/cookies')
    print(r.text)
    # '{"cookies": {}}'


If you want to manually add cookies to your session, use the
:ref:`Cookie utility functions <api-cookies>` to manipulate
:attr:`Session.cookies <requests.Session.cookies>`.

Sessions can also be used as context managers::

    with requests.Session() as s:
        s.get('http://httpbin.org/cookies/set/sessioncookie/123456789')

This will make sure the session is closed as soon as the ``with`` block is
exited, even if unhandled exceptions occurred.


.. admonition:: Remove a Value From a Dict Parameter

    Sometimes you'll want to omit session-level keys from a dict parameter. To
    do this, you simply set that key's value to ``None`` in the method-level
    parameter. It will automatically be omitted.

All values that are contained within a session are directly available to you.
See the :ref:`Session API Docs <sessionapi>` to learn more.