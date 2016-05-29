# vagrant-ansible-mesos

Mesos cluster. Tested with 2 nodes on VirtualBox.

## Initialize

	cp conf/zoo.cfg.sample conf/zoo.cfg

## Run

	vagrant up
	ansible-playbook --private-key=~/.vagrant.d/insecure_private_key -u vagrant -i staging site.yml

## Test

	MASTER=$(mesos-resolve `cat /etc/mesos/zk`)
	mesos-execute --master=$MASTER --name="cluster-test" --command="sleep 5"

## Troubleshooting

- "Failed to connect to the host via ssh."
You might get this error after running `vagrant destroy && vagrant up` because the ECDSA host key for 192.168.9.11 will have changed. The suggested sollution is: `ssh-keygen -f "~/.ssh/known_hosts" -R 192.168.9.11`. Try to manually connect via ssh, to see if this is the case.

	ssh -i ~/.vagrant.d/insecure_private_key vagrant@192.168.9.11 -p 22

- Gathering facts

	ansible --private-key=~/.vagrant.d/insecure_private_key -u vagrant -i staging -m setup all

## More information

- https://open.mesosphere.com/getting-started/install/

