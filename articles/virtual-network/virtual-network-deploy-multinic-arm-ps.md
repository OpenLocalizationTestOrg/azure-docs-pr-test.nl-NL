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
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a>Een virtuele machine maken met meerdere NIC's met behulp van PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-deploy-multinic-arm-ps.md)
> * [Azure CLI](virtual-network-deploy-multinic-arm-cli.md)
> * [Sjabloon](virtual-network-deploy-multinic-arm-template.md)
> * [PowerShell (klassiek)](virtual-network-deploy-multinic-classic-ps.md)
> * [Azure CLI (klassiek)](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md).  In dit artikel wordt beschreven hoe u Hallo Resource Manager-implementatiemodel, die Microsoft voor de meeste nieuwe implementaties in plaats van Hallo aanbeveelt [klassieke implementatiemodel](virtual-network-deploy-multinic-classic-ps.md).
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.

## <a name="prerequisites"></a>Vereisten
Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario. toocreate voltooien van deze resources Hallo volgende stappen:

1. Navigeer te[Hallo sjabloonpagina](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Hallo sjabloon pagina toohello rechts van **bovenliggende resourcegroep**, klikt u op **tooAzure implementeren**.
3. Indien nodig, Hallo parameterwaarden te wijzigen en volg de stappen Hallo in hello Azure preview portal toodeploy Hallo-resourcegroep.

> [!IMPORTANT]
> Zorg ervoor dat de namen van opslagaccounts uniek zijn. Er kan geen dubbele opslagaccountnamen in Azure.
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Hallo back-end virtuele machines maken
Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:

* **Storage-account voor gegevensschijven**. Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt. Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.
* **NIC's**. Elke virtuele machine heeft twee NIC's, één voor toegang tot de database, en één voor beheer.
* **Beschikbaarheidsset**. Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.  

### <a name="step-1---start-your-script"></a>Stap 1: uw script starten
U kunt downloaden Hallo volledige PowerShell-script gebruikt [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1). Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.

1. Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.

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
3. Hallo bestaande resources die nodig zijn voor uw implementatie worden opgehaald.

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Stap 2: de benodigde resources voor uw virtuele machines maken
Moet u een nieuwe resourcegroep, een opslagaccount voor gegevensschijven hello, toocreate en een beschikbaarheidsset voor alle virtuele machines. U standaardquery ook nodig Hallo lokale administrator-accountreferenties voor elke virtuele machine. toocreate uitvoeren van deze resources Hallo volgende stappen.

1. Maak een nieuwe resourcegroep.

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. Maak een nieuwe premium storage-account in Hallo resourcegroep die eerder is gemaakt.

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. Maak een nieuwe beschikbaarheidsset.

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. Lokale beheerder Hallo account referenties toobe gebruikt voor elke VM ophalen.

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a>Stap 3: Hallo NIC's en back-end virtuele machines maken
U moet een lus toocreate toouse zoals veel VM's als u wilt gebruiken en maken Hallo nodig NIC's en virtuele machines in hello for-lus. toocreate hello NIC's en virtuele machines, uitvoeren Hallo stappen te volgen.

1. Start een `for` lus toorepeat Hallo opdrachten toocreate een virtuele machine en twee NIC's vaak als nodig, op basis van de waarde van Hallo Hallo `$numberOfVMs` variabele.
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Hallo die NIC voor toegang tot de database gebruikt maken.

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. Hallo die NIC voor externe toegang gebruikt maken. U ziet hoe deze NIC een tooit NSG die is gekoppeld.

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. Maak `vmConfig` object.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. Maak twee gegevensschijven per VM. U ziet dat Hallo gegevensschijven in Hallo premium storage-account eerder hebt gemaakt.

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

6. Hallo-besturingssysteem en afbeelding toobe gebruikt voor Hallo VM configureren.

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. Hallo twee NIC's bovenstaande toohello toevoegen `vmConfig` object.

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. Hallo OS-schijf maken en Hallo VM maken. Kennisgeving Hallo `}` eindigt Hallo `for` lus.

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a>Stap 4: Hallo-script uitvoeren
Nu dat u hebt gedownload en gewijzigd Hallo script op basis van uw behoeften runt hij toocreate Hallo-database voor back-end virtuele machines met meerdere NIC's een script.

1. Sla uw script en voer dit uit Hallo **PowerShell** opdrachtprompt of **PowerShell ISE**. Ziet u Hallo initiële uitvoer, als volgt:

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. Na een paar minuten invullen Hallo referenties gevraagd en klik op **OK**. Hallo onderstaande uitvoer vertegenwoordigt één VM. Kennisgeving Hallo hele proces duurt 8 minuten toocomplete.

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
