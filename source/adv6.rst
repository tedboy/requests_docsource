.. _body-content-workflow:

Body Content Workflow
---------------------

By default, when you make a request, the body of the response is downloaded
immediately. You can override this behaviour and defer downloading the response
body until you access the :attr:`Response.content <requests.Response.content>`
attribute with the ``stream`` parameter::

    tarball_url = 'https://github.com/kennethreitz/requests/tarball/master'
    r = requests.get(tarball_url, stream=True)

At this point only the response headers have been downloaded and the connection
remains open, hence allowing us to make content retrieval conditional::

    if int(r.headers['content-length']) < TOO_LONG:
      content = r.content
      ...

You can further control the workflow by use of the :meth:`Response.iter_content() <requests.Response.iter_content>`
and :meth:`Response.iter_lines() <requests.Response.iter_lines>` methods.
Alternatively, you can read the undecoded body from the underlying
urllib3 :class:`urllib3.HTTPResponse <urllib3.response.HTTPResponse>` at
:attr:`Response.raw <requests.Response.raw>`.

If you set ``stream`` to ``True`` when making a request, Requests cannot
release the connection back to the pool unless you consume all the data or call
:meth:`Response.close <requests.Response.close>`. This can lead to
inefficiency with connections. If you find yourself partially reading request
bodies (or not reading them at all) while using ``stream=True``, you should
consider using ``contextlib.closing`` (`documented here`_), like this::

    from contextlib import closing

    with closing(requests.get('http://httpbin.org/get', stream=True)) as r:
        # Do things with the response here.

.. _`documented here`: http://docs.python.org/2/library/contextlib.html#contextlib.closing