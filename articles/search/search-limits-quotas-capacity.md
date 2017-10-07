---
title: aaaService limieten in Azure Search | Microsoft Docs
description: Servicelimieten gebruikt voor het plannen van capaciteit en bovengrenzen voor aanvragen en antwoorden voor Azure Search.
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: azure-portal
ms.assetid: 857a8606-c1bf-48f1-8758-8032bbe220ad
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/07/2017
ms.author: heidist
ms.openlocfilehash: cb13a0f1c87a654fb5845c9c741f74a91da5b372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-limits-in-azure-search"></a>Servicelimieten in Azure Search
Maximum beperkt op opslag, workloads en aantallen van indexen, documenten en andere objecten afhankelijk zijn van of u [inrichten van Azure Search](search-create-service-portal.md) op een **vrije**, **Basic**, of **standaard** prijscategorie.

* **Gratis** is een gedeelde multitenant-service die wordt geleverd met uw Azure-abonnement. Het is een optie geen extra kosten voor bestaande abonnees waarmee u tooexperiment met Hallo service voordat u zich aanmeldt voor toegewezen bronnen.
* **Basic** biedt speciale computerbronnen voor productieworkloads op kleinere schaal.
* **Standaard** wordt uitgevoerd op specifieke machines, met een grotere opslag en verwerking capaciteit op elk niveau. Standaard wordt geleverd in vier niveaus: S1, S2, S3 en S3 High-Density (S3 HD).

> [!NOTE]
> Een service is ingericht op een bepaalde laag. Als u toojump lagen tooget meer capaciteit, moet u een nieuwe service (Er is geen in-place upgrade) inrichten. Zie voor meer informatie [Kies een SKU of laag](search-sku-tier.md). toolearn meer over het aanpassen van de capaciteit binnen een service die u al hebt ingericht, Zie [schalen niveaus van de bron voor query's en workloads indexering](search-capacity-planning.md).
>

## <a name="per-subscription-limits"></a>Per abonnement limieten
[!INCLUDE [azure-search-limits-per-subscription](../../includes/azure-search-limits-per-subscription.md)]

## <a name="per-service-limits"></a>Limieten per service
[!INCLUDE [azure-search-limits-per-service](../../includes/azure-search-limits-per-service.md)]

## <a name="per-index-limits"></a>Per index limieten
Er is een-op-een overeenkomst tussen beperkingen met betrekking tot indexen en beperkingen met betrekking tot indexeerfuncties. Gezien een limiet van 200 indexen, Hallo maximale limiet voor indexeerfuncties is ook 200 voor Hallo dezelfde service.

| Resource | Gratis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Index: maximum aantal velden van per index |1000 |100 <sup>1</sup> |1000 |1000 |1000 |1000 |
| Index: maximum score berekenen voor profielen per index |100 |100 |100 |100 |100 |100 |
| Index: maximale functies per profiel |8 |8 |8 |8 |8 |8 |
| Indexeerfuncties: maximale indexering belasting per aanroep |10.000 documenten |Alleen beperkt door het maximum aantal documenten |Alleen beperkt door het maximum aantal documenten |Alleen beperkt door het maximum aantal documenten |Alleen beperkt door het maximum aantal documenten |N.V.T. <sup>2</sup> |
| Indexeerfuncties: de maximale uitvoeringstijd | 1-3 minuten <sup>3</sup> |24 uur |24 uur |24 uur |24 uur |N.V.T. <sup>2</sup> |
| BLOB-indexeerfunctie: maximale blobgrootte, MB |16 |16 |128 |256 |256 |N.V.T. <sup>2</sup> |
| BLOB-indexeerfunctie: maximum aantal tekens inhoud opgehaald uit een blob |32,000 |64,000 |4 miljoen |4 miljoen |4 miljoen |N.V.T. <sup>2</sup> |

<sup>1</sup> basisstaffel is Hallo alleen SKU met een lagere limiet van 100 velden per index.

<sup>2</sup> S3 HD ondersteunt momenteel geen indexeerfuncties. Neem contact op met ondersteuning van Azure als u deze mogelijkheid dringend behoefte hebt.

<sup>3</sup> indexeerfunctie maximale uitvoeringstijd voor de gratis laag Hallo is 3 minuten voor blob-bronnen en 1 minuut voor andere gegevensbronnen.

## <a name="document-size-limits"></a>De maximale grootte document
| Resource | Gratis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| Grootte van afzonderlijke document per Index API |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |< 16 MB |

Grootte van de maximale document toohello verwijst bij het aanroepen van een API-Index. De documentgrootte van het is daadwerkelijk een limiet op Hallo grootte van Hallo aanvraagtekst Index API. Omdat u een batch met meerdere documenten toohello Index API in één keer doorgeven kunt, afhankelijk Hallo groottelimiet daadwerkelijk van hoeveel documenten in Hallo batch zijn. Hallo document maximale grootte is voor een batch met één document 16 MB van JSON.

grootte voor het document af tookeep onthouden tooexclude niet waarop gegevens van Hallo-aanvraag. Afbeeldingen en andere binaire gegevens zijn niet rechtstreeks waarop en mag niet worden opgeslagen in het Hallo-index. niet-waarop gegevens in de lijst met zoekresultaten toointegrate definiëren een niet-doorzoekbare veld waarin een URL-verwijzing toohello bron opgeslagen.

## <a name="workload-limits-queries-per-second"></a>Werkbelasting beperkt (query's per seconde)
| Resource | Gratis | Basic | S1 | S2 | S3 | S3 HD |
| --- | --- | --- | --- | --- | --- | --- |
| QPS |N.v.t. |~3 per replica |~15 per replica |~60 per replica |>60 per replica |>60 per replica |

Query's per seconde (QPS) is een schatting op basis van methodiek, met behulp van de klant gesimuleerde en de daadwerkelijke werkbelastingen tooderive geschatte waarden. Exacte doorvoer van QPS varieert afhankelijk van uw gegevens en Hallo aard van Hallo-query.

Hoewel ruwe schattingen hierboven zijn opgegeven, is een werkelijke tempo moeilijk toodetermine, met name in Hallo die vrije gedeelde waar doorvoer is gebaseerd op beschikbare bandbreedte en concurrentie voor systeemresources-service. In Hallo gratis laag, reken-en opslagbronnen worden gedeeld door meerdere abonnees, dus QPS voor uw oplossing altijd variëren wordt afhankelijk van hoeveel andere werkbelastingen worden uitgevoerd op Hallo hetzelfde moment.

Op Hallo standaard niveau, kunt u schatten QPS meer nauw omdat u controle over meer Hallo parameters hebben. Zie Hallo best practices sectie in [beheren van uw zoekoplossing](search-manage.md) voor instructies voor het toocalculate QPS voor uw werkbelastingen.

## <a name="api-request-limits"></a>Limieten voor API-aanvraag
* Maximum van 16 MB per aanvraag <sup>1</sup>
* Maximale URL-lengte van 8 KB
* Maximaal 1000 documenten per batch van index uploadt, worden samengevoegd of verwijderd
* Maximaal 32 velden in de component $orderby
* Maximale zoeken Termgrootte is 32.766 bytes (32 KB min 2-bytes) van UTF-8-gecodeerde tekst

<sup>1</sup> in Azure Search Hallo hoofdcode van een aanvraag is onderwerp tooan bovengrens van 16 MB, om een limiet van Hallo inhoud van afzonderlijke velden of verzamelingen die anders niet worden beperkt door theoretische limieten te leggen (Zie [ondersteund gegevenstypen](https://msdn.microsoft.com/library/azure/dn798938.aspx) voor meer informatie over het veld samenstelling en beperkingen).

## <a name="api-response-limits"></a>API-reactie limieten
* Maximaal 1000 documenten die worden geretourneerd per pagina met zoekresultaten
* Maximaal 100 suggesties heeft geretourneerd per voorstellen API-aanvraag

## <a name="api-key-limits"></a>Limieten voor API-sleutel
API-sleutels worden gebruikt voor verificatie van de service. Er zijn twee typen. Administratorsleutels zijn opgegeven in de aanvraagheader Hallo en lees-schrijfrechten hebben toohello service te verlenen. Querysleutels zijn alleen-lezen, op Hallo-URL en de tooclient doorgaans gedistribueerde toepassingen.

* Maximaal 2 administratorsleutels per service
* Maximum van 50 querysleutels per service
