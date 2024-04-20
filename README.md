How to complete the weekend homework with commands 

Insall Ansible  
  # yum install ansible
Create SSH key  
  # ssh-key-gen 
Copy ssh key to server B 
  # ssh-copy-id root@10.1.18.190
Set up inventory host file using 
  # mkdir ansibletesting
  # vim inventory  
  add goup name and IP 
Run adhoc command to get current disk space of target server, redirect to outtput.txt
  # ansible -i inventory main -a "df -h" > output.txt 
Create a playbook using copy and archive module 
  # vim ansiblehomework.yaml
  
  ---

- name: Ansible HW Playbook
  gather_facts: false
  hosts: all
  tasks:

    - name: copy NIC file to opt directory and rename HOMEWORK
      copy:
        src: /etc/sysconfig/network-scripts/ifcfg-ens192
        dest: /opt/HOMEWORK
        owner: root
        group: root

    - name: archive and compress /var/log/secure into /var/log/secure.tar.gz
      archive:
        path: /var/log/secure
        dest: /var/log/secure.tar.gz
        format: gz

  Run playbook
    # ansible-playbook -i inventory ansiblehomework.yaml
