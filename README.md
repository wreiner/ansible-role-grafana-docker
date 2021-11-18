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
