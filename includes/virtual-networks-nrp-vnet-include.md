## <a name="virtual-network"></a><span data-ttu-id="686f1-101">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="686f1-101">Virtual Network</span></span>
<span data-ttu-id="686f1-102">Virtuele netwerken (VNET) en subnetten bronnen het definiëren van een beveiligingsgrens voor werkbelastingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="686f1-102">Virtual Networks (VNET) and subnets resources help define a security boundary for workloads running in Azure.</span></span> <span data-ttu-id="686f1-103">Een VNet wordt gekenmerkt door een verzameling van adresruimten, gedefinieerd als CIDR-blokken.</span><span class="sxs-lookup"><span data-stu-id="686f1-103">A VNet is characterized by a collection of address spaces, defined as CIDR blocks.</span></span> 

> [!NOTE]
> <span data-ttu-id="686f1-104">Netwerkbeheerders bent bekend met CIDR-notatie.</span><span class="sxs-lookup"><span data-stu-id="686f1-104">Network administrators are familiar with CIDR notation.</span></span> <span data-ttu-id="686f1-105">Als u niet bekend met CIDR bent, [meer informatie over het](http://whatismyipaddress.com/cidr).</span><span class="sxs-lookup"><span data-stu-id="686f1-105">If you are not familiar with CIDR, [learn more about it](http://whatismyipaddress.com/cidr).</span></span>
> 
> 

![VNet met meerdere subnetten](./media/resource-groups-networking/Figure4.png)

<span data-ttu-id="686f1-107">Vnet's bevatten de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="686f1-107">VNets contain the following properties.</span></span>

| <span data-ttu-id="686f1-108">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="686f1-108">Property</span></span> | <span data-ttu-id="686f1-109">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="686f1-109">Description</span></span> | <span data-ttu-id="686f1-110">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="686f1-110">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="686f1-111">**de addressSpace**</span><span class="sxs-lookup"><span data-stu-id="686f1-111">**addressSpace**</span></span> |<span data-ttu-id="686f1-112">Verzameling van adresvoorvoegsels waaruit het VNet in CIDR-notatie</span><span class="sxs-lookup"><span data-stu-id="686f1-112">Collection of address prefixes that make up the VNet in CIDR notation</span></span> |<span data-ttu-id="686f1-113">192.168.0.0/16</span><span class="sxs-lookup"><span data-stu-id="686f1-113">192.168.0.0/16</span></span> |
| <span data-ttu-id="686f1-114">**subnetten**</span><span class="sxs-lookup"><span data-stu-id="686f1-114">**subnets**</span></span> |<span data-ttu-id="686f1-115">Verzameling van subnetten die gezamenlijk de VNet</span><span class="sxs-lookup"><span data-stu-id="686f1-115">Collection of subnets that make up the VNet</span></span> |<span data-ttu-id="686f1-116">Zie [subnetten](#Subnets) hieronder.</span><span class="sxs-lookup"><span data-stu-id="686f1-116">see [subnets](#Subnets) below.</span></span> |
| <span data-ttu-id="686f1-117">**IP-adres**</span><span class="sxs-lookup"><span data-stu-id="686f1-117">**ipAddress**</span></span> |<span data-ttu-id="686f1-118">IP-adres is toegewezen aan een object.</span><span class="sxs-lookup"><span data-stu-id="686f1-118">IP address assigned to object.</span></span> <span data-ttu-id="686f1-119">Dit is een alleen-lezen eigenschap.</span><span class="sxs-lookup"><span data-stu-id="686f1-119">This is a read-only property.</span></span> |<span data-ttu-id="686f1-120">104.42.233.77</span><span class="sxs-lookup"><span data-stu-id="686f1-120">104.42.233.77</span></span> |

### <a name="subnets"></a><span data-ttu-id="686f1-121">Subnetten</span><span class="sxs-lookup"><span data-stu-id="686f1-121">Subnets</span></span>
<span data-ttu-id="686f1-122">Een subnet is een onderliggende resource van een VNet en helpt bij het segmenten van adresruimten binnen een CIDR-blok met behulp van IP-adresvoorvoegsels definiëren.</span><span class="sxs-lookup"><span data-stu-id="686f1-122">A subnet is a child resource of a VNet, and helps define segments of address spaces within a CIDR block, using IP address prefixes.</span></span> <span data-ttu-id="686f1-123">NIC's worden toegevoegd aan subnetten en verbonden met virtuele machines, tegelijk connectiviteit biedt voor verschillende werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="686f1-123">NICs can be added to subnets, and connected to VMs, providing connectivity for various workloads.</span></span>

<span data-ttu-id="686f1-124">Subnetten bevatten de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="686f1-124">Subnets contain the following properties.</span></span> 

| <span data-ttu-id="686f1-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="686f1-125">Property</span></span> | <span data-ttu-id="686f1-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="686f1-126">Description</span></span> | <span data-ttu-id="686f1-127">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="686f1-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="686f1-128">**addressPrefix**</span><span class="sxs-lookup"><span data-stu-id="686f1-128">**addressPrefix**</span></span> |<span data-ttu-id="686f1-129">Één adresvoorvoegsel waaruit het subnet in CIDR-notatie</span><span class="sxs-lookup"><span data-stu-id="686f1-129">Single address prefix that make up the subnet in CIDR notation</span></span> |<span data-ttu-id="686f1-130">192.168.1.0/24</span><span class="sxs-lookup"><span data-stu-id="686f1-130">192.168.1.0/24</span></span> |
| <span data-ttu-id="686f1-131">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="686f1-131">**networkSecurityGroup**</span></span> |<span data-ttu-id="686f1-132">NSG wordt toegepast op het subnet</span><span class="sxs-lookup"><span data-stu-id="686f1-132">NSG applied to the subnet</span></span> |<span data-ttu-id="686f1-133">Zie [nsg's](#Network-Security-Group)</span><span class="sxs-lookup"><span data-stu-id="686f1-133">see [NSGs](#Network-Security-Group)</span></span> |
| <span data-ttu-id="686f1-134">**Migratiestatus**</span><span class="sxs-lookup"><span data-stu-id="686f1-134">**routeTable**</span></span> |<span data-ttu-id="686f1-135">De routetabel is toegepast op het subnet</span><span class="sxs-lookup"><span data-stu-id="686f1-135">Route table applied to the subnet</span></span> |<span data-ttu-id="686f1-136">Zie [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="686f1-136">see [UDR](#Route-table)</span></span> |
| <span data-ttu-id="686f1-137">**ipConfigurations**</span><span class="sxs-lookup"><span data-stu-id="686f1-137">**ipConfigurations**</span></span> |<span data-ttu-id="686f1-138">Verzameling van IP-configruation objecten die worden gebruikt door de NIC's die zijn verbonden met het subnet</span><span class="sxs-lookup"><span data-stu-id="686f1-138">Collection of IP configruation objects used by NICs connected to the subnet</span></span> |<span data-ttu-id="686f1-139">Zie [UDR](#Route-table)</span><span class="sxs-lookup"><span data-stu-id="686f1-139">see [UDR](#Route-table)</span></span> |

<span data-ttu-id="686f1-140">Voorbeeld VNet in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="686f1-140">Sample VNet in JSON format:</span></span>

    {
        "name": "TestVNet",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/virtualNetworks",
        "location": "westus",
        "tags": {
            "displayName": "VNet"
        },
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "addressSpace": {
                "addressPrefixes": [
                    "192.168.0.0/16"
                ]
            },
            "subnets": [
                {
                    "name": "FrontEnd",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                    "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "addressPrefix": "192.168.1.0/24",
                        "networkSecurityGroup": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-BackEnd"
                        },
                        "routeTable": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/routeTables/UDR-FrontEnd"
                        },
                        "ipConfigurations": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConfigurations/ipconfig1"
                            },
                            ...]
                    }
                },
                ...]
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="686f1-141">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="686f1-141">Additional resources</span></span>
* <span data-ttu-id="686f1-142">Vindt u meer informatie over [VNet](../articles/virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="686f1-142">Get more information about [VNet](../articles/virtual-network/virtual-networks-overview.md).</span></span>
* <span data-ttu-id="686f1-143">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163650.aspx) voor VNets.</span><span class="sxs-lookup"><span data-stu-id="686f1-143">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163650.aspx) for VNets.</span></span>
* <span data-ttu-id="686f1-144">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163618.aspx) voor subnetten.</span><span class="sxs-lookup"><span data-stu-id="686f1-144">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163618.aspx) for Subnets.</span></span>

