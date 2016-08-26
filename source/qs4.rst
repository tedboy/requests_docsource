.. module:: requests.models

Binary Response Content
-----------------------

You can also access the response body as bytes, for non-text requests::

    >>> r.content
    b'[{"repository":{"open_issues":0,"url":"https://github.com/...

The ``gzip`` and ``deflate`` transfer-encodings are automatically decoded for you.

For example, to create an image from binary data returned by a request, you can
use the following code::

    >>> from PIL import Image
    >>> from io import BytesIO

    >>> i = Image.open(BytesIO(r.content))