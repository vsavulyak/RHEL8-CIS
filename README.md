
# Ansible homework  
- [x] *Create github account to store the homework*  
- [x] *Download latest RHEL-8 CIS benchmark from https://www.cisecurity.org/benchmark/red_hat_linux/*  
- [x] *Implement with Ansible playbooks logic for following CIS chapters :*  
     - [x] *1.1.1. Disable unused filesystems*  
     - [x] *2.3. Service Clients*  
     - [x] *4.2.1 Configure rsyslog*  

# Playbook Usage  
To enable/disable related chapters/subchapters edit file (by default enabled all items)
```
vi defaults/main.yml
```
```yaml
task1_cis_1_1_1   : true     #    1.1.1 Disable unused filesystems 

task1_cis_1_1_1_1 : true     #  1.1.1.1 Ensure mounting of cramfs filesystems is disabled (Automated)
task1_cis_1_1_1_2 : true     #  1.1.1.2 Ensure mounting of vFAT filesystems is limited (Manual)
task1_cis_1_1_1_3 : true     #  1.1.1.3 Ensure mounting of squashfs filesystems is disabled (Automated)
task1_cis_1_1_1_4 : true     #  1.1.1.4 Ensure mounting of udf filesystems is disabled (Automated)
  
task2_cis_2_3     : true     #      2.3 Service Clients
						   
task2_cis_2_3_1   : true     #    2.3.1 Ensure NIS Client is not installed (Automated)
task2_cis_2_3_2   : true     #    2.3.2 Ensure telnet client is not installed (Automated) 
task2_cis_2_3_3   : true     #    2.3.3 Ensure LDAP client is not installed (Automated)
						   
task3_cis_4_2_1   : true     #    4.2.1 Configure rsyslog
						   
task3_cis_4_2_1_1 : true     #    4.2.1 Ensure rsyslog is installed (Automated)
task3_cis_4_2_1_2 : true     #  4.2.1.1 Ensure the rsyslog service is enabled and active (Automated)
task3_cis_4_2_1_3 : true     #  4.2.1.2 Ensure the operating system monitors all remote access methods (Automated)
task3_cis_4_2_1_4 : true     #  4.2.1.3 Ensure rsyslog Service is enabled (Automated)
task3_cis_4_2_1_5 : true     #  4.2.1.4 Ensure rsyslog default file permissions configured (Automated)
task3_cis_4_2_1_6 : true     #  4.2.1.5 Ensure logging is configured (Manual)
```
To start patch **Localhost** run:
```
ansible-playbook localhost.yml
```
To start patch **Remote** hosts add hosts 
to inventory file hosts.txt, for example:
```yml
[host-group1]
alias-PC1 ansible_host=172.16.1.10 ansible_user=myuser ansible_ssh_pass=myuserpwd ansible_sudo_pass=rootpwd
```
or specify another inventory filename instead of hosts.txt in ansible.cfg:  
```yaml
[defaults]
...
inventory         = ./hosts.txt
...
```
and run (by default will be applied for **all host-groups** listed in this file ):
```
ansible-playbook remote.yml
```
or edit remote.yml and specify group-name instead of **all**  
for example run it only for host-group1
```yaml
---
- hosts: host-group1
  become: true

  roles:
      - role: "{{ playbook_dir }}"
```
