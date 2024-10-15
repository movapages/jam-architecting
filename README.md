### JAM Architecting
><small>JAM Architecting Workout</small>

#### 1. Objectives

#### 2. Event Booking System Overview

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

##### ___Redis DB CRUD___

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



#### 5. Required JAM-Stack PoC



#### 6. Deliverables?


