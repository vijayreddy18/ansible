[Document_ ANISBLE.docx](https://github.com/vijayreddy18/ansible/files/15046945/Document_.ANISBLE.docx)

#ANISBLE

Ansible Commands
Ping to Reach Respective Hosts:
1.	ansible all -m ping # This command is used to test connectivity to all hosts specified in the inventory file.

Execute Command 'uptime' on Respective Hosts:
2.	ansible all -m command -a #'uptime' Executes the uptime command on all hosts to display system uptime.

3.	Execute Command 'ls -la' on Respective Hosts:
ansible all -m command -a 'ls -la' # Executes the ls -la command on all hosts to list files and directories with detailed information.

4.	Create a Test File on Respective Hosts:
ansible all -m command -a 'touch testfile' #Creates a test file named test file on all hosts.

5.	Check if Test File Exists on Servers:
ansible all -m stat -a "path=/home/ansadmin/testfile" #This command checks if the file test file exists on the servers.




Yum Commands

1.	Install Git Package on Hosts:
ansible all -m yum -a 'name=git' Installs the Git package on all hosts. If execution from root user is required, use the following command:

ansible all -m yum -a 'name=git' -b The -b option indicates to become root.

2.	Check Installed Git Packages:
yum list installed | grep git Lists all installed Git packages on the servers.

Note: Green output indicates a fresh installation, while yellow indicates that the package already exists.

3.	User Management

Create User 'modi' with Root Privileges: ansible all -m user -a 'name=modi' -b This command creates a user named Modi with root permissions.

4.	Gather System Information:
ansible all -m setup This command gathers all system information related to Ansible.



Inventory Management in Ansible Introduction 
In Ansible, managing multiple hosts is facilitated through an inventory, which is essentially a list or grouping of managed hosts.

Inventory File The inventory file is a collection of hosts, each identified by its hostname or IP address. It serves as a central location to define the hosts that Ansible will manage.

Default Location The default location for the inventory file is:
/etc/ansible/hosts
Custom Inventory File You can create your own inventory file in any location under the same user. For example: touch inventory.ini 
Specifying Inventory Path When executing Ansible commands, you need to specify the path to the inventory file if it's located in a different directory. 
For instance: ansible all -i inventory.ini -m ping # Same path ansible all -i /etc/home/abc/inventory.ini -m ping
 # Different path Configuration To avoid specifying the full path to the inventory file every time, you can modify configurations in the Ansible configuration file (ansible.cfg). By changing the default host path to your custom path, you simplify command execution.
Ansible Configuration /etc/ansible/ansible.cfg Customization Options In the Ansible configuration file located at /etc/ansible/ansible.cfg, various configurations can be modified to tailor Ansible's behaviours according to your requirements.

Forks Configuration The forks option controls the number of parallel connections Ansible can make to managed hosts. By default, Ansible executes commands sequentially, but by setting forks to a higher value, you can enable parallel execution.
Example:
make file Copy code forks = 5 This configuration allows Ansible to execute commands simultaneously on up to 5 hosts.
Default Module in Ansible Command Module When executing commands with Ansible, if the module argument is omitted, the command module is used by default. This behaviour is dictated by the configuration set in ansible.cfg.

Default Module Configuration By default, the module name specified in the ansible.cfg file is used. If desired, you can modify this default module setting.

Hierarchy of Ansible Configuration Files Ansible follows a specific hierarchy to determine which configuration file to use. The order of precedence is as follows:

ANSIBLE_CFG environment variable.
ansible.cfg file in the current directory 
ansible.cfg file in the user's home directory /etc/ansible/ansible.cfg system-wide configuration file 

Ansible Modules and Playbooks
Ansible Modules Definition: Ansible modules are reusable and standalone scripts that can be executed locally or on remote servers. They facilitate tasks such as user creation, software installation, and configuration updates.

Usage: Modules enable administrators to perform various tasks efficiently across multiple systems using Ansible commands.
Example:

ansible all -m user -a 'name=john' -b This command creates a user named "john" on all specified hosts with root permissions.

Ansible Playbooks Definition: An Ansible playbook is a text file written in YAML format, typically with the file extension. yml. It serves as a configuration file for defining tasks and orchestrating automation workflows.

Structure:

Playbooks start with the document marker ---. 
Each item in a YAML file begins with a single dash –
Hosts and tasks are mandatory elements within a playbook YAML file. 
Comments are indicated by the # symbol. 
Usage: Playbooks provide a structured approach to automation, allowing administrators to define tasks, target hosts, and manage configurations in a declarative manner.

Example Playbook:
---
- hosts: all
  tasks:
    - name: Create user
      user:
        name: john
        become: yes
This playbook defines a task to create a user named "john" on all hosts, with elevated privileges (root permissions).



By default, Ansible does not gather facts automatically when executing a playbook. However, it will execute fact gathering even if it's not explicitly mentioned in the playbook. To skip fact gathering, you can specify gather_facts: no in your playbook.

Commands to Check Playbook Before Execution Before executing the playbook, it's advisable to perform syntax and indentation checks to avoid errors. Use the following command:
ansible-playbook user.yml --check or -C This command will check the indentation of the YAML file and identify any syntax errors, allowing you to fix them before execution.

Ansible Playbook: Installing Packages
name: Installing packages
hosts: all 
become: true 
gather_facts: no
tasks:
 name: Installing package 
 yum: name: git 
 state: present

Explanation:
 *Name: Installing packages #This playbook is named "Installing packages". 
*Hosts: All # Tasks will be executed on all hosts specified in the inventory file.
* Become: true # the tasks will run with elevated privileges (usually as root).
 *Gather Facts: no # Fact gathering is disabled to speed up the execution process. 
*Tasks: Name: Installing package # This task is named "Installing package". 
*Yum Module: # The yum module is used to manage packages on the system. 
*Name: git # Specifies the name of the package to be installed (in this case, Git). 
*State: # present Indicates that the package should be installed if it's not already present.
Additional Information: Package States: absent or removed: Removes the package. installed or present: Installs the package. latest: Updates the package to the latest version.

