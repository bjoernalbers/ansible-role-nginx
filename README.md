# Ansible Role: Nginx

An Ansible role to manage Nginx.

## Requirements

This role has been tested under Debian Buster.
Other Debian versions and derivates might work as well.

## Role Variables

### `nginx_sites_available`

Dictionary of available sites.
The key determines the config file name and its value the file content.

Example:

```yaml
nginx_sites_available:
  example.com: |
    server {
      listen 80;
      root /var/www/example.com;
      server_name example.com www.example.com;
      location / {
        try_files $uri $uri/ =404;
      }
    }
```

## Dependencies

None

Example Playbook
----------------

```yaml
- hosts: all
  roles:
     - role: bjoernalbers.nginx
```

## License

This Ansible role is released under the [MIT License](LICENSE.txt).
