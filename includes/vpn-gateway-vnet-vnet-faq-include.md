<span data-ttu-id="cc4b7-101">De veelgestelde vragen voor VNet-naar-VNet zijn van toepassing op VPN Gateway-verbindingen.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-101">The VNet-to-VNet FAQ applies to VPN Gateway connections.</span></span> <span data-ttu-id="cc4b7-102">Zie [Peering op virtueel netwerk](../articles/virtual-network/virtual-network-peering-overview.md) voor VNet-peering</span><span class="sxs-lookup"><span data-stu-id="cc4b7-102">If you are looking for VNet Peering, see [Virtual Network Peering](../articles/virtual-network/virtual-network-peering-overview.md)</span></span>

### <a name="does-azure-charge-for-traffic-between-vnets"></a><span data-ttu-id="cc4b7-103">Worden er door Azure kosten in rekening gebracht voor verkeer tussen VNets?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-103">Does Azure charge for traffic between VNets?</span></span>

<span data-ttu-id="cc4b7-104">VNet-naar-VNet-verkeer binnen dezelfde regio is gratis in beide richtingen wanneer u een VPN Gateway-verbinding gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-104">VNet-to-VNet traffic within the same region is free for both directions when using a VPN gateway connection.</span></span> <span data-ttu-id="cc4b7-105">Voor uitgaand VNet-naar-VNet-verkeer tussen regio's gelden de tarieven voor uitgaande gegevensoverdracht tussen VNets op basis van de bronregio's.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-105">Cross region VNet-to-VNet egress traffic is charged with the outbound inter-VNet data transfer rates based on the source regions.</span></span> <span data-ttu-id="cc4b7-106">Raadpleeg de [pagina met VPN Gateway-prijzen](https://azure.microsoft.com/pricing/details/vpn-gateway/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-106">Refer to the [VPN Gateway pricing page](https://azure.microsoft.com/pricing/details/vpn-gateway/) for details.</span></span> <span data-ttu-id="cc4b7-107">Zie de [pagina met prijzen voor virtuele netwerken](https://azure.microsoft.com/pricing/details/virtual-network/) als u uw VNets verbindt op basis van VNet-peering in plaats van VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-107">If you are connecting your VNets using VNet Peering, rather than VPN Gateway, see the [Virtual Network pricing page](https://azure.microsoft.com/pricing/details/virtual-network/).</span></span>

### <a name="does-vnet-to-vnet-traffic-travel-across-the-internet"></a><span data-ttu-id="cc4b7-108">Verloopt VNet-naar-VNet-verkeer via internet?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-108">Does VNet-to-VNet traffic travel across the Internet?</span></span>

<span data-ttu-id="cc4b7-109">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-109">No.</span></span> <span data-ttu-id="cc4b7-110">Voor VNet-naar-VNet-verkeer wordt het Microsoft-netwerk gebruikt in plaats van internet.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-110">VNet-to-VNet traffic travels across the Microsoft Azure backbone, not the Internet.</span></span>

### <a name="is-vnet-to-vnet-traffic-secure"></a><span data-ttu-id="cc4b7-111">Is het VNet-naar-VNet-verkeer beveiligd?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-111">Is VNet-to-VNet traffic secure?</span></span>

<span data-ttu-id="cc4b7-112">Ja, het is beveiligd met IPsec/IKE-versleuteling.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-112">Yes, it is protected by IPsec/IKE encryption.</span></span>

### <a name="do-i-need-a-vpn-device-to-connect-vnets-together"></a><span data-ttu-id="cc4b7-113">Heb ik een VPN-apparaat nodig om VNets met elkaar te verbinden?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-113">Do I need a VPN device to connect VNets together?</span></span>

<span data-ttu-id="cc4b7-114">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-114">No.</span></span> <span data-ttu-id="cc4b7-115">Om meerdere virtuele netwerken van Azure met elkaar te verbinden, hebt u geen VPN-apparaat nodig, tenzij cross-premises connectiviteit is vereist.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-115">Connecting multiple Azure virtual networks together doesn't require a VPN device unless cross-premises connectivity is required.</span></span>

### <a name="do-my-vnets-need-to-be-in-the-same-region"></a><span data-ttu-id="cc4b7-116">Moeten mijn VNets zich in dezelfde regio bevinden?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-116">Do my VNets need to be in the same region?</span></span>

<span data-ttu-id="cc4b7-117">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-117">No.</span></span> <span data-ttu-id="cc4b7-118">De virtuele netwerken kunnen zich in dezelfde of verschillende Azure-regio's (locaties) bevinden.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-118">The virtual networks can be in the same or different Azure regions (locations).</span></span>

### <a name="if-the-vnets-are-not-in-the-same-subscription-do-the-subscriptions-need-to-be-associated-with-the-same-ad-tenant"></a><span data-ttu-id="cc4b7-119">Als de VNets niet tot hetzelfde abonnement behoren, moeten de abonnementen dan aan dezelfde AD-tenant zijn gekoppeld?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-119">If the VNets are not in the same subscription, do the subscriptions need to be associated with the same AD tenant?</span></span>

<span data-ttu-id="cc4b7-120">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-120">No.</span></span>

### <a name="can-i-use-vnet-to-vnet-along-with-multi-site-connections"></a><span data-ttu-id="cc4b7-121">Kan ik VNet-naar-VNet- én multi-site-verbindingen gebruiken?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-121">Can I use VNet-to-VNet along with multi-site connections?</span></span>

<span data-ttu-id="cc4b7-122">Ja.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-122">Yes.</span></span> <span data-ttu-id="cc4b7-123">U kunt virtuele-netwerkverbindingen tegelijk gebruiken met multi-site-VPN’s.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-123">Virtual network connectivity can be used simultaneously with multi-site VPNs.</span></span>

### <a name="how-many-on-premises-sites-and-virtual-networks-can-one-virtual-network-connect-to"></a><span data-ttu-id="cc4b7-124">Met hoeveel on-premises sites en virtuele netwerken kan één virtueel netwerk verbinding maken?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-124">How many on-premises sites and virtual networks can one virtual network connect to?</span></span>

<span data-ttu-id="cc4b7-125">Zie de tabel [Gatewayvereisten](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="cc4b7-125">See [Gateway requirements](../articles/vpn-gateway/vpn-gateway-about-vpn-gateway-settings.md#requirements) table.</span></span>

### <a name="can-i-use-vnet-to-vnet-to-connect-vms-or-cloud-services-outside-of-a-vnet"></a><span data-ttu-id="cc4b7-126">Kan ik VNet-naar-VNet gebruiken om virtuele machines of cloudservices met elkaar te verbinden buiten een VNet?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-126">Can I use VNet-to-VNet to connect VMs or cloud services outside of a VNet?</span></span>

<span data-ttu-id="cc4b7-127">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-127">No.</span></span> <span data-ttu-id="cc4b7-128">VNet naar VNet ondersteunt het verbinden van virtuele netwerken.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-128">VNet-to-VNet supports connecting virtual networks.</span></span> <span data-ttu-id="cc4b7-129">Er is geen ondersteuning voor het verbinden van virtuele machines of cloudservices die geen deel uitmaken van een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-129">It does not support connecting virtual machines or cloud services that are not in a virtual network.</span></span>

### <a name="can-a-cloud-service-or-a-load-balancing-endpoint-span-vnets"></a><span data-ttu-id="cc4b7-130">Kan een cloudservice of een taakverdelingseindpunt VNets overbruggen?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-130">Can a cloud service or a load balancing endpoint span VNets?</span></span>

<span data-ttu-id="cc4b7-131">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-131">No.</span></span> <span data-ttu-id="cc4b7-132">Een cloudservice of een taakverdelingseindpunt kan geen virtuele netwerken overbruggen, zelfs niet als ze met elkaar zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-132">A cloud service or a load balancing endpoint can't span across virtual networks, even if they are connected together.</span></span>

### <a name="can-i-used-a-policybased-vpn-type-for-vnet-to-vnet-or-multi-site-connections"></a><span data-ttu-id="cc4b7-133">Kan ik een op beleid gebaseerd VPN-type gebruiken voor VNet-naar-VNet- of multi-site-verbindingen?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-133">Can I used a PolicyBased VPN type for VNet-to-VNet or Multi-Site connections?</span></span>

<span data-ttu-id="cc4b7-134">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-134">No.</span></span> <span data-ttu-id="cc4b7-135">VNet-naar-VNet- en multi-site-verbindingen vereisen Azure VPN-gateways met op route gebaseerde VPN-typen (voorheen dynamische routering genoemd).</span><span class="sxs-lookup"><span data-stu-id="cc4b7-135">VNet-to-VNet and Multi-Site connections require Azure VPN gateways with RouteBased (previously called Dynamic Routing) VPN types.</span></span>

### <a name="can-i-connect-a-vnet-with-a-routebased-vpn-type-to-another-vnet-with-a-policybased-vpn-type"></a><span data-ttu-id="cc4b7-136">Kan ik een VNet met een op route gebaseerd VPN-type verbinden met een op beleid gebaseerd VPN-type?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-136">Can I connect a VNet with a RouteBased VPN Type to another VNet with a PolicyBased VPN type?</span></span>

<span data-ttu-id="cc4b7-137">Nee, voor beide virtuele netwerken MOET gebruik worden gemaakt van op route gebaseerde VPN's (voorheen dynamische routering genoemd).</span><span class="sxs-lookup"><span data-stu-id="cc4b7-137">No, both virtual networks MUST be using route-based (previously called Dynamic Routing) VPNs.</span></span>

### <a name="do-vpn-tunnels-share-bandwidth"></a><span data-ttu-id="cc4b7-138">Delen VPN-tunnels bandbreedte?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-138">Do VPN tunnels share bandwidth?</span></span>

<span data-ttu-id="cc4b7-139">Ja.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-139">Yes.</span></span> <span data-ttu-id="cc4b7-140">Alle VPN-tunnels van het virtuele netwerk delen de beschikbare bandbreedte op de Azure VPN-gateway en dezelfde SLA voor VPN-gatewaybedrijfstijd in Azure.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-140">All VPN tunnels of the virtual network share the available bandwidth on the Azure VPN gateway and the same VPN gateway uptime SLA in Azure.</span></span>

### <a name="are-redundant-tunnels-supported"></a><span data-ttu-id="cc4b7-141">Worden redundante tunnels ondersteund?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-141">Are redundant tunnels supported?</span></span>

<span data-ttu-id="cc4b7-142">Redundante tunnels tussen twee virtuele netwerken worden ondersteund, mits één virtuele-netwerkgateway is geconfigureerd als actief-actief.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-142">Redundant tunnels between a pair of virtual networks are supported when one virtual network gateway is configured as active-active.</span></span>

### <a name="can-i-have-overlapping-address-spaces-for-vnet-to-vnet-configurations"></a><span data-ttu-id="cc4b7-143">Mogen er overlappende adresruimten zijn voor VNet-naar-VNet-configuraties?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-143">Can I have overlapping address spaces for VNet-to-VNet configurations?</span></span>

<span data-ttu-id="cc4b7-144">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-144">No.</span></span> <span data-ttu-id="cc4b7-145">Er mag geen sprake zijn van overlappende IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-145">You can't have overlapping IP address ranges.</span></span>

### <a name="can-there-be-overlapping-address-spaces-among-connected-virtual-networks-and-on-premises-local-sites"></a><span data-ttu-id="cc4b7-146">Mogen er overlappende adresruimten zijn tussen de verbonden virtuele netwerken en on-premises lokale sites?</span><span class="sxs-lookup"><span data-stu-id="cc4b7-146">Can there be overlapping address spaces among connected virtual networks and on-premises local sites?</span></span>

<span data-ttu-id="cc4b7-147">Nee.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-147">No.</span></span> <span data-ttu-id="cc4b7-148">Er mag geen sprake zijn van overlappende IP-adresbereiken.</span><span class="sxs-lookup"><span data-stu-id="cc4b7-148">You can't have overlapping IP address ranges.</span></span>



