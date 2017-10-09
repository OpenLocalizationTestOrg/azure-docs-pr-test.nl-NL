---
title: op basis van aaaHD rendabele standaardopslag en Azure VM-schijven | Microsoft Docs
description: Bespreek rendabele standaardopslag en niet-beheerde en beheerde VM-schijven.
services: storage
documentationcenter: 
author: yuemlu
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: yuemlu
ms.openlocfilehash: c9162eaea50cdd43862378e62dcff9a3d762e092
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cost-effective-standard-storage-and-unmanaged-and-managed-azure-vm-disks"></a>Rendabele standaardopslag en niet-beheerde en beheerde Azure VM-schijven

Azure Standard-opslag biedt ondersteuning voor betrouwbare, goedkope schijven voor virtuele machines waarop niet latentie gevoelig werkbelastingen worden uitgevoerd. Het ondersteunt ook blobs, tabellen, wachtrijen en -bestanden. Met de Standard-opslag Hallo gegevens opgeslagen op de harde schijven (HDD's). Als u werkt met virtuele machines, kunt u standaardopslag schijven voor ontwikkel-/ Testscenario's en minder kritieke werkbelastingen en premium-schijven voor opslag voor essentiële productietoepassingen. Standard-opslag is beschikbaar in alle Azure-regio's. 

In dit artikel wordt de nadruk gelegd op Hallo gebruik van standard-opslag voor VM-schijven. Raadpleeg voor meer informatie over Hallo gebruik van opslag met blobs, tabellen, wachtrijen en bestanden toohello [inleiding tooStorage](../storage-introduction.md).

## <a name="disk-types"></a>Schijftypen

Er zijn twee manieren toocreate standaardschijven voor Azure Virtual machines:

**Schijven zonder begeleiding**: dit is de oorspronkelijke methode Hallo waar u Hallo storage accounts die worden gebruikt toostore Hallo VHD-bestanden die overeenkomen met het VM-schijven toohello beheren. VHD-bestanden worden opgeslagen als pagina-blobs in opslagaccounts. Niet-beheerde schijven kunnen worden aangesloten tooany Azure VM-grootte, Hallo virtuele machines die gebruikmaken van Premium-opslag, voornamelijk zoals Hallo DSv2 en GS-serie. Virtuele machines in Azure ondersteuning voor het koppelen van verschillende standaardschijven toestaan van too256 TB opslagruimte per virtuele machine.

[**Azure-beheerde schijven**](../../virtual-machines/windows/managed-disks-overview.md): deze functie Hallo storage-accounts voor Hallo VM-schijven gebruikt voor u beheert. U geeft Hallo type (Premium of standaard) en de grootte van de schijf moet u en Azure maakt en beheert Hallo schijf voor u. U hebt geen tooworry over Hallo schijven brengen tussen meerdere opslagaccounts in volgorde tooensure blijft u binnen Hallo schaalbaarheidslimieten voor opslagaccounts Hallo--Azure verwerkt die voor u.

Hoewel beide typen schijven beschikbaar zijn, wordt u aangeraden schijven beheerd tootake profiteren van veel functies.

tooget de slag met Azure Standard-opslag, gaat u naar [gratis aan de slag](https://azure.microsoft.com/pricing/free-trial/). 

Voor informatie over hoe toocreate een virtuele machine met schijven beheerd Raadpleeg een van volgende Hallo artikelen.

* [Een virtuele machine maken met behulp van Resource Manager en PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)
* [Maak een Linux-VM met hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)

## <a name="standard-storage-features"></a>Standard-opslag-functies 

We gaan verdiepen in enkele Hallo functies van de Standard-opslag. Zie voor meer informatie [inleiding tooAzure opslag](../storage-introduction.md).

**Standard-opslag**: Azure Standard-opslag biedt ondersteuning voor Azure-schijven, Azure Blobs, Azure File storage, Azure-tabellen en wachtrijen in Azure. toouse standaard opslagservices, beginnen met [maken van een Azure Storage-account](storage-create-storage-account.md#create-a-storage-account).

**Standard-opslag-schijven:** standaardopslag schijven kunnen worden gekoppeld tooall Azure VM's met inbegrip van grootte-serie VM's voor Premium-opslag gebruikt zoals Hallo DSv2 en GS-serie. De schijf van een standard-opslag kan alleen worden aangesloten tooone VM. U kunt echter een of meer van deze schijven tooa VM, up toohello maximale schijf-aantal gedefinieerd voor de grootte van die VM koppelen. In Hallo sectie op standaard Storage Scalability and Performance Targets volgen, wordt er Hallo specificaties in meer detail beschreven. 

**Standaard pagina-blob**: standaard pagina-blobs zijn gebruikte toohold permanente schijven voor virtuele machines en kunnen ook rechtstreeks via REST net als andere soorten Azure Blobs worden geopend. [Pagina-blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) zijn van een verzameling 512-byte-'s die zijn geoptimaliseerd voor willekeurige lees- en schrijfbewerkingen. 

**Storage-replicatie:** In de meeste regio's, gegevens in een standaard opslagaccount gerepliceerde lokaal of geogerepliceerde in meerdere datacentrums kunnen worden. Hallo vier typen replicatie beschikbaar zijn lokaal redundante opslag (LRS), Zone-redundante opslag (ZRS), geografisch redundante opslag (GRS) en geografisch redundante opslag met leestoegang (RA-GRS). Beheerde schijven in de Standard-opslag ondersteunt momenteel lokaal redundante opslag (LRS) alleen. Zie voor meer informatie [Opslagreplicatie](../storage-redundancy.md).

## <a name="scalability-and-performance-targets"></a>Schaalbaarheids- en prestatiedoelen

In deze sectie wordt beschreven Hallo schaalbaarheids- en prestatiedoelen u tooconsider moet als standard-opslag.

### <a name="account-limits--does-not-apply-toomanaged-disks"></a>Limieten – toomanaged schijven is niet van toepassing

| **Resource** | **Standaardlimiet** |
|--------------|-------------------|
| TB per storage-account  | 500 TB |
| Maximale inkomende<sup>1</sup> per storage-account (ons regio's) | 10 Gbps als GRS/ZRS is ingeschakeld, 20 Gbps voor LRS |
| Maximum aantal uitgaande<sup>1</sup> per storage-account (ons regio's) | 20 Gbps als RA-GRS/GRS/ZRS is ingeschakeld, 30 Gbps voor LRS |
| Maximale inkomende<sup>1</sup> per storage-account (Europese en Aziatische regio's) | 5 Gbps als GRS/ZRS is ingeschakeld, 10 Gbps voor LRS |
| Maximum aantal uitgaande<sup>1</sup> per storage-account (Europese en Aziatische regio's) | 10 Gbps als RA-GRS/GRS/ZRS is ingeschakeld, 15 Gbps voor LRS |
| Totale snelheid van aanvragen voor (ervan uitgaande dat de grootte van 1 KB object) per storage-account | Up too20, 000 IOP's, entiteiten per seconde of berichten per seconde |

<sup>1</sup> inkomend verwijst tooall (aanvragen) verzonden gegevens tooa storage-account. Uitgaande gegevens verwijst tooall gegevens (antwoorden) ontvangen van een opslagaccount.

Zie voor meer informatie [Azure Storage Scalability and Performance Targets](../storage-scalability-targets.md).

Als Hallo van uw toepassing hello schaalbaarheidsdoelen van een enkele opslagaccount overschrijdt behoeften, bouwen van uw toepassing toouse meerdere opslagaccounts en partitioneren van uw gegevens over de storage-accounts. Ook kunt u beheerde Azure-schijven en Azure Hallo partitionerings- en plaatsing van uw gegevens u wilt beheren.

### <a name="standard-disks-limits"></a>Standaardschijven limieten

In tegenstelling tot de Premium-schijven Hallo i/o-bewerkingen per seconde (IOPS) en de doorvoer (bandbreedte) van standaardschijven niet ingericht. Hallo prestaties van standaardschijven is afhankelijk van Hallo VM grootte toowhich Hallo schijf is gekoppeld, niet toohello grootte van Hallo schijf. U kunt tooachieve up toohello prestaties beperken die worden vermeld in de onderstaande tabel voor Hallo kan verwachten.

**Standaardschijven limieten (beheerde en onbeheerde)**

| **VM-laag**            | **Basis VM-laag** | **Standaard VM-laag** |
|------------------------|-------------------|----------------------|
| De grootte van de maximale diskette          | 4095 GB           | 4095 GB              |
| Maximaal 8 KB IOP's per schijf | Up too300         | Up too500            |
| Maximale Bandwidth per schijf | Up too60 MB/s     | Up too60 MB/s        |

Als uw werkbelasting schijfondersteuning met hoge prestaties, lage latentie is vereist, moet u rekening houden met behulp van Premium-opslag. Ga naar tooknow meer voordelen van Premium-opslag [High-Performance Premium-opslag- en Azure VM-schijven](../storage-premium-storage.md). 

## <a name="snapshots-and-copy-blob"></a>Momentopnamen en blob kopiëren

toohello Storage-service, Hallo VHD-bestand is een pagina-blob. U kunt momentopnamen van pagina-blobs en kopieer deze tooanother locatie, zoals een ander opslagaccount.

### <a name="unmanaged-disks"></a>Niet-beheerde schijven

U kunt maken [incrementele momentopnamen](../../virtual-machines/windows/incremental-snapshots.md) voor niet-beheerde standaard in de Hallo dezelfde schijven manier als u momentopnamen met Standard-opslag. U wordt aangeraden dat u momentopnamen maken en kopieer deze momentopnamen tooa geografisch redundante standard-opslagaccount als de bronschijf in een account met lokaal redundante opslag is. Zie voor meer informatie [Azure redundantie opslagopties](../storage-redundancy.md).

Als een schijf aangesloten tooa VM is, worden bepaalde API-bewerkingen zijn niet toegestaan op Hallo-schijven. Bijvoorbeeld, u kunt niet uitvoeren een [Blob kopiëren](/rest/api/storageservices/Copy-Blob) bewerking op de blob zolang Hallo schijf is gekoppeld tooa VM. In plaats daarvan eerst een momentopname maken van blob met behulp van Hallo [momentopname Blob](/rest/api/storageservices/Snapshot-Blob) REST-API-methode en voert u Hallo [Blob kopiëren](/rest/api/storageservices/Copy-Blob) Hallo momentopname toocopy Hallo schijf is gekoppeld. U kunt ook Hallo schijf loskoppelen en vervolgens alle noodzakelijke bewerkingen uitvoeren.

toomaintain geografisch redundante exemplaren van de momentopnamen, kunt u momentopnamen van een lokaal redundante opslag tooa geografisch redundante opslag met standaard rekening kopiëren met behulp van AzCopy of Blob kopiëren. Zie voor meer informatie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](storage-use-azcopy.md) en [Blob kopiëren](/rest/api/storageservices/Copy-Blob).

Zie voor gedetailleerde informatie voor het uitvoeren van de REST-bewerkingen op de pagina-blobs in opslagaccounts standaard [REST-API van Azure Storage-Services](/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference).

### <a name="managed-disks"></a>Managed Disks

Een momentopname voor een beheerde schijf is een alleen-lezen kopie van beheerde Hallo-schijf die wordt opgeslagen als een standard-beheerde schijven. Incrementele momentopnamen worden momenteel niet ondersteund voor schijven die worden beheerd, maar worden ondersteund in toekomstige Hallo.

Als een beheerde schijf gekoppelde tooa VM, worden bepaalde API-bewerkingen zijn niet toegestaan op Hallo-schijven. U kunt bijvoorbeeld een shared access signature (SAS) tooperform een kopieerbewerking niet genereren tijdens het Hallo-schijf is aangesloten tooa VM. In plaats daarvan maakt eerst een momentopname van Hallo schijf en Voer Hallo kopie van Hallo momentopname. U kunt ook Hallo schijf loskoppelen en vervolgens een shared access signature (SAS) tooperform Hallo kopieerbewerking te genereren.

## <a name="pricing-and-billing"></a>Prijzen en facturering

Wanneer u de Standard-opslag, hello volgende factureringsvoorwaarden van toepassing:

* Standard-opslag zonder begeleiding schijven/gegevensgrootte 
* Beheerde standaardschijven
* Standard-opslag-momentopnamen
* Uitgaande gegevensoverdracht
* Transacties

**De grootte van de schijf en gegevens van de opslagruimte zonder begeleiding:** voor niet-beheerde schijven en andere gegevens (blobs, tabellen, wachtrijen en -bestanden), u in rekening worden gebracht alleen Hallo hoeveelheid ruimte u gebruikt. Bijvoorbeeld, als u een virtuele machine waarvan pagina-blob is ingericht als 127 GB, maar hello VM is in feite alleen met behulp van 10 GB aan ruimte, wordt u gefactureerd voor 10 GB aan ruimte. Standard-opslag van too8191 GB en standaard niet-beheerde schijven up too4095 GB ondersteund. 

**Schijven die worden beheerd:** beheerde schijven worden gefactureerd op Hallo ingericht grootte. Als de schijf is ingericht als een schijf van 10 GB en u alleen met behulp van 5 GB, wordt nog steeds in rekening gebracht voor Hallo inrichten grootte van 10 GB.

**Momentopnamen**: momentopnamen van standaardschijven wordt gefactureerd voor Hallo extra capaciteit die wordt gebruikt door Hallo momentopnamen. Zie voor informatie over momentopnamen [maken van een momentopname van een Blob](/rest/api/storageservices/Creating-a-Snapshot-of-a-Blob).

**Uitgaande gegevensoverdracht**: [uitgaande gegevensoverdracht](https://azure.microsoft.com/pricing/details/data-transfers/) (gegevens uit de Azure-datacenters gaan) worden gefactureerd voor bandbreedtegebruik.

**Transactie**: Azure rekent $0.0036 per 100.000 transacties voor standard-opslag. Transacties omvatten zowel lees en bewerkingen toostorage schrijven.

Zie voor gedetailleerde informatie over prijzen voor Standard-opslag, virtuele Machines en schijven beheerd:

* [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Virtuele Machines prijzen](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Beheerde schijven prijzen](https://azure.microsoft.com/pricing/details/managed-disks)

## <a name="azure-backup-service-support"></a>Ondersteuning voor Azure Backup-service 

Virtuele machines met niet-beheerde schijven kunt een back-up maken met Azure Backup. [Meer informatie](../../backup/backup-azure-vms-first-look-arm.md).

U kunt ook hello Azure Backup-service gebruiken met schijven beheerd toocreate een back-uptaak met back-ups op basis van tijd, eenvoudig herstel van de virtuele machine en back-up bewaarbeleid. U vindt meer informatie over dit op [met behulp van Azure Backup-service voor virtuele machines met schijven beheerd](../../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup).

## <a name="next-steps"></a>Volgende stappen

* [Inleiding tooAzure opslag](../storage-introduction.md)

* [Een opslagaccount maken](../storage-create-storage-account.md)

* [Overzicht Managed Disks](../../virtual-machines/windows/managed-disks-overview.md)

* [Een virtuele machine maken met behulp van Resource Manager en PowerShell](/azure/virtual-machines/windows/quick-create-powershell.md)

* [Maak een Linux-VM met hello Azure CLI 2.0](../../virtual-machines/windows/quick-create-cli.md)
