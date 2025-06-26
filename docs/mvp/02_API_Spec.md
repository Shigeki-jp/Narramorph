# API Design Draft for Narramorph

## 1. User APIs
### 1.1 Register User (Optional if using wallet)
- **POST** /users/register  
- Request: { username, email, password }  
- Response: { userId, username, createdAt }

### 1.2 Get User Info
- **GET** /users/{userId}  
- Response: { userId, username, profile, createdAt }

### 1.3 Follow User
- **POST** /users/{userId}/follow  
- Request: { followerId }  
- Response: { success: true }

### 1.4 Unfollow User
- **DELETE** /users/{userId}/follow  
- Request: { followerId }  
- Response: { success: true }

---

## 2. Plot APIs
### 2.1 Create New Plot
- **POST** /plots  
- Request: { userId, parentPlotId (nullable), title, content, tags, illustrationUrl }  
- Response: { plotId, createdAt }

### 2.2 Get Plot Details
- **GET** /plots/{plotId}  
- Response: { plotId, userId, title, content, tags, illustrationUrl, createdAt, likesCount, commentsCount }

### 2.3 Like a Plot
- **POST** /plots/{plotId}/like  
- Request: { userId }  
- Response: { success: true, totalLikes }

### 2.4 Comment on Plot
- **POST** /plots/{plotId}/comments  
- Request: { userId, commentText }  
- Response: { commentId, createdAt }

### 2.5 Get Plot Comments
- **GET** /plots/{plotId}/comments  
- Response: [ { commentId, userId, commentText, createdAt }, ... ]

---

## 3. Notification APIs
### 3.1 Get Notifications for User
- **GET** /users/{userId}/notifications  
- Response: [ { notificationId, type, message, read, createdAt }, ... ]

### 3.2 Mark Notification as Read
- **POST** /notifications/{notificationId}/read  
- Response: { success: true }

---

## 4. Search APIs
### 4.1 Search Plots by Tag or Keyword
- **GET** /search/plots?tag={tag}&keyword={keyword}  
- Response: [ { plotId, title, snippet, createdAt }, ... ]

---

## Notes
- Authentication is planned via wallet integration (e.g., Phantom) replacing traditional user registration.
- Plot ownership and key data are recorded on Solana blockchain as NFTs.
- Illustration uploads are stored and linked via IPFS.
- Neo4j is used to manage plot relationships and branching structures.

