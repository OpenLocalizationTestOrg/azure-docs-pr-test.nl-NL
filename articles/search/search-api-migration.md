---
title: aaaUpgrading toohello Azure Search Service REST API versie 2016-09-01 | Microsoft Docs
description: Een upgrade toohello Azure Search Service REST API versie 2016-09-01
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: d0276b9cc52996a59f9aa726c27e62c6082eb908
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-service-rest-api-version-2016-09-01"></a>Een upgrade toohello Azure Search Service REST API versie 2016-09-01
Als u versie 2015-02-28 of 2015-02-28-Preview Hallo [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), dit artikel helpt u bij het bijwerken van uw toepassing toouse Hallo volgende algemeen beschikbaar API-versie, 2016-09-01.

Versie 2016-09-01 Hallo REST-API bevat een aantal wijzigingen uit eerdere versies. Dit zijn vooral achterwaarts compatibel, zodat uw code te wijzigen, moet alleen minimale inspanning, afhankelijk van welke versie u hebt gebruikt vóór nodig. Zie [stappen tooupgrade](#UpgradeSteps) voor instructies over het toochange uw code toouse Hallo nieuwe API-versie.

> [!NOTE]
> Verschillende versies van de REST-API, met inbegrip van de meest recente Hallo biedt ondersteuning voor uw Azure Search-service-exemplaar. Wanneer deze niet langer Hallo recentste is, maar het is raadzaam dat u de nieuwste versie van code toouse Hallo migreert, kunt u een versie toouse blijven.

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a>Wat is er nieuw in versie 2016-09-01
Versie 2016-09-01 is Hallo tweede algemeen beschikbaar release van hello Azure Search Service REST API. Nieuwe functies in deze API-versie:

* [Aangepaste analyzers](https://aka.ms/customanalyzers), waarmee u tootake controle over Hallo proces van het converteren van tekst in worden geïndexeerd en doorzoekbare tokens.
* [Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) en [Azure Table Storage](search-howto-indexing-azure-tables.md) indexeerfuncties waarmee u tooeasily gegevens importeren uit Azure storage in Azure Search op een planning of op aanvraag.
* [Veld toewijzingen](search-indexer-field-mappings.md), waarmee u toocustomize hoe indexeerfuncties gegevens importeren in Azure Search.
* ETags, waarmee u tooupdate Hallo definities van indexen, Indexeerfuncties en gegevensbronnen op een manier gelijktijdigheid-safe. 

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a>Stappen tooupgrade
Als u een van versie 2015-02-28 upgrade, u waarschijnlijk geen toomake wijzigingen tooyour code, dan toochange Hallo versienummer. Hallo alleen situaties waarin u toochange code mogelijk moet zijn wanneer:

* Uw code mislukt wanneer het niet-herkende eigenschappen worden geretourneerd in een API-reactie. Standaard moet worden genegeerd in uw toepassing eigenschappen die niet wordt herkend.
* Uw code zich blijft voordoen API-aanvragen en tooresend probeert ze toohello nieuwe API-versie. Bijvoorbeeld: dit kan gebeuren als uw toepassing blijft voortzetting tokens die zijn geretourneerd door het Hallo-API van zoekservice draaien (voor meer informatie zoekt `@search.nextPageParameters` in Hallo [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).

Als beide situaties tooyou toepast, vervolgens moet u mogelijk toochange uw code dienovereenkomstig. Anders geen wijzigingen moeten niet nodig, tenzij u wilt dat toostart met Hallo [nieuwe functies](#WhatsNew) van 2016-09-01-versie.

Als u een van versie 2015-02-28-Preview upgrade, Hallo hierboven is ook van toepassing, maar u moet ook rekening houden sommige preview-functies zijn niet beschikbaar in versie 2016-09-01:

* Azure Blob Storage-indexeerfunctie ondersteuning voor CSV-bestanden en blobs met JSON-matrices.
* Synoniemen
* 'Meer als volgt' query 's

Als uw code deze functies gebruikt, zich u niet kunnen tooupgrade too2016-09-01 zonder uw gebruik ervan worden verwijderd.

> [!IMPORTANT]
> Maak onthouden, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving.
> 
> 

## <a name="conclusion"></a>Conclusie
Als u meer informatie over het gebruik van Azure Search Service REST API Hallo nodig, raadpleegt u Hallo onlangs bijgewerkt [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) op MSDN.

Uw feedback is Welkom op Azure Search. Als u problemen ondervindt, kunt u gratis tooask ons voor hulp bij het Hallo [Azure Search MSDN-forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) of [StackOverflow](http://stackoverflow.com/). Als vraagt u een vraag over Azure zoeken op StackOverflow, zorg ervoor dat tootag met `azure-search`.

Hartelijk dank voor het gebruik van Azure Search.

