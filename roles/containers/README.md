# Hillsborough College Containers role

Ansible role to deploy or remove container imags on target hosts.

## Role Variables
|         Variable              | description                        | type   | default | required |  
|-------------------------------|------------------------------------|--------|---------|----------|  
| `containers_package_manifest` | Packages to install on target host | `list` |  null   | `false`  |  
| `containers_registry` | Registry url with namespace        | `str` | null | `true` |  
| `containers_registry_user` | Username to use to login to a registry | `str` | null | `false` |  
| `containers_registry_token` | Token to use to login to a registry | `str` | null | `false` |  
| `containers_runtime_name`     | String to use when naming the container at runtime | `str` | null | `true` |  
| `containers_runtime_image` | Name of the container to pull and deploy | `str` | null | `false` |  
| `containers_runtime_image_tag` | Image tag to pull from registry | `str` | latest | `false` |  
| `containers_runtime_image_state` | Expected state of container on target host | `str` | null | `true` |  


### Dependencies

```yaml
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
        containers_registry: quay.io/desync
        containers_runtime_name: hillsborough-webserver
        containers_runtime_image: hillsborough-webserver
        containers_runtime_image_tag: latest
        containers_runtime_image_state: present
        containers_package_manifest:
          - podman 
```

### License

GPL-3.0

### Author

Justin Herron <jherron@net-dev.net>
