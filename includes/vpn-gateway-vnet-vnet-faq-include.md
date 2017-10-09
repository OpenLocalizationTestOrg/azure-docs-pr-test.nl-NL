Hallo Veelgestelde vragen over VNet-naar-VNet is van toepassing tooVPN gatewayverbindingen. Zie [Peering op virtueel netwerk](../articles/virtual-network/virtual-network-peering-overview.md) voor VNet-peering

### <a name="does-azure-charge-for-traffic-between-vnets"></a>Worden er door Azure kosten in rekening gebracht voor verkeer tussen VNets?

VNet-naar-VNet-verkeer binnen Hallo dezelfde regio is gratis voor beide richtingen wanneer u een VPN-gatewayverbinding. Cross-regio VNet-naar-VNet uitgaande verkeer wordt in rekening gebracht met Hallo uitgaande inter-VNet tarieven voor gegevensoverdracht op basis van regio's Hallo-bron. Raadpleeg toohello [VPN-Gateway pagina met prijzen](https://azure.microsoft.com/pricing/details/vpn-gateway/) voor meer informatie. Als u verbinding van uw vnet's met behulp van de VNet-Peering, in plaats van VPN-Gateway maakt, Zie Hallo [virtueel netwerk pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a>VNet-naar-VNet-verkeer passeren Hallo Internet?

Nee. VNet-naar-VNet-verkeer via Hallo Microsoft Azure-backbone niet Hallo Internet wordt verzonden.

### <a name="is-vnet-to-vnet-traffic-secure"></a>Is het VNet-naar-VNet-verkeer beveiligd?

Ja, het is beveiligd met IPsec/IKE-versleuteling.

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a>Heb ik een VPN-apparaat tooconnect VNets samen nodig?

Nee. Om meerdere virtuele netwerken van Azure met elkaar te verbinden, hebt u geen VPN-apparaat nodig, tenzij cross-premises connectiviteit is vereist.

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a>Hoeft mijn VNets toobe in Hallo dezelfde regio?

Nee. Hallo virtuele netwerken kunnen zich in Hallo dezelfde of verschillende Azure-regio's (locaties).

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a>Als Hallo VNets zich niet op dezelfde Hallo abonnement, Hallo abonnementen hoeft toobe gekoppeld aan Hallo dezelfde AD-tenant?

Nee.

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a>Kan ik VNet-naar-VNet- én multi-site-verbindingen gebruiken?

Ja. U kunt virtuele-netwerkverbindingen tegelijk gebruiken met multi-site-VPN’s.

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a>Met hoeveel on-premises sites en virtuele netwerken kan één virtueel netwerk verbinding maken?

Zie de tabel [Gatewayvereisten](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a>Kan ik een VNet-naar-VNet tooconnect VM's gebruiken of cloudservices buiten een VNet?

Nee. VNet naar VNet ondersteunt het verbinden van virtuele netwerken. Er is geen ondersteuning voor het verbinden van virtuele machines of cloudservices die geen deel uitmaken van een virtueel netwerk.

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a>Kan een cloudservice of een taakverdelingseindpunt VNets overbruggen?

Nee. Een cloudservice of een taakverdelingseindpunt kan geen virtuele netwerken overbruggen, zelfs niet als ze met elkaar zijn verbonden.

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a>Kan ik een op beleid gebaseerd VPN-type gebruiken voor VNet-naar-VNet- of multi-site-verbindingen?

Nee. VNet-naar-VNet- en multi-site-verbindingen vereisen Azure VPN-gateways met op route gebaseerde VPN-typen (voorheen dynamische routering genoemd).

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a>Kan ik een VNet met een op route gebaseerd VPN-Type tooanother VNet met een PolicyBased VPN-type verbinden?

Nee, voor beide virtuele netwerken MOET gebruik worden gemaakt van op route gebaseerde VPN's (voorheen dynamische routering genoemd).

### <a name="do-vpn-tunnels-share-bandwidth"></a>Delen VPN-tunnels bandbreedte?

Ja. Alle VPN-tunnels van het virtuele netwerk Hallo delen Hallo beschikbare bandbreedte op Hallo Azure VPN-gateway en dezelfde SLA voor VPN-gateway bedrijfstijd in Azure Hallo.

### <a name="are-redundant-tunnels-supported"></a>Worden redundante tunnels ondersteund?

Redundante tunnels tussen twee virtuele netwerken worden ondersteund, mits één virtuele-netwerkgateway is geconfigureerd als actief-actief.

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a>Mogen er overlappende adresruimten zijn voor VNet-naar-VNet-configuraties?

Nee. Er mag geen sprake zijn van overlappende IP-adresbereiken.

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a>Mogen er overlappende adresruimten zijn tussen de verbonden virtuele netwerken en on-premises lokale sites?

Nee. Er mag geen sprake zijn van overlappende IP-adresbereiken.



