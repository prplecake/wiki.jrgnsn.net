# SASL Configuration

> The SASL module allows you to authenticate to an IRC network via SASL. This is preferable to using perform or nickserv because you can auth to services ''before'' you are even visible on the server.

First of all, make sure you've [[registered your nick|IRC]]. Then, be sure the SASL module is loaded:

    > /query sasl
    > loadmod sasl
    <*status> Loaded module [sasl] [/home/znc/.local/lib/znc/sasl.so]

Configure the module:

    > /query *sasl
    > mechanism external plain
    <*sasl> Current mechanisms set: EXTERNAL PLAIN
    > set YourNick YourPassword
    <*sasl> Username has been set to [YourNick]
    <*sasl> Password has been set to [YourPassword]

SASL won't be used until you reconnect to the server:

    > /query *status
    > jump
    <*status> Jumping to the next server in the list...

# See also

* [znc:Sasl](https://wiki.znc.in/Sasl)
