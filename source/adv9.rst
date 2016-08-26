.. _chunk-encoding:

Chunk-Encoded Requests
----------------------

Requests also supports Chunked transfer encoding for outgoing and incoming requests.
To send a chunk-encoded request, simply provide a generator (or any iterator without
a length) for your body::

    def gen():
        yield 'hi'
        yield 'there'

    requests.post('http://some.url/chunked', data=gen())

For chunked encoded responses, it's best to iterate over the data using
:meth:`Response.iter_content() <requests.Response.iter_content>`. In
an ideal situation you'll have set ``stream=True`` on the request, in which
case you can iterate chunk-by-chunk by calling ``iter_content`` with a ``chunk_size``
parameter of ``None``. If you want to set a maximum size of the chunk,
you can set a ``chunk_size`` parameter to any integer.