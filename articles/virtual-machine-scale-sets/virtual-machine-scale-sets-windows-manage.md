---
title: Beheren van virtuele machines in een virtuele-Machineschaalset | Microsoft Docs
description: Virtuele machines in een virtuele-machineschaalset ingesteld met Azure PowerShell beheren.
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d35fa77a-de96-4ccd-a332-eb181d1f4273
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: d09a020b903e5f43afe03b86c675bcc1eb536cbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="24198-103">Beheren van virtuele machines in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="24198-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="24198-104">De taken in dit artikel gebruiken voor het beheren van virtuele machines in uw virtuele-machineschaalset.</span><span class="sxs-lookup"><span data-stu-id="24198-104">Use the tasks in this article to manage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="24198-105">De meeste taken die betrekking hebben op het beheren van een virtuele machine in een schaalset vereisen dat u weet dat de exemplaar-ID van de computer die u wilt beheren.</span><span class="sxs-lookup"><span data-stu-id="24198-105">Most of the tasks that involve managing a virtual machine in a scale set require that you know the instance ID of the machine that you want to manage.</span></span> <span data-ttu-id="24198-106">U kunt [Azure Resource Explorer](https://resources.azure.com) de exemplaar-ID van een virtuele machine in een schaalset vinden.</span><span class="sxs-lookup"><span data-stu-id="24198-106">You can use [Azure Resource Explorer](https://resources.azure.com) to find the instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="24198-107">U kunt ook Resource Explorer gebruiken om te controleren of de status van de taken die u hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="24198-107">You also use Resource Explorer to verify the status of the tasks that you finish.</span></span>

<span data-ttu-id="24198-108">Zie [Azure PowerShell installeren en configureren](/powershell/azure/overview) voor informatie over het installeren van de nieuwste versie van Azure PowerShell, het selecteren van het abonnement en het aanmelden bij uw account.</span><span class="sxs-lookup"><span data-stu-id="24198-108">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="24198-109">Informatie weergeven over een schaalset</span><span class="sxs-lookup"><span data-stu-id="24198-109">Display information about a scale set</span></span>
<span data-ttu-id="24198-110">U kunt algemene informatie over een schaalset, die ook wordt aangeduid als de instantieweergave ophalen.</span><span class="sxs-lookup"><span data-stu-id="24198-110">You can get general information about a scale set, which is also referred to as the instance view.</span></span> <span data-ttu-id="24198-111">Of u krijgt meer specifieke informatie, zoals informatie over de resources in de schaalset.</span><span class="sxs-lookup"><span data-stu-id="24198-111">Or, you can get more specific information, such as information about the resources in the scale set.</span></span>

<span data-ttu-id="24198-112">Vervang de waarden tussen aanhalingstekens met de naam of de resourcegroep en schaal ingesteld en voer vervolgens de opdracht:</span><span class="sxs-lookup"><span data-stu-id="24198-112">Replace the quoted values with the name or your resource group and scale set and then run the command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="24198-113">Deze retourneert ongeveer het volgende:</span><span class="sxs-lookup"><span data-stu-id="24198-113">It returns something like this:</span></span>

    Id                                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/myvmss1
    Name                                        : myvmss1
    Type                                        : Microsoft.Compute/virtualMachineScaleSets
    Location                                    : centralus
    Sku                                         :
      Name                                      : Standard_A0
      Tier                                      : Standard
      Capacity                                  : 3
    UpgradePolicy                               :
      Mode                                      : Manual
    VirtualMachineProfile                       :
      OsProfile                                 :
        ComputerNamePrefix                      : vmss1
        AdminUsername                           : admin1
        WindowsConfiguration                    :
          ProvisionVMAgent                      : True
          EnableAutomaticUpdates                : True
    StorageProfile                              :
      ImageReference                            :
        Publisher                               : MicrosoftWindowsServer
        Offer                                   : WindowsServer
        Sku                                     : 2012-R2-Datacenter
        Version                                 : latest
      OsDisk                                    :
        Name                                    : vmssosdisk
        Caching                                 : ReadOnly
        CreateOption                            : FromImage
        VhdContainers[0]                        : https://astore.blob.core.windows.net/vmss
        VhdContainers[1]                        : https://gstore.blob.core.windows.net/vmss
        VhdContainers[2]                        : https://mstore.blob.core.windows.net/vmss
        VhdContainers[3]                        : https://sstore.blob.core.windows.net/vmss
        VhdContainers[4]                        : https://ystore.blob.core.windows.net/vmss
    NetworkProfile                              :
      NetworkInterfaceConfigurations[0]         :
        Name                                    : mync1
        Primary                                 : True
        IpConfigurations[0]                     :
          Name                                  : ip1
          Subnet                                :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/virtualNetworks/myvn1/subnets/mysn1
          LoadBalancerBackendAddressPools[0]    :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/backendAddressPools/bepool1
        LoadBalancerInboundNatPools[0]          :
            Id                                  : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Network/loadBalancers/mylb1/inboundNatPools/natpool1
    ExtensionProfile                            :
      Extensions[0]                             :
        Name                                    : Microsoft.Insights.VMDiagnosticsSettings
        Publisher                               : Microsoft.Azure.Diagnostics
        Type                                    : IaaSDiagnostics
        TypeHandlerVersion                      : 1.5
        AutoUpgradeMinorVersion                 : True
        Settings                                : {"xmlCfg":"...","storageAccount":"astore"}
    ProvisioningState                           : Succeeded

<span data-ttu-id="24198-114">De aanhalingstekens waarden vervangt door de naam van de resource-groep en scale set.</span><span class="sxs-lookup"><span data-stu-id="24198-114">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="24198-115">Vervang  *#*  met exemplaar-id van de virtuele machine die u wilt u informatie wilt over en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="24198-115">Replace *#* with the instance identifier of the virtual machine that you want to get information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="24198-116">Het resultaat dat lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="24198-116">It returns something like this example:</span></span>

    Id                            : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/
                                    virtualMachineScaleSets/myvmss1/virtualMachines/0
    Name                          : myvmss1_0
    Type                          : Microsoft.Compute/virtualMachineScaleSets/virtualMachines
    Location                      : centralus
    InstanceId                    : 0
    Sku                           :
      Name                        : Standard_A0
      Tier                        : Standard
    LatestModelApplied            : True
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : 4.0.20160617
      OsDisk                      :
        OsType                    : Windows
        Name                      : vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8
        Vhd                       :
          Uri                     : https://astore.blob.core.windows.net/vmss/vmssosdisk-os-0-e11cad52959b4b76a8d9f26c5190c4f8.vhd
        Caching                   : ReadOnly
        CreateOption              : FromImage
    OsProfile                     :
      ComputerName                : myvmss1-0
      AdminUsername               : admin1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
        EnableAutomaticUpdates    : True
    NetworkProfile                :
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachineScaleSets/
                                    myvmss1/virtualMachines/0/networkInterfaces/mync1
    ProvisioningState             : Succeeded
    Resources[0]                  :
      Id                          : /subscriptions/{sub-id}/resourceGroups/myrg1/providers/Microsoft.Compute/virtualMachines/
                                    myvmss1_0/extensions/Microsoft.Insights.VMDiagnosticsSettings
      Name                        : Microsoft.Insights.VMDiagnosticsSettings
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Azure.Diagnostics
      VirtualMachineExtensionType : IaaSDiagnostics
      TypeHandlerVersion          : 1.5
      AutoUpgradeMinorVersion     : True
      Settings                    : {"xmlCfg":"...","storageAccount":"astore"}
      ProvisioningState           : Succeeded

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="24198-117">Een virtuele machine te starten in een schaalset</span><span class="sxs-lookup"><span data-stu-id="24198-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="24198-118">De aanhalingstekens waarden vervangt door de naam van de resource-groep en scale set.</span><span class="sxs-lookup"><span data-stu-id="24198-118">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="24198-119">Vervang  *#*  met de id van de virtuele machine die u wilt starten en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="24198-119">Replace *#* with the identifier of the virtual machine that you want to start and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="24198-120">In Resource Explorer, ziet u de status van het exemplaar **met**:</span><span class="sxs-lookup"><span data-stu-id="24198-120">In Resource Explorer, we can see that the status of the instance is **running**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T02:10:08.0730839+00:00"
      },
      {
        "code": "PowerState/running",
        "level": "Info",
        "displayStatus": "VM running"
      }
    ]

<span data-ttu-id="24198-121">U kunt alle virtuele machines in de schaal instelt met behulp van de parameter - InstanceId niet starten.</span><span class="sxs-lookup"><span data-stu-id="24198-121">You can start all the virtual machines in the scale set by not using the -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="24198-122">Een virtuele machine in een scale-verzameling stoppen</span><span class="sxs-lookup"><span data-stu-id="24198-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="24198-123">De aanhalingstekens waarden vervangt door de naam van de resource-groep en scale set.</span><span class="sxs-lookup"><span data-stu-id="24198-123">Replace the quoted values with the name of your resource group and scale set.</span></span> <span data-ttu-id="24198-124">Vervang  *#*  met de id van de virtuele machine die u wilt stoppen en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="24198-124">Replace *#* with the identifier of the virtual machine that you want to stop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="24198-125">In Resource Explorer, ziet u de status van het exemplaar **ongedaan**:</span><span class="sxs-lookup"><span data-stu-id="24198-125">In Resource Explorer, we can see that the status of the instance is **deallocated**:</span></span>

    "statuses": [
      {
        "code": "ProvisioningState/succeeded",
        "level": "Info",
        "displayStatus": "Provisioning succeeded",
        "time": "2016-03-15T01:25:17.8792929+00:00"
      },
      {
        "code": "PowerState/deallocated",
        "level": "Info",
        "displayStatus": "VM deallocated"
      }
    ]

<span data-ttu-id="24198-126">Als u wilt stoppen van een virtuele machine en deze niet ongedaan gemaakt, gebruikt u de parameter - StayProvisioned.</span><span class="sxs-lookup"><span data-stu-id="24198-126">To stop a virtual machine and not deallocate it, use the -StayProvisioned parameter.</span></span> <span data-ttu-id="24198-127">U kunt de virtuele machines in de set met behulp van de exemplaar-id - parameter niet stoppen.</span><span class="sxs-lookup"><span data-stu-id="24198-127">You can stop all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="24198-128">Opnieuw opstarten van een virtuele machine in een schaalset</span><span class="sxs-lookup"><span data-stu-id="24198-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="24198-129">De aanhalingstekens waarden vervangt door de naam van de resourcegroep en de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24198-129">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="24198-130">Vervang  *#*  met de id van de virtuele machine die u wilt starten en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="24198-130">Replace *#* with the identifier of the virtual machine that you want to restart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="24198-131">U kunt alle virtuele machines in de set met behulp van de parameter - InstanceId niet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="24198-131">You can restart all the virtual machines in the set by not using the -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="24198-132">Een virtuele machine verwijderen uit een schaalset</span><span class="sxs-lookup"><span data-stu-id="24198-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="24198-133">De aanhalingstekens waarden vervangt door de naam van de resourcegroep en de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24198-133">Replace the quoted values with the name of your resource group and the scale set.</span></span> <span data-ttu-id="24198-134">Vervang  *#*  met de id van de virtuele machine die u wilt verwijderen en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="24198-134">Replace *#* with the identifier of the virtual machine that you want to remove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="24198-135">U kunt de virtuele-machineschaalset in één keer verwijderen met behulp van de exemplaar-id - parameter niet.</span><span class="sxs-lookup"><span data-stu-id="24198-135">You can remove the virtual machine scale set all at once by not using the -InstanceId parameter.</span></span>

## <a name="change-the-capacity-of-a-scale-set"></a><span data-ttu-id="24198-136">De capaciteit van een schaalset wijzigen</span><span class="sxs-lookup"><span data-stu-id="24198-136">Change the capacity of a scale set</span></span>
<span data-ttu-id="24198-137">U kunt toevoegen of verwijderen van virtuele machines met het wijzigen van de capaciteit van de set.</span><span class="sxs-lookup"><span data-stu-id="24198-137">You can add or remove virtual machines by changing the capacity of the set.</span></span> <span data-ttu-id="24198-138">Haal de schaalaanpassingsset die u wilt wijzigen, de capaciteit aan wat u wilt dat het instellen en werk vervolgens de schaal instelt met de nieuwe capaciteit.</span><span class="sxs-lookup"><span data-stu-id="24198-138">Get the scale set that you want to change, set the capacity to what you want it to be, and then update the scale set with the new capacity.</span></span> <span data-ttu-id="24198-139">In deze opdrachten kunt u de tussen aanhalingstekens waarden vervangt door de naam van de resourcegroep en de schaal is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="24198-139">In these commands, replace the quoted values with the name of your resource group and the scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="24198-140">Als u virtuele machines van de schaalaanpassingsset verwijdert, worden de virtuele machines met de hoogste id eerst verwijderd.</span><span class="sxs-lookup"><span data-stu-id="24198-140">If you are removing virtual machines from the scale set, the virtual machines with the highest ids are removed first.</span></span>

