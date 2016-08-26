Transport Adapters
------------------

As of v1.0.0, Requests has moved to a modular internal design. Part of the
reason this was done was to implement Transport Adapters, originally
`described here`_. Transport Adapters provide a mechanism to define interaction
methods for an HTTP service. In particular, they allow you to apply per-service
configuration.

Requests ships with a single Transport Adapter, the :class:`HTTPAdapter
<requests.adapters.HTTPAdapter>`. This adapter provides the default Requests
interaction with HTTP and HTTPS using the powerful `urllib3`_ library. Whenever
a Requests :class:`Session <requests.Session>` is initialized, one of these is
attached to the :class:`Session <requests.Session>` object for HTTP, and one
for HTTPS.

Requests enables users to create and use their own Transport Adapters that
provide specific functionality. Once created, a Transport Adapter can be
mounted to a Session object, along with an indication of which web services
it should apply to.

::

    >>> s = requests.Session()
    >>> s.mount('http://www.github.com', MyAdapter())

The mount call registers a specific instance of a Transport Adapter to a
prefix. Once mounted, any HTTP request made using that session whose URL starts
with the given prefix will use the given Transport Adapter.

Many of the details of implementing a Transport Adapter are beyond the scope of
this documentation, but take a look at the next example for a simple SSL use-
case. For more than that, you might look at subclassing the
:class:`BaseAdapter <requests.adapters.BaseAdapter>`.

Example: Specific SSL Version
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The Requests team has made a specific choice to use whatever SSL version is
default in the underlying library (`urllib3`_). Normally this is fine, but from
time to time, you might find yourself needing to connect to a service-endpoint
that uses a version that isn't compatible with the default.

You can use Transport Adapters for this by taking most of the existing
implementation of HTTPAdapter, and adding a parameter *ssl_version* that gets
passed-through to `urllib3`. We'll make a Transport Adapter that instructs the
library to use SSLv3::

    import ssl

    from requests.adapters import HTTPAdapter
    from requests.packages.urllib3.poolmanager import PoolManager


    class Ssl3HttpAdapter(HTTPAdapter):
        """"Transport adapter" that allows us to use SSLv3."""

        def init_poolmanager(self, connections, maxsize, block=False):
            self.poolmanager = PoolManager(
                num_pools=connections, maxsize=maxsize,
                block=block, ssl_version=ssl.PROTOCOL_SSLv3)

.. _`described here`: http://www.kennethreitz.org/essays/the-future-of-python-http
.. _`urllib3`: https://github.com/shazow/urllib3