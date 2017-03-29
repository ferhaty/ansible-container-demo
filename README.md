# Ansible Container Demo

Demo of containerized Node.JS app deployment to OpenShift with Ansible Container

## Running a local OpenShift cluster with minishift
```
$ brew install minishift
$ minishift start --vm-driver=virtualbox
$ minishift console

login: developer:developer / admin:admin

console url: https://192.168.99.100:8443
```

### Prepare the OpenShift environment
```
$ oc login --token=<token> --server=<openshift server> or $ oc login --username=developer --password=developer
$ oc new-project ansible-container-demo
```

## Building and deploying the demo app

### Building the container
```
$ ansible-container build
```

### Pushing the container to a registry
```
$ ansible-container push --push-to docker.io/<username> --username <username>
```

### Generate playbook and role for the OpenShift deployment
```
$ ansible-container shipit openshift --pull-from docker.io/<username> --save-config
```

### Deploy to OpenShift
```
$ cd ansible && ansible-playbook shipit-openshift.yml
```

### Check logs
```
$ oc logs dc/web
```

### Get pods and forward local ports to the cluster to access the pods
```
$ oc get pods
NAME          READY     STATUS    RESTARTS   AGE
web-1-k1nn0   1/1       Running   0          31m
$ oc port-forward web-1-k1nn0 8080:8080
Forwarding from 127.0.0.1:8080 -> 8080
Forwarding from [::1]:8080 -> 8080
....
```

### Check whether the app is accessible
```
$ curl http://localhost:8080
Hello World
```
