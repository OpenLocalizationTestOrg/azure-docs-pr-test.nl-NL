---
title: Netwerkbeveiligingsgroepen - Azure PowerShell beheren | Microsoft Docs
description: Informatie over het beheren van netwerkbeveiligingsgroepen met behulp van PowerShell.
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
ms.openlocfilehash: ca7f4926ca4edf9d20612aca74f6ae5f0ed847b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-network-security-groups-using-powershell"></a><span data-ttu-id="8c77d-103">Netwerkbeveiligingsgroepen met behulp van PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="8c77d-103">Manage network security groups using PowerShell</span></span>

[!INCLUDE [virtual-network-manage-arm-selectors-include.md](../../includes/virtual-network-manage-nsg-arm-selectors-include.md)]

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="8c77d-104">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8c77d-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8c77d-105">In dit artikel wordt behandeld met het implementatiemodel van Resource Manager, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel aanbeveelt.</span><span class="sxs-lookup"><span data-stu-id="8c77d-105">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the classic deployment model.</span></span>
>

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="8c77d-106">Informatie ophalen</span><span class="sxs-lookup"><span data-stu-id="8c77d-106">Retrieve Information</span></span>
<span data-ttu-id="8c77d-107">U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="8c77d-107">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="8c77d-108">Bestaande nsg's weergeven</span><span class="sxs-lookup"><span data-stu-id="8c77d-108">View existing NSGs</span></span>
<span data-ttu-id="8c77d-109">Uitvoeren als u wilt weergeven van alle bestaande nsg's in een abonnement, het `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c77d-109">To view all existing NSGs in a subscription, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="8c77d-110">Verwachte resultaat:</span><span class="sxs-lookup"><span data-stu-id="8c77d-110">Expected result:</span></span>

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


<span data-ttu-id="8c77d-111">Voor de lijst met nsg's in een specifieke resourcegroep, voer de `Get-AzureRmNetworkSecurityGroup` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="8c77d-111">To view the list of NSGs in a specific resource group, run the `Get-AzureRmNetworkSecurityGroup` cmdlet.</span></span>

<span data-ttu-id="8c77d-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8c77d-112">Expected output:</span></span>

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

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="8c77d-113">Lijst met alle regels voor een NSG</span><span class="sxs-lookup"><span data-stu-id="8c77d-113">List all rules for an NSG</span></span>
<span data-ttu-id="8c77d-114">Om weer te geven van de regels van een NSG met de naam **NSG-FrontEnd**, voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-114">To view the rules of an NSG named **NSG-FrontEnd**, enter the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd | Select SecurityRules -ExpandProperty SecurityRules
```

<span data-ttu-id="8c77d-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="8c77d-115">Expected output:</span></span>

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
> <span data-ttu-id="8c77d-116">U kunt ook `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` voor een lijst met de standaardregels van de **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="8c77d-116">You can also use `Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name "NSG-FrontEnd" | Select DefaultSecurityRules -ExpandProperty DefaultSecurityRules` to list the default rules from the **NSG-FrontEnd** NSG.</span></span>
> 

### <a name="view-nsgs-associations"></a><span data-ttu-id="8c77d-117">Nsg's koppelingen weergeven</span><span class="sxs-lookup"><span data-stu-id="8c77d-117">View NSGs associations</span></span>
<span data-ttu-id="8c77d-118">Om weer te geven welke bronnen de **NSG-FrontEnd** NSG koppelen, is de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8c77d-118">To view what resources the **NSG-FrontEnd** NSG is associate with, run the following command:</span></span>

```powershell
Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
```

<span data-ttu-id="8c77d-119">Zoek naar de **NetworkInterfaces** en **subnetten** eigenschappen zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="8c77d-119">Look for the **NetworkInterfaces** and **Subnets** properties as shown below:</span></span>

    NetworkInterfaces    : []
    Subnets              : [
                             {
                               "Id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                               "IpConfigurations": []
                             }
                           ]

<span data-ttu-id="8c77d-120">In het vorige voorbeeld is het NSG niet gekoppeld aan alle netwerkinterfaces (NIC's); het is gekoppeld aan een subnet met de naam **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="8c77d-120">In the previous example, the NSG is not associated to any network interfaces (NICs); it is associated to a subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="8c77d-121">Regels beheren</span><span class="sxs-lookup"><span data-stu-id="8c77d-121">Manage rules</span></span>
<span data-ttu-id="8c77d-122">U kunt regels toevoegen aan een bestaande NSG, bestaande regels bewerken en regels te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8c77d-122">You can add rules to an existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="8c77d-123">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="8c77d-123">Add a rule</span></span>
<span data-ttu-id="8c77d-124">Een regel voor toestaan toevoegen **inkomende** verkeer op poort **443** vanaf een willekeurige computer naar de **NSG-FrontEnd** NSG, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c77d-124">To add a rule allowing **inbound** traffic to port **443** from any machine to the **NSG-FrontEnd** NSG, complete the following steps:</span></span>

1. <span data-ttu-id="8c77d-125">Voer de volgende opdracht om de bestaande NSG ophalen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-125">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell   
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="8c77d-126">Voer de volgende opdracht om een regel toevoegen aan het NSG:</span><span class="sxs-lookup"><span data-stu-id="8c77d-126">Run the following command to add a rule to the NSG:</span></span>

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

3. <span data-ttu-id="8c77d-127">Voer de volgende opdracht voor het opslaan van de wijzigingen in de NSG:</span><span class="sxs-lookup"><span data-stu-id="8c77d-127">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```
    <span data-ttu-id="8c77d-128">Verwachte uitvoer met alleen de beveiligingsregels voor verbindingen:</span><span class="sxs-lookup"><span data-stu-id="8c77d-128">Expected output showing only the security rules:</span></span>
   
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

### <a name="change-a-rule"></a><span data-ttu-id="8c77d-129">Een regel wijzigen</span><span class="sxs-lookup"><span data-stu-id="8c77d-129">Change a rule</span></span>
<span data-ttu-id="8c77d-130">Wijzigen van de regel die eerder is gemaakt waarmee binnenkomend verkeer van de **Internet** alleen de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="8c77d-130">To change the rule created above to allow inbound traffic from the **Internet** only, follow the steps below.</span></span>

1. <span data-ttu-id="8c77d-131">Voer de volgende opdracht om de bestaande NSG ophalen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-131">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell 
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="8c77d-132">Voer de volgende opdracht met de regelinstellingen van de nieuwe:</span><span class="sxs-lookup"><span data-stu-id="8c77d-132">Run the following command with the new rule settings:</span></span>

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

3. <span data-ttu-id="8c77d-133">Voer de volgende opdracht voor het opslaan van de wijzigingen in de NSG:</span><span class="sxs-lookup"><span data-stu-id="8c77d-133">To save the changes made to the NSG, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="8c77d-134">Verwachte uitvoer met alleen de beveiligingsregels voor verbindingen:</span><span class="sxs-lookup"><span data-stu-id="8c77d-134">Expected output showing only the security rules:</span></span>
   
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

### <a name="delete-a-rule"></a><span data-ttu-id="8c77d-135">Een regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c77d-135">Delete a rule</span></span>
1. <span data-ttu-id="8c77d-136">Voer de volgende opdracht om de bestaande NSG ophalen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-136">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="8c77d-137">Voer de volgende opdracht om de regel verwijderen uit het NSG:</span><span class="sxs-lookup"><span data-stu-id="8c77d-137">Run the following command to remove the rule from the NSG:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityRuleConfig -NetworkSecurityGroup $nsg -Name https-rule
    ```

3. <span data-ttu-id="8c77d-138">Sla de wijzigingen in de NSG met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-138">Save the changes made to the NSG, by running the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkSecurityGroup -NetworkSecurityGroup $nsg
    ```

    <span data-ttu-id="8c77d-139">Verwachte uitvoer met alleen de beveiligingsregels, kennisgeving de **https-regel** wordt niet meer vermeld:</span><span class="sxs-lookup"><span data-stu-id="8c77d-139">Expected output showing only the security rules, notice the **https-rule** is no longer listed:</span></span>
   
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

## <a name="manage-associations"></a><span data-ttu-id="8c77d-140">Koppelingen beheren</span><span class="sxs-lookup"><span data-stu-id="8c77d-140">Manage associations</span></span>
<span data-ttu-id="8c77d-141">U kunt een NSG aan subnetten en NIC's kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="8c77d-141">You can associate an NSG to subnets and NICs.</span></span> <span data-ttu-id="8c77d-142">U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="8c77d-142">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-to-a-nic"></a><span data-ttu-id="8c77d-143">Een NSG aan een NIC koppelt</span><span class="sxs-lookup"><span data-stu-id="8c77d-143">Associate an NSG to a NIC</span></span>
<span data-ttu-id="8c77d-144">Om te koppelen de **NSG-FrontEnd** NSG aan de **TestNICWeb1** NIC, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c77d-144">To associate the **NSG-FrontEnd** NSG to the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="8c77d-145">Voer de volgende opdracht om de bestaande NSG ophalen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-145">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

2. <span data-ttu-id="8c77d-146">Voer de volgende opdracht op te halen van de bestaande NIC en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-146">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

3. <span data-ttu-id="8c77d-147">Stel de **NetworkSecurityGroup** eigenschap van de **NIC** variabele met de waarde van de **NSG** variabele met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-147">Set the **NetworkSecurityGroup** property of the **NIC** variable to the value of the **NSG** variable, by entering the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $nsg
    ```

4. <span data-ttu-id="8c77d-148">Voer de volgende opdracht voor het opslaan van de wijzigingen in de NIC:</span><span class="sxs-lookup"><span data-stu-id="8c77d-148">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="8c77d-149">Verwachte uitvoer waarin alleen de **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="8c77d-149">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : {
                                 "SecurityRules": [],
                                 "DefaultSecurityRules": [],
                                 "NetworkInterfaces": [],
                                 "Subnets": [],
                                 "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                               }

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="8c77d-150">Een NSG van een NIC ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="8c77d-150">Dissociate an NSG from a NIC</span></span>
<span data-ttu-id="8c77d-151">Ontkoppelen de **NSG-FrontEnd** NSG van de **TestNICWeb1** NIC, de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c77d-151">To dissociate the **NSG-FrontEnd** NSG from the **TestNICWeb1** NIC, complete the following steps:</span></span>

1. <span data-ttu-id="8c77d-152">Voer de volgende opdracht op te halen van de bestaande NIC en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-152">Run the following command to retrieve the existing NIC and store it in a variable:</span></span>

    ```powershell
    $nic = Get-AzureRmNetworkInterface -ResourceGroupName RG-NSG -Name TestNICWeb1
    ```

2. <span data-ttu-id="8c77d-153">Stel de **NetworkSecurityGroup** eigenschap van de **NIC** variabele **$null** met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-153">Set the **NetworkSecurityGroup** property of the **NIC** variable to **$null** by running the following command:</span></span>

    ```powershell
    $nic.NetworkSecurityGroup = $null
    ```

3. <span data-ttu-id="8c77d-154">Voer de volgende opdracht voor het opslaan van de wijzigingen in de NIC:</span><span class="sxs-lookup"><span data-stu-id="8c77d-154">To save the changes made to the NIC, run the following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $nic
    ```
   
    <span data-ttu-id="8c77d-155">Verwachte uitvoer waarin alleen de **NetworkSecurityGroup** eigenschap:</span><span class="sxs-lookup"><span data-stu-id="8c77d-155">Expected output showing only the **NetworkSecurityGroup** property:</span></span>
   
        NetworkSecurityGroup : null

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="8c77d-156">Een NSG van een subnet ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="8c77d-156">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="8c77d-157">Ontkoppelen de **NSG-FrontEnd** NSG van de **FrontEnd** het subnet van de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="8c77d-157">To dissociate the **NSG-FrontEnd** NSG from the **FrontEnd** subnet, complete the following steps:</span></span>

1. <span data-ttu-id="8c77d-158">Voer de volgende opdracht op te halen van de bestaande VNet en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-158">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="8c77d-159">Voer de volgende opdracht voor het ophalen van de **FrontEnd** subnet en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-159">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="8c77d-160">Stel de **NetworkSecurityGroup** eigenschap van de **subnet** variabele **$null** met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-160">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by entering the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $null
    ```

4. <span data-ttu-id="8c77d-161">Sla de wijzigingen aangebracht in het subnet moet u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8c77d-161">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="8c77d-162">Verwachte uitvoer waarin alleen de eigenschappen van de **FrontEnd** subnet.</span><span class="sxs-lookup"><span data-stu-id="8c77d-162">Expected output showing only the properties of the **FrontEnd** subnet.</span></span> <span data-ttu-id="8c77d-163">U ziet dat er zich geen eigenschap voor **NetworkSecurityGroup**:</span><span class="sxs-lookup"><span data-stu-id="8c77d-163">Notice there isn't a property for **NetworkSecurityGroup**:</span></span>
   
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

### <a name="associate-an-nsg-to-a-subnet"></a><span data-ttu-id="8c77d-164">Een NSG aan een subnet koppelt</span><span class="sxs-lookup"><span data-stu-id="8c77d-164">Associate an NSG to a subnet</span></span>
<span data-ttu-id="8c77d-165">Om te koppelen de **NSG-FrontEnd** NSG aan de **FronEnd** subnet opnieuw, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8c77d-165">To associate the **NSG-FrontEnd** NSG to the **FronEnd** subnet again, complete the following steps:</span></span>

1. <span data-ttu-id="8c77d-166">Voer de volgende opdracht op te halen van de bestaande VNet en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-166">Run the following command to retrieve the existing VNet and store it in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName RG-NSG -Name TestVNet
    ```

2. <span data-ttu-id="8c77d-167">Voer de volgende opdracht voor het ophalen van de **FrontEnd** subnet en op te slaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-167">Run the following command to retrieve the **FrontEnd** subnet and store it in a variable:</span></span>

    ```powershell
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name FrontEnd
    ```
 
3. <span data-ttu-id="8c77d-168">Voer de volgende opdracht om de bestaande NSG ophalen en opslaan in een variabele:</span><span class="sxs-lookup"><span data-stu-id="8c77d-168">Run the following command to retrieve the existing NSG and store it in a variable:</span></span>

    ```powershell
    $nsg = Get-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd
    ```

4. <span data-ttu-id="8c77d-169">Stel de **NetworkSecurityGroup** eigenschap van de **subnet** variabele **$null** met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8c77d-169">Set the **NetworkSecurityGroup** property of the **subnet** variable to **$null** by running the following command:</span></span>

    ```powershell
    $subnet.NetworkSecurityGroup = $nsg
    ```

5. <span data-ttu-id="8c77d-170">Sla de wijzigingen aangebracht in het subnet moet u de volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8c77d-170">To save the changes made to the subnet, run the following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

    <span data-ttu-id="8c77d-171">Verwachte uitvoer waarin alleen de **NetworkSecurityGroup** eigenschap van de **FrontEnd** subnet:</span><span class="sxs-lookup"><span data-stu-id="8c77d-171">Expected output showing only the **NetworkSecurityGroup** property of the **FrontEnd** subnet:</span></span>
   
        ...
        "NetworkSecurityGroup": {
                                  "SecurityRules": [],
                                  "DefaultSecurityRules": [],
                                  "NetworkInterfaces": [],
                                  "Subnets": [],
                                  "Id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd"
                                }
        ...

## <a name="delete-an-nsg"></a><span data-ttu-id="8c77d-172">Een NSG verwijderen</span><span class="sxs-lookup"><span data-stu-id="8c77d-172">Delete an NSG</span></span>
<span data-ttu-id="8c77d-173">U kunt een NSG alleen verwijderen als deze niet aan een resource zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8c77d-173">You can only delete an NSG if it's not associated to any resource.</span></span> <span data-ttu-id="8c77d-174">Volg de onderstaande stappen voor het verwijderen van een NSG.</span><span class="sxs-lookup"><span data-stu-id="8c77d-174">To delete an NSG, follow the steps below.</span></span>

1. <span data-ttu-id="8c77d-175">Om te controleren van de resources die zijn gekoppeld aan een NSG, voer de `azure network nsg show` zoals weergegeven in [weergave nsg's koppelingen](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="8c77d-175">To check the resources associated to an NSG, run the `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="8c77d-176">Als de NSG gekoppeld aan een NIC's is, voert u de `azure network nic set` zoals in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC) voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="8c77d-176">If the NSG is associated to any NICs, run the `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="8c77d-177">Als de NSG gekoppeld aan een subnet is, voert u de `azure network vnet subnet set` zoals in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet) voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="8c77d-177">If the NSG is associated to any subnet, run the `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="8c77d-178">Voer de volgende opdracht voor het verwijderen van de NSG:</span><span class="sxs-lookup"><span data-stu-id="8c77d-178">To delete the NSG, run the following command:</span></span>

    ```powershell
    Remove-AzureRmNetworkSecurityGroup -ResourceGroupName RG-NSG -Name NSG-FrontEnd -Force
    ```
   
   > [!NOTE]
   > <span data-ttu-id="8c77d-179">De `-Force` parameter zorgt ervoor dat u hoeft niet te bevestigen.</span><span class="sxs-lookup"><span data-stu-id="8c77d-179">The `-Force` parameter ensures you don't need to confirm the deletion.</span></span>
   > 

## <a name="next-steps"></a><span data-ttu-id="8c77d-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8c77d-180">Next steps</span></span>
* <span data-ttu-id="8c77d-181">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="8c77d-181">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

