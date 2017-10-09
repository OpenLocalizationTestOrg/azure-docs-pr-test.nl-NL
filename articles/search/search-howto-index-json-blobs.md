---
title: aaaIndexing JSON-blobs met Azure Search blob indexeerfunctie
description: Indexeren van JSON-blobs met Azure Search blob indexeerfunctie
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Indexeren van JSON-blobs met Azure Search blob indexeerfunctie
Dit artikel laat zien hoe tooconfigure Azure Search blob indexeerfunctie tooextract gestructureerd inhoud uit blobs die JSON bevatten.

## <a name="scenarios"></a>Scenario's
Standaard [Azure Search-indexeerfunctie voor blob](search-howto-indexing-azure-blob-storage.md) JSON-blobs worden geparseerd als een enkel deel van de tekst. Vaak wilt u toopreserve Hallo structuur van uw JSON-documenten. Bijvoorbeeld: opgegeven Hallo JSON-document

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

u kunt dit in een Azure Search-document met 'text', 'datePublished' en 'tags' velden tooparse.

U kunt ook wanneer uw blobs bevatten een **matrix met JSON-objecten**, kunt u elk element van Hallo matrix toobecome een afzonderlijk Azure Search-document. Bijvoorbeeld, krijgt een blob met deze JSON:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

u kunt uw Azure Search-index met drie afzonderlijke documenten, elk met velden 'id' en 'text' vullen.

> [!IMPORTANT]
> Hallo JSON-matrix parseren functionaliteit is momenteel in preview. Dit is alleen beschikbaar in Hallo REST-API met versie **2015-02-28-Preview**. Denk erom, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving.
>
>

## <a name="setting-up-json-indexing"></a>Instellen van JSON indexeren
Indexeren van JSON-blobs is vergelijkbaar toohello standaarddocument uitpakken. Maak eerst Hallo datasource precies zoals u normaal doet: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Vervolgens Hallo doel search-index maken als u er nog geen hebt. 

Ten slotte Maak een indexeerfunctie en stel Hallo `parsingMode` parameter te`json` (tooindex elke blob als één document) of `jsonArray` (als uw blobs JSON-matrices bevatten en moet u elk element van een matrix toobe behandeld als een afzonderlijk document):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Gebruik indien noodzakelijk **veld toewijzingen** toopick Hallo eigenschappen van toopopulate Hallo bron JSON-document dat wordt gebruikt uw search-index van het doel, zoals wordt weergegeven in de volgende sectie Hallo.

> [!IMPORTANT]
> Als u werkt met `json` of `jsonArray` parseren van de modus Azure Search wordt ervan uitgegaan dat alle blobs in uw gegevensbron JSON bevatten. Als u een combinatie van JSON toosupport moet en niet-JSON-blobs in Hallo dezelfde gegevensbron, laat ons weten op [onze UserVoice-site](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Met behulp van documenten voor veld toewijzingen toobuild zoeken
Op dit moment Azure Search kan niet worden geïndexeerd willekeurige JSON-documenten rechtstreeks, omdat het ondersteunt alleen primitieve gegevenstypen, tekenreeksmatrices en GeoJSON punten. U kunt echter **veld toewijzingen** toopick onderdelen van uw JSON-document en 'til' deze in op het hoogste niveau van de velden van Hallo zoekdocument. toolearn over de basisprincipes van veld toewijzingen, Zie [veld-verwijzingen voor Azure Search-indexeerfunctie overbruggen Hallo verschillen tussen de gegevensbronnen en zoekindexen](search-indexer-field-mappings.md).

Terugkomen tooour voorbeeld JSON-document:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Stel dat u hebt een search-index met de volgende velden Hallo: `text` van het type `Edm.String`, `date` van het type `Edm.DateTimeOffset`, en `tags` van het type `Collection(Edm.String)`. toomap uw JSON naar Hallo gewenst vorm, Hallo volgende veldtoewijzingen gebruiken:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Hallo bron veldnamen in Hallo-toewijzingen zijn opgegeven met Hallo [JSON aanwijzer](http://tools.ietf.org/html/rfc6901) notatie. U start met een schuine streep toorefer toohello hoofdmap van uw JSON-document vervolgens Hallo desired-eigenschap (op een willekeurige niveau geneste) met behulp van doorsturen slash gescheiden pad kiezen.

U kunt ook tooindividual matrixelementen verwijzen met behulp van een op nul gebaseerde index. Bijvoorbeeld: toopick Hallo eerste element van Hallo 'labels' matrix van Hallo hierboven bijvoorbeeld een veldtoewijzing als volgt gebruiken:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Als de naam van een bron in een veld toewijzing pad tooa-eigenschap die niet bestaat in de JSON verwijst, wordt er zonder fouten toewijzing overgeslagen. Dit wordt gedaan zodat we kunnen documenten met een ander schema (dit is een algemene gebruiksvoorbeeld) ondersteunen. Omdat er geen validatie, moet u tootake voorzichtig tooavoid typefouten in uw toewijzing veld opgeven.
>
>

Als uw JSON-documenten alleen eenvoudige op het hoogste niveau eigenschappen bevatten, moet u mogelijk geen veldtoewijzingen helemaal. Bijvoorbeeld, als uw JSON lijkt op deze, Hallo op het hoogste niveau eigenschappen 'text', 'datePublished' en 'tags' rechtstreeks toegewezen toohello overeenkomende velden in de search-index Hallo:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Hier volgt een volledige indexeerfunctie nettolading met veldtoewijzingen:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>Geneste matrices van JSON indexeren
Wat gebeurt er als u tooindex desgewenst een matrix van JSON-objecten, maar dat matrix ergens is genest binnen Hallo document? U kunt kiezen welke eigenschap bevat Hallo-matrix met Hallo `documentRoot` configuratie-eigenschap. Als bijvoorbeeld uw blobs moeten uitzien:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Gebruik deze configuratie tooindex Hallo matrix in Hallo `level2` eigenschap:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Help ons Azure Search te verbeteren
Als u hebt het functieaanvragen of suggesties voor verbeteringen, bereiken toous op onze [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
