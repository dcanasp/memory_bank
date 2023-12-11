### Backend Server

- **TypeScript on EC2**: main server 
### Video Processing

Both of this microservices will be using a queued system (kafka/rabbitMQ) 
- **First microservice**: a service that will process the video in low quality
	- **[[Racecar]]**: a separate service that will run along side this one, this service will create the thumbnails 
- **Second microservice**: a service that will process the video in high quality
### Video Storage

- **AWS S3 Buckets**: each user has a folder, where it's videos are stored
### Database Management

- **SQL for Metadata (PostgreSQL)**: will store metadata (tags that a user must send with a video, length, categories, views), likes, an index for each video, and those sort of things. for complex querys an orm WONT be used 
- **NoSQL for Comments (MongoDB)**: i want to edit each collection for comments, because i won't do anything with this data.
### Algorithms and Notifications

- **Backend Algorithms**: Search algorithms, feed algorithms ...
- **Notifications via Email (SMTP/AWS SES)**: