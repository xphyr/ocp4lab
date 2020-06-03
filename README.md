```
> source ~/venv/bin/activate
```

## Intro

This set of playbooks will do the following

1) create a server with dnsmasq installed and configured to support OSE4 install
2) clone the RHCOS image and create a bootstrap, master and worker node machines
3) start the machines

## Using Python3 virtual environment

You can install Ansible and its required libraries by doing the following:

```
$ python3 -m venv ./venv
$ source venv/bin/activate
$ pip3 install ansible pyVim PyVmomi
```

## To begin 

You need to follow the setup instructions for OSE 4 [here](https://docs.openshift.com/container-platform/4.3/installing/installing_vsphere/installing-vsphere.html#installation-obtaining-installer_installing-vsphere)

### If you are running from a MAC use the Dockerfile to create a image to run in
```
$ docker build -t ose4lab:latest .
$ docker run -it -v $(pwd)/ansible:/ocpinstall/ansible ose4lab:latest /bin/bash
```

./openshift-install --dir= wait-for bootstrap-complete --log-level=info

## Creating a haproxy load balancer

1. Install Centos8 or RHEL8
2. `yum install haproxy`
3. Create/update haproxy.cfg
4. `sudo setsebool -P haproxy_connect_any 1`
5. `firewall-cmd --permanent --add-port=6443/tcp`
6. `firewall-cmd --permanent --add-port=22623/tcp`
7. `firewall-cmd --permanent --add-port=80/tcp`
8. `firewall-cmd --permanent --add-port=443/tcp`
9. `firewall-cmd --permanent --add-port=1936/tcp`
10. `firewall-cmd --reload`

## Using the ansible script

1. Follow the steps here https://docs.openshift.com/container-platform/4.4/installing/installing_vsphere/installing-vsphere.html#installation-vsphere-config-yaml_installing-vsphere
2. Follow the steps here: https://docs.openshift.com/container-platform/4.4/installing/installing_vsphere/installing-vsphere.html#installation-user-infra-generate-k8s-manifest-ignition_installing-vsphere
3. Once you generate the ignition files, copy them into the ansible files directory