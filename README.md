# Aritain_infra
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

#cloud_testapp HW description

testapp_IP = 35.190.205.2

testapp_port = 9292

In this homework an instance for application deployment was created in GCP.

For installing all dependancies and deploying the application itself the 3 .sh files were created: install_ruby.sh, install_mongodb.sh and deploy.sh.

Also, as an additional task there was created an .sh file as a startup script for GCP instance deployment. This script was used as a part of GCP instance console creation command:


	gcloud compute instances create reddit-app-test\
  	--boot-disk-size=10GB \
  	--image-family ubuntu-1604-lts \
  	--image-project=ubuntu-os-cloud \
  	--machine-type=g1-small \
  	--tags puma-server \
  	--metadata-from-file startup-script=/home/ganhart/otus/Aritain_infra/startup_script.sh \
  	--restart-on-failure

As the last task, the firewall GCP rule was created via server's console with a following command:

	gcloud compute --project=oceanic-monitor-262408 firewall-rules create default-puma-server --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:9292 --source-ranges=0.0.0.0/0 --target-tags=puma-server

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

#cloud_bastion HW description

bastion_IP = 35.210.214.67

someinternalhost_IP = 10.132.0.4


The following command can be used for a direct access to internal host in GCP via bastion host

	ssh -t -i ~/.ssh/Ganhart -A Ganhart@*External bastion IP* ssh *Internal host IP*


To simplify the access to internal host the alias was configured in ssh configuration file, so the following command can be used

	ssh someinternalhost

Here is the listing of the SSH configuration file:

	host bastion
        	User Ganhart
        	HostName 35.210.214.67
        	Port 22
        	IdentityFile ~/.ssh/Ganhart
        	ForwardAgent yes

	host someinternalhost
        	User Ganhart
        	hostname 10.132.0.4
        	Port 22
        	ProxyJump bastion

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

Useful stuff:

Adding a public key for GCP access

        eval $(ssh-agent)
        ssh-add ~/.ssh/Ganhart
        ssh-add -L - key check
