.. module:: requests.models

JSON Response Content
---------------------

There's also a builtin JSON decoder, in case you're dealing with JSON data::

    >>> import requests

    >>> r = requests.get('https://api.github.com/events')
    >>> r.json()
    [{u'repository': {u'open_issues': 0, u'url': 'https://github.com/...

In case the JSON decoding fails, ``r.json()`` raises an exception. For example, if
the response gets a 204 (No Content), or if the response contains invalid JSON,
attempting ``r.json()`` raises ``ValueError: No JSON object could be decoded``.

It should be noted that the success of the call to ``r.json()`` does **not**
indicate the success of the response. Some servers may return a JSON object in a
failed response (e.g. error details with HTTP 500). Such JSON will be decoded
and returned. To check that a request is successful, use
``r.raise_for_status()`` or check ``r.status_code`` is what you expect.