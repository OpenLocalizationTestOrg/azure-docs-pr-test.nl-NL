## <a name="route-tables"></a><span data-ttu-id="405a6-101">Routetabellen</span><span class="sxs-lookup"><span data-stu-id="405a6-101">Route tables</span></span>
<span data-ttu-id="405a6-102">Route tabel resources bevat routes die worden gebruikt om te definiëren hoe verkeer stroomt binnen uw Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="405a6-102">Route table resources contains routes used to define how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="405a6-103">De gebruiker gedefinieerde routes (UDR) kunt u alle verkeer verzenden vanaf een bepaald subnet naar een virtueel apparaat zoals een firewall of inbraakdetectie detectie-systeem (id's).</span><span class="sxs-lookup"><span data-stu-id="405a6-103">You can use user defined routes (UDR) to send all traffic from a given subnet to a virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="405a6-104">U kunt een routetabel aan subnetten koppelen.</span><span class="sxs-lookup"><span data-stu-id="405a6-104">You can associate a route table to subnets.</span></span> 

<span data-ttu-id="405a6-105">Routetabellen bevatten de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="405a6-105">Route tables contain the following properties.</span></span>

| <span data-ttu-id="405a6-106">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="405a6-106">Property</span></span> | <span data-ttu-id="405a6-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="405a6-107">Description</span></span> | <span data-ttu-id="405a6-108">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="405a6-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="405a6-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="405a6-109">**routes**</span></span> |<span data-ttu-id="405a6-110">Verzameling van de gebruiker gedefinieerde routes in de routetabel</span><span class="sxs-lookup"><span data-stu-id="405a6-110">Collection of user defined routes in the route table</span></span> |<span data-ttu-id="405a6-111">Zie [door de gebruiker gedefinieerde routes](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="405a6-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="405a6-112">**subnetten**</span><span class="sxs-lookup"><span data-stu-id="405a6-112">**subnets**</span></span> |<span data-ttu-id="405a6-113">Verzameling van de routetabel wordt toegepast op subnetten</span><span class="sxs-lookup"><span data-stu-id="405a6-113">Collection of subnets the route table is applied to</span></span> |<span data-ttu-id="405a6-114">Zie [subnetten](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="405a6-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="405a6-115">De gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="405a6-115">User defined routes</span></span>
<span data-ttu-id="405a6-116">U kunt udr's om op te geven waar verkeer moet worden gezonden, maken op basis van het doeladres.</span><span class="sxs-lookup"><span data-stu-id="405a6-116">You can create UDRs to specify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="405a6-117">U kunt een route beschouwen als de standaard gateway-definitie op basis van het doeladres van een netwerkpakket.</span><span class="sxs-lookup"><span data-stu-id="405a6-117">You can think of a route as the default gateway definition based on the destination address of a network packet.</span></span>

<span data-ttu-id="405a6-118">Udr's bevatten de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="405a6-118">UDRs contain the following properties.</span></span> 

| <span data-ttu-id="405a6-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="405a6-119">Property</span></span> | <span data-ttu-id="405a6-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="405a6-120">Description</span></span> | <span data-ttu-id="405a6-121">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="405a6-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="405a6-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="405a6-122">**addressPrefix**</span></span> |<span data-ttu-id="405a6-123">Adresvoorvoegsel of volledige IP-adres voor de bestemming</span><span class="sxs-lookup"><span data-stu-id="405a6-123">Address prefix, or full IP address for the destination</span></span> |<span data-ttu-id="405a6-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="405a6-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="405a6-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="405a6-125">**nextHopType**</span></span> |<span data-ttu-id="405a6-126">Type apparaat dat het verkeer wordt verzonden naar</span><span class="sxs-lookup"><span data-stu-id="405a6-126">Type of device the traffic will be sent to</span></span> |<span data-ttu-id="405a6-127">Internet VirtualAppliance, VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="405a6-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="405a6-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="405a6-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="405a6-129">IP-adres voor de volgende hop</span><span class="sxs-lookup"><span data-stu-id="405a6-129">IP address for the next hop</span></span> |<span data-ttu-id="405a6-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="405a6-130">192.168.1.4</span></span> |

<span data-ttu-id="405a6-131">Voorbeeld routetabel in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="405a6-131">Sample route table in JSON format:</span></span>

    {
        "name": "UDR-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/routeTables",
        "location": "westus",
        "properties": {
            "provisioningState": "Succeeded",
            "routes": [
                {
                    "name": "RouteToFrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-BackEnd/routes/RouteToFrontEnd",
                    "etag": "W/\"v\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "nextHopType": "VirtualAppliance",
                        "nextHopIpAddress": "192.168.0.4"
                    }
                }
            ],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd"
                }
            ]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="405a6-132">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="405a6-132">Additional resources</span></span>
* <span data-ttu-id="405a6-133">Vindt u meer informatie over [udr's](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="405a6-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="405a6-134">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502549.aspx) voor routetabellen.</span><span class="sxs-lookup"><span data-stu-id="405a6-134">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="405a6-135">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502539.aspx) voor de gebruiker gedefinieerde routes (udr's).</span><span class="sxs-lookup"><span data-stu-id="405a6-135">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

