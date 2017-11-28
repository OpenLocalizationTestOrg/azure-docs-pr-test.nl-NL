---
title: aaaIndexing Azure Table storage met Azure Search | Microsoft Docs
description: Meer informatie over hoe tooindex gegevens opgeslagen in Azure Table storage met Azure Search
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Azure Table storage met Azure Search-index
Dit artikel laat zien hoe toouse Azure Search tooindex gegevens opgeslagen in Azure Table storage.

## <a name="set-up-azure-table-storage-indexing"></a>Instellen van Azure Table storage indexeren

U kunt een indexeerfunctie Azure Table-opslag instellen met behulp van deze bronnen:

* [Azure Portal](https://ms.portal.azure.com)
* Azure Search [REST-API](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations)
* Azure Search [.NET SDK](https://aka.ms/search-sdk)

Hier ziet Hallo stroom met behulp van Hallo REST-API. 

### <a name="step-1-create-a-datasource"></a>Stap 1: Een gegevensbron maken

Een gegevensbron geeft aan welke gegevens tooindex, hello referenties nodig tooaccess Hallo gegevens en Hallo-beleid waarmee Azure Search tooefficiently wijzigingen in Hallo gegevens identificeren.

Voor tabel indexeren, moet de datasource Hallo Hallo volgende eigenschappen hebben:

- **naam** Hallo unieke naam van de datasource Hallo binnen uw search-service is.
- **type** moet `azuretable`.
- **referenties** parameter Hallo account opslagverbindingsreeks bevat. Zie Hallo [referenties opgeven](#Credentials) sectie voor meer informatie.
- **container** sets Hallo tabelnaam en een optionele query.
    - Hallo-tabelnaam opgeven met behulp van Hallo `name` parameter.
    - Geef eventueel een query met behulp van Hallo `query` parameter. 

> [!IMPORTANT] 
> Gebruik indien mogelijk een filter op PartitionKey voor betere prestaties. Een andere query biedt een volledige tabelscan leiden tot slechte prestaties voor grote tabellen. Zie Hallo [Prestatieoverwegingen](#Performance) sectie.


een gegevensbron toocreate:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Zie voor meer informatie over Hallo maken Datasource API [Datasource maken](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Manieren toospecify referenties ####

U kunt Hallo referenties opgeven voor Hallo-tabel in een van de volgende manieren: 

- **Volledige toegang account opslagverbindingsreeks**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` Hallo verbindingsreeks kunt u krijgen via hello Azure-portal door te gaan toohello **blade Opslagaccount** > **instellingen**   >  **Sleutels** (voor klassieke opslagaccounts) of **instellingen** > **toegangssleutels** (voor Azure Resource Manager storage-accounts).
- **Storage-account shared access signature-verbindingsreeks**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` shared access signature voor Hallo Hallo lijst en leesrechten op (tabellen in dit geval) containers en objecten (tabelrijen) moet hebben.
-  **Shared access signature voor tabel**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` shared access signature voor Hallo moet query (lezen) machtigingen hebben op Hallo tabel.

Toegang tot de handtekeningen voor meer informatie over gedeelde opslag, Zie [gedeelde handtekeningen voor toegang](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Als u gedeelde toegang handtekening referenties gebruikt, moet u tooupdate Hallo datasource referenties regelmatig met vernieuwde handtekeningen tooprevent ze zijn verlopen. Als shared access signature referenties is verlopen, mislukt Hallo indexeerfunctie met een foutbericht te 'opgegeven in de verbindingsreeks Hallo referenties zijn ongeldig of verlopen."  

### <a name="step-2-create-an-index"></a>Stap 2: Een index maken
Hallo index geeft Hallo velden in een document, Hallo kenmerken, en andere constructies definiëren die vorm Hallo-zoekfunctie.

een index toocreate:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Zie voor meer informatie over het maken van indexen [Create Index](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Stap 3: Maak een indexeerfunctie
Een indexeerfunctie een gegevensbron is verbonden met een doel search-index en vindt u een planning tooautomate Hallo gegevens vernieuwen. 

Wanneer het Hallo-index en gegevensbron worden gemaakt, bent u klaar toocreate Hallo indexeerfunctie:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Deze indexeerfunctie wordt elke twee uur uitgevoerd. (Hallo schema-interval is ingesteld, te 'PT2H'.) een indexeerfunctie toorun elke 30 minuten ingesteld hello-interval te 'PT30M'. Hallo kortste voor het interval is vijf minuten. Hallo-schema is optioneel. Als u dit weglaat, wordt er een indexeerfunctie uitgevoerd slechts eenmaal wanneer deze gemaakt. U kunt echter een indexeerfunctie uitvoeren op aanvraag op elk gewenst moment.   

Zie voor meer informatie over Hallo API maken voor indexering [indexeerfunctie maken](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Omgaan met verschillende veldnamen
Soms wijken Hallo veldnamen in uw bestaande index af van de eigenschapsnamen Hallo in de tabel. U kunt toewijzingen toomap Hallo eigenschap veldnamen uit Hallo tabel toohello veldnamen gebruiken in uw search-index. Zie toolearn meer informatie over het veldtoewijzingen [veld-verwijzingen voor Azure Search-indexeerfunctie overbruggen Hallo verschillen tussen de gegevensbronnen en zoekindexen](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Ingang document sleutels
In Azure Search identificatie Hallo documentsleutel unieke van een document. Elke search-index moet exact één sleutelveld van het type `Edm.String`. Hallo sleutelveld is vereist voor elk document dat toohello index wordt toegevoegd. (In feite de Hallo alleen vereist veld.)

Aangezien de tabelrijen hebben een samengestelde sleutel, Azure Search genereert een synthetische veld `Key` die een samenvoeging van de partitie sleutel- en sleutelwaarden is. Bijvoorbeeld, als een rij van het PartitionKey is `PK1` en RowKey `RK1`, vervolgens Hallo `Key` waarde van veld is `PK1RK1`.

> [!NOTE]
> Hallo `Key` waarde mag de tekens die ongeldig in het document sleutels, zoals streepjes zijn bevatten. U kunt maken met ongeldige tekens met behulp van Hallo `base64Encode` [veld toewijzing functie](search-indexer-field-mappings.md#base64EncodeFunction). Als u dit doet, moet u tooalso gebruik URL-safe Base64-codering wanneer zoals Lookup doorgeven van een document sleutels in de API aanroept.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Detectie van incrementele indexeren en verwijderen
Bij het instellen van een tabel indexeerfunctie toorun volgens een schema, deze alleen nieuwe of bijgewerkte rijen, zoals wordt bepaald door een rij reindexes `Timestamp` waarde. U hebt geen toospecify een wijzigingsbeleid. Incrementele indexeren is automatisch ingeschakeld.

tooindicate dat bepaalde documenten moeten worden verwijderd van de index hello, kunt u een strategie voor voorlopig verwijderen gebruiken. Toevoegen in plaats van een rij verwijdert, een eigenschap tooindicate dat deze wordt verwijderd en een voorlopig detectie van het verwijderingsbeleid voor Hallo datasource instellen. Bijvoorbeeld, Hallo beleid na acht dat een rij is verwijderd als Hallo rij een eigenschap heeft `IsDeleted` met Hallo waarde `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Prestatieoverwegingen

Azure Search gebruikt standaard Hallo queryfilter te volgen: `Timestamp >= HighWaterMarkValue`. Omdat Azure-tabellen een secundaire index op Hallo hoeft `Timestamp` veld, dit type query vereist een volledige tabelscan en kan daarom langzaam is voor grote tabellen.


Hier vindt u twee mogelijke methoden voor het verbeteren van de tabel indexering prestaties. Deze beide benaderingen afhankelijk van het gebruik van Tabelpartities: 

- Als uw gegevens kunnen natuurlijk verschillende partitie bereiken worden gepartitioneerd, maakt u een gegevensbron en een bijbehorende indexeerfunctie voor elke partitiebereik. Elke indexeerfunctie heeft tooprocess nu alleen een specifieke partitiebereik, wat resulteert in betere prestaties van query's. Als het Hallo-gegevens die moeten worden geïndexeerd toobe is een klein aantal vaste partities nog beter: elke indexeerfunctie biedt alleen een scan van de partitie. Bijvoorbeeld, toocreate een gegevensbron voor het verwerken van een partitiebereik met sleutels van `000` te`100`, een query als volgt gebruiken: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Als uw gegevens is gepartitioneerd door tijd (bijvoorbeeld: u maakt een nieuwe partitie elke dag of week), overweeg Hallo benadering te volgen: 
    - Gebruik een query Hallo vorm: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Indexeerfunctie voortgang controleren met behulp van [ophalen indexeerfunctie Status API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status), en regelmatig bijwerken Hallo `<TimeStamp>` voorwaarde van Hallo-query op basis van de Hallo meest recente geslaagde high-water-mark. 
    - Met deze methode als u een volledige indexeren tootrigger nodig moet u tooreset Hallo datasource query in toevoeging tooresetting Hallo indexeerfunctie. 


## <a name="help-us-make-azure-search-better"></a>Help ons Azure Search te verbeteren
Als u functieaanvragen of suggesties voor verbeteringen, dient u ze op onze [UserVoice site](https://feedback.azure.com/forums/263029-azure-search/).
