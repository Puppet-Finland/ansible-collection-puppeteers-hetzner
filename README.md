# Ansible Collection - puppeteers.hetzner

This Ansible collection contains content specific to Hetzner Cloud.

# Roles

## puppeteers.hetzner.floating_ip

This role activates floating IPs for a host. It is assumed that both both IPv4
and IPv6 IPs are available. Role variables:

* **puppeteers_hetzner_floating_ip_v4**: your IPv4 floating IP
* **puppeteers_hetzner_floating_ip_v6**: your IPv6 floating IP

Currently on RHEL derivatives are supported. This role has been tested on RHEL
9 and 10 derivatives (Rocky Linux and Alma Linux)

## puppeteers.hetzner.firewalld_zone_mapping

This role bind an interface to a firewalld zone. This helps in Hetzner where
networks attached to private networks do not get automatically assigned to any
firewalld zone. The role takes two parameters:

* **puppeteers_hetzner_firewalld_zone_mapping_zone**: the firewalld zone (default: *eth1*)
* **puppeteers_hetzner_firewalld_zone_mapping_interface**: the interface (default: *internal*)

## puppeteers.hetzner.networking

This role is an opinionated networking role for Hetzner Cloud virtual machines.
Its main purpose is to configure the Hetzner Cloud private network interface
correctly with split DNS.

The role does a bunch of things:

* Removes the *hc-utils* (Hetzner utils) package which could otherwise cause problems
* Forces cloud-init to use the "network-manager" network renderer
* Creates a NetworkManager connection file for the interface with static IP
  settings, including an IPv4 address, DNS settings and routes.
* Disables carrier detection for the private interface (it never comes up in Hetzner Cloud)
* Installs and enables systemd-resolved

Example usage:

```
puppeteers_hetzner_networking_private_connection_ipv4_address: "10.50.0.100/32"
puppeteers_hetzner_networking_private_connection_ipv4_dns: "10.184.5.15;10.184.5.16;"
puppeteers_hetzner_networking_private_connection_ipv4_dns_search: "mydomain.in;"
puppeteers_hetzner_networking_private_connection_ipv4_routes:
  - "route1=10.15.0.0/16,10.50.0.5,101"
  - "route2=10.16.0.0/16,10.50.0.5,101"
  - "route3=10.17.0.0/16,10.50.0.5,101"
  - "route4=172.16.0.0/24,10.50.0.5,101"
```

If your private network interface or NetworkManager connection names are not
"eth1" and "Wired connection 1", respectively, you change them. For example:

```
puppeteers_hetzner_networking_private_connection_name: eth2
puppeteers_hetzner_networking_private_connection_interface: eth2
```

# License

This project is licensed under the BSD-2-Clause license. See
[LICENSE](LICENSE).
