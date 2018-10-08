# Kubernetes
Manifests for deploying things on Kubernetes.  I run a single-node K8S cluster on my home Linux box (Fedora 28 as of this writing), configured via `kubeadm`.  This cluster is only accessible privately, so certain things aren't hardened as much as they could be.

## Foswiki
I have a home-built foswiki docker image (based on Centos and a foswiki rpm).  The actual wiki data is passed in as a volume from the host.  The foswiki service uses NodePort 30000 and everything is deployed in the `foswiki` namespace.

TODO: Refresh the foswiki docker image or use one of the publicly-available images

```
# kubectl create -f foswiki.yaml
```

## OpenGrok
This uses the OpenGrok image from `https://hub.docker.com/r/opengrok/docker/`.  The opengrok service uses NodePort 30001 for web access, NodePort 30002 for ssh and everything is deployed in the `opengrok` namespace.

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