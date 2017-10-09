---
title: een virtuele machine met meerdere NIC's - Azure PowerShell aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een virtuele machine met meerdere NIC's met behulp van PowerShell.
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="abb0e-103">Een virtuele machine maken met meerdere NIC's met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb0e-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="abb0e-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb0e-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="abb0e-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="abb0e-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="abb0e-106">Sjabloon</span><span class="sxs-lookup"><span data-stu-id="abb0e-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="abb0e-107">PowerShell (klassiek)</span><span class="sxs-lookup"><span data-stu-id="abb0e-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="abb0e-108">Azure CLI (klassiek)</span><span class="sxs-lookup"><span data-stu-id="abb0e-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="abb0e-109">Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="abb0e-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="abb0e-110">In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="abb0e-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="abb0e-111">Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.</span><span class="sxs-lookup"><span data-stu-id="abb0e-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abb0e-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="abb0e-112">Prerequisites</span></span>
<span data-ttu-id="abb0e-113">Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="abb0e-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="abb0e-114">toocreate voltooien van deze resources Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="abb0e-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="abb0e-115">Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="abb0e-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="abb0e-116">Hallo sjabloon pagina toohello rechts van **bovenliggende resourcegroep**, klikt u op **tooAzure implementeren**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="abb0e-117">Indien nodig, Hallo parameterwaarden te wijzigen en volg de stappen Hallo in hello Azure preview portal toodeploy Hallo-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="abb0e-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="abb0e-118">Zorg ervoor dat de namen van opslagaccounts uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="abb0e-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="abb0e-119">Er kan geen dubbele opslagaccountnamen in Azure.</span><span class="sxs-lookup"><span data-stu-id="abb0e-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="abb0e-120">Hallo back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="abb0e-120">Create hello back-end VMs</span></span>
<span data-ttu-id="abb0e-121">Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="abb0e-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="abb0e-122">**Storage-account voor gegevensschijven**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-122">**Storage account for data disks**.</span></span> <span data-ttu-id="abb0e-123">Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="abb0e-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="abb0e-124">Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.</span><span class="sxs-lookup"><span data-stu-id="abb0e-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="abb0e-125">**NIC's**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-125">**NICs**.</span></span> <span data-ttu-id="abb0e-126">Elke virtuele machine heeft twee NIC's, één voor toegang tot de database, en één voor beheer.</span><span class="sxs-lookup"><span data-stu-id="abb0e-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="abb0e-127">**Beschikbaarheidsset**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-127">**Availability set**.</span></span> <span data-ttu-id="abb0e-128">Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.</span><span class="sxs-lookup"><span data-stu-id="abb0e-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="abb0e-129">Stap 1: uw script starten</span><span class="sxs-lookup"><span data-stu-id="abb0e-129">Step 1 - Start your script</span></span>
<span data-ttu-id="abb0e-130">U kunt downloaden Hallo volledige PowerShell-script gebruikt [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="abb0e-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="abb0e-131">Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.</span><span class="sxs-lookup"><span data-stu-id="abb0e-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="abb0e-132">Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="abb0e-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="abb0e-133">Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.</span><span class="sxs-lookup"><span data-stu-id="abb0e-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="abb0e-134">Hallo bestaande resources die nodig zijn voor uw implementatie worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="abb0e-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="abb0e-135">Stap 2: de benodigde resources voor uw virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="abb0e-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="abb0e-136">Moet u een nieuwe resourcegroep, een opslagaccount voor gegevensschijven hello, toocreate en een beschikbaarheidsset voor alle virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="abb0e-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="abb0e-137">U standaardquery ook nodig Hallo lokale administrator-accountreferenties voor elke virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="abb0e-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="abb0e-138">toocreate uitvoeren van deze resources Hallo volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="abb0e-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="abb0e-139">Maak een nieuwe resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="abb0e-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="abb0e-140">Maak een nieuwe premium storage-account in Hallo resourcegroep die eerder is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="abb0e-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="abb0e-141">Maak een nieuwe beschikbaarheidsset.</span><span class="sxs-lookup"><span data-stu-id="abb0e-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="abb0e-142">Lokale beheerder Hallo account referenties toobe gebruikt voor elke VM ophalen.</span><span class="sxs-lookup"><span data-stu-id="abb0e-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="abb0e-143">Stap 3: Hallo NIC's en back-end virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="abb0e-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="abb0e-144">U moet een lus toocreate toouse zoals veel VM's als u wilt gebruiken en maken Hallo nodig NIC's en virtuele machines in hello for-lus.</span><span class="sxs-lookup"><span data-stu-id="abb0e-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="abb0e-145">toocreate hello NIC's en virtuele machines, uitvoeren Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="abb0e-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="abb0e-146">Start een `for` lus toorepeat Hallo opdrachten toocreate een virtuele machine en twee NIC's vaak als nodig, op basis van de waarde van Hallo Hallo `$numberOfVMs` variabele.</span><span class="sxs-lookup"><span data-stu-id="abb0e-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="abb0e-147">Hallo die NIC voor toegang tot de database gebruikt maken.</span><span class="sxs-lookup"><span data-stu-id="abb0e-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="abb0e-148">Hallo die NIC voor externe toegang gebruikt maken.</span><span class="sxs-lookup"><span data-stu-id="abb0e-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="abb0e-149">U ziet hoe deze NIC een tooit NSG die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="abb0e-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="abb0e-150">Maak `vmConfig` object.</span><span class="sxs-lookup"><span data-stu-id="abb0e-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="abb0e-151">Maak twee gegevensschijven per VM.</span><span class="sxs-lookup"><span data-stu-id="abb0e-151">Create two data disks per VM.</span></span> <span data-ttu-id="abb0e-152">U ziet dat Hallo gegevensschijven in Hallo premium storage-account eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="abb0e-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="abb0e-153">Hallo-besturingssysteem en afbeelding toobe gebruikt voor Hallo VM configureren.</span><span class="sxs-lookup"><span data-stu-id="abb0e-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="abb0e-154">Hallo twee NIC's bovenstaande toohello toevoegen `vmConfig` object.</span><span class="sxs-lookup"><span data-stu-id="abb0e-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="abb0e-155">Hallo OS-schijf maken en Hallo VM maken.</span><span class="sxs-lookup"><span data-stu-id="abb0e-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="abb0e-156">Kennisgeving Hallo `}` eindigt Hallo `for` lus.</span><span class="sxs-lookup"><span data-stu-id="abb0e-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="abb0e-157">Stap 4: Hallo-script uitvoeren</span><span class="sxs-lookup"><span data-stu-id="abb0e-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="abb0e-158">Nu dat u hebt gedownload en gewijzigd Hallo script op basis van uw behoeften runt hij toocreate Hallo-database voor back-end virtuele machines met meerdere NIC's een script.</span><span class="sxs-lookup"><span data-stu-id="abb0e-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="abb0e-159">Sla uw script en voer dit uit Hallo **PowerShell** opdrachtprompt of **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="abb0e-160">Ziet u Hallo initiële uitvoer, als volgt:</span><span class="sxs-lookup"><span data-stu-id="abb0e-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="abb0e-161">Na een paar minuten invullen Hallo referenties gevraagd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="abb0e-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="abb0e-162">Hallo onderstaande uitvoer vertegenwoordigt één VM.</span><span class="sxs-lookup"><span data-stu-id="abb0e-162">hello output below represents a single VM.</span></span> <span data-ttu-id="abb0e-163">Kennisgeving Hallo hele proces duurt 8 minuten toocomplete.</span><span class="sxs-lookup"><span data-stu-id="abb0e-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
