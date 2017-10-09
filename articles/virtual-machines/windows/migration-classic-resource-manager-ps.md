---
title: aaaMigrate tooResource Manager met PowerShell | Microsoft Docs
description: Dit artikel begeleidt u bij Hallo platform ondersteund migratie van IaaS-resources, zoals virtuele machines (VM's), virtuele netwerken (vnet's) en storage-accounts van klassieke tooAzure Resource Manager (ARM) met behulp van Azure PowerShell-opdrachten
services: virtual-machines-windows
documentationcenter: 
author: singhkays
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 2b3dff9b-2e99-4556-acc5-d75ef234af9c
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: kasing
ms.openlocfilehash: b5b2987da292f1c241be71a354b0c2e1a96a07c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-iaas-resources-from-classic-tooazure-resource-manager-by-using-azure-powershell"></a>Migreren van IaaS-resources van klassieke tooAzure Resource Manager met behulp van Azure PowerShell
Deze stappen ziet u hoe toouse Azure PowerShell toomigrate infrastructuur opdrachten als een dienst (IaaS) resources vanuit Hallo classic deployment model toohello Azure Resource Manager-implementatiemodel.

Als u wilt, kunt u ook resources migreren door middel van Hallo [Azure-opdrachtregelinterface (Azure CLI)](../linux/migration-classic-resource-manager-cli.md).

* Zie voor achtergrondinformatie over ondersteunde migratiescenario's [Platform ondersteund migratie van IaaS-resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-overview.md).
* Zie voor gedetailleerde instructies en een overzicht van migratie [technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md).
* [Bekijk de meest voorkomende migratiefouten](migration-classic-resource-manager-errors.md)

<br>
Hier volgt een stroomdiagram tooidentify Hallo volgorde waarin stappen toobe uitgevoerd tijdens een migratie moeten

![Schermafbeelding van de migratiestappen Hallo](media/migration-classic-resource-manager/migration-flow.png)

## <a name="step-1-plan-for-migration"></a>Stap 1: Plannen voor migratie
Hier volgen enkele aanbevolen procedures die wij adviseren kijkt u bij het evalueren van IaaS-Resourcemigratie van klassieke tooResource Manager:

* Lees Hallo [ondersteunde en niet-ondersteunde functies en configuraties](migration-classic-resource-manager-overview.md). Als u virtuele machines die gebruikmaken van niet-ondersteunde configuraties of functies hebt, raden wij wachten op Hallo configuratie of onderdeel ondersteuning toobe aangekondigd. U kunt ook als deze aan uw behoeften voldoet, verwijdert u deze functie of verlaten die configuratie tooenable migratie.
* Als u scripts die uw infrastructuur en toepassingen vandaag implementeert geautomatiseerde, kunt u toocreate instellingen voor een vergelijkbaar met behulp van deze scripts voor de migratie. U kunt ook voorbeeld omgevingen instellen met behulp van hello Azure-portal.

> [!IMPORTANT]
> Toepassingsgateways worden momenteel niet ondersteund voor migratie van klassiek tooResource Manager. Hallo gateway toomigrate een klassiek virtueel netwerk met een toepassingsgateway verwijderen voordat u een netwerk voorbereiden bewerking toomove Hallo uitvoert. Nadat u Hallo migratie hebt voltooid, sluit u Hallo gateway in Azure Resource Manager.
>
>ExpressRoute-gateways die verbinding maken met tooExpressRoute circuits in een ander abonnement kunnen niet automatisch worden gemigreerd. In dergelijke gevallen Hallo ExpressRoute-gateway verwijderen, Migreer het virtuele netwerk Hallo en maak Hallo-gateway. Zie [migreren ExpressRoute-circuits en bijbehorende virtuele netwerken vanuit Hallo klassieke toohello Resource Manager-implementatiemodel](../../expressroute/expressroute-migration-classic-resource-manager.md) voor meer informatie.
>
>

## <a name="step-2-install-hello-latest-version-of-azure-powershell"></a>Stap 2: Installeer de meest recente versie van Azure PowerShell Hallo
Er zijn twee manieren tooinstall Azure PowerShell: [PowerShell Gallery](https://www.powershellgallery.com/profiles/azure-sdk/) of [Web Platform Installer (WebPI)](http://aka.ms/webpi-azps). WebPI ontvangt maandelijkse updates. PowerShell Gallery ontvangt updates doorlopend. In dit artikel is gebaseerd op Azure PowerShell versie 2.1.0.

Zie voor installatie-instructies [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).

<br>

## <a name="step-3-ensure-that-you-are-an-administrator-for-hello-subscription-in-azure-portal"></a>Stap 3: Zorg ervoor dat u een beheerder zijn voor het Hallo-abonnement in Azure-portal
tooperform deze migratie kan u moet worden toegevoegd als medebeheerder voor Hallo-abonnement in Hallo [Azure-portal](https://portal.azure.com).

1. Meld u aan bij Hallo [Azure-portal](https://portal.azure.com).
2. Selecteer op de Hub-menu Hallo **abonnement**. Als u deze niet ziet, selecteert u **meer services**.
3. Vermelding in het juiste abonnement Hallo vinden en vervolgens bekijkt hello **mijn rol** veld. Voor een medebeheerder Hallo-waarde moet _accountbeheerder_.

Als u niet kunt tooadd een CO-beheerder bent, klikt u vervolgens contact op met een servicebeheerder of medebeheerder Hallo abonnement tooget zelf toegevoegd.   

## <a name="step-4-set-your-subscription-and-sign-up-for-migration"></a>Stap 4: Stel uw abonnement en aanmelden voor migratie
Eerst een PowerShell-prompt. Voor de migratie, moet u tooset van uw omgeving voor zowel klassieke en het Resource Manager.

Meld u aan tooyour-account voor Hallo Resource Manager-model.

```powershell
    Login-AzureRmAccount
```

Hallo beschikbare abonnementen ophalen met behulp van de volgende opdracht Hallo:

```powershell
    Get-AzureRMSubscription | Sort Name | Select Name
```

Stel uw Azure-abonnement voor Hallo huidige sessie. In dit voorbeeld sets Hallo standaardnaam van het abonnement te**mijn Azure-abonnement**. De naam van het abonnement voor Hallo-voorbeeld vervangen door uw eigen.

```powershell
    Select-AzureRmSubscription –SubscriptionName "My Azure Subscription"
```

> [!NOTE]
> Registratie is een eenmalige stap, maar u moet dit doen eenmaal voordat u de migratie. Zonder te registreren ziet u Hallo volgende foutbericht weergegeven:
>
> *BadRequest: Abonnement is niet geregistreerd voor migratie.*
>
>

Registreren bij de Hallo migratie resourceprovider met behulp van de volgende opdracht Hallo:

```powershell
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Wacht vijf minuten voor Hallo registratie toofinish. U kunt de status van de Hallo van Hallo goedkeuring controleren met behulp van de volgende opdracht Hallo:

```powershell
    Get-AzureRmResourceProvider -ProviderNamespace Microsoft.ClassicInfrastructureMigrate
```

Zorg ervoor dat RegistrationState `Registered` voordat u doorgaat.

Nu tooyour-account voor het klassieke model Hallo aanmelden.

```powershell
    Add-AzureAccount
```

Hallo beschikbare abonnementen ophalen met behulp van de volgende opdracht Hallo:

```powershell
    Get-AzureSubscription | Sort SubscriptionName | Select SubscriptionName
```

Stel uw Azure-abonnement voor Hallo huidige sessie. In dit voorbeeld wordt een standaardabonnement hello te**mijn Azure-abonnement**. De naam van het abonnement voor Hallo-voorbeeld vervangen door uw eigen.

```powershell
    Select-AzureSubscription –SubscriptionName "My Azure Subscription"
```

<br>

## <a name="step-5-make-sure-you-have-enough-azure-resource-manager-virtual-machine-cores-in-hello-azure-region-of-your-current-deployment-or-vnet"></a>Stap 5: Controleer of er voldoende virtuele Machine van Azure Resource Manager kernen in hello Azure-regio van uw huidige implementatie of VNET
U kunt Hallo volgende PowerShell-opdracht toocheck Hallo Huidig aantal kernen dat u in Azure Resource Manager hebt gebruiken. toolearn meer informatie over quota core, Zie [limieten en hello Azure Resource Manager](../../azure-subscription-service-limits.md#limits-and-the-azure-resource-manager).

In dit voorbeeld controleert op Hallo beschikbaarheid in Hallo **VS-West** regio. Hallo voorbeeld regionaam vervangen door uw eigen.

```powershell
Get-AzureRmVMUsage -Location "West US"
```

## <a name="step-6-run-commands-toomigrate-your-iaas-resources"></a>Stap 6: Uitvoeren opdrachten toomigrate uw IaaS-resources
> [!NOTE]
> Alle Hallo bewerkingen hier beschreven zijn idempotent. Als er een probleem dan een niet-ondersteunde functie of een configuratiefout, raden wij aan dat u opnieuw Hallo proberen voorbereiden, afgebroken of doorgevoerd, bewerking. Hallo platform probeert vervolgens Hallo actie opnieuw.
>
>

## <a name="step-61-option-1---migrate-virtual-machines-in-a-cloud-service-not-in-a-virtual-network"></a>Stap 6.1: Optie 1 - migreren van virtuele machines in een cloudservice (niet in een virtueel netwerk)
Haal de lijst Hallo van cloud-services met behulp van de volgende opdracht Hallo en kies Hallo cloudservice die u wilt toomigrate. Als Hallo virtuele machines in de cloudservice Hallo in een virtueel netwerk zijn of als ze web-of werkrollen hebben, retourneert Hallo opdracht een foutbericht weergegeven.

```powershell
    Get-AzureService | ft Servicename
```

De naam van de Hallo implementatie voor cloudservice Hallo opgehaald. In dit voorbeeld is de naam van Hallo service **mijn Service**. Servicenaam Hallo-voorbeeld vervangen door uw eigen servicenaam.

```powershell
    $serviceName = "My Service"
    $deployment = Get-AzureDeployment -ServiceName $serviceName
    $deploymentName = $deployment.DeploymentName
```

Bereid Hallo virtuele machines in de cloudservice Hallo voor migratie. U hebt twee opties toochoose uit.

* **Optie 1. Migreer het Hallo VMs tooa platform gemaakte virtuele netwerk**

    Eerst valideren als u met behulp van de volgende opdrachten Hallo Hallo-cloudservice kunt migreren:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    $validate.ValidationMessages
    ```

    Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren. Als validatie gelukt is, dan kunt u op toohello **voorbereiden** stap:

    ```powershell
    Move-AzureService -Prepare -ServiceName $serviceName `
        -DeploymentName $deploymentName -CreateNewVirtualNetwork
    ```
* **Optie 2. Migreren van tooan bestaand virtueel netwerk in Hallo Resource Manager-implementatiemodel**

    In dit voorbeeld sets Hallo Resourcegroepnaam te**myResourceGroup**, virtuele-netwerknaam te Hallo**myVirtualNetwork** en subnetnaam te Hallo**mySubNet**. Hallo-namen in Hallo voorbeeld vervangen door Hallo namen van uw eigen resources.

    ```powershell
    $existingVnetRGName = "myResourceGroup"
    $vnetName = "myVirtualNetwork"
    $subnetName = "mySubNet"
    ```

    Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:

    ```powershell
    $validate = Move-AzureService -Validate -ServiceName $serviceName `
        -DeploymentName $deploymentName -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName -VirtualNetworkName $vnetName -SubnetName $subnetName
    $validate.ValidationMessages
    ```

    Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren. Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met Hallo voorbereidingsstap te volgen:

    ```powershell
        Move-AzureService -Prepare -ServiceName $serviceName -DeploymentName $deploymentName `
        -UseExistingVirtualNetwork -VirtualNetworkResourceGroupName $existingVnetRGName `
        -VirtualNetworkName $vnetName -SubnetName $subnetName
    ```

Nadat Hallo Prepare-bewerking is geslaagd met een van de voorgaande opties hello, een query migratiestatus Hallo Hallo virtuele machines. Zorg ervoor dat ze Hallo `Prepared` status.

In dit voorbeeld sets Hallo VM-naam te**myVM**. Voorbeeldnaam Hallo vervangen door de naam van uw eigen VM.

```powershell
    $vmName = "myVM"
    $vm = Get-AzureVM -ServiceName $serviceName -Name $vmName
    $vm.VM.MigrationState
```

Controleer de configuratie voor resources voorbereid met behulp van PowerShell of Azure-portal Hallo HALLO hallo. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:

```powershell
    Move-AzureService -Abort -ServiceName $serviceName -DeploymentName $deploymentName
```

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:

```powershell
    Move-AzureService -Commit -ServiceName $serviceName -DeploymentName $deploymentName
```

## <a name="step-61-option-2---migrate-virtual-machines-in-a-virtual-network"></a>Stap 6.1: Optie 2: migreren van virtuele machines in een virtueel netwerk

toomigrate virtuele machines in een virtueel netwerk die u migreert Hallo virtueel netwerk. Hallo virtuele machines migreren automatisch met het virtuele netwerk Hallo. Pick Hallo virtueel netwerk dat u wilt dat toomigrate.
> [!NOTE]
> [Migreren van één klassieke virtuele machine](migrate-single-classic-to-resource-manager.md) door het maken van een nieuwe Resource Manager-virtuele machine met beheerd schijven met Hallo VHD (besturingssysteem en data)-bestanden van Hallo virtuele machine.
<br>

> [!NOTE]
> Hallo virtuele-netwerknaam kan afwijken van wat wordt weergegeven in Hallo nieuwe Portal. Hallo nieuwe Azure Portal wordt weergegeven naam als Hallo `[vnet-name]` maar Hallo werkelijke virtuele-netwerknaam is van het type `Group [resource-group-name] [vnet-name]`. Voordat u migreert, lookup Hallo werkelijke virtuele-netwerknaam met Hallo opdracht `Get-AzureVnetSite | Select -Property Name` of weergeven in Hallo oude Azure-Portal. 

In dit voorbeeld sets Hallo virtuele-netwerknaam te**myVnet**. Hallo voorbeeld van de virtuele-netwerknaam vervangen door uw eigen.

```powershell
    $vnetName = "myVnet"
```

> [!NOTE]
> Als het virtuele netwerk Hallo bevat of werkrollen of VM's met niet-ondersteunde configuraties, krijgt u een validatiefoutbericht.
>
>

Eerst valideren als u Hallo virtueel netwerk met behulp van de volgende opdracht Hallo kunt migreren:

```powershell
    Move-AzureVirtualNetwork -Validate -VirtualNetworkName $vnetName
```

Hallo voorgaande opdracht geeft alle waarschuwingen en fouten die migratie blokkeren. Als validatie geslaagd is, kunt klikt u vervolgens u doorgaan met Hallo voorbereidingsstap te volgen:

```powershell
    Move-AzureVirtualNetwork -Prepare -VirtualNetworkName $vnetName
```

Controleer de configuratie voor virtuele machines voorbereid met behulp van Azure PowerShell of Azure-portal Hallo HALLO hallo. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:

```powershell
    Move-AzureVirtualNetwork -Abort -VirtualNetworkName $vnetName
```

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:

```powershell
    Move-AzureVirtualNetwork -Commit -VirtualNetworkName $vnetName
```

## <a name="step-62-migrate-a-storage-account"></a>Stap 6.2 migreren, een opslagaccount
Zodra u klaar bent met het migreren van Hallo virtuele machines, wordt u aangeraden dat u migreert Hallo storage-accounts.

Voordat u Hallo storage-account migreert, uitvoeren voorafgaand aan de vereiste controles in:

* **Klassieke virtuele machines waarvan schijven zijn opgeslagen in het opslagaccount Hallo migreren**

    Voorafgaand aan de opdracht retourneert eigenschappen RoleName en DiskName van alle Hallo klassieke VM-schijven in Hallo storage-account. RoleName is Hallo-naam van Hallo virtuele machine toowhich die een schijf is gekoppeld. Als de voorgaande opdracht retourneert schijven Verzeker u ervan dat virtuele machines toowhich deze schijven zijn gekoppeld worden gemigreerd voordat u migreert Hallo storage-account.
    ```powershell
     $storageAccountName = 'yourStorageAccountName'
      Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Select-Object -ExpandProperty AttachedTo -Property `
      DiskName | Format-List -Property RoleName, DiskName

    ```
* **Niet-gekoppelde klassieke VM schijven die zijn opgeslagen in Hallo storage-account verwijderen**

    Zoeken naar niet-gekoppelde schijven in de klassieke VM in Hallo opslag rekening met volgende opdracht:

    ```powershell
        $storageAccountName = 'yourStorageAccountName'
        Get-AzureDisk | where-Object {$_.MediaLink.Host.Contains($storageAccountName)} | Where-Object -Property AttachedTo -EQ $null | Format-List -Property DiskName  

    ```
    Als de bovenstaande opdracht retourneert schijven Verwijder deze schijven met volgende opdracht:

    ```powershell
       Remove-AzureDisk -DiskName 'yourDiskName'
    ```
* **VM-installatiekopieën verwijderen opgeslagen in het opslagaccount Hallo**

    Opdracht vóór retourneert alle Hallo VM-installatiekopieën met besturingssysteemschijf opgeslagen in Hallo storage-account.
     ```powershell
        Get-AzureVmImage | Where-Object { $_.OSDiskConfiguration.MediaLink -ne $null -and $_.OSDiskConfiguration.MediaLink.Host.Contains($storageAccountName)`
                                } | Select-Object -Property ImageName, ImageLabel
     ```
     Voorafgaand aan de opdracht retourneert alle Hallo VM-installatiekopieën met gegevensschijven in Hallo storage-account is opgeslagen.
     ```powershell

        Get-AzureVmImage | Where-Object {$_.DataDiskConfigurations -ne $null `
                                         -and ($_.DataDiskConfigurations | Where-Object {$_.MediaLink -ne $null -and $_.MediaLink.Host.Contains($storageAccountName)}).Count -gt 0 `
                                        } | Select-Object -Property ImageName, ImageLabel
     ```
    Verwijder alle Hallo VM-installatiekopieën geretourneerd door de bovenstaande opdrachten met behulp van de voorgaande opdracht:
    ```powershell
    Remove-AzureVMImage -ImageName 'yourImageName'
    ```

Elk opslagaccount voor migratie met behulp van de volgende opdracht Hallo valideren. In dit voorbeeld Hallo opslagaccountnaam is **myStorageAccount**. Voorbeeldnaam Hallo vervangen door Hallo-naam van uw eigen opslagaccount.

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Validate -StorageAccountName $storageAccountName
```

Volgende stap is tooPrepare Hallo storage-account voor migratie

```powershell
    $storageAccountName = "myStorageAccount"
    Move-AzureStorageAccount -Prepare -StorageAccountName $storageAccountName
```

Controleer de configuratie van Hallo voor Hallo voorbereid storage-account met behulp van Azure PowerShell of hello Azure-portal. Als u niet klaar voor de migratie bent en u toogo back toohello oude status wilt, gebruikt u Hallo volgende opdracht:

```powershell
    Move-AzureStorageAccount -Abort -StorageAccountName $storageAccountName
```

Als Hallo voorbereide configuratie er goed uitziet, kunt u verder gaan en Hallo resources met behulp van de volgende opdracht Hallo doorvoeren:

```powershell
    Move-AzureStorageAccount -Commit -StorageAccountName $storageAccountName
```

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van de migratie van IaaS-resources van klassieke tooAzure Resource Manager-platform ondersteund](migration-classic-resource-manager-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Technische deep dive op platform ondersteund migratie van klassiek tooAzure Resource Manager](migration-classic-resource-manager-deep-dive.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Migratie van IaaS-resources van klassieke tooAzure Resource Manager plannen](migration-classic-resource-manager-plan.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [CLI toomigrate IaaS resources van klassieke tooAzure Resource Manager gebruiken](../linux/migration-classic-resource-manager-cli.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Community-hulpprogramma's voor hulp bij de migratie van IaaS-resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-community-tools.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk de meest voorkomende migratiefouten](migration-classic-resource-manager-errors.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* [Bekijk Hallo veelgestelde meest vragen over migreren IaaS resources van klassieke tooAzure Resource Manager](migration-classic-resource-manager-faq.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
