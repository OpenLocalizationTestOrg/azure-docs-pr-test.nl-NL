---
title: aaaCreate netwerkbeveiligingsgroepen - Azure CLI 1.0 | Microsoft Docs
description: Meer informatie over hoe toocreate en netwerkbeveiligingsgroepen hello Azure CLI 1.0 met implementeren.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/17/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: eeb7feedab959d92659e03c5c46d93fdfc08faea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-hello-azure-cli-10"></a><span data-ttu-id="0bc60-103">Netwerk met behulp van Azure CLI 1.0 Hallo beveiligingsgroepen maken</span><span class="sxs-lookup"><span data-stu-id="0bc60-103">Create network security groups using hello Azure CLI 1.0</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="0bc60-104">CLI-versies toocomplete Hallo taak</span><span class="sxs-lookup"><span data-stu-id="0bc60-104">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="0bc60-105">U kunt met een van de volgende versies van de CLI Hallo Hallo-taak uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0bc60-105">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="0bc60-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – onze CLI voor Hallo klassieke en resource management implementatiemodellen (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="0bc60-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="0bc60-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -onze CLI next generation voor Hallo resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="0bc60-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for hello resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="0bc60-108">In dit artikel bevat informatie over Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="0bc60-108">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="0bc60-109">U kunt ook [nsg's maken in het klassieke implementatiemodel Hallo](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="0bc60-109">You can also [create NSGs in hello classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="0bc60-110">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="0bc60-110">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> 

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="0bc60-111">Hoe toocreate NSG Hallo voor Hallo front-end-subnet</span><span class="sxs-lookup"><span data-stu-id="0bc60-111">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="0bc60-112">toocreate een NSG met de naam met de naam *NSG-FrontEnd* op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="0bc60-112">toocreate an NSG named named *NSG-FrontEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="0bc60-113">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="0bc60-113">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="0bc60-114">Voer Hallo **azure config mode** opdracht tooswitch tooResource modus Manager, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0bc60-114">Run hello **azure config mode** command tooswitch tooResource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="0bc60-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="0bc60-116">Voer Hallo **nsg azure-netwerk maken** opdracht toocreate een NSG.</span><span class="sxs-lookup"><span data-stu-id="0bc60-116">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="0bc60-117">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd
        data:    Name                            : NSG-FrontEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
   
    <span data-ttu-id="0bc60-118">Parameters:</span><span class="sxs-lookup"><span data-stu-id="0bc60-118">Parameters:</span></span>
   
   * <span data-ttu-id="0bc60-119">**-g (of --resourcegroep)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="0bc60-120">Naam van resourcegroep Hallo waar Hallo NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc60-120">Name of hello resource group where hello NSG will be created.</span></span> <span data-ttu-id="0bc60-121">In ons scenario *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="0bc60-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="0bc60-122">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-122">**-l (or --location)**.</span></span> <span data-ttu-id="0bc60-123">Azure-regio waar hello nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc60-123">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="0bc60-124">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="0bc60-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="0bc60-125">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-125">**-n (or --name)**.</span></span> <span data-ttu-id="0bc60-126">Naam voor Hallo nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="0bc60-126">Name for hello new NSG.</span></span> <span data-ttu-id="0bc60-127">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="0bc60-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="0bc60-128">Voer Hallo **azure-netwerk nsg regel maken** opdracht toocreate een regel waarmee toegang tooport 3389 (RDP) van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="0bc60-128">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="0bc60-129">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up hello network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkSecurityGroups/NSG-FrontEnd/securityRules/rdp
        -rule
        data:    Name                            : rdp-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 3389
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="0bc60-130">Parameters:</span><span class="sxs-lookup"><span data-stu-id="0bc60-130">Parameters:</span></span>
   
   * <span data-ttu-id="0bc60-131">**-a (of--nsg-naam)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="0bc60-132">Naam van Hallo NSG in welke Hallo regel wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0bc60-132">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="0bc60-133">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="0bc60-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="0bc60-134">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-134">**-n (or --name)**.</span></span> <span data-ttu-id="0bc60-135">Naam voor de nieuwe regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="0bc60-135">Name for hello new rule.</span></span> <span data-ttu-id="0bc60-136">In ons scenario *rdp-regel*.</span><span class="sxs-lookup"><span data-stu-id="0bc60-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="0bc60-137">**-c (of--access)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-137">**-c (or --access)**.</span></span> <span data-ttu-id="0bc60-138">Toegangsniveau voor Hallo regel (weigeren of toestaan).</span><span class="sxs-lookup"><span data-stu-id="0bc60-138">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="0bc60-139">**-p (of--protocol)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="0bc60-140">Protocol (Tcp, Udp of *) voor Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="0bc60-140">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="0bc60-141">**-r (of--richting)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-141">**-r (or --direction)**.</span></span> <span data-ttu-id="0bc60-142">Richting van de verbinding (inkomend of uitgaand).</span><span class="sxs-lookup"><span data-stu-id="0bc60-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="0bc60-143">**-y (of--prioriteit)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-143">**-y (or --priority)**.</span></span> <span data-ttu-id="0bc60-144">Prioriteit voor het Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="0bc60-144">Priority for hello rule.</span></span>
   * <span data-ttu-id="0bc60-145">**-f (of--bron adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="0bc60-146">Voorvoegsel voor bronadres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="0bc60-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="0bc60-147">**-o (of--bronpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="0bc60-148">Bronpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="0bc60-148">Source port, or port range.</span></span>
   * <span data-ttu-id="0bc60-149">**-e (of--bestemming adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="0bc60-150">Voorvoegsel voor doeladres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="0bc60-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="0bc60-151">**-u (of--doelpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="0bc60-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="0bc60-152">Doelpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="0bc60-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="0bc60-153">Voer Hallo **azure-netwerk nsg regel maken** opdracht toocreate een regel waarmee toegang tooport 80 (HTTP) van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="0bc60-153">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="0bc60-154">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="0bc60-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-FrontEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : Internet
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 80
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="0bc60-155">Voer Hallo **azure network vnet subnet set** opdracht toolink hello NSG toohello front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="0bc60-155">Run hello **azure network vnet subnet set** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="0bc60-156">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb2/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICWeb1/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="0bc60-157">Hoe toocreate hello NSG voor Hallo terug subnet beëindigen</span><span class="sxs-lookup"><span data-stu-id="0bc60-157">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="0bc60-158">toocreate een NSG met de naam met de naam *NSG-back-end* op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="0bc60-158">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="0bc60-159">Voer Hallo **nsg azure-netwerk maken** opdracht toocreate een NSG.</span><span class="sxs-lookup"><span data-stu-id="0bc60-159">Run hello **azure network nsg create** command toocreate an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="0bc60-160">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd
        data:    Name                            : NSG-BackEnd
        data:    Type                            : Microsoft.Network/networkSecurityGroups
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Security group rules:
        data:    Name                           Source IP          Source Port  Destination IP  Destination Port  Protocol  Direction  Access  Priority
        data:    -----------------------------  -----------------  -----------  --------------  ----------------  --------  ---------  ------  --------
        data:    AllowVnetInBound               VirtualNetwork     *            VirtualNetwork  *                 *         Inbound    Allow   65000   
        data:    AllowAzureLoadBalancerInBound  AzureLoadBalancer  *            *               *                 *         Inbound    Allow   65001   
        data:    DenyAllInBound                 *                  *            *               *                 *         Inbound    Deny    65500   
        data:    AllowVnetOutBound              VirtualNetwork     *            VirtualNetwork  *                 *         Outbound   Allow   65000   
        data:    AllowInternetOutBound          *                  *            Internet        *                 *         Outbound   Allow   65001   
        data:    DenyAllOutBound                *                  *            *               *                 *         Outbound   Deny    65500   
        info:    network nsg create command OK
2. <span data-ttu-id="0bc60-161">Voer Hallo **azure-netwerk nsg regel maken** opdracht toocreate een regel waarmee toegang tooport 1433 (SQL) van Hallo front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="0bc60-161">Run hello **azure network nsg rule create** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="0bc60-162">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/sql-rule
        data:    Name                            : sql-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination IP                  : *
        data:    Destination Port                : 1433
        data:    Protocol                        : Tcp
        data:    Direction                       : Inbound
        data:    Access                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="0bc60-163">Voer Hallo **azure-netwerk nsg regel maken** opdracht toocreate een regel waarmee toegang toohello Internet weigert uit.</span><span class="sxs-lookup"><span data-stu-id="0bc60-163">Run hello **azure network nsg rule create** command toocreate a rule that denies access toohello Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="0bc60-164">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="0bc60-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        networkSecurityGroups/NSG-BackEnd/securityRules/web-rule
        data:    Name                            : web-rule
        data:    Type                            : Microsoft.Network/networkSecurityGroups/securityRules
        data:    Provisioning state              : Succeeded
        data:    Source IP                       : *
        data:    Source Port                     : *
        data:    Destination IP                  : Internet
        data:    Destination Port                : *
        data:    Protocol                        : *
        data:    Direction                       : Outbound
        data:    Access                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="0bc60-165">Voer Hallo **azure network vnet subnet set** opdracht toolink hello NSG toohello back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="0bc60-165">Run hello **azure network vnet subnet set** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="0bc60-166">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="0bc60-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up hello subnet "BackEnd"
        data:    Id                              : /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/BackEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : BackEnd
        data:    Address prefix                  : 192.168.2.0/24
        data:    Network security group          : [object Object]
        data:    IP configurations:
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL1/ip
        Configurations/ipconfig1
        data:      /subscriptions/628dad04-b5d1-4f10-b3a4-dc61d88cf97c/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNICSQL2/ip
        Configurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK

