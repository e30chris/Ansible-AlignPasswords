Ansible-AlignPassword
========================

## The Problem:
A group of servers get their passwords updated every 3 months with a new shared password.  The servers passwords are then inconsistently updated leaving a group of servers with one of several possible user passwords.  

## The Goal:
Use Ansible to attempt to login to each server using each of the possible passwords to find the correct one and log it.  The final step of the playbook will have Ansible logging into each server using the found to be correct password and updating each server to a new shared password. 

_**note - using the same root password on all your servers is a terrible idea and completely against the SysAdmin Bible.  Use random passwords and keys!**_


## HowTo:

  * Download the playbook from
    * GitHub - [repo](https://github.com/e30chris/Ansible-AlignPassword)
    * Galaxy - [repo](https://galaxy.ansible.com/list#/roles/1134)
  * Create a branch to edit the variables for your environment
  
  ```
  sandor@pineapplez:$ cd ~/Codestuff/ansibles/Ansible-AlignPassword
  sandor@pineapplez:$ git checkout -b qatenv    
  ```
  
  * ansible-vault the file that will contain the passwords.
  
  ```
  sandor@pineapplez:$ ansible-vault encrypt group_vars/all
  ```
  
  * Edit the vars for the environment
  
  ```
  sandor@pineapplez:$ ansible-vault edit group_vars/all
  ```
  
  * Add the inventory to hosts
  * Verify Ansible connect with ping pong
  
  ```
  sandor@pineapplez:$ ansible -i hosts all -m ping
  ```
  
  * Run the playbook
  
  ```
  sandor@pineapplez:$ ansible-playbook -i hosts site.yml -vv
  ```

## Common Task Actions

  * Attempt to login to each server using all possible passwords
  * Register which passwords work on each server
  * Set a new shared password for every server  
  

## Variables

Go here:

```
group_vars/all
```

With this format:

```
variable: value
```