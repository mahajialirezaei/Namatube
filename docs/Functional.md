# Namatube Functional Requirements

## 1. User Management (U-01)
- **U-011 [High]:** User registration via email.
- **U-012 [High]:** User login (Email, Password, or OAuth).
- **U-013 [High]:** Token-based authentication (JWT) upon successful login.
- **U-014 [Medium]:** Profile editing capabilities.
- **U-015 [High]:** Password recovery via email.
- **U-016 [High]:** Session management (Logout, terminate active sessions).
- **U-017 [Medium]:** Two-Factor Authentication (2FA) support.

## 2. Video Management (V-01)
- **V-011 [High]:** Upload capability for users.
- **V-012 [High]:** Video placed in a processing queue upon upload.
- **V-013 [High]:** Transcoding into multiple resolutions/qualities.
- **V-014 [High]:** Automatic extraction of metadata (duration, title, thumbnail).
- **V-015 [High]:** Publish video after successful processing.
- **V-016 [Medium]:** Error handling and status logging for failed processing.
- **V-017 [Medium]:** Video deletion by the user.
- **V-018 [High]:** Privacy settings (Public / Unlisted / Private).
- **V-019 [Medium]:** Categorization upon upload.

## 3. Playback and Access (P-01)
- **P-011 [High]:** Adaptive bitrate streaming based on bandwidth.
- **P-012 [High]:** View counting mechanism.
- **P-013 [Medium]:** Tracking and saving watch history independently for users.
- **P-014 [High]:** Access control enforcement based on video privacy markers.

## 4. Search and Discovery
- **S-01 Search:** Full-text search on title/desc [High], Advanced filtering (Date, Popularity) [Medium], Autocomplete [Low], Tag/Metadata search [Medium].
- **R-01 Recommendations:** Personalized suggestions based on watch history [Medium], Trending content [High], Related/similar videos on watch page [Medium].

## 5. Interactions (C-01)
- **C-012 [High]:** Comment on videos.
- **C-013 [Medium]:** Reply to threads/comments.
- **C-014 [High]:** Like and Dislike actions on videos.
- **C-015 [High]:** Channel Subscriptions.
- **C-016 [Medium]:** User-generated content reports for violations.

## 6. Notifications (NO-01)
- **NO-011 [Medium]:** Alerts for new videos from subscribed channels.
- **NO-012 [Low]:** Mention/reply alerts.
- **NO-013 [Medium]:** System alerts for upload/processing completion.

## 7. App Features (Admin, Playlists, Library, Network)
- **A-01 Admin:** View violation reports [High], Suspend/Ban users [High], Delete violating videos [High], Monitor system health [Medium].
- **W-01 Playlists:** Create, update, and manage playlists [Medium].
- **L-01 Library/History:** Save for later [Medium], View/Clear watch history [Medium].
- **N-01/RP-01 Operations:** Network simulation tasks panel in admin (NAT, Subnetting, IPv4) [Low], Export reports to CSV/JSON [Low].
