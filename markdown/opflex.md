<!-- .slide: data-state="section-break" id="opflex" data-timing="10" -->
## Opflex - Control Protocol

* A Policy-driven system to control a large set of physical and virtual devices.
* It works on the basis of a common Model understood by the controller and the agents which communicate with the policy elements.
* The APIC uses JSON-RPC over TCP

Note:
 The model is used by Cloud and SDN Controllers to transform objects in OpenStack to policy-driven network object structures. The APIC driver plugin (ML2) translates policy from OpenStack networks into ACI policies. The GBP plugin transforms OpenStack in itself to adopt a policy driven network object structure that equates the ACI application policies.


<!-- .slide: data-state="normal" id="opflex-model" data-menu-title="Opflex" class="opflex" data-timing="40" -->
## Opflex Model

<figure>
    <img alt="Opflex with OpenDayLight and OpenVswitch"
        data_src="images/opflex-model.jpg" />
</figure>
