The [[server]], you can have any [[OS]] you like, but the recommended by them is Amazon linux.

This server will have a public [[ip]], just like a private one. to connect do it from the aws console, or from your local cmd. With this option you will need a .pem file, that stores your key (they generate it when creating)

The .pem file MUST be secure, so only admins should be able to read it, for this on windows, you need to set it like this:
![[pem configuration.png]]

amazon gives a single server to multiple users, so we share the same servers with different spaces allocated to each (you cannot se what the other users have).


When you turn off your device the [[Ip]] will change, unless you have a [[Elastic ip]]