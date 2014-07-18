Monitoring Openstack using Nagios3 and NRPE agents

A sample Nagios deployment: http://108.244.166.6/nagios3/
username: nagiosadmin
password: nagiosadmin

- Overall Requirements:
	- Server: nagios3
	- Client Node: nagios-nrpe-server
	- API Checks: Openstack tenant with username and password. In these scripts a tenant: cookbook with username: admin and password: openstack has been used.


- Keystone:
	- Nagios Server:
		- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_keystone_host.cfg
		- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_keystone_service.cfg
	- Nagios Agent:
		- NRPE plugins: 
			- client-os-controller-keystone/usr/lib/nagios/plugins/check_keystone
			- client-os-controller-keystone/usr/lib/nagios/plugins/check_service.sh
		- NRPE commands:
			- client-os-controller-keystone/etc/nagios/nrpe.d/openstack_keystone_checks.cfg

- Glance:
	- Nagios Server:
		- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_glance_host.cfg
		- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_glance_service.cfg
	- Nagios Agent:
		- NRPE plugins: 
			- client-os-controller-glance/usr/lib/nagios/plugins/check_glance_api
			- client-os-controller-glance/usr/lib/nagios/plugins/check_service.sh
		- NRPE commands:
			- client-os-controller-glance/etc/nagios/nrpe.d/openstack_glance_checks.cfg


- Cinder:
	- Volume Controller:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_cinder_host.cfg
			- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_cinder_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- client-os-controller-cinder/usr/lib/nagios/plugins/check_cinder-api
				- client-os-controller-cinder/usr/lib/nagios/plugins/check_service.sh
			- NRPE commands:
				- client-os-controller-cinder/etc/nagios/nrpe.d/openstack_cinder_controller_checks.cfg
	- Volume node:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_node_cinder_host.cfg
			- Service config: nagios-server/etc/nagios3/conf.d/openstack_node_cinder_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- client-os-controller-cinder/usr/lib/nagios/plugins/check_service.sh
			- NRPE commands:
				- client-os-controller-cinder/etc/nagios/nrpe.d/openstack_cinder_node_checks.cfg
	
- Nova:
	- Compute Controller:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_nova_host.cfg
			- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_nova_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- client-os-controller-nova/usr/lib/nagios/plugins/check_nova-api
				- client-os-controller-nova/usr/lib/nagios/plugins/check_service.sh
			- NRPE commands:
				- client-os-controller-nova/etc/nagios/nrpe.d/openstack_nova_controller_checks.cfg

	- Compute Node:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_node_nova_host.cfg
			- Service config: 
				- nagios-server/etc/nagios3/conf.d/openstack_node_nova_service.cfg
				- nagios-server/etc/nagios3/conf.d/openstack_node_kvm_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- client-os-controller-nova/usr/lib/nagios/plugins/check_nova-api
				- client-os-controller-nova/usr/lib/nagios/plugins/check_service.sh
				- client-os-controller-nova/usr/lib/nagios/plugins/check_kvm_cpustats
				- client-os-controller-nova/usr/lib/nagios/plugins/check_kvm_instance
				- client-os-controller-nova/usr/lib/nagios/plugins/check_kvm_memstats
			- NRPE commands:
				- client-os-controller-nova/etc/nagios/nrpe.d/openstack_nova_node_checks.cfg
				- client-os-controller-nova/etc/nagios/nrpe.d/openstack_kvm_checks.cfg
	
- Swift:
	- Object Store Controller:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_swift_host.cfg
			- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_swift_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- client-os-controller-nova/usr/lib/nagios/plugins/check_swift
			- NRPE commands:
				- client-os-controller-swift/etc/nagios/nrpe.d/openstack_swift_controller_checks.cfg

	- Object Store Node:
		- Nagios Server:
			- Host config: nagios-server/etc/nagios3/conf.d/openstack_node_swift_storage_{1..4}_host.cfg
			- Host Group config: nagios-server/etc/nagios3/conf.d/openstack_node_swift_hostgroup.cfg
			- Service config: nagios-server/etc/nagios3/conf.d/openstack_node_swift_storage_service.cfg
		- Nagios Agent:
			- NRPE plugins: 
				- No custom plugin.
			- NRPE commands:
				- client-os-node-swift/etc/nagios/nrpe.d/openstack_swift_node_checks.cfg
