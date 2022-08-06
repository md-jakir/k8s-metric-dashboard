# Prerquisits to set-up k8s cluster using vagrant: 
- Need to install vagrant in host machine
- Need to install VirtualBox 

# Provisioning VM machine
Provisioning cluster nodes (VirtualBox VMs) using vagrant and installing Docker and Kubeadm packages in cluster nodes.
To create cluster I've firstly writing vagrant script with specificaton and mention ansible playbook location for master and worker nodes location in vagrant script and used following command as well as we can use individual vagrant script to create individual clusetr node and then apply ansible script from ansible machine. here I've mentioned both method. The following commands are used to provision VM using vagrant script. 

$ vagrant init

$ vagrant up

To create cluster here, I use weave CNI pluging for pod network. 

# k8s-metric server: 
When Cluster is ready to use then deploying metric server and Kubernetes dashboard. To create metric server we need a serviceaccount for accessing the cluster resouces and authenticatoin as well as authorization. We need also to create RBAC for the serviceaccount that what can do this serviceaccount in the cluster. For metric server Deployment I'am using a deployment defination yaml file. 

Note: If metric server isn't running for the certificate issue then need to patch using the following command or we can use selfsign certificate for the metric server. 

$ kubectl patch deployment metrics-server -n kube-system --type 'json' -p '[{"op": "add", "path": "/spec/template/spec/containers/0/args/-", "value": "--kubelet-insecure-tls"}]'

# K8s-dashboard deployment: 
Kubernetes dashboard is a web UI for the cluster to see the all workloads running. To deploy dashboard need serviceaccount for dashbaord application as well as admin user as a service account who can login into dashboard and able to see the all namespace workloads running. For cluster admin here, I've created cluster-admin.yml. A nodeport service is creaed for the dashboard so that we can access the dashboard from outside. To access the dashboard need to get the admin user token and it would be get by the following command.

$ kubectl get secret -n kubernetes-dashboard $(kubectl get serviceaccount admin -n kubernetes-dashboard -o jsonpath="{.secrets[0].name}") -o jsonpath="{.data.token}" | base64 --decode

Output token: 
eyJhbGciOiJSUzI1NiIsImtpZCI6Imt4UzV0cjZ3Z19UY0k4YTBSUUEyMUxCR3hMRUpwSF9ndHIweWoyR1BrcEEifQ.eyJpc3MiOiJrdWJlcm5ldGVzL3NlcnZpY2VhY2NvdW50Iiwia3ViZXJuZXRlcy5pby9zZXJ2aWNlYWNjb3VudC9uYW1lc3BhY2UiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VjcmV0Lm5hbWUiOiJrdWJlcm5ldGVzLWRhc2hib2FyZC10b2tlbi1mcm1rbSIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50Lm5hbWUiOiJrdWJlcm5ldGVzLWRhc2hib2FyZCIsImt1YmVybmV0ZXMuaW8vc2VydmljZWFjY291bnQvc2VydmljZS1hY2NvdW50LnVpZCI6IjdjNTMzNmE3LWIzYWEtNDczMy1hODY5LTEzZWZkZTYzMjlmNiIsInN1YiI6InN5c3RlbTpzZXJ2aWNlYWNjb3VudDprdWJlcm5ldGVzLWRhc2hib2FyZDprdWJlcm5ldGVzLWRhc2hib2FyZCJ9.ohn68o1U0rrED4Bdfb9ePVayjcdGpe8ZQqmIux36fVkqRs5Sy3L_SoUMtUHyQwL6ddic2Ubmd4yu768PPFJbatNBjCwu88aM7nkr8B8aETrY1P8we46Gxs4Ptm-qSma1RDz1-trYlU-1JqT2s7IYh6RyVyuOZk-dAdwgo6EhJuLeTU7ERQaXVEwnPjgaLVlJOzVxolquA-AxHO5zjmO-eQYbflLbktFyTZSAhpgD7KAafPnykDNSa-yg2uRZyz3MZApJ1WHUDBD5Hk2kx3zWv62w5hgjEEjZPn8tHCkJ5diBWu866E-fKNZEcE5OtgE3zGW4StiPIzGQJAT17RqIMg









