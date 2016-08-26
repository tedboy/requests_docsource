Header Ordering
---------------

In unusual circumstances you may want to provide headers in an ordered manner. If you pass an ``OrderedDict`` to the ``headers`` keyword argument, that will provide the headers with an ordering. *However*, the ordering of the default headers used by Requests will be preferred, which means that if you override default headers in the ``headers`` keyword argument, they may appear out of order compared to other headers in that keyword argument.

If this is problematic, users should consider setting the default headers on a :class:`Session <requests.Session>` object, by setting :attr:`Session <requests.Session.headers>` to a custom ``OrderedDict``. That ordering will always be preferred.