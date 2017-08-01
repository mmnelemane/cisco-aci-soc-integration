<!-- .slide: data-state="section-break" id="neutron-services" data-timing="10" -->
# Distributed Neutron Services

Note:
 - A deepdive into each Distributed service offered by ACI OpFlex Architecture.


<!-- .slide: data-state="normal" id="nat-external-routing" data-menu-title="NAT and External Routing" class="optimized-services" data-timing="40" -->
## OVS NAT and External Routing

<figure>
    <img alt="Opflex Local OVS NAT Subnet Architecture"
        data-src="images/nat-extrouting.jpg" style="display: flex; justify-content: center; width: 65%;height: 55%;margin-left: 20px;margin-bottom: 80px;" />
</figure>

Note:
- Three distinct IP subnets are required for NAT - Link Subnet, Source-NAT Subnet and FloatingIP-Subnet.
- ACI Fabric need only take care of external routing since NAT function itself is local to the compute host.
- VRF(Virtual Routing Forwarding) instance has 
   - an interface to physical link to the external next-hop router
   - an interface with an IP from FloatingIP-Subnet and SNAT-Subnet.
   - a loopback interface for routing protocol interaction.


<!-- .slide: data-state="normal" id="opflex-dhcp" data-menu-title="OpFlex DHCP Service" class="optimized-services" data-timing="40" -->
## Optimized DHCP Services

<figure>
    <img alt="OpFlex based DHCP Architecture"
        data-src="images/optimized-dhcp.jpg" style="display: flex; justify-content: center; width: 65%;height: 55%;margin-left: 20px;margin-bottom: 80px;" />
</figure>

Note:
- The distributed services communicate over the Management network to the Neutron server for allocation of IP Addressing and DHCP options.


<!-- .slide: data-state="normal" id="opflex-metadata" data-menu-title="OpFlex Metadata Proxy" class="optimized-services" data-timing="40" -->
## Optimized Metadata Services

<figure>
    <img alt="OpFlex based Metadata Proxy Architecture"
        data-src="images/optimized-metadata.jpg" style="display: flex; justify-content: center; width: 65%;height: 55%;margin-left: 20px;margin-bottom: 80px;" />
</figure>

Note:
- The agent-ovs service reads the OpFlex service file and programs a flow in OVS to direct Metadata service requests to the local neutron-metadata-agent. 
- The local agent runs in a separate Linux namespace on the compute host.
- The Metadata Proxy function accesses Nova-API and Nova Metadata Service on the controller over the Management network to deliver VM-specific metadata to each VM instance.
