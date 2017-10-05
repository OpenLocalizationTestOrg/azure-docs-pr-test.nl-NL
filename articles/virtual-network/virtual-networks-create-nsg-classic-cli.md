---
title: Het nsg's maken in de klassieke modus met de Azure CLI | Microsoft Docs
description: Meer informatie over het maken en nsg's implementeren in de klassieke modus met de Azure CLI
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: 17d98950-5fbb-4653-bef6-d822ab37541e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 115a1937a4c88ba2b986a40c84b1b759ed5e03b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-nsgs-classic-in-the-azure-cli"></a><span data-ttu-id="a857f-103">Het nsg's (klassiek) maken in de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="a857f-103">How to create NSGs (classic) in the Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="a857f-104">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="a857f-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="a857f-105">U kunt ook [nsg's maken in het Resource Manager-implementatiemodel](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a857f-105">You can also [create NSGs in the Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="a857f-106">De Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van het bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="a857f-106">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="a857f-107">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, eerst de testomgeving door bouwen [maken van een VNet](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a857f-107">If you want to run the commands as they are displayed in this document, first build the test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-create-the-nsg-for-the-front-end-subnet"></a><span data-ttu-id="a857f-108">Het maken van het NSG voor de front-end-subnet</span><span class="sxs-lookup"><span data-stu-id="a857f-108">How to create the NSG for the front end subnet</span></span>
<span data-ttu-id="a857f-109">Een NSG met de naam te maken met de naam **NSG-FrontEnd** op basis van het bovenstaande scenario, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="a857f-109">To create an NSG named named **NSG-FrontEnd** based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="a857f-110">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="a857f-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="a857f-111">Voer de  **`azure config mode`**  opdracht uit om te schakelen naar de klassieke modus, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="a857f-111">Run the **`azure config mode`** command to switch to classic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="a857f-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="a857f-113">Voer de  **`azure network nsg create`**  opdracht voor het maken van een NSG.</span><span class="sxs-lookup"><span data-stu-id="a857f-113">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="a857f-114">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : NSG-FrontEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="a857f-115">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a857f-115">Parameters:</span></span>
   
   * <span data-ttu-id="a857f-116">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-116">**-l (or --location)**.</span></span> <span data-ttu-id="a857f-117">Azure-regio waar de nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a857f-117">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="a857f-118">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="a857f-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="a857f-119">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-119">**-n (or --name)**.</span></span> <span data-ttu-id="a857f-120">Naam voor de nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="a857f-120">Name for the new NSG.</span></span> <span data-ttu-id="a857f-121">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a857f-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="a857f-122">Voer de  **`azure network nsg rule create`**  opdracht maakt u een regel waarmee toegang tot poort 3389 (RDP) van het Internet.</span><span class="sxs-lookup"><span data-stu-id="a857f-122">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 3389 (RDP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="a857f-123">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : rdp-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 3389
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
   
    <span data-ttu-id="a857f-124">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a857f-124">Parameters:</span></span>
   
   * <span data-ttu-id="a857f-125">**-a (of--nsg-naam)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="a857f-126">Naam van de NSG waarin de regel wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a857f-126">Name of the NSG in which the rule will be created.</span></span> <span data-ttu-id="a857f-127">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a857f-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="a857f-128">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-128">**-n (or --name)**.</span></span> <span data-ttu-id="a857f-129">Naam voor de nieuwe regel.</span><span class="sxs-lookup"><span data-stu-id="a857f-129">Name for the new rule.</span></span> <span data-ttu-id="a857f-130">In ons scenario *rdp-regel*.</span><span class="sxs-lookup"><span data-stu-id="a857f-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="a857f-131">**-c (of--actie)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-131">**-c (or --action)**.</span></span> <span data-ttu-id="a857f-132">Toegangsniveau voor de regel (weigeren of toestaan).</span><span class="sxs-lookup"><span data-stu-id="a857f-132">Access level for the rule (Deny or Allow).</span></span>
   * <span data-ttu-id="a857f-133">**-p (of--protocol)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="a857f-134">Protocol (Tcp, Udp of *) voor de regel.</span><span class="sxs-lookup"><span data-stu-id="a857f-134">Protocol (Tcp, Udp, or *) for the rule.</span></span>
   * <span data-ttu-id="a857f-135">**-r (of--type)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-135">**-r (or --type)**.</span></span> <span data-ttu-id="a857f-136">Richting van de verbinding (inkomend of uitgaand).</span><span class="sxs-lookup"><span data-stu-id="a857f-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="a857f-137">**-y (of--prioriteit)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-137">**-y (or --priority)**.</span></span> <span data-ttu-id="a857f-138">Prioriteit voor de regel.</span><span class="sxs-lookup"><span data-stu-id="a857f-138">Priority for the rule.</span></span>
   * <span data-ttu-id="a857f-139">**-f (of--bron adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="a857f-140">Voorvoegsel voor bronadres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="a857f-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="a857f-141">**-o (of--bronpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="a857f-142">Bronpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="a857f-142">Source port, or port range.</span></span>
   * <span data-ttu-id="a857f-143">**-e (of--bestemming adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="a857f-144">Voorvoegsel voor doeladres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="a857f-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="a857f-145">**-u (of--doelpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="a857f-146">Doelpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="a857f-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="a857f-147">Voer de  **`azure network nsg rule create`**  opdracht voor het maken van een regel die toegang tot poort 80 (HTTP) van het Internet is.</span><span class="sxs-lookup"><span data-stu-id="a857f-147">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 80 (HTTP) from the Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="a857f-148">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="a857f-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-FrontEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : INTERNET
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 200
        info:    network nsg rule create command OK
6. <span data-ttu-id="a857f-149">Voer de  **`azure network nsg subnet add`**  opdracht het NSG koppelen aan de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="a857f-149">Run the **`azure network nsg subnet add`** command to link the NSG to the front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="a857f-150">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-FrontEnd"
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-to-create-the-nsg-for-the-back-end-subnet"></a><span data-ttu-id="a857f-151">Het maken van het NSG voor de back-end-subnet</span><span class="sxs-lookup"><span data-stu-id="a857f-151">How to create the NSG for the back end subnet</span></span>
<span data-ttu-id="a857f-152">Een NSG met de naam te maken met de naam *NSG-back-end* op basis van het bovenstaande scenario, volg de onderstaande stappen.</span><span class="sxs-lookup"><span data-stu-id="a857f-152">To create an NSG named named *NSG-BackEnd* based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="a857f-153">Voer de  **`azure network nsg create`**  opdracht voor het maken van een NSG.</span><span class="sxs-lookup"><span data-stu-id="a857f-153">Run the **`azure network nsg create`** command to create an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="a857f-154">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : NSG-BackEnd
        data:    Location                        : West US
        data:    Security group rules:
        data:    Name                               Source IP           Source Port  Destination IP   Destination Port  Protocol  Type      Action  Prior
        ity  Default
        data:    ---------------------------------  ------------------  -----------  ---------------  ----------------  --------  --------  ------  -----
        ---  -------
        data:    ALLOW VNET OUTBOUND                VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Outbound  Allow   65000
             true   
        data:    ALLOW VNET INBOUND                 VIRTUAL_NETWORK     *            VIRTUAL_NETWORK  *                 *         Inbound   Allow   65000
             true   
        data:    ALLOW AZURE LOAD BALANCER INBOUND  AZURE_LOADBALANCER  *            *                *                 *         Inbound   Allow   65001
             true   
        data:    ALLOW INTERNET OUTBOUND            *                   *            INTERNET         *                 *         Outbound  Allow   65001
             true   
        data:    DENY ALL OUTBOUND                  *                   *            *                *                 *         Outbound  Deny    65500
             true   
        data:    DENY ALL INBOUND                   *                   *            *                *                 *         Inbound   Deny    65500
             true   
        info:    network nsg create command OK
   
    <span data-ttu-id="a857f-155">Parameters:</span><span class="sxs-lookup"><span data-stu-id="a857f-155">Parameters:</span></span>
   
   * <span data-ttu-id="a857f-156">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-156">**-l (or --location)**.</span></span> <span data-ttu-id="a857f-157">Azure-regio waar de nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a857f-157">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="a857f-158">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="a857f-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="a857f-159">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="a857f-159">**-n (or --name)**.</span></span> <span data-ttu-id="a857f-160">Naam voor de nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="a857f-160">Name for the new NSG.</span></span> <span data-ttu-id="a857f-161">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="a857f-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="a857f-162">Voer de  **`azure network nsg rule create`**  opdracht maakt u een regel waarmee toegang tot poort 1433 (SQL) van de front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="a857f-162">Run the **`azure network nsg rule create`** command to create a rule that allows access to port 1433 (SQL) from the front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="a857f-163">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : sql-rule
        data:    Source address prefix           : 192.168.1.0/24
        data:    Source Port                     : *
        data:    Destination address prefix      : *
        data:    Destination Port                : 1433
        data:    Protocol                        : TCP
        data:    Type                            : Inbound
        data:    Action                          : Allow
        data:    Priority                        : 100
        info:    network nsg rule create command OK
3. <span data-ttu-id="a857f-164">Voer de  **`azure network nsg rule create`**  opdracht voor het maken van een regel die de toegang met Internet weigert.</span><span class="sxs-lookup"><span data-stu-id="a857f-164">Run the **`azure network nsg rule create`** command to create a rule that denies access to the Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="a857f-165">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="a857f-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up the network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up the network security group "NSG-BackEnd"
        data:    Name                            : web-rule
        data:    Source address prefix           : *
        data:    Source Port                     : *
        data:    Destination address prefix      : INTERNET
        data:    Destination Port                : 80
        data:    Protocol                        : TCP
        data:    Type                            : Outbound
        data:    Action                          : Deny
        data:    Priority                        : 200
        info:    network nsg rule create command OK
4. <span data-ttu-id="a857f-166">Voer de  **`azure network nsg subnet add`**  opdracht het NSG koppelen aan het subnet voor back-end.</span><span class="sxs-lookup"><span data-stu-id="a857f-166">Run the **`azure network nsg subnet add`** command to link the NSG to the back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="a857f-167">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a857f-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up the network security group "NSG-BackEndX"
        info:    Looking up the subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

