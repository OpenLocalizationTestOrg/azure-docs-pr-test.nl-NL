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
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a>Een virtuele machine (klassiek) maken met meerdere NIC's met behulp van PowerShell

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

U kunt virtuele machines (VM's) in Azure maken en koppelen van meerdere netwerkinterfaces (NIC's) van netwerk-tooeach van uw virtuele machines. Meerdere NIC's inschakelen scheiding van verkeerstypen tussen NIC's. Bijvoorbeeld verbonden een die NIC met Internet, Hallo communiceren kan terwijl een andere alleen met interne bronnen niet communiceert toohello Internet. Hallo mogelijkheid tooseparate netwerkverkeer via meerdere NIC's is vereist voor veel virtuele netwerkapparaten, zoals toepassingen en optimalisatie van WAN-oplossingen.

> [!IMPORTANT]
> Azure heeft twee verschillende implementatiemodellen voor het maken van en werken met resources: [Resource Manager en het klassieke model](../resource-manager-deployment-model.md). In dit artikel wordt behandeld met het klassieke implementatiemodel Hallo. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe tooperform deze stappen Hallo [Resource Manager-implementatiemodel](virtual-network-deploy-multinic-arm-ps.md).

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

Hallo volgt gebruik van een resourcegroep met de naam *IaaSStory* voor Hallo-webservers en een resourcegroep met de naam *IaaSStory-back-end* voor Hallo DB-servers.

## <a name="prerequisites"></a>Vereisten

Voordat u Hallo DB servers maken kunt, moet u toocreate hello *IaaSStory* resourcegroep met alle Hallo benodigde resources voor dit scenario. toocreate deze resources, volledige Hallo stappen volgen. Een virtueel netwerk maken door de stappen te volgen Hallo in Hallo [een virtueel netwerk maken](virtual-networks-create-vnet-classic-netcfg-ps.md) artikel.

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a>Hallo back-end virtuele machines maken
Hallo die back-end-VM's afhankelijk zijn van Hallo maken van Hallo resources te volgen:

* **Subnet backend**. Hallo databaseservers zal deel uitmaken van een apart subnet toosegregate verkeer. Hallo onderstaande script verwacht in dit subnet tooexist in een vnet met de naam *WTestVnet*.
* **Storage-account voor gegevensschijven**. Voor betere prestaties Hallo gegevensschijven op Hallo databaseservers Solid-State station (SSD)-technologie, waarvoor een premium storage-account gebruikt. Zorg ervoor dat hello Azure-locatie implementeren van toosupport premium-opslag.
* **Beschikbaarheidsset**. Alle databaseservers tooa één beschikbaarheidsset worden toegevoegd, tooensure ten minste één Hallo VM's actief is tijdens het onderhoud.

### <a name="step-1---start-your-script"></a>Stap 1: uw script starten
U kunt downloaden Hallo volledige PowerShell-script gebruikt [hier](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1). Hallo stappen hieronder toochange Hallo script toowork in uw omgeving.

1. Hallo-waarden van Hallo variabelen hieronder op basis van uw bestaande resourcegroep geïmplementeerd boven in wijzigen [vereisten](#Prerequisites).

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. Hallo waarden wijzigen van Hallo variabelen hieronder op basis van waarden Hallo gewenste toouse voor uw back-end-implementatie.

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

### <a name="step-2---create-necessary-resources-for-your-vms"></a>Stap 2: de benodigde resources voor uw virtuele machines maken
U moet een nieuwe cloudservice en een opslag-voor gegevensschijven Hallo voor alle virtuele machines account toocreate. U moet ook toospecify een afbeelding en een lokale administrator-account voor Hallo virtuele machines. toocreate voltooien van deze resources Hallo volgende stappen:

1. Maak een nieuwe cloudservice.

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. Maak een nieuwe premium storage-account.

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. Hallo set storage-account die eerder is gemaakt als Hallo huidige opslagaccount voor uw abonnement.

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. Selecteer een afbeelding voor Hallo VM.

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. Hallo lokale administrator-accountreferenties instellen.

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a>Stap 3: virtuele machines maken
U moet een lus toocreate toouse zoals veel VM's als u wilt gebruiken en maken Hallo nodig NIC's en virtuele machines in hello for-lus. toocreate hello NIC's en virtuele machines, uitvoeren Hallo stappen te volgen.

1. Start een `for` lus toorepeat Hallo opdrachten toocreate een virtuele machine en twee NIC's vaak als nodig, op basis van de waarde van Hallo Hallo `$numberOfVMs` variabele.

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. Maak een `VMConfig` object Hallo-installatiekopie, grootte en beschikbaarheidsset voor Hallo VM opgeven.

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. Hallo VM inrichten als een virtuele machine van Windows.

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. Hallo standaard NIC instellen en deze een statisch IP-adres toewijzen.

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. Een tweede NIC voor elke virtuele machine toevoegen.

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. Toodata schijven maken voor elke virtuele machine.

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

7. Elke virtuele machine en end Hallo lus maken.

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a>Stap 4: Hallo-script uitvoeren
Nu dat u hebt gedownload en gewijzigd Hallo script op basis van uw behoeften runt hij toocreate Hallo-database voor back-end virtuele machines met meerdere NIC's een script.

1. Sla uw script en voer dit uit Hallo **PowerShell** opdrachtprompt of **PowerShell ISE**. U ziet Hallo initiële uitvoer, zoals hieronder wordt weergegeven.

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. Hallo-informatie die nodig is in Hallo referenties gevraagd en klik op invullen **OK**. onderstaande Hallo-uitvoer geretourneerd.

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
