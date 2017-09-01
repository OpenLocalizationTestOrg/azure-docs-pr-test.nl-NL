De veelgestelde vragen voor VNet-naar-VNet zijn van toepassing op VPN Gateway-verbindingen. Zie [Peering op virtueel netwerk](../articles/virtual-network/virtual-network-peering-overview.md) voor VNet-peering

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Worden er door Azure kosten in rekening gebracht voor verkeer tussen VNets?

VNet-naar-VNet-verkeer binnen dezelfde regio is gratis in beide richtingen wanneer u een VPN Gateway-verbinding gebruikt. Voor uitgaand VNet-naar-VNet-verkeer tussen regio's gelden de tarieven voor uitgaande gegevensoverdracht tussen VNets op basis van de bronregio's. Raadpleeg de [pagina met VPN Gateway-prijzen](https://azure.microsoft.com/pricing/details/vpn-gateway/) voor meer informatie. Zie de [pagina met prijzen voor virtuele netwerken](https://azure.microsoft.com/pricing/details/virtual-network/) als u uw VNets verbindt op basis van VNet-peering in plaats van VPN Gateway.

### <a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a>Verloopt VNet-naar-VNet-verkeer via internet?

Nee. Voor VNet-naar-VNet-verkeer wordt het Microsoft-netwerk gebruikt in plaats van internet.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Is het VNet-naar-VNet-verkeer beveiligd?

Ja, het is beveiligd met IPsec/IKE-versleuteling.

### <a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a>Heb ik een VPN-apparaat nodig om VNets met elkaar te verbinden?

Nee. Om meerdere virtuele netwerken van Azure met elkaar te verbinden, hebt u geen VPN-apparaat nodig, tenzij cross-premises connectiviteit is vereist.

### <a name="do-my-vnets-need-to-be-in-the-same-region"></a>Moeten mijn VNets zich in dezelfde regio bevinden?

Nee. De virtuele netwerken kunnen zich in dezelfde of verschillende Azure-regio's (locaties) bevinden.

### <a name="if-the-vnets-are-not-in-the-same-subscription-do-the-subscriptions-need-to-be-associated-with-the-same-ad-tenant"></a>Als de VNets niet tot hetzelfde abonnement behoren, moeten de abonnementen dan aan dezelfde AD-tenant zijn gekoppeld?

Nee.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Kan ik VNet-naar-VNet- én multi-site-verbindingen gebruiken?

Ja. U kunt virtuele-netwerkverbindingen tegelijk gebruiken met multi-site-VPN’s.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Met hoeveel on-premises sites en virtuele netwerken kan één virtueel netwerk verbinding maken?

Zie de tabel [Gatewayvereisten](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a>Kan ik VNet-naar-VNet gebruiken om virtuele machines of cloudservices met elkaar te verbinden buiten een VNet?

Nee. VNet naar VNet ondersteunt het verbinden van virtuele netwerken. Er is geen ondersteuning voor het verbinden van virtuele machines of cloudservices die geen deel uitmaken van een virtueel netwerk.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Kan een cloudservice of een taakverdelingseindpunt VNets overbruggen?

Nee. Een cloudservice of een taakverdelingseindpunt kan geen virtuele netwerken overbruggen, zelfs niet als ze met elkaar zijn verbonden.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Kan ik een op beleid gebaseerd VPN-type gebruiken voor VNet-naar-VNet- of multi-site-verbindingen?

Nee. VNet-naar-VNet- en multi-site-verbindingen vereisen Azure VPN-gateways met op route gebaseerde VPN-typen (voorheen dynamische routering genoemd).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a>Kan ik een VNet met een op route gebaseerd VPN-type verbinden met een op beleid gebaseerd VPN-type?

Nee, voor beide virtuele netwerken MOET gebruik worden gemaakt van op route gebaseerde VPN's (voorheen dynamische routering genoemd).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Delen VPN-tunnels bandbreedte?

Ja. Alle VPN-tunnels van het virtuele netwerk delen de beschikbare bandbreedte op de Azure VPN-gateway en dezelfde SLA voor VPN-gatewaybedrijfstijd in Azure.

### <a name="are-redundant-tunnels-supported"></a>Worden redundante tunnels ondersteund?

Redundante tunnels tussen twee virtuele netwerken worden ondersteund, mits één virtuele-netwerkgateway is geconfigureerd als actief-actief.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Mogen er overlappende adresruimten zijn voor VNet-naar-VNet-configuraties?

Nee. Er mag geen sprake zijn van overlappende IP-adresbereiken.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Mogen er overlappende adresruimten zijn tussen de verbonden virtuele netwerken en on-premises lokale sites?

Nee. Er mag geen sprake zijn van overlappende IP-adresbereiken.



