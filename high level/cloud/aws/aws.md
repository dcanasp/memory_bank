Amazon Web Services (AWS) is the world's most broadly adopted cloud platform. AWS offers over 200 fully featured services from data centers globally.

AWS provides Mainly 3 types of services
- Infrastructure as a Service (**IaaS**) 
- Platform as a Service (**PasS**)
- Software as a Service (**SaaS**)

examples of what you can find are raw [[server]]s, auto managed and scaled [[server]]s, all types of [[mid level/databases/Database|databases]] and storage options, all the [[network]] you might need and already working and usable software, some times even giants like Netflix prefer to use AWS services instead of doing their own.

# Core Concepts
## Shared responsibility model

Aws will do some part, but you must also do your part on maintaining secure your services. Aws is not responsible of your customer's data. Nor for how you manage your network security. If you fail at providing for your users, that's on you, and not on Aws. Meanwhile Aws is responsible on maintaining the [[hardware]], You will never worry about that.
## Region
In AWS, services are **always** **associated** with a specific **region**[^1]. This geographical designation is crucial because it affects pricing, availability, and the types of services offered. Each region has its own set of resources and independent pricing structure, and service availability can vary from one region to another. Notably, not all regions offer the same AWS services.


[^1]: there are a few exceptions notably [[Networking#CloudFront|CloudFront]] as it's job is to bring content to multiple regions at a time.

AWS operates in ~30 Regions and  ~110 Availability Zones. Picking the closest is not always the best as it can be pricier
#### Availability zones
Each AWS region is composed of multiple isolated locations known as Availability Zones (AZs). These zones are physical data centers within a region, each with redundant power, networking, and connectivity to ensure fault tolerance and high [[availability]]. AWS services are built to leverage multiple Availability Zones to provide greater reliability and scalability.

for AWS to create a region they must have at least 3 availability. and they must be 60 miles apart from each other 
#### Edge locations
Places were you can save information so that it’s closer to the end user. they are more common and deployed in major cities and highly populated areas around the world. Mostly used on [[Networking]] for [[CDN]] and [[DNS]] management
### local zones
Small local semi-regions that have limited services.
### direct connect
AWS Direct Connect allows for a private connection between an AWS region and your data center, office, or colocation environment. This service can reduce network costs, increase bandwidth, and provide a more consistent network experience compared to internet-based connections.
### Aws backbone
## Console
The AWS Management Console is a web-based interface for managing AWS services. It provides an intuitive graphical user interface to access and manage the services running in the AWS cloud. Most times you will be accessing your AWS services from here. The interface were you can create and monitor all that AWS offers. ![[awsConsole.png]]
## SDK
The AWS SDKs (Software Development Kits) allow developers to access and manage AWS services programmatically, available for every [[programming languages]]. This is what you will use in your [[Backend]] apps simplify using AWS services by wrapping the underlying [[API]] calls with intuitive methods for developers. This is how you truly access your services after creating them

For using them you need *access keys*, these include *access key ID* and *secret access key*.  this should always be done under a [[high level/cloud/aws/Security#IAM|IAM role]] for security reasons. Also you specify the region you are trying to access on the configuration. On the SKD you can do anything you could on the console, like creating servers, tables among others.

## CDK
for bigger teams it's better to have tangible configuration files ...

how it works...
## Pricing
### Pay as you go
The most common approach, you only pay for what you consume, there are no additional costs or termination fees. it's useful when consuming small amounts
### reserved instances
By committing to use AWS resources over a specified term (one or three years), users can receive a significant discount compared to on-demand instance pricing.
### Credits
### Free tier
There are some services that are always free (most of these have to be used with others), others have a free capacity (the first x request are free), and others for the first 12 months are free under a certain amount of conditions
### Aws calculator
AWS has a really good calculator were you can specify the services you will use, all of the details and it will tell you how much would they charge you in that case. 
# services
Aws divides it's services on product categories, the main ones are:
- [[high level/cloud/aws/Compute|Compute]]
- [[Storage]]
- [[high level/cloud/aws/Database|Database]]
- [[Networking]]
- [[high level/cloud/aws/Security|Security]] and Monitoring
- Analytics
- Machine Learning
- [[Application integration]]
- [[Containers]]

