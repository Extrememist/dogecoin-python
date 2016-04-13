****************************
  Introduction
****************************

The goal of this library is to make it easier for:

- Payment gateways to support bitbean
- Merchant sites to integrate bitbean payments directly
- Other services that require (micro-)payments to use bitbean

In this initial release it implements a thin wrapper around the 
bitbean JSON-RPC API. Using this API from Python directly is conceptually very simple, 
here is the example from the API 
documentation page:

::

    from jsonrpc import ServiceProxy
    
    access = ServiceProxy("http://user:password@127.0.0.1:8332")
    access.getinfo()
    access.listreceivedbyaddress(6)
    access.sendtoaddress("11yEmxiMso2RsFVfBcCa616npBvGgxiBX", 10)

However, this approach has some disadvantages, one thing is that error handling is complex, as it
requires manually checking the contents of :const:`JSONException` objects.

``bitbean-python`` attempts to create an even more friendly interface by wrapping the JSON-RPC API. The major advantages
compared to a raw ``jsonrpc`` based approach are:

- Better exception handling. Exceptions are converted to subclasses of :class:`~bitbeanrpc.exceptions.bitbeanException`.

- Automatic bitbean configuration loading. In case the ``bitbean -server`` or ``bitbeand`` program runs on the same 
  machine as the client script, and as the same user, the configuration file can automatically be parsed. This
  makes it unneccesary to explicitly specify a *username* and *password*. Of course, this is still possible.

- Documentation in Pythonish format. You are reading this right now.

- The functions 
  :func:`~bitbeanrpc.connection.bitbeanConnection.getinfo`, :func:`~bitbeanrpc.connection.bitbeanConnection.listreceivedbyaccount`,
  :func:`~bitbeanrpc.connection.bitbeanConnection.listreceivedbyaddress`, 
  :func:`~bitbeanrpc.connection.bitbeanConnection.listtransactions` and more return actual Python objects, instead of simply
  dictionaries. This makes for cleaner code, as the fields can simply be addressed with ``x.foo`` instead of 
  ``x['foo']``.

The plan for future releases is to add a more high-level interface on top of this.

