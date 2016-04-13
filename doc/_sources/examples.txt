****************************
  Examples
****************************

A basic program that uses ``python-bitbean`` looks like this:

First, import the library and exceptions.

::

    import bitbeanrpc
    from bitbeanrpc.exceptions import InsufficientFunds

Then, we connect to the currently running ``bitbean`` instance of the current user on the local machine
with one call to
:func:`~bitbeanrpc.connect_to_local`. This returns a :class:`~bitbeanrpc.connection.bitbeanConnection` objects:

::

    conn = bitbeanrpc.connect_to_local()

Try to move one bitbean from account ``testaccount`` to account ``testaccount2`` using 
:func:`~bitbeanrpc.connection.bitbeanConnection.move`. Catch the :class:`~bitbeanrpc.exceptions.InsufficientFunds`
exception in the case the originating account is broke:

::  

    try: 
        conn.move("testaccount", "testaccount2", 1.0)
    except InsufficientFunds,e:
        print "Account does not have enough funds available!"


Retrieve general server information with :func:`~bitbeanrpc.connection.bitbeanConnection.getinfo` and print some statistics:

::

    info = conn.getinfo()
    print "Blocks: %i" % info.blocks
    print "Connections: %i" % info.connections
    print "Difficulty: %f" % info.difficulty
  

