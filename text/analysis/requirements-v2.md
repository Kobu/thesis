---
id: requirements-v2
aliases: []
tags: []
---

## Functional requirements

#### User management

- users can view other users profiles
  - this displays:
    - recent activity
    - most used tags
    - most used categories
    - activity chart
- users can set their profiles to private or public
  - public profile -> whole profile can be viewed
  - private profile -> no profile information is accessible for users
- users can create ad-hoc user groups
  - this is possible for private AND public profiles
  - ad-hoc user group can be shared with an URL link
  - this link can be shared with other users who can then join this session as participants
  - creator of the group can set category, tags and duration of the sessions
  - all participants of the group need to "Ready up", only then the session can be started by creator of the group
  - this session is recorded in users history and statistics
    - including all participants

#### Session management

##### Tags

- users can create nested tags
  - ordinal tag: `life`
  - nested tag: `life/self-help/reading`
  - users can filter based on any part of the nested tag, eg `life/self-help`, `life`

#### UI/UX

- users can specify custom theme
- users can save custom filter on their dashboard (MORE INFO NEEDED)

## Non-functional requirements

- cli app should be written in rust or python
