# Ansible playbooks for Linux - install Gui.

* XFCE(SLIM)

## Getting started

### Supported distributions

* Ubuntu Trusty
* Debian (Not tested)

Other versions of the distributions listed above might work, but no guarantees given. See testing if you want to try running the distribution of your choice in virtual machines.

### Installing Ansible
You can install Ansible by following the [official installation documentation](http://docs.ansible.com/ansible/intro_installation.html). For Windows 10 users, you can use the instructions for Ubuntu after [installing the Linux subsystem](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide). For older Windows version, please [check this tutorial on running Ansible on cygwin](https://www.jeffgeerling.com/project/running-ansible-within-windows).

### Clone the repository
```shell
git clone git@github.com:Rishats/ansible_gui_for_linux_server.git
```

### Configure your inventory files
The inventory files are located in the inventory directory. Check the example for development and read the [Ansible documentation](http://docs.ansible.com/ansible/intro_inventory.html).

### Configure your host variables
Host variables control some of the aspects how the machine is configured. Store the host variable file with the same name as the hostname in the inventory file. Below is an example for the local development machine. 

```yaml
# User for VPS
system_user:
  user_login: user
  user_password: pwd
```

#### Supported variables

| Name                                   | Description                                                                                                            | Required |
|----------------------------------------|------------------------------------------------------------------------------------------------------------------------|----------|
| user_login                             | Configured user with sudo access.                          | Yes       |
| user_password                             | Configured user password.                          | Yes       |

### Install
1) git clone project.
2) create file server.yml in host_vars and paste data from server_example.yml.
3) python3 -m venv env
4) source env/bin/activate
5) pip install -r requirements.txt
6) ansible -i inventory/server servers -m ping
7) python3 $(which ansible-playbook) -i inventory main.yml

## Running

### Checking SSH access
After you have done with the configuration make sure you have SSH access to the servers that listed on the inventory file. You can test this by using the ping module. Troubleshooting the SSH connection is the out of scope of this repository. Please note that you can set the SSH user and port in the inventory file, see the development for example.

```shell
ansible -i inventory/server servers -m ping
localhost | SUCCESS => {
    "changed": false,
    "ping": "pong"
}
```

### Running the Playbook
You can run the playbook on all hosts with the following command:
```shell
ansible-playbook -i inventory main.yml
```  

### Running custom playbooks
Sometimes you have something specific which laravel_monolit does not cover. In that case you can create your custom playbooks. Store the playbooks to `roles/custom/files` with the .yml extension and they will be executed on all roles.

## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.
