---
title: aaaCreate een Windows-VM met PowerShell | Microsoft Docs
description: Windows virtuele machines met behulp van Azure PowerShell en het klassieke implementatiemodel Hallo maken.
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>Een Windows-machine maken met PowerShell en Hallo klassieke implementatiemodel
> [!div class="op_single_selector"]
> * [Azure portal - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure heeft twee verschillende implementatiemodellen voor het maken en werken met resources: [Resource Manager en Classic](../../../resource-manager-deployment-model.md). In dit artikel bevat informatie over met behulp van Hallo klassieke implementatiemodel. Microsoft raadt aan dat de meeste nieuwe implementaties het Resource Manager-model hello gebruiken. Meer informatie over hoe te[u deze stappen uitvoert met behulp van de Resource Manager-model Hallo](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

Deze stappen ziet u hoe toocustomize een set van Azure PowerShell-opdrachten die maken en vooraf configureren van een op basis van Windows Azure virtuele machine met behulp van een benadering bouwsteen. U kunt dit proces tooquickly een opdrachtset voor een nieuwe Windows gebaseerde virtuele machine maken en uitbreiden van een bestaande implementatie of toocreate meerdere opdracht stelt u die snel bouwen van een aangepaste ontwikkelen en testen of de IT pro-omgeving.

Deze stappen volgt een benadering invullen-in-the-lege waarden voor het maken van Azure PowerShell-opdrachtsets. Deze methode kan nuttig zijn als u nieuwe tooPowerShell of u alleen tooknow welke toospecify waarden voor geslaagde configuratie wilt. Geavanceerde PowerShell-gebruikers kunnen ondernemen Hallo opdrachten en vervangen door hun eigen waarden voor Hallo variabelen (Hallo regels beginnen met '$').

Als u dit nog niet hebt gedaan, gebruikt u de instructies Hallo in [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell op de lokale computer. Vervolgens opent u een Windows PowerShell-opdrachtprompt.

## <a name="step-1-add-your-account"></a>Stap 1: Uw account toevoegen
1. Typ achter de PowerShell-prompt Hallo **Add-AzureAccount** en klik op **Enter**. 
2. Typ Hallo e-mailadres gekoppeld aan uw Azure-abonnement en klik op **doorgaan**. 
3. Typ in het Hallo-wachtwoord voor je account. 
4. Klik op **aanmelden**.

## <a name="step-2-set-your-subscription-and-storage-account"></a>Stap 2: Uw abonnement en storage-account instellen
Uw Azure-abonnement en storage-account instellen door deze opdrachten in Windows PowerShell-opdrachtprompt Hallo. Alles binnen de aanhalingstekens hello, inclusief Hallo < en > tekens, met de juiste namen Hallo vervangen.

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

Kunt u de naam van de juiste abonnement Hallo krijgen via Hallo SubscriptionName-eigenschap van Hallo Hallo **Get-AzureSubscription** opdracht. Kunt u Hallo juist opslagaccountnaam krijgen via de eigenschap Label van de uitvoer Hallo HALLO hallo **Get-AzureStorageAccount** opdracht, na het uitvoeren van Hallo **Select-AzureSubscription** opdracht.

## <a name="step-3-determine-hello-imagefamily"></a>Stap 3: Hallo ImageFamily bepalen
Vervolgens moet u toodetermine hello ImageFamily of labelwaarde voor Hallo specifieke installatiekopie bijbehorende toohello gewenste toocreate virtuele Azure-machine. U kunt Hallo lijst met beschikbare ImageFamily waarden met deze opdracht ophalen.

    Get-AzureVMImage | select ImageFamily -Unique

Hier volgen enkele voorbeelden van waarden ImageFamily voor Windows-computers:

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise in WindowsServer 2012

Als u Hallo-installatiekopie die u zoekt vinden, opent u een nieuw exemplaar van Hallo teksteditor van uw keuze of Hallo PowerShell Integrated Scripting Environment (ISE). Hallo volgende kopiëren naar nieuw tekstbestand Hallo of Hallo PowerShell ISE, Hallo ImageFamily waarde te vervangen.

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

In sommige gevallen is Hallo installatiekopie met de naam in Hallo labeleigenschap in plaats van Hallo ImageFamily waarde. Als u Hallo-installatiekopie die u zoekt met Hallo ImageFamily eigenschap niet vinden, lijst Hallo afbeeldingen door de eigenschap Label met deze opdracht.

    Get-AzureVMImage | select Label -Unique

Als u de juiste installatiekopie Hallo met deze opdracht vinden, opent u een nieuw exemplaar van Hallo teksteditor van uw keuze of Hallo PowerShell ISE. Hallo volgende naar nieuw tekstbestand Hallo of PowerShell ISE, vervangen door de labelwaarde Hallo Hallo kopiëren.

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>Stap 4: De opdrachtset bouwen
Bouw Hallo rest van de opdracht die is ingesteld door de juiste reeks blokken hieronder Hallo kopiëren naar uw nieuw tekstbestand of Hallo ISE invullen van de waarden van variabelen Hallo en Hallo < en > tekens verwijderen. Zie Hallo twee [voorbeelden](#examples) aan Hallo einde van dit artikel voor een idee van Hallo eindresultaat.

Start de opdracht die is ingesteld door een van deze twee opdracht blokken (vereist) te kiezen.

Optie 1: Geef de naam van een virtuele machine en een grootte.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

Optie 2: Geef een naam, de grootte en de naam van de beschikbaarheidsset.

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

Zie voor Hallo InstanceSize waarden voor D, DS of G-serie virtuele machines [virtuele Machine en Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).

> [!NOTE]
> Als u een Enterprise Agreement met Software Assurance hebt en tootake profiteren van Windows Server Hallo van plan bent [hybride gebruik voordeel](https://azure.microsoft.com/pricing/hybrid-use-benefit/), voeg de **- LicenseType** parameter toohello  **Nieuwe AzureVMConfig** cmdlet Hallo-waarde doorgegeven **Windows_Server** voor typische Hallo gebruiksvoorbeeld.  Zorg ervoor dat u gebruikmaakt van een installatiekopie die u hebt geüpload; u kunt een standaardinstallatiekopie van Hallo galerie niet gebruiken met Hallo hybride gebruiken voordeel.
> 
> 

Geef desgewenst voor een zelfstandige Windows-computer Hallo lokale administrator-account en wachtwoord.

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

Kies een sterk wachtwoord. toocheck de sterkte Zie [wachtwoord Checker: met behulp van sterke wachtwoorden](https://www.microsoft.com/security/pc-security/password-checker.aspx).

Eventueel tooadd Hallo Windows computer tooan bestaande Active Directory-domein Hallo lokale administrator-account en wachtwoord, hello domein, en Hallo naam en het wachtwoord van een domeinaccount opgeven.

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Zie voor aanvullende vooraf configuratieopties voor virtuele machines op basis van Windows hello syntaxis voor Hallo **Windows** en **WindowsDomain** parametersets [ Voeg AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).

Desgewenst toewijzen Hallo virtuele machine, een specifiek IP-adres, een statische DIP genoemd.

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

U kunt controleren of een specifiek IP-adres beschikbaar met:

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

Desgewenst toewijzen Hallo virtuele machine tooa specifieke subnet in een Azure-netwerk.

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

Voegt u desgewenst een virtuele machine van één schijf toohello.

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Voor een Active Directory-domeincontroller te $hcaching ingesteld 'None'.

Voegt u desgewenst Hallo virtuele machine tooan bestaande taakverdeling set voor het externe verkeer.

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

Ten slotte, kies een van deze blokken vereist opdracht voor het maken van Hallo virtuele machine.

Optie 1: Maak Hallo virtuele machine in een bestaande cloudservice.

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

korte naam van de cloudservice Hallo Hallo is Hallo-naam die wordt weergegeven in de lijst van de Hallo van Cloud Services in hello Azure-portal of in Hallo lijst met resourcegroepen in hello Azure-portal.

Optie 2: Maak Hallo virtuele machine in een bestaande cloudservice en het virtuele netwerk.

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>Stap 5: Voer de opdrachtset
Bekijk hello Azure PowerShell-opdrachtset die u gebouwd in een teksteditor of Hallo PowerShell ISE die bestaan uit meerdere blokken van opdrachten uit stap 4. Zorg ervoor dat u alle variabelen van Hallo nodig hebt opgegeven en of ze de juiste waarden Hallo hebben. Controleer ook of u alle Hallo < en > tekens hebt verwijderd.

Als u gebruikmaakt van een teksteditor, wordt Hallo-opdracht kopiëren toohello Klembord instellen en vervolgens met de rechtermuisknop op uw Windows PowerShell-opdrachtprompt openen. Hiermee Hallo opdrachtset als een reeks PowerShell-opdrachten uitgeven en maakt u uw virtuele machine van Azure. U kunt ook Hallo-opdracht ingesteld in PowerShell ISE Hallo uitvoeren.

Als u deze virtuele machine opnieuw of een vergelijkbare maakt, kunt u:

* Sla deze opdracht ingesteld als het bestand in een PowerShell-script (*.ps1).
* Opslaan van deze opdracht ingesteld als een Azure Automation-runbook in Hallo **Automation-Accounts** sectie Hallo Azure-portal.

## <a id="examples"></a>Voorbeelden
Hier vindt u twee voorbeelden van het gebruik van Hallo stappen hierboven toobuild Azure PowerShell-opdrachtsets die op basis van Windows Azure virtuele machines maken.

### <a name="example-1"></a>Voorbeeld 1
Ik moet een PowerShell opdracht ingesteld toocreate Hallo eerste virtuele machine voor een Active Directory-domeincontroller:

* Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.
* Hallo naam AZDC1 heeft.
* Een zelfstandige computer is.
* Heeft een schijf aanvullende gegevens van 20 GB.
* Hallo statisch IP-adres 192.168.244.4 heeft.
* Staat in subnet van de Hallo back-end van Hallo AZDatacenter virtuele netwerk.
* In de cloudservice hello Azure TailspinToys is.

Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine, met lege regels tussen elk blok omwille van de leesbaarheid.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a>Voorbeeld 2
Ik moet een PowerShell opdracht ingesteld toocreate een virtuele machine voor een line-of-business-server die:

* Hallo Windows Server 2012 R2 Datacenter installatiekopie gebruikt.
* Hallo naam LOB1 heeft.
* Is een lid van domein van Hallo corp.contoso.com.
* Heeft een schijf aanvullende gegevens van 200 GB.
* Hallo FrontEnd subnet Hallo AZDatacenter virtueel netwerk heeft.
* In de cloudservice hello Azure TailspinToys is.

Hier volgt Hallo bijbehorende Azure PowerShell-opdracht set toocreate van deze virtuele machine.

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a>Volgende stappen
Als u een besturingssysteemschijf die groter is dan 127 GB nodig hebt, kunt u [expand Hallo OS station](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

