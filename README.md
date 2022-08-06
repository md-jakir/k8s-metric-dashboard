# Prerquisits to set-up k8s cluster: 
- Need to install vagrant in host machine
- Need to install VirtualBox 

# Provisioning VM machine
Provisioning cluster nodes (VirtualBox VMs) using vagrant and installing Docker and Kubeadm packages in cluster nodes.
To create cluster I've firstly writing vagrant script with specificaton and mention ansible playbook location for master and worker nodes location in vagrant script and used following command as well as we can use individual vagrant script to create individual clusetr node and then apply ansible script from ansible machine. here I've mentioned both method. The following commands are used to provision VM using vagrant script. 

$ vagrant init

$ vagrant up

To create cluster here, I use weave CNI pluging for pod network. 

# k8s-metric server: 
When Cluster is ready to use then deploying metric server and Kubernetes dashboard. To create metric server we need a serviceaccount for accessing the cluster resouces and authenticatoin as well as authorization. We need also to create RBAC for the serviceaccount that what can do this serviceaccount in the cluster. For Deployment I'am using a deployment defination yaml file. 

