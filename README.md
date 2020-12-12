Ansible Advanced - Homework 
Table of Contents
1.	Business Use Case
2.	Configure Ansible Tower cluster with isolated node 
3.	Provision the QA environment on the OpenStack platform & Deploy 3-Tier App on QA environment and perform smoke test
4.	Provision the Production environment on the AWS platform & Deploy 3-Tier App on AWS environment and perform smoke test
5.	Homework lab execution

1. Business Use Case
In this scenario, you are a consultant assigned to a telecommunications company called MitziCom. MitziCom provides hosting and cloud services to a variety of clients from medium-sized companies to enterprise giants.
MitziCom has asked you to lead a 30- to 40-hour proof-of-concept (POC) using Red Hat Ansible Tower. The purpose of the POC is to determine the feasibility of using Ansible Tower as a CI/CD tool for automating continuous deployment of an internal three-tier application on QA and production environments. Note that this requires maintaining several instances of the application.
2. Configure Ansible Tower cluster with isolated node 
	First, you provision the Ansible Advanced - Homework and Ansible Advanced NG - OpenStack lab environments. You provision the Ansible Advanced - Three Tier App environment in a later section.
	Ansible Tower is deployed in the Ansible Advanced - Homework environment.
	Fork the https://github.com/netprakashmeet/nextgen_ansible_advanced_homework.git repository 
	After forking the repository, clone the forked repository from your account onto the control host of the Ansible Advanced - Homework lab environment under the /root directory.
	Ansible Playbooks are provided to provision the network, security groups, flavor, and key pairs on OpenStack.
	From the cloned repo copy labrc file in your home dir and edit to setup env variables which we will be using in the whole lab.
	Run the site-setup-prereqs.yaml playbook to provision the network, flavor, security groups, and SSH keys on OpenStack:
	From your web browser, connect to tower1.${TOWER_GUID}.example.opentlc.com to verify that the isolated node is operational, using admin for the username and password As provided in email.
	OpenStack components are provisioned for you and are created by the site-setup-prereqs.yaml playbook
	Update Ansible Tower WebUI admin password.Reset r3dh4t1! as admin password after sign-in using password provided in email.
	Run the site-config-tower.yml playbook to create the job templates and workflow template:
Provision the QA environment on the OpenStack platform & Deploy 3-Tier App on QA environment and perform smoke test 

	Provision QA Env Job Template will run site-osp-instances.yml playbook, it will help to provision RHOSP instances to support the deployment of a three-tier application on QA environment using the network details and flavour specified in the previous section.
	3tier app deployment on QA Env Job Template will run site-3tier-app.yml playbook, it will help to deploy 3-Tier application on the QA environment
	Smoke test QA Env Job Template will run site-smoke-osp.yml playbook, it will help to perform Smoke test on 3-Tier application on the QA environment
	playbook named site-osp-delete.yml to destroy the QA environment on RHOSP if the smoke test fails.
Provision the Production environment on the AWS platform & Deploy 3-Tier App on AWS environment and perform smoke test

	Provision Prod Env Job Template will run aws_provision.yml playbook, it will help to provision AWS instances to support the deployment of a three-tier application on Production environment 
	3 tier app on Prod Job Template will run site-3tier-app.yml playbook, it will help to deploy 3-Tier application on the Production environment
	Smoke test Prod env Job Template will run  site-smoketest-aws.yml playbook, it will help to perform Smoke test on 3-Tier application on the Production environment
Homework lab execution
Execute the workflow template from the Ansible Tower UI, which must be able to run successfully according to these requirements:
•	Provision instances in the OpenStack QA environment
•	Deploy the application in the QA environment
•	Run the smoke test to verify the application
o	Clean up if the test fails
•	Provision instances on AWS using order_svc.sh script for the production environment
•	Deploy the application in the production environment
•	Run the smoke test to verify the application


