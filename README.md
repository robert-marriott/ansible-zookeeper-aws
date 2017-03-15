# ansible-zookeeper-aws
## Test playbook to deploy zookeeper on an AWS cluster that is already standing

### Assumptions:
* Machines exist
* CentOS 6 Hosts

### Tasks:
* Check Java version
   * Update Java
* Install Zookeeper on target machines

### Start ssh agent with your key
```sh
$ ssh-agent bash
$ ssh-add ~/.ssh/YOUR_KEY.pem
```

### Install ansible Oracle Java install plugin
This has an included role to verify Java on the target machine
```sh
$ ansible-galaxy install ansiblebit.oracle-java
```

### Modify _local_ hosts file to point to your hosts
```# Main list of hosts to install zookeeper on
# Main list of hosts to install zookeeper on
[zookeepernodes]
some.ip.address.es zookeeper_id=1
some.ip.address.es zookeeper_id=2

# Host if targeting a single installation
[zookeeper-standalone]
some.ip.address.es zookeeper_id=1

# Hosts for cluster mode
[zookeeper-cluster]
some.ip.address.es zookeeper_id=1
some.ip.address.es zookeeper_id=2
```
Copy hosts file to ansible directory
```sh
$ cp hosts /usr/local/etc/ansible/hosts
```

### Run the ansible playbook
```
$ ansible-playbook zookeeper_cluster.yml
```
