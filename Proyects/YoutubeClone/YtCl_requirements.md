https://github.com/sonufrienko/microservice
check that repo
## features and requirements

**Phase 1: Essential Features**

1. **User Management (High Priority):**
    
    - Secure registration and login with JWT authentication.
    - User data storage and management.
    - Profile management (optional).
    
2. **Video Upload and Processing (High Priority):**
    
    - API endpoint for video upload.
    - Video transcoding and thumbnail generation (Lambda functions).
    - Secure video storage in S3 buckets.
    
3. **Video Storage and Retrieval (High Priority):**
    
    - Efficient video storage with different S3 storage classes.
    - API endpoints for retrieving video files and thumbnails.
    - Caching for frequently accessed videos (ElastiCache).
    
4. **Metadata Management (Medium Priority):**
    
    - Store and manage video metadata (title, description, tags, etc.).
    - Utilize metadata for search indexing and recommendations.
    
5. **Video Playback (Medium Priority):**
    
    - Implement adaptive bitrate streaming (HLS or DASH).
    - Manage buffer sizes and quality selection options.
    
6. **Basic Search Functionality (Medium Priority):**
    
    - Search videos based on metadata.
    - Include basic filtering and sorting options.
    

**Phase 2: Extended Features (Optional)**

1. **Likes/Dislikes (Low Priority):**
    
    - User interaction system for likes/dislikes.
    - Update recommendations based on user interaction.
    
2. **Comments System (Low Priority):**
    
    - API endpoints for posting and retrieving comments.
    - Basic moderation or filtering mechanisms.
    
3. **Recommendation Algorithm (Low Priority):**
    
    - Develop a basic recommendation system based on user history or video metadata.
    - Consider incorporating machine learning models in the future.
    

**Phase 3: Advanced Features (Optional)**

1. **Subscriptions:**
    
    - Implement a subscription system for channels.
    - Update user feeds based on subscriptions.
    
2. **Notifications:**
    
    - Notify users about new videos or recommendations.
    - Utilize email or other communication channels.
    
3. **Video Analytics:**
    - Track video views, likes/dislikes, and user demographics.
    - Provide analytics reports for video publishers.