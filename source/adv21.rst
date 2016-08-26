.. _timeouts:

Timeouts
--------

Most requests to external servers should have a timeout attached, in case the
server is not responding in a timely manner. By default, requests do not time
out unless a timeout value is set explicitly. Without a timeout, your code may
hang for minutes or more.

The **connect** timeout is the number of seconds Requests will wait for your
client to establish a connection to a remote machine (corresponding to the
`connect()`_) call on the socket. It's a good practice to set connect timeouts
to slightly larger than a multiple of 3, which is the default `TCP packet
retransmission window <http://www.hjp.at/doc/rfc/rfc2988.txt>`_.

Once your client has connected to the server and sent the HTTP request, the
**read** timeout is the number of seconds the client will wait for the server
to send a response. (Specifically, it's the number of seconds that the client
will wait *between* bytes sent from the server. In 99.9% of cases, this is the
time before the server sends the first byte).

If you specify a single value for the timeout, like this::

    r = requests.get('https://github.com', timeout=5)

The timeout value will be applied to both the ``connect`` and the ``read``
timeouts. Specify a tuple if you would like to set the values separately::

    r = requests.get('https://github.com', timeout=(3.05, 27))

If the remote server is very slow, you can tell Requests to wait forever for
a response, by passing None as a timeout value and then retrieving a cup of
coffee.

::

    r = requests.get('https://github.com', timeout=None)

.. _`connect()`: http://linux.die.net/man/2/connect
