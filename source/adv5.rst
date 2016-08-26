.. _ca-certificates:

CA Certificates
---------------

By default, Requests bundles a set of root CAs that it trusts, sourced from the
`Mozilla trust store`_. However, these are only updated once for each Requests
version. This means that if you pin a Requests version your certificates can
become extremely out of date.

From Requests version 2.4.0 onwards, Requests will attempt to use certificates
from `certifi`_ if it is present on the system. This allows for users to update
their trusted certificates without having to change the code that runs on their
system.

For the sake of security we recommend upgrading certifi frequently!

.. _HTTP persistent connection: https://en.wikipedia.org/wiki/HTTP_persistent_connection
.. _connection pooling: https://urllib3.readthedocs.io/en/latest/pools.html
.. _certifi: http://certifi.io/
.. _Mozilla trust store: https://hg.mozilla.org/mozilla-central/raw-file/tip/security/nss/lib/ckfw/builtins/certdata.txt