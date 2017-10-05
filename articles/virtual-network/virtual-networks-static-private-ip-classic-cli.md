---
title: "Configureren van privé IP-adressen voor virtuele machines (klassiek) - Azure CLI 1.0 | Microsoft Docs"
description: "Informatie over het configureren van privé IP-adressen voor virtuele machines (klassiek) met behulp van de Azure-opdrachtregelinterface (CLI) 1.0."
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
ms.openlocfilehash: ed0fe2fea20671063395b9ff089599853278989d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-the-azure-cli-10"></a><span data-ttu-id="74b0d-103">Privé IP-adressen voor een virtuele machine (klassiek) met behulp van de Azure CLI 1.0 configureren</span><span class="sxs-lookup"><span data-stu-id="74b0d-103">Configure private IP addresses for a virtual machine (Classic) using the Azure CLI 1.0</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="74b0d-104">Dit artikel is van toepassing op het klassieke implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="74b0d-104">This article covers the classic deployment model.</span></span> <span data-ttu-id="74b0d-105">U kunt ook [een statisch privé IP-adres in het Resource Manager-implementatiemodel beheren](virtual-networks-static-private-ip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="74b0d-105">You can also [manage a static private IP address in the Resource Manager deployment model](virtual-networks-static-private-ip-arm-cli.md).</span></span>

<span data-ttu-id="74b0d-106">De Azure CLI Voorbeeldopdrachten onderstaande verwacht een eenvoudige omgeving al gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74b0d-106">The sample Azure CLI commands below expect a simple environment already created.</span></span> <span data-ttu-id="74b0d-107">Als u wilt de opdrachten uitvoeren zoals ze worden weergegeven in dit document, eerst de testomgeving wordt beschreven in bouwen [een vnet maken](virtual-networks-create-vnet-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="74b0d-107">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-classic-cli.md).</span></span>

## <a name="how-to-specify-a-static-private-ip-address-when-creating-a-vm"></a><span data-ttu-id="74b0d-108">Een statisch privé IP-adres opgeven bij het maken van een virtuele machine</span><span class="sxs-lookup"><span data-stu-id="74b0d-108">How to specify a static private IP address when creating a VM</span></span>
<span data-ttu-id="74b0d-109">Maken van een nieuwe virtuele machine met de naam *DNS01* in een nieuwe cloudservice met de naam *TestService* op basis van het bovenstaande scenario, als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="74b0d-109">To create a new VM named *DNS01* in a new cloud service named *TestService* based on the scenario above, follow these steps:</span></span>

1. <span data-ttu-id="74b0d-110">Als u Azure CLI nog nooit hebt gebruikt, raadpleegt u [De Azure CLI installeren en configureren](../cli-install-nodejs.md) en volgt u de instructies tot het punt waar u uw Azure-account en -abonnement moet selecteren.</span><span class="sxs-lookup"><span data-stu-id="74b0d-110">If you have never used Azure CLI, see [Install and Configure the Azure CLI](../cli-install-nodejs.md) and follow the instructions up to the point where you select your Azure account and subscription.</span></span>
2. <span data-ttu-id="74b0d-111">Voer de **azure service maken** opdracht voor het maken van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="74b0d-111">Run the **azure service create** command to create the cloud service.</span></span>
   
        azure service create TestService --location uscentral
   
    <span data-ttu-id="74b0d-112">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="74b0d-112">Expected output:</span></span>
   
        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name TestService
        info:    service create command OK
3. <span data-ttu-id="74b0d-113">Voer de **azure virtuele machine maken** opdracht voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="74b0d-113">Run the **azure create vm** command to create the VM.</span></span> <span data-ttu-id="74b0d-114">Let op de waarde voor een statisch privé IP-adres.</span><span class="sxs-lookup"><span data-stu-id="74b0d-114">Notice the value for a static private IP address.</span></span> <span data-ttu-id="74b0d-115">De lijst die na de uitvoer wordt weergegeven, beschrijft de gebruikte parameters.</span><span class="sxs-lookup"><span data-stu-id="74b0d-115">The list shown after the output explains the parameters used.</span></span>
   
        azure vm create -l centralus -n DNS01 -w TestVNet -S "192.168.1.101" TestService bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2 adminuser AdminP@ssw0rd
   
    <span data-ttu-id="74b0d-116">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="74b0d-116">Expected output:</span></span>
   
        info:    Executing command vm create
        warn:    --vm-size has not been specified. Defaulting to "Small".
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
   
   * <span data-ttu-id="74b0d-117">**-l (of --locatie)**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-117">**-l (or --location)**.</span></span> <span data-ttu-id="74b0d-118">Azure-regio waar de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74b0d-118">Azure region where the VM will be created.</span></span> <span data-ttu-id="74b0d-119">In ons scenario *centralus*.</span><span class="sxs-lookup"><span data-stu-id="74b0d-119">For our scenario, *centralus*.</span></span>
   * <span data-ttu-id="74b0d-120">**-n (of--vm-naam)**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-120">**-n (or --vm-name)**.</span></span> <span data-ttu-id="74b0d-121">Naam van de virtuele machine moet worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74b0d-121">Name of the VM to be created.</span></span>
   * <span data-ttu-id="74b0d-122">**-w (of--virtuele-netwerknaam)**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-122">**-w (or --virtual-network-name)**.</span></span> <span data-ttu-id="74b0d-123">De naam van de VNet waar de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74b0d-123">Name of the VNet where the VM will be created.</span></span> 
   * <span data-ttu-id="74b0d-124">**-S (of--statisch ip-)**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-124">**-S (or --static-ip)**.</span></span> <span data-ttu-id="74b0d-125">Statische privé IP-adres voor de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="74b0d-125">Static private IP address for the VM.</span></span>
   * <span data-ttu-id="74b0d-126">**TestService**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-126">**TestService**.</span></span> <span data-ttu-id="74b0d-127">Naam van de cloudservice waar de virtuele machine wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74b0d-127">Name of the cloud service where the VM will be created.</span></span>
   * <span data-ttu-id="74b0d-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-128">**bd507d3a70934695bc2128e3e5a255ba__RightImage-Windows-2012R2-x64-v14.2**.</span></span> <span data-ttu-id="74b0d-129">De afbeelding die wordt gebruikt voor het maken van de virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="74b0d-129">Image used to create the VM.</span></span>
   * <span data-ttu-id="74b0d-130">**adminuser**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-130">**adminuser**.</span></span> <span data-ttu-id="74b0d-131">Lokale beheerder voor de virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="74b0d-131">Local administrator for the Windows VM.</span></span>
   * <span data-ttu-id="74b0d-132">**AdminP@ssw0rd**.</span><span class="sxs-lookup"><span data-stu-id="74b0d-132">**AdminP@ssw0rd**.</span></span> <span data-ttu-id="74b0d-133">Lokale administrator-wachtwoord voor de virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="74b0d-133">Local administrator password for the Windows VM.</span></span>

## <a name="how-to-retrieve-static-private-ip-address-information-for-a-vm"></a><span data-ttu-id="74b0d-134">Het statische privé IP-adresgegevens voor een virtuele machine ophalen</span><span class="sxs-lookup"><span data-stu-id="74b0d-134">How to retrieve static private IP address information for a VM</span></span>
<span data-ttu-id="74b0d-135">Voer de volgende opdracht in de Azure CLI om weer te geven het statische privé IP-adresgegevens voor de virtuele machine met het bovenstaande script gemaakt, en houd rekening met de waarde voor *netwerk StaticIP*:</span><span class="sxs-lookup"><span data-stu-id="74b0d-135">To view the static private IP address information for the VM created with the script above, run the following Azure CLI command and observe the value for *Network StaticIP*:</span></span>

    azure vm static-ip show DNS01

<span data-ttu-id="74b0d-136">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="74b0d-136">Expected output:</span></span>

    info:    Executing command vm static-ip show
    info:    Getting virtual machines
    data:    Network StaticIP "192.168.1.101"
    info:    vm static-ip show command OK

## <a name="how-to-remove-a-static-private-ip-address-from-a-vm"></a><span data-ttu-id="74b0d-137">Een statisch privé IP-adres van een virtuele machine verwijderen</span><span class="sxs-lookup"><span data-stu-id="74b0d-137">How to remove a static private IP address from a VM</span></span>
<span data-ttu-id="74b0d-138">Toegevoegd aan de virtuele machine in het bovenstaande script Voer de volgende opdracht in de Azure CLI het statische privé IP-adres verwijderen:</span><span class="sxs-lookup"><span data-stu-id="74b0d-138">To remove the static private IP address added to the VM in the script above, run the following Azure CLI command:</span></span>

    azure vm static-ip remove DNS01

<span data-ttu-id="74b0d-139">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="74b0d-139">Expected output:</span></span>

    info:    Executing command vm static-ip remove
    info:    Getting virtual machines
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip remove command OK

## <a name="how-to-add-a-static-private-ip-to-an-existing-vm"></a><span data-ttu-id="74b0d-140">Een statisch privé IP-adres toevoegen aan een bestaande virtuele machine</span><span class="sxs-lookup"><span data-stu-id="74b0d-140">How to add a static private IP to an existing VM</span></span>
<span data-ttu-id="74b0d-141">Toevoegen van een statisch privé IP-adres aan de virtuele machine gemaakt met behulp van het script hierboven runt de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="74b0d-141">To add a static private IP address to the VM created using the script above, runt he following command:</span></span>

    azure vm static-ip set DNS01 192.168.1.101

<span data-ttu-id="74b0d-142">Verwachte uitvoer:</span><span class="sxs-lookup"><span data-stu-id="74b0d-142">Expected output:</span></span>

    info:    Executing command vm static-ip set
    info:    Getting virtual machines
    info:    Looking up virtual network
    info:    Reading network configuration
    info:    Updating network configuration
    info:    vm static-ip set command OK

## <a name="next-steps"></a><span data-ttu-id="74b0d-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74b0d-143">Next steps</span></span>
* <span data-ttu-id="74b0d-144">Meer informatie over [gereserveerde openbare IP-adres](virtual-networks-reserved-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="74b0d-144">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="74b0d-145">Meer informatie over [instantieniveau openbare IP (ILPIP)](virtual-networks-instance-level-public-ip.md) adressen.</span><span class="sxs-lookup"><span data-stu-id="74b0d-145">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="74b0d-146">Raadpleeg de [gereserveerd IP-REST-API's](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span><span class="sxs-lookup"><span data-stu-id="74b0d-146">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

