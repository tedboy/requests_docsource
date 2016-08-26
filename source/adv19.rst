.. _blocking-or-nonblocking:

Blocking Or Non-Blocking?
-------------------------

With the default Transport Adapter in place, Requests does not provide any kind
of non-blocking IO. The :attr:`Response.content <requests.Response.content>`
property will block until the entire response has been downloaded. If
you require more granularity, the streaming features of the library (see
:ref:`streaming-requests`) allow you to retrieve smaller quantities of the
response at a time. However, these calls will still block.

If you are concerned about the use of blocking IO, there are lots of projects
out there that combine Requests with one of Python's asynchronicity frameworks.
Two excellent examples are `grequests`_ and `requests-futures`_.

.. _`grequests`: https://github.com/kennethreitz/grequests
.. _`requests-futures`: https://github.com/ross/requests-futures