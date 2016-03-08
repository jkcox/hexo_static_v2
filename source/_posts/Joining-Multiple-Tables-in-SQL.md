title: Joining Multiple Tables in SQL
date: 2016-02-25 14:03:36
tags:
  - SQL
  - Back-end
  - Database
  - ExactTarget
categories:
  - Web Development
  - Back-End
  - SQL
author: John Cox
---
This is just a simple example about how to join tables and how to deal with data from at least 3 tables.

In this example, ExactTarget is where our tables are being stored. The SQL queries are a part of an automation that will execute different steps depending on what action the end user completes. 

The first query runs daily, and is looking for an email address and subscriber key from our subscribers table, where the subscriber was sent the email that we name but did not open the email. We only want people who were sent the email 7 days ago. You can see we are using data from four different tables.
``` mysql
select EmailAddress, a.SubscriberKey
from _subscribers a
JOIN _Sent c
on a.SubscriberKey = c.SubscriberKey
JOIN _Job b
ON c.JobID = b.JobID
WHERE b.EmailName = 'Email_Name'
AND EventDate >=  DATEADD(day,-7, CONVERT( DATE, GETDATE()))
AND EventDate <  DATEADD(day,-6, CONVERT( DATE, GETDATE()))
AND
a.SubscriberKey NOT IN (SELECT SubscriberKey FROM _Open WHERE JobID = b.JobID)
```

The second query is very simliar to the first, the difference being that once our email that we named above is opened, we are querying to see if the end user who opened the email actually followed through and submitted their information to us that is captured on a landing page.

``` mysql
select EmailAddress, a.SubscriberKey
from _subscribers a
JOIN _Sent c
on a.SubscriberKey = c.SubscriberKey
JOIN _Click b
ON c.JobID = b.JobID
WHERE b.LinkName = 'link'
AND c.EventDate >=  DATEADD(day,-7, CONVERT( DATE, GETDATE()))
AND c.EventDate <  DATEADD(day,-6, CONVERT( DATE, GETDATE()))
AND a.SubscriberKey NOT IN (SELECT SubscriberKey FROM link_capture)
``` 

These examples are using data views that are built into ExactTarget.
You can find more info about ExactTarget data views [here](https://help.exacttarget.com/en/documentation/exacttarget/interactions/activities/query_activity/).