---
title: Veelgestelde vragen (FAQ) over Azure IaaS VM schijven | Microsoft Docs
description: Veelgestelde vragen over Azure IaaS VM-schijven en premium-schijven (beheerde en onbeheerde)
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: robinsh
ms.openlocfilehash: 31d0aa67b6ca58b75b432ae94f93ebcf6d730380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-about-azure-iaas-vm-disks-and-managed-and-unmanaged-premium-disks"></a>Veelgestelde vragen over Azure IaaS VM-schijven en beheerde en onbeheerde premium-schijven

Dit artikel worden enkele veelgestelde vragen over Azure beheerd schijven en Azure Premium-opslag.

## <a name="managed-disks"></a>Beheerde schijven

**Wat is Azure beheerd schijven?**

Beheerde schijven is een functie die vereenvoudigt Schijfbeheer voor Azure IaaS VM's met opslagbeheer-account voor u verwerken. Zie voor meer informatie, Hallo [schijven beheerd overzicht](storage-managed-disks-overview.md).

**Als ik een standard-beheerde schijven van een bestaande VHD 80 GB maken, hoeveel die kost mij?**

Een standard-beheerde schijven gemaakt op basis van een VHD 80 GB wordt beschouwd als Hallo volgende beschikbare standaard schijf, grootte, die een schijf S10. U bent in rekening gebracht volgens toohello S10 schijf prijzen. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).

**Zijn er transactiekosten voor standard-beheerde schijven?**

Ja. U kosten in rekening gebracht voor elke transactie. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).

**Voor een standaard beheerde schijf wordt ik in rekening gebracht voor de werkelijke grootte van gegevens op schijf Hallo HALLO hallo of voor Hallo ingerichte capaciteit van Hallo schijf?**

U bent in rekening gebracht op basis van Hallo ingerichte capaciteit van Hallo schijf. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).

**Hoe wordt de prijzen van beheerde premium-schijven verschilt van niet-beheerde schijven?**

Hallo prijzen van beheerde premium-schijven is hetzelfde als niet-beheerde premium-schijven Hallo.

**Kan ik Hallo opslagaccounttype (Standard of Premium) van mijn beheerde schijven wijzigen?**

Ja. U kunt Hallo opslagaccounttype van uw beheerde schijven wijzigen met behulp van hello Azure-portal, PowerShell of hello Azure CLI.

**Is er een manier die ik kan kopiëren of exporteren van een beheerde schijf tooa persoonlijke storage-account?**

Ja. U kunt uw beheerde schijven exporteren met behulp van hello Azure-portal, PowerShell of hello Azure CLI.

**Kan ik een VHD-bestand in een Azure storage-account toocreate een beheerde schijf met een ander abonnement gebruiken?**

Nee.

**Kan ik een VHD-bestand in een Azure storage-account toocreate een beheerde schijf gebruiken in een andere regio?**

Nee.

**Zijn er beperkingen scale voor klanten die gebruikmaken van beheerde schijven?**

Beheerde schijven elimineert Hallo-limieten die zijn gekoppeld aan de storage-accounts. Hallo-aantal beheerde schijven per abonnement is echter beperkt too2, 000 standaard. U kunt ondersteuning tooincrease dit aantal aanroepen.

**Kan ik een incrementele momentopname van een beheerde schijf volgen?**

Nee. de huidige Snapshots Hallo maakt een volledige kopie van een beheerde schijf. We hebben wel echter toosupport incrementele momentopnamen in toekomstige Hallo plannen.

**Kunnen de virtuele machines in een beschikbaarheidsset bestaan uit een combinatie van beheerde en onbeheerde schijven?**

Nee. Hallo virtuele machines in een beschikbaarheidsset moet gebruiken voor alle beheerde schijven of alle niet-beheerde schijven. Wanneer u een beschikbaarheidsset maakt, kunt u kiezen welk type schijven gewenste toouse.

**Is beheerd schijven Hallo standaardoptie in hello Azure-portal?**

Momenteel niet, maar deze worden standaard in toekomstige Hallo Hallo.

**Kan ik een lege beheerde schijf maken?**

Ja. U kunt een lege schijf maken. Een beheerde schijf kan worden gemaakt onafhankelijk van een virtuele machine, bijvoorbeeld zonder tooa VM kunt koppelen.

**Wat is Hallo ondersteund aantal foutdomeinen voor een beschikbaarheidsset die gebruikmaakt van schijven beheerd?**

Hallo ondersteund aantal foutdomeinen is afhankelijk van Hallo regio waar Hallo beschikbaarheidsset die gebruikmaakt van schijven beheerd zich bevindt, 2 of 3.

**Hoe wordt Hallo standaard opslagaccount voor diagnostische gegevens instellen?**

Instellen van een persoonlijke opslagaccount voor diagnostische gegevens van virtuele machine. In toekomstige hello, die we zullen tooswitch diagnostics ook tooManaged schijven.

**Wat voor soort toegangsbeheer op basis van rollen ondersteuning is beschikbaar voor schijven beheerd?**

Schijven ondersteunt drie belangrijkste standaardrollen beheerd:

* Eigenaar: Kunnen alles beheren, inclusief toegang
* Inzender: Kunnen alles beheren behalve toegang
* Lezer: Kunnen alles weergeven, maar geen wijzigingen aanbrengen

**Is er een manier die ik kan kopiëren of exporteren van een beheerde schijf tooa persoonlijke storage-account?**

U kunt een alleen-lezen shared access signature URI voor Hallo beheerd schijf en deze gebruiken toocopy Hallo inhoud tooa persoonlijke opslag account of on-premises opslag ophalen.

**Kan ik een kopie van de beheerde computer maken?**

Klanten kunnen een momentopname van het bijbehorende beheerde schijven en gebruik vervolgens Hallo momentopname toocreate een andere beheerde schijf.

**Worden niet-beheerde schijven nog steeds ondersteund?**

Ja. Wij ondersteunen onbeheerde en beheerde schijven. U wordt aangeraden dat u beheerde schijven voor nieuwe werkbelastingen en uw huidige werkbelastingen toomanaged schijven migreren.


**Als ik een schijf van 128 GB maken en vervolgens te Hallo grootte too130 GB verhogen, ik gefactureerd voor volgende schijfgrootte hello (512 GB)?**

Ja.

**Kan ik geografisch redundante opslag met lokaal redundante opslag maken en zone-redundante opslag schijven die worden beheerd?**

Azure-beheerde schijven ondersteunt momenteel alleen lokaal redundante opslag beheerd schijven.

**Kan ik verkleinen of mijn beheerde schijven afslanken?**

Nee. Deze functie is momenteel niet ondersteund. 

**Kan ik Hallo computer name-eigenschap wijzigen wanneer een gespecialiseerde (niet gemaakt met behulp van hulpprogramma voor systeemvoorbereiding Hallo of gegeneraliseerd) systeemschijf besturingssystemen gebruikte tooprovision een virtuele machine zijn?**

Nee. U kunt Hallo computer name-eigenschap niet bijwerken. Hallo neemt nieuwe virtuele machine deze van Hallo bovenliggende virtuele machine gebruikte toocreate hello besturingssysteemschijf is. 

**Waar vind ik voorbeelden Azure Resource Manager-sjablonen toocreate virtuele machines met beheerde-schijven**
* [Lijst met sjablonen met schijven beheerd](https://github.com/Azure/azure-quickstart-templates/blob/master/managed-disk-support-list.md)
* https://github.com/chagarw/MDPP

## <a name="managed-disks-and-storage-service-encryption"></a>Beheerd schijven en versleuteling van opslag-Service 

**Is Azure Storage-Service: versleuteling standaard ingeschakeld wanneer ik een beheerde schijf maken?**

Ja.

**Wie beheert Hallo versleutelingssleutels?**

Microsoft beheert Hallo versleutelingssleutels.

**Kan ik voor mijn beheerde schijven versleuteling van opslag Service uitschakelen?**

Nee.

**Is versleuteling van opslag Service alleen beschikbaar in specifieke gebieden?**

Nee. Het is beschikbaar in alle Hallo regio's waar beheerd schijven beschikbaar is. Beheerde schijven is beschikbaar in alle openbare regio's en Duitsland.

**Hoe vind ik als mijn beheerde schijf worden versleuteld?**

U vindt hier Hallo tijd waarop een beheerde schijf is gemaakt in hello Azure-portal, Azure CLI Hallo en PowerShell. De schijf wordt versleuteld als Hallo tijd na 9 juni 2017. 

**Hoe kan ik mijn bestaande schijven die zijn gemaakt vóór 10 juni 2017 coderen?**

Vanaf 10 juni 2017 nieuwe gegevens geschreven tooexisting beheerd schijven automatisch versleuteld. We zijn ook tooencrypt bestaande gegevens plannen en Hallo versleuteling asynchroon op Hallo achtergrond gebeurt. Als u bestaande gegevens moet nu worden versleuteld, maakt u een kopie van de schijf. Nieuwe schijf wordt versleuteld.

* [Beheerde schijven kopiëren via hello Azure CLI](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-linux-cli-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)
* [Beheerde schijven met behulp van PowerShell kopiëren](https://docs.microsoft.com/en-us/azure/storage/scripts/storage-windows-powershell-sample-copy-managed-disks-to-same-or-different-subscription?toc=%2fcli%2fmodule%2ftoc.json)

**Zijn beheerde momentopnamen en installatiekopieën versleuteld?**

Ja. Alle beheerde momentopnamen en installatiekopieën die zijn gemaakt na 9 juni 2017 worden automatisch versleuteld. 

**Kan ik virtuele machines met niet-beheerde schijven die zich bevinden op opslagaccounts die zijn of zijn eerder versleutelde toomanaged schijven converteren**

Ja

**Een geëxporteerde VHD van een beheerde schijf of een momentopname ook worden versleuteld?**

Nee. Maar als u een VHD-tooan exporteren gecodeerd storage-account van een versleutelde-beheerde schijven of een momentopname en ze zijn versleuteld. 

## <a name="premium-disks-managed-and-unmanaged"></a>Premium-schijven: beheerde en onbeheerde

**Als een virtuele machine gebruikmaakt van een reeks grootte die ondersteuning biedt voor Premium-opslag, zoals een DSv2 kan ik koppelen zowel premium en standard gegevensschijven?** 

Ja.

**Kan ik zowel premium en standard schijven tooa grootte gegevensreeks die biedt geen ondersteuning voor Premium-opslag, zoals D, Dv2, G of F-serie koppelen?**

Nee. U kunt alleen standaard gegevens schijven tooVMs die geen gebruikmaken van een reeks grootte die ondersteuning biedt voor Premium-opslag kunt koppelen.

**Als ik een gegevensschijf premium van een bestaande VHD die 80 GB maken is, hoeveel die kost?**

Een gegevensschijf premium is gemaakt op basis van een VHD 80 GB wordt beschouwd als Hallo beschikbaar zijn voor het volgende premium-schijfgrootte, die een schijf P10. U bent in rekening gebracht volgens toohello P10 schijf prijzen.

**Zijn er transactie kosten toouse Premium-opslag?**

Er is een vaste kosten voor de grootte van elke schijf, dat wordt meegeleverd met specifieke limieten ingerichte op IOPS en doorvoerlimieten. Hallo andere kosten zijn uitgaande bandbreedte en capaciteit van de momentopname, indien van toepassing. Zie voor meer informatie, Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/storage).

**Wat zijn de limieten voor IOPS en doorvoerlimieten die ik van de schijfcache Hallo ophalen kan Hallo?**

Hallo gecombineerde limieten voor cache en lokale SSD voor een reeks DS 4000 IOP's per core en 33 MB per seconde per core. Hallo GS-serie biedt 5000 IOP's per core en 50 MB per seconde per core.

**Is Hallo die lokale SSD ondersteund voor een VM-schijven beheerd?**

Hallo is lokale SSD tijdelijke opslag die is opgenomen in een VM-schijven worden beheerd. Er is geen extra kosten verbonden voor deze tijdelijke opslag. Het is raadzaam dat u niet deze lokale SSD toostore uw toepassingsgegevens gebruiken omdat deze is niet in Azure Blob-opslag permanent.

**Zijn er gevolgen voor hello gebruiken van TRIM op premium-schijven?**

Er is geen gebruik van de toohello nadeel van TRIM op Azure ofwel premium-schijven of standaardschijven.

## <a name="new-disk-sizes-managed-and-unmanaged"></a>Nieuwe schijfgrootten: beheerde en onbeheerde

**Wat is Hallo grootste schijfgrootte voor het besturingssysteem en gegevensschijven ondersteund?**

Hallo partitietype die ondersteuning biedt voor de schijf van een besturingssysteem voor Azure is Hallo hoofdopstartrecord (MBR). Hallo MBR-indeling ondersteunt een schijfgrootte van too2 TB. Hallo maximale grootte aan die Azure biedt ondersteuning voor de schijf van een besturingssysteem is 2 TB. Azure biedt ondersteuning voor maximaal too4 TB voor gegevensschijven. 

**Wat is Hallo grootste blob paginaformaat dat wordt ondersteund?**

Hallo is pagina-blob biedt ondersteuning voor Azure maximumgrootte 8 TB (8.191 GB). Pagina-blobs die groter zijn dan 4 TB (4095 GB) die zijn gekoppeld tooa VM als gegevens of besturingssysteem schijven worden niet ondersteund.

**Moet ik toouse een nieuwe versie van Azure-hulpprogramma's toocreate, toevoegen, vergroten of verkleinen en uploaden schijven groter dan 1 TB?**

U hoeft niet tooupgrade de toocreate van uw bestaande Azure-hulpprogramma's of schijven die groter zijn dan 1 TB vergroten of verkleinen koppelen. tooupload uw VHD-bestand van lokale rechtstreeks tooAzure als een pagina-blob of een niet-beheerde schijf, moet u toouse Hallo nieuwste hulpprogramma's:

|Azure-hulpprogramma 's      | Ondersteunde versies                                |
|-----------------|---------------------------------------------------|
|Azure PowerShell | Versienummer 4.1.0: release van juni 2017 of hoger|
|Azure CLI v1     | Versienummer 0.10.13: mei 2017 release of hoger|
|AzCopy           | Versienummer 6.1.0: release van juni 2017 of hoger|

Hallo-ondersteuning voor Azure CLI v2 en Azure Storage Explorer is binnenkort beschikbaar. 

**Worden P4 en P6 schijfgrootten ondersteund voor niet-beheerde schijven of pagina-blobs?**

Nee. P4 (32 GB) en P6 schijfgrootten (64 GB) worden alleen ondersteund voor beheerde schijven. Ondersteuning voor niet-beheerde schijven en pagina-blobs is binnenkort beschikbaar.

**Als mijn bestaande premium beheerd schijf kleiner is dan 64 GB is gemaakt voordat Hallo kleine schijf (rond 15 juni 2017) is ingeschakeld, hoe wordt deze in rekening gebracht?**

Bestaande kleine premium-schijven bevat die kleiner is dan 64 GB blijven toobe kosten in rekening gebracht volgens toohello P10 prijscategorie. 

**Hoe kan ik Hallo schijf laag van kleine premium-schijven bevat die kleiner is dan 64 GB van P10 tooP4 of P6 overschakelen?**

U kunt een momentopname van de kleine schijven en vervolgens maakt u een schijf tooautomatically switch Hallo prijzen laag tooP4 of P6 op basis van Hallo ingericht grootte. 


## <a name="what-if-my-question-isnt-answered-here"></a>Wat gebeurt er als mijn vraag hier niet wordt beantwoord?

Als uw vraag hier niet is vermeld, laat ons weten en wij helpen u bij een antwoord vinden. U kunt een vraag op Hallo einde van dit artikel boeken in Hallo opmerkingen. tooengage met hello Azure Storage-team en andere communityleden over dit artikel gebruiken Hallo MSDN [Azure Storage-forum](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata).

toorequest functies, dienen de aanvragen en ideeën toohello [forum met feedback van Azure Storage](https://feedback.azure.com/forums/217298-storage).
