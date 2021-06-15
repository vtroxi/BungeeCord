# BungeeCord hotfix for DynDNS support

**This is a simple hotfix for an issue, I had when running BungeeCord with subservers that were using DynDNS.**

BungeeCord initially resolves the underlying IP of a server's hostname assuming that it does not change afterwards.
This leads to servers becoming unreachable, after the dynamic IP address has changed.

*This fix automatically updates all stored ServerInfos after a connection attempt has failed, thus storing the new ip address of each server and solving the connection issue.*

Modifications:
- The **connect(final ServerConnectRequest request)** method in **[UserConnection](proxy/src/main/java/net/md_5/bungee/UserConnection.java)** has been changed to update stored IPs
- This update happens via the **ProxyConfig** interface and is implemented as **updateServerIPs()** in the **[Configuration](proxy/src/main/java/net/md_5/bungee/conf/Configuration.java)** class


*Please note that this is a fix I made quickly for my own server and is probably not the perfect solution.*
