# Basic Install of Kubernetes with Networking
## standalone kubeadm deployment

These playbooks deploy a very basic installation of kubeadm.
To use them, first edit the "inventory" file to contain the
hostnames of the machines on which you want kubeadm deployed, and edit the
group_vars/ file to set any kubeadm configuration parameters you need.

Then run the playbook, like this:

```
ansible-playbook -i inventory site.yml
```

This is a very simple playbook. It deploys the following:

1. Installs basic components (docker, kubeadm, contiv) 
2. Basic kubernetes cluster using kubeadm (3 nodes is recommended)
3. Calico CNI
4. Istio and sample apps

### Start istio dashboard with access from ec2 instance public ip 

EC2 instances don't know their public ip address (it's managed by AWS infrastructure), so you have to get it from metadata.

From *Master* node:

```
echo "http://$(curl -s http://169.254.169.254/latest/meta-data/public-ipv4):20001/kiali"  # true public url to open dashboard
istioctl dashboard kiali --browser=false --address $(curl -s http://169.254.169.254/latest/meta-data/local-ipv4) # istioctl listening on local ip
```

### Helm

```
curl https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3 | bash
```
