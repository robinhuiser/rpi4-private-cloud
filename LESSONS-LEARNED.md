# Lessons learned

## Proxy

While initially this project implemented a proxy service deployed on the last node in the cluster, this turned out to be a non-reliable, complex solution:

* Multiple network interfaces to route traffic between Kubernetes nodes
* Dual DNS (internal and external)
* Non-conform node setup (since one node had `wlan0` enabled)
* Bringing this interface up or down causes disruption in Kubernetes
* WiFi is slow when pulling updates (takes 4-5 times compared to a wired connection)
* Cannot use an alias for a wired connection since this would screw up the bind configuration of the proxy node

## Using a bastion host for Ansible

Create an SSH configuration file named `work/ssh-bastion.cfg` (example below) and re-run the init task to enable.

~~~ssh
Host 10.0.19.*
  ProxyCommand ssh -W %h:%p user@bastion.domain.com

Host bastion.domain.com
  Hostname bastion.domain.com
  ControlMaster auto
  ControlPath ~/.ssh/ansible-%r@%h:%p
  ControlPersist 5m
~~~

## Notes

* Great article on [Secrets management alternatives](https://medium.com/@gundogdu.emre/kubernetes-secret-management-alternatives-f2b3427a745)
  