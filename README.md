[![Ansible Galaxy](https://img.shields.io/badge/galaxy-nginxinc.nginx__config-5bbdbf.svg)](https://galaxy.ansible.com/nginxinc/nginx_config)
[![Molecule CI/CD](https://github.com/nginxinc/ansible-role-nginx-config/workflows/Molecule%20CI/CD/badge.svg)](https://github.com/nginxinc/ansible-role-nginx-config/actions)
[![License](https://img.shields.io/badge/License-Apache--2.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](https://www.repostatus.org/badges/latest/active.svg)](https://www.repostatus.org/#active)

# 👾 *Help make the NGINX config Ansible role better by participating in our [survey](https://forms.office.com/Pages/ResponsePage.aspx?id=L_093Ttq0UCb4L-DJ9gcUKLQ7uTJaE1PitM_37KR881UM0NCWkY5UlE5MUYyWU1aTUcxV0NRUllJSC4u)!* 👾

# Ansible NGINX Configuration Role

This role configures NGINX Open Source and NGINX Plus on your target host.

**Note:** This role is still in active development. There may be unidentified issues and the role variables may change as development continues.

## Requirements

### Ansible

- This role is developed and tested with [maintained](https://docs.ansible.com/ansible/devel/reference_appendices/release_and_maintenance.html) versions of Ansible core (above `2.12`).
- When using Ansible core, you will also need to install the following collections:

    ```yaml
    ---
    collections:
      - name: ansible.posix
        version: 1.5.4
      - name: community.general
        version: 7.1.0
      - name: community.docker # Only required if you plan to use Molecule (see below)
        version: 3.4.7
    ```

    **Note:** You can alternatively install the Ansible community distribution (what is known as the "old" Ansible) if you don't want to manage individual collections.
- Instructions on how to install Ansible can be found in the [Ansible website](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html#upgrading-ansible-from-version-2-9-and-older-to-version-2-10-or-later).

### Jinja2

- This role uses Jinja2 templates. Ansible core installs Jinja2 by default, but depending on your install and/or upgrade path, you might be running an outdated version of Jinja2. The minimum version of Jinja2 required for the role to properly function is `3.1`.
- Instructions on how to install Jinja2 can be found in the [Jinja2 website](https://jinja.palletsprojects.com/en/3.1.x/intro/#installation).

### Molecule (Optional)

- Molecule is used to test the various functionalities of the role. The recommended version of Molecule to test this role is `4.x`.
- Instructions on how to install Molecule can be found in the [Molecule website](https://molecule.readthedocs.io/en/latest/installation.html). *You will also need to install the Molecule Docker driver.*
- To run the NGINX Plus/App Protect config Molecule tests, you must copy your NGINX Plus/App Protect license to the role's [`files/license`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/files/license/) folder.

  You can alternatively add your NGINX Plus/App Protect repository certificate and key to the local environment. Run the following commands to export these files as base64-encoded variables and execute the Molecule tests:

  ```bash
  export NGINX_CRT=$( cat <path to your certificate file> | base64 )
  export NGINX_KEY=$( cat <path to your key file> | base64 )
  molecule test -s plus
  ```

## Installation

### Ansible Galaxy

To install the latest stable release of the role on your system, use:

```bash
ansible-galaxy install nginxinc.nginx_config
```

Alternatively, if you have already installed the role, update the role to the latest release:

```bash
ansible-galaxy install -f nginxinc.nginx_config
```

### Git

To pull the latest edge commit of the role from GitHub, use:

```bash
git clone https://github.com/nginxinc/ansible-role-nginx-config.git
```

## Platforms

The NGINX config Ansible role supports all platforms supported by [NGINX Open Source](https://nginx.org/en/linux_packages.html#mainline) and [NGINX Plus](https://www.nginx.com/products/technical-specs/).

***Note:** You should be able to use this role to configure any NGINX installation -- wherever/however it's been installed -- at your own risk. Any potential bugs with the role involving unsupported installation methods/platforms will be addressed in a best effort manner and might be outright dismissed.*

## Role Variables

This role has multiple variables. The descriptions and defaults for all these variables can be found in the **[`defaults/main/`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/defaults/main/)** folder in the following files:

| Name | Description |
| ---- | ----------- |
| **[`main.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/defaults/main/main.yml)** | NGINX simple config variables |
| **[`selinux.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/defaults/main/selinux.yml)** | Set up SELinux to allow the necessary connections to your NGINX setup |
| **[`template.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/defaults/main/template.yml)** | NGINX config template variables |
| **[`upload.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/defaults/main/upload.yml)** | NGINX config/HTML/SSL upload variables |

## Example Playbooks

Working functional playbook examples can be found in the **[`molecule/`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/molecule/)** folder in the following files:

| Name | Description |
| ---- | ----------- |
| **[`cleanup_module/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/molecule/cleanup_module/converge.yml)** | Cleanup an NGINX config and configure NGINX supported modules |
| **[`default/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/molecule/default/converge.yml)** | Use the NGINX config templating variables to create an NGINX config |
| **[`plus/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/molecule/plus/converge.yml)** | Use the NGINX config templating variables to create an NGINX Plus config |
| **[`push/converge.yml`](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/molecule/stable_push/converge.yml)** | Push a preexisting config from your system to your NGINX instance |

Do note that if you install this repository via Ansible Galaxy, you will have to replace the role variable in the sample playbooks from `ansible-role-nginx-config` to `nginxinc.nginx_config`.

## Other NGINX Ansible Collections and Roles

You can find the Ansible NGINX Core collection of roles to install and configure NGINX Open Source, NGINX Plus, and NGINX App Protect [here](https://github.com/nginxinc/ansible-collection-nginx).

You can find the Ansible NGINX role to install NGINX OSS and NGINX Plus [here](https://github.com/nginxinc/ansible-role-nginx).

You can find the Ansible NGINX App Protect role to install and configure NGINX App Protect WAF and NGINX App Protect DoS [here](https://github.com/nginxinc/ansible-role-nginx-app-protect).

You can find the Ansible NGINX Unit role to install NGINX Unit [here](https://github.com/nginxinc/ansible-role-nginx-unit).

## License

[Apache License, Version 2.0](https://github.com/nginxinc/ansible-role-nginx-config/blob/main/LICENSE)

## Author Information

[Alessandro Fael Garcia](https://github.com/alessfg)

&copy; [F5, Inc.](https://www.f5.com/) 2020 - 2023
