### Todos
- [x] setUp Ideas ✅ 2023-12-08
- [x] architecture principles learnes ✅ 2023-12-08
- [x] orm ✅ 2023-12-10
- [x] web server ✅ 2023-12-11
- [x] fastify rabbit hole ✅ 2023-12-11
- [x] how is it gonna work ✅ 2023-12-11
- [x] user routes ALL Get ✅ 2023-12-14
- [x] user routes ALL post ✅ 2023-12-14
- [x] videos routes ✅ 2023-12-15
- [ ] finish videos routes
- [x] microservices understanding ✅ 2023-12-29
- [x] first microservice creation ✅ 2023-12-29
- [x] RabbitMQ ✅ 2023-12-21
- [x] S3 storage ✅ 2023-12-21
- [x] gRPC conecrion ✅ 2023-12-29
- [x] mutual TLS conection ✅ 2024-01-02
- [ ] comments routes
- [ ] api gateway with nginx
- [ ] side car thumbnail generator

[[YtCl_requirements||Requirements]]
[[YtCl_architecture||Architecture]]
[[Proyects/YoutubeClone/YtCL_apiGateway||ApiGateway]] 
[[Proyects/YoutubeClone/YtCL_routes||Routes]] 



I'm an experienced backend developer with a strong foundation in computer science, currently pursuing a master's degree. I've decided to create a YouTube clone to enhance my portfolio and learn more about video processing and cloud services. I'm proficient in TypeScript and familiar with AWS services, and I intend to handle the video processing, storage, and serving components myself. The frontend will be minimal as my focus is on building a robust backend.

My project will allow users to watch and publish videos. Videos will be stored on AWS S3. There will be one microservice, that processes and have a sidecar that creates a thumbnail. Metadata will be stored in a PostgreSQL database, while comments will be managed with a NoSQL database like MongoDB, with each video's comments stored as a collection.

I use a message queue for video processing tasks. The main server (on Typescript) uploads to a rabbitMQ broker, and a microservice (on Go) reads this broker, and manages the videos to not loose any data. Notifications will be handled via SMTP or AWS SES. I've expressed a preference for managing database migrations myself and I'm using Sequelize ORM, and raw queries when handling of complex queries.

Your job is to help me and guide me on all of my problems, if you see any error you must tell me, even if it's architecture errors 
