### <a name="is-bgp-supported-on-all-azure-vpn-gateway-skus"></a>Wordt BGP ondersteunt op alle Azure VPN-gateway SKU’s?
Nee, BGP wordt ondersteund op de VPN-gateways **Standard** en **HighPerformance** van Azure. SKU **Basic** wordt NIET ondersteund.

### <a name="can-i-use-bgp-with-azure-policy-based-vpn-gateways"></a>Kan ik BGP gebruiken met beleid-gebaseerde VPN-gateways van Azure?
Nee, BGP wordt alleen ondersteund op route-gebaseerde VPN-gateways.

### <a name="can-i-use-private-asns-autonomous-system-numbers"></a>Kan ik persoonlijke ASN's (autonome systeemnummers) gebruiken?
Ja, u kunt uw eigen openbare ASN's of persoonlijke ASN's voor zowel uw on-premises netwerken en virtuele netwerken van Azure gebruiken.

### <a name="are-there-asns-reserved-by-azure"></a>Zijn er ASN's die zijn gereserveerd door Azure?
Ja, hello volgende ASN's zijn gereserveerd door Azure voor zowel interne als externe peerings:

* Openbare ASN’s: 8075, 8076, 12076
* Privé-ASNs: 65515, 65517, 65518, 65519, 65520

U kunt deze ASN's voor uw on-premises VPN-apparaten opgeven bij het verbinden van tooAzure VPN-gateways.

### <a name="are-there-any-other-asns-that-i-cant-use"></a>Zijn er andere ASN's die ik niet kan gebruiken?
Ja, Hallo na ASN's zijn [gereserveerd door de IANA](http://www.iana.org/assignments/iana-as-numbers-special-registry/iana-as-numbers-special-registry.xhtml) en kan niet worden geconfigureerd op uw Azure VPN-Gateway:

23456, 64496-64511, 65535-65551 en 429496729

### <a name="can-i-use-hello-same-asn-for-both-on-premises-vpn-networks-and-azure-vnets"></a>Kan ik hello gebruiken hetzelfde ASN worden gebruikt voor zowel on-premises VPN-netwerken en Azure VNets?
Nee, u moet verschillende ASN’s toewijzen aan uw on-premises netwerken en uw Azure Vnets als u ze beide verbindt met BGP. Aan Azure VPN-gateways wordt standaard een ASN van 65515 toegewezen, onafhankelijk van of BGP is ingeschakeld voor verbinding tussen gebouwen. U kunt deze standaardwaarde onderdrukken door een andere ASN toe te wijzen bij het maken van Hallo VPN-gateway of Hallo ASN niet wijzigen nadat het Hallo-gateway is gemaakt. U moet tooassign uw lokale ASN's toohello overeenkomt lokale netwerkgateways van Azure.

### <a name="what-address-prefixes-will-azure-vpn-gateways-advertise-toome"></a>Welk adres prefixes wordt Azure VPN-gateways adverteren toome?
Azure VPN-gateway maakt bekend Hallo routes tooyour on-premises BGP-apparaten te volgen:

* Uw VNet-adresvoorvoegsels
* Adresvoorvoegsels voor elke lokale netwerkgateways verbonden toohello Azure VPN-gateway
* Routes die afkomstig zijn van andere BGP peering sessies verbonden toohello Azure VPN-gateway, **behalve standaardroutes of routes die overlappen met een VNet-voorvoegsel**.

### <a name="can-i-advertise-default-route-00000-tooazure-vpn-gateways"></a>Kan ik adverteren standaard route (0.0.0.0/0) tooAzure VPN-gateways?
Ja.

Houd er rekening mee dit forceert alle VNet uitgaande verkeer naar uw on-premises site en wordt voorkomen dat Hallo VNet VMs accepteert openbare communicatie van Hallo Internet rechtstreeks dergelijke RDP of SSH uit Hallo Internet toohello virtuele machines.

### <a name="can-i-advertise-hello-exact-prefixes-as-my-virtual-network-prefixes"></a>Kan ik Hallo exacte voorvoegsels adverteren als mijn virtuele netwerk voorvoegsels

Nee, reclame Hallo dezelfde prefixes, als een van uw virtuele netwerk-adresvoorvoegsels worden geblokkeerd of gefilterd op Hallo Azure-platform. U kunt echter een voorvoegsel aankondigen dat een superset is van wat u in Virtual Network hebt. 

Als het virtuele netwerk Hallo adresruimte 10.0.0.0/16 gebruikt, kan u bijvoorbeeld 10.0.0.0/8 adverteren. U kunt echter niet 10.0.0.0/16 of 10.0.0.0/24 adverteren.

### <a name="can-i-use-bgp-with-my-vnet-to-vnet-connections"></a>Kan ik BGP in combinatie met mijn VNet-naar-VNet-verbindingen gebruiken?
Ja, u kunt BGP zowel gebruiken voor verbindingen tussen gebouwen als voor VNet-naar-VNet-verbindingen.

### <a name="can-i-mix-bgp-with-non-bgp-connections-for-my-azure-vpn-gateways"></a>Kan ik BGP combineren met niet-BGP-verbindingen voor mijn Azure VPN-gateways?
Ja, u kunt zowel BGP combineren en niet-BGP-verbindingen voor Hallo dezelfde Azure VPN-gateway.

### <a name="does-azure-vpn-gateway-support-bgp-transit-routing"></a>Biedt Azure VPN-gateway ondersteuning voor BGP-transitroutering?
Ja, BGP-transitroutering wordt ondersteund, met uitzondering van Hallo dat Azure VPN-gateways worden **niet** adverteren standaard routeert tooother BGP-peers. tooenable onderweg routeren tussen meerdere Azure VPN-gateways, moet u BGP op alle tussenliggende VNet-naar-VNet-verbindingen inschakelen.

### <a name="can-i-have-more-than-one-tunnel-between-azure-vpn-gateway-and-my-on-premises-network"></a>Kan ik meer dan één tunnel aanbrengen tussen een Azure VPN-gateway en mijn on-premises netwerk?
Ja, u kunt meer dan één S2S-VPN-tunnel aanbrengen tussen een Azure VPN-gateway en uw on-premises netwerk. Houd er rekening mee dat deze tunnels van Hallo totaalaantal tunnels voor uw Azure VPN-gateways uitmaken deel en u BGP op beide tunnels inschakelen moet.

Als u twee redundante tunnels tussen uw Azure VPN-gateway en een van uw on-premises netwerken hebt, gebruiken ze bijvoorbeeld 2 tunnels van het totaalaantal voor uw Azure VPN-gateway (10 voor Standard) en 30 voor HighPerformance Hallo.

### <a name="can-i-have-multiple-tunnels-between-two-azure-vnets-with-bgp"></a>Kan ik meerdere tunnels tussen twee Azure VNets met BGP hebben?
Ja, maar minstens één van de virtuele netwerkgateways Hallo moet actief / actief-configuratie.

### <a name="can-i-use-bgp-for-s2s-vpn-in-an-expressroutes2s-vpn-co-existence-configuration"></a>Kan ik BGP gebruiken voor S2S-VPN in een configuratie waarin zowel ExpressRoute als S2S-VPN wordt gebruikt?
Ja. 

### <a name="what-address-does-azure-vpn-gateway-use-for-bgp-peer-ip"></a>Welk adres gebruikt Azure VPN-gateway voor BGP-peer-IP?
Hello Azure VPN-gateway wijst één IP-adres toe uit Hallo GatewaySubnet bereik dat is gedefinieerd voor het virtuele netwerk Hallo. Standaard is deze Hallo na-laatste adres van Hallo bereik. Bijvoorbeeld, als uw GatewaySubnet 10.12.255.0/27, variërend van 10.12.255.0 too10.12.255.31, Hallo BGP-Peer-IP-adres op Hallo Azure VPN-gateway 10.12.255.30 zijn. U vindt deze informatie wanneer u hello Azure VPN-gatewaygegevens weer te geven.

### <a name="what-are-hello-requirements-for-hello-bgp-peer-ip-addresses-on-my-vpn-device"></a>Wat zijn de vereisten Hallo voor Hallo BGP-Peer-IP-adressen op Mijn VPN-apparaat?
Het adres van uw lokale BGP-peer **moet niet** worden dezelfde Hallo Hallo openbare IP-adres van uw VPN-apparaat. Gebruik een ander IP-adres op Hallo VPN-apparaat voor uw BGP-Peer-IP. Het kan een adres toegewezen toohello loopback-interface op Hallo apparaat zijn. Specificeer dit adres in Hallo bijbehorende lokale netwerkgateway die Hallo locatie.

### <a name="what-should-i-specify-as-my-address-prefixes-for-hello-local-network-gateway-when-i-use-bgp"></a>Wat moet ik opgeven als mijn adresvoorvoegsels voor Hallo lokale netwerkgateway wanneer ik BGP gebruik?
Azure Local Network Gateway geeft Hallo eerste adresvoorvoegsels voor Hallo on-premises netwerk. Bij BGP moet u toewijzen Hallo hostvoorvoegsel (/ 32-voorvoegsel) van uw BGP-Peer-IP-adres als de adresruimte Hallo voor dat on-premises netwerk. Als uw BGP-Peer-IP-adres 10.52.255.254 is, moet u "10.52.255.254/32" als lokale netwerkadresruimte Hallo Hallo lokale netwerkgateway voor dit on-premises netwerk. Dit is tooensure die hello Azure VPN gateway vaststelt Hallo BGP-sessie via Hallo S2S VPN-tunnel.

### <a name="what-should-i-add-toomy-on-premises-vpn-device-for-hello-bgp-peering-session"></a>Wat moet ik toomy on-premises VPN-apparaat toevoegen voor Hallo BGP-peeringsessie?
U moet een hostroute van hello Azure BGP-Peer-IP-adres toevoegen op het VPN-apparaat toohello IPsec S2S VPN-tunnel aan te wijzen. Als Azure VPN-Peer-IP-Hallo "10.12.255.30" is, moet u een hostroute voor "10.12.255.30" met een nexthop-interface van de overeenkomende IPsec-tunnelinterface Hallo toevoegen op het VPN-apparaat.

