**Internet Protocol address** is a number assigned to a device connected to a [[computer]] [[network]], it identifies who that node is.
You can set the ip manually or the can be set using the standard protocol dhcp
# types of ip

There are two types of ip's. **Public** and **private**, public are the ones that can directly connect to the internet. Private are the ones that only can be access inside the same [[network]]

## IPv4
Ipv4 is the older version (still used in all of the world). It is represented on 32 bits. An example of an ipv4 is `127.0.0.1`. 

As of writing this, Ipv4 has reached it's maximum address number (4 American billion). to combat this with Ipv4 is that you normally **only** get **one** public IP **per house**, and it's on the [[Router]], your computer does NOT access the internet, it has a private Ip, that data is re routed to the router, and then it gets send, when sent the router keeps your MAC address to return the package to you

The reserved IPs for IPv4 are
- Class A: `10.0.0.0` to `10.255.255.255`
- Class B: `172.16.0.0` to `172.31.255.255`
- Class C: `192.168.0.0` to `192.168.255.255`

## IPv6

Ipv6 is the new standard, but has not been fully adopted yet. It is notably larger (2^128). so they most likely won't run out.
An example of an IPv6 is `2607:f0d0:1002:0051:0000:0000:0000:0004`

In these addresses, leading zeroes in a group can be omitted for brevity, and one sequence of consecutive zeroes can be replaced by a double colon (::), but this can only be done once in an address to avoid ambiguity.

Instead of private addresses, IPv6 uses unique local addresses (**ULA**s). These addresses are not routable on the global internet and are used within local networks, similar to the private address ranges in IPv4.

The range for unique local addresses (ULAs) in IPv6 is `fc00::/7`. This range is divided into two parts:

1. `fc00::/8` - Not yet defined or used.
2. `fd00::/8` - The most commonly used range for ULAs. When generating a ULA, it is typical to use a randomly generated 40-bit value after the `fd` prefix, ensuring uniqueness within a local network.

An example of an IPv6 ULA might be `fd12:3456:789a:1::1`.
