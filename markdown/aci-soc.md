<!-- .slide: data-state="section-break" id="aci-soc" data-timing="10" -->
# ACI Integration with Suse OpenStack Cloud


<!-- .slide: data-state="normal" id="aci-pod-diagram" data-menu-title="ACI POD for SOC" class="aci-soc" data-timing="40" -->
## ACI POD Structure

<figure>
    <img alt="ACI Lab Network Diagram"
        data-src="images/aci-soc.jpg" style="display: flex; justify-content: center; width: 65%;height: 55%;margin-left: 20px;margin-bottom: 80px;" />
</figure>

Note:
- Two Cisco ACI Leafs, 1 admin node, 1 control node, 2 compute nodes
- Control node should be manually assigned an IP to be able to communicate with the Cisco APIC.\
- For the lab the IP is in the range of 10.105.1.110-10.105.1.119


<!-- .slide: data-state="normal" id="aci-soc-steps" data-menu-title="ACI SOC Integration Steps" class="aci-soc" data-timing="40" -->
## ACI Fabric

*   <!-- .element: class="fragment" -->
    Install SUSE OpenStack Cloud until and not including the Neutron barclamp
*   <!-- .element: class="fragment" -->
    Download the special Openvswitch packages and create repo from Admin node
*   <!-- .element: class="fragment" -->
    Install OpenVswitch packages on all nodes and lock them and start ovs service
*   <!-- .element: class="fragment" -->
    On each compute node (From Yast2):
    **   <!-- .element: class="fragment" -->
         - Setup ethernet device to be connected to the fabric
    **   <!-- .element: class="fragment" -->
         - Create and Configure VLAN on the device
    **   <!-- .element: class="fragment" -->
         - Create Routing for the VLAN
    **   <!-- .element: class="fragment" -->
         - Enable DHCP and set MTU to 1600
    **   <!-- .element: class="fragment" -->
         - Create a tunnel bridge with VXLAN
    **   <!-- .element: class="fragment" -->
         - Note the interface name from the lldpctl results (look for PortDescr: field)
*   <!-- .element: class="fragment" -->
    Fill up the necessary paramaters for ACI on the Crowbar UI (network_type, ml2_driver, IPs, user/password etc)
*   <!-- .element: class="fragment" -->
    Apply the neutron barclamp and go ahead with nova, horizon or other necessary barclamps.
    
