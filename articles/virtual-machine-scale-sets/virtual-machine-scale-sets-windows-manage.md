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
# <a name="manage-virtual-machines-in-a-virtual-machine-scale-set"></a>Beheren van virtuele machines in een virtuele-machineschaalset
Hallo-taken in dit artikel toomanage virtuele machines in uw virtuele-machineschaalset gebruiken.

De meeste Hallo-taken die betrekking hebben op het beheren van een virtuele machine in een schaalset vereisen dat u Hallo exemplaar-ID van Hallo machine weet die u toomanage wilt. U kunt [Azure Resource Explorer](https://resources.azure.com) toofind Hallo exemplaar-ID van een virtuele machine in een schaalset. U wordt ook Resource Explorer tooverify Hallo status van Hallo-taken die u hebt voltooid.

Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) voor meer informatie over Hallo meest recente versie van Azure PowerShell installeren, uw abonnement te selecteren en tooyour account aanmelden.

## <a name="display-information-about-a-scale-set"></a>Informatie weergeven over een schaalset
U kunt algemene informatie over een schaalset, dat ook waarnaar wordt verwezen tooas hello instantieweergave ophalen. Of u meer gedetailleerde informatie, zoals informatie over resources in de schaalset Hallo Hallo krijgt.

Vervang de waarden met Hallo-naam of de resourcegroep en schaal ingesteld en voer vervolgens de opdracht Hallo aanhalingstekens Hallo:

    Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"

Deze retourneert ongeveer het volgende:

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

Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen. Vervang  *#*  met Hallo exemplaar-id van Hallo virtuele machine tooget meer informatie wilt over te klikken en vervolgens uit te voeren:

    Get-AzureRmVmssVM -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

Het resultaat dat lijkt op het volgende voorbeeld:

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

## <a name="start-a-virtual-machine-in-a-scale-set"></a>Een virtuele machine te starten in een schaalset
Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen. Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toostart te klikken en vervolgens uit te voeren:

    Start-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

In Resource Explorer, ziet u dat Hallo status van Hallo-exemplaar is **met**:

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

U kunt alle Hallo virtuele machines in Hallo scale ingesteld met behulp van Hallo - exemplaar-id-parameter niet starten.

## <a name="stop-a-virtual-machine-in-a-scale-set"></a>Een virtuele machine in een scale-verzameling stoppen
Hallo waarden met de naam van uw resource groep en scale set Hallo aanhalingstekens vervangen. Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toostop te klikken en vervolgens uit te voeren:

    Stop-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

In Resource Explorer, ziet u dat Hallo status van Hallo-exemplaar is **ongedaan**:

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

een virtuele machine toostop niet ongedaan wordt gemaakt, gebruik Hallo StayProvisioned - parameter. U kunt alle Hallo virtuele machines in Hallo ingesteld met behulp van Hallo - exemplaar-id-parameter niet stoppen.

## <a name="restart-a-virtual-machine-in-a-scale-set"></a>Opnieuw opstarten van een virtuele machine in een schaalset
Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens vervangen. Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt toorestart te klikken en vervolgens uit te voeren:

    Restart-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name" -InstanceId #

U kunt alle Hallo virtuele machines opnieuw opstarten in Hallo ingesteld met behulp van Hallo - exemplaar-id-parameter niet.

## <a name="remove-a-virtual-machine-from-a-scale-set"></a>Een virtuele machine verwijderen uit een schaalset
Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens vervangen. Vervang  *#*  met Hallo-id van Hallo virtuele machine wilt tooremove te klikken en vervolgens uit te voeren:  

    Remove-AzureRmVmss -ResourceGroupName "resource group name" –VMScaleSetName "scale set name" -InstanceId #

U kunt Hallo virtuele-machineschaalset in één keer verwijderen door het Hallo - exemplaar-id-parameter niet gebruikt.

## <a name="change-hello-capacity-of-a-scale-set"></a>Hallo-capaciteit van een schaalset wijzigen
U kunt toevoegen of verwijderen van virtuele machines met het Hallo-capaciteit van Hallo set wijzigen. Hallo-schaalset gewenste toochange, set Hallo capaciteit toowhat u wilt dat deze toobe, en werk vervolgens Hallo scale set met nieuwe capaciteit Hallo ophalen. Vervang in deze opdrachten Hallo waarden met de naam van de groep en Hallo scale ResourceSet Hallo aanhalingstekens.

    $vmss = Get-AzureRmVmss -ResourceGroupName "resource group name" -VMScaleSetName "scale set name"
    $vmss.sku.capacity = 5
    Update-AzureRmVmss -ResourceGroupName "resource group name" -Name "scale set name" -VirtualMachineScaleSet $vmss 

Als u virtuele machines uit Hallo scale set verwijdert, worden eerst Hallo virtuele machines met de hoogste Hallo-id's verwijderd.

