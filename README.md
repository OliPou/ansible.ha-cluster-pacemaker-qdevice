ha-cluster-pacemaker-qdevice
=========

Role for a basic configuring quorum device on pacemaker cluster ( Debian 10).
This role complements the role https://github.com/OndrejHome/ansible.ha-cluster-pacemaker

This role can configure following aspects of pacemaker cluster:
- install needed packages
- create and configure users and groups for running quorum device
- authorize qorum device on each pacemaker nodes
- create or update qorum device cluster configuration (check `allowed_qdevice_changes`)

Requirements
------------
This role depend on role [ondrejhome.pcs-modules-2](https://github.com/OndrejHome/ansible.pcs-modules-2).
You need a cluster fully configured to add your qdevice see : https://github.com/OndrejHome/ansible.ha-cluster-pacemaker.

Role tested on Debian 10.8 with ansible 2.10

Role Variables
--------------

  - user used for authorizing cluster nodes

    ```
    cluster_user: 'hacluster'
    ```

  - password for user used for authorizing cluster nodes

    ```
    cluster_user_pass: 'testtest'
    ```

  - group to which cluster user belongs (should be 'haclient')

    ```
    cluster_group: 'haclient'
    ```

  - enable qdevice on boot on normal

    ```
    cluster_enable_service: true
    ```

  - Whether to add hosts to /etc/hosts. By default an entry for the hostname
    given by `cluster_hostname_fact` is added for each host to `/etc/hosts`.
    This can be disabled by setting `cluster_etc_hosts` to `false`.

    ```
    cluster_etc_hosts: true
    ```

  - To set your quorum device use the value true.

    ```
    cluster_node_is_arbiter: false
    ```

  - Allow update quorum device setting (server qorum device or qdevice_algorithm).

    ```
    qdevice_allowed_change: none
    ```
  - algorithm use by the cluster.

    ```
    qdevice_algorithm: 'ffsplit'
    ```



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: cluster
      roles:
        - ha-cluster-pacemaker-qdevice

      qdevice variable to set:
        qdevice_allowed_change: none
        qdevice_algorithm: 'ffsplit'
        cluster_node_is_arbiter: true
License
-------

GPLv3


Author Information
------------------

To get in touch with author you can create a issue on github when requesting some feature.
