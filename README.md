# ansible_playbook

* ### [hosts](https://github.com/MSRaith/ansible_playbook/blob/main/hosts)
```
[all]
master ansible_host=192.168.1.135 ansible_user=cent ansible_password=cent
node1 ansible_host=192.168.1.149 ansible_user=cent ansible_password=cent
node2 ansible_host=192.168.1.127 ansible_user=cent ansible_password=cent

[host]
node1 ansible_host=192.168.1.149 ansible_user=cent ansible_password=cent
node2 ansible_host=192.168.1.127 ansible_user=cent ansible_password=cent
```
* ### [playbook homework.yaml](https://github.com/MSRaith/ansible_playbook/blob/main/homework.yaml)
```
- name: netology_ml
  hosts: all
  become: yes
  
  vars:
    packages:
      - net-tools
      - git
      - vim
      - tree
      - mc

  tasks:

  - name: Task Ping
    ping:

  - name: Yum Update
    yum:
      update_cache: yes

  - name: Unistall mc
    yum:
      name: mc
      state: absent
  
  - name: Instaling packages
    yum:
      name: "{{packages}}"
      state: latest
 
  - name: Copy file
    copy:
      src: text.txt
      dest: /home/cent
      mode: 0777
  
  - name: Create groups
    group:
      name: "{{item}}"
      state: present
    loop:
      - devops_1
      - test_1

  - name: Create users
    user:
      name: "{{item.client_name}}"
      shell: /bin/bash
      groups: devops_1, test_1
      append: yes
      home: "/home/{{item.home_dir}}"
    with_items:
      - {client_name: devops_1, home_dir: devops_1}
      - {client_name: test_1, home_dir: test_1}
 
```

* ### LOG:
![image](https://github.com/MSRaith/ansible_playbook/assets/89347252/87527fd8-350e-4878-a255-be545771956d)
![image](https://github.com/MSRaith/ansible_playbook/assets/89347252/27a1fa0d-1dd3-4dcc-8452-f3a56b255db0)

