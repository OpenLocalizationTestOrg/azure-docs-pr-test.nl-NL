---
title: aaaData replicatie in Azure Storage | Microsoft Docs
description: Gegevens in uw Microsoft Azure Storage-account worden gerepliceerd voor duurzaamheid en hoge beschikbaarheid. Replicatieopties voor zijn lokaal redundante opslag (LRS), zone-redundante opslag (ZRS), geografisch redundante opslag (GRS) en geografisch redundante opslag met leestoegang (RA-GRS).
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 86bdb6d4-da59-4337-8375-2527b6bdf73f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: ce48d1992fec7bd5ed32feb96b86bef88ca759df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-replication"></a>Azure Storage-replicatie

Hallo-gegevens in uw Microsoft Azure storage-account altijd is gerepliceerd tooensure duurzaamheid en maximale beschikbaarheid. Replicatie wordt gekopieerd uw gegevens zich binnen de Hallo hetzelfde Datacenter of tooa tweede Datacenter, afhankelijk van welke replicatieoptie u kiest. Replicatie beschermt u uw gegevens en behoudt uw toepassing beschikbaarheid in Hallo-gebeurtenis van tijdelijke hardwarefouten. Als uw gegevens gerepliceerde tooa tweede Datacenter, het van een onherstelbare fout in de primaire locatie Hallo beveiligd.

Replicatie zorgt ervoor dat uw storage-account voldoet aan Hallo [Service Level Agreement (SLA) voor opslag](https://azure.microsoft.com/support/legal/sla/storage/) zelfs in Hallo face van fouten. Zie Hallo SLA voor informatie over Azure Storage wordt gegarandeerd dat voor duurzaamheid en beschikbaarheid.

Wanneer u een opslagaccount maakt, kunt u een Hallo volgende replicatieopties selecteren:

* [Lokaal redundante opslag (LRS)](#locally-redundant-storage)
* [Zone-redundante opslag (ZRS)](#zone-redundant-storage)
* [Geografisch redundante opslag (GRS)](#geo-redundant-storage)
* [Geografisch redundante opslag met leestoegang (RA-GRS)](#read-access-geo-redundant-storage)

Geografisch redundante opslag met leestoegang (RA-GRS) is de standaardoptie Hallo wanneer u een opslagaccount maken.

Hallo volgende tabel biedt een snel overzicht van Hallo verschillen tussen LRS, ZRS GRS en RA-GRS, terwijl de volgende secties adres elk type replicatie in meer detail.

| Replicatiestrategie | LRS | ZRS | GRS | RA-GRS |
|:--- |:--- |:--- |:--- |:--- |
| Gegevens worden gerepliceerd in meerdere datacenters. |Nee |Ja |Ja |Ja |
| Gegevens kunnen worden gelezen vanaf een secundaire locatie, evenals de Hallo primaire locatie. |Nee |Nee |Nee |Ja |
| Het aantal exemplaren van de gegevens op afzonderlijke knooppunten. |3 |3 |6 |6 |

Zie [prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/) voor prijsinformatie voor Hallo redundantie van andere opties.

> [!NOTE]
> Premium-opslag ondersteunt alleen lokaal redundante opslag (LRS). Zie voor meer informatie over de Premium-opslag [Premium-opslag: krachtige opslag voor Azure Virtual Machine-werkbelasting](../storage-premium-storage.md).
>

## <a name="locally-redundant-storage"></a>Lokaal redundante opslag
Lokaal redundante opslag (LRS) repliceert uw gegevens driemaal binnen een schaaleenheid opslag die wordt gehost in een datacenter in Hallo regio waarin u uw opslagaccount hebt gemaakt. Een schrijfaanvraag retourneert is alleen nadat deze geschreven tooall drie replica's is. Deze drie replica's elke zich bevinden in domeinen met afzonderlijke fouten en upgradedomeinen binnen één opslag schaaleenheid.

Een schaaleenheid storage is een verzameling van rekken opslagknooppunten. Een domein met fouten (FD) is een groep van knooppunten die staan voor een fysieke eenheid van de fout en kunnen worden beschouwd als knooppunten toohello van dezelfde fysieke rack. Een upgradedomein (UD) is een groep van knooppunten die samen zijn bijgewerkt tijdens Hallo van een service-upgrade (implementatie). Hallo drie replica's zijn verdeeld over UDs en FDs binnen één opslag scale unit tooensure dat gegevens beschikbaar is, zelfs als hardwarefout van invloed is op één rack of wanneer knooppunten zijn bijgewerkt tijdens een implementatie.

LRS is de laagste kosten-optie Hallo en biedt minimaal duurzaamheid vergeleken tooother opties. In geval van een datacenter niveau noodgeval (fire, enzovoort. overspoelen) Hallo mogelijk alle drie replica's verloren of onherstelbare. toomitigate dit risico, wordt geografisch redundante opslag (GRS) aanbevolen voor de meeste toepassingen.

Lokaal redundante opslag nog steeds wenselijk in bepaalde scenario's:

* Biedt de hoogste maximale bandbreedte van Azure Storage-replicatieopties.
* Als uw toepassing gegevens die u kunt eenvoudig opnieuw worden samengesteld opgeslagen, kunt u kiezen voor LRS.
* Sommige toepassingen zijn beperkt tooreplicating gegevens alleen binnen een land vanwege toodata beheervereisten. Een gekoppelde gebied kan worden in een ander land. Zie voor meer informatie over regio paren [Azure-regio's](https://azure.microsoft.com/regions/).

## <a name="zone-redundant-storage"></a>Zone-redundante opslag
Zone-redundante opslag (ZRS) worden uw gegevens asynchroon gerepliceerd in datacenters in één of twee gebieden in toevoeging toostoring drie replica's vergelijkbare tooLRS, dus biedt een hogere duurzaamheid dan LRS. Gegevens die zijn opgeslagen in ZRS is duurzame, zelfs als het primaire datacenter Hallo niet beschikbaar of onherstelbare is.
Klanten die van toouse ZRS plan moet rekening houden die:

* ZRS is alleen beschikbaar voor blok-blobs in opslagaccounts voor algemeen gebruik en wordt ondersteund in versies van de service storage 2014-02-14 en hoger.
* Omdat asynchrone replicatie omvat een vertraging in de gebeurtenis Hallo van een lokale ramp is mogelijk dat wijzigingen die nog niet zijn gerepliceerd toohello secundaire niet verloren als Hallo gegevens kunnen niet worden hersteld vanaf primaire Hallo.
* Hallo replica zijn mogelijk niet beschikbaar totdat Microsoft failover toohello secundaire initieert.
* ZRS-accounts kunnen niet worden geconverteerd hoger tooLRS of GRS. Op deze manier een bestaand LRS of GRS-account kan niet worden geconverteerd tooa ZRS-account.
* ZRS accounts geen metrische gegevens of functionaliteit van logboekregistratie.

## <a name="geo-redundant-storage"></a>Geografisch redundante opslag
Geografisch redundante opslag (GRS) uw gegevens tooa secundaire regio die honderden mijl weg Hallo primaire regio worden gerepliceerd. Als uw storage-account GRS ingeschakeld heeft, zijn uw gegevens is duurzame zelfs in Hallo geval van een volledige regionale uitval of een noodsituatie in welke Hallo primaire regio kan niet worden hersteld.

Voor een opslagaccount met GRS ingeschakeld, is een update eerste doorgevoerd toohello primaire regio, waar deze drie keer is gerepliceerd. Vervolgens Hallo-update is asynchroon gerepliceerd toohello secundaire regio, waar deze ook driemaal gerepliceerd.

Met GRS beide Hallo primaire en secundaire regio's replica's in afzonderlijke foutdomeinen beheren en upgrade uitvoeren van domeinen binnen een schaaleenheid opslag zoals beschreven met LRS.

Overwegingen:

* Omdat asynchrone replicatie omvat een vertraging in de gebeurtenis Hallo van een regionale noodgeval die het is mogelijk dat wijzigingen die nog niet is gerepliceerd toohello secundaire regio worden verbroken als Hallo gegevens kunnen niet worden hersteld van de primaire regio Hallo.
* Hallo-replica is niet beschikbaar, tenzij Microsoft failover toohello secundaire regio initieert. Als Microsoft een failover toohello secundaire regio worden gestart, hebt u lees- en schrijftoegang toothat gegevens nadat het Hallo-failover is voltooid. Zie voor meer informatie [Disaster Recovery richtlijnen](../storage-disaster-recovery-guidance.md). 
* Als een toepassing wil tooread van de secundaire regio hello, moet de gebruiker Hallo RA-GRS inschakelen.

Wanneer u een opslagaccount maakt, kunt u de primaire regio Hallo voor Hallo-account selecteren. Hallo secundaire regio wordt bepaald op basis van de primaire regio hello, en kan niet worden gewijzigd. Hallo volgende tabel ziet u Hallo primaire en secundaire regio koppelingen.

| Primair | Secundair |
| --- | --- |
| Noord-centraal VS |Zuid-centraal VS |
| Zuid-centraal VS |Noord-centraal VS |
| VS - oost |VS - west |
| VS - west |VS - oost |
| Verenigde Staten (oost 2) |VS - midden |
| VS - midden |Verenigde Staten (oost 2) |
| Noord-Europa |West-Europa |
| West-Europa |Noord-Europa |
| Zuidoost-Azië |Oost-Azië |
| Oost-Azië |Zuidoost-Azië |
| China - oost |China - noord |
| China - noord |China - oost |
| Japan - oost |Japan - west |
| Japan - west |Japan - oost |
| Brazilië - zuid |Zuid-centraal VS |
| Australië - oost |Australië - zuidoost |
| Australië - zuidoost |Australië - oost |
| India - zuid |India - midden |
| India - midden |India - zuid |
| India - west |India - zuid |
| VS (overheid) - Iowa |VS (overheid) - Virginia |
| VS (overheid) - Virginia |VS (overheid) - Texas |
| VS (overheid) - Texas |VS (overheid) - Arizona |
| VS (overheid) - Arizona |VS (overheid) - Texas |
| Canada - midden |Canada - oost |
| Canada - oost |Canada - midden |
| Verenigd Koninkrijk West |Verenigd Koninkrijk Zuid |
| Verenigd Koninkrijk Zuid |Verenigd Koninkrijk West |
| Duitsland - centraal |Duitsland - noordoost |
| Duitsland - noordoost |Duitsland - centraal |
| VS - west 2 |West-centraal VS |
| West-centraal VS |VS - west 2 |

Zie voor actuele informatie over regio's die worden ondersteund door Azure [Azure-regio's](https://azure.microsoft.com/regions/).

>[!NOTE]  
> VS Gov Virginia secundaire regio is Gov ons Texas. Voorheen gebruikt Gov ons Virginia Gov ons Iowa als een secundaire regio. TooUS Gov Texas opslagaccounts nog Gov ons Iowa als een secundaire regio worden gemigreerd als een secundaire regio. 
> 
> 

## <a name="read-access-geo-redundant-storage"></a>Geografisch redundante opslag met leestoegang
Geografisch redundante opslag met leestoegang (RA-GRS) maximaliseert de beschikbaarheid voor uw opslagaccount alleen-lezentoegang toohello door gegevens te verstrekken op de secundaire locatie hello, Daarnaast toohello replicatie tussen twee regio's worden geleverd door GRS.

Wanneer u alleen-lezentoegang tooyour gegevens in de secundaire regio Hallo inschakelt, is uw gegevens is beschikbaar op een secundair eindpunt in toevoeging toohello primaire eindpunt voor uw opslagaccount. secundair eindpunt Hallo vergelijkbare toohello primaire eindpunt is, maar voegt Hallo achtervoegsel `–secondary` toohello accountnaam. Bijvoorbeeld, als uw primaire eindpunt voor Blob-service Hallo is `myaccount.blob.core.windows.net`, dan is uw secundaire eindpunt `myaccount-secondary.blob.core.windows.net`. Hallo toegangssleutels voor uw opslagaccount worden Hallo dezelfde voor zowel de primaire en secundaire eindpunten Hallo.

Overwegingen:

* Uw toepassing heeft toomanage welk eindpunt het interactie is met bij gebruik van RA-GRS.
* Omdat asynchrone replicatie omvat een vertraging in de gebeurtenis Hallo van een regionale noodgeval die het is mogelijk dat wijzigingen die nog niet is gerepliceerd toohello secundaire regio worden verbroken als Hallo gegevens kunnen niet worden hersteld van de primaire regio Hallo.
* Als Microsoft failover toohello secundaire regio initieert, hebt u lees- en schrijftoegang toothat gegevens nadat het Hallo-failover is voltooid. Zie voor meer informatie [Disaster Recovery richtlijnen](../storage-disaster-recovery-guidance.md). 
* RA-GRS is bedoeld voor hoge beschikbaarheid. Bekijk Hallo voor richtlijnen voor schaalbaarheid, [prestaties controlelijst](../storage-performance-checklist.md).

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

<a id="howtochange"></a>
#### <a name="1-how-can-i-change-hello-geo-replication-type-of-my-storage-account"></a>1. Hoe kan ik type voor de Hallo geo-replicatie van mijn storage-account wijzigen?

   Kunt u type voor de Hallo geo-replicatie van uw opslagaccount tussen LRS, GRS, wijzigen en RA-GRS met Hallo [Azure-portal](https://portal.azure.com/), [Azure Powershell](storage-powershell-guide-full.md) of programmatisch met behulp van een van onze Client-veel-opslag Bibliotheken. Houd er rekening mee dat ZRS accounts niet geconverteerd LRS of GRS worden. Op deze manier een bestaand LRS of GRS-account kan niet worden geconverteerd tooa ZRS-account.

<a id="changedowntime"></a>
#### <a name="2-will-there-be-any-down-time-if-i-change-hello-replication-type-of-my-storage-account"></a>2. Er zijn uitvaltijd als ik Hallo replicatietype van mijn storage-account wijzigen?

   Nee, er niet een uitvaltijd.

<a id="changecost"></a>
#### <a name="3-will-there-be-any-additional-cost-if-i-change-hello-replication-type-of-my-storage-account"></a>3. Er worden extra kosten als ik Hallo replicatietype van mijn storage-account wijzigen?

   Ja. Als u van LRS tooGRS (of RA-GRS) voor uw opslagaccount wijzigt, zou het zijn dat hiervoor extra kosten voor uitgaande gegevens die zijn betrokken bij het kopiëren van bestaande gegevens van de primaire locatie toohello secundaire locatie. Zodra het Hallo initiële gegevens worden gekopieerd is geen verdere extra uitgaande gratis voor geo Hallo gegevens van Hallo primaire toosecondary locatie te repliceren. Hallo-details voor de bandbreedte kosten vindt u op Hallo [prijzen van Azure-opslag-pagina](https://azure.microsoft.com/pricing/details/storage/blobs/). Als u van GRS tooLRS wijzigt, is er geen extra kosten, maar de gegevens worden verwijderd van de secundaire locatie Hallo.

<a id="ragrsbenefits"></a>
#### <a name="4-how-can-ra-grs-help-me"></a>4. Hoe kunt RA-GRS mij?
   
   GRS storage biedt replicatie van uw gegevens van een primaire tooa secundaire regio die honderden mijl weg Hallo primaire regio. In dit geval is is uw gegevens duurzaam zelfs in Hallo geval van een volledige regionale uitval of een noodsituatie in welke Hallo primaire regio kan niet worden hersteld. RA-GRS opslag bevat dit plus Hallo mogelijkheid tooread Hallo gegevens vanaf de secundaire locatie hello wordt toegevoegd. Voor enkele ideeën over het tooleverage deze mogelijkheid te Zie[ontwerpen van maximaal beschikbare toepassingen RA-GRS opslag](../storage-designing-ha-apps-with-ragrs.md). 

<a id="lastsynctime"></a>
#### <a name="5-is-there-a-way-for-me-toofigure-out-how-long-it-takes-tooreplicate-my-data-from-hello-primary-toohello-secondary-region"></a>5. Is er een manier voor mij toofigure uit hoe lang het duurt tooreplicate mijn gegevens uit Hallo primaire toohello secundaire regio?
   
   Als u RA-GRS opslag gebruikt, kunt u controleren Hallo tijd van laatste synchronisatie van uw opslagaccount. Tijd van laatste synchronisatie is een GMT datum/tijd-waarde; alle primaire schrijfbewerkingen voordat Hallo tijd van laatste synchronisatie hebt geschreven toohello secundaire locatie, dat wil zeggen dat ze beschikbaar toobe lezen vanaf de secundaire locatie Hallo zijn. Primaire schrijft na Hallo tijd van laatste synchronisatie al dan niet meer beschikbaar zijn voor leesbewerkingen nog. U kunt deze waarde Hallo query [Azure-portal](https://portal.azure.com/), [Azure PowerShell](storage-powershell-guide-full.md), of programmatisch met behulp van Hallo REST-API of een van de Hallo clientbibliotheken Storage. 

<a id="outage"></a>
#### <a name="6-how-can-i-switch-toohello-secondary-region-if-there-is-an-outage-in-hello-primary-region"></a>6. Hoe kan ik de secundaire regio toohello overschakelen als er een storing in de primaire regio Hallo?
   
   Raadpleeg het artikel toohello [welke toodo als een Azure Storage-storing optreedt,](../storage-disaster-recovery-guidance.md) voor meer informatie.

<a id="rpo-rto"></a>
#### <a name="7-what-is-hello-rpo-and-rto-with-grs"></a>7. Wat is Hallo RPO en RTO met GRS?
   
   Herstellen Point Objective (RPO): In GRS en RA-GRS Hallo storage-service is asynchroon geo repliceren Hallo gegevens van Hallo primaire toohello secundaire locatie. Als er een noodgeval regionale en een failover uitgevoerd toobe is, vervolgens recente wijzigingen die niet geogerepliceerde zijn mogelijk verloren gegaan. het aantal minuten mogelijk gegevens verloren gegaan Hallo is waarnaar wordt verwezen tooas hello RPO (wat betekent dat Hallo punt in tijd toowhich gegevens kan worden hersteld). We hebben doorgaans een RPO minder dan 15 minuten, maar er is momenteel geen SLA op hoe lang geo-replicatie neemt.

   Beoogde hersteltijd (RTO) uitgevoerd: Dit is een meting van hoe lang het duurt toodo Hallo failover en terughalen Hallo storage-account online als we toodo een failover. Hallo tijd toodo Hallo failover bevat Hallo volgende:
    * Hallo tijd het duurt tooinvestigate en bepalen of we Hallo data-at-Hallo primaire locatie kunt herstellen of als we toodo een failover moet.
    * Failover Hallo account door Hallo primaire DNS-vermeldingen toopoint toohello secundaire locatie te wijzigen.

   We nemen Hallo verantwoordelijkheid van het behouden van uw gegevens zeer ernstig, dus als er een kans op Hallo-gegevens herstellen, wordt houdt uitschakelen Hallo failover doen en zich richten op het herstellen van gegevens op de primaire locatie Hallo Hallo. In toekomstige hello, we tooprovide een API tooallow plant u tootrigger een failover op accountniveau, die vervolgens kunt u toocontrol Hallo RTO zelf, maar dit is nog niet beschikbaar.
   
## <a name="next-steps"></a>Volgende stappen
* [Maximaal beschikbare toepassingen die gebruikmaken van RA-GRS opslag ontwerpen](../storage-designing-ha-apps-with-ragrs.md)
* [Prijzen voor Azure Storage](https://azure.microsoft.com/pricing/details/storage/)
* [Over Azure storage-accounts](../storage-create-storage-account.md)
* [Azure Storage schaalbaarheids- en prestatiedoelen](storage-scalability-targets.md)
* [Microsoft Azure Storage redundantie opties en leestoegang geografisch redundante opslag](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx)
* [SOSP-document - Azure Storage: Een maximaal beschikbare cloudopslagservice met sterke consistentie](http://blogs.msdn.com/b/windowsazurestorage/archive/2011/11/20/windows-azure-storage-a-highly-available-cloud-storage-service-with-strong-consistency.aspx)

