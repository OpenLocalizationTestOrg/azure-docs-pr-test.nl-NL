---
title: Maken van netwerkbeveiligingsgroepen - Azure CLI 1.0 | Microsoft Docs
description: Informatie over het maken en implementeren van netwerkbeveiligingsgroepen met behulp van de Azure CLI 1.0.
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
ms.openlocfilehash: ca8c182651e3c9f2f1f3a85b94361755d8e638d4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-network-security-groups-using-the-azure-cli-10"></a><span data-ttu-id="71a9c-103">Netwerk met behulp van de Azure CLI 1.0 beveiligingsgroepen maken</span><span class="sxs-lookup"><span data-stu-id="71a9c-103">Create network security groups using the Azure CLI 1.0</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="71a9c-104">CLI-versies om de taak uit te voeren</span><span class="sxs-lookup"><span data-stu-id="71a9c-104">CLI versions to complete the task</span></span> 

<span data-ttu-id="71a9c-105">U kunt de taak uitvoeren met behulp van een van de volgende CLI-versies:</span><span class="sxs-lookup"><span data-stu-id="71a9c-105">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="71a9c-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – onze CLI voor het klassieke en resource management-implementatiemodel (in dit artikel)</span><span class="sxs-lookup"><span data-stu-id="71a9c-106">[Azure CLI 1.0](#how-to-create-the-nsg-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="71a9c-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) -onze CLI volgende generatie voor de resource management-implementatiemodel</span><span class="sxs-lookup"><span data-stu-id="71a9c-107">[Azure CLI 2.0](virtual-networks-create-nsg-arm-cli.md) - our next-generation CLI for the resource management deployment model</span></span> 

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="71a9c-108">Dit artikel is van toepassing op het Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="71a9c-108">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="71a9c-109">U kunt ook [nsg's maken in het klassieke implementatiemodel](virtual-networks-create-nsg-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="71a9c-109">You can also [create NSGs in the classic deployment model](virtual-networks-create-nsg-classic-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="71a9c-110">De Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van het bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="71a9c-110">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> 

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="71a9c-111">Het maken van het NSG voor de front-end-subnet</span><span class="sxs-lookup"><span data-stu-id="71a9c-111">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="71a9c-112">Een NSG met de naam te maken met de naam *NSG-FrontEnd* op basis van het bovenstaande scenario, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="71a9c-112">To create an NSG named named *NSG-FrontEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="71a9c-113">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="71a9c-113">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="71a9c-114">Voer de opdracht **azure config mode** uit om over te schakelen naar de modus Resource Manager, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="71a9c-114">Run the **azure config mode** command to switch to Resource Manager mode, as shown below.</span></span>
   
        azure config mode arm
   
    <span data-ttu-id="71a9c-115">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-115">Expected output:</span></span>
   
        info:    New mode is arm
3. <span data-ttu-id="71a9c-116">Voer de **nsg azure-netwerk maken** opdracht voor het maken van een NSG.</span><span class="sxs-lookup"><span data-stu-id="71a9c-116">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-FrontEnd
   
    <span data-ttu-id="71a9c-117">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-117">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="71a9c-118">Parameters:</span><span class="sxs-lookup"><span data-stu-id="71a9c-118">Parameters:</span></span>
   
   * <span data-ttu-id="71a9c-119">**-g (of --resourcegroep)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-119">**-g (or --resource-group)**.</span></span> <span data-ttu-id="71a9c-120">Naam van de resourcegroep waar de NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71a9c-120">Name of the resource group where the NSG will be created.</span></span> <span data-ttu-id="71a9c-121">In ons scenario *TestRG*.</span><span class="sxs-lookup"><span data-stu-id="71a9c-121">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="71a9c-122">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-122">**-l (or --location)**.</span></span> <span data-ttu-id="71a9c-123">Azure-regio waar de nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71a9c-123">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="71a9c-124">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="71a9c-124">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="71a9c-125">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-125">**-n (or --name)**.</span></span> <span data-ttu-id="71a9c-126">Naam voor de nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="71a9c-126">Name for the new NSG.</span></span> <span data-ttu-id="71a9c-127">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="71a9c-127">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="71a9c-128">Voer de **azure-netwerk nsg regel maken** opdracht maakt u een regel waarmee toegang tot poort 3389 (RDP) van het Internet.</span><span class="sxs-lookup"><span data-stu-id="71a9c-128">Run the **azure network nsg rule create** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="71a9c-129">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-129">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        warn:    Using default direction: Inbound
        info:    Looking up the network security rule "rdp-rule"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="71a9c-130">Parameters:</span><span class="sxs-lookup"><span data-stu-id="71a9c-130">Parameters:</span></span>
   
   * <span data-ttu-id="71a9c-131">**-a (of--nsg-naam)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-131">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="71a9c-132">Naam van de NSG waarin de regel wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="71a9c-132">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="71a9c-133">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="71a9c-133">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="71a9c-134">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-134">**-n (or --name)**.</span></span> <span data-ttu-id="71a9c-135">Naam voor de nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="71a9c-135">Name for the new rule.</span></span> <span data-ttu-id="71a9c-136">In ons scenario *rdp-regel*.</span><span class="sxs-lookup"><span data-stu-id="71a9c-136">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="71a9c-137">**-c (of--access)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-137">**-c (or --access)**.</span></span> <span data-ttu-id="71a9c-138">Toegangsniveau voor de regel (weigeren of toestaan).</span><span class="sxs-lookup"><span data-stu-id="71a9c-138">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="71a9c-139">**-p (of--protocol)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-139">**-p (or --protocol)**.</span></span> <span data-ttu-id="71a9c-140">Protocol (Tcp, Udp of *) voor de regel.</span><span class="sxs-lookup"><span data-stu-id="71a9c-140">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="71a9c-141">**-r (of--richting)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-141">**-r (or --direction)**.</span></span> <span data-ttu-id="71a9c-142">Richting van de verbinding (inkomend of uitgaand).</span><span class="sxs-lookup"><span data-stu-id="71a9c-142">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="71a9c-143">**-y (of--prioriteit)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-143">**-y (or --priority)**.</span></span> <span data-ttu-id="71a9c-144">Prioriteit voor de regel.</span><span class="sxs-lookup"><span data-stu-id="71a9c-144">Priority for the rule.</span></span>
   * <span data-ttu-id="71a9c-145">**-f (of--bron adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-145">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="71a9c-146">Voorvoegsel voor bronadres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="71a9c-146">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="71a9c-147">**-o (of--bronpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-147">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="71a9c-148">Bronpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="71a9c-148">Source port, or port range.</span></span>
   * <span data-ttu-id="71a9c-149">**-e (of--bestemming adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-149">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="71a9c-150">Voorvoegsel voor doeladres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="71a9c-150">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="71a9c-151">**-u (of--doelpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="71a9c-151">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="71a9c-152">Doelpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="71a9c-152">Destination port, or port range.</span></span>    
5. <span data-ttu-id="71a9c-153">Voer de **azure-netwerk nsg regel maken** opdracht voor het maken van een regel die toegang tot poort 80 (HTTP) van het Internet is.</span><span class="sxs-lookup"><span data-stu-id="71a9c-153">Run the **azure network nsg rule create** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="71a9c-154">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="71a9c-154">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="71a9c-155">Voer de **azure network vnet subnet set** opdracht het NSG koppelen aan de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="71a9c-155">Run the **azure network vnet subnet set** command to link the NSG to the front end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -o NSG-FrontEnd
   
    <span data-ttu-id="71a9c-156">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-156">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="71a9c-157">Het maken van het NSG voor de back-end-subnet</span><span class="sxs-lookup"><span data-stu-id="71a9c-157">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="71a9c-158">Een NSG met de naam te maken met de naam *NSG-back-end* op basis van het bovenstaande scenario, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="71a9c-158">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="71a9c-159">Voer de **nsg azure-netwerk maken** opdracht voor het maken van een NSG.</span><span class="sxs-lookup"><span data-stu-id="71a9c-159">Run the **azure network nsg create** command to create an NSG.</span></span>
   
        azure network nsg create -g TestRG -l westus -n NSG-BackEnd
   
    <span data-ttu-id="71a9c-160">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-160">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
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
2. <span data-ttu-id="71a9c-161">Voer de **azure-netwerk nsg regel maken** opdracht maakt u een regel waarmee toegang tot poort 1433 (SQL) van de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="71a9c-161">Run the **azure network nsg rule create** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="71a9c-162">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-162">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "sql-rule"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
3. <span data-ttu-id="71a9c-163">Voer de **azure-netwerk nsg regel maken** opdracht voor het maken van een regel die op het Internet van de toegang weigert.</span><span class="sxs-lookup"><span data-stu-id="71a9c-163">Run the **azure network nsg rule create** command to create a rule that denies access to the Internet from.</span></span>
   
        azure network nsg rule create -g TestRG -a NSG-BackEnd -n web-rule -c Deny -p * -r Outbound -y 200 -f * -o * -e Internet -u *
   
    <span data-ttu-id="71a9c-164">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="71a9c-164">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security rule "web-rule"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
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
4. <span data-ttu-id="71a9c-165">Voer de **azure network vnet subnet set** opdracht het NSG koppelen aan het subnet voor back-end.</span><span class="sxs-lookup"><span data-stu-id="71a9c-165">Run the **azure network vnet subnet set** command to link the NSG to the back end subnet.</span></span>
   
        azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -o NSG-BackEnd
   
    <span data-ttu-id="71a9c-166">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71a9c-166">Expected output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Setting subnet "BackEnd"
        info:    Looking up the subnet "BackEnd"
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

