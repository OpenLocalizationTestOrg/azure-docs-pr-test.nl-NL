---
title: aaaManage netwerkbeveiligingsgroepen - Azure PowerShell | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3706ce6c-d9ae-46cb-a048-f0a4e84dc5cc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/14/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 930fe5e0827896ad67b24d84e41a5d3f898ba838
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="ebb4a-103">Netwerkbeveiligingsgroepen met behulp van PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="ebb4a-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="ebb4a-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ebb4a-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ebb4a-105">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="ebb4a-106">Informatie ophalen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-106">Retrieve Information</span></span>
<span data-ttu-id="ebb4a-107">U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="ebb4a-108">Bestaande nsg's weergeven</span><span class="sxs-lookup"><span data-stu-id="ebb4a-108">View existing NSGs</span></span>
<span data-ttu-id="ebb4a-109">tooview alle bestaande nsg's in een abonnement uitvoeren Hallo `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-109">tooview all existing NSGs in a subscription, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="ebb4a-110">Verwachte resultaat:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-110">Expected result:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : WEB1
    ResourceGroupName    : RG101
    Location             : eastus2
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG101/providers/M
                           icrosoft.Network/networkSecurityGroups/WEB1
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]


<span data-ttu-id="ebb4a-111">tooview hello lijst met nsg's in een specifieke resourcegroep of Voer Hallo `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-111">tooview hello list of NSGs in a specific resource group, run hello `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="ebb4a-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-112">Expected output:</span></span>

    Name                 : NSG-BackEnd
    ResourceGroupName    : RG-NSG
    Location             : westus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-BackEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 :                            
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

    Name                 : NSG-FrontEnd
    ResourceGroupName    : RG-NSG
    Location             : eastus
    Id                   : /subscriptions/[Subscription Id]/resourceGroups/NRP-RG/providers/
                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    Etag                 : W/"[Id]"
    ResourceGuid         : [Id]
    ProvisioningState    : Succeeded
    Tags                 : 
    SecurityRules        : [...]
    DefaultSecurityRules : [...]
    NetworkInterfaces    : [...]
    Subnets              : [...]

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="ebb4a-113">Lijst met alle regels voor een NSG</span><span class="sxs-lookup"><span data-stu-id="ebb4a-113">List all rules for an NSG</span></span>
<span data-ttu-id="ebb4a-114">tooview hello regels van een NSG met de naam **NSG-FrontEnd**, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-114">tooview hello rules of an NSG named **NSG-FrontEnd**, enter hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="ebb4a-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-115">Expected output:</span></span>

    Name                     : rdp-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow RDP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 3389
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 100
    Direction                : Inbound

    Name                     : web-rule
    Id                       : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/                           Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
    Etag                     : W/"[Id]"
    ProvisioningState        : Succeeded
    Description              : Allow HTTP
    Protocol                 : Tcp
    SourcePortRange          : *
    DestinationPortRange     : 80
    SourceAddressPrefix      : Internet
    DestinationAddressPrefix : *
    Access                   : Allow
    Priority                 : 101
    Direction                : Inbound

> [!NOTE]
> <span data-ttu-id="ebb4a-116">U kunt ook `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist Hallo standaardregels van Hallo **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` toolist hello default rules from hello **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="ebb4a-117">Nsg's koppelingen weergeven</span><span class="sxs-lookup"><span data-stu-id="ebb4a-117">View NSGs associations</span></span>
<span data-ttu-id="ebb4a-118">tooview welke resources Hallo **NSG-FrontEnd** NSG is met, voert hello van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-118">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="ebb4a-119">Zoek naar Hallo **NetworkInterfaces** en **subnetten** eigenschappen zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-119">Look for hello **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="ebb4a-120">In het vorige voorbeeld Hallo is Hallo NSG niet gekoppeld tooany netwerkinterfaces (NIC's); het is gekoppeld tooa subnet met de naam **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-120">In hello previous example, hello NSG is not associated tooany network interfaces (NICs); it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="ebb4a-121">Regels beheren</span><span class="sxs-lookup"><span data-stu-id="ebb4a-121">Manage rules</span></span>
<span data-ttu-id="ebb4a-122">U kunt regels tooan bestaande NSG toevoegen, bestaande regels bewerken en regels te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-122">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="ebb4a-123">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-123">Add a rule</span></span>
<span data-ttu-id="ebb4a-124">tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-124">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, complete hello following steps:</span></span>

1. <span data-ttu-id="ebb4a-125">Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-125">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="ebb4a-126">Hallo opdracht tooadd na een regel toohello NSG uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-126">Run hello following command tooadd a rule toohello NSG:</span></span>

    ```powershell
    Add-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="ebb4a-127">toosave hello wijzigingen aangebracht toohello NSG, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-127">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="ebb4a-128">Verwachte uitvoer alleen Hallo beveiligingsregels voor verbindingen met:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-128">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "*",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="change-a-rule"></a><span data-ttu-id="ebb4a-129">Een regel wijzigen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-129">Change a rule</span></span>
<span data-ttu-id="ebb4a-130">toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, follow hello steps below.</span></span>

1. <span data-ttu-id="ebb4a-131">Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-131">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="ebb4a-132">Voer Hallo opdracht met de nieuwe regelinstellingen Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-132">Run hello following command with hello new rule settings:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg `
    -Name https-rule `
    -Description "Allow HTTPS" `
    -Access Allow `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 102 `
    -SourceAddressPrefix Internet `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 443
    ```

3. <span data-ttu-id="ebb4a-133">toosave hello wijzigingen aangebracht toohello NSG, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-133">toosave hello changes made toohello NSG, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="ebb4a-134">Verwachte uitvoer alleen Hallo beveiligingsregels voor verbindingen met:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-134">Expected output showing only hello security rules:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 },
                                 {
                                   "Name": "https-rule",
                                   "Etag": "W/\"[Id]\"",
                                   "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/https-rule",
                                   "Description": "Allow HTTPS",
                                   "Protocol": "Tcp",
                                   "SourcePortRange": "*",
                                   "DestinationPortRange": "443",
                                   "SourceAddressPrefix": "Internet",
                                   "DestinationAddressPrefix": "*",
                                   "Access": "Allow",
                                   "Priority": 102,
                                   "Direction": "Inbound",
                                   "ProvisioningState": "Succeeded"
                                 }
                               ]

### <a name="delete-a-rule"></a><span data-ttu-id="ebb4a-135">Een regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-135">Delete a rule</span></span>
1. <span data-ttu-id="ebb4a-136">Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-136">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="ebb4a-137">Hallo volgende opdracht tooremove Hallo regel uit Hallo NSG uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-137">Run hello following command tooremove hello rule from hello NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="ebb4a-138">Hallo wijzigingen toohello NSG, door het uitvoeren van de volgende opdracht Hallo opslaan:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-138">Save hello changes made toohello NSG, by running hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="ebb4a-139">Verwachte uitvoer met alleen Hallo beveiligingsregels, kennisgeving Hallo **https-regel** wordt niet meer vermeld:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-139">Expected output showing only hello security rules, notice hello **https-rule** is no longer listed:</span></span>
   
        Name                 : NSG-FrontEnd
        ...
        SecurityRules        : [
                                 {
                                   "Name": "rdp-rule",
                                   ...
                                 },
                                 {
                                   "Name": "web-rule",
                                   ...
                                 }
                               ]

## <a name="manage-associations"></a><span data-ttu-id="ebb4a-140">Koppelingen beheren</span><span class="sxs-lookup"><span data-stu-id="ebb4a-140">Manage associations</span></span>
<span data-ttu-id="ebb4a-141">U kunt een NSG toosubnets en NIC's kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-141">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="ebb4a-142">U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="ebb4a-143">Een NSG tooa NIC koppelen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-143">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="ebb4a-144">Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-144">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="ebb4a-145">Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-145">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="ebb4a-146">Hallo na de opdracht tooretrieve Hallo bestaande NIC uitvoeren en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-146">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="ebb4a-147">Set Hallo **NetworkSecurityGroup** eigenschap Hallo **NIC** waarde van variabele toohello Hallo **NSG** variabele, door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-147">Set hello **NetworkSecurityGroup** property of hello **NIC** variable toohello value of hello **NSG** variable, by entering hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="ebb4a-148">toosave hello wijzigingen aangebracht toohello NIC, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-148">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="ebb4a-149">Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-149">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="ebb4a-150">Een NSG van een NIC ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="ebb4a-151">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-151">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, complete hello following steps:</span></span>

1. <span data-ttu-id="ebb4a-152">Hallo na de opdracht tooretrieve Hallo bestaande NIC uitvoeren en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-152">Run hello following command tooretrieve hello existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="ebb4a-153">Set Hallo **NetworkSecurityGroup** eigenschap Hallo **NIC** variabele te**$null** door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-153">Set hello **NetworkSecurityGroup** property of hello **NIC** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="ebb4a-154">toosave hello wijzigingen aangebracht toohello NIC, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-154">toosave hello changes made toohello NIC, run hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="ebb4a-155">Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-155">Expected output showing only hello **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="ebb4a-156">Een NSG van een subnet ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="ebb4a-157">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-157">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, complete hello following steps:</span></span>

1. <span data-ttu-id="ebb4a-158">Voer Hallo opdracht tooretrieve Hallo bestaande VNet te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-158">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="ebb4a-159">Voer hello na de opdracht tooretrieve hello **FrontEnd** subnet en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-159">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="ebb4a-160">Set Hallo **NetworkSecurityGroup** eigenschap Hallo **subnet** variabele te**$null** hiertoe Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-160">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by entering hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="ebb4a-161">toosave hello wijzigingen aangebracht toohello subnet, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-161">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="ebb4a-162">Verwachte uitvoer met alleen Hallo eigenschappen van Hallo **FrontEnd** subnet.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-162">Expected output showing only hello properties of hello **FrontEnd** subnet.</span></span> <span data-ttu-id="ebb4a-163">U ziet dat er zich geen eigenschap voor **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
            ...
            Subnets           : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1"
                                      },
                                      {
                                        "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1"
                                      }
                                    ],
                                    "ProvisioningState": "Succeeded"
                                  },
                                    ...
                                ]

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="ebb4a-164">Een NSG tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-164">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="ebb4a-165">Hallo tooassociate **NSG-FrontEnd** NSG toohello **FronEnd** opnieuw subnet, volledige Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-165">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, complete hello following steps:</span></span>

1. <span data-ttu-id="ebb4a-166">Voer Hallo opdracht tooretrieve Hallo bestaande VNet te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-166">Run hello following command tooretrieve hello existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="ebb4a-167">Voer hello na de opdracht tooretrieve hello **FrontEnd** subnet en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-167">Run hello following command tooretrieve hello **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="ebb4a-168">Voer Hallo opdracht tooretrieve Hallo bestaande NSG te volgen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-168">Run hello following command tooretrieve hello existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="ebb4a-169">Set Hallo **NetworkSecurityGroup** eigenschap Hallo **subnet** variabele te**$null** door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-169">Set hello **NetworkSecurityGroup** property of hello **subnet** variable too**$null** by running hello following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="ebb4a-170">toosave hello wijzigingen aangebracht toohello subnet, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-170">toosave hello changes made toohello subnet, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="ebb4a-171">Verwachte uitvoer waarin alleen Hallo **NetworkSecurityGroup** eigenschap Hallo **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-171">Expected output showing only hello **NetworkSecurityGroup** property of hello **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="ebb4a-172">Een NSG verwijderen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-172">Delete an NSG</span></span>
<span data-ttu-id="ebb4a-173">U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-173">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="ebb4a-174">een NSG toodelete Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-174">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="ebb4a-175">toocheck hello resources die zijn gekoppeld tooan NSG, Voer Hallo `azure network nsg show` zoals in [weergave nsg's koppelingen](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="ebb4a-175">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="ebb4a-176">Als Hallo NSG gekoppeld tooany NIC's is, voert u Hallo `azure network nic set` zoals in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC) voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-176">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="ebb4a-177">Als Hallo NSG gekoppeld tooany subnet is, voert u Hallo `azure network vnet subnet set` zoals in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet) voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-177">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="ebb4a-178">toodelete hello NSG, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ebb4a-178">toodelete hello NSG, run hello following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="ebb4a-179">Hallo `-Force` parameter zorgt ervoor dat u hoeft niet tooconfirm Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-179">hello `-Force` parameter ensures you don't need tooconfirm hello deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="ebb4a-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebb4a-180">Next steps</span></span>
* <span data-ttu-id="ebb4a-181">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="ebb4a-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

