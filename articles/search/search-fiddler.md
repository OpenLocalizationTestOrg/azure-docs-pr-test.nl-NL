---
title: aaaHow toouse Fiddler tooevaluate en Azure Search REST-API's testen | Microsoft Docs
description: Gebruik Fiddler om de beschikbaarheid van een benadering code gratis tooverifying Azure Search en uitprobeert Hallo REST-API's.
services: search
documentationcenter: 
author: HeidiSteen
manager: mblythe
editor: 
ms.assetid: 790e5779-c6a3-4a07-9d1e-d6739e6b87d2
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: heidist
ms.openlocfilehash: 2912e1180717d7b40a1e4f7f7f00daf2cc254f0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-fiddler-tooevaluate-and-test-azure-search-rest-apis"></a>Gebruik Fiddler tooevaluate en testen van Azure Search REST-API 's
> [!div class="op_single_selector"]
>
> * [Overzicht](search-query-overview.md)
> * [Search Explorer](search-explorer.md)
> * [Fiddler](search-fiddler.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
>
>

Dit artikel wordt uitgelegd hoe toouse Fiddler, beschikbaar als een [gratis download via Telerik](http://www.telerik.com/fiddler), tooissue HTTP-aanvragen tooand antwoorden weergeven met behulp van hello Azure Search REST API, zonder toowrite code. Azure Search is een volledig beheerde, gehoste Microsoft Azure-service voor zoeken in de cloud. De service is eenvoudig programmeerbaar via .NET en REST API's. Hello Azure Search service REST-API's zijn beschreven op [MSDN](https://msdn.microsoft.com/library/azure/dn798935.aspx).

In de Hallo stappen te volgen, hebt u een index maken, uploaden van documenten, query Hallo index en query Hallo systeem om servicegegevens te zoeken.

toocomplete deze stappen, moet u een Azure Search-service en `api-key`. Zie [maken van een Azure Search-service in Hallo portal](search-create-service-portal.md) voor instructies over hoe tooget gestart.

## <a name="create-an-index"></a>Een index maken
1. Start Fiddler. Op Hallo **bestand** menu uitschakelen **verkeer vastleggen** toohide HTTP-activiteit die geen verband toohello huidige taak.
2. Op Hallo **Composer** tabblad formuleert u een aanvraag dat lijkt op Hallo volgende schermopname.

      ![][1]
3. Selecteer **PUT**.
4. Voer een URL waarmee Hallo service-URL, Aanvraagkenmerken en Hallo api-versie. Enkele aanwijzers tookeep rekening:

   * Gebruik HTTPS als voorvoegsel Hallo.
   * Het aanvraagkenmerk is '/indexes/hotels'. Zo weet Search toocreate index met de naam 'hotels'.
   * De API-versie moet worden opgegeven in kleine letters, als '?api-version=2016-09-01'. API-versies zijn belangrijk omdat Azure Search regelmatig updates implementeert. In zeldzame gevallen kan een service-update kan leiden tot een recente wijziging toohello API. Daarom vereist Azure Search bij elke aanvraag een API-versie, zodat u de volledige controle hebt over de API-versie die wordt gebruikt.

     Hallo volledige URL moet eruitzien vergelijkbare toohello voorbeeld te volgen.

             https://my-app.search.windows.net/indexes/hotels?api-version=2016-09-01
5. Geef de aanvraagheader hello, Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
6. Plak in Hallo velden waaruit de indexdefinitie Hallo aanvraagtekst.

          {
         "name": "hotels",  
         "fields": [
           {"name": "hotelId", "type": "Edm.String", "key":true, "searchable": false},
           {"name": "baseRate", "type": "Edm.Double"},
           {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
           {"name": "hotelName", "type": "Edm.String"},
           {"name": "category", "type": "Edm.String"},
           {"name": "tags", "type": "Collection(Edm.String)"},
           {"name": "parkingIncluded", "type": "Edm.Boolean"},
           {"name": "smokingAllowed", "type": "Edm.Boolean"},
           {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
           {"name": "rating", "type": "Edm.Int32"},
           {"name": "location", "type": "Edm.GeographyPoint"}
          ]
         }
7. Klik op **Uitvoeren**.

In enkele seconden, ziet u een 201 HTTP-antwoord in de sessielijst hello, hetgeen betekent dat Hallo index is gemaakt.

Als u HTTP 504-respons ontvangt, controleert u of dat Hallo URL HTTPS bevat. Als u HTTP-fout 400 of 404 wordt weergegeven, controleert u Hallo aanvraag hoofdtekst tooverify er geen fouten zijn opgetreden kopiëren en plakken. Een HTTP 403 duidt doorgaans op een probleem met Hallo api-sleutel (een ongeldige sleutel of een probleem syntaxis met hoe Hallo api-sleutel is opgegeven).

## <a name="load-documents"></a>Documenten laden
Op Hallo **Composer** tabblad uw aanvraag toopost documenten eruit Hallo volgende. Hallo-hoofdtekst van Hallo-aanvraag bevat Hallo zoekgegevens voor 4 hotels.

   ![][2]

1. Selecteer **POST**.
2. Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?api-version=2016-09-01'. Hallo volledige URL moet eruitzien vergelijkbare toohello voorbeeld te volgen.

         https://my-app.search.windows.net/indexes/hotels/docs/index?api-version=2016-09-01
3. Aanvraag-Header moet worden Hallo hetzelfde als voorheen. Houd er rekening mee dat u Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hallo aanvraagtekst bevat vier documenten toobe toegevoegde toohello hotels index.

         {
         "value": [
         {
             "@search.action": "upload",
             "hotelId": "1",
             "baseRate": 199.0,
             "description": "Best hotel in town",
             "hotelName": "Fancy Stay",
             "category": "Luxury",
             "tags": ["pool", "view", "wifi", "concierge"],
             "parkingIncluded": false,
             "smokingAllowed": false,
             "lastRenovationDate": "2010-06-27T00:00:00Z",
             "rating": 5,
             "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "2",
             "baseRate": 79.99,
             "description": "Cheapest hotel in town",
             "hotelName": "Roach Motel",
             "category": "Budget",
             "tags": ["motel", "budget"],
             "parkingIncluded": true,
             "smokingAllowed": true,
             "lastRenovationDate": "1982-04-28T00:00:00Z",
             "rating": 1,
             "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
           },
           {
             "@search.action": "upload",
             "hotelId": "3",
             "baseRate": 279.99,
             "description": "Surprisingly expensive",
             "hotelName": "Dew Drop Inn",
             "category": "Bed and Breakfast",
             "tags": ["charming", "quaint"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.33207, 47.60621] }
           },
           {
             "@search.action": "upload",
             "hotelId": "4",
             "baseRate": 220.00,
             "description": "This could be hello one",
             "hotelName": "A Hotel for Everyone",
             "category": "Basic hotel",
             "tags": ["pool", "wifi"],
             "parkingIncluded": true,
             "smokingAllowed": false,
             "lastRenovationDate": null,
             "rating": 4,
             "location": { "type": "Point", "coordinates": [-122.12151, 47.67399] }
           }
          ]
         }
5. Klik op **Uitvoeren**.

In enkele seconden ziet u een HTTP 200-respons in de sessielijst Hallo. Hiermee wordt aangegeven Hallo documenten zijn gemaakt. Als u een 207 krijgt, wordt er door ten minste één document tooupload niet. Als u een 404 krijgt, hebt u Hallo koptekst of hoofdtekst van Hallo aanvraag een syntaxisfout.

## <a name="query-hello-index"></a>Query Hallo index
Nu er een index en documenten zijn geladen, kunt u hier query's op uitvoeren.  Op Hallo **Composer** tabblad een **ophalen** opdracht waarmee een query op uw service ziet er vergelijkbare toohello volgende schermopname.

   ![][3]

1. Selecteer **GET**.
2. Geef een URL op die begint met HTTPS, gevolgd door uw service-URL, gevolgd door '/indexes/<indexnaam>/docs/index?', gevolgd door queryparameters. Gebruik als bijvoorbeeld Hallo URL te volgen en vervangt Hallo Voorbeeldnaam van een host met een geldige voor uw service.

         https://my-app.search.windows.net/indexes/hotels/docs?search=motel&facet=category&facet=rating,values:1|2|3|4|5&api-version=2016-09-01

   Deze query zoekt op Hallo term 'motel' en facetcategorieën voor beoordelingen opgehaald.
3. Aanvraag-Header moet worden Hallo hetzelfde als voorheen. Houd er rekening mee dat u Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444

Hallo responscode moet 200 en Hallo antwoorduitvoer moet eruitzien vergelijkbare toohello volgende schermopname.

   ![][4]

Hallo volgende voorbeeldquery is afkomstig uit Hallo [Search Index-bewerking (Azure Search API)](http://msdn.microsoft.com/library/dn798927.aspx) op MSDN. Veel van Hallo voorbeelden van query's in dit onderwerp bevatten spaties, deze zijn niet toegestaan in Fiddler. Vervang elke spatie door een + teken voordat plakken Hallo querytekenreeks voordat u probeert Hallo-query in Fiddler.

**Voordat de spaties zijn vervangen:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate desc&api-version=2016-09-01

**Nadat de spaties zijn vervangen door +:**

        GET /indexes/hotels/docs?search=*&$orderby=lastRenovationDate+desc&api-version=2016-09-01

## <a name="query-hello-system"></a>query Hallo systeem
U kunt ook Hallo system tooget tellingen en opslag documentverbruik opvragen. Op Hallo **Composer** tabblad vergelijkbare toohello volgende eruit ziet uw aanvraag en Hallo respons retourneert een getal voor Hallo aantal documenten en de gebruikte ruimte.

 ![][5]

1. Selecteer **GET**.
2. Geef een URL op die uw service-URL bevat, gevolgd door '/indexes/hotels/stats?api-version=2016-09-01':

         https://my-app.search.windows.net/indexes/hotels/stats?api-version=2016-09-01
3. Geef de aanvraagheader hello, Hallo host en api-sleutel vervangen door waarden die geldig voor uw service zijn.

         User-Agent: Fiddler
         host: my-app.search.windows.net
         content-type: application/json
         api-key: 1111222233334444
4. Hallo aanvraagtekst leeg laten.
5. Klik op **Uitvoeren**. Hier ziet u een HTTP 200-statuscode in de sessielijst Hallo. Selecteer Hallo-vermelding voor de opdracht.
6. Klik op Hallo **Inspectors** en klik op Hallo **Headers** tabblad en selecteer vervolgens Hallo JSON-indeling. U ziet Hallo document count en opslaggrootte (in KB).

## <a name="next-steps"></a>Volgende stappen
Zie [uw Search-service op Azure beheren](search-manage.md) voor een toomanaging zonder code benadering en het gebruik van Azure Search.

<!--Image References-->
[1]: ./media/search-fiddler/AzureSearch_Fiddler1_PutIndex.png
[2]: ./media/search-fiddler/AzureSearch_Fiddler2_PostDocs.png
[3]: ./media/search-fiddler/AzureSearch_Fiddler3_Query.png
[4]: ./media/search-fiddler/AzureSearch_Fiddler4_QueryResults.png
[5]: ./media/search-fiddler/AzureSearch_Fiddler5_QueryStats.png
