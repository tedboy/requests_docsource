.. _verification:

SSL Cert Verification
---------------------

Requests verifies SSL certificates for HTTPS requests, just like a web browser.
By default, SSL verification is enabled, and Requests will throw a SSLError if
it's unable to verify the certificate::

    >>> requests.get('https://requestb.in')
    requests.exceptions.SSLError: hostname 'requestb.in' doesn't match either of '*.herokuapp.com', 'herokuapp.com'

I don't have SSL setup on this domain, so it throws an exception. Excellent. GitHub does though::

    >>> requests.get('https://github.com')
    <Response [200]>

You can pass ``verify`` the path to a CA_BUNDLE file or directory with certificates of trusted CAs::

    >>> requests.get('https://github.com', verify='/path/to/certfile')

.. note:: If ``verify`` is set to a path to a directory, the directory must have been processed using
  the c_rehash utility supplied with OpenSSL.

This list of trusted CAs can also be specified through the ``REQUESTS_CA_BUNDLE`` environment variable.

Requests can also ignore verifying the SSL certificate if you set ``verify`` to False::

    >>> requests.get('https://kennethreitz.com', verify=False)
    <Response [200]>

By default, ``verify`` is set to True. Option ``verify`` only applies to host certs.

You can also specify a local cert to use as client side certificate, as a single
file (containing the private key and the certificate) or as a tuple of both
file's path::

    >>> requests.get('https://kennethreitz.com', cert=('/path/client.cert', '/path/client.key'))
    <Response [200]>

If you specify a wrong path or an invalid cert, you'll get a SSLError::

    >>> requests.get('https://kennethreitz.com', cert='/wrong_path/client.pem')
    SSLError: [Errno 336265225] _ssl.c:347: error:140B0009:SSL routines:SSL_CTX_use_PrivateKey_file:PEM lib

.. warning:: The private key to your local certificate *must* be unencrypted.
   Currently, Requests does not support using encrypted keys.