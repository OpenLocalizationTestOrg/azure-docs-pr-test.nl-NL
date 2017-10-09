## <a name="nic"></a><span data-ttu-id="8cc5e-101">NIC</span><span class="sxs-lookup"><span data-stu-id="8cc5e-101">NIC</span></span>
<span data-ttu-id="8cc5e-102">Een network interface (netwerkinterfacekaart)-bron biedt connectiviteit tooan bestaande netwerksubnet in een VNet-resource.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-102">A network interface card (NIC) resource provides network connectivity tooan existing subnet in a VNet resource.</span></span> <span data-ttu-id="8cc5e-103">Hoewel u een NIC als zelfstandige object maken kunt, moet u tooassociate deze tooanother object tooactually connectiviteit bieden.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-103">Although you can create a NIC as a stand alone object, you need tooassociate it tooanother object tooactually provide connectivity.</span></span> <span data-ttu-id="8cc5e-104">Een NIC kan worden gebruikt tooconnect tooa VM-subnet, een openbare IP-adres of een load balancer.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-104">A NIC can be used tooconnect a VM tooa subnet, a public IP address, or a load balancer.</span></span>  

| <span data-ttu-id="8cc5e-105">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8cc5e-105">Property</span></span> | <span data-ttu-id="8cc5e-106">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8cc5e-106">Description</span></span> | <span data-ttu-id="8cc5e-107">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="8cc5e-107">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cc5e-108">**virtuele machine**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-108">**virtualMachine**</span></span> |<span data-ttu-id="8cc5e-109">VM Hallo NIC is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-109">VM hello NIC is associated with.</span></span> |<span data-ttu-id="8cc5e-110">/Subscriptions/{GUID}/../Microsoft.COMPUTE/virtualMachines/vm1</span><span class="sxs-lookup"><span data-stu-id="8cc5e-110">/subscriptions/{guid}/../Microsoft.Compute/virtualMachines/vm1</span></span> |
| <span data-ttu-id="8cc5e-111">**MAC-adres**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-111">**macAddress**</span></span> |<span data-ttu-id="8cc5e-112">MAC-adres voor Hallo NIC</span><span class="sxs-lookup"><span data-stu-id="8cc5e-112">MAC address for hello NIC</span></span> |<span data-ttu-id="8cc5e-113">een waarde tussen 4 en 30 in</span><span class="sxs-lookup"><span data-stu-id="8cc5e-113">any value between 4 and 30</span></span> |
| <span data-ttu-id="8cc5e-114">**networkSecurityGroup**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-114">**networkSecurityGroup**</span></span> |<span data-ttu-id="8cc5e-115">NSG die is gekoppeld toohello NIC</span><span class="sxs-lookup"><span data-stu-id="8cc5e-115">NSG associated toohello NIC</span></span> |<span data-ttu-id="8cc5e-116">/Subscriptions/{GUID}/../Microsoft.Network/networkSecurityGroups/myNSG1</span><span class="sxs-lookup"><span data-stu-id="8cc5e-116">/subscriptions/{guid}/../Microsoft.Network/networkSecurityGroups/myNSG1</span></span> |
| <span data-ttu-id="8cc5e-117">**dnsSettings**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-117">**dnsSettings**</span></span> |<span data-ttu-id="8cc5e-118">DNS-instellingen voor Hallo NIC</span><span class="sxs-lookup"><span data-stu-id="8cc5e-118">DNS settings for hello NIC</span></span> |<span data-ttu-id="8cc5e-119">Zie [PIP](#Public-IP-address)</span><span class="sxs-lookup"><span data-stu-id="8cc5e-119">see [PIP](#Public-IP-address)</span></span> |

<span data-ttu-id="8cc5e-120">Een Network Interface Card of NIC, vertegenwoordigt een netwerkinterface die gekoppeld tooa virtuele machine (VM worden kan).</span><span class="sxs-lookup"><span data-stu-id="8cc5e-120">A Network Interface Card, or NIC, represents a network interface that can be associated tooa virtual machine (VM).</span></span> <span data-ttu-id="8cc5e-121">Een virtuele machine kan een of meer NIC's hebben.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-121">A VM can have one or more NICs.</span></span>

![NIC's op een enkele virtuele machine](./media/resource-groups-networking/Figure3.png)

### <a name="ip-configurations"></a><span data-ttu-id="8cc5e-123">IP-configuraties</span><span class="sxs-lookup"><span data-stu-id="8cc5e-123">IP configurations</span></span>
<span data-ttu-id="8cc5e-124">NIC's hebben een onderliggend object met de naam **ipConfigurations** met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8cc5e-124">NICs have a child object named **ipConfigurations** containing hello following properties:</span></span>

| <span data-ttu-id="8cc5e-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8cc5e-125">Property</span></span> | <span data-ttu-id="8cc5e-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8cc5e-126">Description</span></span> | <span data-ttu-id="8cc5e-127">Voorbeeldwaarden</span><span class="sxs-lookup"><span data-stu-id="8cc5e-127">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cc5e-128">**subnet**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-128">**subnet**</span></span> |<span data-ttu-id="8cc5e-129">Subnet Hallo NIC is onnected aan.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-129">Subnet hello NIC is onnected to.</span></span> |<span data-ttu-id="8cc5e-130">/Subscriptions/{GUID}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span><span class="sxs-lookup"><span data-stu-id="8cc5e-130">/subscriptions/{guid}/../Microsoft.Network/virtualNetworks/myvnet1/subnets/mysub1</span></span> |
| <span data-ttu-id="8cc5e-131">**privateIPAddress**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-131">**privateIPAddress**</span></span> |<span data-ttu-id="8cc5e-132">IP-adres voor Hallo NIC in Hallo subnet</span><span class="sxs-lookup"><span data-stu-id="8cc5e-132">IP address for hello NIC in hello subnet</span></span> |<span data-ttu-id="8cc5e-133">10.0.0.8</span><span class="sxs-lookup"><span data-stu-id="8cc5e-133">10.0.0.8</span></span> |
| <span data-ttu-id="8cc5e-134">**privateIPAllocationMethod**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-134">**privateIPAllocationMethod**</span></span> |<span data-ttu-id="8cc5e-135">IP-toewijzingsmethode</span><span class="sxs-lookup"><span data-stu-id="8cc5e-135">IP allocation method</span></span> |<span data-ttu-id="8cc5e-136">Dynamische of statische</span><span class="sxs-lookup"><span data-stu-id="8cc5e-136">Dynamic or Static</span></span> |
| <span data-ttu-id="8cc5e-137">**enableIPForwarding**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-137">**enableIPForwarding**</span></span> |<span data-ttu-id="8cc5e-138">Hiermee wordt aangegeven of Hallo NIC kan worden gebruikt voor routering</span><span class="sxs-lookup"><span data-stu-id="8cc5e-138">Whether hello NIC can be used for routing</span></span> |<span data-ttu-id="8cc5e-139">waar of ONWAAR</span><span class="sxs-lookup"><span data-stu-id="8cc5e-139">true or false</span></span> |
| <span data-ttu-id="8cc5e-140">**primaire**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-140">**primary**</span></span> |<span data-ttu-id="8cc5e-141">Of NIC Hallo Hallo primaire NIC voor Hallo VM</span><span class="sxs-lookup"><span data-stu-id="8cc5e-141">Whether hello NIC is hello primary NIC for hello VM</span></span> |<span data-ttu-id="8cc5e-142">waar of ONWAAR</span><span class="sxs-lookup"><span data-stu-id="8cc5e-142">true or false</span></span> |
| <span data-ttu-id="8cc5e-143">**publicIPAddress**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-143">**publicIPAddress**</span></span> |<span data-ttu-id="8cc5e-144">PIP Hallo NIC gekoppeld</span><span class="sxs-lookup"><span data-stu-id="8cc5e-144">PIP associated with hello NIC</span></span> |<span data-ttu-id="8cc5e-145">Zie [DNS-instellingen](#DNS-settings)</span><span class="sxs-lookup"><span data-stu-id="8cc5e-145">see [DNS Settings](#DNS-settings)</span></span> |
| <span data-ttu-id="8cc5e-146">**loadbalancerbackendaddresspools gebruikt**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-146">**loadBalancerBackendAddressPools**</span></span> |<span data-ttu-id="8cc5e-147">Back-end adres pools Hallo die NIC is gekoppeld aan</span><span class="sxs-lookup"><span data-stu-id="8cc5e-147">Back end address pools hello NIC is associated with</span></span> | |
| <span data-ttu-id="8cc5e-148">**loadBalancerInboundNatRules**</span><span class="sxs-lookup"><span data-stu-id="8cc5e-148">**loadBalancerInboundNatRules**</span></span> |<span data-ttu-id="8cc5e-149">Inkomende load balancer NAT-regels Hallo die NIC is gekoppeld aan</span><span class="sxs-lookup"><span data-stu-id="8cc5e-149">Inbound load balancer NAT rules hello NIC is associated with</span></span> | |

<span data-ttu-id="8cc5e-150">Voorbeeld openbare IP-adres in JSON-indeling:</span><span class="sxs-lookup"><span data-stu-id="8cc5e-150">Sample public IP address in JSON format:</span></span>

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

### <a name="additional-resources"></a><span data-ttu-id="8cc5e-151">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8cc5e-151">Additional resources</span></span>
* <span data-ttu-id="8cc5e-152">Lees Hallo [REST-API-naslagdocumentatie](https://msdn.microsoft.com/library/azure/mt163579.aspx) voor NIC's.</span><span class="sxs-lookup"><span data-stu-id="8cc5e-152">Read hello [REST API reference documentation](https://msdn.microsoft.com/library/azure/mt163579.aspx) for NICs.</span></span>

