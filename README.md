# Ansible Role: grafana-docker

Ansible role to create grafana docker container.

## Mandatory Role Variables

This role requires you to set the address on which grafana should listen.

```
grafana_docker__listen_address: "{{ ansible_host }}"
```

The container will be exposed to the _grafana_docker__listen_address_ on port 33000.

Upon first start an admin user will be created with the username _admin_ but the password needs to be set with variables:

```
grafana_docker__grafana_admin_password: !vault
```

Also a secret key needs to be set - this should be a string with random alphanumeric chars:

```
grafana_docker__grafana_secret_key: !vault
```

## Optional Role Variables

Optionally the default theme can be set. If not set it will default do dark:

```
grafana_docker__grafana_default_theme: "light"
```

To add datasources it is possible to use the variable _grafana_docker__datasources_:

```
grafana_docker__datasources:
  - name: prometheus
    ds_type: prometheus
    ds_url: "http://{{ mgmt_ipaddress }}:39090"
    access: proxy
    is_default: true
```

To add public Grafana dashboards use the variable _grafana_docker__official_dashboards_:

```
grafana_docker__official_dashboards:
  # node exporter full
  - folder: General
    dashboard_id: 12486
    dashboard_revision: 2
    state: present
    overwrite: yes
  # blackbox exporter
  - folder: General
    dashboard_id: 7587
    dashboard_revision: 3
    state: present
    overwrite: yes
```

To add local or self-created dashboards use the variable _grafana_docker__local_dashboards_:

```
grafana_docker__local_dashboards:
  - folder: General
    path: "{{ playbook_dir }}/grafana_docker/local_dashboards/some-dashboard-16372.json"
    state: present
    commit_message: Updated by ansible
    overwrite: yes
```

Either put the json files in the inventory or for AWX/Tower users put them into the playbook directory.
