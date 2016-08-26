OAuth 1 Authentication
----------------------

A common form of authentication for several web APIs is OAuth. The ``requests-oauthlib``
library allows Requests users to easily make OAuth authenticated requests::

    >>> import requests
    >>> from requests_oauthlib import OAuth1

    >>> url = 'https://api.twitter.com/1.1/account/verify_credentials.json'
    >>> auth = OAuth1('YOUR_APP_KEY', 'YOUR_APP_SECRET',
                      'USER_OAUTH_TOKEN', 'USER_OAUTH_TOKEN_SECRET')

    >>> requests.get(url, auth=auth)
    <Response [200]>

For more information on how to OAuth flow works, please see the official `OAuth`_ website.
For examples and documentation on requests-oauthlib, please see the `requests_oauthlib`_
repository on GitHub