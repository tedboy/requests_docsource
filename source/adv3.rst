.. _prepared-requests:

Prepared Requests
-----------------

Whenever you receive a :class:`Response <requests.Response>` object
from an API call or a Session call, the ``request`` attribute is actually the
``PreparedRequest`` that was used. In some cases you may wish to do some extra
work to the body or headers (or anything else really) before sending a
request. The simple recipe for this is the following::

    from requests import Request, Session

    s = Session()

    req = Request('POST', url, data=data, headers=headers)
    prepped = req.prepare()

    # do something with prepped.body
    prepped.body = 'No, I want exactly this as the body.'

    # do something with prepped.headers
    del prepped.headers['Content-Type']

    resp = s.send(prepped,
        stream=stream,
        verify=verify,
        proxies=proxies,
        cert=cert,
        timeout=timeout
    )

    print(resp.status_code)

Since you are not doing anything special with the ``Request`` object, you
prepare it immediately and modify the ``PreparedRequest`` object. You then
send that with the other parameters you would have sent to ``requests.*`` or
``Session.*``.

However, the above code will lose some of the advantages of having a Requests
:class:`Session <requests.Session>` object. In particular,
:class:`Session <requests.Session>`-level state such as cookies will
not get applied to your request. To get a
:class:`PreparedRequest <requests.PreparedRequest>` with that state
applied, replace the call to :meth:`Request.prepare()
<requests.Request.prepare>` with a call to
:meth:`Session.prepare_request() <requests.Session.prepare_request>`, like this::

    from requests import Request, Session

    s = Session()
    req = Request('GET',  url, data=data, headers=headers)

    prepped = s.prepare_request(req)

    # do something with prepped.body
    prepped.body = 'Seriously, send exactly these bytes.'

    # do something with prepped.headers
    prepped.headers['Keep-Dead'] = 'parrot'

    resp = s.send(prepped,
        stream=stream,
        verify=verify,
        proxies=proxies,
        cert=cert,
        timeout=timeout
    )

    print(resp.status_code)