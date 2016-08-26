Digest Authentication
---------------------

Another very popular form of HTTP Authentication is Digest Authentication,
and Requests supports this out of the box as well::

    >>> from requests.auth import HTTPDigestAuth
    >>> url = 'http://httpbin.org/digest-auth/auth/user/pass'
    >>> requests.get(url, auth=HTTPDigestAuth('user', 'pass'))
    <Response [200]>