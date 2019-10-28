# playbooks
My ansible playbooks

## mta-prod-status
Pulls nginx_status and uptime data from each host. I'm using [JSON callback](https://github.com/ansible/ansible/blob/devel/lib/ansible/plugins/callback/json.py) and sending this data in Python for further logging to a time series database.
