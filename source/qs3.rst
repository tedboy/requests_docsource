.. module:: requests.models

Response Content
----------------

We can read the content of the server's response. Consider the GitHub timeline
again::

    >>> import requests

    >>> r = requests.get('https://api.github.com/events')
    >>> r.text
    u'[{"repository":{"open_issues":0,"url":"https://github.com/...

Requests will automatically decode content from the server. Most unicode
charsets are seamlessly decoded.

When you make a request, Requests makes educated guesses about the encoding of
the response based on the HTTP headers. The text encoding guessed by Requests
is used when you access ``r.text``. You can find out what encoding Requests is
using, and change it, using the ``r.encoding`` property::

    >>> r.encoding
    'utf-8'
    >>> r.encoding = 'ISO-8859-1'

If you change the encoding, Requests will use the new value of ``r.encoding``
whenever you call ``r.text``. You might want to do this in any situation where
you can apply special logic to work out what the encoding of the content will
be. For example, HTTP and XML have the ability to specify their encoding in
their body. In situations like this, you should use ``r.content`` to find the
encoding, and then set ``r.encoding``. This will let you use ``r.text`` with
the correct encoding.

Requests will also use custom encodings in the event that you need them. If
you have created your own encoding and registered it with the ``codecs``
module, you can simply use the codec name as the value of ``r.encoding`` and
Requests will handle the decoding for you.