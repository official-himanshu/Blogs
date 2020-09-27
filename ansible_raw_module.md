# How to install python in target host using Ansible
![ansible_raw_module](https://github.com/official-himanshu/Blogs/blob/master/ansible.png)

Ansible is an open-source automation engine that automates software provisioning, configuration management, and application deployment. 
Ansible is quickly becoming the popular configuration management tool today. It lets you to control and config the target nodes from single host machine.
As we know the only requirement in target machine is the modern version of python installed. But what if the python version is not installed on the target machines.
You can do it manaully on some machine but what if you have tons of target server which does not have python installed by default.

### The raw module
The ansible_base run on python because we want ansible to manage a wide variety of machines. Any module that Ansible uses against target host uses python internal to make required changes.
But what you do if target does not have python installed? So for this ansible has raw module. This module is very useful and is used in various cases, one of is installing python on target host.
Let's begin that how can we install python on target host using ansible.

### Setting up Ansible to connect with EC2-instance
So before we moving forword we need to configure ansible to connect to ec2-instance.
Firstly we need to make an ansible.cfg file in current directory. As by default ansible use this file to configure any changes because ansible has some precedence rules in which it search ansible.cfg file in current directory by overriding the default /etc/ansible/ansible.cfg.
So, this file looks like as:

    [defaults]
    host_key_checking = false
    private_key_file = ~/.ssh/ansible27sep2020.pem
    remote_user = ubuntu

1. host_key_checking: As we know, if we use ssh to connect to a host for the first time it shows a warning that system is going to add a key to the known_hosts list and we need to type yes to connect to the remote machine.
2. private_key_file: This step is going to give the location of .pem file of target machine in your system.
3. remote_user: It is used to tell ansible the remote user name. If we don't specify that then ansible use our system username to establish connection.

### Inventory
Next we need to create our inventory file which consists of out remote machine ip address. I have created a python group which consist ec2 instance ip address.

    [python]
    13.233.95.58
    
### Creating playbook to install python
Next we need to create a playbook which contains raw module to install python on target machine. I have created a install_python.yml file as follows:

    ---
    - name: Install python in target node with ansible
      hosts: python
      become: true
      gather_facts: no
      pre_tasks:
              - name: install python
                raw: 'sudo apt install -y python3'


In the above playbook the most important part is gather_facts should be no if python is not installed. As we know gather_facts uses python to collect the target machine information. become is uses to get the previlages of root user. 
When we need to install python, this must be specified in pre_tasks section of the playbook. By specifying any pre work in the pre_task, it should first execute pre_tasks after connecting to the host server.

After that raw module contains staright linux command, which consist 'apt' that install the python3 package in target host.

### Running playbook
Running a playbook is as easy as issuing the following command:

    ansible-playbook -i inventory install_python.yml
    
    
After running this command you will see the below output :

    knoldus@knoldus-Vostro-3559:~/Ansible/raw_module$ ansible-playbook -i inventory install_python.yml 

    PLAY [Install python in target node with ansible] ********************************************************************************************

    TASK [install python] ************************************************************************************************************************
    changed: [13.233.95.58]

    PLAY RECAP ***********************************************************************************************************************************
    13.233.95.58               : ok=1    changed=1    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0  
    
    
You can double check that python installed in target host by simple SSHing into the server and type python --version.

### Conclusion
In this blog, we learn that how can we install python in target host with ansible using raw module. There are some workaround with this approach that you should not include this pre-tasks to install python in your main playbook as it is going to install python again and again which is not a good practice.
So it should be run only once. Other thing is that gather_facts is no so you should not use this in main playbook as there as some tasks that use gather_facts to gather some important information of host to use in the playbook like package information.
You can create a separate playbook that will just make sure that all target machines have Python installed. Subsequent Ansible tasks can be added to another playbook where gather_facts can be turned on.



