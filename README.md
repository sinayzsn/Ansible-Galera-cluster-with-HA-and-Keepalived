# Galera cluster with HA and keepaloved
  Galera cluster is about 3 nodes of mysql darabase to be simple,
 HA is about managing and not having one single point of faliure,
 and Keepalived is about puting a floating IP between the HA nodes.
 
 ### Note:
  Keep in mind that the galera cluster works with `ansible 2.9.6` (This what I have tested
  with) nad does not work with higher versions of ansible.
 
 ## How to use it
  First you must install the requirements with the use of the command below,
  after that you need to change th variables in the vars folder of each playbook.
  ```
  ansible-galaxy install -r requirements.yml
  ```
 #### Note: 
 this playbook are created with two seperate playbook, HA and Keepalived
 was created by me with the help of other playbooks and the other was originaly 
 created  by mrlesmithjr that I have made changes to fit my usage.
 in the Galera playbook you need to change multiple files to mach your needs 
 and I have to remind you that every place the changes are needed I will add 
 a (CHANGE_HERE) comment so that you could find them easily, and here 
 I will go through each one:
 #### Galera clusters
 1. in defaults/main.yml:
      * line 30: Change mysql password from root.
      * line 96: change the interface name.
      * line 107: define the name of the cluster.
      * line 155-156: define the user and pass of mariadb_sst_user if enabled.
 2. in vars/main.yml:
      line 11-12: change the ha proxy IP addresses, 
        and if not needed comment them.

#### HA and Keepalived
 1. in vars/main.yml
      change everything note that you need to change in order to be usefull.
      
#### Hosts
Make sure before moving into the next step you have set the hosts right, change the
host file and make sure that every IP addressses is the right place to install.


## Deploy it
All you need to do in order to deploy both of them after you have changed the variables
is to run this command.
```
ansible-playbook -i hosts Deploy.yml
```
