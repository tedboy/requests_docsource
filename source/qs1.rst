.. module:: requests.models


Let's get started with some simple examples.

Make a Request
--------------

Making a request with Requests is very simple.

Begin by importing the Requests module::

    >>> import requests

Now, let's try to get a webpage. For this example, let's get GitHub's public
timeline::

    >>> r = requests.get('https://api.github.com/events')

Now, we have a :class:`Response <requests.Response>` object called ``r``. We can
get all the information we need from this object.

Requests' simple API means that all forms of HTTP request are as obvious. For
example, this is how you make an HTTP POST request::

    >>> r = requests.post('http://httpbin.org/post', data = {'key':'value'})

Nice, right? What about the other HTTP request types: PUT, DELETE, HEAD and
OPTIONS? These are all just as simple::

    >>> r = requests.put('http://httpbin.org/put', data = {'key':'value'})
    >>> r = requests.delete('http://httpbin.org/delete')
    >>> r = requests.head('http://httpbin.org/get')
    >>> r = requests.options('http://httpbin.org/get')

That's all well and good, but it's also only the start of what Requests can
do.