## <a name="public-ip-address"></a><span data-ttu-id="a0ee5-101">Openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="a0ee5-101">Public IP address</span></span>
<span data-ttu-id="a0ee5-102">Een openbare IP-adres resource biedt ofwel een gereserveerde of dynamische Internetgericht IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="a0ee5-103">Hoewel u een openbaar IP-adres als zelfstandige object maken kunt, moet u tooassociate deze tooanother object tooactually Hallo-adres gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-103">Although you can create a public IP address as a stand alone object, you need tooassociate it tooanother object tooactually use hello address.</span></span> <span data-ttu-id="a0ee5-104">U kunt een openbare IP-adres tooa load balancer, toepassingsgateway of een NIC tooprovide toegang toothose internetbronnen koppelen.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-104">You can associate a public IP address tooa load balancer, application  gateway, or a NIC tooprovide Internet access toothose resources.</span></span>  

| <span data-ttu-id="a0ee5-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a0ee5-105">Property</span></span> | <span data-ttu-id="a0ee5-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a0ee5-106">Description</span></span> | <span data-ttu-id="a0ee5-107">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="a0ee5-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0ee5-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="a0ee5-109">Hiermee worden gedefinieerd als Hallo IP-adres *statische* of *dynamische*.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-109">Defines if hello IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="a0ee5-110">statisch, dynamische</span><span class="sxs-lookup"><span data-stu-id="a0ee5-110">static, dynamic</span></span> |
| <span data-ttu-id="a0ee5-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="a0ee5-112">Hiermee definieert u Hallo niet-actieve time-out, met een standaardwaarde van vier minuten.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-112">Defines hello idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="a0ee5-113">Als er geen meer pakketten voor een bepaalde sessie binnen deze tijd wordt ontvangen, worden Hallo-sessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-113">If no more packets for a given session is received within this time, hello session is terminated.</span></span> |<span data-ttu-id="a0ee5-114">een waarde tussen 4 en 30 in</span><span class="sxs-lookup"><span data-stu-id="a0ee5-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="a0ee5-115">**IP-adres**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-115">**ipAddress**</span></span> |<span data-ttu-id="a0ee5-116">IP-adres toegewezen tooobject.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-116">IP address assigned tooobject.</span></span> <span data-ttu-id="a0ee5-117">Dit is een alleen-lezen eigenschap.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-117">This is a read-only property.</span></span> |<span data-ttu-id="a0ee5-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="a0ee5-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="a0ee5-119">DNS-instellingen</span><span class="sxs-lookup"><span data-stu-id="a0ee5-119">DNS settings</span></span>
<span data-ttu-id="a0ee5-120">Openbare IP-adressen hebben een onderliggend object met de naam **dnsSettings** met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a0ee5-120">Public IP addresses have a child object named **dnsSettings** containing hello following properties:</span></span>

| <span data-ttu-id="a0ee5-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a0ee5-121">Property</span></span> | <span data-ttu-id="a0ee5-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a0ee5-122">Description</span></span> | <span data-ttu-id="a0ee5-123">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="a0ee5-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a0ee5-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-124">**domainNameLabel**</span></span> |<span data-ttu-id="a0ee5-125">Host met de naam gebruikt voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-125">Host named used for name resolution.</span></span> |<span data-ttu-id="a0ee5-126">www-, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="a0ee5-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="a0ee5-127">**FQDN-naam**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-127">**fqdn**</span></span> |<span data-ttu-id="a0ee5-128">Volledig gekwalificeerde naam voor Hallo openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-128">Fully qualified name for hello public IP.</span></span> |<span data-ttu-id="a0ee5-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="a0ee5-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="a0ee5-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="a0ee5-130">**reverseFqdn**</span></span> |<span data-ttu-id="a0ee5-131">FQDN-naam die wordt omgezet toohello IP-adres en is geregistreerd in DNS als een PTR-record.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-131">Fully qualified domain name that resolves toohello IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="a0ee5-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-132">www.contoso.com.</span></span> |

<span data-ttu-id="a0ee5-133">Voorbeeld openbare IP-adres in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="a0ee5-133">Sample public IP address in JSON format:</span></span>

    {
       "name": "PIP01",
       "location": "North US",
       "tags": { "key": "value" },
       "properties": {
          "publicIPAllocationMethod": "Static",
          "idleTimeoutInMinutes": 4,
          "ipAddress": "104.42.233.77",
          "dnsSettings": {
             "domainNameLabel": "mylabel",
             "fqdn": "mylabel.westus.cloudapp.azure.com",
             "reverseFqdn": "contoso.com."
          }
       }
    } 

### <a name="additional-resources"></a><span data-ttu-id="a0ee5-134">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="a0ee5-134">Additional resources</span></span>
* <span data-ttu-id="a0ee5-135">Vindt u meer informatie over [openbare IP-adressen](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="a0ee5-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="a0ee5-136">Meer informatie over [exemplaar niveau openbare IP-adressen](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="a0ee5-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="a0ee5-137">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163638.aspx) voor de openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="a0ee5-137">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

