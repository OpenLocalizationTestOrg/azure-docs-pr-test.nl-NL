<span data-ttu-id="ba123-101">Hallo Veelgestelde vragen over VNet-naar-VNet is van toepassing tooVPN gatewayverbindingen.</span><span class="sxs-lookup"><span data-stu-id="ba123-101">hello VNet-to-VNet FAQ applies tooVPN Gateway connections.</span></span> <span data-ttu-id="ba123-102">Zie [Peering op virtueel netwerk](../articles/virtual-network/virtual-network-peering-overview.md) voor VNet-peering</span><span class="sxs-lookup"><span data-stu-id="ba123-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="ba123-103">Worden er door Azure kosten in rekening gebracht voor verkeer tussen VNets?</span><span class="sxs-lookup"><span data-stu-id="ba123-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="ba123-104">VNet-naar-VNet-verkeer binnen Hallo dezelfde regio is gratis voor beide richtingen wanneer u een VPN-gatewayverbinding.</span><span class="sxs-lookup"><span data-stu-id="ba123-104">VNet-to-VNet traffic within hello same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="ba123-105">Cross-regio VNet-naar-VNet uitgaande verkeer wordt in rekening gebracht met Hallo uitgaande inter-VNet tarieven voor gegevensoverdracht op basis van regio's Hallo-bron.</span><span class="sxs-lookup"><span data-stu-id="ba123-105">Cross region VNet-to-VNet egress traffic is charged with hello outbound inter-VNet data transfer rates based on hello source regions.</span></span> <span data-ttu-id="ba123-106">Raadpleeg toohello [VPN-Gateway pagina met prijzen](https://azure.microsoft.com/pricing/details/vpn-gateway/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ba123-106">Refer toohello [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="ba123-107">Als u verbinding van uw vnet's met behulp van de VNet-Peering, in plaats van VPN-Gateway maakt, Zie Hallo [virtueel netwerk pagina met prijzen](https://azure.microsoft.com/pricing/details/virtual-network/).</span><span class="sxs-lookup"><span data-stu-id="ba123-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see hello [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-hello-internet"></a><span data-ttu-id="ba123-108">VNet-naar-VNet-verkeer passeren Hallo Internet?</span><span class="sxs-lookup"><span data-stu-id="ba123-108">Does VNet-to-VNet traffic travel across hello Internet?</span></span>

<span data-ttu-id="ba123-109">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-109">No.</span></span> <span data-ttu-id="ba123-110">VNet-naar-VNet-verkeer via Hallo Microsoft Azure-backbone niet Hallo Internet wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="ba123-110">VNet-to-VNet traffic travels across hello Microsoft Azure backbone, not hello Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="ba123-111">Is het VNet-naar-VNet-verkeer beveiligd?</span><span class="sxs-lookup"><span data-stu-id="ba123-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="ba123-112">Ja, het is beveiligd met IPsec/IKE-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="ba123-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-tooconnect-vnets-together"></a><span data-ttu-id="ba123-113">Heb ik een VPN-apparaat tooconnect VNets samen nodig?</span><span class="sxs-lookup"><span data-stu-id="ba123-113">Do I need a VPN device tooconnect VNets together?</span></span>

<span data-ttu-id="ba123-114">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-114">No.</span></span> <span data-ttu-id="ba123-115">Om meerdere virtuele netwerken van Azure met elkaar te verbinden, hebt u geen VPN-apparaat nodig, tenzij cross-premises connectiviteit is vereist.</span><span class="sxs-lookup"><span data-stu-id="ba123-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-toobe-in-hello-same-region"></a><span data-ttu-id="ba123-116">Hoeft mijn VNets toobe in Hallo dezelfde regio?</span><span class="sxs-lookup"><span data-stu-id="ba123-116">Do my VNets need toobe in hello same region?</span></span>

<span data-ttu-id="ba123-117">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-117">No.</span></span> <span data-ttu-id="ba123-118">Hallo virtuele netwerken kunnen zich in Hallo dezelfde of verschillende Azure-regio's (locaties).</span><span class="sxs-lookup"><span data-stu-id="ba123-118">hello virtual networks can be in hello same or different Azure regions (locations).</span></span>

### <a name="if-hello-vnets-are-not-in-hello-same-subscription-do-hello-subscriptions-need-toobe-associated-with-hello-same-ad-tenant"></a><span data-ttu-id="ba123-119">Als Hallo VNets zich niet op dezelfde Hallo abonnement, Hallo abonnementen hoeft toobe gekoppeld aan Hallo dezelfde AD-tenant?</span><span class="sxs-lookup"><span data-stu-id="ba123-119">If hello VNets are not in hello same subscription, do hello subscriptions need toobe associated with hello same AD tenant?</span></span>

<span data-ttu-id="ba123-120">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="ba123-121">Kan ik VNet-naar-VNet- én multi-site-verbindingen gebruiken?</span><span class="sxs-lookup"><span data-stu-id="ba123-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="ba123-122">Ja.</span><span class="sxs-lookup"><span data-stu-id="ba123-122">Yes.</span></span> <span data-ttu-id="ba123-123">U kunt virtuele-netwerkverbindingen tegelijk gebruiken met multi-site-VPN’s.</span><span class="sxs-lookup"><span data-stu-id="ba123-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="ba123-124">Met hoeveel on-premises sites en virtuele netwerken kan één virtueel netwerk verbinding maken?</span><span class="sxs-lookup"><span data-stu-id="ba123-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="ba123-125">Zie de tabel [Gatewayvereisten](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="ba123-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-tooconnect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="ba123-126">Kan ik een VNet-naar-VNet tooconnect VM's gebruiken of cloudservices buiten een VNet?</span><span class="sxs-lookup"><span data-stu-id="ba123-126">Can I use VNet-to-VNet tooconnect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="ba123-127">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-127">No.</span></span> <span data-ttu-id="ba123-128">VNet naar VNet ondersteunt het verbinden van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="ba123-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="ba123-129">Er is geen ondersteuning voor het verbinden van virtuele machines of cloudservices die geen deel uitmaken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="ba123-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="ba123-130">Kan een cloudservice of een taakverdelingseindpunt VNets overbruggen?</span><span class="sxs-lookup"><span data-stu-id="ba123-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="ba123-131">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-131">No.</span></span> <span data-ttu-id="ba123-132">Een cloudservice of een taakverdelingseindpunt kan geen virtuele netwerken overbruggen, zelfs niet als ze met elkaar zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="ba123-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="ba123-133">Kan ik een op beleid gebaseerd VPN-type gebruiken voor VNet-naar-VNet- of multi-site-verbindingen?</span><span class="sxs-lookup"><span data-stu-id="ba123-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="ba123-134">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-134">No.</span></span> <span data-ttu-id="ba123-135">VNet-naar-VNet- en multi-site-verbindingen vereisen Azure VPN-gateways met op route gebaseerde VPN-typen (voorheen dynamische routering genoemd).</span><span class="sxs-lookup"><span data-stu-id="ba123-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-tooanother-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="ba123-136">Kan ik een VNet met een op route gebaseerd VPN-Type tooanother VNet met een PolicyBased VPN-type verbinden?</span><span class="sxs-lookup"><span data-stu-id="ba123-136">Can I connect a VNet with a RouteBased VPN Type tooanother VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="ba123-137">Nee, voor beide virtuele netwerken MOET gebruik worden gemaakt van op route gebaseerde VPN's (voorheen dynamische routering genoemd).</span><span class="sxs-lookup"><span data-stu-id="ba123-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="ba123-138">Delen VPN-tunnels bandbreedte?</span><span class="sxs-lookup"><span data-stu-id="ba123-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="ba123-139">Ja.</span><span class="sxs-lookup"><span data-stu-id="ba123-139">Yes.</span></span> <span data-ttu-id="ba123-140">Alle VPN-tunnels van het virtuele netwerk Hallo delen Hallo beschikbare bandbreedte op Hallo Azure VPN-gateway en dezelfde SLA voor VPN-gateway bedrijfstijd in Azure Hallo.</span><span class="sxs-lookup"><span data-stu-id="ba123-140">All VPN tunnels of hello virtual network share hello available bandwidth on hello Azure VPN gateway and hello same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="ba123-141">Worden redundante tunnels ondersteund?</span><span class="sxs-lookup"><span data-stu-id="ba123-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="ba123-142">Redundante tunnels tussen twee virtuele netwerken worden ondersteund, mits één virtuele-netwerkgateway is geconfigureerd als actief-actief.</span><span class="sxs-lookup"><span data-stu-id="ba123-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="ba123-143">Mogen er overlappende adresruimten zijn voor VNet-naar-VNet-configuraties?</span><span class="sxs-lookup"><span data-stu-id="ba123-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="ba123-144">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-144">No.</span></span> <span data-ttu-id="ba123-145">Er mag geen sprake zijn van overlappende IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="ba123-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="ba123-146">Mogen er overlappende adresruimten zijn tussen de verbonden virtuele netwerken en on-premises lokale sites?</span><span class="sxs-lookup"><span data-stu-id="ba123-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="ba123-147">Nee.</span><span class="sxs-lookup"><span data-stu-id="ba123-147">No.</span></span> <span data-ttu-id="ba123-148">Er mag geen sprake zijn van overlappende IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="ba123-148">You can't have overlapping IP address ranges.</span></span>



