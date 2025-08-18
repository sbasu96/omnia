============================
Troubleshooting guide
============================

Connecting to ``mysqldb`` container
===================================

    * Start a bash session within the mysqldb pod using the ``podman exec -it mysqldb bash`` command.
    * Connect to mysql using the ``mysql -u <mysqldb_username> -p`` command and provide password when prompted.
    * Connect to database using the ``USE idrac_telemetrydb`` command.


Checking and updating encrypted parameters
=============================================

1. Move to the file path where the parameters are saved (as an example, we will be using ``omnia_config_credentials.yml``): ::

        cd /input

2. To view the encrypted parameters: ::

        ansible-vault view omnia_config_credentials.yml --vault-password-file .omnia_config_credentials_key


3. To edit the encrypted parameters: ::

        ansible-vault edit omnia_config_credentials.yml --vault-password-file .omnia_config_credentials_key


Checking podman container status from the OIM
===============================================
   
   * Use this command to get a list of all running podman conatiners: ``podman ps``
   * Check the status of any specific podman conatiner: ``podman ps -f name=<container_name>``


Troubleshooting task failures during ``omnia.yml`` playbook execution
========================================================================

If any task fails for a host listed in the inventory during the execution of the ``omnia.yml`` playbook, it can cause a cascading effect, resulting in the failure of subsequent tasks in the playbook.

**Resolution**: In such cases, you should begin troubleshooting from the initial point of failure — the first task that encountered an error.

Troubleshooting CoreDNS pod in pending state
========================================================================

When you run the omnia.yml, scheduler.yml, or service_k8s_cluster.yml files, sometimes one of the CoreDNS pods remains in the pending state after the Kubernetes installation. This issue is caused by the dns-autoscaler adjusting the CoreDNS replica counts based on the total number of CPU cores across all the cluster nodes. In some environments, this scaling calculation can lead to an unsupported replica count, resulting in pending pods.

**Resolution**: Do the following:
        1. Retrieve all the deployments using the following command: 
        ::
                kubectl get deployments -A
        2. Delete the dns-autoscaler deployment: 
        ::
                kubectl delete deployment dns-autoscaler -n kube-system
        3. Identify and edit the CoreDNS deployment name from the list of deployments retrieved in step 1: 
        ::
                kubectl edit deployment <coredns-deployment-name> -n kube-system:
                
                    1. Locate the 'replicas' field in the editor and change the value from 3 to 2.
                    2. Save the changes. Kubernetes automatically restarts the CoreDNS deployment.
        4. Wait a few minutes for the pods to restart and verify the CoreDNS status: 
        ::
                kubectl get pods -A
         Ensure that two CoreDNS pods are in the 'Running' state.
