## <a name="traffic-manager-profile"></a><span data-ttu-id="19ab5-101">Traffic Manager-profiel</span><span class="sxs-lookup"><span data-stu-id="19ab5-101">Traffic Manager Profile</span></span>
<span data-ttu-id="19ab5-102">Traffic manager en de onderliggende endpoint-bron inschakelen DNS-routering naar de eindpunten in Azure en buiten Azure.</span><span class="sxs-lookup"><span data-stu-id="19ab5-102">Traffic manager and its child endpoint resource enable DNS routing to endpoints in Azure and outside of Azure.</span></span> <span data-ttu-id="19ab5-103">Dergelijke distributie van verkeer wordt geregeld door de methoden voor het doorsturen beleid.</span><span class="sxs-lookup"><span data-stu-id="19ab5-103">Such traffic distribution is governed by routing  policy methods.</span></span> <span data-ttu-id="19ab5-104">Traffic manager kunt ook eindpunt health moeten worden bewaakt en verkeer op de juiste wijze wordt gewijzigd op basis van de status van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="19ab5-104">Traffic manager also allows endpoint health to be monitored, and traffic diverted appropriately based on the health of an endpoint.</span></span> 

| <span data-ttu-id="19ab5-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="19ab5-105">Property</span></span> | <span data-ttu-id="19ab5-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19ab5-106">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19ab5-107">**trafficRoutingMethod**</span><span class="sxs-lookup"><span data-stu-id="19ab5-107">**trafficRoutingMethod**</span></span> |<span data-ttu-id="19ab5-108">mogelijke waarden zijn *prestaties*, *gewogen*, en *prioriteit*</span><span class="sxs-lookup"><span data-stu-id="19ab5-108">possible values are *Performance*, *Weighted*, and *Priority*</span></span> |
| <span data-ttu-id="19ab5-109">**dnsConfig**</span><span class="sxs-lookup"><span data-stu-id="19ab5-109">**dnsConfig**</span></span> |<span data-ttu-id="19ab5-110">FQDN-naam voor het profiel</span><span class="sxs-lookup"><span data-stu-id="19ab5-110">FQDN for the profile</span></span> |
| <span data-ttu-id="19ab5-111">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="19ab5-111">**Protocol**</span></span> |<span data-ttu-id="19ab5-112">mogelijke waarden zijn protocol bewaking, *HTTP* en *HTTPS*</span><span class="sxs-lookup"><span data-stu-id="19ab5-112">monitoring protocol, possible values are *HTTP* and *HTTPS*</span></span> |
| <span data-ttu-id="19ab5-113">**Poort**</span><span class="sxs-lookup"><span data-stu-id="19ab5-113">**Port**</span></span> |<span data-ttu-id="19ab5-114">bewaking van poort</span><span class="sxs-lookup"><span data-stu-id="19ab5-114">monitoring port</span></span> |
| <span data-ttu-id="19ab5-115">**Pad**</span><span class="sxs-lookup"><span data-stu-id="19ab5-115">**Path**</span></span> |<span data-ttu-id="19ab5-116">controlepad</span><span class="sxs-lookup"><span data-stu-id="19ab5-116">monitoring path</span></span> |
| <span data-ttu-id="19ab5-117">**Eindpunten**</span><span class="sxs-lookup"><span data-stu-id="19ab5-117">**Endpoints**</span></span> |<span data-ttu-id="19ab5-118">container voor eindpunt bronnen</span><span class="sxs-lookup"><span data-stu-id="19ab5-118">container for endpoint resources</span></span> |

### <a name="endpoint"></a><span data-ttu-id="19ab5-119">Eindpunt</span><span class="sxs-lookup"><span data-stu-id="19ab5-119">Endpoint</span></span>
<span data-ttu-id="19ab5-120">Een eindpunt is een onderliggende resource van een Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="19ab5-120">An endpoint is a child resource of a Traffic Manager Profile.</span></span> <span data-ttu-id="19ab5-121">Vertegenwoordigt een service of web-eindpunt waaraan gebruiker verkeer wordt verdeeld op basis van het geconfigureerde beleid in de resource Traffic Manager-profiel.</span><span class="sxs-lookup"><span data-stu-id="19ab5-121">It represents a service or web endpoint to which user traffic is distributed based on the configured policy in the Traffic Manager Profile resource.</span></span> 

| <span data-ttu-id="19ab5-122">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="19ab5-122">Property</span></span> | <span data-ttu-id="19ab5-123">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19ab5-123">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19ab5-124">**Type**</span><span class="sxs-lookup"><span data-stu-id="19ab5-124">**Type**</span></span> |<span data-ttu-id="19ab5-125">het type van het eindpunt, mogelijke waarden zijn *Azure eindpunt*, *Extern eindpunt*, en *genest eindpunt*</span><span class="sxs-lookup"><span data-stu-id="19ab5-125">the type of the endpoint, possible values are *Azure End point*, *External Endpoint*, and  *Nested Endpoint*</span></span> |
| <span data-ttu-id="19ab5-126">**targetResourceId**</span><span class="sxs-lookup"><span data-stu-id="19ab5-126">**targetResourceId**</span></span> |<span data-ttu-id="19ab5-127">openbare IP-adres van een service of web-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="19ab5-127">public IP address of a service or web endpoint.</span></span> <span data-ttu-id="19ab5-128">Dit is een Azure of het externe eindpunt.</span><span class="sxs-lookup"><span data-stu-id="19ab5-128">This can be an Azure or external endpoint.</span></span> |
| <span data-ttu-id="19ab5-129">**Gewicht**</span><span class="sxs-lookup"><span data-stu-id="19ab5-129">**Weight**</span></span> |<span data-ttu-id="19ab5-130">eindpunt gewicht in verkeer management gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19ab5-130">endpoint weight used in traffic management.</span></span> |
| <span data-ttu-id="19ab5-131">**Prioriteit**</span><span class="sxs-lookup"><span data-stu-id="19ab5-131">**Priority**</span></span> |<span data-ttu-id="19ab5-132">prioriteit van het eindpunt, gebruikt voor het definiëren van een actie van failover</span><span class="sxs-lookup"><span data-stu-id="19ab5-132">priority of the endpoint, used to define a failover action</span></span> |

<span data-ttu-id="19ab5-133">Voorbeeld van Traffic Manager in Json-indeling:</span><span class="sxs-lookup"><span data-stu-id="19ab5-133">Sample of Traffic Manager in Json format:</span></span> 

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


## <a name="additional-resources"></a><span data-ttu-id="19ab5-134">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="19ab5-134">Additional resources</span></span>
<span data-ttu-id="19ab5-135">Lees [REST API-documentatie voor Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19ab5-135">Read [REST API documentation for Traffic Manager](https://msdn.microsoft.com/library/azure/mt163664.aspx) for more information.</span></span>

