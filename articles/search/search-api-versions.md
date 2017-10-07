---
title: aaaAPI versies van Azure Search | Microsoft Docs
description: Versie-beleid voor Azure Search REST-API's en Hallo clientbibliotheek in Hallo .NET SDK.
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 0458053a-164e-4682-a802-00097ecde981
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 4fa722fad5577c6b254be7fa673eb240fff316a2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="api-versions-in-azure-search"></a>API-versies in Azure Search
Azure Search regelmatig updates van de functie is uitgevouwen. Soms, maar niet altijd nodig deze updates ons toopublish een nieuwe versie van onze API toopreserve achterwaartse compatibiliteit. Publiceren van een nieuwe versie kunt u toocontrol wanneer en hoe u de search-service-updates in uw code integreren.

Als een regel proberen we toopublish nieuwe versies alleen indien nodig, aangezien deze betrekking op sommige tooupgrade inspanning hebben kan uw code toouse een nieuwe API-versie. We publiceren een nieuwe versie alleen als we toochange moet een bepaald aspect van Hallo API op een manier die achterwaartse compatibiliteit. Dit kan gebeuren vanwege oplossingen tooexisting functies of vanwege de nieuwe functies die surface area van bestaande API wijzigen.

We volgen Hallo dezelfde regel voor SDK-updates. Hello Azure Search SDK volgt Hallo [semantische versioning](http://semver.org/) regels, wat betekent dat de versie ervan bestaat uit drie delen: primaire, secundaire en build-nummer (bijvoorbeeld 1.1.0). We brengen een nieuwe primaire versie Hallo SDK alleen in geval van wijzigingen die problemen met achterwaartse compatibiliteit. We Hallo secundaire versie wordt verhoogd voor vaste functie-updates, en voor oplossingen voor problemen we alleen Hallo build-versie wordt verhoogd.

> [!NOTE]
> Verschillende versies van de REST-API, met inbegrip van de meest recente Hallo biedt ondersteuning voor uw Azure Search-service-exemplaar. Wanneer deze niet langer Hallo recentste is, maar het is raadzaam dat u de nieuwste versie van code toouse Hallo migreert, kunt u een versie toouse blijven. Wanneer u Hallo REST-API gebruikt, moet u Hallo API-versie opgeven in elke aanvraag via Hallo api-versie-parameter. Wanneer u Hallo .NET SDK, bepaalt Hallo-versie van Hallo SDK u de desbetreffende versie Hallo Hallo REST-API. Als u een oudere SDK gebruikt, kunt u blijven toorun die code zonder wijzigingen als Hallo service bijgewerkte toosupport een nieuwere API-versie.

## <a name="snapshot-of-current-versions"></a>Momentopname van huidige versies
Hieronder volgt een momentopname van Hallo huidige versies van alle programming interfaces tooAzure zoeken.

| Interfaces | Meest recente hoofdversie | Status |
| --- | --- | --- |
| [.NET SDK](https://aka.ms/search-sdk) |3.0 |In het algemeen beschikbaar, November 2016 wordt uitgebracht |
| [Voorbeeld van de .NET SDK](https://aka.ms/search-sdk-preview) |2.0-preview |Voorbeeld van augustus 2016 wordt uitgebracht |
| [Service REST API](https://docs.microsoft.com/rest/api/searchservice/) |2016-09-01 |Algemeen beschikbaar |
| [Service REST API-voorbeeld](search-api-2015-02-28-preview.md) |2015-02-28-preview |Preview |
| [Beheer van de .NET SDK](https://aka.ms/search-mgmt-sdk) |2015-08-19 |Algemeen beschikbaar |
| [REST-API voor beheer](https://docs.microsoft.com/rest/api/searchmanagement/) |2015-08-19 |Algemeen beschikbaar |

Voor de REST-API's, waaronder Hallo Hallo `api-version` op elke aanroep is vereist. Dit maakt het eenvoudig tootarget een specifieke versie, zoals een preview-API. Hallo volgende voorbeeld ziet u hoe Hallo `api-version` parameter opgegeven:

    GET https://adventure-works.search.windows.net/indexes/bikes?api-version=2016-09-01

> [!NOTE]
> Hoewel elke aanvraag heeft een `api-version`, wordt aangeraden hello te gebruiken dezelfde versie voor alle API-aanvragen. Dit is vooral van toepassing wanneer nieuwe API-versies introduceren kenmerken of bewerkingen die niet worden herkend door vorige versies. De combinatie van API-versies kan hebben ongewenste gevolgen en moeten worden vermeden.
>
> Hallo Service REST-API en de REST-API Management zijn samengestelde onafhankelijk van elkaar. Er is overeenkomsten in versienummers toevallige.

Algemeen beschikbaar (of GA) API's kunnen worden gebruikt in productie en onderwerp tooAzure serviceovereenkomsten zijn. Preview-versies hebben experimentele functies die niet altijd gemigreerde tooa GA-versie. **We raden u ten zeerste aan met behulp van de preview-API's in productietoepassingen.**

## <a name="about-preview-and-generally-available-versions"></a>Over de versies van Preview en algemeen beschikbaar
Azure Search versies altijd vooraf experimentele functies via Hallo REST-API eerst vervolgens via voorlopige versies van Hallo .NET SDK.

Preview-functies zijn niet gegarandeerd toobe gemigreerd tooa GA-release. Terwijl de functies in een GA-versie worden beschouwd als stabiel en onwaarschijnlijk toochange met uitzondering van kleine neerwaarts compatibele oplossingen en verbeteringen hello, zijn preview-functies beschikbaar voor testen en experimenteren met Hallo doel van het verzamelen van feedback op functie ontwerpen en implementeren.

Echter, omdat preview-functies onderwerp toochange zijn, wordt u aangeraden tegen schrijven productiecode waarmee een afhankelijkheid op preview-versies. Als u van een oudere versie van de preview gebruikmaakt, raden wij aan migreren toohello algemeen beschikbaar (GA) versie.

Voor de .NET SDK Hallo: richtlijnen voor de migratie van de code kan worden gevonden op [Upgrade Hallo .NET SDK](search-dotnet-sdk-migration.md).

Algemene beschikbaarheid betekent dat Azure Search nu onder Hallo serviceovereenkomst (SLA). Hallo SLA kan worden gevonden op [Azure Search-Service Level Agreements](https://azure.microsoft.com/support/legal/sla/search/v1_0/).
