---
title: aaaIndexing CSV blobs met Azure Search-indexeerfunctie voor blobs | Microsoft Docs
description: Meer informatie over hoe tooindex CSV blobs met Azure Search
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: ed3c9cff-1946-4af2-a05a-5e0b3d61eb25
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 12/15/2016
ms.author: eugenesh
ms.openlocfilehash: f2b1ce824e62c5b3f6155c6e88887897cf1a8eae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-csv-blobs-with-azure-search-blob-indexer"></a>Indexeren van CSV-blobs met Azure Search blob indexeerfunctie
Standaard [Azure Search-indexeerfunctie voor blob](search-howto-indexing-azure-blob-storage.md) parseert gescheiden tekst blobs als een enkel deel van de tekst. Met blobs met CSV-gegevens, wilt u echter vaak tootreat elke regel in de blob Hallo als een afzonderlijk document. Gegeven Hallo bijvoorbeeld gescheiden volgende tekst: 

    id, datePublished, tags
    1, 2016-01-12, "azure-search,azure,cloud" 
    2, 2016-07-07, "cloud,mobile" 

tooparse kunt u deze in documenten, 2, die elk 'id', 'datePublished' en 'labels' velden bevat.

In dit artikel leert u hoe tooparse CSV met een Azure Search-indexeerfunctie blob blobs. 

> [!IMPORTANT]
> Deze functionaliteit is momenteel in preview. Dit is alleen beschikbaar in Hallo REST-API met versie **2015-02-28-Preview**. Maak onthouden, preview-API's zijn bedoeld voor testen en evalueren en mag niet worden gebruikt in een productieomgeving. 
> 
> 

## <a name="setting-up-csv-indexing"></a>Instellen van het CSV-indexeren
tooindex CSV blobs, maken of bijwerken van de definitie van een indexeerfunctie Hello `delimitedText` bij het parseren van modus:  

    {
      "name" : "my-csv-indexer",
      ... other indexer properties
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "firstLineContainsHeaders" : true } }
    }

Voor meer informatie over Hallo indexeerfunctie-API maken, Bekijk [indexeerfunctie maken](search-api-indexers-2015-02-28-preview.md#create-indexer).

`firstLineContainsHeaders`Geeft aan dat het eerste (niet-lege) regel Hallo van elke blob kopteksten bevat.
Als blobs niet een initiële kopregel bevatten, worden Hallo headers opgegeven in configuratie van de indexeerfunctie Hallo: 

    "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } } 

Op dit moment wordt alleen Hallo UTF-8-codering ondersteund. Door komma's ook alleen Hallo `','` teken als scheidingsteken hello wordt ondersteund. Als u ondersteuning nodig voor andere coderingen of scheidingstekens, laat ons weten op [onze UserVoice-site](https://feedback.azure.com/forums/263029-azure-search).

> [!IMPORTANT]
> Wanneer u Hallo gescheiden tekst bij het parseren van Azure Search-modus gebruikt, wordt ervan uitgegaan dat alle blobs in de gegevensbron zal CSV. Als u een combinatie van CSV toosupport moet en blobs niet-CSV in Hallo dezelfde gegevensbron, laat ons weten op [onze UserVoice-site](https://feedback.azure.com/forums/263029-azure-search).
> 
> 

## <a name="request-examples"></a>Voorbeelden van aanvraag
Als dit alle hier volgen samen Hallo volledige nettolading voorbeelden. 

Gegevensbron: 

    POST https://[service name].search.windows.net/datasources?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional, my-folder>" }
    }   

Indexeerfunctie:

    POST https://[service name].search.windows.net/indexers?api-version=2015-02-28-Preview
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-csv-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "parameters" : { "configuration" : { "parsingMode" : "delimitedText", "delimitedTextHeaders" : "id,datePublished,tags" } }
    }

## <a name="help-us-make-azure-search-better"></a>Help ons Azure Search te verbeteren
Als u functieaanvragen of suggesties voor verbeteringen hebt, kunt contact toous op onze [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).

