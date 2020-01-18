# Aritain_infra

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

### ansible-1 HW description

In this homehowrk a few basic things with ansible was done. Basically there was created a correcponding directory with a few configuration files:


ansible.cfg - which is self-explanatory, it hold some configuration values which can be used accross all project (basically a usename and it's keys)

inventory & inventory.yml - a list of hosts to work with, the difference with these files is that the .yml one uses the yaml markup

clone.yml - is the first playbook created, it sayd what to do with some hosts already mentioned in inventory files


During this HW we've tried to launch clone.yml but it basically did nothing because terraform already installing the application itself so we had to actually delete the application holder to see the result on ansible execution.

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

### terraform-2 HW description

During this homework the basics of moduling in terraform was learned, so a few of module directories were created including:

app - for application server deployment
db - for db server desployment
vpc - for firewall GCP rule creating


Also the terraform project itself was splitted on two parts: stage and prod. So the corresponding directories were created.

For the last part some module was downloaded from terraform registry (actually from some person's git), the module was made for bucket creation in GCP.


~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

### terraform-1 HW description


During this homework the basics of terraform was learned and a few files were created:

main.tf - the main terraform file where the instructions (configuration) for terraform are located

outputs.tf - describes which parameters to show the user upon execution

variables.tf - contains the declaration of variables used in main.tf, so they can be specified elsewhere

terraform.tfvars - contains the actual variables, which may include some sensetive data


There is also a few files in "files" directory which are needed for application deployment, they are described in main.tf as a provisioners.

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

### packer-base HW description

During this homework a few new files were created.

Ubuntu.json is a packer template for GCP image creation. This files uses a few .sh scripts in "scripts" directory for automatic dependancies installation.

Also the template uses the side file variables.json (.json.example in this case) to allow tweaking the image options without modifying the template itself.

~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

### cloud_testapp HW description

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

### cloud_bastion HW description

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
