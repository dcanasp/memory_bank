# EC2
The [[server]], you can have any [[OS]] you like, but the recommended by them is Amazon linux.

This server will have a public [[IP]], just like a private one. to connect do it from the aws console, or from your local cmd. With this option you will need a .pem file, that stores your key (they generate it when creating)

The .pem file MUST be secure, so only admins should be able to read it, for this on windows, you need to set it like this:
![[pemConfiguration.png]]

amazon gives a single server to multiple users, so we share the same servers with different spaces allocated to each (you cannot se what the other users have).


When you turn off your device the [[IP]] will change, unless you have a [[Networking#Elastic IP|Elastic IP]]

# Lambda
A lambda is the same as a [[server]], it's the whole thing, but instead of being alive all of the time, it only boots when you need it

you call it with a [[Application integration#API Gateway|Aws API Gateway]] if you need your lambda as a result of a http petition, or with a [[Application integration#Event bridge|Event Bridge]] if you just want a [[Cron]] to open your code

# Elastic Beanstalk
You add the code and it will manage all of the infrastructure to fit your needs (no over nor under scaling)
