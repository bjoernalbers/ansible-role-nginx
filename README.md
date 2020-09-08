# Ansible Role: Nginx

An Ansible role to manage Nginx.

## Requirements

This role has been tested under Debian Buster.
Other Debian versions and derivates might work as well.

## Role Variables

### `nginx_config`

Dictionary of extra configuration files.
The key is the file name (without `.conf` suffix) and the value its
content.

Example:

```yaml
nginx_config:
  ssl-tweaks: |
    add_header Strict-Transport-Security "max-age=31536000; includeSubdomains";
    add_header X-Frame-Options DENY;
    add_header X-Content-Type-Options nosniff;
    ssl_ciphers 'kEECDH+CHACHA kEECDH+AESGCM HIGH+kEECDH AESGCM 3DES !SRP !PSK !DSS !MD5 !LOW !MEDIUM !aNULL !eNULL !DH !kECDH';
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
```

## License

This Ansible role is released under the [MIT License](LICENSE.txt).
