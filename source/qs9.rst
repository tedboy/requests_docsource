.. module:: requests.models

POST a Multipart-Encoded File
-----------------------------

Requests makes it simple to upload Multipart-encoded files::

    >>> url = 'http://httpbin.org/post'
    >>> files = {'file': open('report.xls', 'rb')}

    >>> r = requests.post(url, files=files)
    >>> r.text
    {
      ...
      "files": {
        "file": "<censored...binary...data>"
      },
      ...
    }

You can set the filename, content_type and headers explicitly::

    >>> url = 'http://httpbin.org/post'
    >>> files = {'file': ('report.xls', open('report.xls', 'rb'), 'application/vnd.ms-excel', {'Expires': '0'})}

    >>> r = requests.post(url, files=files)
    >>> r.text
    {
      ...
      "files": {
        "file": "<censored...binary...data>"
      },
      ...
    }

If you want, you can send strings to be received as files::

    >>> url = 'http://httpbin.org/post'
    >>> files = {'file': ('report.csv', 'some,data,to,send\nanother,row,to,send\n')}

    >>> r = requests.post(url, files=files)
    >>> r.text
    {
      ...
      "files": {
        "file": "some,data,to,send\\nanother,row,to,send\\n"
      },
      ...
    }

In the event you are posting a very large file as a ``multipart/form-data``
request, you may want to stream the request. By default, ``requests`` does not
support this, but there is a separate package which does -
``requests-toolbelt``. You should read `the toolbelt's documentation
<https://toolbelt.readthedocs.io>`_ for more details about how to use it.

For sending multiple files in one request refer to the :ref:`advanced <advanced>`
section.

.. warning:: It is strongly recommended that you open files in `binary mode`_.
             This is because Requests may attempt to provide the
             ``Content-Length`` header for you, and if it does this value will
             be set to the number of *bytes* in the file. Errors may occur if
             you open the file in *text mode*.

.. _binary mode: https://docs.python.org/2/tutorial/inputoutput.html#reading-and-writing-files