### <a name="what-client-operating-systems-can-i-use-with-point-to-site"></a>Welke clientbesturingssystemen kan ik met punt-naar-site gebruiken?

Hallo volgende clientbesturingssystemen worden ondersteund:

* Windows 7 (32-bits en 64-bits)
* Windows Server 2008 R2 (alleen 64-bits)
* Windows 8 (32-bits en 64-bits)
* Windows 8.1 (32-bits en 64-bits)
* Windows Server 2012 (alleen 64-bits)
* Windows Server 2012 R2 (alleen 64-bits)
* Windows 10

### <a name="can-i-use-any-software-vpn-client-for-point-to-site-that-supports-sstp"></a>Kan ik voor punt-naar-site elke VPN-softwareclient gebruiken die SSTP ondersteunt?

Nee. Ondersteuning is beperkt alleen toohello Windows besturingssysteemversies die hierboven worden genoemd.

### <a name="how-many-vpn-client-endpoints-can-i-have-in-my-point-to-site-configuration"></a>Hoeveel VPN-clienteindpunten kan mijn punt-naar-site-configuratie hebben?

We bieden ondersteuning voor too128 VPN-clients toobe kunnen tooconnect tooa virtuele netwerk op Hallo dezelfde tijd.

### <a name="can-i-use-my-own-internal-pki-root-ca-for-point-to-site-connectivity"></a>Kan ik mijn eigen interne PKI basis-CA voor een punt-naar-site-verbinding gebruiken?

Ja. Voorheen konen alleen zelfondertekende basiscertificaten worden gebruikt. U kunt nog steeds 20 basiscertificaten uploaden.

### <a name="can-i-traverse-proxies-and-firewalls-using-point-to-site-capability"></a>Kan ik met punt-naar-site-functionaliteit proxy's en firewalls passeren?

Ja. We gebruiken de tootunnel SSTP (Secure Socket Tunneling Protocol) via firewalls. Deze tunnel wordt weergegeven als een HTTPs-verbinding.

### <a name="if-i-restart-a-client-computer-configured-for-point-to-site-will-hello-vpn-automatically-reconnect"></a>Als ik een clientcomputer die is geconfigureerd voor punt-naar-Site opnieuw opstart, wordt hello VPN automatisch opnieuw verbinding maken?

Standaard wordt Hallo-clientcomputer niet hersteld Hallo VPN-verbinding automatisch.

### <a name="does-point-to-site-support-auto-reconnect-and-ddns-on-hello-vpn-clients"></a>Ondersteuning voor punt-naar-Site automatisch verbinding maken en DDNS op Hallo VPN-clients?

Automatisch opnieuw verbinding maken en DDNS worden momenteel niet ondersteund in VPN’s met punt-naar-site-verbinding.

### <a name="can-i-have-site-to-site-and-point-to-site-configurations-coexist-for-hello-same-virtual-network"></a>Kan ik Site-naar-Site en punt-naar-Site-configuraties naast elkaar worden gebruikt voor Hallo hetzelfde virtuele netwerk?

Ja. Beide oplossingen werken als de gateway een op RouteBased-type VPN heeft. Voor het klassieke implementatiemodel hello moet u een dynamische gateway. We doen dat geen ondersteuning voor punt-naar-Site voor statische routering VPN-gateways of gateways met Hallo `-VpnType PolicyBased` cmdlet.

### <a name="can-i-configure-a-point-to-site-client-tooconnect-toomultiple-virtual-networks-at-hello-same-time"></a>Kan ik een punt-naar-Site client tooconnect toomultiple virtuele netwerken configureren op Hallo hetzelfde moment?

Ja, dat is mogelijk. Maar Hallo virtuele netwerken kunnen geen overlappende voorvoegsels van een IP- en Hallo punt-naar-Site-adresruimten niet tussen Hallo virtuele netwerken overlappen elkaar.

### <a name="how-much-throughput-can-i-expect-through-site-to-site-or-point-to-site-connections"></a>Hoeveel doorvoer kan ik verwachten via site-naar-site- of punt-naar-site-verbindingen?

Het is moeilijk toomaintain Hallo exacte doorvoer van Hallo VPN-tunnels. IPSec en SSTP zijn cryptografisch zware VPN-protocollen. Doorvoer wordt ook beperkt door Hallo latentie en bandbreedte tussen uw lokale en Hallo Internet.
