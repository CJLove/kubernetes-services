# Kubernetes
Manifests for deploying things on Kubernetes.  I run a single-node K8S cluster on my home Linux box (Fedora 28 as of this writing), configured via `kubeadm`.  This cluster is only accessible privately, so certain things aren't hardened as much as they could be.

## Foswiki
The actual wiki data is passed in as a volume from the host.  The foswiki service uses NodePort 30000 and everything is deployed in the `foswiki` namespace.  This now uses the following Foswiki docker image: https://hub.docker.com/r/timlegge/docker-foswiki.  Note: Foswiki loses configuration state over pod restarts, 


```
# kubectl create -f foswiki.yaml
```

## wiki.js version 1
Experimental deployment of `https:///wiki.js.org/` version 1.x.  This uses NodePort 30005 for web access.  Everything is deployed in the `wiki-js` namespace.  

```
# kubectl apply -f wiki-js.yaml
```

## wiki.js version 2
Experimental deployment of `https://wiki.js.org/` version 2.x (waiting for the beta release).  This uses NodePort 3006 for web access.  Everything is deployed in the `wiki-js2` namespace.

```
# kubectl apply -f wiki-js2.yaml
```


## OpenGrok
This uses the OpenGrok image from `https://hub.docker.com/r/opengrok/docker/`.  The opengrok service uses NodePort 30001 for web access, NodePort 30002 for ssh and everything is deployed in the `opengrok` namespace.  Regular reindixing is disabled, so a cron job is need to exec into the container.

```
# kubectl create -f opengrok.yaml
```

## Service Account and Role Binding
Yaml for creating an `admin-user` service account, a cluster role binding granting that service account user cluster admin rights, and a shell script for retrieving a token for that user that can be used to login to the K8S dashboard.

```
# kubectl create -f serviceAccount.yaml
# kubectl create -f clusterRoleBinding.yaml
```
To get a token:
```
# dashboard.sh
```
