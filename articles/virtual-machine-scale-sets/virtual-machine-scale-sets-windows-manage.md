---
title: virtuele machines in een virtuele-Machineschaalset aaaManage | Microsoft Docs
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
ms.openlocfilehash: 7d848729c0fc708bd596b61feb528cf4bf4bafd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a><span data-ttu-id="eb882-103">Beheren van virtuele machines in een virtuele-machineschaalset</span><span class="sxs-lookup"><span data-stu-id="eb882-103">Manage virtual machines in a virtual machine scale set</span></span>
<span data-ttu-id="eb882-104">Hallo-taken in dit artikel toomanage virtuele machines in uw virtuele-machineschaalset gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eb882-104">Use hello tasks in this article toomanage virtual machines in your virtual machine scale set.</span></span>

<span data-ttu-id="eb882-105">De meeste Hallo-taken die betrekking hebben op het beheren van een virtuele machine in een schaalset vereisen dat u Hallo exemplaar-ID van Hallo machine weet die u toomanage wilt.</span><span class="sxs-lookup"><span data-stu-id="eb882-105">Most of hello tasks that involve managing a virtual machine in a scale set require that you know hello instance ID of hello machine that you want toomanage.</span></span> <span data-ttu-id="eb882-106">U kunt [Azure Resource Explorer](https://resources.azure.com) toofind Hallo exemplaar-ID van een virtuele machine in een schaalset.</span><span class="sxs-lookup"><span data-stu-id="eb882-106">You can use [Azure Resource Explorer](https://resources.azure.com) toofind hello instance ID of a virtual machine in a scale set.</span></span> <span data-ttu-id="eb882-107">U wordt ook Resource Explorer tooverify Hallo status van Hallo-taken die u hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="eb882-107">You also use Resource Explorer tooverify hello status of hello tasks that you finish.</span></span>

<span data-ttu-id="eb882-108">Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.</span><span class="sxs-lookup"><span data-stu-id="eb882-108">See [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) for information about installing hello latest version of Azure PowerShell, selecting your subscription, and signing in tooyour account.</span></span>

## <a name="display-information-about-a-scale-set"></a><span data-ttu-id="eb882-109">Informatie weergeven over een schaalset</span><span class="sxs-lookup"><span data-stu-id="eb882-109">Display information about a scale set</span></span>
<span data-ttu-id="eb882-110">U kunt algemene informatie over een schaalset, dat ook waarnaar wordt verwezen tooas hello instantieweergave ophalen.</span><span class="sxs-lookup"><span data-stu-id="eb882-110">You can get general information about a scale set, which is also referred tooas hello instance view.</span></span> <span data-ttu-id="eb882-111">Of u meer gedetailleerde informatie, zoals informatie over resources in de schaalset Hallo Hallo krijgt.</span><span class="sxs-lookup"><span data-stu-id="eb882-111">Or, you can get more specific information, such as information about hello resources in hello scale set.</span></span>

<span data-ttu-id="eb882-112">Vervang de waarden met Hallo-naam of de resourcegroep en schaal ingesteld en voer vervolgens de opdracht Hallo aanhalingstekens Hallo:</span><span class="sxs-lookup"><span data-stu-id="eb882-112">Replace hello quoted values with hello name or your resource group and scale set and then run hello command:</span></span>

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

<span data-ttu-id="eb882-113">Deze retourneert ongeveer het volgende:</span><span class="sxs-lookup"><span data-stu-id="eb882-113">It returns something like this:</span></span>

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

<span data-ttu-id="eb882-114">Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen.</span><span class="sxs-lookup"><span data-stu-id="eb882-114">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="eb882-115">Vervang  *#*  met Hallo exemplaar-id van Hallo virtuele machine tooget meer informatie wilt over te klikken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eb882-115">Replace *#* with hello instance identifier of hello virtual machine that you want tooget information about and then run it:</span></span>

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="eb882-116">Het resultaat dat lijkt op het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="eb882-116">It returns something like this example:</span></span>

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="eb882-117">Een virtuele machine te starten in een schaalset</span><span class="sxs-lookup"><span data-stu-id="eb882-117">Start a virtual machine in a scale set</span></span>
<span data-ttu-id="eb882-118">Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen.</span><span class="sxs-lookup"><span data-stu-id="eb882-118">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="eb882-119">Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toostart te klikken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eb882-119">Replace *#* with hello identifier of hello virtual machine that you want toostart and then run it:</span></span>

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="eb882-120">In Resource Explorer, ziet u dat Hallo status van Hallo-exemplaar is **met**:</span><span class="sxs-lookup"><span data-stu-id="eb882-120">In Resource Explorer, we can see that hello status of hello instance is **running**:</span></span>

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

<span data-ttu-id="eb882-121">U kunt alle Hallo virtuele machines in Hallo scale ingesteld met behulp van Hallo - exemplaar-id-parameter niet starten.</span><span class="sxs-lookup"><span data-stu-id="eb882-121">You can start all hello virtual machines in hello scale set by not using hello -InstanceId parameter.</span></span>

## <a name="stop-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="eb882-122">Een virtuele machine in een scale-verzameling stoppen</span><span class="sxs-lookup"><span data-stu-id="eb882-122">Stop a virtual machine in a scale set</span></span>
<span data-ttu-id="eb882-123">Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen.</span><span class="sxs-lookup"><span data-stu-id="eb882-123">Replace hello quoted values with hello name of your resource group and scale set.</span></span> <span data-ttu-id="eb882-124">Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toostop te klikken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eb882-124">Replace *#* with hello identifier of hello virtual machine that you want toostop and then run it:</span></span>

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="eb882-125">In Resource Explorer, ziet u dat Hallo status van Hallo-exemplaar is **ongedaan**:</span><span class="sxs-lookup"><span data-stu-id="eb882-125">In Resource Explorer, we can see that hello status of hello instance is **deallocated**:</span></span>

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

<span data-ttu-id="eb882-126">een virtuele machine toostop niet ongedaan wordt gemaakt, gebruik Hallo StayProvisioned - parameter.</span><span class="sxs-lookup"><span data-stu-id="eb882-126">toostop a virtual machine and not deallocate it, use hello -StayProvisioned parameter.</span></span> <span data-ttu-id="eb882-127">U kunt alle Hallo virtuele machines in Hallo ingesteld met behulp van Hallo - exemplaar-id-parameter niet stoppen.</span><span class="sxs-lookup"><span data-stu-id="eb882-127">You can stop all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="restart-a-virtual-machine-in-a-scale-set"></a><span data-ttu-id="eb882-128">Opnieuw opstarten van een virtuele machine in een schaalset</span><span class="sxs-lookup"><span data-stu-id="eb882-128">Restart a virtual machine in a scale set</span></span>
<span data-ttu-id="eb882-129">Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens vervangen.</span><span class="sxs-lookup"><span data-stu-id="eb882-129">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="eb882-130">Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toorestart te klikken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eb882-130">Replace *#* with hello identifier of hello virtual machine that you want toorestart and then run it:</span></span>

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="eb882-131">U kunt alle Hallo virtuele machines opnieuw opstarten in Hallo ingesteld met behulp van Hallo - exemplaar-id-parameter niet.</span><span class="sxs-lookup"><span data-stu-id="eb882-131">You can restart all hello virtual machines in hello set by not using hello -InstanceId parameter.</span></span>

## <a name="remove-a-virtual-machine-from-a-scale-set"></a><span data-ttu-id="eb882-132">Een virtuele machine verwijderen uit een schaalset</span><span class="sxs-lookup"><span data-stu-id="eb882-132">Remove a virtual machine from a scale set</span></span>
<span data-ttu-id="eb882-133">Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens vervangen.</span><span class="sxs-lookup"><span data-stu-id="eb882-133">Replace hello quoted values with hello name of your resource group and hello scale set.</span></span> <span data-ttu-id="eb882-134">Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt tooremove te klikken en vervolgens uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="eb882-134">Replace *#* with hello identifier of hello virtual machine that you want tooremove and then run it:</span></span>  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

<span data-ttu-id="eb882-135">U kunt Hallo virtuele-machineschaalset in één keer verwijderen door het Hallo - exemplaar-id-parameter niet gebruikt.</span><span class="sxs-lookup"><span data-stu-id="eb882-135">You can remove hello virtual machine scale set all at once by not using hello -InstanceId parameter.</span></span>

## <a name="change-hello-capacity-of-a-scale-set"></a><span data-ttu-id="eb882-136">Hallo-capaciteit van een schaalset wijzigen</span><span class="sxs-lookup"><span data-stu-id="eb882-136">Change hello capacity of a scale set</span></span>
<span data-ttu-id="eb882-137">U kunt toevoegen of verwijderen van virtuele machines met het Hallo-capaciteit van Hallo set wijzigen.</span><span class="sxs-lookup"><span data-stu-id="eb882-137">You can add or remove virtual machines by changing hello capacity of hello set.</span></span> <span data-ttu-id="eb882-138">Hallo-schaalset gewenste toochange, set Hallo capaciteit toowhat u wilt dat deze toobe, en werk vervolgens Hallo scale set met nieuwe capaciteit Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="eb882-138">Get hello scale set that you want toochange, set hello capacity toowhat you want it toobe, and then update hello scale set with hello new capacity.</span></span> <span data-ttu-id="eb882-139">Vervang in deze opdrachten Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens.</span><span class="sxs-lookup"><span data-stu-id="eb882-139">In these commands, replace hello quoted values with hello name of your resource group and hello scale set.</span></span>

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

<span data-ttu-id="eb882-140">Als u virtuele machines uit Hallo scale set verwijdert, worden eerst Hallo virtuele machines met de hoogste Hallo-id's verwijderd.</span><span class="sxs-lookup"><span data-stu-id="eb882-140">If you are removing virtual machines from hello scale set, hello virtual machines with hello highest ids are removed first.</span></span>

