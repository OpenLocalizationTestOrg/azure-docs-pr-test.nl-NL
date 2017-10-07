---
title: asynchrone bewerkingen aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe tootrack asynchrone bewerkingen in Azure.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Asynchrone bewerkingen voor Azure bijhouden
Sommige Azure REST-bewerkingen asynchroon uitgevoerd omdat het Hallo-bewerking snel kan niet worden voltooid. Dit onderwerp wordt beschreven hoe tootrack Hallo status van asynchrone bewerkingen via waarden geretourneerd in antwoord Hallo.  

## <a name="status-codes-for-asynchronous-operations"></a>Statuscodes voor asynchrone bewerkingen
Een asynchrone bewerking retourneert in eerste instantie een HTTP-statuscode van een van beide:

* 201 (gemaakt)
* 202 (geaccepteerde) 

Wanneer Hallo-bewerking is voltooid, wordt een:

* 200 (OK)
* 204 (geen inhoud) 

Raadpleeg toohello [REST API-documentatie](/rest/api/) toosee Hallo-antwoorden voor Hallo-bewerking die u uitvoert. 

## <a name="monitor-status-of-operation"></a>Monitor status van bewerking
Hallo asynchrone REST operations return headerwaarden, waarin u toodetermine Hallo status van Hallo bewerking. Er worden mogelijk tooexamine van koptekst van drie waarden:

* `Azure-AsyncOperation`-URL voor de controle op Hallo actieve status van Hallo-bewerking. Als de bewerking voor deze waarde retourneert, gebruik altijd it (in plaats van locatie) tootrack Hallo status van Hallo-bewerking.
* `Location`-URL om te bepalen wanneer een bewerking is voltooid. Gebruik deze waarde alleen als Azure-asynchrone bewerking wordt niet geretourneerd.
* `Retry-After`-het aantal seconden toowait voordat het controleren van de status van de asynchrone bewerking Hallo HALLO hallo.

Niet elke asynchrone bewerking retourneert echter al deze waarden. Bijvoorbeeld, moet u mogelijk tooevaluate hello Azure-asynchrone bewerking headerwaarde voor één bewerking en Hallo locatie header-waarde voor een andere bewerking. 

U haalt Hallo headerwaarden zoals u zou een headerwaarde voor een aanvraag voor ophalen. In C#, ophalen u bijvoorbeeld Hallo header-waarde van een `HttpWebResponse` object met de naam `response` Hello code te volgen:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Azure-asynchrone bewerking aanvraag en -antwoord

tooget hello status van de asynchrone bewerking hello, een GET-aanvraag-toohello-URL in Azure-asynchrone bewerking headerwaarde verzenden.

Hallo-hoofdtekst van het Hallo-antwoord van deze bewerking bevat informatie over het Hallo-bewerking. Hallo toont volgende voorbeeld de mogelijke waarden Hallo geretourneerd van Hallo-bewerking:

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Alleen `status` wordt geretourneerd voor alle antwoorden op. Hallo error-object wordt geretourneerd wanneer het Hallo-status is mislukt of geannuleerd. Alle andere waarden zijn optioneel. Daarom antwoord Hallo die u ontvangt mogelijk anders zijn dan Hallo-voorbeeld.

## <a name="provisioningstate-values"></a>provisioningState waarden

Bewerkingen die maken, bijwerken of verwijderen (PUT, PATCH, verwijderen) een resource doorgaans retourneren een `provisioningState` waarde. Wanneer een bewerking is voltooid, wordt de volgende drie waarden geretourneerd: 

* Geslaagd
* Is mislukt
* Geannuleerd

Alle andere waarden geven Hallo-bewerking wordt nog steeds uitgevoerd. Hallo resourceprovider kan een aangepaste waarde die aangeeft van de status geretourneerd. Bijvoorbeeld, krijgt u **geaccepteerde** wanneer Hallo-aanvraag is ontvangen en wordt uitgevoerd.

## <a name="example-requests-and-responses"></a>Voorbeeld aanvragen en antwoorden

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Start de virtuele machine (202 met Azure-asynchrone bewerking)
Dit voorbeeld ziet u hoe toodetermine status van Hallo **start** bewerking voor virtuele machines. de eerste aanvraag Hallo heeft Hallo volgende indeling:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Deze retourneert statuscode 202. U ziet tussen de headerwaarden Hallo:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

toocheck hello status van de asynchrone bewerking hello, het verzenden van een andere aanvraag toothat-URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

antwoordtekst Hallo bevat Hallo status van Hallo-bewerking:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Resources (201 met Azure-asynchrone bewerking) implementeren

Dit voorbeeld ziet u hoe toodetermine status van Hallo **implementaties** bewerking voor het implementeren van resources tooAzure. de eerste aanvraag Hallo heeft Hallo volgende indeling:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Deze retourneert statuscode 201. Hallo-hoofdtekst van antwoord Hallo omvat:

```json
"provisioningState":"Accepted",
```

U ziet tussen de headerwaarden Hallo:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

toocheck hello status van de asynchrone bewerking hello, het verzenden van een andere aanvraag toothat-URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

antwoordtekst Hallo bevat Hallo status van Hallo-bewerking:

```json
{"status":"Running"}
```

Wanneer het Hallo-implementatie is voltooid, bevat het antwoord Hallo:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Storage-account (202 met locatie en probeer het opnieuw na) maken

Dit voorbeeld ziet u hoe toodetermine status Hallo Hallo **maken** bewerking voor storage-accounts. de eerste aanvraag Hallo heeft Hallo volgende indeling:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

En Hallo aanvraagtekst bevat eigenschappen voor het Hallo-opslagaccount:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Deze retourneert statuscode 202. Tussen headerwaarden hello ziet u Hallo na twee waarden:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Na een wachttijd voor het aantal seconden opgegeven in het opnieuw proberen na, Hallo status van de asynchrone bewerking Hallo controleren door het verzenden van een andere aanvraag toothat-URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Als het Hallo-aanvraag wordt nog steeds uitgevoerd, ontvangt u een statuscode 202. Als het Hallo-aanvraag is voltooid, het ontvangen van een statuscode 200 en Hallo hoofdtekst van antwoord Hallo bevat Hallo eigenschappen van Hallo storage-account dat is gemaakt.

## <a name="next-steps"></a>Volgende stappen

* Zie voor documentatie over elke REST-bewerking [REST API-documentatie](/rest/api/).
* Zie voor meer informatie over het beheren van resources via de REST-API van Resource Manager Hallo [Using Hallo REST-API van Resource Manager](resource-manager-rest-api.md).
* Zie voor meer informatie over het implementeren van sjablonen via Hallo REST-API van Resource Manager [resources met Resource Manager-sjablonen en REST-API van Resource Manager implementeren](resource-group-template-deploy-rest.md).
