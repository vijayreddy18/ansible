#ANISBLE


Ansible Commands
1. Ping to Reach Respective Hosts:


ansible all -m ping
This command is used to test connectivity to all hosts specified in the inventory file.

2. Execute Command 'uptime' on Respective Hosts:


ansible all -m command -a 'uptime'
Executes the uptime command on all hosts to display system uptime.

3. Execute Command 'ls -la' on Respective Hosts:


ansible all -m command -a 'ls -la'
Executes the ls -la command on all hosts to list files and directories with detailed information.

4. Create a Test File on Respective Hosts:

ansible all -m command -a 'touch testfile'
Creates a test file named testfile on all hosts.

5. Check if Test File Exists on Servers:


ansible all -m stat -a "path=/home/ansadmin/testfile"
This command checks if the file testfile exists on the servers.

Yum Commands
1. Install Git Package on Hosts:


ansible all -m yum -a 'name=git'
Installs the Git package on all hosts. If execution from root user is required, use the following command: 

ansible all -m yum -a 'name=git' -b
The -b option indicates to become root.

2. Check Installed Git Packages:

yum list installed | grep git
Lists all installed Git packages on the servers.

Note:
Green output indicates a fresh installation, while yellow indicates that the package already exists.

User Management
1. Create User 'modi' with Root Privileges:
ansible all -m user -a 'name=modi' -b
This command creates a user named modi with root permissions.


Gathering System Information
1. Gather System Information:

ansible all -m setup
This command gathers all system information related to Ansible.
