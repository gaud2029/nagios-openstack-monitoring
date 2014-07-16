Monitoring Openstack using Nagios3 and NRPE agents

A sample Nagios deployment: http://108.244.166.6/nagios3/
username: nagiosadmin
password: nagiosadmin

Server Requirements: nagios3

Monitoring Client Node requirements: nagios-nrpe-server

- Keystone:
	- Nagios Server:
		- Host config: nagios-server/etc/nagios3/conf.d/openstack_controller_keystone_host.cfg
		- Service config: nagios-server/etc/nagios3/conf.d/openstack_controller_keystone_service.cfg
	- Keystone node:
		- NRPE plugins: 
			- client-os-controller-keystone/usr/lib/nagios/plugins/check_keystone
			- client-os-controller-keystone/usr/lib/nagios/plugins/check_service.sh
		- NRPE commands:
			- client-os-controller-keystone/etc/nagios/nrpe.d/openstack_keystone_checks.cfg

- Glance:

- Cinder:

- Nova:

- Swift: