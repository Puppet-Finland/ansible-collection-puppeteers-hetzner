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

# License

This project is licensed under the BSD-2-Clause license. See
[LICENSE](LICENSE).
