A core feature of [[system architecture]]. Currently you deploy as soon as possible, with little changes at a time. There is no point on waiting for giant changes

# CD
Continuous deployment if there is **NO** human intervention or continuous delivery if there is **some** human intervention

This deployment pipeline has 3 main metrics of quality
- cycle time: how long it takes?
- Traceability: can you check all the steps on why an artifact had a problem? sometimes you store the data of all the system in a special [[database]] 
- Repeatability: can you repeat the exact same pipeline multiple times?

# Tactics

## Manage Deployment Pipeline

- **Scale rollouts**: instead of migrating all the users to the new version, deliver it only to few, Testing that they enjoy it and it works. If needed you can roll back
- **Roll back**: If you don't find it as you expected it, reverse the deployment
- **Script** deployment **commands**: deployment should also have documentation (the best one). It should be tested, and accessible to future generations 

## Manage Deployed System

- **Package dependencies**: when you deploy you add everything, packages, [[OS]], utility containers ([[Sidecar]], mesh). This is normally done through [[docker]] images
- **Feature toggle**: Having a kill switch for possible unstable features. so you don't have to drop everything, only the unrequired features
# Patterns

[[microservices]] architecture Makes this increasingly easier.
But when you want to change the application for all users you do a:
- **Blue/green deployment**: you create two separate, but *identical* environments. One environment (blue) is running the current application version and one environment (green) is running the new application version. If the **green works** then you make those the current blue applications and delete the old blue 
- **Rolling upgrade**: also called rolling update. You start updating some of the servers/pods one at a time (in [[kubernetes]] for example). And until they finish updating you swap them, creating a zero downtime deployment

And if you just want to change for a few users, like for testing they like the new interface. You do a:
- **Canary Testing**: When you want to test on a specific set of users (specific demography). You select them as canaries to try the new features. They are routed to the appropriate version of a service through [[DNS]] settings or through discovery-service configuration
- **A/B Testing**: This is when you want to see what changes make users use your application more, Are heavily used on marketing environments. And they can be small things like fonts or colors
