## Overview

This project is a YouTube clone designed to enhance my portfolio and deepen my understanding of video processing and backend managment. It features a robust backend focused on handling video processing, storage, and serving, with a minimalistic frontend.

### Key Features

- **Video Publishing**: Users can upload videos to be processed and stored.
- **Video Watching**: Users can watch videos stored on AWS S3 using MPEG-DASH (adaptive bitrate).
- **Backend Services**: Two servers handling different aspects of the application:
    - **TypeScript Server**: Manages user creation and raw video uploads.
    - **Go Server**: Manages comments, likes, and subscriptions.
- **Video Processing**: Utilizes a microservice architecture with RabbitMQ for uploading. Uses MPEG-DASH and stores videos on s3 with that, also has a sidecar for thumbnail generation.
- **Database Management**: PostgreSQL with Sequelize ORM on TS and no orm on Go.
- **Notification System**: Implemented via SMTP.

## Technical Stack

- **Frontend**: Only for testing the streaming.
- **Backend**:
    - **Languages**: TypeScript, Go.
    - **Database**: PostgreSQL.
    - **ORM**: Sequelize for TS and no orm on Go.
    - **Message Broker**: RabbitMQ.
- **Cloud Services**: AWS S3.
- **Servers**:
    - **API Gateway**: NGINX.
    - **Load balancer**: NGINX.
    - **Video Processing**: Microservice.

## File Structure

- `conf/`: Configuration files for NGINX.
- `frontend/`: Frontend application files.
- `HighQualityMicroservice/`: Microservice for video processing.
- `logs/`: Log files.
- `secondServer/`: Go server for comments, likes, and subscriptions.
- `typescriptServer/`: Main TypeScript server for user and video management.

## Getting Started

If you want to run it locally first download all of the dependencies. Then set up the .env variables on the 3 main paths. Finally you have to start docker and can run `make` and the makefile will start

## License

MIT

# Missing

Sadly i couldn't finish all i wanted to do
- [ ] Basic Search Functionality
- [ ] Recommendation Algorithm
- [ ] Notifications with SMTP
- [ ] Thumbnail generation
