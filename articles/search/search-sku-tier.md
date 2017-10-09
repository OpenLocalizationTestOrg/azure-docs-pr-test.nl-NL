---
title: aaaChoose een SKU of prijscategorie voor Azure Search | Microsoft Docs
description: 'Azure Search kan worden ingericht op deze SKU''s: gratis, basis en standaard, waarbij standaard is beschikbaar in verschillende configuraties van resources en capaciteit niveaus.'
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 8d4b7bca-02a5-43ee-b3f8-03551dfb32fd
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/24/2016
ms.author: heidist
ms.openlocfilehash: eac9a09266db9da4900766808be3bc3b3ff11519
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="choose-a-sku-or-pricing-tier-for-azure-search"></a>Kies een SKU of prijscategorie voor Azure Search
In Azure Search een [service is ingericht](search-create-service-portal.md) op een specifieke prijscategorie of SKU. Opties zijn onder andere **vrije**, **Basic**, of **standaard**, waarbij **standaard** is beschikbaar in meerdere configuraties en capaciteit.

Hallo-doel van dit artikel is toohelp kiezen van een laag. Als een laag capaciteit toobe te laag blijkt, u moet een nieuwe service op Hallo hogere lagen tooprovision en vervolgens de indexen opnieuw te laden. Er is geen in-place upgrade van dezelfde service van een SKU tooanother Hallo.

> [!NOTE]
> Nadat u een laag kiezen en [inrichten van een zoekservice](search-create-service-portal.md), kunt u de replica verhogen en partitie telt binnen Hallo-service. Zie voor instructies [schalen niveaus van de bron voor query's en workloads indexering](search-capacity-planning.md).
>
>

## <a name="how-tooapproach-a-pricing-tier-decision"></a>Hoe een prijzen tooapproach besluit laag
In Azure Search bepaalt Hallo laag niet functiebeschikbaarheid capaciteit. In het algemeen zijn functies beschikbaar op elke laag, met inbegrip van de preview-functies. Hallo één uitzondering is geen ondersteuning voor indexeerfuncties in S3 HD.

> [!TIP]
> Het is raadzaam dat u altijd inrichten een **vrije** service (één per abonnement zonder vervaldatum) zodat de direct beschikbaar voor lichte projecten. Gebruik Hallo **vrije** service voor testen en evalueren; een tweede factureerbare service maken op Hallo **Basic** of **standaard** -laag voor de productie of groter testwerkbelastingen.
>
>

Ga hand voorhanden capaciteit en de kosten van het Hallo-service uitvoeren. De informatie in dit artikel kunt u bepalen welke SKU levert de juiste balans hello, maar voor deze toobe handig is, moet u ten minste ruwe schattingen op Hallo volgende:

* Aantal en de grootte van indexen u van plan bent toocreate
* Aantal en de grootte van documenten tooupload
* Een idee van de query-volume, in termen van query's Per tweede (QPS)

Aantal en de grootte zijn belangrijk omdat de maximale limiet wordt bereikt door middel van een vaste limiet op Hallo aantal indexen of documenten in een service of op resources (opslag of replica's) die worden gebruikt door Hallo-service. Hallo werkelijke limiet voor uw service is afhankelijk van wat eerst wordt gebruikt: bronnen of objecten.

Schattingen in hand moet Hallo stappen te volgen vereenvoudigen Hallo:

* **Stap 1** Hallo SKU beschrijvingen hieronder toolearn over de beschikbare opties bekijken.
* **Stap 2** Hallo vragen hieronder tooarrive op een voorlopige beslissing beantwoorden.
* **Stap 3** uw beslissing voltooien door de vaste limieten op opslag controleren en prijzen.

## <a name="sku-descriptions"></a>Beschrijvingen van de SKU
Hallo volgende tabel bevat beschrijvingen van elke laag.

| Laag | Primaire scenario's |
| --- | --- |
| **Gratis** |Een gedeelde service, zonder kosten, gebruikt voor de evaluatie, onderzoek of kleine werkbelastingen. Omdat deze wordt gedeeld met andere abonnees, varieert query-doorvoer en indexeren op basis van wie Hallo-service wordt gebruikt. Capaciteit is klein (50 MB of 3 indexen met van 10.000 documenten elk). |
| **Basic** |Kleine productieworkloads op specifieke hardware. Maximaal beschikbaar. Capaciteit is maximaal too3 replica's en 1 partitie (2 GB). |
| **S1** |Standaard 1 ondersteunt flexibele combinaties van partities (12) en replica's (12) gebruikt voor gemiddeld productieworkloads op specifieke hardware. U kunt partities en replica's in de combinaties die worden ondersteund door het maximale aantal 36 factureerbare search-eenheden toewijzen. Partities zijn 25 GB en QPS is ongeveer 15 query's per seconde op dit niveau. |
| **S2** |Standaard 2 wordt uitgevoerd groter productieworkloads Hallo dezelfde 36 search-eenheden gebruiken als S1, maar met grotere grootte partities en replica's. Partities zijn 100 GB en QPS is ongeveer 60 query's per seconde op dit niveau. |
| **S3** |Standaard 3 wordt uitgevoerd proportioneel groter productieworkloads op hogere end-systemen in de configuratie van too12 partities of 12 replica's onder 36 search-eenheden. Partities zijn 200 GB en QPS is meer dan 60 query's per seconde op dit niveau. |
| **HD S3** |Standaard 3 high-density is ontworpen voor een groot aantal kleinere indexen. U kunt hebben up too3 partities van 200 GB. QPS is meer dan 60 query's per seconde. |

> [!NOTE]
> Replica- en partitie maximumwaarden wordt gefactureerd uit als de search-eenheden (36 maximale per service eenheid), die legt een effectieve ondergrens dan wat maximaal Hallo impliceert op face-waarde. U kunt maximaal 3 partities hebben bijvoorbeeld toouse Hallo maximaal 12 replica's (12 * 3 = 36 units). Op deze manier verminderen toouse maximale partities too3 replica's. Zie [schalen niveaus van de bron voor query's en workloads in Azure Search indexeren](search-capacity-planning.md) voor een grafiek van toegestane combinaties.
>
>

## <a name="review-limits-per-tier"></a>Limieten per laag controleren
Hallo volgende grafiek is een subset van Hallo limieten van [Servicelimieten in Azure Search](search-limits-quotas-capacity.md). Geeft het Hallo factoren meest waarschijnlijke tooimpact een beslissing SKU. Bij het controleren van de onderstaande Hallo vragen, kunt u toothis grafiek verwijzen.

| Resource | Gratis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Service Level Agreement (SLA) |Nee <sup>1</sup> |Ja |Ja |Ja |Ja |Ja |
| Limieten voor index |3 |5 |50 |200 |200 |1000 <sup>2</sup> |
| Document limieten |10.000 in totaal |1 miljoen per service |15 miljoen per partitie |60 miljoen per partitie |120 miljoen per partitie |1 miljoen per index |
| Maximum aantal partities |N.v.t. |1 |12 |12 |12 |3 <sup>2</sup> |
| Partitiegrootte |Totaal aantal 50 MB |2 GB per service |25 GB per partitie |100 GB per partitie (omhoog tooa maximaal 1,2 TB per service) |200 GB per partitie (omhoog tooa maximaal 2,4 TB per service) |200 GB (omhoog tooa maximaal 600 GB per service) |
| Maximum aantal replica 's |N.v.t. |3 |12 |12 |12 |12 |
| Query's per seconde |N.v.t. |~3 per replica |~15 per replica |~60 per replica |>60 per replica |>60 per replica |

<sup>1</sup> gratis laag en de preview-functies niet bij service level agreements (Sla's) worden geleverd. Voor alle factureerbare lagen, sla's van kracht als u voldoende redundantie voor uw service inricht. Twee of meer replica's zijn vereist voor de SLA voor query (gelezen). Drie of meer replica's zijn vereist voor query's en indexering SLA (lezen / schrijven). het aantal partities Hallo is niet een SLA-overweging. 

<sup>2</sup> S3 en S3 HD worden ondersteund door de infrastructuur van identieke hoge capaciteit, maar elk ervan de maximale limiet bereikt die op verschillende manieren. S3 gericht op een kleiner aantal zeer grote indexen. Als zodanig de resource afhankelijk is van de maximumlimiet (2,4 TB voor elke service). S3 HD is bedoeld voor een groot aantal kleine indexen. S3 HD bereikt 1000 indexen, de grenzen in Hallo vorm van indexbeperkingen. Als u een klant S3 HD die meer dan 1000 indexen nodig heeft, contact op met Microsoft Support voor meer informatie over tooproceed.

## <a name="eliminate-skus-that-dont-meet-requirements"></a>Elimineren SKU's die niet voldoen aan vereisten
Hallo volgende vragen kunt u op de juiste SKU beslissing voor uw workload Hallo binnenkomen.

1. Hebt u **Service Level Agreement (SLA)** vereisten? U kunt elke categorie factureerbare (basis op up), maar u moet de service voor de redundantie configureren. Twee of meer replica's zijn vereist voor de SLA voor query (gelezen). Drie of meer replica's zijn vereist voor query's en indexering SLA (lezen / schrijven). het aantal partities Hallo is niet een SLA-overweging.
2. **Hoeveel indexeert** hebben die u nodig? Een van de grootste variabelen Hallo waarbij in een beslissing SKU is Hallo aantal indexen die worden ondersteund door elke SKU. Ondersteuning van de index wordt weergegeven op aanzienlijk verschillen niveaus in de onderste Hallo Prijscategorieën. Vereisten voor het aantal indexen kunnen een primaire factor van een beslissing SKU worden.
3. **Het aantal documenten** worden geladen in elke index? Hallo aantal en de grootte van documenten Hallo uiteindelijke grootte van Hallo index bepaalt. Ervan uitgaande dat u kunt schatten Hallo verwachte grootte van Hallo index, kunt u dit nummer tegen Hallo partitiegrootte per SKU, uitgebreid door het aantal partities vereist toostore Hallo een index van deze grootte vergelijken.
4. **Wat is de belasting van de query verwacht Hallo**? U kunt query werkbelastingen zodra opslagvereisten worden begrepen. S2 en beide S3-SKU's bieden bijna-equivalente doorvoer, maar SLA vereisten zal sprake is van een preview-SKU's.
5. Als u Hallo S2 of S3-laag overweegt, moet u bepalen of u nodig [indexeerfuncties](search-indexer-overview.md). Indexeerfuncties zijn nog niet beschikbaar voor Hallo S3 HD laag. Alternatieve methode is toouse een pushmodel voor index-updates, waarin u toepassing code toopush een gegevensset tooan index schrijven.

De meeste klanten kunnen een specifieke SKU in- of regel op basis van hun toohello antwoorden hierboven vragen. Als u niet zeker weet welke toogo SKU met, kunt u vragen tooMSDN of StackOverflow forums plaatsen, of neem contact op met de Azure-ondersteuning voor verdere informatie.

## <a name="decision-validation-does-hello-sku-offer-sufficient-storage-and-qps"></a>Validatie beschikking: Hallo SKU biedt voldoende opslagruimte en QPS?
Als laatste stap bezoekt Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/search/) en Hallo [per-service en per index secties in Servicelimieten](search-limits-quotas-capacity.md) toodouble selectievakje uw maakt een schatting op basis van limieten voor het abonnement en de service.

Als de vereisten van beide Hallo prijs of opslag buiten het bereik, kunt u toorefactor Hallo werkbelastingen tussen meerdere kleinere services (bijvoorbeeld). Kan u indexen toobe kleinere herontwerp op meer gedetailleerd niveau of gebruik toomake query's efficiënter filtert.

> [!NOTE]
> Vereisten voor opslag kunnen worden te veel hoge als documenten overbodige gegevens bevatten. In het ideale geval bevatten documenten alleen doorzoekbare gegevens of metagegevens. Binaire gegevens is niet-doorzoekbare en moet worden opgeslagen afzonderlijk (mogelijk in een Azure table of blob-opslag) met een veld in Hallo index toohold een URL toohello externe referentiegegevens. Hallo maximale grootte van een afzonderlijk document is 16 MB (of minder als u bulksgewijs meerdere documenten in één aanvraag uploaden zijn). Zie [Servicelimieten in Azure Search](search-limits-quotas-capacity.md) voor meer informatie.
>
>

## <a name="next-step"></a>Volgende stap
Als u welk SKU is Hallo rechts passen weet, kunt u verder met deze stappen:

* [Maken van een service voor zoeken in Hallo-portal](search-create-service-portal.md)
* [Hallo-toewijzing van partities en replica's tooscale uw service wijzigen](search-capacity-planning.md)
