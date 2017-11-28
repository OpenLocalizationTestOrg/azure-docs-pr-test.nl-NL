---
title: een Azure Search-index aaaCreate | Microsoft Azure | Gehoste cloud search-service
description: Wat is een index in Azure Search en hoe wordt deze gebruikt?
services: search
documentationcenter: 
author: ashmaka
ms.assetid: a395e166-bf2e-4fca-8bfc-116a46c5f7b1
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 12/08/2016
ms.author: ashmaka
ms.openlocfilehash: c01cc654ff91427c8f1569b2f5b060a0a0f044c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index"></a>Een Azure Search-index maken
> [!div class="op_single_selector"]
> * [Overzicht](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

## <a name="what-is-an-index"></a>Wat is een index?
Een *index* is een permanente opslag van *documenten* en andere constructies die worden gebruikt door een Azure Search-service. Een document is een eenheid die bestaat uit gegevens die kunnen worden doorzocht in uw index. Een e-commercedetailhandel heeft bijvoorbeeld een document voor elk item dat wordt verkocht, een nieuwsbureau heeft een document voor elk artikel, enzovoort. Deze begrippen toomore bekend database-equivalenten toewijzen: een *index* is gelijksoortige tooa *tabel*, en *documenten* grofweg gelijk te zijn*rijen* in een tabel.

Wanneer u documenten toevoegt of uploadt en verzenden zoeken query's tooAzure zoeken, dient u uw aanvragen tooa specifieke index in uw zoekservice.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Veldtypen en kenmerken in een Azure Search-index
Als u uw schema definiëren, moet u Hallo-naam, type en kenmerken van elk veld in de index. Hallo veldtype classificeert Hallo-gegevens die zijn opgeslagen in dat veld. Kenmerken worden ingesteld op afzonderlijke velden toospecify hoe Hallo veld wordt gebruikt. Hallo volgende tabellen bevatten Hallo typen en kenmerken die u kunt opgeven.

### <a name="field-types"></a>Veldtypen
| Type | Beschrijving |
| --- | --- |
| *Edm.String* |Tekst die van tokens kan worden voorzien om te zoeken in de volledige tekst (woordafbreking, afleiding, enzovoort). |
| *Collection(Edm.String)* |Een lijst met tekenreeksen die van tokens kan worden voorzien om te zoeken in de volledige tekst. Er is geen theoretische bovengrens op Hallo aantal items in een verzameling, maar Hallo 16 MB bovengrens voor de nettolading van toepassing toocollections. |
| *Edm.Boolean* |Bevat de waarden waar/niet waar. |
| *Edm.Int32* |32-bits waarden van een heel getal. |
| *Edm.Int64* |64-bits waarden van een heel getal. |
| *Edm.Double* |Numerieke gegevens met dubbele precisie. |
| *Edm.DateTimeOffset* |Datum tijdwaarden die worden weergegeven in Hallo OData-V4-indeling (bijvoorbeeld `yyyy-MM-ddTHH:mm:ss.fffZ` of `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`). |
| *Edm.GeographyPoint* |Een punt voor een geografische locatie op Hallo wereld. |

Gedetailleerdere informatie over ondersteunde Azure-Search[-gegevenstypen vindt u hier](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Veldkenmerken
| Kenmerk | Beschrijving |
| --- | --- |
| *Sleutel* |Een tekenreeks waarmee Hallo unieke ID van elk document, dat wordt gebruikt om op te zoeken. Elke index moet een sleutel hebben. Slechts één veld kan Hallo-sleutel en het type tooEdm.String moet worden ingesteld. |
| *Ophalen mogelijk* |Hiermee geeft u op of een veld in een zoekresultaat kan worden geretourneerd. |
| *Filterbaar* |Hiermee kunt Hallo veld toobe gebruikt in een filterquery's. |
| *Sorteerbaar* |Hiermee kan een query toosort zoekresultaten wilt weergeven met behulp van dit veld. |
| *Facetten mogelijk* |Hiermee kunt u een veld toobe gebruikt in een [facetnavigatie](search-faceted-navigation.md) structuur voor de gebruiker te filteren. Doorgaans velden met terugkerende waarden waarmee u toogroup kunt samen met meerdere documenten (bijvoorbeeld meerdere documenten die onder een bepaalde merk- of servicecategorie vallen) werken het beste als facetten. |
| *Doorzoekbaar* |Aanhalingstekens Hallo veld doorzoekbare voor volledige tekst. |

Gedetailleerdere informatie over ondersteunde Azure-Search[-indexkenmerken vindt u hier](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Richtlijnen voor het definiëren van een indexschema
Bij het ontwerpen van uw index, moet u de tijd nemen in Hallo fase toothink elke beslissing plannen. Het is belangrijk dat u uw zoekopdracht gebruiker ervaring en zakelijke behoeften rekening houden bij het ontwerpen van uw index als elk veld Hallo moet worden toegewezen [juiste kenmerken](https://docs.microsoft.com/rest/api/searchservice/Create-Index). Een index wijzigen nadat deze is geïmplementeerd omvat het opnieuw opbouwen en laden Hallo-gegevens.

Als u de vereisten voor gegevensopslag wilt wijzigen, kunt u de capaciteit vergroten of verkleinen door partities toe te voegen of te verwijderen. Zie[Uw zoekservice in Azure beheren](search-manage.md) of [Servicelimieten](search-limits-quotas-capacity.md) voor meer informatie.

