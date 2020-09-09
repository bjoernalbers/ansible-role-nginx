# Ansible Role: Nginx

An Ansible role to manage Nginx.

## Requirements

This role has been tested under Debian Buster.
Other Debian versions and derivates might work as well.

## Role Variables

### `nginx_config_files`

Dictionary of extra configuration files which will be placed inside `conf.d`.
The key is the file name and the value its content.

Example:

```yaml
nginx_config:
  ssl.conf: |
    ssl_protocols TLSv1.2 TLSv1.3;
    #...
```

### `nginx_available_sites`

Dictionary of available sites.
The key determines the config file name and its value the file content.

Example:

```yaml
nginx_available_sites:
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

### `nginx_enabled_sites`

List of enabled sites.
The values must match the keys from `nginx_available_sites`.

Example:

```yaml
nginx_enabled_sites:
  - default
  - example.com
```

## Dependencies

None

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: bjoernalbers.nginx
      nginx_config_files:
        ssl.conf: |
          ssl_certificate      /etc/letsencrypt/live/example.com/fullchain.pem;
          ssl_certificate_key  /etc/letsencrypt/live/example.com/privkey.pem;
          ssl_protocols        TLSv1.2 TLSv1.3;
          ssl_session_cache    shared:SSL:10m;
          ssl_session_timeout  1d;
          ssl_ciphers ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES128-SHA;
      nginx_available_sites:
        example.com: |
          server {
            listen 443 ssl;
            root /var/www/example.com;
            server_name example.com www.example.com;
            location / {
              try_files $uri $uri/ =404;
            }
          }
```

## License

This Ansible role is released under the [MIT License](LICENSE.txt).
