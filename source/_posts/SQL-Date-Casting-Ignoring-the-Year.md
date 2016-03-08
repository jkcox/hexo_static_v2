title: 'SQL Date Casting, Ignoring the Year'
tags:
  - SQL
  - Back-end
  - Database
categories:
  - Web Development
  - Back-End
  - SQL
date: 2016-02-24 10:39:00
author: John Cox
---
We were building an automated email that would send every Monday and let all employees know who had a birthday or work anniversary that week.

We quickly came across an issue with the data that required some brainstorming (and googling). Each record also had a random year, so our SQL query would need to ignore the year. 

Here is an example of how to use a query to find a date in a SQL database, ignoring the year. In this example we are looking for birthdays within a week.

``` mysql
SELECT first_name, last_name, birthday, photo_url
FROM birthday_db
WHERE DATEADD( Year, DATEPART( Year, GETDATE()) – DATEPART( Year, birthday), birthday)
BETWEEN CONVERT( DATE, GETDATE())
AND CONVERT( DATE, GETDATE() + 6)
```
The birthday is shifted to current year by adding the number of years between birthday and the current year. It does not matter if someone is born in 1970 or 1980, anyone within the specified 7 days will be returned.  After that, a simple date range comparison is used. ```CONVERT()``` allows us to ignore the timestamp and only use the date portion. Date format is ```YYYY-MM-DD```, where ```GETDATE()```returns ```YYYY-MM-DD HH:MI:SS```.