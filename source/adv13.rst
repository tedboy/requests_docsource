.. _streaming-requests:

Streaming Requests
------------------

With :meth:`Response.iter_lines() <requests.Response.iter_lines>` you can easily
iterate over streaming APIs such as the `Twitter Streaming
API <https://dev.twitter.com/streaming/overview>`_. Simply
set ``stream`` to ``True`` and iterate over the response with
:meth:`~requests.Response.iter_lines()`::

    import json
    import requests

    r = requests.get('http://httpbin.org/stream/20', stream=True)

    for line in r.iter_lines():

        # filter out keep-alive new lines
        if line:
            print(json.loads(line))

.. warning::

    :meth:`~requests.Response.iter_lines()` is not reentrant safe.
    Calling this method multiple times causes some of the received data
    being lost. In case you need to call it from multiple places, use
    the resulting iterator object instead::

        lines = r.iter_lines()
        # Save the first line for later or just skip it

        first_line = next(lines)

        for line in lines:
            print(line)