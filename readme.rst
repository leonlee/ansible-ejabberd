ejabberd deploy
===============

========
Usage
========

`Ansible`_ can be used inside a `Virtualenv`_::

	$ virtualenv venv && source venv/bin/activate
	$ pip install ansible


In order to deploy the logging stack with `Ansible`_, run the *ansible-playbook* command against your
desired environment *inventory*::

    $ ansible-playbook -i inventory/<environment> jabber.yml

To deploy the following command can be used::

	$ ansible-playbook -i inventory/<environment> jabber.yml

Testing
-------

The ejabberd deploy project comes with a working `Vagrant`_ configuration including Vagrantfile and
vagrant inventory. To deploy to `Vagrant`_, simply::

    $ vagrant up
    $ ansible-playbook -i inventory/vagrant.inv jabber.yml

Note: Vagrant >= 1.5 is needed for this and the extensions pack is necessary

Note: this project uses https://github.com/smdahlen/vagrant-hostmanager

Note: it may take `Vagrant`_ a few seconds after boot to be available via SSH. If you want to check
the status of the `Vagrant`_ boxes you can::

    $ ansible -i inventory/vagrant.inv all -m ping

2 Test users are created by default 1. the admin user with password test, the other a user called test with the same password.

a web client is installed by default for testing purposes accesible in port 80.

for easy of testing this deployment comes with a vagrant file with 3 boxes debian,ubuntu,centos all install a fully functioning jabber server with a web client. aditional users should be created eihter with the ejabberd webui or ejabberdctl

EC2
---

to provision EC2 you can use::
  
  ansible-playbook -i inventory/local.inv ec2-prov.yml

you will need to have aws_vars/aws-creds.yml with your credential for this to work.

after ec2 has been provisioned you can deploy with::

  ansible-playbook -i ec2.py jabber.yml

there is a bit of an issue here using default cominity AMI's and is that they all have root disabled and no default standart user, so you will have to use -u ubuntu or whatever default user there is for debian and centos distro


.. _`Ansible`: http://ansible.com
.. _`Virtualenv`: http://www.virtualenv.org/
.. _`Vagrant`: http://www.vagrantup.com/