Compliance
----------

Requests is intended to be compliant with all relevant specifications and
RFCs where that compliance will not cause difficulties for users. This
attention to the specification can lead to some behaviour that may seem
unusual to those not familiar with the relevant specification.

Encodings
^^^^^^^^^

When you receive a response, Requests makes a guess at the encoding to
use for decoding the response when you access the :attr:`Response.text
<requests.Response.text>` attribute. Requests will first check for an
encoding in the HTTP header, and if none is present, will use `chardet
<http://pypi.python.org/pypi/chardet>`_ to attempt to guess the encoding.

The only time Requests will not do this is if no explicit charset
is present in the HTTP headers **and** the ``Content-Type``
header contains ``text``. In this situation, `RFC 2616
<http://www.w3.org/Protocols/rfc2616/rfc2616-sec3.html#sec3.7.1>`_ specifies
that the default charset must be ``ISO-8859-1``. Requests follows the
specification in this case. If you require a different encoding, you can
manually set the :attr:`Response.encoding <requests.Response.encoding>`
property, or use the raw :attr:`Response.content <requests.Response.content>`.