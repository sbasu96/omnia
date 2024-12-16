Ubuntu
======

========== ============= =============
OS Version Control Plane Cluster Nodes
========== ============= =============
22.04        Yes            Yes
24.04        Yes            Yes
========== ============= =============

.. note::
    * Omnia supports only the "server install image" version of Ubuntu on the control plane and the cluster nodes.
    * Omnia does not currently support Slurm on Ubuntu.
    * FreeIPA server is not provided in the default Ubuntu repositories. OpenLDAP is provided as an alternative.
    * PowerVault storage devices are not compatible with the Ubuntu operating system. As a result, Omnia running on Ubuntu clusters does not support the configuration of PowerVault storage devices.