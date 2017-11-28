## <a name="nic"></a><span data-ttu-id="08aa6-101">NIC</span><span class="sxs-lookup"><span data-stu-id="08aa6-101">NIC</span></span>
<span data-ttu-id="08aa6-102">Een bron-interface (netwerkinterfacekaart) biedt een netwerkverbinding met een bestaand subnet in een VNet-resource.</span><span class="sxs-lookup"><span data-stu-id="08aa6-102">A network interface card (NIC) resource provides network connectivity to an existing subnet in a VNet resource.</span></span> <span data-ttu-id="08aa6-103">Hoewel u een NIC als zelfstandige object maken kunt, moet u deze koppelen aan een ander object daadwerkelijk om verbinding te bieden.</span><span class="sxs-lookup"><span data-stu-id="08aa6-103">Although you can create a NIC as a stand alone object, you need to associate it to another object to actually provide connectivity.</span></span> <span data-ttu-id="08aa6-104">Een NIC kan worden gebruikt om een virtuele machine met een subnet, een openbare IP-adres of een load balancer.</span><span class="sxs-lookup"><span data-stu-id="08aa6-104">A NIC can be used to connect a VM to a subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="08aa6-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="08aa6-105">Property</span></span> | <span data-ttu-id="08aa6-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="08aa6-106">Description</span></span> | <span data-ttu-id="08aa6-107">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="08aa6-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa6-108">**virtuele machine**</span><span class="sxs-lookup"><span data-stu-id="08aa6-108">**virtualMachine**</span></span> |<span data-ttu-id="08aa6-109">Virtuele machine de NIC is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="08aa6-109">VM the NIC is associated with.</span></span> |<span data-ttu-id="08aa6-110">/Subscriptions/{GUID}/../Microsoft.COMPUTE/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="08aa6-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="08aa6-111">**MAC-adres**</span><span class="sxs-lookup"><span data-stu-id="08aa6-111">**macAddress**</span></span> |<span data-ttu-id="08aa6-112">MAC-adres voor de NIC</span><span class="sxs-lookup"><span data-stu-id="08aa6-112">MAC address for the NIC</span></span> |<span data-ttu-id="08aa6-113">een waarde tussen 4 en 30 in</span><span class="sxs-lookup"><span data-stu-id="08aa6-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="08aa6-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="08aa6-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="08aa6-115">NSG die is gekoppeld naar de NIC.</span><span class="sxs-lookup"><span data-stu-id="08aa6-115">NSG associated to the NIC</span></span> |<span data-ttu-id="08aa6-116">/Subscriptions/{GUID}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="08aa6-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="08aa6-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="08aa6-117">**dnsSettings**</span></span> |<span data-ttu-id="08aa6-118">DNS-instellingen voor de NIC</span><span class="sxs-lookup"><span data-stu-id="08aa6-118">DNS settings for the NIC</span></span> |<span data-ttu-id="08aa6-119">Zie [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="08aa6-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="08aa6-120">Een Network Interface Card of NIC, vertegenwoordigt een netwerkinterface die gekoppeld aan een virtuele machine (VM worden kan).</span><span class="sxs-lookup"><span data-stu-id="08aa6-120">A Network Interface Card, or NIC, represents a network interface that can be associated to a virtual machine (VM).</span></span> <span data-ttu-id="08aa6-121">Een virtuele machine kan een of meer NIC's hebben.</span><span class="sxs-lookup"><span data-stu-id="08aa6-121">A VM can have one or more NICs.</span></span>

![NIC's op een enkele virtuele machine](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="08aa6-123">IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="08aa6-123">IP configurations</span></span>
<span data-ttu-id="08aa6-124">NIC's hebben een onderliggend object met de naam **ipConfigurations** met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="08aa6-124">NICs have a child object named **ipConfigurations** containing the following properties:</span></span>

| <span data-ttu-id="08aa6-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="08aa6-125">Property</span></span> | <span data-ttu-id="08aa6-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="08aa6-126">Description</span></span> | <span data-ttu-id="08aa6-127">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="08aa6-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08aa6-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="08aa6-128">**subnet**</span></span> |<span data-ttu-id="08aa6-129">Subnet van de NIC is onnected aan.</span><span class="sxs-lookup"><span data-stu-id="08aa6-129">Subnet the NIC is onnected to.</span></span> |<span data-ttu-id="08aa6-130">/Subscriptions/{GUID}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="08aa6-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="08aa6-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="08aa6-131">**privateIPAddress**</span></span> |<span data-ttu-id="08aa6-132">IP-adres voor de NIC in het subnet</span><span class="sxs-lookup"><span data-stu-id="08aa6-132">IP address for the NIC in the subnet</span></span> |<span data-ttu-id="08aa6-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="08aa6-133">10.0.0.8</span></span> |
| <span data-ttu-id="08aa6-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="08aa6-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="08aa6-135">IP-toewijzingsmethode</span><span class="sxs-lookup"><span data-stu-id="08aa6-135">IP allocation method</span></span> |<span data-ttu-id="08aa6-136">Dynamische of statische</span><span class="sxs-lookup"><span data-stu-id="08aa6-136">Dynamic or Static</span></span> |
| <span data-ttu-id="08aa6-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="08aa6-137">**enableIPForwarding**</span></span> |<span data-ttu-id="08aa6-138">Hiermee wordt aangegeven of de NIC kan worden gebruikt voor routering</span><span class="sxs-lookup"><span data-stu-id="08aa6-138">Whether the NIC can be used for routing</span></span> |<span data-ttu-id="08aa6-139">waar of ONWAAR</span><span class="sxs-lookup"><span data-stu-id="08aa6-139">true or false</span></span> |
| <span data-ttu-id="08aa6-140">**primaire**</span><span class="sxs-lookup"><span data-stu-id="08aa6-140">**primary**</span></span> |<span data-ttu-id="08aa6-141">Hiermee wordt aangegeven of de NIC is de primaire NIC voor de virtuele machine</span><span class="sxs-lookup"><span data-stu-id="08aa6-141">Whether the NIC is the primary NIC for the VM</span></span> |<span data-ttu-id="08aa6-142">waar of ONWAAR</span><span class="sxs-lookup"><span data-stu-id="08aa6-142">true or false</span></span> |
| <span data-ttu-id="08aa6-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="08aa6-143">**publicIPAddress**</span></span> |<span data-ttu-id="08aa6-144">PIP die zijn gekoppeld aan de NIC</span><span class="sxs-lookup"><span data-stu-id="08aa6-144">PIP associated with the NIC</span></span> |<span data-ttu-id="08aa6-145">Zie [DNS-instellingen](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="08aa6-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="08aa6-146">**loadbalancerbackendaddresspools gebruikt**</span><span class="sxs-lookup"><span data-stu-id="08aa6-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="08aa6-147">Back-end-adresgroepen die de NIC is gekoppeld</span><span class="sxs-lookup"><span data-stu-id="08aa6-147">Back end address pools the NIC is associated with</span></span> | |
| <span data-ttu-id="08aa6-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="08aa6-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="08aa6-149">Binnenkomende NAT-regels voor load balancer is die de NIC is gekoppeld aan</span><span class="sxs-lookup"><span data-stu-id="08aa6-149">Inbound load balancer NAT rules the NIC is associated with</span></span> | |

<span data-ttu-id="08aa6-150">Voorbeeld openbare IP-adres in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="08aa6-150">Sample public IP address in JSON format:</span></span>

    {
        "name": "lb-nic1-be",
        "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be",
        "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"",
        "type": "Microsoft.Network/networkInterfaces",
        "location": "eastus",
        "properties": {
            "provisioningState": "Succeeded",
            "resourceGuid": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
            "ipConfigurations": [
                {
                    "name": "NIC-config",
                    "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be/ipConfigurations/NIC-config",
                    "etag": "W/\"0027f1a2-3ac8-49de-b5d5-fd46550500b1\"",
                    "properties": {
                        "provisioningState": "Succeeded",
                        "privateIPAddress": "10.0.0.4",
                        "privateIPAllocationMethod": "Dynamic",
                        "subnet": {
                            "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet"
                        },
                        "loadBalancerBackendAddressPools": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool"
                            }
                        ],
                        "loadBalancerInboundNatRules": [
                            {
                                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1"
                            }
                        ]
                    }
                }
            ],
            "dnsSettings": { ... },
            "macAddress": "00-0D-3A-10-F1-29",
            "enableIPForwarding": false,
            "primary": true,
            "virtualMachine": {
                "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/nrprg/providers/Microsoft.Compute/virtualMachines/web1"
            }
        }
    }

### <a name="additional-resources"></a><span data-ttu-id="08aa6-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="08aa6-151">Additional resources</span></span>
* <span data-ttu-id="08aa6-152">Lees de [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163579.aspx) voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="08aa6-152">Read the [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

