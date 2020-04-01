# pyquake2 - Python Quake 2 Library

**pyquake2** is a Python library to query and execute RCON commands on a Quake 2 server.

It is a 'demake' of [urthub's pyquake3](https://github.com/urthub/pyquake3) which itself was a complete rewrite of an earlier [pyquake3](http://misc.slowchop.com/misc/wiki/pyquake3) module that [Gerald Kaszuba](http://geraldkaszuba.com/) wrote.

This pyquake2 module was developed for and tested with [qt2pro](https://skuller.net/q2pro/) server.


# Features
- Send RCON commands
- Access server variables
- Collect player information (e.g. name, ping, frags and IP address)


# Example
```python
    SERVER = "localhost:27910"
    PASSWORD = "admin"

    q = PyQuake2(server=SERVER, rcon_password=PASSWORD)
    q.update()
    print "The server name of '%s' is %s, running map %s with %s player(s)." % (q.get_address(), q.values['hostname'], q.values['mapname'], len(q.players))

    # Player info
    for gamer in q.players:
        print "\t%s with %s frags and a %s ms ping" % (gamer.name, gamer.frags, gamer.ping)

    # To get IP info
    q.rcon_update()
    for gamer in q.players:
        print "\t%s (%s) has IP address of %s" % (gamer.name, gamer.num, gamer.address)

    # Broadcast messages to all players
    q.broadcast("pyquake2 is great!")

    # Change levels
    q.change_level("marics55")

    # Simple command loop
    # commands are anything that follow /rcon PASSWORD eg:
    #   say hi
    #   gamemap dm1
    import readline
    while True:
        cmd = raw_input("> ")
        if cmd == "":
            break
        q.rcon(cmd)

```
