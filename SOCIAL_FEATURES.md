# Social Features Documentation

## Overview
Comprehensive social functionality for the Emotion-Aware Music Recommendation Engine, enabling users to share, collaborate, and discover playlists within a vibrant community.

## Features Implemented

### 1. Playlist Sharing
**Backend:**
- `SharePlaylistRequest` - Configure sharing settings
- `PlaylistSharingService` - Manage share links and permissions
- Share tokens with UUID for secure access
- Configurable expiration dates
- Public/private visibility controls

**API Endpoints:**
- `POST /api/social/playlists/:id/share` - Share a playlist
- `GET /api/social/shared/:token` - View shared playlist
- `DELETE /api/social/playlists/:id/share` - Revoke share

**Frontend:**
- `SharePlaylistModal` component with visibility, permissions, and expiration settings
- One-click link copying
- Integrated into PlaylistView component

### 2. Follow System
**Backend:**
- `Follow` model with follower/following relationships
- `SocialService.followUser()` - Create follow relationship
- Mutual follow detection (isFollowing, isFollowedBy)
- Follow stats (followers count, following count)

**API Endpoints:**
- `POST /api/social/users/:id/follow` - Follow user
- `DELETE /api/social/users/:id/follow` - Unfollow user
- `GET /api/social/users/:id/follow-stats` - Get follow statistics
- `GET /api/social/users/:id/followers` - Get followers list
- `GET /api/social/users/:id/following` - Get following list

**Frontend:**
- `UserProfilePage` with follow/unfollow button
- Follower/following counts displayed
- Activity feed filtered by followed users

### 3. Public Playlist Gallery
**Backend:**
- `SharedPlaylist` model with isPublic flag
- Trending algorithm based on recent activity (likes, comments, shares)
- Time-range filtering (day, week, month)
- View count tracking

**API Endpoints:**
- `GET /api/social/playlists/public` - Browse public playlists
- `GET /api/social/playlists/trending` - Get trending playlists

**Frontend:**
- `DiscoverPage` with search, filters, and sorting
- Trending/Recent toggle
- Emotion-based color coding
- Grid layout with playlist previews
- Click to view shared playlist

### 4. Comments & Ratings
**Backend:**
- `PlaylistComment` model with nested replies
- `PlaylistRating` model (1-5 stars)
- Comment likes functionality
- Rating statistics with distribution

**API Endpoints:**
- `POST /api/social/playlists/:id/comments` - Add comment
- `GET /api/social/playlists/:id/comments` - Get comments
- `POST /api/social/comments/:id/like` - Like/unlike comment
- `DELETE /api/social/comments/:id` - Delete comment
- `POST /api/social/playlists/:id/rate` - Rate playlist
- `GET /api/social/playlists/:id/ratings` - Get rating stats

**Frontend:**
- `PlaylistComments` component with nested replies
- Real-time like updates
- Reply threading
- `SharedPlaylistPage` with 5-star rating system
- Rating distribution display

### 5. Collaborative Playlists
**Backend:**
- `CollaborativePlaylist` model
- Permission system (add/remove tracks, edit details, invite others)
- Invitation workflow (pending/accepted/declined)
- Collaborator management

**API Endpoints:**
- `POST /api/social/playlists/:id/collaborative` - Enable collaboration
- `POST /api/social/playlists/:id/collaborators` - Invite collaborator
- `POST /api/social/playlists/:id/collaborators/respond` - Accept/decline invitation
- `GET /api/social/playlists/collaborative` - Get collaborative playlists
- `DELETE /api/social/playlists/:id/collaborators/:userId` - Remove collaborator

**Features:**
- Granular permissions per playlist
- Invitation notifications
- Real-time collaboration tracking

### 6. Activity Feed
**Backend:**
- `Activity` model tracking user actions
- Activity types: playlist_created, playlist_shared, playlist_liked, playlist_commented, user_followed, collaboration_joined
- Global feed and personal feed (from followed users)
- Activity filtering by type
- TTL-based auto-cleanup (90 days)

**API Endpoints:**
- `GET /api/social/feed` - Get activity feed
- `GET /api/social/feed/global` - Get global feed

**Frontend:**
- `ActivityFeed` component with real-time updates
- Icon-based activity types
- Relative timestamps ("just now", "5m ago")
- User filtering (personal/global)
- Integrated into UserProfilePage

### 7. Notifications
**Backend:**
- `Notification` model
- Notification types: new_follower, playlist_liked, playlist_commented, comment_reply, collaboration_invite
- Read/unread status
- Auto-cleanup of old read notifications (30 days)

**API Endpoints:**
- `GET /api/social/notifications` - Get notifications
- `PUT /api/social/notifications/:id/read` - Mark as read
- `PUT /api/social/notifications/read-all` - Mark all as read
- `GET /api/social/notifications/unread-count` - Get unread count
- `DELETE /api/social/notifications/:id` - Delete notification

**Frontend:**
- Notification bell in Navigation with unread count badge
- Real-time notification updates

## Database Models

### Follow
```typescript
{
  follower: ObjectId (User),
  following: ObjectId (User),
  createdAt: Date
}
```

### SharedPlaylist
```typescript
{
  playlist: ObjectId (Playlist),
  owner: ObjectId (User),
  shareToken: String (UUID),
  isPublic: Boolean,
  allowComments: Boolean,
  allowCollaboration: Boolean,
  expiresAt: Date (optional),
  views: Number
}
```

### PlaylistComment
```typescript
{
  playlist: ObjectId (Playlist),
  user: ObjectId (User),
  content: String,
  parentComment: ObjectId (optional),
  likes: [ObjectId (User)]
}
```

### PlaylistRating
```typescript
{
  playlist: ObjectId (Playlist),
  user: ObjectId (User),
  rating: Number (1-5),
  review: String (optional)
}
```

### CollaborativePlaylist
```typescript
{
  playlist: ObjectId (Playlist),
  owner: ObjectId (User),
  collaborators: [ObjectId (User)],
  permissions: {
    canAddTracks: Boolean,
    canRemoveTracks: Boolean,
    canEditDetails: Boolean,
    canInviteOthers: Boolean
  },
  invitations: [{
    user: ObjectId,
    invitedBy: ObjectId,
    status: 'pending' | 'accepted' | 'declined',
    invitedAt: Date,
    respondedAt: Date
  }]
}
```

### Activity
```typescript
{
  user: ObjectId (User),
  type: ActivityType,
  action: String,
  targetType: 'playlist' | 'user' | 'emotion' | 'track',
  targetId: ObjectId (optional),
  metadata: Object,
  isPublic: Boolean
}
```

### Notification
```typescript
{
  user: ObjectId (User),
  type: NotificationType,
  from: ObjectId (User, optional),
  targetType: 'playlist' | 'comment' | 'invitation',
  targetId: ObjectId (optional),
  message: String,
  isRead: Boolean
}
```

## Frontend Components

### SharePlaylistModal
- Modal dialog for sharing playlists
- Visibility toggle (Public/Private)
- Permission checkboxes (Comments, Collaboration)
- Expiration dropdown (1/7/30/90 days or never)
- Share link with copy button

### DiscoverPage
- Public playlist gallery
- Search functionality
- Filter by trending/recent
- Time range selector
- Emotion-based color coding
- Grid layout with stats

### SharedPlaylistPage
- View shared playlists
- Emotion-themed header
- Track list display
- 5-star rating system
- Comment section
- View/like/comment/share stats

### PlaylistComments
- Nested comment threads
- Reply functionality
- Like/unlike comments
- Delete own comments
- Real-time updates

### ActivityFeed
- Activity stream display
- Icon-based activity types
- Relative timestamps
- Filter by user/global
- Clickable user profiles

### UserProfilePage
- User statistics (playlists, followers, following)
- Follow/unfollow button
- Activity feed tab
- Playlists tab
- Followers tab

## API Routes Summary

All routes prefixed with `/api/social/`

**Sharing:**
- POST `/playlists/:id/share`
- GET `/shared/:token`
- DELETE `/playlists/:id/share`
- GET `/playlists/public`
- GET `/playlists/trending`

**Following:**
- POST `/users/:id/follow`
- DELETE `/users/:id/follow`
- GET `/users/:id/follow-stats`
- GET `/users/:id/followers`
- GET `/users/:id/following`

**Comments:**
- POST `/playlists/:id/comments`
- GET `/playlists/:id/comments`
- POST `/comments/:id/like`
- DELETE `/comments/:id`

**Ratings:**
- POST `/playlists/:id/rate`
- GET `/playlists/:id/ratings`

**Collaboration:**
- POST `/playlists/:id/collaborative`
- POST `/playlists/:id/collaborators`
- POST `/playlists/:id/collaborators/respond`
- GET `/playlists/collaborative`
- DELETE `/playlists/:id/collaborators/:userId`

**Activity Feed:**
- GET `/feed`
- GET `/feed/global`

**Notifications:**
- GET `/notifications`
- PUT `/notifications/:id/read`
- PUT `/notifications/read-all`
- GET `/notifications/unread-count`
- DELETE `/notifications/:id`

## Usage Examples

### Share a Playlist
```typescript
const sharePlaylist = async (playlistId: string) => {
  const response = await axios.post(
    `http://localhost:5000/api/social/playlists/${playlistId}/share`,
    {
      isPublic: true,
      allowComments: true,
      allowCollaboration: false,
      expiresIn: 30 // days
    },
    {
      headers: { Authorization: `Bearer ${token}` }
    }
  );
  
  console.log('Share URL:', response.data.shareUrl);
};
```

### Follow a User
```typescript
const followUser = async (userId: string) => {
  await axios.post(
    `http://localhost:5000/api/social/users/${userId}/follow`,
    {},
    {
      headers: { Authorization: `Bearer ${token}` }
    }
  );
};
```

### Add a Comment
```typescript
const addComment = async (playlistId: string, content: string) => {
  const response = await axios.post(
    `http://localhost:5000/api/social/playlists/${playlistId}/comments`,
    { content },
    {
      headers: { Authorization: `Bearer ${token}` }
    }
  );
  
  return response.data;
};
```

### Rate a Playlist
```typescript
const ratePlaylist = async (playlistId: string, rating: number) => {
  await axios.post(
    `http://localhost:5000/api/social/playlists/${playlistId}/rate`,
    { rating, review: 'Great playlist!' },
    {
      headers: { Authorization: `Bearer ${token}` }
    }
  );
};
```

## Security Considerations

1. **Authentication:** All write operations require JWT token authentication
2. **Authorization:** Users can only delete their own comments/playlists
3. **Share Tokens:** UUID-based tokens prevent enumeration attacks
4. **Rate Limiting:** Express rate limiter prevents abuse
5. **Expiration:** Automatic cleanup of expired shares and old data
6. **Input Validation:** Content length limits on comments/reviews
7. **CORS:** Configured for specific frontend origin

## Performance Optimizations

1. **Indexes:** Strategic MongoDB indexes on frequently queried fields
2. **TTL Indexes:** Automatic cleanup of old activities and notifications
3. **Pagination:** Offset/limit support for large datasets
4. **Aggregation:** Efficient trending calculation using MongoDB aggregation
5. **Caching:** View counts updated incrementally
6. **Lazy Loading:** Frontend components load data on demand

## Future Enhancements

- Real-time notifications via WebSocket
- Playlist recommendations based on social graph
- User mentions in comments (@username)
- Rich media in comments (images, emojis)
- Playlist analytics dashboard
- Social sharing to external platforms (Twitter, Facebook)
- User badges and achievements
- Playlist collections/folders
- Advanced search with filters
- Mobile-optimized views
