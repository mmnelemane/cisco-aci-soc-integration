<!-- .slide: data-state="section-break" id="aci-openstack" data-timing="10" -->
# ACI-OpenStack integration


<!-- .slide: data-state="normal" id="opflex-ml2-1" data-menu-title="Opflex ML2 Software Architecture" class="aci-openstack" data-timing="40" -->
## OpenStack with ACI and OpFlex ML2

*   <!-- .element: class="fragment" -->
    Typically uses: 
    *   a Nexus 9000 Spine/Leaf topology, 
*   <!-- .element: class="fragment" -->
    *   an APIC cluster and 
*   <!-- .element: class="fragment" -->
    *   a group of servers 
*   <!-- .element: class="fragment" -->
    ML2 uses Opflex as a new network_type
*   <!-- .element: class="fragment" -->
    Can use VXLAN or VLAN encapsulations
*   <!-- .element: class="fragment" -->
    Uses a modified OpenVSwitch package and local software agents on each compute host

<!-- .slide: data-state="normal" id="opflex-ml2-2" data-menu-title="Opflex ML2 Software Architecture" class="aci-openstack" data-timing="40" -->
## OpenStack with ACI and OpFlex ML2

<div class="opflex-openstack">
  <img class="opflex-ml2"
      data-src="images/opflexml2-openstack.jpg"
      alt="OpenStack with ACI architecture with OpFlex ML2" />
</div>

Note:
- The APIC mechanism driver translates Neutron networking elements such as a network, subnet, router or external network into APIC constructs within the ACI Policy Model.
- An OpFlex proxy from the ACI leaf switch exchanges policy information with the Agent-OVS instance in each compute host, effectively extending the ACI switch fabric and policy model into the virtual switch resulting in a cohesive system that can apply networking policy anywhere in the combined virtual and physical switching fabric starting from the virtual port where a VM instance attaches to the network.



<!-- .slide: data-state="normal" id="opflex-agent-1" data-menu-title="Opflex Agent Architecture on Compute" class="aci-openstack" data-timing="40" -->
## Opflex Agent on OpenStack Compute

<div class="opflex-openstack">
  <img class="opflex-ml2"
      data-src="images/opflexml2-openstack.jpg"
      alt="OpenStack with ACI architecture with OpFlex ML2" />
</div>

<!-- .slide: data-state="normal" id="opflex-agent-2" data-menu-title="Opflex Agent Architecture on Compute" class="aci-openstack" data-timing="40" -->
## Opflex Agent on OpenStack Compute

*   <!-- .element: class="fragment" -->
    neutron-opflex-agent receives endpoint information from OpenStack through ML2 driver
*   <!-- .element: class="fragment" -->
    Endpoint files are located at /var/lib/opflex-agent-ovs/endpoints
*   <!-- .element: class="fragment" -->
    Agent-ovs programs the OVS

Note:
- The agent-ovs uses the endpoint information to resolve policy for the endpoints through the OpFlex Proxy on the connected ACI Leaf switch.
- The agent-ovs then programs policy on OVS using Open Flow for policies that can be enforced locally.
- Non-local policies are enforced on the upstream leaf switch.


<!-- .slide: data-state="normal" id="distributed-neutron-1" data-menu-title="Distributed Neutron Services" class="aci-openstack" data-timing="40" -->
## Distributed Neutron Services

*   <!-- .element: class="fragment" -->
    NAT for External Networks
*   <!-- .element: class="fragment" -->
    Layer 3 Forwarding - local traffic for same-tenant instances on the node
*   <!-- .element: class="fragment" -->
    DHCP - Distributed DORA functionality and optimized mode
*   <!-- .element: class="fragment" -->
    Metadata Proxy - option to use distributed or traditional approach 

<!-- .slide: data-state="normal" id="distributed-neutron-2" data-menu-title="Distributed Neutron Services" class="aci-openstack" data-timing="40" -->
## Distributed Neutron Services

<div class="opflex-openstack">
  <img class="distributed-neutron"
      data-src="images/distributed-neutron.jpg"
      alt="Logical OpenStack Network Connectivity with Distributed Neutron Services" />
</div>

Note: 

NAT for External Networks:
- The OpFlex ML2 driver distributes source NAT and Floating IP functions for OpenStack to the OVS of the compute hosts.
- Packets destined for IP addresses not defined in the private OpenStack Tenant space are automatically NATed prior to egressing a compute host. 

L3 Forwarding:
- Neutron L3 Agent is replaced by a combination of L3 forwarding in the ACI Fabric and a local forwarding within a compute node. 

DHCP:
- Allows a Distributed DHCP approach using the agent-ovs, distributing the DHCP function across the compute nodes, and keep DHCP Discovery, Offer, Request and Acknowledge traffic local to the host and ensures reliable allocation of IP addressing to VM instances.
- Central Neutron address management functions communicate DHCP addressing and options to the local agent-ovs over the management network. 

Metadata Proxy:
- OpFlex ML2 allows Nova-Metadata Proxy to be distributed on each compute host. 
- VMs receive instance-specific information (instance-id, hostnames, SSH keys) from Nova Metadata Service and reached through Neutron service acting as a proxy.
