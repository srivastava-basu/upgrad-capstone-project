---
- name: Installation of packages and Nginx Server
  hosts: all
  become: true
  tasks:
    - name:
      ping:
    - name: Update repositories cache and install nginx
      apt:
        name: nginx
        update_cache: yes
    - name: Ensure nginx is running
      systemd:
        name: nginx
        state: started
        enabled: yes
- name: Copy the AWS Index File
  hosts: awsvm
  become: true
  tasks:
    - name: Create directory for static content
      file:
        path: /var/www/html/hello-world
        state: directory
        mode: 0755
    - name: Create "index.html" file with "hello world" content
      template:
        src: /home/ubuntu/indexFiles/index-aws.html
        dest: /var/www/html/hello-world/index.html
        mode: 0644
    - name: Copy "index.html" to default Nginx location
      copy:
        src: /var/www/html/hello-world/index.html
        dest: /var/www/html/index.html
        mode: 0644
        remote_src: true

    - name: Enable default Nginx website
      file:
        src: /etc/nginx/sites-available/default
        path: /etc/nginx/sites-enabled/default
        state: link

    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
- name: Copy the Azure Index File
  hosts: azurevm
  become: true
  tasks:
    - name: Create directory for static content
      file:
        path: /var/www/html/hello-world
        state: directory
        mode: 0755
    - name: Create "index.html" file with "hello world" content
      template:
        src: /home/ubuntu/indexFiles/index-azure.html
        dest: /var/www/html/hello-world/index.html
        mode: 0644
    - name: Copy "index.html" to default Nginx location
      copy:
        src: /var/www/html/hello-world/index.html
        dest: /var/www/html/index.html
        mode: 0644
        remote_src: true

    - name: Enable default Nginx website
      file:
        src: /etc/nginx/sites-available/default
        path: /etc/nginx/sites-enabled/default
        state: link

    - name: Restart Nginx
      service:
        name: nginx
        state: restarted
