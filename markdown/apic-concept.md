<!-- .slide: data-state="section-break" id="apic-concept" data-timing="10" -->
# ACI - Application Centric Infrastructure


<!-- .slide: data-state="normal" id="aci-overview" data-menu-title="APIC-ACI" class="aci" data-timing="40" -->
## ACI - APIC interaction

*   <!-- .element: class="fragment" -->
    Allows requirements to define network
*   <!-- .element: class="fragment" -->
    The APIC manages the ACI multi-tenant fabric

<figure>
    <img alt="Application Requirements Define the network"
        data-src="images/aci-overview.jpg" style="width: 68%; height: 60%; display: flex; justify-content: center;" />
</figure>


<!-- .slide: data-state="normal" id="aci-fabric-1" data-menu-title="ACI Fabric" class="aci" data-timing="40" -->
## ACI Fabric

<figure>
    <img alt="ACI Fabric Overview"
        data-src="images/aci-fabric.jpg" 
    />
</figure>


<!-- .slide: data-state="normal" id="aci-fabric-2" data-menu-title="ACI Fabric" class="aci" data-timing="40" -->
## ACI Fabric

*   <!-- .element: class="fragment" -->
    Includes Cisco Nexus 9000 Series modular switches, APIC host.
*   <!-- .element: class="fragment" -->
    Run in Leaf/Spine ACI fabric mode.
*   <!-- .element: class="fragment" -->
    Consistent low-latency forwarding across high BW links (40 GB - 100 GB)
*   <!-- .element: class="fragment" -->
    Uses 2 hops for cross-leaf
*   <!-- .element: class="fragment" -->
    Uses an Object-Oriented Operating System


<!-- .slide: data-state="normal" id="aci-topology" data-menu-title="ACI Physical Topology" class="aci" data-timing="40" -->
## ACI Physical Topology

<figure>
    <img alt="ACI Physical Topology"
        data-src="images/physical-topology.jpg" style="width: 68%; height: 60%; display: flex; justify-content: center;" />
</figure>

Note:

* These switches form a "fat-tree" network by connecting each leaf node to each spine node; all other devices connect to the leaf nodes. 
* The APIC manages the ACI fabric. The recommended minimum configuration is a cluster of 3 replicated hosts. 
* The APIC management functions do not operate on the datapath of the fabric.

* NX-OS is an Object Oriented OS.

* The OS renders policies from the APIC into a concrete model that runs in the physical infrastructure. 
* The concrete model is analogous to compiled software; it is the form of the model that the switch operating system can execute. 
* All the switch nodes contain a complete copy of the concrete model. 
* When an administrator creates a policy in the APIC that represents a configration, the APIC updates the logical model. 
* The APIC then performs the intermediate step of creating a fully elaborated policy that it pushes into all the switch nodes where the concrete model is updated.


<!-- .slide: data-state="normal" id="apic-ui" data-menu-title="APIC Controller Interface" class="aci" data-timing="40" -->
## APIC Controller UI

<figure>
    <img alt="APIC Controller Screen"
        data-src="images/APIC-controller.jpg" style="width: 68%; height: 60%; display: flex; justify-content: center;" />
</figure>


<!-- .slide: data-state="normal" id="aci-policy-model-1" data-menu-title="ACI Policy Model" class="aci" data-timing="40" -->
## ACI Policy Model

<figure>>
    <img alt="ACI Policy Model"
        data-src="images/aci-policy-model.jpg"
/>
</figure>


<!-- .slide: data-state="normal" id="aci-policy-model-2" data-menu-title="ACI Policy Model" class="aci" data-timing="40" -->
## ACI Policy Model

*   <!-- .element: class="fragment" -->
    Specifies application requirements policies
*   <!-- .element: class="fragment" -->
    Model-driven framework
*   <!-- .element: class="fragment" -->
    Each unit is a Managed Object (MO)
*   <!-- .element: class="fragment" -->
    Grouping on the basis of tenants
*   <!-- .element: class="fragment" -->
    VRF and BD provide private network
 

Note:

Model-Driven :
* User initiates change on a fabric object
* APIC applies the change to policy model
* The model change then triggers change in the managed endpoint

* The logical configurations are rendered into concrete configurations by applying the policies in relation to the available physical resources.
* The system prohibits communications with new devices until the policy model is updated to include the new device.
* Admins only need to configure logical configurations and APIC policies 

* VRF defines L3 address domain
* One or more Bridge domains are associated with a VRF
* Application profiles defines policies, services and relationships between EPGs (service endpoints)
* EPG is a collection of endpoints decoupled from physical and logical topology
* Tenant network policies are configured separately from fabric access policies
* Bridge domain represents a L2 forwarding construct within the fabric
* BD is linked with VRF and have at least one subnet can be operated in flood mode or optimized mode

