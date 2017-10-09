## <a name="traffic-manager-profile"></a><span data-ttu-id="8876d-101">Traffic Manager-profiel</span><span class="sxs-lookup"><span data-stu-id="8876d-101">Traffic Manager Profile</span></span>
<span data-ttu-id="8876d-102">Schakel DNS-routering tooendpoints in Azure en buiten Azure Traffic manager en de onderliggende endpoint-bron.</span><span class="sxs-lookup"><span data-stu-id="8876d-102">Traffic manager and its child endpoint resource enable DNS routing tooendpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="8876d-103">Dergelijke distributie van verkeer wordt geregeld door de methoden voor het doorsturen beleid.</span><span class="sxs-lookup"><span data-stu-id="8876d-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="8876d-104">Traffic manager kunt ook eindpunt health toobe bewaakt en verkeer op de juiste wijze wordt gewijzigd op basis van Hallo-status van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8876d-104">Traffic manager also allows endpoint health toobe monitored, and traffic diverted appropriately based on hello health of an endpoint.</span></span> 

| <span data-ttu-id="8876d-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8876d-105">Property</span></span> | <span data-ttu-id="8876d-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8876d-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8876d-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="8876d-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="8876d-108">mogelijke waarden zijn *prestaties*, *gewogen*, en *prioriteit*</span><span class="sxs-lookup"><span data-stu-id="8876d-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="8876d-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="8876d-109">**dnsConfig**</span></span> |<span data-ttu-id="8876d-110">FQDN-naam voor het Hallo-profiel</span><span class="sxs-lookup"><span data-stu-id="8876d-110">FQDN for hello profile</span></span> |
| <span data-ttu-id="8876d-111">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="8876d-111">**Protocol**</span></span> |<span data-ttu-id="8876d-112">mogelijke waarden zijn protocol bewaking, *HTTP* en *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="8876d-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="8876d-113">**Poort**</span><span class="sxs-lookup"><span data-stu-id="8876d-113">**Port**</span></span> |<span data-ttu-id="8876d-114">bewaking van poort</span><span class="sxs-lookup"><span data-stu-id="8876d-114">monitoring port</span></span> |
| <span data-ttu-id="8876d-115">**Pad**</span><span class="sxs-lookup"><span data-stu-id="8876d-115">**Path**</span></span> |<span data-ttu-id="8876d-116">controlepad</span><span class="sxs-lookup"><span data-stu-id="8876d-116">monitoring path</span></span> |
| <span data-ttu-id="8876d-117">**Eindpunten**</span><span class="sxs-lookup"><span data-stu-id="8876d-117">**Endpoints**</span></span> |<span data-ttu-id="8876d-118">container voor eindpunt bronnen</span><span class="sxs-lookup"><span data-stu-id="8876d-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="8876d-119">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="8876d-119">Endpoint</span></span>
<span data-ttu-id="8876d-120">Een eindpunt is een onderliggende resource van een Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="8876d-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="8876d-121">Vertegenwoordigt een service of web-eindpunt toowhich gebruikersverkeer wordt verdeeld op basis van beleid in Traffic Manager-profiel resource Hallo Hallo geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8876d-121">It represents a service or web endpoint toowhich user traffic is distributed based on hello configured policy in hello Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="8876d-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8876d-122">Property</span></span> | <span data-ttu-id="8876d-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8876d-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8876d-124">**Type**</span><span class="sxs-lookup"><span data-stu-id="8876d-124">**Type**</span></span> |<span data-ttu-id="8876d-125">type Hallo van Hallo eindpunt van de mogelijke waarden zijn *Azure eindpunt*, *Extern eindpunt*, en *genest eindpunt*</span><span class="sxs-lookup"><span data-stu-id="8876d-125">hello type of hello endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="8876d-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="8876d-126">**targetResourceId**</span></span> |<span data-ttu-id="8876d-127">openbare IP-adres van een service of web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8876d-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="8876d-128">Dit is een Azure of het externe eindpunt.</span><span class="sxs-lookup"><span data-stu-id="8876d-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="8876d-129">**Gewicht**</span><span class="sxs-lookup"><span data-stu-id="8876d-129">**Weight**</span></span> |<span data-ttu-id="8876d-130">eindpunt gewicht in verkeer management gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8876d-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="8876d-131">**Prioriteit**</span><span class="sxs-lookup"><span data-stu-id="8876d-131">**Priority**</span></span> |<span data-ttu-id="8876d-132">prioriteit van het Hallo-eindpunt, gebruikte toodefine een actie van failover</span><span class="sxs-lookup"><span data-stu-id="8876d-132">priority of hello endpoint, used toodefine a failover action</span></span> |

<span data-ttu-id="8876d-133">Voorbeeld van Traffic Manager in Json-indeling:</span><span class="sxs-lookup"><span data-stu-id="8876d-133">Sample of Traffic Manager in Json format:</span></span> 

        {
            "apiVersion": "[variables('tmApiVersion')]",
            "type": "Microsoft.Network/trafficManagerProfiles",
            "name": "VMEndpointExample",
            "location": "global",
            "dependsOn": [
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '0')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '1')]",
                "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'), '2')]",
            ],
            "properties": {
                "profileStatus": "Enabled",
                "trafficRoutingMethod": "Weighted",
                "dnsConfig": {
                    "relativeName": "[parameters('dnsname')]",
                    "ttl": 30
                },
                "monitorConfig": {
                    "protocol": "http",
                    "port": 80,
                    "path": "/"
                },
                "endpoints": [
                    {
                        "name": "endpoint0",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 0))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint1",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 1))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    },
                    {
                        "name": "endpoint2",
                        "type": "Microsoft.Network/trafficManagerProfiles/azureEndpoints",
                        "properties": {
                            "targetResourceId": "[resourceId('Microsoft.Network/publicIPAddresses',concat(variables('publicIPAddressName'), 2))]",
                            "endpointStatus": "Enabled",
                            "weight": 1
                        }
                    }
                ]
            }
        }


## <a name="additional-resources"></a><span data-ttu-id="8876d-134">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8876d-134">Additional resources</span></span>
<span data-ttu-id="8876d-135">Lees [REST API-documentatie voor Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8876d-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

