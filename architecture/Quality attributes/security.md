A core feature of [[system architecture]]. Security is granting access to the authorized users meanwhile protecting from the unauthorized, the commonly known as attackers. To do this there are three key components. 
- **Confidentiality**: Only you should be able to access your data
- **Integrity**: No one should be able to change your data
- **Availability**: Your system should always be available, even when under [[some attacks|attacks]] 

>[!important]
If you truly want security you should have [[Web Security]] and [[Network Security]].


A very important fact about security is protecting the *SPOF* (Single Point Of Failure) or in graph theory called *cut vertices* (articulation points). These are the points in your system that if turned off would disconnect all of the services. For example a unique [[mid level/databases/Database|Database]] or a [[load balancer]] if these fall down, the rest of the program is unable to operate. 

A final good security concept is to verify on **three** steps.
- With something you know (a password)
- Something you are (Biometric)
- Something you Have (USB with another private key)

To achieve security you have compromise on other things like [[Performance]], [[Modifiability]], [[Availability]] and of course **costs**. Security can be the most cost full part of a system, But not having it costs more

# Tactics

## Detect attacks
First of all. Let's remember [[some attacks]] that are used today.

- **Detect intrusion**: Comparing each movement a user (via their request) do to what a normal user should do. If a user is trying to access the [[mid level/databases/Database]] directly or contacting the main servers instead of the [[ApiGateway]] there is something wrong and that user should be banned.
	Another important part in intrusion is checking [[IP]]s and connection times, when someone has a abnormal amount of connections, and then the system get's slow. Something happened
- Verify **message integrity**: Whenever downloading any resources, files, or things like that you should be using a **checksum** or a [[hash]]. This makes impossible someone on the [[some attacks#Man in the Middle (MitM)|middle]] changing the files
- Detect **message delay**: Your services normally should take an X amount of time, if it starts taking longer than usual it could be a possible attack

## Resist attacks
- **Authentication**: Anything valuable should be accessed after a Password, one-time password, [[digital certificates]], two-factor authentication, or biometric identification. Also include a CAPTCHA just in case
- **Authorize**: make sure that a person can only access what it's theirs. No checking others data!
- **Limit access**: By default mistrust the users, don't deliver if you aren't sure it's them
- **Limit exposure**: The public access points should know as few as possible, even if they fall, they have nothing of value
- **Encrypt data**: Always use [[HTTPS]], when possible encrypt non frequent data. In this topic is also important that the final [[server]]s don't have source code. They should only have the executable code.
- **Separate entities**: You should have the regular data on the main [[server]] meanwhile the sensitive data should be on a different [[server]]
## Recover from attacks
- **Revoke access**: If there is the believe that you are under attack (and you are losing) you should limit the access to sensitive data, and disconnect the servers from the main [[network]]
- **Inform actors**: If you are under attack make it a immediate problem, talk to your team, every second counts
## React to attacks
- **Audit**: after an attack verify there are no bad actors inside of system
- **non repudiation**: Every transaction should have the traceability of who made it. If some bad actor access the system (most times are employees) we should know who they were 
# Patterns

## Intercepting Validator

create a wrapper between the source and the destination. All data passes through it. And it's job is to **Detect attacks**, it validates any misuse or unusual activity, and if found it will take measurements

## Intrusion Prevention System (IPS)

An element whose main purpose is to **identify** and **analyze** any **suspicious activity**. If the activity is deemed acceptable, it is allowed. Conversely, if it is suspicious, the activity is **prevented** and **reported**. These systems look for suspicious patterns of overall usage, not just anomalous messages. It *Detects attacks* and also *Resist attacks*. This is similar to a [[firewall]]
