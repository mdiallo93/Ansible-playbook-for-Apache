# Ansible-playbook-for-Apache
Ansible-playbook for Apache


---

- hosts: lab
  become: yes
  tasks:

  - name: install Apache
    yum:
       name: httpd
       state: latest

  - name: Create index file for apache
    file:
      name: /var/www/html/index.html
      state: touch

  - name: adding web content
    lineinfile:
     line: "Apache deployed by ansible"
     path: /var/www/html/index.html

  - name: ensure httpd is running
    service:
      name: httpd
      state: started

  - name: open port 80 for http access
    firewalld:
      service: http
      permanent: true
      state: enabled

  - name: Restart the firewalld service to load in the firewall changes
    service:
     name: firewalld
