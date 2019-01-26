# mongo shell
````
# To display the database you are using, type db:
db
# select a db to use, 使用某个 db
use myDB 
# create a new DataBase
# If a database does not exist, MongoDB creates the database when you first store data for that database.
#  As such, you can switch to a non-existent database and perform the following operation in the [`mongo`] shell
use myNewDB
db.myNewCollection1.insertOne( { x: 1 } )

````
## collection
````
# If a collection does not exist, MongoDB creates the collection when you first store data for that collection.
db.myNewCollection2.insertOne( { x: 1 } )
db.myNewCollection3.createIndex( { y: 1 } )
# Both the `insertOne()` and the `createIndex()` operations create their respective collection if they do not already exist.

````

## Connection
```
# 指定一个非默认端口
mongo --port 28015

# 使用一个 connection string 
mongo mongodb://mongodb0.example.com:28015

# command-line option `--host <host>:<port>`
mongo --host mongodb0.example.com:28015

# use the `--host <host>` and `--port <port>` command-line options
mongo --host mongodb0.example.com --port 28015

```
## MongoDB Instance with Authentication
```
# You can use the `--username <user>` and `--password`, `--authenticationDatabase <db>` command-line options
mongo --username alice --password --authenticationDatabase admin --host mongodb0.examples.com --port 28015
# If you do not specify the password in the connection string, the shell will prompt for the password.

```
## stop start restart mongod
```
Additionally, if you have installed MongoDB using a package manager for [Ubuntu] or [Debian] then you can stop mongodb (previously mongod) as follows:

*   Upstart: `sudo service mongodb stop`

*   Sysvinit: `sudo /etc/init.d/mongodb stop`

Or on [Mac OS X]

*   Find PID of mongod process using `$ top`

*   Kill the process by `$ kill <PID>` 

Or on Red Hat based systems:

*   `service mongod stop`

```
