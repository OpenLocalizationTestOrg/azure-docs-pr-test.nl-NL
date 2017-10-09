---
title: aaaMobile Engagement exporteren-API-overzicht
description: Meer informatie over Hallo basisbeginselen over het exporteren van de onbewerkte gegevens gegenereerd door de gebruiker apparaten tooleverage in uw eigen hulpprogramma 's
services: mobile-engagement
documentationcenter: mobile
author: kpiteira
manager: erikre
editor: 
ms.assetid: 9380d47b-d7fa-4d4c-888f-97e6482196bb
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 04/26/2016
ms.author: kapiteir
ms.openlocfilehash: f55be29a29878e74f6a33419f08a5574a07a7478
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="mobile-engagement-export-api-overview"></a>Overzicht van Mobile Engagement Export-API
## <a name="introduction"></a>Inleiding
In dit document leert u Hallo basisbeginselen over het exporteren van de onbewerkte gegevens gegenereerd door de gebruiker apparaten tooleverage in uw eigen hulpmiddelen.

## <a name="pre-requisites"></a>Vereisten
Hallo onbewerkte gegevens exporteren van Mobile Engagement vereist:

* API authentication setup toobe kunnen toouse Hallo API's (Zie [verificatie handmatige installatie](mobile-engagement-api-authentication-manual.md)),
* Hallo REST-API's of hello gebruiken [.net SDK](mobile-engagement-dotnet-sdk-service-api.md),
* Een Azure Storage-account.

> [!NOTE]
> Ook wordt geadviseerd de Hallo uitstekende [Microsoft Azure Storage Explorer](http://storageexplorer.com/), ten minste tijdens de ontwikkelingsfase Hallo zoals deze voor interactie met Azure Storage biedt een eenvoudige toouse gebruikersinterface.
> 
> 

## <a name="what-can-be-exported"></a>Wat kunnen worden geëxporteerd?
Mobile Engagement kunt de gebruikers toocollect veel soorten gegevens, en daarom geschikt heeft verschillende typen export zijn toothese verschillende gegevenstypen.
Er zijn 2 essentiële typen van uitvoer:

* Momentopname: doorgaans tooexport gegevens die staat voor een status en waarvoor de Mobile Engagement geen hebben een geschiedenis gebruikt. Dit bevat bijvoorbeeld Tags (app-info)-tokens of push campagne feedback. Als gevolg hiervan exporteren deze typen zijn niet gerelateerd tooa datum.
* historische: dit type uitvoer wordt gebruikt voor gegevens die zich bijvoorbeeld na verloop van tijd zoals gebeurtenissen of activiteiten.

Hallo in de volgende tabel beschrijft uitgebreid Hallo mogelijke uitvoer:

| Type exporteren | Gegevenstype | Beschrijving |
| --- | --- | --- |
| Momentopname |Push |Exporteren van een van de feedback Push campagnes op basis van per apparaat-id/userid genereert |
| Momentopname |Label |Genereert een export van Hallo labels (app-info) van tooeach apparaten |
| Momentopname |Apparaat |Exporteren van een van de meeste Hallo gegevens over apparaten zoals Hallo technicals (model, landinstellingen, tijdzone,...), Hallo labels, gezien eerst genereert... |
| Momentopname |Token |Uitvoer van alle geldige Hallo-tokens genereert |
| Historische |Activiteit |Genereert een export van alle Hallo activiteiten voor elk apparaat op een opgegeven periode |
| Historische |Gebeurtenis |Genereert een export van alle Hallo activiteiten voor elk apparaat op een opgegeven periode |
| Historische |Job |Genereert een exporteren van alle Hallo-taken voor elk apparaat op een opgegeven periode |
| Historische |Fout |Genereert een exporteren met alle Hallo fouten voor elk apparaat op een opgegeven periode |

## <a name="how-does-it-work"></a>Hoe werkt het?
Uitvoer zijn lang actieve taken die kan leiden tot grote gegevensbestanden. Daarom kunnen ze aangeroepen tooreturn onmiddellijk een bestand toodownload niet.
In de volgorde tooexport gegevens van Mobile Engagement, hebt u toocreate een **taak exporteren** via API waarin u in het algemeen opgeeft:

* Hallo type export (momentopname of historische)
* Hallo-gegevenstype.
* Hallo **Azure Storage-Container** (met inbegrip van een geldige SAS met schrijftoegang) waar Hallo resultaat van Hallo exporteren worden geschreven.
* bijvoorbeeld voorbeeld Container URL-parameter zouden worden https://[StorageAccountName].blob.core.windows.net/[ContainerName]? [SASWritePermissionsToken]  

Hier volgt een voorbeeld van een echte wereld. https://testazmeexport.BLOB.Core.Windows.NET/test1234azme?SV=2015-12-11&SS=b&Srt=SCO&SP=rwdlac&se=2016-12-17T04:59:26Z & st = 2016-12-16T20:59:26Z & spr = https & sig = KRF3aVWjp2NEJDzjlmoplmu0M9HHlLdkBWRPAFmw90Q % 3D

Houd er rekening mee dat het enkele minuten voordat uw taak toobe gestart duren kan en vervolgens kan worden uitgevoerd vanuit een paar seconden voor kleine apps tooseveral uur voor apps met een groot aantal gebruikers- of -activiteit.

Zodra het Hallo-taak is gemaakt, is het mogelijk toocheck de toosee status als het nog steeds uitgevoerd of als deze is voltooid.

Zodra het Hallo-taak is voltooid, is Hallo resulterende gegevensbestand beschikbaar op Hallo opgegeven storage-container.

