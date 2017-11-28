## <a name="public-ip-address"></a><span data-ttu-id="d15ed-101">Openbaar IP-adres</span><span class="sxs-lookup"><span data-stu-id="d15ed-101">Public IP address</span></span>
<span data-ttu-id="d15ed-102">Een openbare IP-adres resource biedt ofwel een gereserveerde of dynamische Internetgericht IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d15ed-102">A public IP address resource provides either a reserved or dynamic Internet facing IP address.</span></span> <span data-ttu-id="d15ed-103">Hoewel u een openbaar IP-adres als zelfstandige object maken kunt, moet u deze koppelen aan een ander object daadwerkelijk het adres te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d15ed-103">Although you can create a public IP address as a stand alone object, you need to associate it to another object to actually use the address.</span></span> <span data-ttu-id="d15ed-104">U kunt een openbare IP-adres aan een load balancer, toepassingsgateway of een NIC die toegang tot het Internet op deze resources koppelen.</span><span class="sxs-lookup"><span data-stu-id="d15ed-104">You can associate a public IP address to a load balancer, application  gateway, or a NIC to provide Internet access to those resources.</span></span>  

| <span data-ttu-id="d15ed-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d15ed-105">Property</span></span> | <span data-ttu-id="d15ed-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d15ed-106">Description</span></span> | <span data-ttu-id="d15ed-107">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="d15ed-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d15ed-108">**publicIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="d15ed-108">**publicIPAllocationMethod**</span></span> |<span data-ttu-id="d15ed-109">Hiermee wordt aangegeven of het IP-adres *statische* of *dynamische*.</span><span class="sxs-lookup"><span data-stu-id="d15ed-109">Defines if the IP address is *static* or *dynamic*.</span></span> |<span data-ttu-id="d15ed-110">statisch, dynamische</span><span class="sxs-lookup"><span data-stu-id="d15ed-110">static, dynamic</span></span> |
| <span data-ttu-id="d15ed-111">**idleTimeoutInMinutes**</span><span class="sxs-lookup"><span data-stu-id="d15ed-111">**idleTimeoutInMinutes**</span></span> |<span data-ttu-id="d15ed-112">Hiermee definieert u de niet-actieve time-out met een standaardwaarde van vier minuten.</span><span class="sxs-lookup"><span data-stu-id="d15ed-112">Defines the idle time out, with a default value of 4 minutes.</span></span> <span data-ttu-id="d15ed-113">Als er geen meer pakketten voor een bepaalde sessie binnen deze tijd wordt ontvangen, wordt de sessie wordt beëindigd.</span><span class="sxs-lookup"><span data-stu-id="d15ed-113">If no more packets for a given session is received within this time, the session is terminated.</span></span> |<span data-ttu-id="d15ed-114">een waarde tussen 4 en 30 in</span><span class="sxs-lookup"><span data-stu-id="d15ed-114">any value between 4 and 30</span></span> |
| <span data-ttu-id="d15ed-115">**IP-adres**</span><span class="sxs-lookup"><span data-stu-id="d15ed-115">**ipAddress**</span></span> |<span data-ttu-id="d15ed-116">IP-adres is toegewezen aan een object.</span><span class="sxs-lookup"><span data-stu-id="d15ed-116">IP address assigned to object.</span></span> <span data-ttu-id="d15ed-117">Dit is een alleen-lezen eigenschap.</span><span class="sxs-lookup"><span data-stu-id="d15ed-117">This is a read-only property.</span></span> |<span data-ttu-id="d15ed-118">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="d15ed-118">104.42.233.77</span></span> |

### <a name="dns-settings"></a><span data-ttu-id="d15ed-119">DNS-instellingen</span><span class="sxs-lookup"><span data-stu-id="d15ed-119">DNS settings</span></span>
<span data-ttu-id="d15ed-120">Openbare IP-adressen hebben een onderliggend object met de naam **dnsSettings** met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d15ed-120">Public IP addresses have a child object named **dnsSettings** containing the following properties:</span></span>

| <span data-ttu-id="d15ed-121">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d15ed-121">Property</span></span> | <span data-ttu-id="d15ed-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d15ed-122">Description</span></span> | <span data-ttu-id="d15ed-123">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="d15ed-123">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d15ed-124">**domainNameLabel**</span><span class="sxs-lookup"><span data-stu-id="d15ed-124">**domainNameLabel**</span></span> |<span data-ttu-id="d15ed-125">Host met de naam gebruikt voor naamomzetting.</span><span class="sxs-lookup"><span data-stu-id="d15ed-125">Host named used for name resolution.</span></span> |<span data-ttu-id="d15ed-126">www-, ftp, vm1</span><span class="sxs-lookup"><span data-stu-id="d15ed-126">www, ftp, vm1</span></span> |
| <span data-ttu-id="d15ed-127">**FQDN-naam**</span><span class="sxs-lookup"><span data-stu-id="d15ed-127">**fqdn**</span></span> |<span data-ttu-id="d15ed-128">Volledig gekwalificeerde naam voor het openbare IP-adres.</span><span class="sxs-lookup"><span data-stu-id="d15ed-128">Fully qualified name for the public IP.</span></span> |<span data-ttu-id="d15ed-129">www.westus.cloudapp.Azure.com</span><span class="sxs-lookup"><span data-stu-id="d15ed-129">www.westus.cloudapp.azure.com</span></span> |
| <span data-ttu-id="d15ed-130">**reverseFqdn**</span><span class="sxs-lookup"><span data-stu-id="d15ed-130">**reverseFqdn**</span></span> |<span data-ttu-id="d15ed-131">FQDN-naam die wordt omgezet naar het IP-adres en is geregistreerd in DNS als een PTR-record.</span><span class="sxs-lookup"><span data-stu-id="d15ed-131">Fully qualified domain name that resolves to the IP address and is registered in DNS as a PTR record.</span></span> |<span data-ttu-id="d15ed-132">www.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d15ed-132">www.contoso.com.</span></span> |

<span data-ttu-id="d15ed-133">Voorbeeld openbare IP-adres in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="d15ed-133">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="d15ed-134">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="d15ed-134">Additional resources</span></span>
* <span data-ttu-id="d15ed-135">Vindt u meer informatie over [openbare IP-adressen](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="d15ed-135">Get more information about [public IP addresses](../articles/virtual-network/virtual-networks-reserved-public-ip.md).</span></span>
* <span data-ttu-id="d15ed-136">Meer informatie over [exemplaar niveau openbare IP-adressen](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span><span class="sxs-lookup"><span data-stu-id="d15ed-136">Learn about [instance level public IP addresses](../articles/virtual-network/virtual-networks-instance-level-public-ip.md).</span></span>
* <span data-ttu-id="d15ed-137">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163638.aspx) voor de openbare IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="d15ed-137">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163638.aspx) for public IP addresses.</span></span>

