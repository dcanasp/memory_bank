**DNS** (Domain Name System), which is essentially the phonebook of the Internet. It translates human-readable domain names (like `www.example.com`) into [[IP]] addresses that computers use to identify each other on the [[network]].

### How It Works

1. **Query**: When you type a URL into a browser, a DNS query is generated.
2. **Lookup**: This query goes to a DNS [[server]], which looks up the domain name and finds the corresponding IP address.
3. **Response**: The IP address is sent back to your browser.
4. **Connection**: Your browser uses this IP address to establish a connection to the [[server]] hosting the website.

### Key Components

- **Domain Name**: A human-readable address (e.g., `www.example.com`). This name follows the RFC 952 standard. No underscores nor special characters
- **IP Address**: A unique numerical label assigned to each device connected to a computer network.
- **DNS Server**: A server that contains a database of public IP addresses and their associated hostnames.
- **Resolver**: Part of the browser that queries DNS servers.

### Types of DNS Records

- **A Record**: Maps a domain name to an IPv4 address.
- **AAAA Record**: Maps a domain name to an IPv6 address.
- **CNAME Record**: Redirects one domain to another domain.
- **MX Record**: Specifies mail exchange servers for email delivery.
- **NS Record**: Indicates the authoritative name server for a domain.

### DNS in Security

- **Vulnerabilities**: DNS is often a target for attacks like DNS [[some attacks#Spoofing|Spoofing]] or DNS Cache Poisoning.
- **DNSSEC**: An extension to DNS, DNS Security Extensions (DNSSEC) adds a layer of security by validating responses with digital signatures.


### Importance

- **Internet Navigation**: DNS is critical for the functioning of the internet, translating user-friendly domain names to IP addresses.
- **Scalability**: It makes it easier to change the IP addresses of services and to scale internet services globally.

### Example

- **Website Access**:
    - A user enters `www.example.com` into their browser.
    - The browser sends a DNS query, which is resolved to an [[IP]] address like `192.0.2.1`.
    - The browser connects to this IP address to retrieve and display the website.

### Common errors
#### RFC 952

This one is very simple but hard to debug. Your DNS name must follow this regex pattern:
`ValidHostnameRegex = "^(([a-zA-Z0-9]|[a-zA-Z0-9][a-zA-Z0-9\-]*[a-zA-Z0-9])\.)*([A-Za-z0-9]|[A-Za-z0-9][A-Za-z0-9\-]*[A-Za-z0-9])$";`

These are the rules visualized.
![[DNS_Regex.png]]
Mainly. Only letters, numbers and "-" allowed. underscores are not allowed. This is specially important in [[docker]] whenever you create your own [[network]] and DNS names