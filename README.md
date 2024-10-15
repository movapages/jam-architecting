### JAM Architecting
><small>JAM Architecting Workout</small>

#### 1. Objectives

#### 2. Event Booking System Overview

The overall flowchart of main processes to be implemented with the application looks as following (see the diagram below):

![Process List](Event%20Booking%20System%20Structure%20Flowchart.png)


#### 3. DBs & Data Models

Redis DB interconnectivity fits in Next.js capabilities with the mediation of [redis](https://www.npmjs.com/package/redis) package. However, it may be useful even with Redis to implement kind of caching mechanism, if the need arises.

##### ___Redis DB Basic structure___


````
 +-------------------------------+        +-------------------------------+
 |          Event List           |        |       Event Booking           |
 +-------------------------------+        +-------------------------------+
 | id            (PK)            | <----- | event_id       (FK)           |
 | title                         |        | user_id                       |
 | notes                         |        +-------------------------------+
 | datetime                      |
 | owner_id                      |
 | status                        |
 +-------------------------------+
````

##### ___Redis DB Data Samples___
````
# Event -

event:123
  id       : 123
  title    : "Team Meeting"
  notes    : "Discuss project updates"
  datetime : "2024-10-20T15:30:00"
  owner_id : 1
  status   : "scheduled"

# Event Booking (Users who booked event 123) -

event_bookings:123
  1   # User ID 1 booked the event
  2   # User ID 2 booked the event
````

##### ___Redis DB CRUD Query Examples___

1. <ins>Create a new event</ins>

````
HMSET event:123 id 123 title "Team Meeting" notes "Weekly sync-up" datetime "2024-10-20T15:30:00" owner_id 1 status "scheduled"
````

2. <ins>Book an Event</ins>

````
SADD event_bookings:123 1  # User 1 books the event
SADD event_bookings:123 2  # User 2 books the event
````

3. <ins>List all users per event</ins>

````
SMEMBERS event_bookings:123
````

#### 4. UI Mockups, UI Libs

1. <ins>User Authentication</ins>

![User Authentication](Container_web_user_authentication.png)

> <small><strong>NB:</strong> Mobile first design implementation should adhere to well-known best practices - one-column layout built on top of media queries, etc. Check the _login_ form sample below.</small>

![Mobile-first](Container_login_register.png)

2. <ins>Event Dashboard</ins>

![Dashboard](EventTrack%20-%20Event%20List%20Dashboard.png)

3. <ins>Single Event View</ins>

![Single Event](EventTrack%20-%20Event%20View.png)

4. <ins>Event Update</ins>

![Event Update](EventTrack%20-%20Event%20Edit.png)

> <small><strong>NB:</strong> It's possible to make use of in-place editing for each field separately.</small>
 
5. <ins>Event Create</ins>

![Event Create](EventTrack%20-%20Event%20Create.png)


6. <ins>Admin Panel</ins>

Admin panel should employ the same framework of React components shared with User UI, namely: dashboard and single event view.
Plus, one more state to list all registered users (read-only mode).
For this it may suffice to widen the dashboard component API to enable it listing different data sets by means of extra configuration object.

It may happen the customer will require a hardened access control to the panel and resources pertained to it,
and separate (physically) this resource from common userland; it means this part may be hosted/deployed on a different domain/host, and 
reside in a separate repository, etc.

To make all sharable parts available for both applications and keep them in sync in the process of constant development, we may consider use of Nx monorepo...


#### 5. JAM-Stack PoC: Next-Auth + Sanity CMS

Please, check the PoC repository and demo pages.


#### 6. Deliverables & CI/CD

TBD
