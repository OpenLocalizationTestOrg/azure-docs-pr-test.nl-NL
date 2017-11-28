---
title: aaaHow toocreate nsg's bij het gebruik van de klassieke modus hello Azure CLI | Microsoft Docs
description: Meer informatie over hoe toocreate en nsg's implementeren in de klassieke modus hello Azure CLI gebruiken
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
ms.openlocfilehash: eb78861e10a0dd950bb2c3783ee957d1cce55016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-nsgs-classic-in-hello-azure-cli"></a><span data-ttu-id="963d3-103">Hoe toocreate nsg's (klassiek) in de Azure CLI Hallo</span><span class="sxs-lookup"><span data-stu-id="963d3-103">How toocreate NSGs (classic) in hello Azure CLI</span></span>
[!INCLUDE [virtual-networks-create-nsg-selectors-classic-include](../../includes/virtual-networks-create-nsg-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="963d3-104">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="963d3-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="963d3-105">U kunt ook [nsg's maken in de Resource Manager-implementatiemodel Hallo](virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="963d3-105">You can also [create NSGs in hello Resource Manager deployment model](virtual-networks-create-nsg-arm-cli.md).</span></span>

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

<span data-ttu-id="963d3-106">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt op basis van Hallo bovenstaande scenario.</span><span class="sxs-lookup"><span data-stu-id="963d3-106">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="963d3-107">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst Hallo testomgeving door bouwen [maken van een VNet](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="963d3-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment by [creating a VNet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toocreate-hello-nsg-for-hello-front-end-subnet"></a><span data-ttu-id="963d3-108">Hoe toocreate NSG Hallo voor Hallo front-end-subnet</span><span class="sxs-lookup"><span data-stu-id="963d3-108">How toocreate hello NSG for hello front end subnet</span></span>
<span data-ttu-id="963d3-109">toocreate een NSG met de naam met de naam **NSG-FrontEnd** op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="963d3-109">toocreate an NSG named named **NSG-FrontEnd** based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="963d3-110">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="963d3-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="963d3-111">Voer Hallo  **`azure config mode`**  tooswitch tooclassic opdrachtmodus, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="963d3-111">Run hello **`azure config mode`** command tooswitch tooclassic mode, as shown below.</span></span>
   
        azure config mode asm
   
    <span data-ttu-id="963d3-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-112">Expected output:</span></span>
   
        info:    New mode is asm
3. <span data-ttu-id="963d3-113">Voer Hallo  **`azure network nsg create`**  opdracht toocreate een NSG.</span><span class="sxs-lookup"><span data-stu-id="963d3-113">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-FrontEnd
   
    <span data-ttu-id="963d3-114">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-114">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-FrontEnd"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="963d3-115">Parameters:</span><span class="sxs-lookup"><span data-stu-id="963d3-115">Parameters:</span></span>
   
   * <span data-ttu-id="963d3-116">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-116">**-l (or --location)**.</span></span> <span data-ttu-id="963d3-117">Azure-regio waar hello nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="963d3-117">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="963d3-118">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="963d3-118">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="963d3-119">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-119">**-n (or --name)**.</span></span> <span data-ttu-id="963d3-120">Naam voor Hallo nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="963d3-120">Name for hello new NSG.</span></span> <span data-ttu-id="963d3-121">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="963d3-121">For our scenario, *NSG-FrontEnd*.</span></span>
4. <span data-ttu-id="963d3-122">Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 3389 (RDP) van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="963d3-122">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 3389 (RDP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n rdp-rule -c Allow -p Tcp -r Inbound -y 100 -f Internet -o * -e * -u 3389
   
    <span data-ttu-id="963d3-123">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-123">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "rdp-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
   
    <span data-ttu-id="963d3-124">Parameters:</span><span class="sxs-lookup"><span data-stu-id="963d3-124">Parameters:</span></span>
   
   * <span data-ttu-id="963d3-125">**-a (of--nsg-naam)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-125">**-a (or --nsg-name)**.</span></span> <span data-ttu-id="963d3-126">Naam van Hallo NSG in welke Hallo regel wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="963d3-126">Name of hello NSG in which hello rule will be created.</span></span> <span data-ttu-id="963d3-127">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="963d3-127">For our scenario, *NSG-FrontEnd*.</span></span>
   * <span data-ttu-id="963d3-128">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-128">**-n (or --name)**.</span></span> <span data-ttu-id="963d3-129">Naam voor de nieuwe regel Hallo.</span><span class="sxs-lookup"><span data-stu-id="963d3-129">Name for hello new rule.</span></span> <span data-ttu-id="963d3-130">In ons scenario *rdp-regel*.</span><span class="sxs-lookup"><span data-stu-id="963d3-130">For our scenario, *rdp-rule*.</span></span>
   * <span data-ttu-id="963d3-131">**-c (of--actie)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-131">**-c (or --action)**.</span></span> <span data-ttu-id="963d3-132">Toegangsniveau voor Hallo regel (weigeren of toestaan).</span><span class="sxs-lookup"><span data-stu-id="963d3-132">Access level for hello rule (Deny or Allow).</span></span>
   * <span data-ttu-id="963d3-133">**-p (of--protocol)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-133">**-p (or --protocol)**.</span></span> <span data-ttu-id="963d3-134">Protocol (Tcp, Udp of *) voor Hallo regel.</span><span class="sxs-lookup"><span data-stu-id="963d3-134">Protocol (Tcp, Udp, or *) for hello rule.</span></span>
   * <span data-ttu-id="963d3-135">**-r (of--type)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-135">**-r (or --type)**.</span></span> <span data-ttu-id="963d3-136">Richting van de verbinding (inkomend of uitgaand).</span><span class="sxs-lookup"><span data-stu-id="963d3-136">Direction of connection (Inbound or Outbound).</span></span>
   * <span data-ttu-id="963d3-137">**-y (of--prioriteit)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-137">**-y (or --priority)**.</span></span> <span data-ttu-id="963d3-138">Prioriteit voor het Hallo-regel.</span><span class="sxs-lookup"><span data-stu-id="963d3-138">Priority for hello rule.</span></span>
   * <span data-ttu-id="963d3-139">**-f (of--bron adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-139">**-f (or --source-address-prefix)**.</span></span> <span data-ttu-id="963d3-140">Voorvoegsel voor bronadres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="963d3-140">Source address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="963d3-141">**-o (of--bronpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-141">**-o (or --source-port-range)**.</span></span> <span data-ttu-id="963d3-142">Bronpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="963d3-142">Source port, or port range.</span></span>
   * <span data-ttu-id="963d3-143">**-e (of--bestemming adresvoorvoegsel)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-143">**-e (or --destination-address-prefix)**.</span></span> <span data-ttu-id="963d3-144">Voorvoegsel voor doeladres in CIDR- of met standaardlabels.</span><span class="sxs-lookup"><span data-stu-id="963d3-144">Destination address prefix in CIDR or using default tags.</span></span>
   * <span data-ttu-id="963d3-145">**-u (of--doelpoortbereik)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-145">**-u (or --destination-port-range)**.</span></span> <span data-ttu-id="963d3-146">Doelpoort, of een poortbereik.</span><span class="sxs-lookup"><span data-stu-id="963d3-146">Destination port, or port range.</span></span>
5. <span data-ttu-id="963d3-147">Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 80 (HTTP) van Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="963d3-147">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 80 (HTTP) from hello Internet.</span></span>
   
        azure network nsg rule create -a NSG-FrontEnd -n web-rule -c Allow -p Tcp -r Inbound -y 200 -f Internet -o * -e * -u 80
   
    <span data-ttu-id="963d3-148">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="963d3-148">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-FrontEnd"
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
6. <span data-ttu-id="963d3-149">Voer Hallo  **`azure network nsg subnet add`**  opdracht toolink hello NSG toohello front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="963d3-149">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello front end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-FrontEnd --vnet-name TestVNet --subnet-name FrontEnd
   
    <span data-ttu-id="963d3-150">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-150">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-FrontEnd"
        info:    network nsg subnet add command OK

## <a name="how-toocreate-hello-nsg-for-hello-back-end-subnet"></a><span data-ttu-id="963d3-151">Hoe toocreate hello NSG voor Hallo terug subnet beëindigen</span><span class="sxs-lookup"><span data-stu-id="963d3-151">How toocreate hello NSG for hello back end subnet</span></span>
<span data-ttu-id="963d3-152">toocreate een NSG met de naam met de naam *NSG-back-end* op basis van de bovenstaande scenario voor hello, Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="963d3-152">toocreate an NSG named named *NSG-BackEnd* based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="963d3-153">Voer Hallo  **`azure network nsg create`**  opdracht toocreate een NSG.</span><span class="sxs-lookup"><span data-stu-id="963d3-153">Run hello **`azure network nsg create`** command toocreate an NSG.</span></span>
   
        azure network nsg create -l uswest -n NSG-BackEnd
   
    <span data-ttu-id="963d3-154">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-154">Expected output:</span></span>
   
        info:    Executing command network nsg create
        info:    Creating a network security group "NSG-BackEnd"
        info:    Looking up hello network security group "NSG-BackEnd"
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
   
    <span data-ttu-id="963d3-155">Parameters:</span><span class="sxs-lookup"><span data-stu-id="963d3-155">Parameters:</span></span>
   
   * <span data-ttu-id="963d3-156">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-156">**-l (or --location)**.</span></span> <span data-ttu-id="963d3-157">Azure-regio waar hello nieuwe NSG wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="963d3-157">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="963d3-158">In ons scenario *westus*.</span><span class="sxs-lookup"><span data-stu-id="963d3-158">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="963d3-159">**-n (of --naam)**.</span><span class="sxs-lookup"><span data-stu-id="963d3-159">**-n (or --name)**.</span></span> <span data-ttu-id="963d3-160">Naam voor Hallo nieuwe NSG.</span><span class="sxs-lookup"><span data-stu-id="963d3-160">Name for hello new NSG.</span></span> <span data-ttu-id="963d3-161">In ons scenario *NSG-FrontEnd*.</span><span class="sxs-lookup"><span data-stu-id="963d3-161">For our scenario, *NSG-FrontEnd*.</span></span>
2. <span data-ttu-id="963d3-162">Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang tooport 1433 (SQL) van Hallo front-end-subnet.</span><span class="sxs-lookup"><span data-stu-id="963d3-162">Run hello **`azure network nsg rule create`** command toocreate a rule that allows access tooport 1433 (SQL) from hello front end subnet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n sql-rule -c Allow -p Tcp -r Inbound -y 100 -f 192.168.1.0/24 -o * -e * -u 1433
   
    <span data-ttu-id="963d3-163">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-163">Expected output:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "sql-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
3. <span data-ttu-id="963d3-164">Voer Hallo  **`azure network nsg rule create`**  opdracht toocreate een regel waarmee toegang toohello Internet weigert.</span><span class="sxs-lookup"><span data-stu-id="963d3-164">Run hello **`azure network nsg rule create`** command toocreate a rule that denies access toohello Internet.</span></span>
   
        azure network nsg rule create -a NSG-BackEnd -n web-rule -c Deny -p Tcp -r Outbound -y 200 -f * -o * -e Internet -u 80
   
    <span data-ttu-id="963d3-165">Verwachte putput:</span><span class="sxs-lookup"><span data-stu-id="963d3-165">Expected putput:</span></span>
   
        info:    Executing command network nsg rule create
        info:    Looking up hello network security group "NSG-BackEnd"
        info:    Creating a network security rule "web-rule"
        info:    Looking up hello network security group "NSG-BackEnd"
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
4. <span data-ttu-id="963d3-166">Voer Hallo  **`azure network nsg subnet add`**  opdracht toolink hello NSG toohello back-end subnet.</span><span class="sxs-lookup"><span data-stu-id="963d3-166">Run hello **`azure network nsg subnet add`** command toolink hello NSG toohello back end subnet.</span></span>
   
        azure network nsg subnet add -a NSG-BackEnd --vnet-name TestVNet --subnet-name BackEnd
   
    <span data-ttu-id="963d3-167">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="963d3-167">Expected output:</span></span>
   
        info:    Executing command network nsg subnet add
        info:    Looking up hello network security group "NSG-BackEndX"
        info:    Looking up hello subnet "BackEnd"
        info:    Looking up network configuration
        info:    Creating a network security group "NSG-BackEndX"
        info:    network nsg subnet add command OK

