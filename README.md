Welcome to Ben Ahoure Lab! :)

# Ansible Lab: Multi-Playbook Setup

## Overview
This lab involves setting up an Ansible controller on an Ubuntu server to manage four clients: two Amazon Linux (AMZ) and two Ubuntu clients. Using Ansible, we’ll verify connectivity, deploy an Apache web server with a custom message, install Git, and use the debug module to display a custom message across all hosts.

## Requirements
- Ansible installed on the controller (Ubuntu).
- Four client machines: 2 Amazon Linux (AMZ) and 2 Ubuntu.
- SSH access configured between the Ansible controller and all clients.

## Steps

### 1. Setup and Verify Connection
Ensure the Ansible controller can connect to the clients by using the `ansible -m ping` command to confirm connectivity.

### 2. Playbook Structure
The playbook has three main plays:

#### Play 1: Deploy Apache on Ubuntu Clients
This play deploys an Apache web server on all Ubuntu clients and configures a custom welcome message.

- **Tasks**:
  - Upgrade all packages to the latest version.
  - Install Apache.
  - Start and enable the Apache service.
  - Copy a custom `index.html` file to the web directory.

#### Play 2: Install Git on Ubuntu Clients
This play installs Git on all Ubuntu clients to ensure version control is set up.

#### Play 3: Debug Message on All Hosts
This play uses the debug module to display a custom message ("You are on Ben Ahoure Network") on all hosts.

### Example Playbook Code
```yaml
- name: Install Apache on Ubuntu clients
  hosts: ubuntu-clients
  tasks:
    - name: Upgrade all packages
      ansible.builtin.apt:
        name: '*'
        state: latest
    - name: Install Apache
      ansible.builtin.apt:
        name: apache2
        state: present
    - name: Start Apache service
      ansible.builtin.service:
        name: apache2
        state: started
    - name: Enable Apache service
      ansible.builtin.service:
        name: apache2
        enabled: yes
    - name: Copy custom index.html to web directory
      ansible.builtin.copy:
        src: index.html
        dest: /var/www/html/index.html

- name: Install Git on Ubuntu clients
  hosts: ubuntu-clients
  tasks:
    - name: Install Git
      ansible.builtin.apt:
        name: git
        state: present
        update_cache: yes

- name: Debug Message on All Hosts
  hosts: all
  tasks:
    - name: Display custom message
      ansible.builtin.debug:
        msg: "You are on Ben Ahoure Network"
```

This README provides a structured overview of the lab setup and tasks, ensuring you meet all requirements. 

Happy Learning From Ben Ahoure!