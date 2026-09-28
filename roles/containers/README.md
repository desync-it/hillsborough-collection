# Hillsborough College Containers role

Ansible role to deploy or remove container imags on target hosts.

## Role Variables

### Lists
| Variable | description | type | default | required |
|----------|-------------|------|---------|----------|
|`containers_deployment_manifest` | header variable to hold a list of dictionaries | `list` | `[]` | true |

### Dictionary format
| Variable | description | type | default | required |
|----------|-------------|------|---------|----------|
| `name`   | Short description | `str` | "" | `true` |
| `registry` | URL container of the container registry | `str` | "" | `false` if `image_state` is absent |
| `registry_user` | Username to login to container registry | `str` | "" | `false` if `image_state` is absent | 
| `registry_token` | Token to use to login to container registry | `str` | "" | `false` if `image_state` is absent |
| `image_name` | Name of image in container registry and expected name of container to run on target hosts | `str` | "" | `true` |
| `image_state` | Supported values `present` or `absent` | `str` | "" | `true` |
| `image_tag`  | `Container tag to pull` | `str` | "" | `true` |

### Dependencies
```
- name: containers.podman
  type: collection
  version: >= 1.20.2
``` 

### Example Playbook
```
---
- name: Manage containers
  hosts: all

  roles:
    - role: hillsborough.college.containers
      vars:
        containers_manifest:
           - name: Deploy the gears web server
             registry: registry.gitlab.com/hillsborough-college
             registry_user: "{{ containers_registry_user }}"
             registry_password: "{{ containers_registry_password }}"
             image_name: hillsborough-webserver
             image_state: present
             image_tag: v1.0
```

### License

GPL-3.0

### Author

Justin Herron <jherron@net-dev.net>
