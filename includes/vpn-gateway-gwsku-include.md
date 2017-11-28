<span data-ttu-id="f46a1-101">Wanneer u een virtuele netwerkgateway maakt, moet u de gewenste gateway-SKU opgeven.</span><span class="sxs-lookup"><span data-stu-id="f46a1-101">When you create a virtual network gateway, you need to specify the gateway SKU that you want to use.</span></span> <span data-ttu-id="f46a1-102">Selecteer de SKU's die aan uw vereisten voldoen op basis van de typen werkbelasting, doorvoer, functies en SLA's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-102">Select the SKUs that satisfy your requirements based on the types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="f46a1-103"><a name="workloads"></a>Productie *vs.* werkbelastingen voor ontwikkelen en testen</span><span class="sxs-lookup"><span data-stu-id="f46a1-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="f46a1-104">Vanwege de verschillen in SLA's en functiesets, raden we de volgende SKU's aan voor productie *vs.* ontwikkelen en testen:</span><span class="sxs-lookup"><span data-stu-id="f46a1-104">Due to the differences in SLAs and feature sets, we recommend the following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="f46a1-105">**Workload**</span><span class="sxs-lookup"><span data-stu-id="f46a1-105">**Workload**</span></span>                       | <span data-ttu-id="f46a1-106">**SKU's**</span><span class="sxs-lookup"><span data-stu-id="f46a1-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="f46a1-107">**Productie, kritieke werkbelastingen**</span><span class="sxs-lookup"><span data-stu-id="f46a1-107">**Production, critical workloads**</span></span> | <span data-ttu-id="f46a1-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="f46a1-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="f46a1-109">**Ontwikkelen en testen of conceptontwerpen**</span><span class="sxs-lookup"><span data-stu-id="f46a1-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="f46a1-110">Basic</span><span class="sxs-lookup"><span data-stu-id="f46a1-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="f46a1-111">Als u de oude SKU's gebruikt, zijn de aanbevelingen voor de productie-SKU Standard- en HighPerformance-SKU's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-111">If you are using the old SKUs, the production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="f46a1-112">Zie [Gateway-SKU's (verouderde SKU's)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md) voor informatie over de oude SKU's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-112">For information on the old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="f46a1-113"><a name="feature"></a>Gateway-SKU-functiesets</span><span class="sxs-lookup"><span data-stu-id="f46a1-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="f46a1-114">De nieuwe gateway SKU's stroomlijnen de functiesets die worden aangeboden op de gateways:</span><span class="sxs-lookup"><span data-stu-id="f46a1-114">The new gateway SKUs streamline the feature sets offered on the gateways:</span></span>

| <span data-ttu-id="f46a1-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="f46a1-115">**SKU**</span></span>| <span data-ttu-id="f46a1-116">**Functies**</span><span class="sxs-lookup"><span data-stu-id="f46a1-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="f46a1-117">**Basic**</span><span class="sxs-lookup"><span data-stu-id="f46a1-117">**Basic**</span></span>   | <span data-ttu-id="f46a1-118">**Op route gebaseerd VPN**: 10 tunnels met P2S</span><span class="sxs-lookup"><span data-stu-id="f46a1-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="f46a1-119">**Op beleid gebaseerd VPN**: (IKEv1): 1 tunnel; geen P2S</span><span class="sxs-lookup"><span data-stu-id="f46a1-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="f46a1-120">**VpnGw1, VpnGw2 en VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="f46a1-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="f46a1-121">**Op route gebaseerd VPN**: maximaal 30 tunnels (*), P2S, BGP, actief-actief, aangepast IPsec/IKE-beleid, ExpressRoute/VPN samen</span><span class="sxs-lookup"><span data-stu-id="f46a1-121">**Route-based VPN**: up to 30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="f46a1-122">(*) U kunt "PolicyBasedTrafficSelectors" configureren om een op route gebaseerde VPN-gateway (VpnGw1, VpnGw2, VpnGw3) te verbinden met meerdere on-premises, op beleid gebaseerde firewallapparaten.</span><span class="sxs-lookup"><span data-stu-id="f46a1-122">(*) You can configure "PolicyBasedTrafficSelectors" to connect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) to multiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="f46a1-123">Raadpleeg [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) (VPN-gateways verbinden met meerdere on-premises,op beleid gebaseerde VPN-apparaten met behulp van PowerShell) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f46a1-123">Refer to [Connect VPN gateways to multiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="f46a1-124"><a name="resize"></a>Het formaat van gateway-SKU's wijzigen</span><span class="sxs-lookup"><span data-stu-id="f46a1-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="f46a1-125">U kunt wisselen tussen VpnGw1-, VpnGw2- en VpnGw3-SKU's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="f46a1-126">Als u met de oude gateway-SKU's werkt, kunt u wisselen tussen Basic-, Standard- en HighPerformance-SKU's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-126">When working with the old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="f46a1-127">U kunt**niet** wisselen van Basic-/Standard-/HighPerformance-SKU's naar de nieuwe VpnGw2-/VpnGw1-/VpnGw3-SKU's.</span><span class="sxs-lookup"><span data-stu-id="f46a1-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs to the new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="f46a1-128">U moet in plaats daarvan naar de nieuwe SKU's [migreren](#migrate).</span><span class="sxs-lookup"><span data-stu-id="f46a1-128">You must, instead, [migrate](#migrate) to the new SKUs.</span></span>

###  <span data-ttu-id="f46a1-129"><a name="migrate"></a>Van oude SKU's naar nieuwe SKU's migreren</span><span class="sxs-lookup"><span data-stu-id="f46a1-129"><a name="migrate"></a>Migrating from old SKUs to the new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
