---
title: "privé IP-adressen voor virtuele machines (klassiek) - Azure CLI 1.0 aaaConfigure | Microsoft Docs"
description: "Meer informatie over hoe tooconfigure privé IP-adressen voor virtuele machines (klassiek) met Azure-opdrachtregelinterface (CLI) 1.0 Hallo."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 17386acf-c708-4103-9b22-ff9bf04b778d
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 417a57181bcf5c2e6101bf3bdf63fc94ebc99df5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-cli-10"></a><span data-ttu-id="5f7fc-103">Privé IP-adressen voor een virtuele machine (klassiek) met behulp van Azure CLI 1.0 Hallo configureren</span><span class="sxs-lookup"><span data-stu-id="5f7fc-103">Configure private IP addresses for a virtual machine (Classic) using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="5f7fc-104">In dit artikel bevat informatie over Hallo klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-104">This article covers hello classic deployment model.</span></span> <span data-ttu-id="5f7fc-105">U kunt ook [een statisch privé IP-adres in Hallo Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5f7fc-105">You can also [manage a static private IP address in hello Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="5f7fc-106">Hello Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-106">hello sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="5f7fc-107">Als u toorun Hallo opdrachten wilt zoals ze worden weergegeven in dit document, eerst bouwen Hallo testomgeving beschreven in [een vnet maken](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5f7fc-107">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="5f7fc-108">Hoe toospecify een statisch privé IP-adres bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5f7fc-108">How toospecify a static private IP address when creating a VM</span></span>
<span data-ttu-id="5f7fc-109">een nieuwe virtuele machine met de naam toocreate *DNS01* in een nieuwe cloudservice met de naam *TestService* op basis van de bovenstaande Hallo scenario, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-109">toocreate a new VM named *DNS01* in a new cloud service named *TestService* based on hello scenario above, follow these steps:</span></span>

1. <span data-ttu-id="5f7fc-110">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) en volg de instructies Hallo toohello punt waar u uw Azure-account en abonnement selecteren.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-110">If you have never used Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) and follow hello instructions up toohello point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="5f7fc-111">Voer Hallo **azure service maken** opdracht toocreate Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-111">Run hello **azure service create** command toocreate hello cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="5f7fc-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="5f7fc-113">Voer Hallo **azure virtuele machine maken** opdracht toocreate Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-113">Run hello **azure create vm** command toocreate hello VM.</span></span> <span data-ttu-id="5f7fc-114">Let op Hallo-waarde voor een statisch privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-114">Notice hello value for a static private IP address.</span></span> <span data-ttu-id="5f7fc-115">Hallo-lijst die wordt weergegeven na Hallo uitvoer wordt uitgelegd Hallo parameters die worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-115">hello list shown after hello output explains hello parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="5f7fc-116">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting too"Small".
        info:    Looking up image bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2
        info:    Looking up virtual network
        info:    Looking up cloud service
        warn:    --location option will be ignored
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Retrieving storage accounts
        info:    Creating VM
        info:    OK
        info:    vm create command OK
   
   * <span data-ttu-id="5f7fc-117">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-117">**-l (or --location)**.</span></span> <span data-ttu-id="5f7fc-118">Azure-regio waar Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-118">Azure region where hello VM will be created.</span></span> <span data-ttu-id="5f7fc-119">In ons scenario *centralus*.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="5f7fc-120">**-n (of--vm-naam)**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="5f7fc-121">Naam van Hallo VM toobe gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-121">Name of hello VM toobe created.</span></span>
   * <span data-ttu-id="5f7fc-122">**-w (of--virtuele-netwerknaam)**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="5f7fc-123">Naam van Hallo VNet waar Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-123">Name of hello VNet where hello VM will be created.</span></span> 
   * <span data-ttu-id="5f7fc-124">**-S (of--statisch ip-)**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="5f7fc-125">Statisch privé IP-adres Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-125">Static private IP address for hello VM.</span></span>
   * <span data-ttu-id="5f7fc-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-126">**TestService**.</span></span> <span data-ttu-id="5f7fc-127">Naam van de cloudservice Hallo waar Hallo VM wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-127">Name of hello cloud service where hello VM will be created.</span></span>
   * <span data-ttu-id="5f7fc-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="5f7fc-129">Afbeelding die wordt gebruikt toocreate hello VM.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-129">Image used toocreate hello VM.</span></span>
   * <span data-ttu-id="5f7fc-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-130">**adminuser**.</span></span> <span data-ttu-id="5f7fc-131">Lokale beheerder voor de virtuele machine van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-131">Local administrator for hello Windows VM.</span></span>
   * <span data-ttu-id="5f7fc-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="5f7fc-133">Lokale administrator-wachtwoord voor de virtuele machine van Windows hello.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-133">Local administrator password for hello Windows VM.</span></span>

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="5f7fc-134">Hoe de gegevens voor een VM voor het adres van tooretrieve statische privé-IP</span><span class="sxs-lookup"><span data-stu-id="5f7fc-134">How tooretrieve static private IP address information for a VM</span></span>
<span data-ttu-id="5f7fc-135">tooview hello statische privé-IP adresgegevens voor Hallo VM gemaakt met bovenstaande Hallo-script uitvoeren hello Azure CLI-opdracht te volgen en bekijk Hallo-waarde voor *netwerk StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-135">tooview hello static private IP address information for hello VM created with hello script above, run hello following Azure CLI command and observe hello value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="5f7fc-136">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="5f7fc-137">Hoe tooremove een statisch privé IP-adres van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="5f7fc-137">How tooremove a static private IP address from a VM</span></span>
<span data-ttu-id="5f7fc-138">tooremove hello statisch privé IP-adres toegevoegd toohello VM in Hallo script hierboven uitvoeren hello Azure CLI-opdracht te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-138">tooremove hello static private IP address added toohello VM in hello script above, run hello following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="5f7fc-139">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-tooadd-a-static-private-ip-tooan-existing-vm"></a><span data-ttu-id="5f7fc-140">Hoe een statisch privé IP-tooan tooadd bestaande VM</span><span class="sxs-lookup"><span data-stu-id="5f7fc-140">How tooadd a static private IP tooan existing VM</span></span>
<span data-ttu-id="5f7fc-141">tooadd een statisch privé IP-adres toohello VM gemaakt Hallo script hierboven runt met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-141">tooadd a static private IP address toohello VM created using hello script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="5f7fc-142">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f7fc-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="5f7fc-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f7fc-143">Next steps</span></span>
* <span data-ttu-id="5f7fc-144">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5f7fc-145">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="5f7fc-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="5f7fc-146">Raadpleeg Hallo [gereserveerde IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f7fc-146">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

