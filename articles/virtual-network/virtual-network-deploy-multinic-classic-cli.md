---
title: een VM (klassiek) met meerdere NIC's - Azure CLI 1.0 aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een VM (klassiek) met meerdere NIC's met behulp van Azure-opdrachtregelinterface (CLI) 1.0 Hallo.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: b436e41e-866c-439f-a7c7-7b4b041725ef
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 181bfb28027caff33410ca94744e79206a2a0d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="42979-103">Een virtuele machine (klassiek) maken met meerdere NIC's met behulp van hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="42979-103">Create a VM (Classic) with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="42979-104">U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="42979-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="42979-105">Meerdere NIC's inschakelen scheiding van verkeerstypen tussen NIC's.</span><span class="sxs-lookup"><span data-stu-id="42979-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="42979-106">Bijvoorbeeld verbonden een die NIC met Internet, Hallo communiceren kan terwijl een andere alleen met interne bronnen niet communiceert toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="42979-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="42979-107">Hallo mogelijkheid tooseparate netwerkverkeer via meerdere NIC's is vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="42979-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="42979-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="42979-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="42979-109">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="42979-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="42979-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="42979-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="42979-111">Meer informatie over hoe tooperform deze stappen Hallo [Resource Manager-implementatiemodel](virtual-network-deploy-multinic-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="42979-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="42979-112">Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.</span><span class="sxs-lookup"><span data-stu-id="42979-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42979-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="42979-113">Prerequisites</span></span>
<span data-ttu-id="42979-114">Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="42979-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="42979-115">toocreate deze resources, volledige Hallo stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="42979-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="42979-116">Een virtueel netwerk maken door de stappen te volgen Hallo in Hallo [een virtueel netwerk maken](virtual-networks-create-vnet-classic-cli.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="42979-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-cli.md) article.</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="deploy-hello-back-end-vms"></a><span data-ttu-id="42979-117">Implementeer Hallo back-end virtuele machines</span><span class="sxs-lookup"><span data-stu-id="42979-117">Deploy hello back-end VMs</span></span>
<span data-ttu-id="42979-118">Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="42979-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="42979-119">**Storage-account voor gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="42979-119">**Storage account for data disks**.</span></span> <span data-ttu-id="42979-120">Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="42979-120">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="42979-121">Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="42979-121">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="42979-122">**NIC's**.</span><span class="sxs-lookup"><span data-stu-id="42979-122">**NICs**.</span></span> <span data-ttu-id="42979-123">Elke virtuele machine heeft twee NIC's, één voor toegang tot de database, en één voor beheer.</span><span class="sxs-lookup"><span data-stu-id="42979-123">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="42979-124">**Beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="42979-124">**Availability set**.</span></span> <span data-ttu-id="42979-125">Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.</span><span class="sxs-lookup"><span data-stu-id="42979-125">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="42979-126">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="42979-126">Step 1 - Start your script</span></span>
<span data-ttu-id="42979-127">U kunt downloaden Hallo volledige bash-script waarmee [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="42979-127">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-cli.sh).</span></span> <span data-ttu-id="42979-128">Voer Hallo stappen toochange Hallo script toowork in uw omgeving te volgen:</span><span class="sxs-lookup"><span data-stu-id="42979-128">Complete hello following steps toochange hello script toowork in your environment:</span></span>

1. <span data-ttu-id="42979-129">Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="42979-129">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    location="useast2"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    ```
2. <span data-ttu-id="42979-130">Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="42979-130">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendCSName="IaaSStory-Backend"
    prmStorageAccountName="iaasstoryprmstorage"
    image="0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskPrefix="db"
    dataDiskName="datadisk"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="42979-131">Stap 2: de benodigde resources voor uw virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="42979-131">Step 2 - Create necessary resources for your VMs</span></span>
1. <span data-ttu-id="42979-132">Maak een nieuwe cloudservice voor alle back-end-VM's.</span><span class="sxs-lookup"><span data-stu-id="42979-132">Create a new cloud service for all backend VMs.</span></span> <span data-ttu-id="42979-133">Gebruik van de kennisgeving Hallo Hallo `$backendCSName` variabele voor naam resourcegroep hello, en `$location` voor hello Azure-regio.</span><span class="sxs-lookup"><span data-stu-id="42979-133">Notice hello use of hello `$backendCSName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure service create --serviceName $backendCSName \
        --location $location
    ```

2. <span data-ttu-id="42979-134">Maak een premium storage-account voor Hallo OS en gegevens schijven toobe die wordt gebruikt door uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="42979-134">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --location $location \
        --type PLRS
    ```

### <a name="step-3---create-vms-with-multiple-nics"></a><span data-ttu-id="42979-135">Stap 3: virtuele machines maken met meerdere NIC 's</span><span class="sxs-lookup"><span data-stu-id="42979-135">Step 3 - Create VMs with multiple NICs</span></span>
1. <span data-ttu-id="42979-136">Start een lus toocreate meerdere virtuele machines, op basis van Hallo `numberOfVMs` variabelen.</span><span class="sxs-lookup"><span data-stu-id="42979-136">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="42979-137">Geef voor elke VM Hallo naam en IP-adres van elk van de Hallo twee NIC's.</span><span class="sxs-lookup"><span data-stu-id="42979-137">For each VM, specify hello name and IP address of each of hello two NICs.</span></span>

    ```azurecli
    nic1Name=$vmNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x

    nic2Name=$vmNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    ```

3. <span data-ttu-id="42979-138">Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="42979-138">Create hello VM.</span></span> <span data-ttu-id="42979-139">Let op Hallo gebruik van Hallo `--nic-config` parameter, met een lijst met alle NIC's met de naam, subnet en IP-adres.</span><span class="sxs-lookup"><span data-stu-id="42979-139">Notice hello usage of hello `--nic-config` parameter, containing a list of all NICs with name, subnet, and IP address.</span></span>

    ```azurecli
    azure vm create $backendCSName $image $username $password \
        --connect $backendCSName \
        --vm-name $vmNamePrefix$suffixNumber \
        --vm-size $vmSize \
        --availability-set $avSetName \
        --blob-url $prmStorageAccountName.blob.core.windows.net/vhds/$osDiskName$suffixNumber.vhd \
        --virtual-network-name $vnetName \
        --subnet-names $backendSubnetName \
        --nic-config $nic1Name:$backendSubnetName:$ipAddress1::,$nic2Name:$backendSubnetName:$ipAddress2::
    ```

4. <span data-ttu-id="42979-140">Maak twee gegevensschijven voor elke VM.</span><span class="sxs-lookup"><span data-stu-id="42979-140">For each VM, create two data disks.</span></span>

    ```azurecli
    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-1.vhd

    azure vm disk attach-new $vmNamePrefix$suffixNumber \
        $diskSize \
        vhds/$dataDiskPrefix$suffixNumber$dataDiskName-2.vhd
    done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="42979-141">Stap 4: Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="42979-141">Step 4 - Run hello script</span></span>
<span data-ttu-id="42979-142">Nu dat u hebt gedownload en gewijzigd Hallo-script op basis van uw behoeften, Hallo script toocreate Hallo terug uitvoeren end-database VM's met meerdere NIC's.</span><span class="sxs-lookup"><span data-stu-id="42979-142">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="42979-143">Sla uw script en voer dit uit uw **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="42979-143">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="42979-144">U ziet Hallo initiële uitvoer, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="42979-144">You will see hello initial output, as shown below.</span></span>

        info:    Executing command service create
        info:    Creating cloud service
        data:    Cloud service name IaaSStory-Backend
        info:    service create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM

2. <span data-ttu-id="42979-145">Hallo uitvoering beëindigd na een paar minuten en ziet u de rest Hallo van Hallo uitvoer zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="42979-145">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>

        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm create
        info:    Looking up image 0b11de9248dd4d87b18621318e037d37__RightImage-Ubuntu-14.04-x64-v14.2.1
        info:    Looking up virtual network
        info:    Looking up cloud service
        info:    Getting cloud service properties
        info:    Looking up deployment
        info:    Creating VM
        info:    OK
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Getting virtual machines
        info:    Adding Data-Disk
        info:    vm disk attach-new command OK
