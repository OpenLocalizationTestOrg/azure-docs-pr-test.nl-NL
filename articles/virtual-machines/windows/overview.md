---
title: Overzicht van virtuele Machines aaaWindows | Microsoft Docs
description: Meer informatie over het maken en beheren van virtuele Windows-machines in Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager,azure-service-management
ms.assetid: fbae9c8e-2341-4ed0-bb20-fd4debb2f9ca
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 8015b1aa4bcdaac2e721f25d85a5bc995a22f0f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-windows-virtual-machines-in-azure"></a>Overzicht van virtuele Windows-machines in Azure

Azure Virtual Machines (VM) vormen een van de diverse typen [schaalbare on-demand computerresources](../../app-service-web/choose-web-site-cloud-service-vm.md) die Azure biedt. Normaal gesproken u een virtuele machine als u meer controle over de computeromgeving Hallo dan hello andere opties bieden nodig. In dit artikel vindt u informatie over wat u moet overwegen voordat u een VM maakt, hoe u deze maakt en hoe u deze beheert.

Een Azure VM-geeft u de flexibiliteit van virtualisatie zonder toobuy Hallo en onderhouden Hallo fysieke hardware waarop deze wordt uitgevoerd. U moet echter nog steeds toomaintain Hallo VM door het uitvoeren van taken, zoals het configureren, patchen en Hallo-software die wordt uitgevoerd op deze installeren.

Virtuele machines in Azure kunnen op verschillende manieren worden gebruikt. Een aantal voorbeelden:

* **Ontwikkeling en tests** : Azure VM's bieden een snelle en eenvoudige manier toocreate een computer met specifieke configuraties vereist toocode en testen van een toepassing.
* **Toepassingen in de cloud Hallo** – omdat de aanvraag voor uw toepassing kunt fluctueren, kan deze financieel aantrekkelijk toorun maken op een virtuele machine in Azure. U betaalt voor extra virtuele machines wanneer u ze nodig hebt en schakelt ze uit wanneer u ze niet meer nodig hebt.
* **Uitgebreide datacenter** – virtuele machines in een Azure-netwerk kan eenvoudig worden verbonden tooyour bedrijfsnetwerk.

aantal virtuele machines die gebruikmaakt van uw toepassing Hello kunt opschalen en uit toowhatever is vereist toomeet uw behoeften.

## <a name="what-do-i-need-toothink-about-before-creating-a-vm"></a>Wat moet ik toothink over voordat u een virtuele machine maakt?
Er is altijd een groot aantal [overwegingen bij het ontwerpen](/architecture/reference-architectures/virtual-machines-linux?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) wanneer u de infrastructuur van een toepassing verder uitwerkt in Azure. Deze aspecten van een virtuele machine zijn belangrijk toothink over voordat u begint:

* Hallo-namen van de toepassingsresources van uw
* Hallo-locatie waar Hallo resources worden opgeslagen
* Hallo-grootte van Hallo VM
* Hallo kunt u het maximum aantal VM's die kunnen worden gemaakt
* Hallo-besturingssysteem dat Hallo VM wordt uitgevoerd
* Hallo-configuratie van Hallo VM nadat deze is gestart
* Hallo verwante resources die Hallo die VM moet

### <a name="naming"></a>Naamgeving
Een virtuele machine heeft een [naam](/architecture/best-practices/naming-conventions#naming-rules-and-restrictions?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toegewezen tooit en er is een computernaam die is geconfigureerd als onderdeel van het Hallo-besturingssysteem. Hallo-naam van een virtuele machine kan worden up too15 tekens.

Als u Azure toocreate hello besturingssysteemschijf, Hallo computernaam en naam van de virtuele machine Hallo zijn Hallo dezelfde. Als u [uploaden en uw eigen installatiekopie gebruiken](upload-generalized-managed.md) die een eerder geconfigureerde besturingssysteem bevat en toocreate een virtuele machine worden gebruikt, Hallo namen kunnen afwijken. We raden aan dat wanneer u uw eigen installatiekopiebestand uploadt, u maakt de computernaam Hallo in Hallo-besturingssysteem en de naam van de virtuele machine Hallo Hallo dezelfde.

### <a name="locations"></a>Locaties
Alle resources in Azure gemaakt worden gedistribueerd over meerdere [geografische regio's](https://azure.microsoft.com/regions/) Hallo wereld. Normaal gesproken Hallo regio heet **locatie** bij het maken van een virtuele machine. Voor een VM geeft Hallo locatie waar Hallo virtuele harde schijven zijn opgeslagen.

Deze tabel bevat enkele Hallo manieren om een lijst met beschikbare locaties.

| Methode | Beschrijving |
| --- | --- |
| Azure Portal |Selecteer een locatie in de lijst Hallo bij het maken van een virtuele machine. |
| Azure PowerShell |Gebruik Hallo [Get-AzureRmLocation](/powershell/module/azurerm.resources/get-azurermlocation) opdracht. |
| REST API |Gebruik Hallo [locaties lijst](https://docs.microsoft.com/rest/api/resources/subscriptions#Subscriptions_ListLocations) bewerking. |

### <a name="vm-size"></a>VM-grootte
Hallo [grootte](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) Hallo VM die u gebruikt, wordt bepaald door Hallo werkbelasting die u toorun wilt. Hallo-grootte die u bepaalt vervolgens factoren zoals de verwerking van kracht, geheugen en opslagcapaciteit. Azure biedt een groot aantal verschillende grootten toosupport verschillende manieren van gebruik.

Azure kosten een [uurprijs](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) op basis van de grootte en het besturingssysteem Hallo van de virtuele machine. Voor de hele uren Azure rekent alleen voor Hallo minuten gebruikt. De opslag wordt afzonderlijk berekend en in rekening gebracht.

### <a name="vm-limits"></a>VM-limieten
Uw abonnement heeft standaard [quotalimieten](../../azure-subscription-service-limits.md) dat kan invloed hebben op Hallo-implementatie van veel VM's voor uw project. de huidige limiet Hallo op basis van per abonnement is 20 VM's per regio. Limieten kunnen worden verhoogd door een ondersteuningsticket in te dienen met een aanvraag voor een verhoging.

### <a name="operating-system-disks-and-images"></a>Schijven en installatiekopieën voor een besturingssysteem
Virtuele machines gebruiken [virtuele harde schijven (VHD's)](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) toostore hun besturingssysteem (OS) en gegevens. VHD's worden ook gebruikt voor afbeeldingen van Hallo die u uit tooinstall een besturingssysteem kiezen kunt. 

Azure biedt veel [marketplace-installatiekopieën](https://azure.microsoft.com/marketplace/virtual-machines/) toouse met verschillende versies en typen van Windows Server-besturingssystemen. Marketplace-installatiekopieën worden aangeduid met uitgever, aanbieding, SKU en versie van de installatiekopie (de versie wordt meestal gespecificeerd als meest recente). 

Deze tabel ziet enkele manieren waarop u Hallo-informatie voor een afbeelding vindt.

| Methode | Beschrijving |
| --- | --- |
| Azure Portal |Hallo-waarden worden automatisch opgegeven voor u wanneer u een installatiekopie toouse selecteert. |
| Azure PowerShell |[Get-AzureRMVMImagePublisher](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimagepublisher): locatie "location"<BR>[Get-AzureRMVMImageOffer](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.5.0/get-azurermvmimageoffer): locatie "location", uitgever "publisherName"<BR>[Get-AzureRMVMImageSku](/powershell/module/azurerm.compute/get-azurermvmimagesku): locatie "location", uitgever "publisherName", aanbieding: "offerName" |
| REST-API’s |[Uitgevers van installatiekopieën weergeven](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publishers)<BR>[Aanbiedingen van installatiekopieën weergeven](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offers)<BR>[Installatiekopie-SKU's weergeven](https://docs.microsoft.com/rest/api/compute/platformimages/platformimages-list-publisher-offer-skus) |

U kunt ervoor kiezen te[uploaden en uw eigen installatiekopie gebruiken](upload-generalized-managed.md#upload-the-vhd-to-your-storage-account) en wanneer u dit doet, Hallo de naam van uitgever, aanbieding en sku worden niet gebruikt.

### <a name="extensions"></a>Extensies
VM-[extensies](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) geven uw VM meer mogelijkheden via de post-implementatieconfiguratie en geautomatiseerde taken.

Deze algemene taken kunnen worden uitgevoerd met extensies:

* **Aangepaste scripts uitvoeren** – hello [extensie voor aangepaste scripts](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kunt u werkbelastingen op Hallo VM configureren door het uitvoeren van uw script wanneer hello VM is ingericht.
* **Implementeren en beheren van configuraties** – hello [PowerShell Desired State Configuration (DSC)-extensie](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) kunt u DSC op een VM-toomanage instellen configuraties en omgevingen.
* **Verzamelen van diagnostische gegevens** – hello [Azure-extensie voor diagnostische gegevens](extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) helpt bij het configureren van Hallo VM toocollect diagnostics-gegevens die gebruikt toomonitor worden kunnen Hallo status van uw toepassing.

### <a name="related-resources"></a>Gerelateerde resources
Hallo-resources in deze tabel worden gebruikt door VM Hallo en moeten tooexist of worden gemaakt wanneer Hallo VM is gemaakt.

| Resource | Vereist | Beschrijving |
| --- | --- | --- |
| [Resourcegroep](../../azure-resource-manager/resource-group-overview.md) |Ja |Hallo VM moet zijn opgenomen in een resourcegroep. |
| [Opslagaccount](../../storage/common/storage-create-storage-account.md) |Ja |Hallo VM moet Hallo storage account toostore de virtuele harde schijven. |
| [Virtueel netwerk](../../virtual-network/virtual-networks-overview.md) |Ja |Hallo VM moet lid zijn van een virtueel netwerk. |
| [Openbaar IP-adres](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) |Nee |Hallo VM kan een openbare tooit tooremotely voor IP-adres toegewezen toegang tot hebben. |
| [Netwerkinterface](../../virtual-network/virtual-network-network-interface.md) |Ja |Hallo VM moet Hallo network interface toocommunicate in Hallo-netwerk. |
| [Gegevensschijven](attach-managed-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |Nee |Hallo VM kan gegevens schijven tooexpand opslagmogelijkheden bevatten. |

## <a name="how-do-i-create-my-first-vm"></a>Hoe kan ik mijn eerste VM maken?
U hebt verschillende mogelijkheden voor het maken van uw VM. Hallo keuze die u maakt, is afhankelijk van Hallo-omgeving in. 

Deze tabel bevat informatie tooget die u beginnen met het opstellen van uw virtuele machine.

| Methode | Artikel |
| --- | --- |
| Azure Portal |[Maak een virtuele machine met Windows met behulp van Hallo-portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Sjablonen |[Een virtuele Windows-machine maken met een Resource Manager-sjabloon](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Azure PowerShell |[Een Windows-VM maken met behulp van PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| Client-SDK 's |[Azure-bronnen implementeren met C#](csharp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) |
| REST-API’s |[Een VM maken of bijwerken](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-create-or-update) |

U hoopt natuurlijk dat alles goed gaat, maar soms gaat er iets fout. Als deze situatie zich tooyou voordoet, bekijkt hello informatie in [problemen bij de implementatie met het maken van een virtuele Windows-machine in Azure Resource Manager oplossen](troubleshoot-deployment-new-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="how-do-i-manage-hello-vm-that-i-created"></a>Hoe beheer ik Hallo VM die ik heb gemaakt?
VM's kunnen worden beheerd via een op een browser gebaseerde portal, opdrachtregelprogramma's met ondersteuning voor het uitvoeren van scripts of rechtstreeks via API's. Sommige veelvoorkomende beheertaken die u kunt uitvoeren zijn informatie ophalen over een VM aanmelden tooa VM, het beheren van beschikbaarheid en back-ups maken.

### <a name="get-information-about-a-vm"></a>Informatie over een VM ophalen
Deze tabel ziet u een aantal manieren waarop Hallo die u informatie over een virtuele machine ophalen kunt.

| Methode | Beschrijving |
| --- | --- |
| Azure Portal |Klik op het menu hub Hallo **virtuele Machines** en selecteer vervolgens Hallo VM op Hallo-lijst. Op Hallo blade voor Hallo VM hebt u toegang toooverview informatie, instellingswaarden en bewaking metrische gegevens. |
| Azure PowerShell |Zie voor meer informatie over het gebruik van PowerShell toomanage VMs [maken en beheren van Windows-VM's met Azure PowerShell-module Hallo](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |
| REST API |Gebruik Hallo [informatie over het ophalen van VM](https://docs.microsoft.com/rest/api/compute/virtualmachines/virtualmachines-get) bewerking tooget informatie over een virtuele machine. |
| Client-SDK 's |Zie voor meer informatie over het gebruik van C# toomanage VMs [beheren van virtuele Machines van Azure met Azure Resource Manager en C#](csharp-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). |

### <a name="log-on-toohello-vm"></a>Meld u aan toohello VM
U de knop verbinden hello te gebruiken in hello Azure-portal[een Remote Desktop (RDP)-sessie starten](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Dingen kunnen soms fout gaan wanneer u probeert een verbinding met extern toouse. Als deze situatie zich tooyou voordoet, bekijk Hallo help-informatie in [problemen met extern bureaublad-verbindingen tooan Azure virtuele machine met Windows](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="manage-availability"></a>Beschikbaarheid beheren
Het is belangrijk voor u toounderstand hoe te[hoge beschikbaarheid garanderen](manage-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) voor uw toepassing. Deze configuratie omvat het maken van meerdere virtuele machines tooensure die ten minste één wordt uitgevoerd.

Voor uw implementatie tooqualify voor onze 99.95 VM Service Level Agreement, moet u toodeploy twee of meer virtuele machines die de werkbelasting binnen een [beschikbaarheidsset](tutorial-availability-sets.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Deze configuratie zorgt ervoor dat uw virtuele machines worden verdeeld over meerdere foutdomeinen en worden geïmplementeerd op hosts met verschillende onderhoudsvensters. Hallo volledige [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/) wordt uitgelegd Hallo gegarandeerde beschikbaarheid van Azure als geheel.

### <a name="back-up-hello-vm"></a>Back-up Hallo VM
Een [Recovery Services-kluis](../../backup/backup-introduction-to-azure-backup.md) gebruikte tooprotect gegevens en activa in Azure Backup- en Azure Site Recovery services is. U kunt ook een Recovery Services-kluis gebruiken[implementeren en beheren van back-ups voor Resource Manager geïmplementeerde VM's met behulp van PowerShell](../../backup/backup-azure-vms-automation.md). 

## <a name="next-steps"></a>Volgende stappen
* Als het uw bedoeling is toowork met Linux VM's, bekijkt u [Azure- en Linux](../linux/overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Meer informatie over richtlijnen over het instellen van uw infrastructuur in Hallo Hallo [voorbeeld Azure-infrastructuur scenario](infrastructure-example.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
