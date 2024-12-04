.. _ovn-bgp-agent:

=============
OVN BGP Agent
=============

The OVN BGP Agent allows to expose VMs/Containers through BGP on OVN :

* Expose VMs with FIPs or on Provider Networks through BGP on OVN environments
* Expose VMs on Tenant Networks through EVPN on OVN environments.

Enabling OVN BGP Agent
======================

Enable the ovn-bgp-agent service in ``globals.yml``:

.. code-block:: yaml

   enable_ovn_bgp_agent: "yes"

OVN BGP Agent Configuration
===========================

Available configuration options and for the OVN BGP Agent are:

.. code-block:: yaml

   ovn_bgp_agent_logging_debug: "{{ openstack_logging_debug }}"
   # We only provide an example here, this should be configured through host based file overrides
   bgp_loopback_ip: "10.1.2.60"
   bgp_loopback_interface: "lo"
   bgp_local_asn: "64999"
   ovn_bgp_agent_driver: "nb_ovn_bgp_driver"
   ovn_bgp_agent_exposing_method: "underlay"

The ovn-bgp-agent is deploy by default on all computes and network nodes.

OVN BGP Agent Configuration Examples
====================================

You should read the doc and choose the correct **ovn_bgp_agent_driver**
and **ovn_bgp_agent_exposing_method**,
based on the use case you want to implement.

The docs are available here:
`ovn-bgp-agent documentation <https://docs.openstack.org/ovn-bgp-agent/latest/>`_

If you want to add more configuration option to the default bgp-agent.conf
for example the **expose_tenant_networks** or
**expose_ipv6_gua_tenant_networks**
you can use
`Service Configuration <https://docs.openstack.org/kolla-ansible/latest/admin/advanced-configuration.html#openstack-service-configuration-in-kolla>`_.

For example create a file named **bgp-agent.conf**
in /etc/config/kolla/bgp-agent.conf:

.. code-block:: ini

   [DEFAULT]
   expose_tenant_networks = True
   expose_ipv6_gua_tenant_networks = True
