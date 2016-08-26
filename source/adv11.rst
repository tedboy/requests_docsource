.. _event-hooks:

Event Hooks
-----------

Requests has a hook system that you can use to manipulate portions of
the request process, or signal event handling.

Available hooks:

``response``:
    The response generated from a Request.


You can assign a hook function on a per-request basis by passing a
``{hook_name: callback_function}`` dictionary to the ``hooks`` request
parameter::

    hooks=dict(response=print_url)

That ``callback_function`` will receive a chunk of data as its first
argument.

::

    def print_url(r, *args, **kwargs):
        print(r.url)

If an error occurs while executing your callback, a warning is given.

If the callback function returns a value, it is assumed that it is to
replace the data that was passed in. If the function doesn't return
anything, nothing else is effected.

Let's print some request method arguments at runtime::

    >>> requests.get('http://httpbin.org', hooks=dict(response=print_url))
    http://httpbin.org
    <Response [200]>