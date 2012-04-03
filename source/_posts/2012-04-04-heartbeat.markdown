---
layout: post
title: "Heartbeat Install Guide"
date: 2012-04-04 00:25
comments: true
categories: cloud
---
##What - The use of Heartbeat

Heartbeat is a High-Availability ( HA ) system which keep service alive. For example, Server_1 has a httpd service, and once if it had been shutdown accidently, then the service will stop. There's a workaround for this situation, prepare Server_2 and duplicate the service settings on it. Install Heartbeat on both of them. When Heartbeat starts working on both servers, it provides a virtual ip. If any one of servers stop working, the other one will takeover the job.

The clients are linking to the virtual ip, they don't know the server has been shutdown. Heartbeat guarantees the service will keep serving clients when any one of its server is alive.

##How - Install Heartbeat

###Environment

Server_1

* CentOS 5.6
* ip: 192.168.0.1

Server_2

* CentOS 5.6
* ip: 192.168.0.2

Virtual ip: 192.168.0.200


### Step 1

It's really easy to install heartbeat on RHEL5 / CentOS.

    wget -O /etc/yum.repos.d/clusterlabs.repo http://clusterlabs.org/rpm/epel-5/clusterlabs.repo
    yum install -y heartbeat

We're going to use httpd for testing, if you don't have this…

    yum install -y httpd

NOTICE: Both serevers require heartbeat and httpd be installed.

### Step 2

Next, copy configurations. NOTICE: Your heartbeat version might be different.

    cp /usr/share/doc/heartbeat-3.0.3/authkeys /etc/ha.d/
    cp /usr/share/doc/heartbeat-3.0.3/ha.cf /etc/ha.d/
    cp /usr/share/doc/heartbeat-3.0.3/haresources /etc/ha.d/

### Step 3

Setting up the authkeys

    vim /etc/ha.d/authkeys

Type

    auth 1 # auth num
    1 md5 dalema # auth num, auth method, auth secret

Change privilege

	chmod 600 /etc/ha.d/authkeys

### Step 4

Setting up ha.cf

Append the settings on the tail of ha.cf

	logfile /var/log/ha.log
	keepalive 2
	deadtime 30
	initdead 120
	bcast eth0
	auto_failback on
	node Server_1 # Server 1's hostname
	node Server_2 # Srever 2's hostname
	ping 192.168.0.25 # it's your gateway ip
	respawn hacluster /usr/lib64/heartbeat/ipfail
	apiauth ipfail gid=haclient uid=hacluster

### Step 5

Setting up the haresources.

Append

    # point current server's httpd service to the virtual ip
    Server_1 192.168.0.200

### Step 6

Copy settings to Server_2

	scp -r /etc/ha.d/ root@192.168.0.2:/etc/

### Step 7

Write some html for testing.

On Server_1

	echo "It's Server_1, my heart is beating." > /var/www/html/index.html

On Server_2

	echo "It's Server_1, my heart is beating." > /var/www/html/index.html

### Step 8

Test heartbeat is working or not.

Start the service on both serevers ( It takes 2 mins )

	service heartbeat restart

or

	/etc/init.d/heartbeat start

Use browser to connect http://192.168.0.1 and http://192.168.0.200,
Both should work well. And http://192.168.0.2 should be no response.

Then shutdown Server_1's heartbeat

    service heartbeat stop

Now, http://192.168.0.2 and http://192.168.0.200 should be workable, and http://192.168.0.1 should be no response.

If you restart the heartbeat on Server_1, the Server_2's job will be taken over by Server_1.

    service heartbeat start

Heartbeat will automatically handle your httpd, you don't have to worry about that. For the clients outside the cluster, they should connect to the virtual ip.

## Troubleshoot

The udpport default is 694, make sure you did not block it in your firewall.

And make sure your library in ha.cf has right version, 64-bit is /usr/lib64/..., 32-bit is /usr/lib/...

## Resources

Heartbeat could use with Pacemaker, or use corosync instead of Heartbeat. For more detail, visit

[Official Guide](http://www.linux-ha.org/doc/users-guide/users-guide.html)
