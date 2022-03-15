### :star: RHCE  
  ---
![image](image/redhat.png)<br>
&nbsp;&nbsp;[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT "MIT License")
&nbsp;&nbsp;[![Active](http://img.shields.io/badge/Status-Active-green.svg)](https://github.com/soficx/)

---
### Description:

These are a few practice exams to get ready for the Red Hat Certified Engineer exam<br> 
The first practice exam was created by [Lisenet](https://www.lisenet.com/2019/ansible-sample-exam-for-ex294/) . The exam cover as many of the exam [objectives](https://www.redhat.com/en/services/training/ex294-red-hat-certified-engineer-rhce-exam-red-hat-enterprise-linux-8?section=Objectives) as possible

---
#
## Contents 

  - [RHCE8 Practice Exam 1](#rhce8-practice-exam-1)
  - [RHCE8 Practice Exam 2](#rhce8-practice-exam-2)

---
###### ***Requirements*** :
 - You will need five RHEL 8 virtual machines to be able to successfully complete all questions.
 - One VM will be configured as an Ansible control node. 
 - Other four VMs will be used to apply playbooks to solve the sample exam questions. 

#### RHCE8 Practice Exam 1 

- ***Task 1 :*** <br> 
	Install ansible package on the control node (including any dependencies) and configure the
	following:<br>
	- 1 - Create a regular user **automation** with the password of devops. Use this user for all sample
	exam tasks.
	- 2 - All playbooks and other Ansible configuration that you create for this sample exam should
	be stored in /home/automation/plays.<br>
	- 3 - Create a configuration file /home/automation/plays/ansible.cfg to meet the following requirements:
		- The roles path should include /home/automation/plays/roles, as well as any other path that may be required for the course of the sample exam.
		- The inventory file path is /home/automation/plays/inventory.
		- Privilege escallation is disabled by default.
		- Ansible should be able to manage 10 hosts at a single time.
		- Ansible should connect to all managed nodes using the automation user.
		- Create an inventory file /home/automation/plays/inventory with the following:
			- ansible2.hl.local is a member of the proxy host group.
			- ansible3.hl.local is a member of the webservers host group.
			- ansible4.hl.local is a member of the webservers host group.
			- ansible5.hl.local is a member of the database host group<br>

[Solution of Task1](#solution-of-task1)

- ***Task 2 :*** <br> 
	- Generate an SSH key pair on the control node for the automation user. You can perform this step manually. 
	- Write a script ***/home/automation/plays/adhoc.sh*** that uses Ansible ad-hoc commands to achieve the following:
		- User **automation** is created on all inventory hosts.
		- The SSH public key that you just generated is copied to all managed hosts for the automation user.
		- The automation user has full sudo access on all managed nodes without having to provide a password.

	After running the adhoc.sh bash script, you should be able to SSH into all managed hosts using the automation user without a password, as well as a run all
	privileged commands.

[Solution of Task2](#solution-of-task2)

- ***Task 3 :*** <br> 

- Create a playbook **/home/automation/plays/motd.yml** that runs on all inventory hosts and does the following:<br>
 The playbook should replace any existing content of /etc/motd with text. Text depends on the host group.
  - On hosts in the proxy host group the line should be “Welcome to HAProxy server”.
  -	On hosts in the webserver host group the line should be “Welcome to Apache server”.
  -	On hosts in the database host group the line should be “Welcome to MySQL server”

[Solution of Task3](#solution-of-task3)

- ***Task 4 :*** <br> 

	Create a playbook **/home/automation/plays/sshd.yml** that runs on all inventory hosts and configures SSHD daemon as follows:
	1. banner is set to /etc/motd
	2. X11Forwarding is disabled
	3. MaxAuthTries is set to 3

[Solution of Task4](#solution-of-task4)

- ***Task 5 :*** <br> 
	Create Ansible vault file **/home/automation/plays/secret.yml**. Encryption/decryption password is devops.<br>
	Add the following variables to the vault:
	1. user_password with value of devops
	2. database_password with value of devops


[Solution of Task5](#solution-of-task5)


- ***Task 6 :*** <br> 
You have been provided with the list of users below. Use **/home/automation/plays/vars/user_list.yml** file to save this content.
```yml
---
users:
  - username: alice
    uid: 1201
  - username: vincent
    uid: 1202
  - username: sandy
    uid: 2201
  - username: patrick
    uid: 2202
```
-	Create a playbook **/home/automation/plays/users.yml** that uses the vault file **/home/automation/plays/secret.yml** to achieve the following:
	1. Users whose user ID starts with 1 should be created on servers in the webservers host group. 
	2. Users whose user ID starts with 2 should be created on servers in the database host group.
	3. All users should be members of a supplementary group wheel. All users password should be used from the user_password variable
	4. Shell should be set to /bin/bash for all users.
	5. Account passwords should use the SHA512 hash format.<br>
After running the playbook, users should be able to SSH into their respective servers without passwords.

[Solution of Task6](#solution-of-task6)


-  ***Task 7 :***<br> 
  - Create a playbook **/home/automation/plays/regular_tasks.yml** that runs on servers in the proxy host group and does the following:
	  1. A root crontab record is created that runs every hour.
	  2. The cron job appends the file /var/log/time.log with the output from the date command.

[Solution of Task7](#solution-of-task7)

-  ***Task 8 :***<br> 
	Create a playbook **/home/automation/plays/repository.yml** that runs on servers in the database host group and does the following:
	 1. A YUM repository file is created.
	 2. The name of the repository is mysql56-community.
	 3. The description of the repository is “MySQL 5.6 YUM Repo”.
	 4. Repository baseurl is http://repo.mysql.com/yum/mysql-5.6-community/el/7/x86_64/.
	 5. Repository GPG key is at http://repo.mysql.com/RPM-GPG-KEY-mysql.
	 6. Repository GPG check is enabled.
	 7. Repository is enabled.

   [Solution of Task8](#solution-of-task8)

-  ***Task 9 :***<br> 
 Create a role called sample-mysql and store it in **/home/automation/plays/roles**. The role should satisfy the following requirements:
  1. A primary partition number 1 of size 800MB on device /dev/sdb is created.
  2. An LVM volume group called vg_database is created that uses the primary partition created above.
  3. An LVM logical volume called lv_mysql is created of size 512MB in the volume group
  vg_database.
  4. An XFS filesystem on the logical volume lv_mysql is created.
  5. Logical volume lv_mysql is permanently mounted on /mnt/mysql_backups.
  6. mysql-community-server package is installed.
  7. Firewall is configured to allow all incoming traffic on MySQL port TCP 3306.
  8. MySQL root user password should be set from the variable database_password (see task
#5).
  9. MySQL server should be started and enabled on boot.
  10.MySQL server configuration file is generated from the my.cnf.j2 Jinja2 template with the following content:
```txt
[mysqld]
bind_address = {{ ansible_default_ipv4.address }}
skip_name_resolve
datadir=/var/lib/mysql
socket=/var/lib/mysql/mysql.sock
symbolic-links=0
sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
[mysqld_safe]
log-error=/var/log/mysqld.log
pid-file=/var/run/mysqld/mysqld.pid
``` 
Create a playbook /home/automation/plays/mysql.yml that uses the role and runs on hosts in the
database host group.
[Solution of Task9](#solution-of-task9)

-  ***Task 10 :***<br> 
  Use Ansible Galaxy to download and install geerlingguy.haproxy role in **/home/automation/plays/roles**.
  Create a playbook **/home/automation/plays/haproxy.yml** that runs on servers in the proxy host group and does the following:
   1. Use geerlingguy.haproxy role to load balance request between hosts in the webservers host group.
   2. Use **roundrobin** load balancing method.
   3. HAProxy backend servers should be configured for HTTP only (port 80).
   4. Firewall is configured to allow all incoming traffic on port TCP 80.
  If your playbook works, then doing “curl http://ansible2.hl.local/” should return output from the web server (see task #9 ).
  Running the command again should return output from the other web server.

[Solution of Task10](#solution-of-task10)


-  ***Task 11 :***<br> 
  Create a playbook **/home/automation/plays/selinux.yml** that runs on hosts in the webservers host group and does the following:
	1. Uses the selinux RHEL system role.
	2. Enables httpd_can_network_connect SELinux boolean.
	3. The change must survive system reboot

[Solution of Task11](#solution-of-task11)

-  ***Task 12 :***<br> 
   Create a playbook **/home/automation/plays/sysctl.yml** that runs on all inventory hosts and does the following:
   1. If a server has more than 2048MB of RAM, then parameter vm.swappiness is set to 10.
   2. If a server has less than 2048MB of RAM, then the following error message is displayed: Server memory less than 2048MB

  [Solution of Task12](#solution-of-task12)


-  ***Task 13 :***<br> 
   Create a playbook **/home/automation/plays/archive.yml** that runs on hosts in the database host group and does the following:
   1. A file **/mnt/mysql_backups/database_list.txt** is created that contains the following line: dev,test,qa,prod.
   2. A gzip archive of the file /mnt/mysql_backups/database_list.txt is created and stored in /mnt/mysql_backups/archive.gz


[Solution of Task13](#solution-of-task13)


-  ***Task 14 :***<br> 

   Create a playbook **/home/automation/plays/packages.yml** that runs on all inventory hosts and does the following:
   1. Installs tcpdump and mailx packages on hosts in the proxy host groups.
   2. Installs lsof and mailx and packages on hosts in the database host groups.

[Solution of Task14](#solution-of-task14)

-  ***Task 15 :***<br> 
  Create a playbook **/home/automation/plays/target.yml** that runs on hosts in the webserver host group and does the following:
   1. Sets the default boot target to multi-user.

  [Solution of Task15](#solution-of-task15)


-  ***Task 16 :***<br> 
   Create a playbook **/home/automation/plays/server_list.yml** that does the following:
   1. Playbook uses a Jinja2 template server_list.j2 to create a file /etc/server_list.txt on hosts in
   the database host group.
   2. The file /etc/server_list.txt is owned by the automation user.
   3. File permissions are set to 0600.
   4. SELinux file label should be set to net_conf_t.
   5. The content of the file is a list of FQDNs of all inventory hosts.
   After running the playbook, the content of the file /etc/server_list.txt should be the following:
   ansible2.hl.local
   ansible3.hl.local
   ansible4.hl.local
   ansible5.hl.local
Note: if the FQDN of any inventory host changes, re-running the playbook should update the file
with the new values.

[Solution of Task16](#solution-of-task16)


### Solution of Task1
```yaml
  Ansible-installation : 
  # yum list installed platform-python 
  # yum install ansible 
  # ansible --version 
 1- # useradd automation 
    # echo "devops" | passwd --stdin automation 
 2- # su - automation 
    # mkdir plays ; cd plays 
 3- # vim ansible.cfg 
    ## Ansible.config file 
    [defaults]
    role_path = ./roles
    inventory = ./inventory
    forks = 10
    remote_user = automation 
    [privilege_escalation]
    become = False

    # vim inventory 
    [proxy]
    ansible2.hl.local 
    [webservers]
    ansible3.hl.local 
    ansible4.hl.local 
    [database]
    ansible5.hl.local 
    
    # ansible all --list-hosts
```
### Solution of Task2
```bash
# echo "automation ALL=(ALL)  NOPASSWD:ALL" > /etc/sudoers.d/automation
# ssh-keygen 
# vim adhoc.sh 
	#!/bin/bash
    # you can specify the inventory file with -i option 
    ansible all -m user -a "user='automation'\
    comment='User Create by Ansible'" -u root --ask-pass 

    ansible all -m authorized_key -a "user=automation state=present \
    key={{ lookup('file', '/home/automation/.ssh/id_rsa.pub') }}" -u root --ask-pass

    ansible all -m copy -a "src='/etc/sudoers.d/automation' dest='/etc/sudoers.d/'" -u root --ask-pass

# chmod 755 adhoc.sh 
# ./adhoc.sh
```
### Solution of Task3

```bash
# mkdir group_vars ; cd group_vars
# echo "message: Welcome to HAProxy server" >> proxy
# echo "message: Welcome to Apache server" >> webserver
# echo "message: Welcome to MySQLserver" >> database

```
```yaml
--- 
- name: Customize the message of the day
  hosts: all
  tasks:
    - name: Create the message of the day according to the managed host
      copy:
        content: "{{ message }}"
        dest: /etc/motd 
        owner: root
        group: root 
        mode: '0644'
...
```


###  Solution of Task4
```bash
# vim defaults/main.yml 
# sshd config variables
ssh_config: 
  - start_line: "^banner"
    line: "banner /etc/motd"
  - start_line: "X11Forwarding"
    line: "X11Forwarding no"
  - start_line: "^#MaxAuthTries"
    line: "MaxAuthTries yes"
```

```yaml
--- 
- name: Configure the sshd service 
  hosts: all 
  vars_files:
    - defaults/main.yml
  tasks: 
    - name: Adding sshd config 
      lineinfile:
        path: /etc/ssh/sshd_config 
        regexp: "{{ item.start_line }}"
        line: "{{ item.line }}"
      loop: "{{ ssh_config }}"
      notify: restart sshd 
      # don't forget to restart the service
  handler:
    - name: restart sshd 
      service: 
        name: sshd 
        state: restarted
...


# ansible all -m command -a 'grep "MaxAuthTries" /etc/ssh/sshd_config' 
```
### Solution of Task5
```bash
# ansible-vault create secret.yml
New Vault password: devops
Confirm New Vault password: devops

---
user_password: devops
database_password: devops

using the decr with vault-file : 
# vim vault-key
devops
# chmod 400 vault-key 
# ansible-vault view secret.yml --vault-password-file vault-key 
	
---
user_password: devops
database_password: devops
```

### Solution of Task6
```yaml
---
- name: Create users
  hosts: all
  become: yes
  vars_files:
    - ./users_list.yml
    - ./secret.yml
  tasks:
    - name: Ensure group is exist
      group:
        name: wheel
        state: present
    - name: Create users that starts with 1 in their uid
      user:
        name: "{{ item.username }}"
        group: wheel
        password: "{{ user_password | password_hash('sha512') }}"
        shell: /bin/bash
        update_password: on_create
      with_items: "{{ users }}"
      when:
        - ansible_fqdn in groups['webservers']
        - "item.uid|string|first == '1'"

    - name: Create users that starts with 2 in their uid
      user:
        name: "{{ item.username }}"
        group: wheel
        password: "{{ user_password | password_hash('sha512') }}"
        shell: /bin/bash
        update_password: on_create
      with_items: "{{ users }}"
      when:
        - ansible_fqdn in groups['database']
        - "item.uid|string|first == '2'"
```
### Solution of Task7
```yaml
---
- name: Scheduled tasks
  hosts: proxy
  become: yes
  tasks:
    - name: Ensure file exists
      file:
        path: /var/log/time.log
        state: touch
        mode: 0644
    - name: Create cronjob for root user
      cron:
        name: "check time"
        hour: "*/1"
        user: root
        job: "date >> /var/log/time.log"
```
### Solution of Task8
```yaml
---
- name: Software repositories
  hosts: database
  become: yes
  tasks:
    - name: Create msyql repository
      yum_repository:
        name: mysql56-community
        description: "MySQL 5.6 YUM Repo"
        baseurl: "http://repo.mysql.com/yum/mysql-5.6-community/el/7/x86_64/"
        enabled: yes
        gpgcheck: yes
        gpgkey: "http://repo.mysql.com/RPM-GPG-KEY-mysql"

# ansible database -m command -a 'cat /etc/yum.repos.d/MariaDB-10.5.repo' -b
```
### Solution of Task9
```yaml
# cd roles 
# ansible-galaxy init sample-mysql
# cd sample-mysql
# vim vars/main.yml

---
partitions: 
  - number: 1
    start: 1MiB
    end: 800MiB
    device: /dev/sdb

volume_groups: 
  - name: vg_database
    device: /dev/sdb1  

logical_volumes: 
  - name: lv_mysql 
    size: 512MiB
    vgroup: vg_database
    mount_path: /mnt/mysql_backups 

mysql_service: mariadb
mysql_packages:
  - mariadb
  - mariadb-server
  - python3-PyMySQL
...


```

```yaml
# vim tasks/main.yml
---
- name: Create a primary partition on /dev/sdb 
  parted: 
    device: "{{ item.device }}"
    number: "{{ item.number }}"
    part_start: "{{ item.start }}"
    part_end: "{{ item.end }}"
    part_type: primary
    state: present
    unit: MiB
  loop: "{{ partitions }}"
  
- name: Ensure Volume group exist 
  lvg: 
    vg: "{{ item.name }}" 
    pvs: "{{ item.device }}" 
  loop: "{{ volume_groups }}" 

- name: Ensure Logical Volume exist    
  lvol: 
    lv: "{{ item.name }}" 
    vg: "{{ item.vgroup }}" 
    size: "{{ item.size }}" 
    state: present
  loop: "{{ logical_volumes }}" 
  when: item.name not in ansible_lvm["lvs"]

- name: Create XFS filesystem 
  filesystem: 
    dev: "/dev/{{ item.vgroup }}/{{ item.name }}"
    type: xfs
  loop: "{{ logical_volumes }}" 

- name: Ensure Correct Capacity for {{ lv_name }}
  lvol:
    vg: "{{ item.vgroup }}"
    lv: "{{ item.name }}"
    size: "{{ item.size }}" 
    resizefs: true
    force: yes
  loop: "{{ logical_volumes }}" ## remembre that the fs XFS does not support shrinking capacity

- name: Ensure the FS is mounted 
  mount: 
    src: /dev/{{ item.vgroup }}/{{ item.name }}"
    path: "{{ item.mount_path }}"
    fstype: xfs 
    state: mounted
  loop: "{{ logical_volumes }}" 

- name: Ensure mysql is installed
  yum:
    name: "{{ packages }}" 
    state: present

- name: Ensure MySQL is enabled and started
  service: 
    name: "{{ mysql_service }}"  
    state: started
    enabled: true

- name: Enable MySQL in firewalld 
  firewalld: 
    service: "{{ mysql_service }}"
    state: enabled 
    permanent: true
    immediate: true

- name: Change MySQL root user password
  mysql_user: 
    name: root 
    password: "{{ database_password  }}" 
    state: present

- name: Copy my.cnf.j2 to /etc/my.cnf
  template:
    src: my.cnf.j2
    dest: /etc/my.cnf
  notify: restart mysql 
```

```yaml
# vim handlers/main.yml
---
- name: restart mysql 
  service: 
    name: "{{ mysql_srv }}" 
    state: restarted
```

```yaml
# vim templates/my.cfg.j2
  {{ ansible_managed }}
  [mysqld]
  bind_address = {{ ansible_facts['default_ipv4']['address'] }}
  skip_name_resolve
  datadir = /var/lib/mysql
  socket = /var/lib/mysql/mysql.sock
  symbolic-links = 0
  sql_mode = NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
  [mysqld_safe]
  log-error = /var/log/mysqld.log
  pid-file = /var/run/mysqld/mysqld.pid
```

```yaml
# vim mysql.yml
--- 
- name: Install mysql role 
  hosts: databse
  vars_files:
    - secret.yml
  roles: 
    sample-mysql

```
### Solution of Task10
```bash
# ansible-galaxy install geerlingguy.haproxy -p roles/
```
```yml
---
- name: Configure HAPROXY
  hosts: proxy
  become: yes
  roles:
    - geerlingguy.haproxy
  vars:
    haproxy_frontend_port: 80
    haproxy_frontend_mode: 'http'
    haproxy_backend_balance_method: 'roundrobin'
    haproxy_backend_servers:
      - name: app1
        address: 10.0.0.23		# The @ ip of the webservers
      - name: app2
        address: 10.0.0.25
  tasks:
    - name: Ensure firewalld and its dependencies are installed
      yum:
        name: firewalld
        state: latest

    - name: Ensure firewalld is running
      service:
        name: firewalld
        state: started
        enabled: yes

   - name: Ensure firewalld is allowing to the traffic
     firewalld:
       port: 80/tcp
       permanent: yes
       immediate: yes
       state: enabled

# ansible proxy -m command -a 'systemctl is-enabled haproxy' -b
# curl http://ansible2.hl.local/
```
#### Solution of Task11
> If you get stuck and forget the syntax, try this command :

```bash
# find /usr/share/ -iname example-selinux*		
```
```yml
---
- name: Configure SELinux
  hosts: webservers
  become: true
  tasks:
    - name: Configure SELinux
      block:
        - include_role:
            name: rhel-system-roles.selinux
      rescue:
        # Fail if failed for a different reason than selinux_reboot_required.
        - name: handle errors
          fail:
            msg: "role failed"
          when: not selinux_reboot_required
        - name: restart managed host
          reboot:
            msg: "Ansible updates triggered"
          ignore_errors: true

        - name: wait for managed host to come back 
          wait_for_connections: 
            delay: 10
            timeout: 300

        - name: reapply the role
          include_role:
            name: rhel-system-roles.selinux
```
### Solution of Task12
```yaml
---
- name: Set sysctl Parameters
  hosts: all
  become: true
  vars: 
    min_ram_mb: 2048
  tasks:

    - name: Print error message
      debug:
        msg: "Server memory less than 2048MB"
    when: ansible_memtotal_mb < min_ram_mb

    - name: set vm.swappiness to 10
      sysctl:
        name: vm.swappiness
        value: '10'
        state: present
      when: ansible_memtotal_mb > min_ram_mb
```
### Solution of Task13
```yaml
--
- name: Use Archiving
  hosts: database
  become: yes
  tasks:

    - name: Create a directory if it does not exist 
      file:
        path: /mnt/mysql_backups/
        state: directory
        mode: 0775
        owner: root
        group: root

    - name: Copy the content
      copy:
       content: "dev,test,qa,prod"
       dest: /mnt/mysql_backups/database_list.txt

    - name: Create archive
      archive:
        path: /mnt/mysql_backups/database_list.txt
        dest: /mnt/mysql_backups/archive.gz
        format: gz
```
--### Solution of Task14
```yaml
---
- name: Install packages
  hosts: all
  become: yes
  tasks:

    - name: Installs tcpdump and mailx packages on hosts in the proxy host groups
      yum:
        name:
          - tcpdump
          - mailx
        state: latest
      when: inventory_hostname in groups['proxy']
      
    - name: Installs lsof and mailx and packages on hosts in the database host groups
      yum:
        name:
          - lsof
          - mailx
        state: latest
      when: inventory_hostname in groups['database']
```
### Solution of Task15
```yaml
---
- name: default boot target
  hosts: webservers
  become: yes
  tasks:
    - name: Set default boot target to multi-user
      file:
        src: /usr/lib/systemd/system/multi-user.target
        dest: /etc/systemd/system/default.target
        state: link
```
### Solution of Task16
```yaml
# vim server_list.j2
{% for host in groups['all'] %}
{{ hostvars[host].inventory_hostname }}
{% endfor %}
```
```yaml
# vim server_list.yml
---
- name: Create and Use Templates to Create Customised Configuration Files
  hosts: database
  become: yes
  tasks:
    - name: Create server list
      template:
        src: ./server_list.j2
        dest: /etc/server_list.txt
        owner: cloud_user
        mode: '0600'
        setype: net_conf_t
```

#### RHCE8 Practice Exam 2

- Will be updated soon 
