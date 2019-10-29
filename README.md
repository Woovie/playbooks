# playbooks
My ansible playbooks

## mta-prod-status
Pulls nginx\_status and uptime data from each host. I'm using [JSON callback](https://github.com/ansible/ansible/blob/devel/lib/ansible/plugins/callback/json.py) and sending this data in Python for further logging to a time series database.

## create-jump-users.yml
Creates an 'ansible' user and my own personal user, creates .ssh with 0700 in their home, touches .ssh/authorized\_keys as 0600, and adds the public key to the file. This uses users.yml with contains my variables to load in for iterating each of these tasks.

## users.yml
My user and my ansible user and their public keys. Further data may be added here in the future if need be.

## setup-login.yml
* Enables passwordless sudo in `/etc/sudoers`
* disables root login in `/etc/ssh/sshd_config`
* changes SSH port to `2250` in `/etc/ssh/sshd_config`
* opens port `2250` in firewalld
* adds port `2250` to `ssh_port_t` context with semanage
* Restarts `sshd` services
* Removes `ssh` services from firewalld
