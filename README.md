# ansible_gitlab

first tasks
* replace in /host_vars/server.name.tld.yaml
* * gitlab_url
* * gitlab_registry_fqdn
* * gitlab_smtp_address
* * gitlab_smtp_domain
* replace server.name.tld in /hosts.yaml
* rename /host_vars/server.name.tld.yaml to your fqdn.yaml / same as in hosts.yaml 

note: included docker role is for ubuntu bionic / 18

```bash
ansible-playbook ansible_gitlab.yaml -l FQDN.IN.HOSTS.YAML -v
```

partial example: reconfigure only runners
```bash
ansible-playbook ansible_gitlab.yaml -l FQDN.IN.HOSTS.YAML -t gitlab_runners -v
```
