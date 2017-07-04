
TrinityX
========

Welcome to TrinityX!

TrinityX is the new generation of ClusterVision's open-source HPC platform. It is designed from the ground up to provide all services required in a modern HPC system, and to allow full customization of the installation. Also it includes optional modules for specific needs, such as an OpenStack cloud, Docker on the compute nodes and the ability to partition a cluster.

The full documentation is available in the ``doc`` subdirectory.


Quick start
-----------

1. Install CentOS Minimal on your controller(s)

2. Configure network interfaces that will be used in the cluster, e.g public, provisioning and MPI networks

3. Install ``git``::

    # yum install git

4. Clone TrinityX repository into your working directory and go to the configuration directory::

    # git clone http://github.com/clustervision/trinityx
    # cd trinityX/configuration

5. Based on whether you're setting up HA or not, edit a corresponding configuration file:
       
     -     ``controller-nonHA.cfg``
     -     ``controller-HA.cfg``

   or better yet, create a custom configuration file that overrides all the neccessary parameters::

     # vim my.cfg
     #!/bin/bash
     
     . controller-HA.cfg
   
     # Controller network settings
     CTRL1_HOSTNAME=controller1
     CTRL1_IP=192.168.10.254
     
     CTRL2_HOSTNAME=controller2
     CTRL2_IP=192.168.10.253
     
     CTRL_HOSTNAME=controller
     CTRL_IP=192.168.10.252
     
     DOMAIN=cluster
     
     COROSYNC_CTRL1_IP=192.168.50.254
     COROSYNC_CTRL2_IP=192.168.50.253
     
     # Shared FS options
     SHARED_FS_TYPE=drbd
     SHARED_FS_DEVICE=/dev/rootvg/drbd
     
     #Firewalld
     FWD_PUBLIC_IF="eth0"
     FWD_TRUSTED_IF="eth1 eth2"
   
     # Luna network
     LUNA_NETWORK=192.168.10.0
     LUNA_DHCP_RANGE_START=192.168.10.150
     LUNA_DHCP_RANGE_END=192.168.10.200


6. Start TrinityX installation::

    # ./configure.sh <target_configuration_file> |& tee -a install.log
    
7. Create a default compute image::

    # ./configure.sh images-create-compute.cfg |& tee -a image.log


This will set up the controller with the default configuration, then create and set up a compute image.

