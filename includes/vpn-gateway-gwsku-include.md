<span data-ttu-id="4e1b3-101">Wanneer u een virtuele netwerkgateway maakt, moet u toospecify Hallo gateway SKU die u toouse wilt.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-101">When you create a virtual network gateway, you need toospecify hello gateway SKU that you want toouse.</span></span> <span data-ttu-id="4e1b3-102">Selecteer Hallo-SKU's die voldoen aan uw behoeften op basis van Hallo typen werkbelastingen, doorvoercapaciteit, functies en sla's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-102">Select hello SKUs that satisfy your requirements based on hello types of workloads, throughputs, features, and SLAs.</span></span>

[!INCLUDE [classic SKU](./vpn-gateway-classic-sku-support-include.md)]

[!INCLUDE [Aggregated throughput by SKU](./vpn-gateway-table-gwtype-aggtput-include.md)]

###  <span data-ttu-id="4e1b3-103"><a name="workloads"></a>Productie *vs.* werkbelastingen voor ontwikkelen en testen</span><span class="sxs-lookup"><span data-stu-id="4e1b3-103"><a name="workloads"></a>Production *vs.* Dev-Test Workloads</span></span>

<span data-ttu-id="4e1b3-104">Vervaldatum toohello verschillen in de sla en functiesets, wordt aangeraden Hallo SKU's voor productie na *versus* dev-test:</span><span class="sxs-lookup"><span data-stu-id="4e1b3-104">Due toohello differences in SLAs and feature sets, we recommend hello following SKUs for production *vs.* dev-test:</span></span>

| <span data-ttu-id="4e1b3-105">**Workload**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-105">**Workload**</span></span>                       | <span data-ttu-id="4e1b3-106">**SKU's**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-106">**SKUs**</span></span>               |
| ---                                | ---                    |
| <span data-ttu-id="4e1b3-107">**Productie, kritieke werkbelastingen**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-107">**Production, critical workloads**</span></span> | <span data-ttu-id="4e1b3-108">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="4e1b3-108">VpnGw1, VpnGw2, VpnGw3</span></span> |
| <span data-ttu-id="4e1b3-109">**Ontwikkelen en testen of conceptontwerpen**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-109">**Dev-test or proof of concept**</span></span>   | <span data-ttu-id="4e1b3-110">Basic</span><span class="sxs-lookup"><span data-stu-id="4e1b3-110">Basic</span></span>                  |
|                                    |                        |

<span data-ttu-id="4e1b3-111">Als u oude hello, SKU's, Hallo productie SKU aanbevelingen zijn Standard en HighPerformance SKU's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-111">If you are using hello old SKUs, hello production SKU recommendations are Standard and HighPerformance SKUs.</span></span> <span data-ttu-id="4e1b3-112">Zie voor informatie over Hallo oude SKU's, [Gateway-SKU's (verouderde SKU's)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span><span class="sxs-lookup"><span data-stu-id="4e1b3-112">For information on hello old SKUs, see [Gateway SKUs (legacy SKUs)](../articles/vpn-gateway/vpn-gateway-about-skus-legacy.md).</span></span>

###  <span data-ttu-id="4e1b3-113"><a name="feature"></a>Gateway-SKU-functiesets</span><span class="sxs-lookup"><span data-stu-id="4e1b3-113"><a name="feature"></a>Gateway SKU feature sets</span></span>

<span data-ttu-id="4e1b3-114">Hallo nieuwe gateway-SKU's stroomlijnen Hallo functiesets aangeboden op Hallo gateways:</span><span class="sxs-lookup"><span data-stu-id="4e1b3-114">hello new gateway SKUs streamline hello feature sets offered on hello gateways:</span></span>

| <span data-ttu-id="4e1b3-115">**SKU**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-115">**SKU**</span></span>| <span data-ttu-id="4e1b3-116">**Functies**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-116">**Features**</span></span>|
| ---    | ---         |
|<span data-ttu-id="4e1b3-117">**Basic**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-117">**Basic**</span></span>   | <span data-ttu-id="4e1b3-118">**Op route gebaseerd VPN**: 10 tunnels met P2S</span><span class="sxs-lookup"><span data-stu-id="4e1b3-118">**Route-based VPN**: 10 tunnels with P2S</span></span><br><br><span data-ttu-id="4e1b3-119">**Op beleid gebaseerd VPN**: (IKEv1): 1 tunnel; geen P2S</span><span class="sxs-lookup"><span data-stu-id="4e1b3-119">**Policy-based VPN**: (IKEv1): 1 tunnel; no P2S</span></span>|
| <span data-ttu-id="4e1b3-120">**VpnGw1, VpnGw2 en VpnGw3**</span><span class="sxs-lookup"><span data-stu-id="4e1b3-120">**VpnGw1, VpnGw2, and VpnGw3**</span></span> | <span data-ttu-id="4e1b3-121">**Route gebaseerde VPN-**: too30 tunnels (*), P2S, BGP, actieve, aangepaste IPsec/IKE-beleid, naast elkaar bestaan ExpressRoute/VPN</span><span class="sxs-lookup"><span data-stu-id="4e1b3-121">**Route-based VPN**: up too30 tunnels (*), P2S, BGP, active-active, custom IPsec/IKE policy, ExpressRoute/VPN co-existence</span></span> |
|        |             |

<span data-ttu-id="4e1b3-122">(*) U kunt 'PolicyBasedTrafficSelectors' tooconnect een op route gebaseerde VPN-gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises firewall op beleid gebaseerde apparaten configureren.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-122">(*) You can configure "PolicyBasedTrafficSelectors" tooconnect a route-based VPN gateway (VpnGw1, VpnGw2, VpnGw3) toomultiple on-premises policy-based firewall devices.</span></span> <span data-ttu-id="4e1b3-123">Raadpleeg te[verbinding maken met VPN-gateways toomultiple on-premises op beleid gebaseerde VPN-apparaten met behulp van PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-123">Refer too[Connect VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) for details.</span></span>

###  <span data-ttu-id="4e1b3-124"><a name="resize"></a>Het formaat van gateway-SKU's wijzigen</span><span class="sxs-lookup"><span data-stu-id="4e1b3-124"><a name="resize"></a>Resizing gateway SKUs</span></span>

1. <span data-ttu-id="4e1b3-125">U kunt wisselen tussen VpnGw1-, VpnGw2- en VpnGw3-SKU's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-125">You can resize between VpnGw1, VpnGw2, and VpnGw3 SKUs.</span></span>
2. <span data-ttu-id="4e1b3-126">Als u werkt met Hallo oude gateway-SKU's, kunt u het formaat van tussen Basic, Standard en HighPerformance SKU's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-126">When working with hello old gateway SKUs, you can resize between Basic, Standard, and HighPerformance SKUs.</span></span>
2. <span data-ttu-id="4e1b3-127">U **kan niet** vergroten of verkleinen van standaard-Basic/HighPerformance SKU's toohello nieuwe VpnGw2-VpnGw1/VpnGw3-SKU's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-127">You **cannot** resize from Basic/Standard/HighPerformance SKUs toohello new VpnGw1/VpnGw2/VpnGw3 SKUs.</span></span> <span data-ttu-id="4e1b3-128">U moet in plaats daarvan [migreren](#migrate) toohello nieuwe SKU's.</span><span class="sxs-lookup"><span data-stu-id="4e1b3-128">You must, instead, [migrate](#migrate) toohello new SKUs.</span></span>

###  <span data-ttu-id="4e1b3-129"><a name="migrate"></a>Migreren van oude SKU's toohello nieuwe SKU's</span><span class="sxs-lookup"><span data-stu-id="4e1b3-129"><a name="migrate"></a>Migrating from old SKUs toohello new SKUs</span></span>

[!INCLUDE [Migrate SKU](./vpn-gateway-migrate-legacy-sku-include.md)]
