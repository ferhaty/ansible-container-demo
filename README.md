# Ansible Container Demo

Demo of Node.JS app deployment to OpenShift with Ansible Container

## Building and deploying the demo app
```
$ ansible-container build
$ ansible-container push --push-to docker.io/<username> --username <username>
$ ansible-container shipit openshift --pull-from docker.io/<username> --save-config
$ oc login --token=<token> --server=<openshift server>
$ oc new-project ansible-container-demo
$ cd ansible && ansible-playbook shipit-openshift.yml
```
