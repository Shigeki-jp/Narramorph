# Narramorph Database Design Draft (Neo4j)

## Main Nodes (Entities)

### 1. User
- userId (unique identifier, e.g. wallet address)
- userName
- firstAuthenticationDate
- profileInfo (optional)

### 2. Plot
- plotId (unique identifier, e.g. UUID)
- title
- contentText
- creationDate
- ownerId (linked to User node)
- tags (multiple)

### 3. Illustration
- illustrationId
- imageUrl or IPFS hash
- creationDate
- uploader (linked to User)

### 4. Comment
- commentId
- content
- postDate
- author (linked to User)

## Relationships

- (User)-[:FOLLOWS]->(User)  
  Follow relationships between users.

- (User)-[:CREATED]->(Plot)  
  User creates a plot.

- (Plot)-[:FORKED_FROM]->(Plot)  
  A plot branched from another plot (parent-child relation).

- (Plot)-[:HAS_ILLUSTRATION]->(Illustration)  
  Illustration attached to a plot.

- (User)-[:LIKED]->(Plot)  
  User likes a plot.

- (User)-[:COMMENTED]->(Comment)  
  User posts a comment.

- (Comment)-[:ON]->(Plot)  
  Comment belongs to a plot.

## Data Structure Visualization

```plaintext
(User)-[:CREATED]->(Plot)<-[:FORKED_FROM]-(Plot)
        \                     \
         [:LIKED]              [:HAS_ILLUSTRATION]->(Illustration)
        /
   (User)-[:FOLLOWS]->(User)
