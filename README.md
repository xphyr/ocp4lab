```
> source ~/venv/bin/activate
```

## Intro

This set of playbooks will do the following

1) create a server with dnsmasq installed and configured to support OSE4 install
2) clone the RHCOS image and create a bootstrap, master and worker node machines
3) start the machines


## To begin 

You need to follow the setup instructions for OSE 4 [here](https://docs.openshift.com/container-platform/4.3/installing/installing_vsphere/installing-vsphere.html#installation-obtaining-installer_installing-vsphere)

### If you are running from a MAC use the Dockerfile to create a image to run in
```
$ docker build -t ose4lab:latest .
$ docker run -it -v $(pwd)/ansible:/ocpinstall/ansible ose4lab:latest /bin/bash
```

./openshift-install --dir= wait-for bootstrap-complete --log-level=info