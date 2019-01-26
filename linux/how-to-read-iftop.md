## Install iftop

First, turn on EPEL repo on Linux. See [how to install and enable epel repo on CentOS / RHEL / Scientific Linux v4.x/5.x/6.x](https://www.cyberciti.biz/faq/fedora-sl-centos-redhat6-enable-epel-repo/) for more information. Type the following [yum command to install iftop on](https://www.cyberciti.biz/faq/rhel-centos-fedora-linux-yum-command-howto/ "yum command usage") RHEL/CentOS/Fedora Linux:
```
yum -y install iftop
```

```
iftop
```
![iftop command result](https://upload-images.jianshu.io/upload_images/2319400-531fb5e62e287809.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

iftop will display these information.

The top level is a measurement unit. The addresses below is the interaction between your computer (for example is dev-machine-2.local) to the outside addresses. Each addresses has 2 connections in pair. Iftop show us the interaction at the 2, 10, 40 seconds interval.

For example, we will take a look on the top address.

    dev-machine-2.local in the preceding 2 seconds is sent 416 b data to the address 69.174.48.129
    In the preceding 10 seconds dev-machine-2.local is sent 6.83Kb data
    In the preceding 40 seconds dev-machine-2.local. 6.83Kb data

At the same time :

    69.174.48.129 in the preceding 2 seconds is sent 1.05Kb data to dev-machine-2.local
    In the preceding 10 seconds it sent 42.5Kb data
    In the preceding 40 seconds it sent 42.5Kb data again

At the bottom line, iftop show us the some results :

    Cumulative TX and RX data
    Peak TX and RX data over the last 40 seconds
    Total transfer rates averaged over 2 seconds, 10 seconds and 40 seconds

## Turn on Port display

To turn on port display, add -P option with iftop

    # iftop -P

## Display bandwidth rates in bytes/sec

By default, iftop will display rates in bits/sec. To display it in bytes/sec, we can use -B option.

    # iftop -B

