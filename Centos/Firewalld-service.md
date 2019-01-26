##  Cannot set LC_CTYPE to default locale: No such file or directory
````
$ locale
locale: Cannot set LC_CTYPE to default locale: No such file or directory
locale: Cannot set LC_ALL to default locale: No such file or directory
````

Open terminal and fire the below command:

```
export LC_ALL="en_US.UTF-8"
```

## How to Start and Enable Firewalld on CentOS 7
````
# Enable Firewalld
# To enable firewalld, run the following command as root:
systemctl enable firewalld

# Start Firewalld
# To start firewalld, run the following command as root:
systemctl start firewalld

# Check the Status of Firewalld
# To check the status of firewalld, run the following command as root:
systemctl status firewalld
````
Be Sociable, Share!

