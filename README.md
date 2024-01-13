# IN_PROGRESS DigitalOcean ActiveDirectory with Centos-7 and Ubuntu

## Specifications

This repository also contains VagrantFile, with little adjustments you can try this on local environment.

macOS: Sonoma 14.2.1

Centos: centos-7-x64

Ubuntu: ubuntu-23-10-x64

## PRE-INSTRUCTIONS
1. Add your machine SSH to DigitalOcean account
2. Update hosts file position
   
   a) ansible_ssh_private_key_file (path to your public ssh file)
4. Create API token and add to your DigitalOcean project
5. Update vars files to your personal preferences
   
   a) Update u_token in Connection vars (api_token)
   
   b) Update u_ssh in Connection vars (ssh fingerprint)
   
   c) Update hosts_dest with your actual path to the hosts file (you can use pwd)
   
   d) Update ad_domain, realm_name and users with your personal preference

## RUN INSTRUCTIONS
1. Run droplet yml: ansible-playbook -i hosts.ini droplet.yml
   
   Playbook drops Active Directory server and initial user. It automatically creates inventory files (and adds ips) with recently created servers. Additionaly creates ip_vars.yml file that saves ours ip servers for the future playbooks.
   
3. Run Active Directory server playbook: ansible-playbook -i hosts.ini ad.yml
   
   This Playbook installs required packages to become an AD and automatically make changes to DNS and network config files. It may requite additional server restart (sudo reboot). Besides that joins AD with admin user and creates network directory
   
5. Run app.yml: ansible-playbook -i hosts.ini app.yml
   
   This Playbook installs required packages to join AD, joins AD server and adds recently created network directory

## Droplet Delete

If you would like to delete droplet, simply switch both states of "Create Digitalocean droplet" from PRESENT to ABSENT and run playbook.

## Links 

https://askubuntu.com/questions/1109923/18-04-joining-ad-problems

https://zerosandones.us/2023/01/06/join-linux-to-active-directory/

https://computingforgeeks.com/join-ubuntu-debian-to-active-directory-ad-domain/
