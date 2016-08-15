# training-infrastructure-polling-app

A polling application to keep the MuleSoft training application DB connection alive. Each request resets the max_timeout of the backing RDS database. 

The application polls each of these URLs: 

* In one flow: `polls mu.mulesoft-training.com/essentials/american` followed by  `mu.mulesoft-training.com/essentials/accounts/show`
* In one flow: `polls ilt.mulesoft-training.com/essentials/american` followed by  `ilt.mulesoft-training.com/essentials/accounts/show`

There is a an issue where any of these URLs will occassionally return a 500 status, or other exception, due to the training application keeping the DB connection open after the backing Amazon RDS (database) server (iltdb.mulesoft-training.com or mudb.mulesoft-training.com) exceeds its wait_timeout interval. 

Each flow in this app checks for a 500 result, and if a 500 result is returned, the flow tries again. The second HTTP request seems to succeed, and re-connects the training application to the Amazon RDS server. 

---
#Parameters

This application has the following parameters. Each is a polling frequency in seconds. 

- ilt.poll.frequency=40
- ilt.poll.frequency2=15
- mu.poll.frequency2=45
- mu.poll.frequency=40

---

Note: This application is a temporary kludge until we can get the DB connection pooling correct in the main training application. 
