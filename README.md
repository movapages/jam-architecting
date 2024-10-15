### JAM Architecting
><small>JAM Architecting Workout</small>

#### 1. Objectives

#### 2. Event Booking System Overview

The overall flowchart of main processes to be implemented looks as followin (see the diagram below):

![Process List](Event%20Booking%20System%20Structure%20Flowchart.png)


#### 3. DBs & Data Models

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

> <small><strong>NB:</strong> Mobile first design implementation should adhere to well-known best practices - one-column layout, etc. Check the _login_ form sample below.</small>

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



#### 5. JAM-Stack PoC: Next-Auth + Sanity CMS

Please, check the PoC repository and demo pages.


#### 6. Deliverables & CI/CD

TBD
