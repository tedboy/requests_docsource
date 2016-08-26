.. _proxies:

Proxies
-------

If you need to use a proxy, you can configure individual requests with the
``proxies`` argument to any request method::

    import requests

    proxies = {
      'http': 'http://10.10.1.10:3128',
      'https': 'http://10.10.1.10:1080',
    }

    requests.get('http://example.org', proxies=proxies)

You can also configure proxies by setting the environment variables
``HTTP_PROXY`` and ``HTTPS_PROXY``.

::

    $ export HTTP_PROXY="http://10.10.1.10:3128"
    $ export HTTPS_PROXY="http://10.10.1.10:1080"

    $ python
    >>> import requests
    >>> requests.get('http://example.org')

To use HTTP Basic Auth with your proxy, use the `http://user:password@host/` syntax::

    proxies = {'http': 'http://user:pass@10.10.1.10:3128/'}

To give a proxy for a specific scheme and host, use the
`scheme://hostname` form for the key.  This will match for
any request to the given scheme and exact hostname.

::

    proxies = {'http://10.20.1.128': 'http://10.10.1.10:5323'}

Note that proxy URLs must include the scheme.

SOCKS
^^^^^

.. versionadded:: 2.10.0

In addition to basic HTTP proxies, Requests also supports proxies using the
SOCKS protocol. This is an optional feature that requires that additional
third-party libraries be installed before use.

You can get the dependencies for this feature from ``pip``:

.. code-block:: bash

    $ pip install requests[socks]

Once you've installed those dependencies, using a SOCKS proxy is just as easy
as using a HTTP one::

    proxies = {
        'http': 'socks5://user:pass@host:port',
        'https': 'socks5://user:pass@host:port'
    }

.. _compliance:
