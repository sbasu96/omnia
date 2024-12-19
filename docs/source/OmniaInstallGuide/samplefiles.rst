Sample Files
=============

inventory file
-----------------

.. caution:: All the file contents mentioned below are case sensitive.

::

        #Batch Scheduler: Slurm

        [slurm_control_node]

        10.5.1.101

        [slurm_node]

        10.5.1.103

        10.5.1.104

        [login]

        10.5.1.105



        #General Cluster authentication server

        [auth_server]

        10.5.1.106

        #AI Scheduler: Kubernetes

        [kube_control_plane]

        10.5.1.101

        [etcd]

        10.5.1.101

        [kube_node]

        10.5.1.102

        10.5.1.103

        10.5.1.104

        10.5.1.105

        10.5.1.106

.. note::

            * For Slurm, all the applicable inventory groups are ``slurm_control_node``, ``slurm_node``, and ``login``.
            * For Kubernetes, all the applicable groups are ``kube_control_plane``, ``kube_node``, and ``etcd``.
            * The centralized authentication server inventory group, that is ``auth_server``, is common for both Slurm and Kubernetes.
            * For secure login node functionality, ensure to add the ``login`` group in the provided inventory file.

software_config.json for Ubuntu
---------------------------------

::

    {
        "cluster_os_type": "ubuntu",
        "cluster_os_version": "22.04",
        "repo_config": "partial",
        "softwares": [
            {"name": "amdgpu", "version": "6.2.2"},
            {"name": "cuda", "version": "12.3.2"},
            {"name": "bcm_roce", "version": "230.2.54.0"},
            {"name": "ofed", "version": "24.01-0.3.3.1"},
            {"name": "openldap"},
            {"name": "secure_login_node"},
            {"name": "nfs"},
            {"name": "beegfs", "version": "7.4.2"},
            {"name": "k8s", "version":"1.29.5"},
            {"name": "roce_plugin"},
            {"name": "jupyter"},
            {"name": "kubeflow"},
            {"name": "kserve"},
            {"name": "pytorch"},
            {"name": "tensorflow"},
            {"name": "vllm"},
            {"name": "telemetry"},
            {"name": "ucx", "version": "1.15.0"},
            {"name": "openmpi", "version": "4.1.6"},
            {"name": "intelgaudi", "version": "1.18.0-524"},
            {"name": "csi_driver_powerscale", "version":"v2.11.0"}
        ],

        "bcm_roce": [
            {"name": "bcm_roce_libraries", "version": "230.2.54.0"}
        ],
        "amdgpu": [
            {"name": "rocm", "version": "6.2.2" }
        ],
        "intelgaudi": [
            {"name": "intel"}
        ],
        "vllm": [
            {"name": "vllm_amd"},
            {"name": "vllm_nvidia"}
        ],
        "pytorch": [
            {"name": "pytorch_cpu"},
            {"name": "pytorch_amd"},
            {"name": "pytorch_nvidia"},
            {"name": "pytorch_gaudi"}
        ],
        "tensorflow": [
            {"name": "tensorflow_cpu"},
            {"name": "tensorflow_amd"},
            {"name": "tensorflow_nvidia"}
        ]
    }

software_config.json for RHEL/Rocky Linux
-------------------------------------------

.. note:: For Rocky Linux OS, the ``cluster_os_type`` in the below sample will be ``rocky``.

::

        {
            "cluster_os_type": "rhel",
            "cluster_os_version": "8.8",
            "repo_config": "partial",
            "softwares": [
                {"name": "amdgpu", "version": "6.2.2"},
                {"name": "cuda", "version": "12.3.2"},
                {"name": "ofed", "version": "24.01-0.3.3.1"},
                {"name": "freeipa"},
                {"name": "openldap"},
                {"name": "secure_login_node"},
                {"name": "nfs"},
                {"name": "beegfs", "version": "7.4.2"},
                {"name": "slurm"},
                {"name": "k8s", "version":"1.29.5"},
                {"name": "jupyter"},
                {"name": "kubeflow"},
                {"name": "kserve"},
                {"name": "pytorch"},
                {"name": "tensorflow"},
                {"name": "vllm"},
                {"name": "telemetry"},
                {"name": "intel_benchmarks", "version": "2024.1.0"},
                {"name": "amd_benchmarks"},
                {"name": "utils"},
                {"name": "ucx", "version": "1.15.0"},
                {"name": "openmpi", "version": "4.1.6"},
                {"name": "csi_driver_powerscale", "version":"v2.11.0"}
            ],

            "amdgpu": [
                {"name": "rocm", "version": "6.2.2" }
            ],
            "vllm": [
                {"name": "vllm_amd"},
                {"name": "vllm_nvidia"}
            ],
            "pytorch": [
                {"name": "pytorch_cpu"},
                {"name": "pytorch_amd"},
                {"name": "pytorch_nvidia"}
            ],
            "tensorflow": [
                {"name": "tensorflow_cpu"},
                {"name": "tensorflow_amd"},
                {"name": "tensorflow_nvidia"}
            ]

        }

inventory file for additional NIC and Kernel parameter configuration
-------------------------------------------------------------------------

.. note:: You can use either or combine node IP, service tags, or hostname in the below inventory file.

Choose fom any of the templates provided below:

::

    #---------Template1---------

    [cluster1]
    10.5.0.1
    10.5.0.2

    [cluster1:vars]
    Categories=category-1

    #---------Template2---------

    [cluster2]
    10.5.0.5 Categories=category-4
    10.5.0.6 Categories=category-5

    #---------Template3---------

    10.5.0.3 Categories=category-2
    10.5.0.4 Categories=category-3


inventory file to delete node from the cluster
-------------------------------------------------

::

    [nodes]
    10.5.0.33

pxe_mapping_file.csv
------------------------------------

::

    SERVICE_TAG,HOSTNAME,ADMIN_MAC,ADMIN_IP,BMC_IP
    XXXXXXX,n1,xx:yy:zz:aa:bb:cc,10.5.0.101,10.3.0.101
    XXXXXXX,n2,aa:bb:cc:dd:ee:ff,10.5.0.102,10.3.0.102


switch_inventory
------------------
::

    10.3.0.101
    10.3.0.102


powervault_inventory
------------------
::

    10.3.0.105




NFS Server inventory file
-------------------------


::

    #General Cluster Storage
    #NFS node
    [nfs]
    #node10


Inventory for iDRAC telemetry
------------------------------

::

    [idrac]
    10.10.0.1

.. note:: Only iDRAC/BMC IPs should be provided.

