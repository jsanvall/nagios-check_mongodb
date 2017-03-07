# nagios-check_mongodb
Check a MongoDB Database

Usage: 
``` 
check_mongodb -h 127.0.0.1 -u root -p 1234 -d local -q "db.test.findOne()"
```
Output:
```
OK - MongoDB

CRITICAL - Failed to execute query db.test.findOne() on MongoDB host 127.0.0.1
```

Requirements: 
```
mongodb client
```
