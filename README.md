swift-setup, Openstack Swift install scripts


1. Dependencies:

	python2.7
	fabric, python library


2. Setup:

  a. Nodes:

	Configure the settings for a swift cluster in config.py

	A cluster consists of proxy nodes and worker nodes.
	Proxies are connected to to interact with a swift installation
	and are network bandwidth dependent. Workers actually store
	objects on disk and are cpu/disk dependent. An individual node
	can be both a proxy and worker, and a cluster can have multiple
	proxies! For more information on Swift check the documentation
	at: http://docs.openstack.org/developer/swift/

	One boss machine should be set, where we will build swift 
	specific configuration files. Swift must be installed on the
	boss machine so it is recommended to make this a machine in
	the cluster.

	One object expirer per cluster should be defined as well.

	If an ssh key is set, the variable keyfile should be the path, to
	the private key. Additionally a password can be set, or read in
	when the script is run with machinedef.prompt_for_password().

	Ideally A cluster should consist of at least 3 machines. If there
	are less worker nodes then the replication factor (repfactor variable)
	must be set accordingly.

  b. Filesystem

	The worker nodes require a filesystem that supports xattrs.
	We can set up a loopback filesystem, and if so, dev_setup should
	be set to True. Swift assumes we are using a separate partition
	for storage, however we can disable it by setting uselocalfs to True.
	Various filesystem parameters can be set, check config.py or machinedef.py for mor info. 

	The Default sets up a 2 GB loopback filesystem in /srv/node, mounted at /srv/node/swiftfs

  c. Authentication System

  	We can use either the tempauth system that comes with swift, or Swauth, a more developed auth system. By default we install swauth (and it is recommended) but tempauth can still be installed. For more info on tempauth check the Swift documentation listed above. For more info on Swauth check the github repo here: 
  	https://github.com/gholt/swauth


3. Usage

  a. Installation

  	To run a full installation: fab swift_install
  	!! Make sure all the configure options are set in config.py !!

  b. Utility

  	To restart all swift processes: fab swift_restart
  	To distribute ring files: fab distribute_rings


4. Copyright

	Copyright (c) 2013 University of Victoria 
 
	Permission is hereby granted, free of charge, to any person obtaining a copy of this software 
	and/or hardware specification (the “Work”) to deal in the Work without restriction, including 
	without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or 
	sell copies of the Work, and to permit persons to whom the Work is furnished to do so, subject to 
	the following conditions: 
	 
	The above copyright notice and this permission notice shall be included in all copies or 
	substantial portions of the Work. 
	 
	THE WORK IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS 
	OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF 
	MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND 
	NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT 
	HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, 
	WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, 
	OUT OF OR IN CONNECTION WITH THE WORK OR THE USE OR OTHER DEALINGS 
	IN THE WORK.