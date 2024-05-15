# IAM
Identity and Access Management is the service that allows to control authentication (creating new IAM Users) and authorization (who has access). You create IAM accounts on the management control, these have some *Access keys* for the Aws SDK, and you enter to the Aws console using this IAM role.
## Policies
You create policies as rules (on json format) that must be followed. For example some policies block deleting data and only allow read access 
## User
The IAM account you create is called an User, on a single Aws account you can have multiple IAM Users. And you can add policies to them
## Group
You create a group to assign Users with the same policies. So for example, readers are only able to read, meanwhile admins can access the billing console  
Groups are for the living
## Role
role is a preset of policies for services. Your [[server]] should not be able to delete your [[mid level/databases/Database|Database]]. You assing a role to it so no matter what, it can't do it.
Roles are for the non-living.
## Recommended practices
- Never use Root user
- Create personalized IAM users for each person that will enter the console
- Always use groups
- least privilege
- Always use custom policies, not default
- MFA
- Roles are key on servers
# Shield
Protection from [[some attacks#DDOS (Distributed Denial of Service)||DDOS]]. There are two levels of the service
- Standard:
already working, it protects [[Networking#CloudFront|CloudFront]], [[Networking#Route 53|Route 53]] and [[Networking#ELB|ELB]], that way your standard workflow will be protected from [[some attacks#DDOS (Distributed Denial of Service)|DDOS]], as those should be the unique open points to the end user
- Advanced:
It's a more refined version, it includes a better logging, and a complete safety to any type of [[some attacks#DDOS (Distributed Denial of Service)||DDOS]], not only https ones, also Advanced shield can protect other services
# WAF
AWS Web application [[firewall]], it's a whole service that will apply some security rules, and block access based on those rules (like [[IP]] origin, packages length among others)

# Monitoring
these services are for Monitoring that is a separate product category, but closely related to security
## CloudWatch
Service to monitor the resources that Aws uses, the applications executed. It shows you the [[CPU]] usage, the [[network]] usage and others in real time
## CloudTrail
Service that stores each action that is done on your Aws account, any instance creation, modification, deleting will appear here