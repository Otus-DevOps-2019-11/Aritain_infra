# Aritain_infra
~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~ ~

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
