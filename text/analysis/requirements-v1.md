---
id: requirements
aliases: []
tags: []
---

## Functional requirements

#### Authentication

- users are allowed to create accounts
- users can use OAuth 2.0 via common auth providers
  - google, discord, github, microsoft...

#### Authorization

- admin can manage users profiles
- admin can manage users sessions
- owner can promote other users to admins
- regular users (from now on just "users") cannot access other users' profiles

#### Session management

- users can can create/update/delete a session
  - timed session - working as a stopwatch
  - fixed session - known `from` and `to` dates
  - repeated session - takes place at the same time for given period
    - must specify time interval when the repeated session is active
    - must specify the frequency
      - supported periods are:
        - daily
        - weekly
        - biweekly
        - monthly
        - quaterly
        - half yearly
        - yearly
      - examples
        - every `day` at `8 pm` for `60 minutes`
        - every `week` on `monday` at `10:00` till `12:00`
- users can provide a description to a session

##### Tags

- users can create/delete/update tags
- users can change color of tag badge
- users can add multiple tags to a session
- users can create/delete/update category-specific tags
  - a category-specific tag can only be added to sessions with given category
- users can view detailed page for specified `tag`
  - this includes statistics only for given `tag`

##### Categories

- users can view detailed page for specified `category`
  - this includes statistics only for given `category`
- users must associate a session with a category
  - each session must have exactly one category

##### Statistics

- users can view statistics of their data for given time period
  - examples
    - total sessions
    - total time spent on sessions
    - current daily streak of sessions
- users can view and filter charts based on their sessions
  - filter criteria
    - `from` and `to` - time interval when the session took place
    - on or multiple `category` - specified category
    - on or multiple `tag` - specified tag

##### Misc

- users can export all sessions in json format
- users can import sessions from json files

---

## Non-functional requirements

- the system should support running on linux based machines
- the system should use english i18n
- the system should be hosted in cloud
- the system should not load any page for more than 3 seconds
- backend of the system should be written in rust
- frontend of the system should be written in typescript using nextjs
- postgresql should be used as the DB

