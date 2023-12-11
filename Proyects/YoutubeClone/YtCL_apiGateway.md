**Main Server:**

- **[[high level/code/design patterns/ApiGateway||API Gateway]]:**
    - `/users`: Manage user registration, login, and profile updates.
    - `/videos`: Upload video information (metadata) and receive upload URLs.
		    - `/videos/{id}/stream`: Accepts a video ID and returns a streaming URL for the appropriate video format and bitrate based on the user's network conditions. This endpoint would need to:
		    - Query the video metadata to identify the available formats and thumbnails.
		    - Select the appropriate video format based on user request and network conditions.
		    - Generate a temporary signed URL for the chosen video file in S3.
		    - Return the signed URL along with any required metadata (e.g., subtitles, thumbnails) in the response.

    - `/comments`: Manage video comments (create, read, update, delete).
    - `/search`: Search for videos based on metadata.
    - `/recommendations`: Get personalized video recommendations.
    - `/analytics`: Access video analytics data (views, likes/dislikes, etc.).
    
**Video Processing Microservices:**

- **Low-Quality Microservice:**
    - `/process-video`: Receives video upload request and generates a low-quality version for quick preview.
    - `/generate-thumbnail`: Receives low-quality video and generates a low-resolution thumbnail.
    - Publishes video information and thumbnail details to Kafka/RabbitMQ queue.
- **High-Quality Microservice:**
    - Consumes video information and thumbnail details from Kafka/RabbitMQ queue.
    - `/process-video`: Transcodes video to higher resolutions.
    - `/generate-thumbnail`: Generates high-resolution thumbnails for each transcoded version.
    - Stores high-quality video files and thumbnails in S3.

**Sidecar Containers:**

- **Thumbnail Generation:**
    - `/analyze-video`: Receives video object and extracts relevant information for thumbnail generation (e.g., key frames).
    - `/generate-thumbnail`: Generates thumbnail based on extracted information and sends it to the appropriate microservice.