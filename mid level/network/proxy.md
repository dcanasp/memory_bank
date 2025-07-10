**Proxy servers** act as intermediaries between clients and servers, handling requests and responses on behalf of either. This intermediary role provides several benefits, such as security, anonymity, and performance optimization. However, the direction of traffic flow determines whether the proxy is considered **forward** or **reverse**.

## Forward Proxy

All the traffic you do, goes to the proxy, who actually makes the request

- Acts on behalf of the client.
- Hides the client's [[IP]] address from the [[server]], offering anonymity.
- Can be used to bypass content restrictions or censorship.
- May cache frequently accessed content, improving performance.
- Can be used to restrict access to some webs ( for example a school that block all access to social media) 
- In an enterprise, a proxy is used so only the computers connected to it can access the database
- Public proxy servers, web filters in corporate networks.

## Reverse Proxy
All the traffic that is going to the server get's intercepted by the proxy, who then decides what to do with the flow

- Acts on behalf of the server.
- Hides the server's [[IP]] address from the client, enhancing security.
- Can improve performance by [[Load balancer|load balancing]] requests across multiple servers.
- Offers additional features like caching, compression, and [[SSL]] encryption.
- That exact use case is really important, if you have a [[SSL]] certificate, you have to fetch it, a proxy manages that 
- Web hosting companies, [[CDN|CDNs]].
- Implementing special **[[architecture/Quality attributes/security]] rules**, for example banning all request that come from X banned IPs, or all the request that have a [[sql injections]]  
- Implementing a [[firewall#Types of Firewalls|WAF]]

## how

The most common proxy is [[nginx]]

