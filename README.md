# deployments

This repo contains files for doing a product deployment:

* Pre-requisites 
 - Generate a passwordless SSH between Jenkins Master & Kubernetes Master
 - update kubehosts with the Kubernetes Master IP address 
 - Install Python on Kuberntes Master: apt install python
 - Install Ansible on Jenkins Master or Set Ansible Master as a node to Jenkins
	- Create a local hosts file which refers to a demo group and Kubernetes Master

* Create a Jenkins Job which get the following parameters from the user:
 - deployenv (default to dev)
 - dbhost (default to devdb)
 - dbuser (default to devuser)
 - deployImage (defaults to wezvacicd)

* Update dockerhub.yml with the correct username & password

* Encrypt the dockerhub.yml using Ansible-Vault

* Using the parameters create deployvars.yml which has the respective variables and corresponding values:
deployenv: dev
dbhost: devdb
dbuser: devuser
deployImage: wezvacicd

* Invoke the playbook
echo "== Preparing the prerequiste =="
echo "deployenv: $deployenv" >> deployvars.yml
echo "dbhost: $dbhost" >> deployvars.yml
echo "dbuser: $dbuser" >> deployvars.yml
echo "deployImage: $deployImage" >> deployvars.yml

$ ansible-playbook deploy.yml -i kubehosts (or)
$ ansible-playbook deploy.yml --ask-vault-pass

