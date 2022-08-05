# k8s-metric-dashboard
Creating Master and Workers node using Vagrant, Create K8s cluster using Ansible and deploy metric server and k8s dashboard

# Provision VM machine 
Provisioning cluster nodes (VirtualBox VMs) using vagrant and installing Docker and Kubeadm packages in cluster nodes.
Here, I have created cluser node individual using vagrant machine and then used ansible script to create Kubernetes cluser from ansible machine.
To create cluster I've firstly writing vagrant script with specificaton and mention ansible playbook location for master and worker nodes location in vagrant script and used following command. 

$ vagrant init

$ vagrant up

