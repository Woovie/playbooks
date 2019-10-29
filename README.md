# playbooks
My ansible playbooks

## mta-prod-status
Pulls nginx\_status and uptime data from each host. I'm using [JSON callback](https://github.com/ansible/ansible/blob/devel/lib/ansible/plugins/callback/json.py) and sending this data in Python for further logging to a time series database.

## create-jump-users.yml
Goal: Create non-root users to login with.

Tasks:
* Create each user
* Create each user's `.ssh` folder with secure permissoins
* Touch each user's `.ssh/authorized_keys` with secure permissions
* Add each user's public key to their `.ssh/authorized_keys` file

## users.yml
Contains the data for my user and the `ansible` user.

## setup-login.yml
Goal: SSH "hardening" by at least changing the port and disabling some basic insecurities.

This significantly lowers number of login attempts. It's not real hardening, but it does some basic security changes that help a lot with system security.

Tasks:
* Enables passwordless sudo in `/etc/sudoers`
* Disables root login in `/etc/ssh/sshd_config`
* Changes SSH port to `2250` in `/etc/ssh/sshd_config`
* Opens port `2250` in firewalld
* Adds port `2250` to `ssh_port_t` context with semanage
* Restarts `sshd` services
* Removes `ssh` services from firewalld
