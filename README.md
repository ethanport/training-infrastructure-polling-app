# training-infrastructure-polling-app
A polling application to keep the MuleSoft training application DB connection alive. Each request resets the max_timeout of the backing RDS database. 

#Parameters
This application has the following parameters. Each is a polling frequency in seconds. 

- ilt.poll.frequency=40
- ilt.poll.frequency2=15
- mu.poll.frequency2=45
- mu.poll.frequency=40
