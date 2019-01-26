# start mongodb
```
sudo service mongod start
```
# Verify that MongoDB has started successfully
You can verify that the `mongod` process has started successfully by checking the contents of the log file at`/var/log/mongodb/mongod.log` for a line reading
```
[initandlisten] waiting for connections on port <port>
```
where <port> is the port configured in /etc/mongod.conf, 27017 by default.

You can optionally ensure that MongoDB will start following a system reboot by issuing the following command:
```
sudo chkconfig mongod on
```
# Stop MongoDB
As needed, you can stop the `mongod` process by issuing the following command:
```
sudo service mongod stop
```
# Restart MongoDB
You can restart the `mongod` process by issuing the following command
```
sudo service mongod restart
```
You can follow the state of the process for errors or important messages by watching the output in the /var/log/mongodb/mongod.log file.

# Uninstall MongoDB Community Edition
To completely remove MongoDB from a system, you must remove the MongoDB applications themselves, the configuration files, and any directories containing data and logs. The following section guides you through the necessary steps.

## 1  Stop MongoDB
```
sudo service mongod stop
```
## 2 Remove Packages
Remove any MongoDB packages that you had previously installed.
```
sudo yum erase $(rpm -qa | grep mongodb-org)
```
## 3 Remove Data Directories
Remove MongoDB databases and log files.
```
sudo rm -r /var/log/mongodb
sudo rm -r /var/lib/mongo
```
