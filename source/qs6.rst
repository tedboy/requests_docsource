.. module:: requests.models

Raw Response Content
--------------------

In the rare case that you'd like to get the raw socket response from the
server, you can access ``r.raw``. If you want to do this, make sure you set
``stream=True`` in your initial request. Once you do, you can do this::

    >>> r = requests.get('https://api.github.com/events', stream=True)

    >>> r.raw
    <requests.packages.urllib3.response.HTTPResponse object at 0x101194810>

    >>> r.raw.read(10)
    '\x1f\x8b\x08\x00\x00\x00\x00\x00\x00\x03'

In general, however, you should use a pattern like this to save what is being
streamed to a file::

    with open(filename, 'wb') as fd:
        for chunk in r.iter_content(chunk_size):
            fd.write(chunk)

Using ``Response.iter_content`` will handle a lot of what you would otherwise
have to handle when using ``Response.raw`` directly. When streaming a
download, the above is the preferred and recommended way to retrieve the
content.