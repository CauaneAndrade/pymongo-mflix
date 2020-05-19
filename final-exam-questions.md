# Final Exam

```Python

```

## Final: Question 1
### Problem:

Assume a collection called elections that holds data about all United States Presidential Elections since 1789.
All the documents in the elections collection look like this:

```Python
{
  "year" : 1828,
  "winner" : "Andrew Jackson",
  "winner_running_mate" : "John C. Calhoun",
  "winner_party" : "Democratic",
  "winner_electoral_votes" : 178,
  "total_electoral_votes" : 261
}
```

total_electoral_votes represents the total number of electoral votes that year, and winner_electoral_votes represents the number of electoral votes received by the winning candidates.

Which of the following queries will retrieve all the Republican winners with at least 160 electoral votes?

### Choose the best answer:

```Python
db.elections.find( { "winner_party": "Republican",
                     "winner_electoral_votes": { "$gte": 160 } } )
```


## Final: Question 2
### Problem:

Consider a collection of phones called phones, used by a phone manufacturer to keep track of the phones currently in production.

Each document in phones looks like this:

```Python
{
  "model": 5,
  "date_issued" : ISODate("2016-07-27T20:27:52.834Z"),
  "software_version": 4.8,
  "needs_to_update": false
}
```

There is an update required for phones with software_version earlier than 4.0. Anyone still using a version older than 4.0 will be asked to update.

The phone manufacturer wants to set the flag needs_to_update to true when the value of software_version is lower than 4.0. For example, a document like this one:


```Python
{
  "model": 5,
  "date_issued" : ISODate("2014-03-04T14:23:43.123Z"),
  "software_version": 3.7,
  "needs_to_update": false
}
```

```Python
{
  "model": 5,
  "date_issued" : ISODate("2014-03-04T14:23:43.123Z"),
  "software_version": 3.7,
  "needs_to_update": true
}
```

### Choose the best answer:

```Python
db.phones.update_many( { "software_version": { "$lt": 4.0 } },
                       { "$set": { "needs_to_update": True } } )
```

## Final: Question 3
### Problem:

Suppose an instance of MongoClient is created with the default settings:

```Python
from pymongo import MongoClient

uri = "mongodb+srv://m220-user:m220-pass@m220-lessons-mcxlm.mongodb.net/test"
mc = MongoClient(uri)

mc.stats
```

What will be the output of mc.stats?

### Choose the best answer:

```Python
Database(MongoClient(host=['m220-lessons-shard-00-02-mcxlm.mongodb.net:27017', 'm220-lessons-shard-00-00-mcxlm.mongodb.net:27017', 'm220-lessons-shard-00-01-mcxlm.mongodb.net:27017'], document_class=dict, tz_aware=False, connect=True, authsource='admin', replicaset='m220-lessons-shard-0', ssl=True), 'stats')
```

## Final: Question 4
### Problem:

Suppose a client application is sending writes to a replica set with 3 nodes:

    `IMAGE`

Before returning an acknowledgement back to the client, the replica set waits.

When the write has been applied by the nodes marked in stripes, it returns an acknowledgement back to the client.

What Write Concern was used in this operation?

### Choose the best answer:

```Python
w: majority
```

## Final: Question 5
### Problem:

Given the following bulk write statement, to a collection called employees:

```Python
requests = [
  InsertOne({ '_id': 11, 'name': 'Edgar Martinez', 'salary': "8.5M" }),    # Insert #1
  InsertOne({ '_id': 3, 'name': 'Alex Rodriguez', 'salary': "18.3M" }),    # Insert #2
  InsertOne({ '_id': 24, 'name': 'Ken Griffey Jr.', 'salary': "12.4M" }),  # Insert #3
  InsertOne({ '_id': 11, 'name': 'David Bell', 'salary': "2.5M" }),        # Insert #4
  InsertOne({ '_id': 19, 'name': 'Jay Buhner', 'salary': "5.1M" })         # Insert #5
]

response = employees.bulk_write(requests)
```

Assume the employees collection is empty, and that there were no network errors in the execution of the bulk write.

Which of the insert operations in requests will succeed?

### Check all answers that apply:
- Insert #1
- Insert #2
- Insert #3


## Final: Question 6
### Problem:

Suppose a client application is sending writes to a replica set with three nodes, but the primary node stops responding:

Assume that none of the connection settings have been changed, and that the client is only sending insert statements with write concern w: 1 to the server.

After 30 seconds, the client still cannot connect to a new primary. Which of the following exceptions will be raised by Pymongo?

### Choose the best answer:
- ServerSelectionTimeoutError

## Final: Question 7
### Problem:

Assume a collection called people_heights with documents that look like this:

```Python
{
  "name": "Ada",
  "height": 1.7
}
```

Which of the following queries will find only the 4th- and 5th-tallest people in the people_heights collection?

### Choose the best answer:

```Python
db.people_heights.find().sort("height", -1).skip(3).limit(2)
```