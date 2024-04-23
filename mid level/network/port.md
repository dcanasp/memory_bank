A virtual point where a [[network]] connection starts and ends. Only the [[program|programs]] that needs network access should be using a port. It allows for multiplexing (a lot of services on the same machine).

from 0-1023 are the universal [[protocols#Main Network Protocols|protocols]], the http, ftp ...

The limit of port is based on the machine, each port is using resources, so that is the real limit

Port management is an essential part of [[Network Security]]. And Most applications block some default ports.

Finally [[web browser]]s based on chromiun block by default some ports [restricted ports](https://chromium.googlesource.com/chromium/src.git/+/refs/heads/master/net/base/port_util.cc)  
