4.1.X to 4.2 (Ubuntu)
=====================


Known Issues
-------------

* At present, qemu-kvm does not update cleanly.  You can avoid any
  issues with this by manually upgrading qemu-kvm prior to starting
  the chef-client run.  If you forget to do this, fear not.  The run
  will fail, at which point you can manually upgrade qemu-kvm and then
  run chef-client again with no issues.  Currently this takes a couple
  of runs.  Make sure you've got the havana repos set up.  I've filed
  a bug: https://bugs.launchpad.net/ubuntu/+source/qemu/+bug/1243403

  apt-get install -y qemu-kvm qemu-utils qemu-system-common qemu-system-x86


* The dependencies on the nova-common package in ubuntu are incorrect,
  resulting in the required version of python-cmd2 not being
  installed.  This means you get stack traces on nova-manage service
  list, for example.  This can be resolved by apt-get install
  python-cmd2.  We've filed a package bug here:
  https://bugs.launchpad.net/ubuntu/+source/nova/+bug/1242925


4.1.X to 4.2 (CentOS6/RHEL6)
============================


Known Issues
------------

* Openstack Dashboard requires manual upgrade. 
  RUN: `yum install openstack-dashboard` or else the package will not be 
  upgraded which causes horizon to look for quantumclient as an import. 
  Manually upgrading this package solves the issue. After this installation 
  run chef-client normally.

* Openstack Dashboard wants to upgrade the package 
  "python-django-openstack-auth.noarch" to version "1.1.2-1". This
  causes the dashboard to fail authentication and die. The specific error is,
  '"POST /auth/login/ HTTP/1.1" 403 1006' and is only seen when in single 
  server mode. To get around this, install the the previous package version 
  "1.0.11-1.el6". Presently you have to downgrade to the "1.0.11-1.el6" 
  package. 
  Bug filed Here: https://bugzilla.redhat.com/show_bug.cgi?id=1000391
