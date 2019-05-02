# DEPRECATED!

DEPRECATED in favour of [coopdevs/opencell-provisioning](https://gitlab.com/coopdevs/opencell-provisioning/).

# OpenCell Provision

Ansible project to provision a server of [OpenCell](https://opencellsoft.com/) last version.

## Requeriments

This project has been thinked to run in Ubuntu 18.04 (Bionic)

* Ansible 2.5.2 or last

You can find more information about Ansible [here](http://docs.ansible.com/)

## Usage
**TODO:** Add instructions to deploy with the SH and the Docker Compose file: https://docker.opencellsoft.com

## Playbooks

### Create System Administrators users - `playbooks/sys_admins.yml`

This playbook use the [`sys-admins` role](https://github.com/coopdevs/sys-admins-role) of Coopdevs to manage the system administrators users.

### Provision - `playbooks/provision.yml`
This playbook do:

* Install the system packages
* Create `opencell` user to deploy and start/stop/restart the dockers
* Install NGINX and Certbot to manage the Let's Encrypt certificates

To use, run:
```
ansible-playbook playbooks/provision.yml -u USER --limit HOSTGROUP
```

## Configurable Variables

This examples are from `./inventory/host_vars/local.tryton.coop/config.yml`. You can create new `host_vars` folder with your domain as name and modify this vars.
We recommend encrypting the variables with sensitive information with [Ansible Vualt](https://docs.ansible.com/ansible/2.4/vault.html) and use `--ask-vault-pass` in the command line.

* Sysadmins
```YAML
system_administrators_group:      # System administrators group
system_administrators:            # List of system administrators added to the group
  - name:                         # User name
    ssh_key:                      # User SSH public key file path
    state:                        # User state (present/absent)
```

* Certbot vars
```YAML
certificate_authority_email:      # Mail to use in Let's Encrypt to generate  the certificate
```

## Ansible Community Roles

To download the community roles, you can run:
```
ansible-galaxy install -r requirements.yml
```

### List of Galaxy roles:

* [SysAdmins Role](https://galaxy.ansible.com/coopdevs/sys-admins-role) -- We are waiting to the new release because we use the new features added with the [#PR9](https://github.com/coopdevs/certbot_nginx/pull/9)
* [Certbot NGINX Role](https://galaxy.ansible.com/coopdevs/certbot_nginx)
* [NGINX Role](https://galaxy.ansible.com/jdauphant/nginx)

## Devenv

## Contributing

1. Fork it (<https://github.com/coopdevs/opencell_provisioning>)
2. Create your feature branch (`git checkout -b feature/fooBar`)
3. Commit your changes (`git commit -am 'Add some fooBar'`)
4. Push to the branch (`git push origin feature/fooBar`)
5. Create a new Pull Request
