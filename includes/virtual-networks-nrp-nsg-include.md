## <a name="network-security-group"></a><span data-ttu-id="af9fe-101">Netwerkbeveiligingsgroep</span><span class="sxs-lookup"><span data-stu-id="af9fe-101">Network Security Group</span></span>
<span data-ttu-id="af9fe-102">Een NSG-resource wordt Hallo maken van een beveiligingsgrens voor werkbelastingen, door het implementeren van toestaan en weigeren regels.</span><span class="sxs-lookup"><span data-stu-id="af9fe-102">An NSG resource enables hello creation of security boundary for workloads, by implementing allow and deny rules.</span></span> <span data-ttu-id="af9fe-103">Deze regels kunnen worden toegepast tooa VM, een NIC of een subnet.</span><span class="sxs-lookup"><span data-stu-id="af9fe-103">Such rules can be applied tooa VM, a NIC, or a subnet.</span></span>

| <span data-ttu-id="af9fe-104">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="af9fe-104">Property</span></span> | <span data-ttu-id="af9fe-105">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="af9fe-105">Description</span></span> | <span data-ttu-id="af9fe-106">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="af9fe-106">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af9fe-107">**subnetten**</span><span class="sxs-lookup"><span data-stu-id="af9fe-107">**subnets**</span></span> |<span data-ttu-id="af9fe-108">Lijst met subnet-id's Hallo die NSG wordt toegepast op.</span><span class="sxs-lookup"><span data-stu-id="af9fe-108">List of subnet ids hello NSG is applied to.</span></span> |<span data-ttu-id="af9fe-109">/Subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span><span class="sxs-lookup"><span data-stu-id="af9fe-109">/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd</span></span> |
| <span data-ttu-id="af9fe-110">**securityRules**</span><span class="sxs-lookup"><span data-stu-id="af9fe-110">**securityRules**</span></span> |<span data-ttu-id="af9fe-111">Lijst met beveiligingsregels voor verbindingen die gezamenlijk Hallo NSG</span><span class="sxs-lookup"><span data-stu-id="af9fe-111">List of security rules that make up hello NSG</span></span> |<span data-ttu-id="af9fe-112">Zie [beveiligingsregel](#Security-rule) hieronder</span><span class="sxs-lookup"><span data-stu-id="af9fe-112">See [Security rule](#Security-rule) below</span></span> |
| <span data-ttu-id="af9fe-113">**defaultSecurityRules**</span><span class="sxs-lookup"><span data-stu-id="af9fe-113">**defaultSecurityRules**</span></span> |<span data-ttu-id="af9fe-114">Lijst met beveiligingsregels standaard aanwezig zijn in elke NSG</span><span class="sxs-lookup"><span data-stu-id="af9fe-114">List of default security rules present in every NSG</span></span> |<span data-ttu-id="af9fe-115">Zie [standaard beveiligingsregels](#Default-security-rules) hieronder</span><span class="sxs-lookup"><span data-stu-id="af9fe-115">See [Default security rules](#Default-security-rules) below</span></span> |

* <span data-ttu-id="af9fe-116">**De beveiligingsregel** -meerdere regels gedefinieerd door een NSG kan hebben.</span><span class="sxs-lookup"><span data-stu-id="af9fe-116">**Security rule** - An NSG can have multiple security rules defined.</span></span> <span data-ttu-id="af9fe-117">Elke regel kunt toestaan of weigeren van verschillende typen verkeer.</span><span class="sxs-lookup"><span data-stu-id="af9fe-117">Each rule can allow or deny different types of traffic.</span></span>

### <a name="security-rule"></a><span data-ttu-id="af9fe-118">De beveiligingsregel</span><span class="sxs-lookup"><span data-stu-id="af9fe-118">Security rule</span></span>
<span data-ttu-id="af9fe-119">Een beveiligingsregel is een onderliggende resource van een NSG met Hallo eigenschappen hieronder.</span><span class="sxs-lookup"><span data-stu-id="af9fe-119">A security rule is a child resource of an NSG containing hello properties below.</span></span>

| <span data-ttu-id="af9fe-120">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="af9fe-120">Property</span></span> | <span data-ttu-id="af9fe-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="af9fe-121">Description</span></span> | <span data-ttu-id="af9fe-122">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="af9fe-122">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af9fe-123">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="af9fe-123">**description**</span></span> |<span data-ttu-id="af9fe-124">Beschrijving voor de regel Hallo</span><span class="sxs-lookup"><span data-stu-id="af9fe-124">Description for hello rule</span></span> |<span data-ttu-id="af9fe-125">Binnenkomend verkeer toestaan voor alle VM's in het subnet X</span><span class="sxs-lookup"><span data-stu-id="af9fe-125">Allow inbound traffic for all VMs in subnet X</span></span> |
| <span data-ttu-id="af9fe-126">**Protocol**</span><span class="sxs-lookup"><span data-stu-id="af9fe-126">**protocol**</span></span> |<span data-ttu-id="af9fe-127">Protocol toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-127">Protocol toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-128">TCP, UDP of *</span><span class="sxs-lookup"><span data-stu-id="af9fe-128">TCP, UDP, or *</span></span> |
| <span data-ttu-id="af9fe-129">**sourcePortRange**</span><span class="sxs-lookup"><span data-stu-id="af9fe-129">**sourcePortRange**</span></span> |<span data-ttu-id="af9fe-130">Bron poort bereik toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-130">Source port range toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-131">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="af9fe-131">80, 100-200, *</span></span> |
| <span data-ttu-id="af9fe-132">**destinationPortRange**</span><span class="sxs-lookup"><span data-stu-id="af9fe-132">**destinationPortRange**</span></span> |<span data-ttu-id="af9fe-133">Bestemming poort bereik toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-133">Destination port range toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-134">80, 100-200, *</span><span class="sxs-lookup"><span data-stu-id="af9fe-134">80, 100-200, *</span></span> |
| <span data-ttu-id="af9fe-135">**sourceAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="af9fe-135">**sourceAddressPrefix**</span></span> |<span data-ttu-id="af9fe-136">Bron adres voorvoegsel toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-136">Source address prefix toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="af9fe-137">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="af9fe-138">**destinationAddressPrefix**</span><span class="sxs-lookup"><span data-stu-id="af9fe-138">**destinationAddressPrefix**</span></span> |<span data-ttu-id="af9fe-139">Bestemming adres voorvoegsel toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-139">Destination address prefix toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="af9fe-140">10.10.10.1, 10.10.10.0/24, VirtualNetwork</span></span> |
| <span data-ttu-id="af9fe-141">**richting**</span><span class="sxs-lookup"><span data-stu-id="af9fe-141">**direction**</span></span> |<span data-ttu-id="af9fe-142">Richting van verkeer toomatch voor Hallo regel</span><span class="sxs-lookup"><span data-stu-id="af9fe-142">Direction of traffic toomatch for hello rule</span></span> |<span data-ttu-id="af9fe-143">binnenkomend of uitgaand</span><span class="sxs-lookup"><span data-stu-id="af9fe-143">inbound or outbound</span></span> |
| <span data-ttu-id="af9fe-144">**prioriteit**</span><span class="sxs-lookup"><span data-stu-id="af9fe-144">**priority**</span></span> |<span data-ttu-id="af9fe-145">Prioriteit voor het Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="af9fe-145">Priority for hello rule.</span></span> <span data-ttu-id="af9fe-146">Regels worden gecontroleerd op volgorde van prioriteit, wanneer een regel van toepassing is, geen regels meer getest voor matching.</span><span class="sxs-lookup"><span data-stu-id="af9fe-146">Rules are checked int he order of priority, once a rule applies, no more rules are tested for matching.</span></span> |<span data-ttu-id="af9fe-147">10, 100, 65000</span><span class="sxs-lookup"><span data-stu-id="af9fe-147">10, 100, 65000</span></span> |
| <span data-ttu-id="af9fe-148">**toegang**</span><span class="sxs-lookup"><span data-stu-id="af9fe-148">**access**</span></span> |<span data-ttu-id="af9fe-149">Type toegang tooapply als Hallo regel matcht</span><span class="sxs-lookup"><span data-stu-id="af9fe-149">Type of access tooapply if hello rule matches</span></span> |<span data-ttu-id="af9fe-150">toestaan of weigeren</span><span class="sxs-lookup"><span data-stu-id="af9fe-150">allow or deny</span></span> |

<span data-ttu-id="af9fe-151">Voorbeeld NSG in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="af9fe-151">Sample NSG in JSON format:</span></span>

    {
        "name": "NSG-BackEnd",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkSecurityGroups",
        "location": "westus",
        "tags": {
            "displayName": "NSG - Front End"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "securityRules": [
                {
                    "name": "rdp-rule",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd/securityRules/rdp-rule",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "description": "Allow RDP",
                        "protocol": "Tcp",
                        "sourcePortRange": "*",
                        "destinationPortRange": "3389",
                        "sourceAddressPrefix": "Internet",
                        "destinationAddressPrefix": "*",
                        "access": "Allow",
                        "priority": 100,
                        "direction": "Inbound"
                    }
                }
            ],
            "defaultSecurityRules": [
                { [...],
            "subnets": [
                {
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                }
            ]
        }
    }

### <a name="default-security-rules"></a><span data-ttu-id="af9fe-152">Standaardbeveiligingsregels</span><span class="sxs-lookup"><span data-stu-id="af9fe-152">Default security rules</span></span>

<span data-ttu-id="af9fe-153">Standaard-Beveiligingsregels hebben Hallo dezelfde eigenschappen beschikbaar zijn in de beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-153">Default security rules have hello same properties available in security rules.</span></span> <span data-ttu-id="af9fe-154">Deze bestaan tooprovide basisconnectiviteit tussen resources met nsg's toegepast toothem een.</span><span class="sxs-lookup"><span data-stu-id="af9fe-154">They exist tooprovide basic connectivity between resources that have NSGs applied toothem.</span></span> <span data-ttu-id="af9fe-155">Zorg ervoor dat u weet welk [standaard beveiligingsregels](../articles/virtual-network/virtual-networks-nsg.md#default-rules) bestaan.</span><span class="sxs-lookup"><span data-stu-id="af9fe-155">Make sure you know which [default security rules](../articles/virtual-network/virtual-networks-nsg.md#default-rules) exist.</span></span>

### <a name="additional-resources"></a><span data-ttu-id="af9fe-156">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="af9fe-156">Additional resources</span></span>
* <span data-ttu-id="af9fe-157">Vindt u meer informatie over [nsg's](../articles/virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="af9fe-157">Get more information about [NSGs](../articles/virtual-network/virtual-networks-nsg.md).</span></span>
* <span data-ttu-id="af9fe-158">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163615.aspx) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="af9fe-158">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163615.aspx) for NSGs.</span></span>
* <span data-ttu-id="af9fe-159">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163580.aspx) voor beveiligingsregels voor verbindingen.</span><span class="sxs-lookup"><span data-stu-id="af9fe-159">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163580.aspx) for security rules.</span></span>
