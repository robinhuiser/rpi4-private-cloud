# Troubles and solutions

You will run into issues... hence this page with symptoms & diagnoses + common commands ;-)

## Common commands

~~~bash
# View a certificate
$ openssl x509 -text -noout -in /path/to/your/certificate.csr

# Force regenerating kubernetes certificates - as root
$ mv mv /var/snap/microk8s/current/var/lock/no-cert-reissue \
    /var/snap/microk8s/current/var/lock/no-cert-reissue_OLD
# -- wait for new front-proxy, kubelet and server files
$ ls -ltr /var/snap/microk8s/current/certs
# -- recreate lock
$ mv mv /var/snap/microk8s/current/var/lock/no-cert-reissue_OLD \
    /var/snap/microk8s/current/var/lock/no-cert-reissue
~~~