## <a name="route-tables"></a><span data-ttu-id="b6cdb-101">Routetabellen</span><span class="sxs-lookup"><span data-stu-id="b6cdb-101">Route tables</span></span>
<span data-ttu-id="b6cdb-102">Route tabel resources bevat routes gebruikt toodefine hoe verkeersstromen binnen uw Azure-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-102">Route table resources contains routes used toodefine how traffic flows within your Azure infrastructure.</span></span> <span data-ttu-id="b6cdb-103">U kunt door de gebruiker gedefinieerde routes (UDR) toosend al het verkeer van een bepaald subnet tooa virtueel apparaat, zoals een firewall of inbraakdetectie detectie-systeem (id's) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-103">You can use user defined routes (UDR) toosend all traffic from a given subnet tooa virtual appliance, such as a firewall or intrusion detection system (IDS).</span></span> <span data-ttu-id="b6cdb-104">U kunt een route tabel toosubnets koppelen.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-104">You can associate a route table toosubnets.</span></span> 

<span data-ttu-id="b6cdb-105">Routetabellen bevatten Hallo volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-105">Route tables contain hello following properties.</span></span>

| <span data-ttu-id="b6cdb-106">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b6cdb-106">Property</span></span> | <span data-ttu-id="b6cdb-107">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b6cdb-107">Description</span></span> | <span data-ttu-id="b6cdb-108">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="b6cdb-108">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6cdb-109">**routes**</span><span class="sxs-lookup"><span data-stu-id="b6cdb-109">**routes**</span></span> |<span data-ttu-id="b6cdb-110">Verzameling van de gebruiker gedefinieerde routes in de routetabel Hallo</span><span class="sxs-lookup"><span data-stu-id="b6cdb-110">Collection of user defined routes in hello route table</span></span> |<span data-ttu-id="b6cdb-111">Zie [door de gebruiker gedefinieerde routes](#User-defined-routes)</span><span class="sxs-lookup"><span data-stu-id="b6cdb-111">see [user defined routes](#User-defined-routes)</span></span> |
| <span data-ttu-id="b6cdb-112">**subnetten**</span><span class="sxs-lookup"><span data-stu-id="b6cdb-112">**subnets**</span></span> |<span data-ttu-id="b6cdb-113">Verzameling van subnetten Hallo routetabel wordt te toegepast</span><span class="sxs-lookup"><span data-stu-id="b6cdb-113">Collection of subnets hello route table is applied too</span></span>|<span data-ttu-id="b6cdb-114">Zie [subnetten](#Subnets)</span><span class="sxs-lookup"><span data-stu-id="b6cdb-114">see [subnets](#Subnets)</span></span> |

### <a name="user-defined-routes"></a><span data-ttu-id="b6cdb-115">De gebruiker gedefinieerde routes</span><span class="sxs-lookup"><span data-stu-id="b6cdb-115">User defined routes</span></span>
<span data-ttu-id="b6cdb-116">U kunt udr's toospecify waar verkeer moet worden gezonden, maken op basis van het doeladres.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-116">You can create UDRs toospecify where traffic should be sent to, based on its destination address.</span></span> <span data-ttu-id="b6cdb-117">U kunt een route beschouwen als Hallo standaard gateway-definitie op basis van het doeladres Hallo van een netwerkpakket.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-117">You can think of a route as hello default gateway definition based on hello destination address of a network packet.</span></span>

<span data-ttu-id="b6cdb-118">Udr's bevatten de volgende eigenschappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-118">UDRs contain hello following properties.</span></span> 

| <span data-ttu-id="b6cdb-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b6cdb-119">Property</span></span> | <span data-ttu-id="b6cdb-120">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b6cdb-120">Description</span></span> | <span data-ttu-id="b6cdb-121">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="b6cdb-121">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b6cdb-122">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="b6cdb-122">**addressPrefix**</span></span> |<span data-ttu-id="b6cdb-123">Adresvoorvoegsel of volledige IP-adres voor de bestemming Hallo</span><span class="sxs-lookup"><span data-stu-id="b6cdb-123">Address prefix, or full IP address for hello destination</span></span> |<span data-ttu-id="b6cdb-124">192.168.1.0/24, 192.168.1.101</span><span class="sxs-lookup"><span data-stu-id="b6cdb-124">192.168.1.0/24, 192.168.1.101</span></span> |
| <span data-ttu-id="b6cdb-125">**nextHopType**</span><span class="sxs-lookup"><span data-stu-id="b6cdb-125">**nextHopType**</span></span> |<span data-ttu-id="b6cdb-126">Type apparaat Hallo verkeer worden te verzonden</span><span class="sxs-lookup"><span data-stu-id="b6cdb-126">Type of device hello traffic will be sent too</span></span>|<span data-ttu-id="b6cdb-127">Internet VirtualAppliance, VPN-Gateway</span><span class="sxs-lookup"><span data-stu-id="b6cdb-127">VirtualAppliance, VPN Gateway, Internet</span></span> |
| <span data-ttu-id="b6cdb-128">**nextHopIpAddress**</span><span class="sxs-lookup"><span data-stu-id="b6cdb-128">**nextHopIpAddress**</span></span> |<span data-ttu-id="b6cdb-129">IP-adres voor de volgende hop Hallo</span><span class="sxs-lookup"><span data-stu-id="b6cdb-129">IP address for hello next hop</span></span> |<span data-ttu-id="b6cdb-130">192.168.1.4</span><span class="sxs-lookup"><span data-stu-id="b6cdb-130">192.168.1.4</span></span> |

<span data-ttu-id="b6cdb-131">Voorbeeld routetabel in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="b6cdb-131">Sample route table in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="b6cdb-132">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="b6cdb-132">Additional resources</span></span>
* <span data-ttu-id="b6cdb-133">Vindt u meer informatie over [udr's](../articles/virtual-network/virtual-networks-udr-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b6cdb-133">Get more information about [UDRs](../articles/virtual-network/virtual-networks-udr-overview.md).</span></span>
* <span data-ttu-id="b6cdb-134">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502549.aspx) voor routetabellen.</span><span class="sxs-lookup"><span data-stu-id="b6cdb-134">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502549.aspx) for route tables.</span></span>
* <span data-ttu-id="b6cdb-135">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt502539.aspx) voor de gebruiker gedefinieerde routes (udr's).</span><span class="sxs-lookup"><span data-stu-id="b6cdb-135">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt502539.aspx) for user defined routes (UDRs).</span></span>

