
# Ansible LAMP Stack Deployment

This repository contains an Ansible project designed to automate the installation and configuration of a LAMP stack (Linux, Apache, MySQL, PHP) along with phpMyAdmin on a Debian 12 server.

## Project Structure

```
.
├── ansible.cfg               # Ansible configuration file
├── host_vars                 # Variables specific to hosts
│   └── debian12.yml          # Host-specific variables for Debian 12
├── inventory                 # Inventory file defining hosts
│   └── hosts                 # List of hosts to run the playbook on
├── playbook.yml              # Main Ansible playbook
└── roles                     # Directory containing Ansible roles
    ├── apache                # Apache installation and configuration role
    │   ├── handlers
    │   │   └── main.yml      # Handlers for Apache
    │   ├── tasks
    │   │   └── main.yml      # Apache tasks
    │   └── templates
    │       └── apache.conf.j2 # Jinja2 template for Apache configuration
    ├── mysql                 # MySQL installation and configuration role
    │   └── tasks
    │       └── main.yml      # MySQL tasks
    ├── php                   # PHP installation and configuration role
    │   ├── tasks
    │   │   └── main.yml      # PHP tasks
    │   └── templates
    │       └── info.php.j2   # Jinja2 template for a PHP info file
    └── phpmyadmin            # phpMyAdmin installation and configuration role
        ├── tasks
        │   └── main.yml      # phpMyAdmin tasks
        └── templates
            └── phpmyadmin.conf.j2 # Jinja2 template for phpMyAdmin configuration
```

## Prerequisites

- Ansible installed on the control node
- A Debian 12 server listed in the inventory file
- SSH access to the target host with appropriate privileges

## Roles

### 1. Apache
This role installs and configures Apache2. The configuration file `apache.conf.j2` is applied from a Jinja2 template to customize Apache settings.

- **Tasks**: Located in `roles/apache/tasks/main.yml`
- **Handlers**: Located in `roles/apache/handlers/main.yml` for reloading/restarting the Apache service when necessary.
- **Template**: `apache.conf.j2` defines the Apache configuration.

### 2. MySQL
This role installs and configures MySQL.

- **Tasks**: Located in `roles/mysql/tasks/main.yml`, which sets up the MySQL server.

### 3. PHP
This role installs PHP and creates a sample `info.php` file for testing.

- **Tasks**: Located in `roles/php/tasks/main.yml`
- **Template**: `info.php.j2` is a basic PHP info file for testing the server.

### 4. phpMyAdmin
This role installs and configures phpMyAdmin for easy database management.

- **Tasks**: Located in `roles/phpmyadmin/tasks/main.yml`
- **Template**: `phpmyadmin.conf.j2` is applied for the phpMyAdmin configuration.

## Inventory

The `inventory/hosts` file lists the target server(s) where the playbook will run. Modify this file to define your own hosts. Example structure:

```
[webservers]
192.168.1.10
```

## Variables

Host-specific variables are stored in `host_vars/debian12.yml`. These may include configurations like:

```yaml
---
apache_port: 80
mysql_root_password: your_root_password
php_version: specify_php_version
```

Feel free to customize variables to fit your environment.

## Usage

1. Clone this repository:
    ```bash
    git clone https://github.com/your-repo/ansible-lamp-stack.git
    cd ansible-lamp-stack
    ```

2. Update the inventory file (`inventory/hosts`) with your server's IP.

3. Adjust host-specific variables in `host_vars/debian12.yml` if needed.

4. Run the playbook:

   - **If using `ansible.cfg`** (which already defines the inventory):
     ```bash
     ansible-playbook playbook.yml
     ```

   - **If not using `ansible.cfg`**, specify the inventory manually:
     ```bash
     ansible-playbook -i inventory/hosts playbook.yml
     ```

## Customization

- **Apache**: Customize `roles/apache/templates/apache.conf.j2` to configure Apache settings such as virtual hosts or additional modules.
- **MySQL**: Update `roles/mysql/tasks/main.yml` to set additional database users, databases, or security configurations.
- **PHP**: Modify `roles/php/templates/info.php.j2` or add additional PHP configuration as needed.
- **phpMyAdmin**: Customize `phpMyAdmin` configuration in `roles/phpmyadmin/templates/phpmyadmin.conf.j2`.

## Contributing

Feel free to open issues, submit pull requests, or offer suggestions to improve this project.

## Author

- **Abhishek Mandal**
- [GitHub Profile](https://github.com/abhisheksmandal)
