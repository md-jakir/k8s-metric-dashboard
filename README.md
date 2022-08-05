# k8s-metric-dashboard
Creating Master and Workers node using Vagrant, Create K8s cluster using Ansible and deploy metric server and k8s dashboard

# Provision VM machine
Provisioning cluster nodes (VirtualBox VMs) using vagrant and installing Docker and Kubeadm packages in cluster nodes.
To create cluster I've firstly writing vagrant script with specificaton and mention ansible playbook location for master and worker nodes location in vagrant script and used following command. One masetr node and two worker nodes defined by N=2 will formed as cluster. 

$ vagrant init

$ vagrant up

To create cluster here, I use weave CNI pluging for pod network. 

