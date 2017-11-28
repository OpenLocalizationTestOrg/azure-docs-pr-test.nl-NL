---
title: aaaManage netwerkbeveiligingsgroepen - Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe toomanage netwerkbeveiligingsgroepen met behulp van Azure-opdrachtregelinterface (CLI) 1.0 Hallo.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/21/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9a429f947abbcb5fa6adb40c84504f68efd5e20e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="bc855-103">Netwerkbeveiligingsgroepen met behulp van Azure CLI 1.0 Hallo beheren</span><span class="sxs-lookup"><span data-stu-id="bc855-103">Manage network security groups using hello Azure CLI 1.0</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="bc855-104">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="bc855-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="bc855-105">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="bc855-106">[Azure CLI 1.0](#View-existing-NSGs) – onze CLI voor Hallo klassieke en resource management implementatiemodellen</span><span class="sxs-lookup"><span data-stu-id="bc855-106">[Azure CLI 1.0](#View-existing-NSGs) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="bc855-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) -onze volgende generatie CLI voor Hallo resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="bc855-107">[Azure CLI 2.0](virtual-network-manage-nsg-arm-cli.md) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-network-manage-nsg-intro-include.md](../../includes/virtual-network-manage-nsg-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="bc855-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="bc855-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="bc855-109">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van het klassieke implementatiemodel hello aanbeveelt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bc855-109">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-manage-nsg-arm-scenario-include.md](../../includes/virtual-network-manage-nsg-arm-scenario-include.md)]

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="retrieve-information"></a><span data-ttu-id="bc855-110">Informatie ophalen</span><span class="sxs-lookup"><span data-stu-id="bc855-110">Retrieve Information</span></span>
<span data-ttu-id="bc855-111">U kunt uw bestaande nsg's weergeven, regels voor een bestaande NSG ophalen en weten welke resources een NSG is gekoppeld aan.</span><span class="sxs-lookup"><span data-stu-id="bc855-111">You can view your existing NSGs, retrieve rules for an existing NSG, and find out what resources an NSG is associated to.</span></span>

### <a name="view-existing-nsgs"></a><span data-ttu-id="bc855-112">Bestaande nsg's weergeven</span><span class="sxs-lookup"><span data-stu-id="bc855-112">View existing NSGs</span></span>
<span data-ttu-id="bc855-113">tooview hello lijst met nsg's in een specifieke resourcegroep of Voer Hallo `azure network nsg list` opdracht zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bc855-113">tooview hello list of NSGs in a specific resource group, run hello `azure network nsg list` command as shown below.</span></span>

```azurecli
azure network nsg list --resource-group RG-NSG
```

<span data-ttu-id="bc855-114">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-114">Expected output:</span></span>

    info:    Executing command network nsg list
    + Getting hello network security groups
    data:    Name          Location
    data:    ------------  --------
    data:    NSG-BackEnd   westus
    data:    NSG-FrontEnd  westus
    info:    network nsg list command OK

### <a name="list-all-rules-for-an-nsg"></a><span data-ttu-id="bc855-115">Lijst met alle regels voor een NSG</span><span class="sxs-lookup"><span data-stu-id="bc855-115">List all rules for an NSG</span></span>
<span data-ttu-id="bc855-116">tooview hello regels van een NSG met de naam **NSG-FrontEnd**, voert hello `azure network nsg show` opdracht zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bc855-116">tooview hello rules of an NSG named **NSG-FrontEnd**, run hello `azure network nsg show` command as shown below.</span></span> 

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd
```

<span data-ttu-id="bc855-117">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-117">Expected output:</span></span>

    info:    Executing command network nsg show
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Name                            : NSG-FrontEnd
    data:    Type                            : Microsoft.Network/networkSecurityGroups
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    Tags                            : displayName=NSG - Front End
    data:    Security group rules:
    data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
    data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
    data:    rdp-rule                       Internet           *            *               3389              Tcp       Inbound    Allow   100
    data:    web-rule                       Internet           *            *               80                Tcp       Inbound    Allow   101
    data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000
    data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001
    data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500
    data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000
    data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001
    data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500
    info:    network nsg show command OK

> [!NOTE]
> <span data-ttu-id="bc855-118">U kunt ook `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist Hallo regels uit Hallo **NSG-FrontEnd** NSG.</span><span class="sxs-lookup"><span data-stu-id="bc855-118">You can also use `azure network nsg rule list --resource-group RG-NSG --nsg-name NSG-FrontEnd` toolist hello rules from hello **NSG-FrontEnd** NSG.</span></span>
>

### <a name="view-nsg-associations"></a><span data-ttu-id="bc855-119">Weergave NSG koppelingen</span><span class="sxs-lookup"><span data-stu-id="bc855-119">View NSG associations</span></span>

<span data-ttu-id="bc855-120">tooview welke resources Hallo **NSG-FrontEnd** NSG koppelen aan, voert Hallo is `azure network nsg show` opdracht zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="bc855-120">tooview what resources hello **NSG-FrontEnd** NSG is associate with, run hello `azure network nsg show` command as shown below.</span></span> <span data-ttu-id="bc855-121">U ziet dat Hallo enige verschil Hallo gebruik van Hallo is **--json** parameter.</span><span class="sxs-lookup"><span data-stu-id="bc855-121">Notice that hello only difference is hello use of hello **--json** parameter.</span></span>

```azurecli
azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json
```

<span data-ttu-id="bc855-122">Zoek naar Hallo **networkInterfaces** en **subnetten** eigenschappen zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="bc855-122">Look for hello **networkInterfaces** and **subnets** properties as shown below:</span></span>

    "networkInterfaces": [],
    ...
    "subnets": [
        {
            "id": "/subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
        }
    ],
    ...

<span data-ttu-id="bc855-123">Hallo bovenstaande voorbeeld Hallo NSG niet is gekoppeld tooany netwerkinterfaces (NIC's) en het bijbehorende tooa subnet met de naam is **FrontEnd**.</span><span class="sxs-lookup"><span data-stu-id="bc855-123">In hello example above, hello NSG is not associated tooany network interfaces (NICs), and it is associated tooa subnet named **FrontEnd**.</span></span>

## <a name="manage-rules"></a><span data-ttu-id="bc855-124">Regels beheren</span><span class="sxs-lookup"><span data-stu-id="bc855-124">Manage rules</span></span>
<span data-ttu-id="bc855-125">U kunt regels tooan bestaande NSG toevoegen, bestaande regels bewerken en regels te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc855-125">You can add rules tooan existing NSG, edit existing rules, and remove rules.</span></span>

### <a name="add-a-rule"></a><span data-ttu-id="bc855-126">Een regel toevoegen</span><span class="sxs-lookup"><span data-stu-id="bc855-126">Add a rule</span></span>
<span data-ttu-id="bc855-127">tooadd een regel waarmee **inkomende** verkeer tooport **443** van een machine toohello **NSG-FrontEnd** NSG, Voer Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bc855-127">tooadd a rule allowing **inbound** traffic tooport **443** from any machine toohello **NSG-FrontEnd** NSG, enter hello following command:</span></span>

```azurecli
azure network nsg rule create --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --description "Allow access tooport 443 for HTTPS" \
    --protocol Tcp \
    --source-address-prefix * \
    --source-port-range * \
    --destination-address-prefix * \
    --destination-port-range 443 \
    --access Allow \
    --priority 102 \
    --direction Inbound
```

<span data-ttu-id="bc855-128">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-128">Expected output:</span></span>

    info:    Executing command network nsg rule create
    + Looking up hello network security rule "allow-https"
    + Creating a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : *
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule create command OK

### <a name="change-a-rule"></a><span data-ttu-id="bc855-129">Een regel wijzigen</span><span class="sxs-lookup"><span data-stu-id="bc855-129">Change a rule</span></span>
<span data-ttu-id="bc855-130">toochange hello regel bovenstaande tooallow binnenkomend verkeer van Hallo **Internet** alleen, voert hello volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="bc855-130">toochange hello rule created above tooallow inbound traffic from hello **Internet** only, run hello following command:</span></span>

```azurecli
azure network nsg rule set --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --source-address-prefix Internet
```

<span data-ttu-id="bc855-131">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-131">Expected output:</span></span>

    info:    Executing command network nsg rule set
    + Looking up hello network security group "NSG-FrontEnd"
    + Setting a network security rule "allow-https"
    + Looking up hello network security group "NSG-FrontEnd"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/allow-https
    data:    Name                            : allow-https
    data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
    data:    Provisioning state              : Succeeded
    data:    Description                     : Allow access tooport 443 for HTTPS
    data:    Source IP                       : Internet
    data:    Source Port                     : *
    data:    Destination IP                  : *
    data:    Destination Port                : 443
    data:    Protocol                        : Tcp
    data:    Direction                       : Inbound
    data:    Access                          : Allow
    data:    Priority                        : 102
    info:    network nsg rule set command OK

### <a name="delete-a-rule"></a><span data-ttu-id="bc855-132">Een regel verwijderen</span><span class="sxs-lookup"><span data-stu-id="bc855-132">Delete a rule</span></span>
<span data-ttu-id="bc855-133">toodelete hello regel gemaakt hierboven Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-133">toodelete hello rule created above, run hello following command:</span></span>

```azurecli
azure network nsg rule delete --resource-group RG-NSG \
    --nsg-name NSG-FrontEnd \
    --name allow-https \
    --quiet
```

> [!NOTE]
> <span data-ttu-id="bc855-134">Hallo `--quiet` parameter zorgt ervoor dat u hoeft niet tooconfirm Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc855-134">hello `--quiet` parameter ensures you don't need tooconfirm hello deletion.</span></span>
>

<span data-ttu-id="bc855-135">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-135">Expected output:</span></span>

    info:    Executing command network nsg rule delete
    + Looking up hello network security group "NSG-FrontEnd"
    + Deleting network security rule "allow-https"
    info:    network nsg rule delete command OK

## <a name="manage-associations"></a><span data-ttu-id="bc855-136">Koppelingen beheren</span><span class="sxs-lookup"><span data-stu-id="bc855-136">Manage associations</span></span>
<span data-ttu-id="bc855-137">U kunt een NSG toosubnets en NIC's kunt koppelen.</span><span class="sxs-lookup"><span data-stu-id="bc855-137">You can associate an NSG toosubnets and NICs.</span></span> <span data-ttu-id="bc855-138">U kunt ook een NSG van elke bron die deze gekoppeld ontkoppelen.</span><span class="sxs-lookup"><span data-stu-id="bc855-138">You can also dissociate an NSG from any resource it's associated to.</span></span>

### <a name="associate-an-nsg-tooa-nic"></a><span data-ttu-id="bc855-139">Een NSG tooa NIC koppelen</span><span class="sxs-lookup"><span data-stu-id="bc855-139">Associate an NSG tooa NIC</span></span>
<span data-ttu-id="bc855-140">Hallo tooassociate **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-140">tooassociate hello **NSG-FrontEnd** NSG toohello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG \
    --name TestNICWeb1 \
    --network-security-group-name NSG-FrontEnd
```

<span data-ttu-id="bc855-141">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-141">Expected output:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Looking up hello network security group "NSG-FrontEnd"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Network security group          : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
    data:    Virtual machine                 : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-nic"></a><span data-ttu-id="bc855-142">Een NSG van een NIC ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="bc855-142">Dissociate an NSG from a NIC</span></span>

<span data-ttu-id="bc855-143">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **TestNICWeb1** NIC, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-143">toodissociate hello **NSG-FrontEnd** NSG from hello **TestNICWeb1** NIC, run hello following command:</span></span>

```azurecli
azure network nic set --resource-group RG-NSG --name TestNICWeb1 --network-security-group-id ""
```

> [!NOTE]
> <span data-ttu-id="bc855-144">Kennisgeving Hallo ' ' (lege) waarde voor Hallo `network-security-group-id` parameter.</span><span class="sxs-lookup"><span data-stu-id="bc855-144">Notice hello "" (empty) value for hello `network-security-group-id` parameter.</span></span> <span data-ttu-id="bc855-145">Dit is hoe u een koppeling tooan NSG verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bc855-145">That is how you remove an association tooan NSG.</span></span> <span data-ttu-id="bc855-146">Niet dezelfde hello Hallo `network-security-group-name` parameter.</span><span class="sxs-lookup"><span data-stu-id="bc855-146">You can't do hello same with hello `network-security-group-name` parameter.</span></span>
> 

<span data-ttu-id="bc855-147">Verwachte resultaat:</span><span class="sxs-lookup"><span data-stu-id="bc855-147">Expected result:</span></span>

    info:    Executing command network nic set
    + Looking up hello network interface "TestNICWeb1"
    + Updating network interface "TestNICWeb1"
    + Looking up hello network interface "TestNICWeb1"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1
    data:    Name                            : TestNICWeb1
    data:    Type                            : Microsoft.Network/networkInterfaces
    data:    Location                        : westus
    data:    Provisioning state              : Succeeded
    data:    MAC address                     : 00-0D-3A-30-A1-F8
    data:    Enable IP forwarding            : false
    data:    Tags                            : displayName=NetworkInterfaces - Web
    data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Compute/virtualMachines/Web1
    data:    IP configurations:
    data:      Name                          : ipconfig1
    data:      Provisioning state            : Succeeded
    data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/publicIPAddresses/TestPIPWeb1
    data:      Private IP address            : 192.168.1.5
    data:      Private IP Allocation Method  : Dynamic
    data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:
    info:    network nic set command OK

### <a name="dissociate-an-nsg-from-a-subnet"></a><span data-ttu-id="bc855-148">Een NSG van een subnet ontkoppelen</span><span class="sxs-lookup"><span data-stu-id="bc855-148">Dissociate an NSG from a subnet</span></span>
<span data-ttu-id="bc855-149">Hallo toodissociate **NSG-FrontEnd** NSG van Hallo **FrontEnd** subnet, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-149">toodissociate hello **NSG-FrontEnd** NSG from hello **FrontEnd** subnet, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-id ""
```

<span data-ttu-id="bc855-150">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-150">Expected output:</span></span>

    info:    Executing command network vnet subnet set
    + Looking up hello subnet "FrontEnd"
    + Setting subnet "FrontEnd"
    + Looking up hello subnet "FrontEnd"
    data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
    data:    Type                            : Microsoft.Network/virtualNetworks/subnets
    data:    ProvisioningState               : Succeeded
    data:    Name                            : FrontEnd
    data:    Address prefix                  : 192.168.1.0/24
    data:    IP configurations:
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
    data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
    data:
    info:    network vnet subnet set command OK

### <a name="associate-an-nsg-tooa-subnet"></a><span data-ttu-id="bc855-151">Een NSG tooa subnet koppelen</span><span class="sxs-lookup"><span data-stu-id="bc855-151">Associate an NSG tooa subnet</span></span>
<span data-ttu-id="bc855-152">Hallo tooassociate **NSG-FrontEnd** NSG toohello **FronEnd** subnet Hallo na de opdracht opnieuw uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-152">tooassociate hello **NSG-FrontEnd** NSG toohello **FronEnd** subnet again, run hello following command:</span></span>

```azurecli
azure network vnet subnet set --resource-group RG-NSG \
    --vnet-name TestVNet \
    --name FrontEnd \
    --network-security-group-name NSG-FronEnd
```

> [!NOTE]
> <span data-ttu-id="bc855-153">Hallo bovenstaande opdracht werkt alleen omdat Hallo **NSG-FrontEnd** hello NSG wordt dezelfde resourcegroep bevinden als het virtuele netwerk Hallo **TestVNet**.</span><span class="sxs-lookup"><span data-stu-id="bc855-153">hello command above only works because hello **NSG-FrontEnd** NSG is in hello same resource group as hello virtual network **TestVNet**.</span></span> <span data-ttu-id="bc855-154">Als Hallo NSG zich in een andere resourcegroep, moet u toouse hello `--network-security-group-id` parameter in plaats daarvan en geef de volledige id Hallo voor Hallo NSG.</span><span class="sxs-lookup"><span data-stu-id="bc855-154">If hello NSG is in a different resource group, you need toouse hello `--network-security-group-id` parameter instead, and provide hello full id for hello NSG.</span></span> <span data-ttu-id="bc855-155">U kunt Hallo-id ophalen door het uitvoeren van `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` en zoekt Hallo **id** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="bc855-155">You can retrieve hello id by running `azure network nsg show --resource-group RG-NSG --name NSG-FrontEnd --json` and looking for hello **id** property.</span></span> 
> 

<span data-ttu-id="bc855-156">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-156">Expected output:</span></span>

        info:    Executing command network vnet subnet set
        + Looking up hello subnet "FrontEnd"
        + Looking up hello network security group "NSG-FrontEnd"
        + Setting subnet "FrontEnd"
        + Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ipConfigurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/RG-NSG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ipConfigurations/ipconfig1
        data:
        info:    network vnet subnet set command OK

## <a name="delete-an-nsg"></a><span data-ttu-id="bc855-157">Een NSG verwijderen</span><span class="sxs-lookup"><span data-stu-id="bc855-157">Delete an NSG</span></span>
<span data-ttu-id="bc855-158">U kunt een NSG alleen verwijderen als het tooany resource niet is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="bc855-158">You can only delete an NSG if it's not associated tooany resource.</span></span> <span data-ttu-id="bc855-159">een NSG toodelete Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="bc855-159">toodelete an NSG, follow hello steps below.</span></span>

1. <span data-ttu-id="bc855-160">toocheck hello resources die zijn gekoppeld tooan NSG, Voer Hallo `azure network nsg show` zoals in [weergave nsg's koppelingen](#View-NSGs-associations).</span><span class="sxs-lookup"><span data-stu-id="bc855-160">toocheck hello resources associated tooan NSG, run hello `azure network nsg show` as shown in [View NSGs associations](#View-NSGs-associations).</span></span>
2. <span data-ttu-id="bc855-161">Als Hallo NSG gekoppeld tooany NIC's is, voert u Hallo `azure network nic set` zoals in [ontkoppelen van een NSG van een NIC](#Dissociate-an-NSG-from-a-NIC) voor elke NIC.</span><span class="sxs-lookup"><span data-stu-id="bc855-161">If hello NSG is associated tooany NICs, run hello `azure network nic set` as shown in [Dissociate an NSG from a NIC](#Dissociate-an-NSG-from-a-NIC) for each NIC.</span></span> 
3. <span data-ttu-id="bc855-162">Als Hallo NSG gekoppeld tooany subnet is, voert u Hallo `azure network vnet subnet set` zoals in [een NSG van een subnet ontkoppelen](#Dissociate-an-NSG-from-a-subnet) voor elk subnet.</span><span class="sxs-lookup"><span data-stu-id="bc855-162">If hello NSG is associated tooany subnet, run hello `azure network vnet subnet set` as shown in [Dissociate an NSG from a subnet](#Dissociate-an-NSG-from-a-subnet) for each subnet.</span></span>
4. <span data-ttu-id="bc855-163">toodelete hello NSG, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bc855-163">toodelete hello NSG, run hello following command:</span></span>

    ```azurecli
    azure network nsg delete --resource-group RG-NSG --name NSG-FrontEnd --quiet
    ```

    <span data-ttu-id="bc855-164">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="bc855-164">Expected output:</span></span>

        info:    Executing command network nsg delete
        + Looking up hello network security group "NSG-FrontEnd"
        + Deleting network security group "NSG-FrontEnd"
        info:    network nsg delete command OK

## <a name="next-steps"></a><span data-ttu-id="bc855-165">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bc855-165">Next steps</span></span>
* <span data-ttu-id="bc855-166">[Logboekregistratie inschakelen](virtual-network-nsg-manage-log.md) voor nsg's.</span><span class="sxs-lookup"><span data-stu-id="bc855-166">[Enable logging](virtual-network-nsg-manage-log.md) for NSGs.</span></span>

