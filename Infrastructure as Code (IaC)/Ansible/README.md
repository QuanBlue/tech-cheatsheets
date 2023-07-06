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
      <a href="https://github.com/quanblue/tech-cheatsheets/tree/master/Infrastructure%20as%20Code%20(IaC)">IaC page</a>
  </b>
</p>

<br/>

<details open>
<summary><b>📖 Table of Contents</b></summary>

-  [Introduction](#rainbow-introduction)
-  [CLI Cheatsheet](#clipboard-cli-cheatsheet)
-  [Key concepts](#key-key-concepts)
-  [Getting Started](#rocket-getting-started)
   -  [Inventory](#inventory)
      -  [Inventory File Format - Cheatsheet](#inventory-file-format---cheatsheet)
         -  [Hosts and Groups](#hosts-and-groups)
         -  [Inventory syntax](#inventory-syntax)
   -  [Playbook, Tasks, Modules and Templates](#playbook-tasks-modules-and-templates)
      -  [Playbook syntax](#playbook-syntax)
      -  [Template](#template)
         -  [Template module](#template-module)
         -  [Template file syntax](#template-file-syntax)
   -  [Debugging and Variables](#debugging-and-variables)
      -  [Variables](#variables)
      -  [Debugging syntax](#debugging-syntax)
   -  [Roles](#roles)
      -  [Role Definition](#role-definition)
      -  [Using Roles](#using-roles)
-  [Useful links](#chains-useful-links)
-  [Relate Project](#link-relate-project)
-  [Credits](#sparkles-credits)
</details>

# :rainbow: Introduction

**Ansible** is an open-source automation tool used for configuration management, application deployment, and orchestration. It simplifies complex IT tasks by allowing you to automate the provisioning, configuration, and management of systems in a streamlined and efficient manner. With Ansible, you can define your infrastructure as code, automate repetitive tasks, and achieve consistent, scalable, and auditable infrastructure management.

# :clipboard: CLI Cheatsheet

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

# :key: Key concepts

-  **Inventory(\*):** An inventory is a file or set of files that _define the hosts and groups of hosts on which Ansible will operate_. It specifies the target machines where Ansible will run tasks.
-  **Playbooks(\*):** Playbooks are files written in `YAML` format that _define a set of tasks and configurations to be executed by Ansible_. Playbooks describe the desired state of the system and orchestrate the execution of tasks across hosts.
-  **Tasks:** _Tasks are the building blocks of `playbooks`_. Each task represents a unit of work to be performed, such as executing a command, managing a file, or restarting a service.
   > -  Tasks are executed sequentially on hosts defined in the playbook.
   > -  1 task = 1 module
-  **Modules:** Modules are units of code that Ansible _uses to perform specific tasks on managed hosts_. They can manage system configurations, interact with APIs, install packages, and more.
   > Ansible ships with a wide range of modules, and you can also create custom modules.
-  **Roles:** Roles _provide a way to organize and package related tasks, variables, and files into reusable units_. They allow you to structure your `playbooks` in a modular and scalable manner, promoting code reuse and maintainability.
-  **Variables:** Variables are _used to store data that can be referenced and reused throughout `playbooks` and `roles`_. They can be defined at various levels, including host level, group level, and globally.
   > Variables can be static or dynamically generated.
-  **Handlers:** Handlers _are tasks that are only executed when triggered_ by a notification. They are typically used to manage services or perform specific actions after a change has been made, such as restarting a service when a configuration file is modified.
-  **Facts:** Facts _are pieces of information about managed hosts_ gathered by Ansible. They include system details like IP addresses, operating system, hardware information, and more.
   > Facts are automatically collected and can be used as variables in `playbooks`.
-  **Templates:** Templates are files written in a templating language (usually Jinja2) that allow you to _generate dynamic content_.
   > They are useful for generating configuration files customized for each host or incorporating variable values into files.
-  **Vault:** Vault is a feature in Ansible that _allows you to encrypt sensitive data_, such as passwords or API keys, within playbooks or variable files.
   > It ensures that sensitive information is stored securely and can only be decrypted during playbook execution.

# :rocket: Getting Started

## Inventory

The default location for this file is `/etc/ansible/hosts`. You can specify a different inventory file at the command line using the `-i <path>` option or in configuration using inventory.

> Run: `ansible-inventory -i <inventory-file> --list` to display inventory information.

### Inventory File Format - Cheatsheet

#### Hosts and Groups

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

#### Inventory syntax

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

## Playbook, Tasks, Modules and Templates

A playbook is a file containing one or more `plays`. A play is a list of `tasks` to be executed on one or more hosts. A task is a call to an `ansible module`.

> Run: `ansible-playbook <playbook-file>` to execute a playbook.

### Playbook syntax

```yml
# playbook.yml
---
- name: <Playbook Name>
  hosts: <target_hosts>
  become: true # Enable privilege escalation if necessary

  tasks:
     - name: <Task Name>
       <module_name>: <module_parameters>
       register: result # Store the result of the task for later use

     - name: <Another Task>
       <module_name>: <module_parameters>

     - name: <Conditional Task>
       <module_name>: <module_parameters>
       when: result.changed # Run the task only if a previous task changed something

     - name: <Looping Task>
       <module_name>: <module_parameters>
       loop:
          - item1
          - item2
          - item3
       loop_control:
          loop_var: my_item # Assign a loop variable for each iteration

     - name: Include Task from File
       include_tasks: tasks/other_task.yml

  handlers:
     - name: Restart Service
       service:
          name: my_service
          state: restarted

  vars: # Define variables specific to this playbook
     variable_name: value

- name: <Another Playbook Name>
  hosts: <another_target_hosts>
  become: true # Enable privilege escalation if necessary

  tasks:
     - name: <Task Name>
       <module_name>: <module_parameters>
       register: result # Store the result of the task for later use
```

<details>
   <summary>Example</summary>

```yml
# playbook.yml
- hosts: web_server
  tasks:
     - name: Test ping
       ping:
     - name: Install nginx
       apt:
          name: nginx
          state: latest

- hosts: database
  tasks:
     - name: Install mongodb
       apt:
          name: mongodb
          state: latest

- hosts: web_application
     - name: Install Neofetch
       apt:
          name: neofetch
          state: latest
     - name: Run Neofetch
       command:
          cmd: neofetch
```

</details>

### Template

#### Template module

```yml
# playbook.yml
- tasks:
     templates:
        src: <template_file> # Template file - Jinja2 (.j2) - in Ansible machine
        dest: <destination_file> # Destination file - in remote machine
```

#### Template file syntax

```jinja2
<!-- template.j2 -->

<!-- Template inclusion -->
{% include 'another_template.j2' %}

<!-- loop -->
{% for item in my_list %}
   Item: {{ item }}
{% endfor %}


<!-- condition -->
{% if condition %}
   Do something
   {% elif another_condition %}
      Do something else
   {% else %}
      Do another thing
{% endif %}

<!-- filter -->
{{ my_variable | capitalize }}
```

<details>
   <summary>Example</summary>

```yml
# playbook.yml - ansible machine
- hosts: all
  tasks:
     - template:
          src: template.j2
          dest: /home/admin/template.j2
  vars:
     items_list:
        - item1
        - item2
```

```jinja2
<!-- template.j2  - ansible machine -->

{% for item in items_list %}
   Item: {{ item }}
{% endfor %}

{% if items_list[2] == 'item3' %}
   Item: item3
{% else %}
   Can not find item3
{% endif %}
```

Run `ansible-playbook playbook.yml` to execute the playbook.

Check the result in `/home/admin/template.j2` file at `remote machine`:

```jinja2
<!-- /home/admin/template.j2 - remote machine -->

Item: item1
Item: item2
Can not find item3
```

</details>

> Ref:
>
> -  [Ansible modules](https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html)
> -  [Playbook syntax](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html#yaml-syntax)
> -  [Template design document](https://jinja.palletsprojects.com/en/3.1.x/templates/)

## Debugging and Variables

Using module `debug` to print out variables.

### Variables

Variables can define in `playbook`, `inventory` or `group_vars` files.

-  In `playbook` file, define variables in `vars` section.

   ```yml
   # playbook.yml
   [...]
   vars:
      <variable_name>: <value>
   ```

-  In `inventory` file, define variables in `all` section.

   ```yml
   # inventory.yml
   [...]
   [<hostname>]
   <host_variable>=<value>
   ```

-  In `group_vars` file, define variables in `group_name.yml` file in `group_vars` directory.
   ```yml
   # group_vars/group_name.yml
   ---
   <variable_name>: <variable_value>
   <another_variable>: <another_value>
   ```

Type of variables:

-  `array`: `["item1", "item2", "item3"]`
   ```yml
   # playbook.yml
   - host: all
     tasks:
        debug:
           var: http_port[0]
     vars:
        http_port:
           - 80
           - 8080
   ```
-  `dictionary`: `{"key1": "value1", "key2": "value2"}`
   ```yml
   # playbook.yml
   - host: all
     tasks:
        debug:
           var: foo['field1']
     vars:
        foo:
           field1: one
           field2: two
   ```
-  `string`: `"string"`

   ```yml
   # playbook.yml
   - host: all
     tasks:
        debug:
           var: foo
     vars:
        foo: bar
   ```

> **Note:** special variable: `ansible_facts`

> Ref
>
> -  [Special Variables](https://docs.ansible.com/ansible/latest/reference_appendices/special_variables.html)
> -  [Facts and Magic variables](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_vars_facts.html)

### Debugging syntax

```yml
# playbook.yml
  [...]
  tasks:
    - name: <Task name>
      <module_name>: <module_parameters>
      register: <output_variable> # Store the output of the task for later use

    # print a variable value, use the debug module with the msg parameter
    - name: Print variable value
      debug:
        msg: "{{ <variable_name> }}"

    #  print debug information, use the debug module with the var parameter
    - name: Print debug information
      debug:
        var: <some_variable>

    # print output of another task
    - name: Print debug information
      debug:
        var: <output_variable> # Use the output variable from the previous task (First task)

    # conditionally display debug output using the when statement
    - name: Conditional debug output
      debug:
        msg: "This will only be printed if the condition is true."
      when: condition
```

<details>
   <summary>Example</summary>

```yml
# playbook.yml
---
- name: Debugging
  hosts: web_server

  tasks:
     - name: Show IPv4
       debug:
          var: ansible_all_ipv4_addresses

     - name: Print Architecture
       debug:
          msg: "{{ ansible_facts['ansible_architecture'] }}"
```

</details>

> Ref:
>
> -  [Debug modules](https://docs.ansible.com/ansible/latest/collections/ansible/builtin/debug_module.html)

## Roles

### Role Definition

Roles follow `Ansible` rule to organize `playbook` and `tasks` into a directory structure.

A role typically includes the following directory structure:

```bash
roles/
├── common/               #  This hierarchy represents a "role"
│   ├── tasks/            #
│   │   └── main.yml      #  <-- tasks file can include smaller files if warranted
│   ├── handlers/         #
│   │   └── main.yml      #  <-- Handlers file
│   ├── templates/        #  <-- files for use with the template resource
│   │   └── ntp.conf.j2   #  <------- templates end in .j2
│   ├── files/            #
│   │   ├── bar.txt       # <-- files for use with the copy resource
│   │   └── foo.sh        # <-- script files for use with the script resource
│   ├── vars/             #
│   │   └── main.yml      # <-- variables associated with this role
│   ├── defaults/         #
│   │   └── main.yml      # <-- default lower priority variables for this role
│   ├── meta/             #
│   │   └── main.yml      # <-- role dependencies
│   ├── library/          # roles can also include custom modules
│   ├── module_utils/     # roles can also include custom module_utils
│   └── lookup_plugins/   # or other types of plugins, like lookup in this case
├── webtier/              # same kind of structure as "common" was above, done for the webtier role
│   └── ...
├── monitoring/           # same kind of structure as "common" was above, done for the monitoring role
│   └── ...
└── fooapp/               # same kind of structure as "common" was above, done for the fooapp  role
    └── ...
```

By default **Ansible** will look in each directory within a role for a `main.yml` file for relevant content (also `main.yaml` and `main`):

-  `tasks/main.yml` - the main list of tasks that the role executes.
-  `handlers/main.yml` - handlers, which may be used within or outside this role.
-  `library/my_module.py` - modules, which may be used within this role (see Embedding modules and plugins in roles for more information).
-  `defaults/main.yml` - default variables for the role (see Using Variables for more information). These variables have the lowest priority of any variables available, and can be easily overridden by any other variable, including inventory variables.
-  `vars/main.yml` - other variables for the role (see Using Variables for more information).
-  `files/main.yml` - files that the role deploys.
-  `templates/main.yml` - templates that the role deploys.
-  `meta/main.yml` - metadata for the role, including role dependencies and optional Galaxy metadata such as platforms supported.

### Using Roles

We have `playbook` and `roles` directory structure as below:

```bash
/etc/ansible/
├── playbook.yml
└── roles/
    └── common/
        ├── tasks/
        │   └── main.yml
        └── vars/
            └── main.yml
```

Content of files:

```yml
# playbook.yml
---
- hosts: webservers
  roles:
     - common
```

```yml
# roles/common/tasks/main.yml
---
- name: Debugging
  debug:
     var: ip_address
```

```yml
# roles/common/vars/main.yml
ip_address: 0.0.0.0
```

It will execute `tasks/main.yml` and `vars/main.yml` in `common` role.

**Execute:** `ansible-playbook /etc/ansible/playbook.yml`

> Ref:
>
> -  [Ansible roles](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)

# :chains: Useful links

-  [Inventory guide](https://docs.ansible.com/ansible/latest/inventory_guide/intro_inventory.html)
-  [Ansible modules](https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html)
-  [Playbook syntax](https://docs.ansible.com/ansible/latest/reference_appendices/YAMLSyntax.html#yaml-syntax)
-  [Ansible roles](https://docs.ansible.com/ansible/latest/playbook_guide/playbooks_reuse_roles.html)
-  [Ansible-Semaphore](https://www.ansible-semaphore.com/)

# :link: Relate Project

-  [**ansible-automation**](https://github.com/QuanBlue/ansible-automation) - Helping you auto create Ansible VPS and Ubuntu VPSs. Auto generate Inventory

# :sparkles: Credits

This software uses the following open source packages:

-  [Ansible](https://www.ansible.com/)
-  Emojis are taken from [here](https://github.com/arvida/emoji-cheat-sheet.com)

---

> Bento [@quanblue](https://bento.me/quanblue) &nbsp;&middot;&nbsp;
> GitHub [@QuanBlue](https://github.com/QuanBlue) &nbsp;&middot;&nbsp; Gmail quannguyenthanh558@gmail.com
