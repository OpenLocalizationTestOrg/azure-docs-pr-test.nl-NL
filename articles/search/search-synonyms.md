---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: Voorlopige documentatie voor Hallo synoniemen (preview)-functie, worden weergegeven in hello Azure Search REST-API.
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Synoniemen in Azure Search (preview)

Synoniemen in zoekmachines koppelen gelijkwaardige termen die impliciet Vouw Hallo bereik van een query zonder Hallo gebruiker tooactually Hallo term bieden. Bijvoorbeeld vallen bepaalde Hallo term 'aquaduct' en synoniem koppelingen van 'hondachtige' en 'puppy', alle documenten met 'aquaduct', 'hondachtige' of 'puppy' binnen Hallo bereik van Hallo-query.

In Azure Search wordt synoniem uitbreiding uitgevoerd op moment dat de query. U kunt synoniem maps tooa service niets onderbreking van de tooexisting bewerkingen toevoegen. U kunt toevoegen een **synonymMaps** tooa veld eigenschapdefinitie zonder toorebuild Hallo index. Zie voor meer informatie [Index bijwerken](https://docs.microsoft.com/rest/api/searchservice/update-index).

## <a name="feature-availability"></a>Beschikbaarheid van functies

Hallo-synoniemen functie is momenteel in preview en alleen ondersteund de meest recente preview-api-versie Hallo (api-version = 2016-09-01-Preview). Azure Portal biedt er momenteel geen ondersteuning voor. Omdat Hallo API-versie op Hallo-aanvraag is opgegeven, is het mogelijk toocombine algemeen beschikbaar (GA) en de preview-API's in Hallo dezelfde app. Preview-API's niet onder de SERVICEOVEREENKOMST en de functies zijn kan echter wel wijzigen, zodat u kunt beter niet met deze in productietoepassingen.

## <a name="how-toouse-synonyms-in-azure-search"></a>Hoe toouse synoniemen in Azure zoeken

In Azure Search is synoniem ondersteuning gebaseerd op synoniem maps dat u definieert en tooyour service uploaden. Deze toewijzingen deel uitmaken van een onafhankelijke resource (zoals indexen of gegevensbronnen) en kunnen worden gebruikt door een doorzoekbaar veld in een index in uw zoekservice.

Synoniem toegewezen en indexen onafhankelijk worden bewaard. Zodra u een kaart synoniem definiëren en upload het tooyour service, kunt u Hallo synoniem functie op een veld inschakelen door een nieuwe eigenschap toe te voegen **synonymMaps** in Hallo velddefinitie. Maken, bijwerken en verwijderen van die een synoniem-kaart altijd een hele document-bewerking is, wat betekent dat u geen maken, bijwerken of delen van Hallo synoniem kaart incrementeel te verwijderen. Zelfs een afzonderlijke vermelding bijwerken vereist een opnieuw laden.

Synoniemen opnemen in uw toepassing search is een proces in twee stappen:

1.  Toevoegen van een synoniem kaart tooyour search-service via Hallo onderstaande API's.  

2.  Configureer een doorzoekbare toouse Hallo synoniem veldtoewijzing in Hallo indexdefinitie.

### <a name="synonymmaps-resource-apis"></a>SynonymMaps Resource API 's

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Toevoegen of bijwerken van een kaart synoniem onder uw service en met behulp van posten of te plaatsen.

Synoniem maps worden geüpload toohello service via POST of PUT. Elke regel moet worden gevolgd door een nieuwe regelteken hello (\n). U kunt definiëren van too5, 000 regels per synoniem kaart in een gratis service en 10.000 regels in andere SKU's. Elke regel kan van too20 uitbreidingen hebben.

In dit voorbeeld moet synoniem maps Hallo Apache Solr indeling die hieronder wordt beschreven. Als u een bestaande synoniem woordenlijst in een andere indeling en toouse wilt deze rechtstreeks laat ons weten op [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

U kunt een nieuwe synoniem-toewijzing met behulp van HTTP POST, zoals in het volgende voorbeeld Hallo maken:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

U kunt ook gebruik van PUT en Hallo synoniem toewijzingsnaam op Hallo URI opgeven. Als Hallo synoniem kaart niet bestaat, wordt deze gemaakt.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Apache Solr synoniem indeling

Hallo Solr indeling ondersteunt gelijkwaardige en expliciete synoniem toewijzingen. Regels voor apparaatgroeptoewijzing voldoen toohello open-source synoniem filterspecificatie van Apache Solr, in dit document beschreven: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Hieronder volgt een voorbeeldregel voor de equivalente synoniemen.
```
              USA, United States, United States of America
```

Met de Hallo regel hierboven, zoeken query 'VS' te vergroten 'VS' of 'Verenigde Staten' of 'Verenigde Staten van Amerika'.

Expliciete toewijzing wordt aangeduid met een pijl ' = > '. Als u opgeeft, een reeks termijn van een zoekopdracht die overeenkomt met de Hallo linkerzijde van ' = > ' wordt vervangen door Hallo alternatieven aan de rechterkant Hallo. Hallo regel onderstaande gezien, zoekquery's 'Washington', 'Staat Washington' of "WA" alle herschreven te "WA". Expliciete toewijzing alleen van toepassing is in de opgegeven Hallo richting en herschrijven Hallo query "WA" niet te 'Washington' in dit geval.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Lijst synoniem maps onder uw service.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Een kaart synoniem onder uw service ophalen.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Verwijderen van een kaart synoniemen onder uw service.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Configureer een doorzoekbare toouse Hallo synoniem veldtoewijzing in Hallo indexdefinitie.

De eigenschap van een nieuw veld **synonymMaps** mag gebruikte toospecify een synoniem kaart toouse voor een doorzoekbaar veld. Synoniem maps service level bronnen en kunnen worden verwezen vanuit elk veld van een index onder Hallo-service.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** kan worden opgegeven voor de doorzoekbare velden van het Hallo-type 'Edm.String' of 'Verzameling (EDM.String)'.

> [!NOTE]
> In dit voorbeeld, kunt u slechts één synoniem toewijzen per veld hebben. Als u meerdere synoniem maps toouse wilt, laat ons weten op [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Gevolgen van synoniemen voor andere zoekfuncties

Hallo synoniemen functie herschrijft Hallo oorspronkelijke query met synoniemen Hello OR-operator. Om deze reden behandelen treffers syntaxismarkering en -profielen scoren de oorspronkelijke termijn Hallo en synoniemen als equivalent.

Synoniem functie toosearch query's van toepassing is en is niet van toepassing toofilters of facetten. Op deze manier worden suggesties alleen gebaseerd op de oorspronkelijke termijn Hallo; synoniem overeenkomsten worden niet weergegeven in het Hallo-antwoord.

Synoniem uitbreidingen zijn niet van toepassing toowildcard zoektermen; voorvoegsel, bij benadering, en de regex-voorwaarden worden niet aangevuld.

## <a name="tips-for-building-a-synonym-map"></a>Tips voor het bouwen van een synoniem-kaart

- Een beknopte, goed ontworpen synoniem-kaart is efficiënter dan een volledige lijst van mogelijke overeenkomsten. Uitzonderlijk groot of complex woordenlijsten langer tooparse nemen en van invloed zijn op Hallo Querylatentie als Hallo query toomany synoniemen wordt uitgebreid. In plaats van de schatting waarmee voorwaarden kunnen worden gebruikt, kunt u de werkelijke voorwaarden Hallo via krijgen een [verkeer analyserapport zoeken](search-traffic-analytics.md).

- Als een inleiding en de validatie oefening inschakelen en vervolgens gebruik dit rapport tooprecisely bepalen welke voorwaarden profiteren van een overeenkomst synoniem en ga vervolgens verder met toouse als validatie van de kaart synoniem opstellen van een beter resultaat. Hallo vooraf gedefinieerd rapport, tegels Hallo 'meest algemene zoekquery's ' en 'nul resultaat zoekquery's ', krijgt u Hallo benodigde informatie.

- U kunt meerdere synoniem toewijzingen maken voor uw zoektoepassing (bijvoorbeeld per taal als de toepassing meerdere talen van de klant base ondersteunt). Een veld kunt een van beide op dit moment alleen kunnen gebruiken. U kunt de eigenschap synonymMaps van een veld op elk gewenst moment bijwerken.

## <a name="next-steps"></a>Volgende stappen

- Als u een bestaande index in een ontwikkelomgeving (niet-productieve) hebt, experimenteren met een kleine woordenlijst toosee hoe Hallo toevoeging van synoniemen Hallo zoekervaring, met inbegrip van de gevolgen voor score berekenen voor profielen, treffers markeringen en suggesties verandert.

- [Inschakelen van search traffic analytics](search-traffic-analytics.md) en gebruik Hallo vooraf gedefinieerde Power BI-rapport toolearn welke termen worden gebruikt Hallo meeste en welke waarden retourneren nul documenten. . Met deze inzichten worden herzien Hallo woordenlijst tooinclude synoniemen voor niet-productieve query's die moeten worden het omzetten van toodocuments in uw index.
