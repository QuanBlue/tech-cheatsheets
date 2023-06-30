<h1 align="center">
  <img src="./assets/ansible-logo.png" alt="icon" height="150"></img>
  <br>
  <b>Ansible Cheatsheet</b>
</h1>

<p align="center">Automation tool for configuration management, orchestration, and application deployment across infrastructure.</p>

<!-- Badges -->
<p align="center">
  <a href="https://github.com/quanblue/tech-cheatsheets/graphs/contributors">
    <img src="https://img.shields.io/github/contributors/quanblue/tech-cheatsheets" alt="contributors" />
  </a>
  <a href="">
    <img src="https://img.shields.io/github/last-commit/quanblue/tech-cheatsheets" alt="last update" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/network/members">
    <img src="https://img.shields.io/github/forks/quanblue/tech-cheatsheets" alt="forks" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/stargazers">
    <img src="https://img.shields.io/github/stars/quanblue/tech-cheatsheets" alt="stars" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/issues/">
    <img src="https://img.shields.io/github/issues/quanblue/tech-cheatsheets" alt="open issues" />
  </a>
  <a href="https://github.com/quanblue/tech-cheatsheets/blob/master/LICENSE">
    <img src="https://img.shields.io/github/license/quanblue/tech-cheatsheets.svg" alt="license" />
  </a>
</p>

<p align="center">
  <b>
      <a href="https://github.com/quanblue/tech-cheatsheets">Home page</a> •
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/CI.CD">CI/CD page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [:rainbow: Introduction](#rainbow-introduction)
-  [CLI Cheatsheet](#cli-cheatsheet)
-  [Key concepts](#key-concepts)
   -  [Inventory](#inventory)
   -  [Playbooks](#playbooks)
   -  [Tasks](#tasks)
   -  [Modules](#modules)
   -  [Roles](#roles)
   -  [Variables](#variables)
   -  [Handlers](#handlers)
   -  [Facts](#facts)
   -  [Templates](#templates)
   -  [Vault](#vault)
-  [:chains: Useful links](#chains-useful-links)
-  [:sparkles: Credits](#sparkles-credits)
</details>

# :rainbow: Introduction

**Ansible** is an open-source automation tool used for configuration management, application deployment, and orchestration. It simplifies complex IT tasks by allowing you to automate the provisioning, configuration, and management of systems in a streamlined and efficient manner. With Ansible, you can define your infrastructure as code, automate repetitive tasks, and achieve consistent, scalable, and auditable infrastructure management.

# CLI Cheatsheet

Running Ansible tasks.

```bash
ansible <host-pattern> -m <module-name>
ansible -i <inventory-file> -m <module-name>
```

Run Playbooks

```bash
ansible-playbook <playbook-file>
```

Manages Ansible roles.

```bash
ansible-galaxy install <role-name>
ansible-galaxy init <role-name>
```

Encrypts and decrypts sensitive data in Ansible files.

```bash
ansible-vault create <file-name>
ansible-vault edit <file-name>
ansible-vault decrypt <file-name>
```

Displays Ansible configuration settings.

```bash
ansible-config list
ansible-config view
```

Displays documentation for Ansible modules.

```bash
ansible-doc <module-name>
```

Displays Ansible inventory information.

```bash
ansible-inventory -i <inventory-file> --list
```

Opens an interactive Ansible console.

```bash
ansible-console
```

Pulls and applies configurations from Ansible on remote hosts.

```bash
ansible-pull -U <repository-url> <playbook-file>
```

# Key concepts

## Inventory

**Inventory:** An inventory is a file or set of files that _define the hosts and groups of hosts on which Ansible will operate_. It specifies the target machines where Ansible will run tasks.

The default location for this file is `/etc/ansible/hosts`. You can specify a different inventory file at the command line using the `-i <path>` option or in configuration using inventory.

-  **Hosts and Groups:**

   -  `[group_name]`: Defines a group of hosts.
   -  `<host1_name> ansible_host=<host1_ip>`: Defines a host name (alias) and its IP address.
   -  `<host1_ip> ansible_user=<username>`: Defines the remote username for a host.
   -  `<group_name>: <child_group1>, <child_group2>`: Defines group hierarchy.

-  **Patterns for Host Selection:**

   -  `all`: Selects all hosts.
   -  `host1_ip`: Selects a specific host.
   -  `group_name: Selects all hosts in a group.
   -  `group1:&group2`: Selects hosts common to both groups.
   -  `group_name[0]`: Selects the first host in a group.

-  **Variables:**
   -  `ansible_host`: Defines the host's IP address.
   -  `ansible_user`: Defines the remote username for a host.
   -  `ansible_password`: Defines the remote password for a host.
   -  `ansible_port`: Defines the SSH port for a host.
   -  `ansible_connection`: Defines the connection type (e.g., ssh, local, etc.).
   -  `ansible_ssh_private_key_file`: Defines the SSH private key file path.
   -  `ansible_become_user`: Defines the user to become (sudo/su) on the remote host.

Inventory files are written in `INI` or `YAML` format.

```ini
; inventory.ini

[<group_name>]
<host1_ip>
<host2_ip> ansible_user=<username>
<host3_name> ansible_host=<host3_ip> ansible_user=<username> ansible_password=<password>

[<child_group>]
<host4_name> ansible_host=<host4_ip>

[<group_name>:children]
<child_group>
```

```yaml
# inventory.yaml

all:
   hosts:
      <host1_ip>:
      <host2_ip>:
         ansible_user: <username>
      <host3_name>:
         ansible_host: <host3_ip>
         ansible_user: <username>
         ansible_password: <password>

   children:
      <child_group>:
         hosts:
            <child_host>:
               <host4_name>:
                  ansible_host: <host4_ip>

<group_name>:
   children:
      - <child_group>
```

<details>
   <summary>Example</summary>

In `ini`

```ini
; inventory.ini

[web_client]
192.168.1.10
192.168.1.11 ansible_user=admin

[web_sever]
express_js ansible_host=192.168.1.12 ansible_user=admin ansible_password=admin

[database]
mongodb ansible_host=192.168.1.13

[web_application:children]
web_client
web_sever
database
```

In `yaml`

```yaml
# inventory.yaml

web_application:
   children:
      web_client:
         hosts:
            192.168.1.10:
            192.168.1.11:
               ansible_user: admin
      web_server:
         hosts:
            express_js:
               ansible_host: 192.168.1.12
               ansible_user: admin
               ansible_password: admin
      database:
         hosts:
            mongodb:
               ansible_host: 192.168.1.13
```

</details>

> Ref: https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html

## Playbooks

**Playbooks:** Playbooks are files written in YAML format that define a set of tasks and configurations to be executed by Ansible. Playbooks describe the desired state of the system and orchestrate the execution of tasks across hosts.

## Tasks

**Tasks:** Tasks are the building blocks of playbooks. Each task represents a unit of work to be performed, such as executing a command, managing a file, or restarting a service. Tasks are executed sequentially on hosts defined in the playbook.

## Modules

**Modules:** Modules are units of code that Ansible uses to perform specific tasks on managed hosts. They can manage system configurations, interact with APIs, install packages, and more. Ansible ships with a wide range of modules, and you can also create custom modules.

## Roles

**Roles:** Roles provide a way to organize and package related tasks, variables, and files into reusable units. They allow you to structure your playbooks in a modular and scalable manner, promoting code reuse and maintainability.

## Variables

**Variables:** Variables are used to store data that can be referenced and reused throughout playbooks and roles. They can be defined at various levels, including host level, group level, and globally. Variables can be static or dynamically generated.

## Handlers

**Handlers:** Handlers are tasks that are only executed when triggered by a notification. They are typically used to manage services or perform specific actions after a change has been made, such as restarting a service when a configuration file is modified.

## Facts

**Facts:** Facts are pieces of information about managed hosts gathered by Ansible. They include system details like IP addresses, operating system, hardware information, and more. Facts are automatically collected and can be used as variables in playbooks.

## Templates

**Templates:** Templates are files written in a templating language (usually Jinja2) that allow you to generate dynamic content. They are useful for generating configuration files customized for each host or incorporating variable values into files.

## Vault

**Vault:** Vault is a feature in Ansible that allows you to encrypt sensitive data, such as passwords or API keys, within playbooks or variable files. It ensures that sensitive information is stored securely and can only be decrypted during playbook execution.

# :chains: Useful links

-  [Inventory guide](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)
-  Ansible-Semaphore

# :sparkles: Credits

This software uses the following open source packages:

-  [Ansible](https://www.ansible.com/)
-  Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com

```

```
