**DRAFT**

# The Open Block Mesh Project

The objective of this project is to run Hyperledger Version 0.6 under the control of Kubernetes on IBM BlueMix SoftLayer to provide Production-Grade Container Orchestration for Hyperledger containers.

* [Kubernetes](https://github.com/kubernetes/kubernetes)
* [Hyperledger](https://github.com/hyperledger)

This work was commissioned by ANZ Bank which is a member of the Hyperledger Project under the direction of 
* [Ben Smillie](https://github.com/benksmillie) (Ben.Smillie@anz.com)
* Technical Manager - Emerging Technology
* [ANZ Bank](http://www.anz.com)

The goal of this project is to provide a rapid platform to stand up a Hyperledger peer fabric for development purposes under the control of Kubernetes.

This installation leverages kubeadm available in Kubernetes Version 1.4 or later.

* [kubeadm](http://kubernetes.io/docs/getting-started-guides/kubeadm/)


## Prepare Operating System

`curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -`

```
cat <<EOF > /etc/apt/sources.list.d/kubernetes.list
deb http://apt.kubernetes.io/ kubernetes-xenial main
EOF
```

`apt-get update`

`apt-get install -y kubelet kubeadm kubectl kubernetes-cni docker.io`



## Installation

Select one system to be the Kubernetes Master and run:

`kubeadm init`

Once the Control Plane is operational join the nodes with:

`kubeadm join --token <token> <master-ip>`

Example
`kubeadm join --token 3f21bc.a6c4e340c8464657 198.199.117.63`

Install the container networking overlay, in this case weave, with:

`kubectl create -f https://git.io/weave-kube`

Get the status of the cluster:

`kubectl get pods --all-namespaces -o wide`



## Application Sock Shop (Optional)

`kubectl create namespace sock-shop`

`kubectl apply -n sock-shop -f "https://github.com/microservices-demo/microservices-demo/blob/master/deploy/kubernetes/complete-demo.yaml?raw=true"`

`kubectl describe svc front-end -n sock-shop`

`kubectl get pods -n sock-shop`

## Weave Cloud (Optional)

`sudo curl -L git.io/scope -o /usr/local/bin/scope`

`sudo chmod a+x /usr/local/bin/scope`

`scope launch --service-token=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxx`

Example
`scope launch --service-token=9bsoaw99bc6i97r944mcsyfp37ybnb5o`

Access the Weaveworks UI on :


https://cloud.weave.works



