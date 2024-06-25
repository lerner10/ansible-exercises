# chrony

Installs and configures chrony on RHEL/CentOS or Debian/Ubuntu servers.

[![Build Status](https://travis-ci.org/engonzal/ansible_role_chrony.svg?branch=master)](https://travis-ci.org/engonzal/ansible_role_chrony)

## Requirements

Note that this role requires root.  Ensure become: yes is set at the top level of your playbook or invoke the role in your playbook like:

```yaml
- hosts: chrony
  roles:
    - role: engonzal.chrony
      become: yes
```

## Role Variables

Available variable with examples are below:

```yaml
chrony_servers:
  - time.cloudflare.com iburst prefer port 1514
chrony_pools:
  - ntp.ubuntu.com        iburst maxsources 2
```

You can specify custom servers and pools, by default the role uses the ubuntu and cloudflare pools.

```yaml
chrony_measurements_statistics_tracking: false
chrony_disable_external_client: true
```

You can also enable some enhanced logging, and allow your chrony daemon to accept incoming ntp connections (disable for security).

## Example Playbook

### Simple Example (defaults)

```yaml
- hosts: servers
  roles:
      - { role: engonzal.chrony }
```

### Advanced Example (custom server)

```yaml
- hosts: servers
  vars:
    chrony_servers:
      # Custom time server with different port
      - time.example.com iburst prefer port 1514
      # Regular time server
      - time.cloudflare.com iburst prefer
  roles:
      - { role: engonzal.chrony }
```

## License

BSD

## Author Information

This role was created in 2019 by Noe Gonzalez (<http://engonzal.com> and <https://buildahomelab.com>)
