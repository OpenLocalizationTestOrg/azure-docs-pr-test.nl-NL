---
title: Statusconfiguratie voor een overzicht van Azure aaaDesired | Microsoft Docs
description: Overzicht voor het gebruik van Hallo Microsoft Azure-extensie-handler voor PowerShell Desired State Configuration. Vereisten, architectuur, cmdlets zoals..
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: bbacbc93-1e7b-4611-a3ec-e3320641f9ba
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 01/09/2017
ms.author: zachal
ms.openlocfilehash: b0337a2f1124f35e5e40c1478bd7530427e59d44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-azure-desired-state-configuration-extension-handler"></a>Inleiding toohello Azure Desired State Configuration-extensie-handler
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Hello Azure VM-Agent en de bijbehorende extensies uitmaken deel van Hallo Microsoft Azure Infrastructure Services. VM-extensies zijn softwareonderdelen die Hallo VM-functionaliteit uitbreiden en verschillende bewerkingen VM vereenvoudigen. Bijvoorbeeld, Hallo VMAccess-extensie worden gebruikte tooreset een beheerderswachtwoord of aangepast Script Hallo extensie gebruikte tooexecute een script op Hallo VM kan worden.

Dit artikel bevat Hallo PowerShell Desired State Configuration (DSC)-extensie voor Azure Virtual machines als onderdeel van hello Azure PowerShell SDK. U kunt nieuwe cmdlets tooupload gebruiken en een PowerShell DSC-configuratie toepassen op een Azure-VM met Hallo PowerShell DSC-extensie is ingeschakeld. Hallo PowerShell DSC-uitbreiding aanroepen in PowerShell DSC tooenact Hallo ontvangen DSC-configuratie op Hallo VM. Deze functionaliteit is ook beschikbaar via hello Azure-portal.

## <a name="prerequisites"></a>Vereisten
**Lokale machine** toointeract met Hallo Azure VM-extensie, of u kunt toouse beide hello Azure-portal hello Azure PowerShell SDK. 

**Gastagent** hello Azure VM die is geconfigureerd door Hallo DSC-configuratie moet toobe een besturingssysteem dat ondersteuning biedt voor Windows Management Framework (WMF) 4.0 ofwel 5.0. Hallo volledige lijst met ondersteunde versies van het besturingssysteem kan worden gevonden op Hallo [versiegeschiedenis van DSC-uitbreiding](https://blogs.msdn.microsoft.com/powershell/2014/11/20/release-history-for-the-azure-dsc-extension/).

## <a name="terms-and-concepts"></a>Termen en begrippen
Deze handleiding wordt ervan uitgegaan bekend bent met de volgende concepten Hallo:

Configuratie: een document DSC-configuratie. 

Knooppunt - doel voor een DSC-configuratie. In dit document verwijst 'knooppunt' altijd tooan Azure VM.

Configuratie - een .psd1 gegevensbestand met milieu gegevens voor een configuratie

## <a name="architectural-overview"></a>Overzicht van architectuur
Hello Azure DSC-uitbreiding gebruikt hello Azure VM-Agent framework toodeliver, nemen en een rapport over DSC-configuraties die zijn uitgevoerd op Azure Virtual machines. Hallo DSC-extensie verwacht een ZIP-bestand met ten minste een configuratie-document en een aantal parameters opgegeven via Hallo-SDK van Azure PowerShell of via hello Azure-portal.

Als het Hallo-extensie is aangeroepen voor Hallo eerst, voert deze een installatieproces. Dit proces wordt een versie van Windows Management Framework (WMF) Hallo Hallo logica te volgen met geïnstalleerd:

1. Als hello Azure VM besturingssysteem Windows Server 2016 is, wordt geen actie ondernomen. Windows Server 2016 heeft al Hallo meest recente versie van PowerShell is geïnstalleerd.
2. Als hello `wmfVersion` eigenschap is opgegeven, die versie van Hallo WMF is geïnstalleerd, tenzij deze is niet compatibel met OS Hallo van de virtuele machine.
3. Als er geen `wmfVersion` eigenschap is opgegeven, Hallo meest toepasselijke versie Hallo WMF is geïnstalleerd.

Installatie van Hallo WMF moet opnieuw worden opgestart. Na opnieuw opstarten, Hallo uitbreiding downloadt Hallo ZIP-bestand is opgegeven in Hallo `modulesUrl` eigenschap. Als deze locatie zich in Azure blob-opslag, een SAS-token kan worden opgegeven in Hallo `sasToken` eigenschap tooaccess Hallo bestand. Nadat Hallo .zip is gedownload en uitgepakt, de functie van de configuratie is gedefinieerd in Hallo `configurationFunction` toogenerate Hallo MOF-bestand wordt uitgevoerd. Hallo-extensie voert `Start-DscConfiguration -Force` op Hallo gegenereerd MOF-bestand. Hallo-extensie uitvoer vastgelegd en schrijft deze weer uit toohello Azure Status kanaal. Vanaf dit punt op Hallo verwerkt DSC LCM bewaking en correctie als normaal. 

## <a name="powershell-cmdlets"></a>PowerShell-cmdlets
PowerShell-cmdlets kunnen worden gebruikt met Azure Resource Manager of Hallo-classic deployment model toopackage, publiceren en DSC-extensie-implementaties controleren. Hallo volgende cmdlets die vermeld zijn Hallo-modules voor klassieke implementatie, maar 'Azure' kan worden vervangen door "AzureRm" toouse hello Azure Resource Manager-model. Bijvoorbeeld: `Publish-AzureVMDscConfiguration` gebruikt Hallo klassieke implementatiemodel, waarbij `Publish-AzureRmVMDscConfiguration` maakt gebruik van Azure Resource Manager. 

`Publish-AzureVMDscConfiguration`wordt in een configuratiebestand, voor afhankelijke DSC-resources wordt gescand en maakt een ZIP-bestand met Hallo-configuratie en DSC-resources nodig tooenact Hallo-configuratie. Daarnaast kunnen er Hallo pakket lokaal via Hallo `-ConfigurationArchivePath` parameter. Het publiceert Hallo ZIP-bestand tooAzure blob-opslag en beveiligt het met een SAS-token.

Hallo ZIP-bestand gemaakt met deze cmdlet heeft Hallo .ps1-configuratiescript op Hallo hoofdmap van de archiefmap Hallo. Bronnen hebben Hallo modulemap geplaatst in de archiefmap Hallo. 

`Set-AzureVMDscExtension`injects hello vereiste instellingen voor Hallo PowerShell DSC-uitbreiding in een VM-configuratie-object. Hallo VM wijzigingen moet in het klassieke implementatiemodel hello, toegepaste tooan virtuele machine van Azure met `Update-AzureVM`. 

`Get-AzureVMDscExtension`haalt status van Hallo DSC-extensie van een bepaalde virtuele machine. 

`Get-AzureVMDscExtensionStatus`haalt status Hallo van Hallo DSC-configuratie door de handler voor Hallo DSC-uitbreiding van kracht. Deze actie kan worden uitgevoerd op een enkele virtuele machine of een groep VM's.

`Remove-AzureVMDscExtension`Hallo-extensie handler verwijdert uit een opgegeven virtuele machine. Deze cmdlet biedt **niet** Hallo-configuratie verwijderen, Hallo WMF verwijderen of wijzigen van Hallo toegepast op Hallo virtuele machine. Hallo-extensie handler worden alleen verwijderd. 

**Belangrijke verschillen in ASM en Azure Resource Manager-cmdlets**

* Azure Resource Manager-cmdlets worden synchroon. ASM-cmdlets zijn asynchroon.
* ResourceGroupName, VMName ArchiveStorageAccountName, versie en locatie zijn alle vereiste parameters in Azure Resource Manager.
* ArchiveResourceGroupName is een nieuwe optionele parameter voor Azure Resource Manager. U kunt deze parameter opgeven wanneer uw storage-account hoort tooa andere resourcegroep dan Hallo een waar Hallo virtuele machine wordt gemaakt.
* ConfigurationArchive wordt ArchiveBlobName aangeroepen in Azure Resource Manager
* ContainerName wordt ArchiveContainerName aangeroepen in Azure Resource Manager
* StorageEndpointSuffix wordt ArchiveStorageEndpointSuffix aangeroepen in Azure Resource Manager
* Hallo AutoUpdate switch is tooAzure Resource Manager tooenable automatische updates van Hallo extensie handler toohello meest recente versie als en wanneer deze beschikbaar toegevoegd. Houd er rekening mee dat deze parameter heeft Hallo potentiële toocause herstarts op Hallo VM wanneer een nieuwe versie van WMF is vrijgegeven Hallo. 

## <a name="azure-portal-functionality"></a>Azure portal-functionaliteit
Blader tooa VM. -Onder Instellingen > Algemeen klik "-extensies." Een nieuw deelvenster wordt gemaakt. Klik op "Toevoegen" en selecteer PowerShell DSC.

Hallo-portal moet invoer.
**Configuratie-Modules of Script**: dit veld is verplicht. Vereist een .ps1-bestand met een configuratiescript of een ZIP-bestand met een .ps1-configuratiescript in Hallo-hoofdmap en alle afhankelijke resources in mappen van de module binnen Hallo .zip. Het kan worden gemaakt met de Hallo `Publish-AzureVMDscConfiguration -ConfigurationArchivePath` opgenomen in het Hallo-SDK van Azure PowerShell cmdlet. Hallo ZIP-bestand is geüpload naar de gebruiker blob-opslag beveiligd door een SAS-token. 

**Bestand met configuratiegegevens PSD1**: dit veld is optioneel. Als uw configuratie een configuratiebestand voor de gegevens in .psd1 vereist, gebruikt u dit veld tooselect deze en upload het tooyour gebruiker blob-opslag, waar deze wordt beveiligd door een SAS-token. 

**Naam van configuratie Modulegekwalificeerde**: .ps1-bestanden kunnen meerdere functies van de configuratie hebben. Voer de naam Hallo van Hallo .ps1 configuratiescript gevolgd door een '\' en Hallo-naam van Hallo configuratie functie. Bijvoorbeeld, als uw script .ps1 heeft configuration.ps1' hello naam' en Hallo configuratie 'IisInstall' is, dus voert u:`configuration.ps1\IisInstall`

**Configuratie argumenten**: als Hallo configuratie functie argumenten aanneemt, deze hier in Hallo-indeling invoeren `argumentName1=value1,argumentName2=value2`. Opmerking: deze indeling is een andere indeling dan hoe configuratie argumenten via PowerShell-cmdlets of de Resource Manager-sjablonen worden geaccepteerd. 

## <a name="getting-started"></a>Aan de slag
Hello Azure DSC-extensie neemt in documenten van DSC-configuratie en ze enacts op Azure Virtual machines. Hier volgt een eenvoudig voorbeeld van een configuratie. Dit lokaal opslaan als 'IisInstall.ps1':

```powershell
configuration IISInstall 
{ 
    node "localhost"
    { 
        WindowsFeature IIS 
        { 
            Ensure = "Present" 
            Name = "Web-Server"                       
        } 
    } 
}
```

volgende stappen plaats Hallo IisInstall.ps1 script op Hallo Hallo opgegeven VM, Hallo configuratie uitvoeren en rapporteren over de status.
###<a name="classic-model"></a>Klassieke model
```powershell
#Azure PowerShell cmdlets are required
Import-Module Azure

#Use an existing Azure Virtual Machine, 'DscDemo1'
$demoVM = Get-AzureVM DscDemo1

#Publish hello configuration script into user storage.
Publish-AzureVMDscConfiguration -ConfigurationPath ".\IisInstall.ps1" -StorageContext $storageContext -Verbose -Force

#Set hello VM toorun hello DSC configuration
Set-AzureVMDscExtension -VM $demoVM -ConfigurationArchive "IisInstall.ps1.zip" -StorageContext $storageContext -ConfigurationName "IisInstall" -Verbose

#Update hello configuration of an Azure Virtual Machine
$demoVM | Update-AzureVM -Verbose

#check on status
Get-AzureVMDscExtensionStatus -VM $demovm -Verbose
```
###<a name="azure-resource-manager-model"></a>Azure Resource Manager-model

```powershell
$resourceGroup = "dscVmDemo"
$location = "westus"
$vmName = "myVM"
$storageName = "demostorage"
#Publish hello configuration script into user storage
Publish-AzureRmVMDscConfiguration -ConfigurationPath .\iisInstall.ps1 -ResourceGroupName $resourceGroup -StorageAccountName $storageName -force
#Set hello VM toorun hello DSC configuration
Set-AzureRmVmDscExtension -Version 2.21 -ResourceGroupName $resourceGroup -VMName $vmName -ArchiveStorageAccountName $storageName -ArchiveBlobName iisInstall.ps1.zip -AutoUpdate:$true -ConfigurationName "IISInstall"

```

## <a name="logging"></a>Logboekregistratie
Logboekbestanden worden opgeslagen:

C:\WindowsAzure\Logs\Plugins\Microsoft.PowerShell.DSC\[versienummer]

## <a name="next-steps"></a>Volgende stappen
Voor meer informatie over PowerShell DSC [gaat u naar de PowerShell-documentatiecentrum hello](https://msdn.microsoft.com/powershell/dsc/overview). 

Hallo onderzoeken [Azure Resource Manager-sjabloon voor Hallo DSC-uitbreiding](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

toofind aanvullende functionaliteit die u met PowerShell DSC beheren kunt [bladeren Hallo PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) voor meer DSC-resources.

Zie voor meer informatie over gevoelige parameters doorgeven in configuraties [beheren van referenties veilig met Hallo DSC-uitbreiding handler](extensions-dsc-credentials.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

