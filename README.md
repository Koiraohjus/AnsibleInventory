# Ansible Home Lab

This project is an Ansible home lab built with VMware and Alpine Linux.

The goal of the lab is to gain hands-on experience with:

- Ansible automation
- Linux server administration
- SSH key authentication
- Automated network configuration
- Routing and NAT
- Infrastructure as Code (IaC)

## Environment

### Control Node

- Linux Mint
- Ansible

### Managed Hosts

- Router
- Client
- Server

## Network Topology

```text
                Management Network
                 10.201.50.0/24

        Router        Client        Server
          eth0          eth0          eth0
            |             |             |
            +-------------+-------------+

------------------------------------------------

               Internal Lab Networks

       10.1.1.0/24             10.2.2.0/24

       Client ---- Router ---- Server
         eth1       eth1 eth2    eth1
```

## Features

### Router

- Static interfaces
- IP forwarding
- NAT / Masquerade
- Routing between client and server networks

### Client

- Static lab interface
- DHCP management interface

### Server

- Static lab interface
- DHCP management interface

## Project Structure

```text
AnsibleInventory/
├── ansible.cfg
├── inventory.yml
├── group_vars/
│   └── all.yml
├── host_vars/
│   ├── router.yml
│   ├── client.yml
│   └── server.yml
├── playbooks/
│   ├── configure_network.yml
│   ├── packages.yml
│   ├── users.yml
│   └── site.yml
├── templates/
│   ├── router_interfaces.j2
│   └── host_interfaces.j2
└── README.md
```

## Inventory

```yaml
all:
  hosts:
    router:
      ansible_host: 10.201.50.251

    client:
      ansible_host: 10.201.50.213

    server:
      ansible_host: 10.201.50.63
```

## Installed Packages

Managed through Ansible:

- bash
- curl
- nano
- vim
- tcpdump
- traceroute
- iproute2
- python3

## User Management

Ansible creates:

- admin user
- wheel group membership
- SSH public key authentication
- hashed password

## Common Commands

Verify connectivity:

```bash
ansible all -m ping
```

Run package installation:

```bash
ansible-playbook playbooks/packages.yml
```

Configure networking:

```bash
ansible-playbook playbooks/configure_network.yml
```

Configure users:

```bash
ansible-playbook playbooks/users.yml
```

Run complete configuration:

```bash
ansible-playbook site.yml
```

## Lessons Learned

- Ansible requires Python on managed hosts.
- SSH key authentication is preferred over passwords.
- Static routes and NAT are required for internet access from internal networks.
- Jinja2 templates simplify network configuration management.
- Infrastructure should be reproducible through playbooks instead of manual commands.
- Configuration should remain functional after reboot.

## Future Improvements

- Docker deployment with Ansible
- Firewall automation
- Ansible roles
- Ansible Vault for secrets
- Monitoring and logging
- Dynamic inventory
- Automated backups

