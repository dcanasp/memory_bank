Project made In university for the class "Software engineering 2". You can find this project on [Github](https://github.com/dcanasp/trUNews). My contribution was doing most of the backend and cloud computing. 

## Mission Statement
Delivering unbiased news with integrity and a seamless user experience, free from intrusive ads.

## Key Features

### User Interface
- Read and save articles
- Share articles via social media and QR codes
- Follow users and communities
- Participate in events

### AI
- Auto-generate natural titles
- Categorize articles 
 (Note: models not included in this repo)

### Personalization
- Discover trending articles and related communities
- Search functionality for users, articles, and communities

### Community Engagement
- Join diverse interest-based communities
- Participate in community-centered events
### Queue System
- RabbitMQ for managing asynchronous tasks (sending messages to AI models)
### Jobs
- Aws Lambdas to run continuously create new articles and update trending
## Technical Stack

- **Programming Language:** TypeScript
- **Database:** PostgreSQL
- **API Communication:** REST
- **Algorithms:**
  - Feed: Softmax based on categories
  - Trending Articles/Authors: Weighted algorithm with sigmoid functions
  - Related communities: Statistical deviation algorithm
  - Enhanced search for articles and users


## Infrastructure

- Fully dockerized environment
- Unit testing with Jest
- Automated server management via GitHub Actions
- Logging with Winston
- ORM: Prisma
- Validation: ZOD
- Scripts for database population and trending algorithm reset
- Documentation: Swagger
- Image processing: Sharp
- Dependency injection: Tsyringe

### Deployment
- Hosted on DockerHub (includes all code and docker-compose)

#### AWS Infrastructure
- EC2 server hosting
- S3 for image storage
- CloudFront for CDN
- Lambda and EventBridge for user activity simulation and trend generation
- SSL certificate via Nginx proxy



