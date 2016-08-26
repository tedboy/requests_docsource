Stuffs from official doc
""""""""""""""""""""""""
http://docs.python-requests.org/en/master/

.. note::
    
    Turned out most of the content here is better of browsing the original documentation page. So rst files below are included in the ``exclude_patterns`` list in ``conf.py``

Requests is the only *Non-GMO* HTTP library for Python, safe for human
consumption.

**Warning:** Recreational use of other HTTP libraries may result in dangerous side-effects,
including: security vulnerabilities, verbose code, reinventing the wheel,
constantly reading documentation, depression, headaches, or even death.

Behold, the power of Requests::

    >>> r = requests.get('https://api.github.com/user', auth=('user', 'pass'))
    >>> r.status_code
    200
    >>> r.headers['content-type']
    'application/json; charset=utf8'
    >>> r.encoding
    'utf-8'
    >>> r.text
    u'{"type":"User"...'
    >>> r.json()
    {u'private_gists': 419, u'total_private_repos': 77, ...}

See `similar code, sans Requests <https://gist.github.com/973705>`_.


Requests allows you to send *organic, grass-fed* HTTP/1.1 requests, without the
need for manual labor. There's no need to manually add query strings to your
URLs, or to form-encode your POST data. Keep-alive and HTTP connection pooling
are 100% automatic, powered by `urllib3 <https://github.com/shazow/urllib3>`_,
which is embedded within Requests.

###################
The Community Guide
###################
This part of the documentation, which is mostly prose, details the Requests ecosystem and community.

.. toctree::
   :maxdepth: 2
   :numbered:
   :caption: Contents
   :name: community

   official_doc.community.faq.rst
   official_doc.community.recommended.rst
   official_doc.community.out-there.rst
   official_doc.community.support.rst

#############################
The API Documentation / Guide
#############################
If you are looking for information on a specific function, class, or method, this part of the documentation is for you.

.. toctree::
   :maxdepth: 2
   :numbered:
   :caption: Contents
   :name: official_api   

   official_doc.api.rst




