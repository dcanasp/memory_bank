# Main server
**Authentication:**

- [x]  **POST /users/register:** Register a new user with username, email, and password.
- [x] **POST /users/login:** Login with username and password.
- [x] **GET /users/me:** Get the currently logged-in user's information.

**User Management:**

- [x] **PUT /users/:id:** Update user information (profile picture, bio, etc.).
- [x] **GET /users/:id:** Get user information by ID.

**Video Upload:**

- [x] **POST /videos:** Upload video file and metadata (title, description, tags, etc.).
- [ ] **GET /videos/:id:** Get video metadata and upload status.

**Video Storage and Retrieval:**

- [ ] **GET /videos/:id/thumbnail:** Get the thumbnail image for the video.
- [ ] **GET /videos/:id/download:** Download the video file.

# second server
**Likes/Dislikes:**

- [ ] **POST /likes/:id/like:** Like/dislike a video.
- [ ] **GET /likes/:id/like:** Get the number of likes and dislikes for a video.

**Comments:**

- [ ] **POST /comments/:id/comments:** Post a comment on a video.
- [ ] **GET /comments/:id/comments:** Get all comments for a video.
- [ ] **DELETE /comments/:id/comments/:commentId:** Delete a comment.

**Subscriptions:**

- [ ] **POST /subscriptions/:channelId:** Subscribe to a channel.
- [ ] **DELETE /subscriptions/:channelId:** Unsubscribe from a channel.
- [ ] **GET /subscriptions/feed:** Get a feed of videos from subscribed channels.

**Video Playback:**

- [ ] **GET /videos/:id/stream:** Get a signed URL for streaming the video file in different formats and quality based on network conditions.

# main server once again
**Search:**

- [ ] **GET /videos/search:** Search for videos based on keywords, tags, and other criteria.
- [ ] **GET /videos/popular:** Get a list of trending or popular videos.

**Notifications:**

- [ ] **POST /notifications/send:** Send a notification to a user.
- [ ] **GET /notifications/unread:** Get a list of unread notifications for the current user.

**Analytics:**

- [] **GET /videos/:id/analytics:** Get video analytics data (views, likes/dislikes, demographics, etc.) 