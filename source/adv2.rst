.. _request-and-response-objects:

Request and Response Objects
----------------------------

Whenever a call is made to ``requests.get()`` and friends, you are doing two
major things. First, you are constructing a ``Request`` object which will be
sent off to a server to request or query some resource. Second, a ``Response``
object is generated once Requests gets a response back from the server.
The ``Response`` object contains all of the information returned by the server and
also contains the ``Request`` object you created originally. Here is a simple
request to get some very important information from Wikipedia's servers::

    >>> r = requests.get('http://en.wikipedia.org/wiki/Monty_Python')

If we want to access the headers the server sent back to us, we do this::

    >>> r.headers
    {'content-length': '56170', 'x-content-type-options': 'nosniff', 'x-cache':
    'HIT from cp1006.eqiad.wmnet, MISS from cp1010.eqiad.wmnet', 'content-encoding':
    'gzip', 'age': '3080', 'content-language': 'en', 'vary': 'Accept-Encoding,Cookie',
    'server': 'Apache', 'last-modified': 'Wed, 13 Jun 2012 01:33:50 GMT',
    'connection': 'close', 'cache-control': 'private, s-maxage=0, max-age=0,
    must-revalidate', 'date': 'Thu, 14 Jun 2012 12:59:39 GMT', 'content-type':
    'text/html; charset=UTF-8', 'x-cache-lookup': 'HIT from cp1006.eqiad.wmnet:3128,
    MISS from cp1010.eqiad.wmnet:80'}

However, if we want to get the headers we sent the server, we simply access the
request, and then the request's headers::

    >>> r.request.headers
    {'Accept-Encoding': 'identity, deflate, compress, gzip',
    'Accept': '*/*', 'User-Agent': 'python-requests/1.2.0'}