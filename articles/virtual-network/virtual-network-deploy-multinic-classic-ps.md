---
title: een VM (klassiek) met meerdere NIC's - Azure PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een VM (klassiek) met meerdere NIC's met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="698e0-103">Een virtuele machine (klassiek) maken met meerdere NIC's met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="698e0-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="698e0-104">U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="698e0-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="698e0-105">Meerdere NIC's inschakelen scheiding van verkeerstypen tussen NIC's.</span><span class="sxs-lookup"><span data-stu-id="698e0-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="698e0-106">Bijvoorbeeld verbonden een die NIC met Internet, Hallo communiceren kan terwijl een andere alleen met interne bronnen niet communiceert toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="698e0-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="698e0-107">Hallo mogelijkheid tooseparate netwerkverkeer via meerdere NIC's is vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="698e0-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="698e0-108">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="698e0-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="698e0-109">In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo.</span><span class="sxs-lookup"><span data-stu-id="698e0-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="698e0-110">Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="698e0-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="698e0-111">Meer informatie over hoe tooperform deze stappen Hallo [Resource Manager-implementatiemodel](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="698e0-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="698e0-112">Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.</span><span class="sxs-lookup"><span data-stu-id="698e0-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="698e0-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="698e0-113">Prerequisites</span></span>

<span data-ttu-id="698e0-114">Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="698e0-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="698e0-115">toocreate deze resources, volledige Hallo stappen volgen.</span><span class="sxs-lookup"><span data-stu-id="698e0-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="698e0-116">Een virtueel netwerk maken door de stappen te volgen Hallo in Hallo [een virtueel netwerk maken](virtual-networks-create-vnet-classic-netcfg-ps.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="698e0-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="698e0-117">Hallo back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="698e0-117">Create hello back-end VMs</span></span>
<span data-ttu-id="698e0-118">Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="698e0-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="698e0-119">**Subnet backend**.</span><span class="sxs-lookup"><span data-stu-id="698e0-119">**Backend subnet**.</span></span> <span data-ttu-id="698e0-120">Hallo databaseservers zal deel uitmaken van een apart subnet toosegregate verkeer.</span><span class="sxs-lookup"><span data-stu-id="698e0-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="698e0-121">Hallo onderstaande script verwacht in dit subnet tooexist in een vnet met de naam *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="698e0-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="698e0-122">**Storage-account voor gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="698e0-122">**Storage account for data disks**.</span></span> <span data-ttu-id="698e0-123">Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="698e0-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="698e0-124">Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="698e0-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="698e0-125">**Beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="698e0-125">**Availability set**.</span></span> <span data-ttu-id="698e0-126">Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.</span><span class="sxs-lookup"><span data-stu-id="698e0-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="698e0-127">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="698e0-127">Step 1 - Start your script</span></span>
<span data-ttu-id="698e0-128">U kunt downloaden Hallo volledige PowerShell-script gebruikt [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="698e0-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="698e0-129">Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="698e0-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="698e0-130">Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="698e0-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="698e0-131">Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="698e0-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="698e0-132">Stap 2: de benodigde resources voor uw virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="698e0-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="698e0-133">U moet een nieuwe cloudservice en een opslag-voor gegevensschijven Hallo voor alle virtuele machines account toocreate.</span><span class="sxs-lookup"><span data-stu-id="698e0-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="698e0-134">U moet ook toospecify een afbeelding en een lokale administrator-account voor Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="698e0-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="698e0-135">toocreate voltooien van deze resources Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="698e0-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="698e0-136">Maak een nieuwe cloudservice.</span><span class="sxs-lookup"><span data-stu-id="698e0-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="698e0-137">Maak een nieuwe premium storage-account.</span><span class="sxs-lookup"><span data-stu-id="698e0-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="698e0-138">Hallo set storage-account die eerder is gemaakt als Hallo huidige opslagaccount voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="698e0-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="698e0-139">Selecteer een afbeelding voor Hallo VM.</span><span class="sxs-lookup"><span data-stu-id="698e0-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="698e0-140">Hallo lokale administrator-accountreferenties instellen.</span><span class="sxs-lookup"><span data-stu-id="698e0-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="698e0-141">Stap 3: virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="698e0-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="698e0-142">U moet een lus toocreate toouse zoals veel VM's als u wilt gebruiken en maken Hallo nodig NIC's en virtuele machines in hello for-lus.</span><span class="sxs-lookup"><span data-stu-id="698e0-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="698e0-143">toocreate hello NIC's en virtuele machines, uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="698e0-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="698e0-144">Start een `for` lus toorepeat Hallo opdrachten toocreate een virtuele machine en twee NIC's vaak als nodig, op basis van de waarde van Hallo Hallo `$numberOfVMs` variabele.</span><span class="sxs-lookup"><span data-stu-id="698e0-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="698e0-145">Maak een `VMConfig` object Hallo-installatiekopie, grootte en beschikbaarheidsset voor Hallo VM opgeven.</span><span class="sxs-lookup"><span data-stu-id="698e0-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="698e0-146">Hallo VM inrichten als een virtuele machine van Windows.</span><span class="sxs-lookup"><span data-stu-id="698e0-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="698e0-147">Hallo standaard NIC instellen en deze een statisch IP-adres toewijzen.</span><span class="sxs-lookup"><span data-stu-id="698e0-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="698e0-148">Een tweede NIC voor elke virtuele machine toevoegen.</span><span class="sxs-lookup"><span data-stu-id="698e0-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="698e0-149">Toodata schijven maken voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="698e0-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="698e0-150">Elke virtuele machine en end Hallo lus maken.</span><span class="sxs-lookup"><span data-stu-id="698e0-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="698e0-151">Stap 4: Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="698e0-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="698e0-152">Nu dat u hebt gedownload en gewijzigd Hallo script op basis van uw behoeften runt hij toocreate Hallo-database voor back-end virtuele machines met meerdere NIC's een script.</span><span class="sxs-lookup"><span data-stu-id="698e0-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="698e0-153">Sla uw script en voer dit uit Hallo **PowerShell** opdrachtprompt of **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="698e0-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="698e0-154">U ziet Hallo initiële uitvoer, zoals hieronder wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="698e0-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="698e0-155">Hallo-informatie die nodig is in Hallo referenties gevraagd en klik op invullen **OK**.</span><span class="sxs-lookup"><span data-stu-id="698e0-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="698e0-156">onderstaande Hallo-uitvoer geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="698e0-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
