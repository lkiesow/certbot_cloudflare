Ansible: Certbot with Cloudflare
================================

Ansible role setting up `certbot` using a DNS challenge via the Cloudflare plugin.

Role Variables
--------------

```yaml
# Email address used for registration with Let's Encrypt
# This address will also receive potential notifications about issued certificates.
# Required
# Default: empty
certbot_cloudflare_email: 'test@example.com'

# Cloudflare API token used to create temporary DNS entries.
# This is not a global account API key!
# Required
# Default: empty
certbot_cloudflare_api_token: '...'

# List of domains requesting a certificate for.
# Default: inventory_hostname
certbot_cloudflare_domains: [ '{{ inventory_hostname }}' ]

# Command executed before generating/renewing certificates.
# Use this e.g. to shut down services which m,ight otherwise interfere.
# This needs to be a valid certbot --pre-hook command line argument.
# Example: --pre-hook 'systemctl stop nginx.service'
# Default: empty
certbot_cloudflare_pre_hook: '...'

# Command executed after generating/renewing certificates.
# Use this to ensure services update their certificates.
# This needs to be a valid certbot --post-hook command line argument.
# Example: --post-hook 'systemctl reload nginx.service'
# Default: empty
certbot_cloudflare_post_hook: '...'
```

Example Playbook
----------------

Example of how to configure and use the role:

```yaml
- hosts: all
  become: true
  roles:
    - role: lkiesow.certbot_cloudflare
      certbot_cloudflare_email: 'test@example.com'
      certbot_cloudflare_api_token: '...'
      certbot_cloudflare_post_hook: '--post-hook "systemctl reload nginx"'
```
