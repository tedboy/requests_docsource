.. _keep-alive:

Keep-Alive
----------

Excellent news — thanks to urllib3, keep-alive is 100% automatic within a session!
Any requests that you make within a session will automatically reuse the appropriate
connection!

Note that connections are only released back to the pool for reuse once all body
data has been read; be sure to either set ``stream`` to ``False`` or read the
``content`` property of the ``Response`` object.
