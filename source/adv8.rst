.. _streaming-uploads:

Streaming Uploads
-----------------

Requests supports streaming uploads, which allow you to send large streams or
files without reading them into memory. To stream and upload, simply provide a
file-like object for your body::

    with open('massive-body', 'rb') as f:
        requests.post('http://some.url/streamed', data=f)

.. warning:: It is strongly recommended that you open files in `binary mode`_.
             This is because Requests may attempt to provide the
             ``Content-Length`` header for you, and if it does this value will
             be set to the number of *bytes* in the file. Errors may occur if
             you open the file in *text mode*.

.. _binary mode: https://docs.python.org/2/tutorial/inputoutput.html#reading-and-writing-files