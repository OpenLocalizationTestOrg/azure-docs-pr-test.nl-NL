---
title: aaaCreate een SQL Server-Machine in Azure PowerShell (Resource Manager) | Microsoft Docs
description: "Bevat de stappen en PowerShell-scripts voor het maken van een virtuele machine in Azure met SQL Server-installatiekopieën voor virtuele machine-galerie."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a>Inrichten van een SQL Server-virtuele machine met Azure PowerShell (Resource Manager)
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a>Overzicht
Deze zelfstudie laat zien hoe een enkele virtuele machine van Azure met toocreate Hallo **Azure Resource Manager** implementatiemodel met Azure PowerShell-cmdlets. We gaan een enkele virtuele machine met een enkele schijf van een installatiekopie in Hallo SQL-galerie maken in deze zelfstudie. Nieuwe providers voor Hallo-opslag-, netwerk- en rekenresources die wordt gebruikt door Hallo virtuele machine u kunt maken. Als u bestaande providers voor een van deze resources hebt, kunt u deze providers in plaats daarvan.

Als u de klassieke versie van dit onderwerp moet hello, Zie [een SQL Server-machine met behulp van Azure PowerShell klassieke inrichten](../classic/ps-sql-create.md).

## <a name="prerequisites"></a>Vereisten
Voor deze zelfstudie hebt u het volgende nodig:

* Een Azure-account en abonnement voordat u begint. Als u niet hebt, zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/).
* [Azure PowerShell)](/powershell/azure/overview), minimale versie van 1.4.0 of hoger (deze zelfstudie geschreven met behulp van versie 1.5.0).
  * tooretrieve uw versie, het type **Azure Get-Module - ListAvailable**.

## <a name="configure-your-subscription"></a>Configureer uw abonnement
Open Windows PowerShell en toegang tooyour Azure-account maken door het uitvoeren van de volgende cmdlet Hallo. U krijgt een teken in het scherm tooenter uw referenties. Gebruik dezelfde Hallo e-mailadres en wachtwoord toosign in toohello Azure-portal te gebruiken.

    Add-AzureRmAccount

Na het aanmelden is ziet u enkele gegevens op het scherm met Hallo abonnements-id waarmee u zich hebt aangemeld in. Dit is Hallo abonnement waarin Hallo bronnen voor deze zelfstudie worden gemaakt tenzij u een ander abonnement tooa wijzigt. Als u meerdere SubscriptionIds hebt, Voer Hallo cmdlet tooreturn na een lijst met alle uw SubscriptionIds:

    Get-AzureRmSubscription

toochange tooanother SubscriptionID, uitvoeren van de volgende cmdlet uit met de gewenste SubscriptionId Hallo.

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a>Definieer de installatiekopie van variabelen
toosimplify bruikbaarheid van en kennis van het script uit deze zelfstudie Hallo voltooid, wordt begin met het definiëren van een aantal variabelen. Het wijzigen van de parameterwaarden Hallo zoals u dat wilt, maar pas op voor de naamgeving beperkingen gerelateerde tooname lengten en speciale tekens bij het wijzigen van Hallo waarden.

### <a name="location-and-resource-group"></a>Locatie en resourcegroep
Gebruik twee variabelen toodefine Hallo gegevens regio en Hallo resourcegroep waarin u Hallo andere bronnen voor Hallo virtuele machine maakt.

Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlets tooinitialize te volgen.

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a>Eigenschappen van opslag
Gebruik hello variabelen toodefine Hallo-account en Hallo opslagtype van opslag toobe gebruikt door Hallo virtuele machine te volgen.

Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen. Houd er rekening mee dat in dit voorbeeld we gebruiken [Premium-opslag](../../../storage/common/storage-premium-storage.md), wat wordt aanbevolen voor productieworkloads. Zie voor meer informatie over deze richtlijnen en andere aanbevelingen [best practices prestaties for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a>Eigenschappen van het netwerk
Hallo na variabelen toodefine Hallo netwerkinterface, Hallo TCP/IP-toewijzingsmethode, Hallo virtuele-netwerknaam, Hallo virtuele subnet-naam, Hallo bereik van IP-adressen voor het virtuele netwerk hello, Hallo bereik van IP-adressen voor het Hallo-subnet en hello gebruiken openbare domein naam label toobe gebruikt door Hallo-netwerk in Hallo virtuele machine.

Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a>Eigenschappen van virtuele machine
Gebruik hello variabelen toodefine Hallo virtuele-machinenaam, Hallo computernaam, de grootte van de virtuele machine Hallo en Hallo besturingssysteem schijfnaam voor Hallo virtuele machine te volgen.

Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a>Eigenschappen van de installatiekopie
Gebruik hello variabelen toodefine Hallo installatiekopie toouse voor Hallo virtuele machine te volgen. In dit voorbeeld wordt Hallo SQL Server 2016 Enterprise afbeelding gebruikt.

Desgewenst wijzigen en vervolgens deze variabelen uitgevoerd Hallo cmdlet tooinitialize te volgen.

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

Houd er rekening mee dat u een volledige lijst met aanbiedingen van SQL Server-installatiekopie met de opdracht Get-AzureRmVMImageOffer Hallo kunt krijgen:

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

En u Hallo SKU's die beschikbaar zijn voor een aanbieding met de opdracht Get-AzureRmVMImageSku Hallo kunt zien. Hallo volgende opdracht toont alle SKU's beschikbaar voor Hallo **SQL2014SP1 WS2012R2** bieden.

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a>Een resourcegroep maken
Met Hallo Resource Manager-implementatiemodel is het eerste Hallo-object dat u maakt Hallo resourcegroep. We gebruiken Hallo [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate een Azure-resourcegroep en de bijbehorende bronnen met Hallo resource groepsnaam en de locatie die is gedefinieerd door het Hallo-variabelen die u eerder is geïnitialiseerd.

Hallo cmdlet toocreate na uw nieuwe resourcegroep uitvoeren.

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a>Een opslagaccount maken
Hallo virtuele machine vereist storage-resources voor de besturingssysteemschijf Hallo en Hallo SQL Server-gegevens en logboekbestanden. Voor eenvoud, u kunt één schijf maken voor beide. U kunt extra schijven met behulp van Hallo bijvoegen [toevoegen Azure-schijf](/powershell/module/azure/add-azuredisk) cmdlet in volgorde tooplace uw SQL Server-gegevens en logboekbestanden op de speciale schijven. We gebruiken Hallo [nieuw AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate een standard-opslag-account in uw nieuwe resourcegroep en met Hallo opslagaccountnaam opslag Sku-naam en locatie die is gedefinieerd met behulp van Hallo variabelen die u hebt eerder is geïnitialiseerd.

Hallo cmdlet toocreate na uw nieuwe opslagaccount uitvoeren.

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a>Maken van netwerkbronnen
Hallo virtuele machine vereist een aantal netwerkbronnen voor verbinding met het netwerk.

* Elke virtuele machine vereist een virtueel netwerk.
* Een virtueel netwerk moet ten minste één subnet dat is gedefinieerd.
* Een netwerkinterface moet worden gedefinieerd met een openbare of een particulier IP-adres.

### <a name="create-a-virtual-network-subnet-configuration"></a>Een virtueel netwerk subnetconfiguratie maken
Er wordt gestart door het maken van de subnetconfiguratie van een voor het virtuele netwerk. In deze zelfstudie maken we een standaard-subnet met Hallo [nieuw AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet. We gaan onze subnetconfiguratie virtueel netwerk maken met de Hallo naam en adres subnetvoorvoegsel gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.

> [!NOTE]
> U kunt aanvullende eigenschappen van Hallo subnetconfiguratie voor virtueel netwerk met behulp van deze cmdlet definiëren, maar dat is buiten bereik Hallo van deze zelfstudie.
>
>

Hallo cmdlet toocreate na de configuratie van uw virtuele subnet uitvoeren.

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a>Een virtueel netwerk maken
Vervolgens maken we onze virtueel netwerk met behulp van Hallo [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet. We maakt onze virtueel netwerk in uw nieuwe resourcegroep met Hallo-naam, locatie en adresvoorvoegsel gedefinieerd met Hallo variabelen die u eerder is geïnitialiseerd, en Hallo subnetten configureren die u hebt gedefinieerd in de vorige stap Hallo.

Hallo cmdlet toocreate na het virtuele netwerk uitvoeren.

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a>Hallo openbare IP-adres maken
Nu dat we onze virtueel netwerk is gedefinieerd hebben, moeten we tooconfigure een IP-adres voor de connectiviteit toohello virtuele machine. We gaan een openbaar IP-adres met behulp van dynamische IP-adressen voor toosupport verbinding met Internet maken voor deze zelfstudie. We gebruiken Hallo [nieuw AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate Hallo openbaar IP-adres in Hallo resource gemaakte groep prevously en met het Hallo-naam, locatie, toewijzingsmethode en DNS-domeinnaamlabel gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.

> [!NOTE]
> U kunt aanvullende eigenschappen Hallo openbare IP-adres met behulp van deze cmdlet definiëren, maar dat is buiten bereik van deze zelfstudie initiële Hallo. U kunt ook een persoonlijk adres of een adres maken met een statisch adres, maar die ook is buiten bereik Hallo van deze zelfstudie.
>
>

Hallo cmdlet toocreate na uw openbare IP-adres uitvoeren.

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a>Hallo-netwerkinterface maken
Er zijn nu gereed toocreate Hallo netwerkinterface die de virtuele machine wordt gebruikt. We gebruiken Hallo [nieuw AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate onze netwerkinterface in resourcegroep Hallo eerder hebt gemaakt en met Hallo-naam, locatie, subnet en openbaar IP-adres is eerder gedefinieerd.

Hallo cmdlet toocreate na de netwerkinterface uitvoeren.

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a>Een VM-object configureren
Nu dat we hebben een opslag- en netwerkbronnen die zijn gedefinieerd, zijn we klaar toodefine rekenresources voor Hallo virtuele machine. In deze zelfstudie wordt we Geef de grootte van de virtuele machine Hallo en verschillende eigenschappen van het besturingssysteem, geef Hallo netwerkinterface die we eerder hebben gemaakt, blob-opslag te definiëren en geef vervolgens de besturingssysteemschijf Hallo.

### <a name="create-hello-vm-object"></a>Hallo VM-object maken
Er wordt gestart door te geven van de grootte van de virtuele machine Hallo. We geven een DS13 voor deze zelfstudie. We gebruiken Hallo [nieuw AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate een object configureerbare virtuele machine met de naam van de Hallo en grootte die is gedefinieerd met behulp van Hallo variabelen die u eerder is geïnitialiseerd.

Hallo na cmdlet toocreate Hallo virtuele machine-object worden uitgevoerd.

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a>Maak een object toohold Hallo referentienaam en het wachtwoord voor de lokale beheerdersreferenties Hallo
Voordat we Hallo besturingssysteem eigenschappen voor Hallo virtuele machine instellen kunt, moet toosupply Hallo referenties voor de lokale beheerdersaccount Hallo als een beveiligde tekenreeks. tooaccomplish, gebruiken we Hallo [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

Hallo volgende cmdlet uitvoeren en typ in Hallo Windows PowerShell-referentie venster Hallo naam en het wachtwoord toouse voor Hallo lokale beheerdersaccount in Hallo Windows virtuele machine.

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a>Hallo besturingssysteem eigenschappen instellen voor Hallo virtuele machine
We kunnen nu de eigenschappen van het besturingssysteem gereed tooset Hallo van virtuele machine. Gebruiken we Hallo [Set AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset type besturingssysteem als Windows hello vereisen Hallo [agent van de virtuele machine](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe geïnstalleerd, geef die Hallo cmdlet schakelt automatisch bijwerken en naam van de virtuele machine Hallo Hallo computernaam en Hallo referentie Hallo variabelen die u eerder is geïnitialiseerd met instellen.

Hallo volgende cmdlet tooset Hallo besturingssysteem eigenschappen voor uw virtuele machine worden uitgevoerd.

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a>Hallo network interface toohello virtuele machine toevoegen
Vervolgens gaat toevoegen we Hallo netwerkinterface dat we eerder toohello virtuele machine gemaakt. We gebruiken Hallo [toevoegen AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd Hallo netwerkinterface Hallo network interface-variabele die u eerder hebt gedefinieerd.

Hallo volgende cmdlet tooset Hallo netwerkinterface voor uw virtuele machine worden uitgevoerd.

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a>Hallo blob-opslaglocatie voor Hallo schijf toobe gebruikt door Hallo virtuele machine instellen
Vervolgens wordt er stelt Hallo blob-opslaglocatie voor Hallo schijf toobe gebruikt door Hallo virtuele machine met behulp van Hallo variabelen die u eerder hebt gedefinieerd.

Hallo na locatie voor de cmdlet tooset Hallo blob-opslag uitvoeren.

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a>Hallo-besturingssysteem schijfeigenschappen instellen voor Hallo virtuele machine
Vervolgens wordt we ingesteld Hallo besturingssysteem schijfeigenschappen voor Hallo virtuele machine. We hello gebruiken [Set AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify die Hallo besturingssysteem voor Hallo virtuele machine, zijn afkomstig van een afbeelding, tooset tooread alleen opslaan in cache (omdat SQL Server wordt geïnstalleerd op Hallo dezelfde schijf) en definiëren naam van de virtuele machine Hallo en Hallo besturingssysteemschijf gedefinieerd met behulp van Hallo variabelen die we eerder hebt gedefinieerd.

Hallo volgende cmdlet tooset Hallo besturingssysteem schijfeigenschappen voor uw virtuele machine worden uitgevoerd.

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a>Hallo platforminstallatiekopie voor Hallo virtuele machine opgeven
Onze laatste stap in de configuratie is toospecify hello platforminstallatiekopie voor de virtuele machine. In deze zelfstudie gebruiken we de meest recente SQL Server 2016 CTP installatiekopie Hallo. We gebruiken Hallo [Set AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse deze installatiekopie zoals gedefinieerd door het Hallo-variabelen die u eerder hebt gedefinieerd.

Hallo volgende cmdlet toospecify hello platforminstallatiekopie voor uw virtuele machine worden uitgevoerd.

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a>Hallo SQL VM maken
Nu u Hallo configuratiestappen hebt voltooid, bent u klaar toocreate Hallo virtuele machine. We gebruiken Hallo [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate Hallo virtuele machine met behulp van Hallo variabelen die we hebt gedefinieerd.

Hallo cmdlet toocreate na uw virtuele machine uitvoeren.

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

Hallo virtuele machine wordt gemaakt. U ziet dat er een standaard opslagaccount voor diagnostische gegevens over opstarten is gemaakt omdat Hallo opslagaccount voor schijf Hallo virtuele machine opgegeven is een premium storage-account.

U kunt nu deze machine weergeven in Azure Portal-toosee hello [het openbare IP-adres en de volledig gekwalificeerde domeinnaam](virtual-machines-windows-portal-sql-server-provision.md).

## <a name="example-script"></a>Voorbeeldscript
Hallo volgende script bevat Hallo voltooid PowerShell-script voor deze zelfstudie. Wordt ervan uitgegaan dat u hebt al setup hello Azure-abonnement toouse Hello **Add-AzureRmAccount** en **Select-AzureRmSubscription** opdrachten.

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a>Volgende stappen
Nadat het Hallo virtuele machine is gemaakt, bent u klaar tooconnect toohello virtuele machine met connectiviteit voor RDP en setup opnieuw uit. Zie voor meer informatie [verbinding maken met virtuele Machine van SQL Server op Azure (Resource Manager) tooa](virtual-machines-windows-sql-connect.md).

