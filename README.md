bash-emr
========

This is a simple set of bash functions for manipulating a
Amazon Elastic MapReduce clusters.

This work is licensed under a [Creative Commons Attribution 3.0 Unported License](http://creativecommons.org/licenses/by/3.0/).

Install
-----

You must install the [Elastic MapReduce Ruby client](http://aws.amazon.com/code/Elastic-MapReduce/2264).

You then must set the __EMR_HOME__ environment variable to the 
ruby client install root directory.

    export EMR_HOME=/path/to/elastic-mapreduce-ruby

Finally, you must source the `setenv.sh` file

    . setenv.sh

Setting __EMR_CRED_JSON__ will allow you to override the `credentials.json` file required by the elastic-mapreduce-ruby client.

Usage
-----

To find an existing cluster:

	emrlist
	
To attach to a cluster, using a _flow id_:

    emrset <flow id>	

To get the current _flow id_:

	emrset

To remotely login to the master node of the current _flow id_:

	emrlogin
	
To remotely login with just the ip address:

	emrlogin <ip address>	

Note that most commands will take the _flow id_ or an _ip address_ to override the default _flow id_ set using `emrset`.

Reference
---------

### emr
This is shorthand for calling from the shell.
    
    emr <some args>

### emrset
When you start a flow on EMR, you will be given a flow id. 
Use __emrset__ to set the flow id for use by many of the other commands
    
    emrset <flow id>
      
Calling __emrset__ without the id returns the current flow id.

### emrlist
Will return all job flows created in the last 2 days

### emrhost
Will return the current master node on the EMR cluster.

### emrlogin
Will remotely login to the master node. 

### emrstat
Will return the current status of a given running flow.

### emrterminate
Will terminate your remote EMR cluster.

### emrscreen
Will launch screen on the master node. Screen must be already installed.
If a screen instance is already running, this command will automatically attach.

### emrtail
Will automatically 'tail' the current flow step logs.
    
    emrtail 2

Without a step number, a list of available steps will be displayed.

### emrproxy
Will create a local SOCKS proxy to the master node. This is useful for accessing
the JobTracker and NameNode. You must install FoxyProxy in FireFox for this to 
work best.

### emrscp
Will scp a given file to the remote master node.
    
    emrscp my-hadoop-app.jar

This is useful if you leave your EMR cluster running and want to manually spawn 
jobs from __emrlogin__ or __emrscreen__.

### emrconf
Will scp all `conf/*-site.xml` files from the master node into the given directory.
    
    emrconf local-conf

This is useful if you leave your EMR cluster running on a AWS VPC and wish to run Hadoop jobs from a local shell.

