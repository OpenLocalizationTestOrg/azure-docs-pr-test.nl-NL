---
title: aaaNetworking patronen voor Azure Service Fabric | Microsoft Docs
description: Beschrijving van algemene patronen voor netwerken voor Service Fabric en hoe toocreate een cluster met behulp van Azure-netwerkfuncties.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a><span data-ttu-id="ff80e-103">Service Fabric netwerken patronen</span><span class="sxs-lookup"><span data-stu-id="ff80e-103">Service Fabric networking patterns</span></span>
<span data-ttu-id="ff80e-104">U kunt uw Azure Service Fabric-cluster integreren met andere Azure-netwerkfuncties.</span><span class="sxs-lookup"><span data-stu-id="ff80e-104">You can integrate your Azure Service Fabric cluster with other Azure networking features.</span></span> <span data-ttu-id="ff80e-105">In dit artikel zien we u hoe toocreate clusters die gebruik Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="ff80e-105">In this article, we show you how toocreate clusters that use hello following features:</span></span>

- [<span data-ttu-id="ff80e-106">Bestaand virtueel netwerk of subnet</span><span class="sxs-lookup"><span data-stu-id="ff80e-106">Existing virtual network or subnet</span></span>](#existingvnet)
- [<span data-ttu-id="ff80e-107">Statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="ff80e-107">Static public IP address</span></span>](#staticpublicip)
- [<span data-ttu-id="ff80e-108">Alleen voor interne load balancer</span><span class="sxs-lookup"><span data-stu-id="ff80e-108">Internal-only load balancer</span></span>](#internallb)
- [<span data-ttu-id="ff80e-109">Interne en externe load balancer</span><span class="sxs-lookup"><span data-stu-id="ff80e-109">Internal and external load balancer</span></span>](#internalexternallb)

<span data-ttu-id="ff80e-110">Service Fabric wordt uitgevoerd in een standaard virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="ff80e-110">Service Fabric runs in a standard virtual machine scale set.</span></span> <span data-ttu-id="ff80e-111">Functionaliteit die u in een virtuele-machineschaalset gebruiken kunt, kunt u met een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="ff80e-111">Any functionality that you can use in a virtual machine scale set, you can use with a Service Fabric cluster.</span></span> <span data-ttu-id="ff80e-112">Hallo netwerken secties met hello Azure Resource Manager-sjablonen voor virtuele-machineschaalsets en Service Fabric zijn identiek.</span><span class="sxs-lookup"><span data-stu-id="ff80e-112">hello networking sections of hello Azure Resource Manager templates for virtual machine scale sets and Service Fabric are identical.</span></span> <span data-ttu-id="ff80e-113">Nadat u tooan bestaande virtuele netwerk implementeert, is het eenvoudig tooincorporate andere netwerkfuncties, zoals Azure ExpressRoute, Azure VPN-Gateway, een netwerkbeveiligingsgroep en virtueel netwerk peering.</span><span class="sxs-lookup"><span data-stu-id="ff80e-113">After you deploy tooan existing virtual network, it's easy tooincorporate other networking features, like Azure ExpressRoute, Azure VPN Gateway, a network security group, and virtual network peering.</span></span>

<span data-ttu-id="ff80e-114">Service Fabric is uniek in vergelijking met andere netwerkfuncties in één aspect.</span><span class="sxs-lookup"><span data-stu-id="ff80e-114">Service Fabric is unique from other networking features in one aspect.</span></span> <span data-ttu-id="ff80e-115">Hallo [Azure-portal](https://portal.azure.com) intern gebruikt Hallo Service Fabric resource provider toocall tooa cluster tooget informatie over de knooppunten en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-115">hello [Azure portal](https://portal.azure.com) internally uses hello Service Fabric resource provider toocall tooa cluster tooget information about nodes and applications.</span></span> <span data-ttu-id="ff80e-116">Hallo Service Fabric-resourceprovider vereist openbaar toegankelijk binnenkomende toegang toohello HTTP gateway poort (standaard poort 19080,) op Hallo management eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-116">hello Service Fabric resource provider requires publicly accessible inbound access toohello HTTP gateway port (port 19080, by default) on hello management endpoint.</span></span> <span data-ttu-id="ff80e-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) gebruikt Hallo management eindpunt toomanage uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ff80e-117">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) uses hello management endpoint toomanage your cluster.</span></span> <span data-ttu-id="ff80e-118">Hallo Service Fabric-resourceprovider gebruikt ook deze poort tooquery informatie over uw cluster, toodisplay in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="ff80e-118">hello Service Fabric resource provider also uses this port tooquery information about your cluster, toodisplay in hello Azure portal.</span></span> 

<span data-ttu-id="ff80e-119">Als poort 19080 is niet toegankelijk is vanaf Hallo Service Fabric-resourceprovider, een bericht zoals *knooppunten is niet gevonden* wordt weergegeven in de portal hello, en de lijst met knooppunt en de toepassing is leeg.</span><span class="sxs-lookup"><span data-stu-id="ff80e-119">If port 19080 is not accessible from hello Service Fabric resource provider, a message like *Nodes Not Found* appears in hello portal, and your node and application list appears empty.</span></span> <span data-ttu-id="ff80e-120">Als u wilt dat toosee uw cluster in hello Azure-portal, de load balancer moet een openbaar IP-adres beschikbaar en uw netwerkbeveiligingsgroep moet de binnenkomende 19080-poortverkeer toestaan.</span><span class="sxs-lookup"><span data-stu-id="ff80e-120">If you want toosee your cluster in hello Azure portal, your load balancer must expose a public IP address, and your network security group must allow incoming port 19080 traffic.</span></span> <span data-ttu-id="ff80e-121">Als uw installatie voldoet niet aan deze vereisten, weergegeven hello Azure-portal Hallo status van het cluster niet.</span><span class="sxs-lookup"><span data-stu-id="ff80e-121">If your setup does not meet these requirements, hello Azure portal does not display hello status of your cluster.</span></span>

## <a name="templates"></a><span data-ttu-id="ff80e-122">Sjablonen</span><span class="sxs-lookup"><span data-stu-id="ff80e-122">Templates</span></span>

<span data-ttu-id="ff80e-123">Alle Service Fabric-sjablonen zijn in [één gedownloade bestand](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span><span class="sxs-lookup"><span data-stu-id="ff80e-123">All Service Fabric templates are in [one download file](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip).</span></span> <span data-ttu-id="ff80e-124">U moet kunnen toodeploy Hallo sjablonen als-is via Hallo PowerShell-opdrachten te volgen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-124">You should be able toodeploy hello templates as-is by using hello following PowerShell commands.</span></span> <span data-ttu-id="ff80e-125">Als u implementeert Hallo bestaande Azure Virtual Network-sjabloon of Hallo statische openbare IP-sjabloon Hallo eerst lezen [initiële setup](#initialsetup) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ff80e-125">If you are deploying hello existing Azure Virtual Network template or hello static public IP template, first read hello [Initial setup](#initialsetup) section of this article.</span></span>

<a id="initialsetup"></a>
## <a name="initial-setup"></a><span data-ttu-id="ff80e-126">Eerste installatie</span><span class="sxs-lookup"><span data-stu-id="ff80e-126">Initial setup</span></span>

### <a name="existing-virtual-network"></a><span data-ttu-id="ff80e-127">Bestaand virtueel netwerk</span><span class="sxs-lookup"><span data-stu-id="ff80e-127">Existing virtual network</span></span>

<span data-ttu-id="ff80e-128">In de Hallo voorbeeld te volgen, we beginnen met een bestaand virtueel netwerk met de naam ExistingRG-vnet in Hallo **ExistingRG** resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ff80e-128">In hello following example, we start with an existing virtual network named ExistingRG-vnet, in hello **ExistingRG** resource group.</span></span> <span data-ttu-id="ff80e-129">naam van het Hallo-subnet is standaard.</span><span class="sxs-lookup"><span data-stu-id="ff80e-129">hello subnet is named default.</span></span> <span data-ttu-id="ff80e-130">Deze standaardresources worden gemaakt wanneer u hello Azure portal toocreate een standaard virtuele machine (VM) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff80e-130">These default resources are created when you use hello Azure portal toocreate a standard virtual machine (VM).</span></span> <span data-ttu-id="ff80e-131">U kan Hallo virtueel netwerk en subnet maken zonder Hallo VM maken, maar Hallo belangrijkste doel van het toevoegen van een cluster tooan bestaand virtueel netwerk is tooprovide network connectivity tooother virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ff80e-131">You could create hello virtual network and subnet without creating hello VM, but hello main goal of adding a cluster tooan existing virtual network is tooprovide network connectivity tooother VMs.</span></span> <span data-ttu-id="ff80e-132">Maken Hallo VM biedt een goed voorbeeld van hoe een bestaand virtueel netwerk wordt meestal gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-132">Creating hello VM gives a good example of how an existing virtual network typically is used.</span></span> <span data-ttu-id="ff80e-133">Als uw Service Fabric-cluster maakt gebruik van alleen een interne load balancer, zonder een openbaar IP-adres, kunt u virtuele machine en de openbare IP-adres als een veilige Hallo *springen vak*.</span><span class="sxs-lookup"><span data-stu-id="ff80e-133">If your Service Fabric cluster uses only an internal load balancer, without a public IP address, you can use hello VM and its public IP as a secure *jump box*.</span></span>

### <a name="static-public-ip-address"></a><span data-ttu-id="ff80e-134">Statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="ff80e-134">Static public IP address</span></span>

<span data-ttu-id="ff80e-135">Een statische openbare IP-adres is doorgaans een speciale resource die wordt afzonderlijk beheerd vanaf Hallo VM of deze toegewezen aan virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ff80e-135">A static public IP address generally is a dedicated resource that's managed separately from hello VM or VMs it's assigned to.</span></span> <span data-ttu-id="ff80e-136">Het ingericht in een specifieke netwerken resourcegroep (als tegengestelde tooin Hallo Service Fabric-clusterresourcegroep zelf).</span><span class="sxs-lookup"><span data-stu-id="ff80e-136">It's provisioned in a dedicated networking resource group (as opposed tooin hello Service Fabric cluster resource group itself).</span></span> <span data-ttu-id="ff80e-137">Maak een statische openbare IP-adres met de naam staticIP1 in Hallo dezelfde ExistingRG resourcegroep, in hello Azure-portal of met behulp van PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ff80e-137">Create a static public IP address named staticIP1 in hello same ExistingRG resource group, either in hello Azure portal or by using PowerShell:</span></span>

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a><span data-ttu-id="ff80e-138">Service Fabric-sjabloon</span><span class="sxs-lookup"><span data-stu-id="ff80e-138">Service Fabric template</span></span>

<span data-ttu-id="ff80e-139">In het Hallo-voorbeelden in dit artikel gebruiken we Hallo Service Fabric template.json.</span><span class="sxs-lookup"><span data-stu-id="ff80e-139">In hello examples in this article, we use hello Service Fabric template.json.</span></span> <span data-ttu-id="ff80e-140">Voordat u een cluster maakt, kunt u Hallo portal wizard standaard toodownload Hallo sjabloon van Hallo-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ff80e-140">You can use hello standard portal wizard toodownload hello template from hello portal before you create a cluster.</span></span> <span data-ttu-id="ff80e-141">Ook kunt u een van de sjablonen Hallo in Hallo [sjablonengalerie](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), zoals Hallo [vijf knooppunten Service Fabric-cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span><span class="sxs-lookup"><span data-stu-id="ff80e-141">You also can use one of hello templates in hello [template gallery](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), like hello [five-node Service Fabric cluster](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).</span></span>

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a><span data-ttu-id="ff80e-142">Bestaand virtueel netwerk of subnet</span><span class="sxs-lookup"><span data-stu-id="ff80e-142">Existing virtual network or subnet</span></span>

1. <span data-ttu-id="ff80e-143">Hallo subnet parameter toohello naam van de bestaande subnet Hallo wijzigen en voeg vervolgens twee nieuwe parameters tooreference Hallo bestaand virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="ff80e-143">Change hello subnet parameter toohello name of hello existing subnet, and then add two new parameters tooreference hello existing virtual network:</span></span>

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. <span data-ttu-id="ff80e-144">Wijziging Hallo `vnetID` variabele toopoint toohello bestaand virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="ff80e-144">Change hello `vnetID` variable toopoint toohello existing virtual network:</span></span>

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. <span data-ttu-id="ff80e-145">Verwijder `Microsoft.Network/virtualNetworks` van uw resources zo Azure geen maakt een nieuw virtueel netwerk:</span><span class="sxs-lookup"><span data-stu-id="ff80e-145">Remove `Microsoft.Network/virtualNetworks` from your resources, so Azure does not create a new virtual network:</span></span>

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. <span data-ttu-id="ff80e-146">Commentaar Hallo virtueel netwerk uit Hallo `dependsOn` kenmerk van `Microsoft.Compute/virtualMachineScaleSets`, zodat u niet afhankelijk zijn van een nieuw virtueel netwerk maken:</span><span class="sxs-lookup"><span data-stu-id="ff80e-146">Comment out hello virtual network from hello `dependsOn` attribute of `Microsoft.Compute/virtualMachineScaleSets`, so you don't depend on creating a new virtual network:</span></span>

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. <span data-ttu-id="ff80e-147">Hallo-sjabloon implementeren:</span><span class="sxs-lookup"><span data-stu-id="ff80e-147">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    <span data-ttu-id="ff80e-148">Na de implementatie, het virtuele netwerk moet zijn opgenomen Hallo nieuwe schaal ingesteld virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="ff80e-148">After deployment, your virtual network should include hello new scale set VMs.</span></span> <span data-ttu-id="ff80e-149">Hallo virtuele machine scale set-knooppunttype moet Hallo bestaand virtueel netwerk en subnetmasker worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ff80e-149">hello virtual machine scale set node type should show hello existing virtual network and subnet.</span></span> <span data-ttu-id="ff80e-150">Ook kunt u Remote Desktop Protocol (RDP) tooaccess Hallo VM die was al niet in het virtuele netwerk Hallo en tooping Hallo nieuwe schaal ingesteld virtuele machines:</span><span class="sxs-lookup"><span data-stu-id="ff80e-150">You also can use Remote Desktop Protocol (RDP) tooaccess hello VM that was already in hello virtual network, and tooping hello new scale set VMs:</span></span>

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

<span data-ttu-id="ff80e-151">Zie voor een ander voorbeeld [een die niet specifiek tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="ff80e-151">For another example, see [one that is not specific tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).</span></span>


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a><span data-ttu-id="ff80e-152">Statische openbare IP-adres</span><span class="sxs-lookup"><span data-stu-id="ff80e-152">Static public IP address</span></span>

1. <span data-ttu-id="ff80e-153">Voeg parameters voor de naam van de Hallo Hallo bestaande statische IP-resourcegroep, naam en volledig gekwalificeerde domeinnaam (FQDN):</span><span class="sxs-lookup"><span data-stu-id="ff80e-153">Add parameters for hello name of hello existing static IP resource group, name, and fully qualified domain name (FQDN):</span></span>

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. <span data-ttu-id="ff80e-154">Hallo verwijderen `dnsName` parameter.</span><span class="sxs-lookup"><span data-stu-id="ff80e-154">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="ff80e-155">(Hallo statisch IP-adres heeft al een.)</span><span class="sxs-lookup"><span data-stu-id="ff80e-155">(hello static IP address already has one.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. <span data-ttu-id="ff80e-156">Een variabele tooreference Hallo bestaande statische IP-adres toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ff80e-156">Add a variable tooreference hello existing static IP address:</span></span>

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. <span data-ttu-id="ff80e-157">Verwijder `Microsoft.Network/publicIPAddresses` van uw resources zo Azure geen maakt een nieuw IP-adres:</span><span class="sxs-lookup"><span data-stu-id="ff80e-157">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. <span data-ttu-id="ff80e-158">Commentaar Hallo IP-adres uit Hallo `dependsOn` kenmerk van `Microsoft.Network/loadBalancers`, zodat u niet afhankelijk zijn van het maken van een nieuw IP-adres:</span><span class="sxs-lookup"><span data-stu-id="ff80e-158">Comment out hello IP address from hello `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address:</span></span>

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. <span data-ttu-id="ff80e-159">In Hallo `Microsoft.Network/loadBalancers` resource, wijziging Hallo `publicIPAddress` element van `frontendIPConfigurations` tooreference Hallo bestaande statisch IP-adres in plaats van een nieuwe:</span><span class="sxs-lookup"><span data-stu-id="ff80e-159">In hello `Microsoft.Network/loadBalancers` resource, change hello `publicIPAddress` element of `frontendIPConfigurations` tooreference hello existing static IP address instead of a newly created one:</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. <span data-ttu-id="ff80e-160">In Hallo `Microsoft.ServiceFabric/clusters` resource wijzigen `managementEndpoint` toohello DNS FQDN Hallo statische IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-160">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toohello DNS FQDN of hello static IP address.</span></span> <span data-ttu-id="ff80e-161">Als u een beveiligde cluster gebruikt, controleert u of u kunt wijzigen *http://* te*https://*.</span><span class="sxs-lookup"><span data-stu-id="ff80e-161">If you are using a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="ff80e-162">(Houd er rekening mee dat deze stap alleen tooService Fabric-clusters geldt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-162">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="ff80e-163">Als u van een virtuele-machineschaalset gebruikmaakt, deze stap overslaan.)</span><span class="sxs-lookup"><span data-stu-id="ff80e-163">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. <span data-ttu-id="ff80e-164">Hallo-sjabloon implementeren:</span><span class="sxs-lookup"><span data-stu-id="ff80e-164">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

<span data-ttu-id="ff80e-165">Na de implementatie kunt u zien dat de load balancer gebonden toohello openbare statische IP-adres uit Hallo is andere resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ff80e-165">After deployment, you can see that your load balancer is bound toohello public static IP address from hello other resource group.</span></span> <span data-ttu-id="ff80e-166">Hallo verbindingseindpunt Service Fabric-client en [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) eindpunt punt toohello DNS FQDN Hallo statische IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-166">hello Service Fabric client connection endpoint and [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint point toohello DNS FQDN of hello static IP address.</span></span>

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a><span data-ttu-id="ff80e-167">Alleen voor interne load balancer</span><span class="sxs-lookup"><span data-stu-id="ff80e-167">Internal-only load balancer</span></span>

<span data-ttu-id="ff80e-168">Dit scenario vervangen Hallo externe load balancer in de Service Fabric standaardsjabloon Hallo door een interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-168">This scenario replaces hello external load balancer in hello default Service Fabric template with an internal-only load balancer.</span></span> <span data-ttu-id="ff80e-169">Zie Hallo voorgaande sectie voor gevolgen voor hello Azure-portal en Hallo Service Fabric-resourceprovider.</span><span class="sxs-lookup"><span data-stu-id="ff80e-169">For implications for hello Azure portal and for hello Service Fabric resource provider, see hello preceding section.</span></span>

1. <span data-ttu-id="ff80e-170">Hallo verwijderen `dnsName` parameter.</span><span class="sxs-lookup"><span data-stu-id="ff80e-170">Remove hello `dnsName` parameter.</span></span> <span data-ttu-id="ff80e-171">(Dit niet nodig.)</span><span class="sxs-lookup"><span data-stu-id="ff80e-171">(It's not needed.)</span></span>

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. <span data-ttu-id="ff80e-172">Als u een statische toewijzingsmethode gebruikt, kunt u eventueel een parameter statische IP-adres toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-172">Optionally, if you use a static allocation method, you can add a static IP address parameter.</span></span> <span data-ttu-id="ff80e-173">Als u een dynamische toewijzingsmethode gebruikt, hoeft u niet toodo deze stap.</span><span class="sxs-lookup"><span data-stu-id="ff80e-173">If you use a dynamic allocation method, you do not need toodo this step.</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. <span data-ttu-id="ff80e-174">Verwijder `Microsoft.Network/publicIPAddresses` van uw resources zo Azure geen maakt een nieuw IP-adres:</span><span class="sxs-lookup"><span data-stu-id="ff80e-174">Remove `Microsoft.Network/publicIPAddresses` from your resources, so Azure does not create a new IP address:</span></span>

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. <span data-ttu-id="ff80e-175">Verwijder Hallo IP-adres `dependsOn` kenmerk van `Microsoft.Network/loadBalancers`, zodat u niet afhankelijk zijn van het maken van een nieuw IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-175">Remove hello IP address `dependsOn` attribute of `Microsoft.Network/loadBalancers`, so you don't depend on creating a new IP address.</span></span> <span data-ttu-id="ff80e-176">Toevoegen van het virtuele netwerk Hallo `dependsOn` omdat Hallo subnet van het virtuele netwerk Hallo Hallo load balancer nu afhankelijk van het kenmerk:</span><span class="sxs-lookup"><span data-stu-id="ff80e-176">Add hello virtual network `dependsOn` attribute because hello load balancer now depends on hello subnet from hello virtual network:</span></span>

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. <span data-ttu-id="ff80e-177">Hallo load balancer wijzigen `frontendIPConfigurations` instellen uit met behulp van een `publicIPAddress`, toousing een subnet en `privateIPAddress`.</span><span class="sxs-lookup"><span data-stu-id="ff80e-177">Change hello load balancer's `frontendIPConfigurations` setting from using a `publicIPAddress`, toousing a subnet and `privateIPAddress`.</span></span> <span data-ttu-id="ff80e-178">`privateIPAddress`een vooraf gedefinieerde statische interne IP-adres gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-178">`privateIPAddress` uses a predefined static internal IP address.</span></span> <span data-ttu-id="ff80e-179">toouse een dynamisch IP-adres verwijderen Hallo `privateIPAddress` element en wijzig vervolgens `privateIPAllocationMethod` te**dynamische**.</span><span class="sxs-lookup"><span data-stu-id="ff80e-179">toouse a dynamic IP address, remove hello `privateIPAddress` element, and then change `privateIPAllocationMethod` too**Dynamic**.</span></span>

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. <span data-ttu-id="ff80e-180">In Hallo `Microsoft.ServiceFabric/clusters` resource wijzigen `managementEndpoint` toopoint toohello interne load balancer-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-180">In hello `Microsoft.ServiceFabric/clusters` resource, change `managementEndpoint` toopoint toohello internal load balancer address.</span></span> <span data-ttu-id="ff80e-181">Als u een beveiligde cluster gebruikt, controleert u of u kunt wijzigen *http://* te*https://*.</span><span class="sxs-lookup"><span data-stu-id="ff80e-181">If you use a secure cluster, make sure you change *http://* too*https://*.</span></span> <span data-ttu-id="ff80e-182">(Houd er rekening mee dat deze stap alleen tooService Fabric-clusters geldt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-182">(Note that this step applies only tooService Fabric clusters.</span></span> <span data-ttu-id="ff80e-183">Als u van een virtuele-machineschaalset gebruikmaakt, deze stap overslaan.)</span><span class="sxs-lookup"><span data-stu-id="ff80e-183">If you are using a virtual machine scale set, skip this step.)</span></span>

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. <span data-ttu-id="ff80e-184">Hallo-sjabloon implementeren:</span><span class="sxs-lookup"><span data-stu-id="ff80e-184">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

<span data-ttu-id="ff80e-185">Na de implementatie maakt gebruik van de load balancer Hallo persoonlijke 10.0.0.250 van statische IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-185">After deployment, your load balancer uses hello private static 10.0.0.250 IP address.</span></span> <span data-ttu-id="ff80e-186">Als u een andere computer die hetzelfde virtuele netwerk hebt, kunt u gaan toohello interne [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-186">If you have another machine in that same virtual network, you can go toohello internal [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) endpoint.</span></span> <span data-ttu-id="ff80e-187">Houd er rekening mee dat deze verbinding tooone Hallo knooppunten achter Hallo load balancer maakt.</span><span class="sxs-lookup"><span data-stu-id="ff80e-187">Note that it connects tooone of hello nodes behind hello load balancer.</span></span>

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a><span data-ttu-id="ff80e-188">Interne en externe load balancer</span><span class="sxs-lookup"><span data-stu-id="ff80e-188">Internal and external load balancer</span></span>

<span data-ttu-id="ff80e-189">In dit scenario u beginnen met Hallo bestaande één knooppunt type externe load balancer en toevoegen van een interne load balancer voor Hallo dezelfde knooppunttype.</span><span class="sxs-lookup"><span data-stu-id="ff80e-189">In this scenario, you start with hello existing single-node type external load balancer, and add an internal load balancer for hello same node type.</span></span> <span data-ttu-id="ff80e-190">Een back-end-poort gekoppeld tooa back-end-adresgroep kan alleen tooa één load balancer worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-190">A back-end port attached tooa back-end address pool can be assigned only tooa single load balancer.</span></span> <span data-ttu-id="ff80e-191">Kies welke load balancer wordt de poorten van uw toepassing, en welke load balancer heeft uw eindpunten voor beheer (poorten 19000 en 19080).</span><span class="sxs-lookup"><span data-stu-id="ff80e-191">Choose which load balancer will have your application ports, and which load balancer will have your management endpoints (ports 19000 and 19080).</span></span> <span data-ttu-id="ff80e-192">Als u Hallo-eindpunten voor beheer op Hallo interne load balancer plaatst, houd rekening Hallo Service Fabric-resource provider-beperkingen die eerder in Hallo artikel besproken.</span><span class="sxs-lookup"><span data-stu-id="ff80e-192">If you put hello management endpoints on hello internal load balancer, keep in mind hello Service Fabric resource provider restrictions discussed earlier in hello article.</span></span> <span data-ttu-id="ff80e-193">In Hallo voorbeeld we gebruiken blijven Hallo-eindpunten voor beheer op Hallo externe load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-193">In hello example we use, hello management endpoints remain on hello external load balancer.</span></span> <span data-ttu-id="ff80e-194">U ook een poort 80 toepassing poort toevoegen en plaats het op Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-194">You also add a port 80 application port, and place it on hello internal load balancer.</span></span>

<span data-ttu-id="ff80e-195">In een cluster met twee knooppunttype is één knooppunttype op Hallo externe load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-195">In a two-node-type cluster, one node type is on hello external load balancer.</span></span> <span data-ttu-id="ff80e-196">Hallo is andere knooppunttype op Hallo interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-196">hello other node type is on hello internal load balancer.</span></span> <span data-ttu-id="ff80e-197">een cluster twee knooppunttype in Hallo portal gemaakt twee knooppunttype sjabloon (die wordt geleverd met twee netwerktaakverdelers) toouse overschakelen Hallo tweede load balancer tooan interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-197">toouse a two-node-type cluster, in hello portal-created two-node-type template (which comes with two load balancers), switch hello second load balancer tooan internal load balancer.</span></span> <span data-ttu-id="ff80e-198">Zie voor meer informatie, Hallo [alleen interne load balancer](#internallb) sectie.</span><span class="sxs-lookup"><span data-stu-id="ff80e-198">For more information, see hello [Internal-only load balancer](#internallb) section.</span></span>

1. <span data-ttu-id="ff80e-199">Parameter van IP-adres van Hallo statische interne load balancer toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-199">Add hello static internal load balancer IP address parameter.</span></span> <span data-ttu-id="ff80e-200">(Zie de vorige secties van dit artikel voor opmerkingen bij de gerelateerde toousing een dynamisch IP-adres,.)</span><span class="sxs-lookup"><span data-stu-id="ff80e-200">(For notes related toousing a dynamic IP address, see earlier sections of this article.)</span></span>

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. <span data-ttu-id="ff80e-201">Een parameter van de poort 80 toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ff80e-201">Add an application port 80 parameter.</span></span>

3. <span data-ttu-id="ff80e-202">interne versies van bestaande Hallo tooadd networking variabelen, kopiëren en plakken en toevoegen '-Int ' toohello naam:</span><span class="sxs-lookup"><span data-stu-id="ff80e-202">tooadd internal versions of hello existing networking variables, copy and paste them, and add "-Int" toohello name:</span></span>

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. <span data-ttu-id="ff80e-203">Als u met Hallo portal gegenereerde sjabloon die gebruikmaakt van toepassing poort 80 begint, portal standaardsjabloon Hallo AppPort1 toegevoegd (poort 80) op Hallo externe load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-203">If you start with hello portal-generated template that uses application port 80, hello default portal template adds AppPort1 (port 80) on hello external load balancer.</span></span> <span data-ttu-id="ff80e-204">In dit geval AppPort1 verwijderen uit Hallo externe load balancer `loadBalancingRules` en tests, zodat u toohello interne load balancer kunt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ff80e-204">In this case, remove AppPort1 from hello external load balancer `loadBalancingRules` and probes, so you can add it toohello internal load balancer:</span></span>

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. <span data-ttu-id="ff80e-205">Toevoegen van een tweede `Microsoft.Network/loadBalancers` resource.</span><span class="sxs-lookup"><span data-stu-id="ff80e-205">Add a second `Microsoft.Network/loadBalancers` resource.</span></span> <span data-ttu-id="ff80e-206">Het lijkt erop vergelijkbare toohello interne load balancer gemaakt in Hallo [alleen interne load balancer](#internallb) sectie, maar gebruikt u Hallo '-Int "load balancer-variabelen en implementeert alleen Hallo toepassing poort 80.</span><span class="sxs-lookup"><span data-stu-id="ff80e-206">It looks similar toohello internal load balancer created in hello [Internal-only load balancer](#internallb) section, but it uses hello "-Int" load balancer variables, and implements only hello application port 80.</span></span> <span data-ttu-id="ff80e-207">Hiermee worden `inboundNatPools`, tookeep RDP-eindpunten op Hallo openbare load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-207">This also removes `inboundNatPools`, tookeep RDP endpoints on hello public load balancer.</span></span> <span data-ttu-id="ff80e-208">Desgewenst kunt u RDP op Hallo interne load balancer verplaatsen `inboundNatPools` van Hallo externe load balancer toothis interne de load balancer:</span><span class="sxs-lookup"><span data-stu-id="ff80e-208">If you want RDP on hello internal load balancer, move `inboundNatPools` from hello external load balancer toothis internal load balancer:</span></span>

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. <span data-ttu-id="ff80e-209">In `networkProfile` voor Hallo `Microsoft.Compute/virtualMachineScaleSets` resource, Hallo interne back-end-adresgroep toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ff80e-209">In `networkProfile` for hello `Microsoft.Compute/virtualMachineScaleSets` resource, add hello internal back-end address pool:</span></span>

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. <span data-ttu-id="ff80e-210">Hallo-sjabloon implementeren:</span><span class="sxs-lookup"><span data-stu-id="ff80e-210">Deploy hello template:</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

<span data-ttu-id="ff80e-211">Na de implementatie ziet u twee load balancers in de resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff80e-211">After deployment, you can see two load balancers in hello resource group.</span></span> <span data-ttu-id="ff80e-212">Als u de netwerktaakverdelers Hallo bladert, ziet u Hallo openbaar IP-adres en management eindpunten (poorten 19000 en 19080) toegewezen toohello openbaar IP-adres.</span><span class="sxs-lookup"><span data-stu-id="ff80e-212">If you browse hello load balancers, you can see hello public IP address and management endpoints (ports 19000 and 19080) assigned toohello public IP address.</span></span> <span data-ttu-id="ff80e-213">Ook ziet u Hallo statische interne IP-adres en de toepassing eindpunt (poort 80) toegewezen toohello interne load balancer.</span><span class="sxs-lookup"><span data-stu-id="ff80e-213">You also can see hello static internal IP address and application endpoint (port 80) assigned toohello internal load balancer.</span></span> <span data-ttu-id="ff80e-214">Beide load balancers gebruik hello dezelfde virtuele-machineschaalset back-end-pool.</span><span class="sxs-lookup"><span data-stu-id="ff80e-214">Both load balancers use hello same virtual machine scale set back-end pool.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ff80e-215">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff80e-215">Next steps</span></span>
[<span data-ttu-id="ff80e-216">Een cluster maken</span><span class="sxs-lookup"><span data-stu-id="ff80e-216">Create a cluster</span></span>](service-fabric-cluster-creation-via-arm.md)
