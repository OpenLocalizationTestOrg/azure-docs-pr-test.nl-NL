---
title: aaaAzure gebeurtenis raster abonnement schema
description: Beschrijft eigenschappen Hallo voor geabonneerde tooan-gebeurtenis met gebeurtenis raster van Azure.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: 6a96d67975a5a733c5ea3c56ea54501f94ea4cd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-grid-subscription-schema"></a>Gebeurtenis raster abonnement schema

een abonnement gebeurtenis raster toocreate, verzendt u een aanvraag toohello maken gebeurtenis abonnement opnieuw. Gebruik Hallo volgende indeling:

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Bijvoorbeeld, een gebeurtenisabonnement voor een opslagaccount met de naam toocreate `examplestorage` in een resourcegroep met de naam `examplegroup`, gebruik Hallo volgende notatie:

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

Hallo beschreven Hallo eigenschappen en het schema voor Hallo hoofdtekst van Hallo-aanvraag.
 
## <a name="event-subscription-properties"></a>Eigenschappen van gebeurtenis abonnement

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| Bestemming | object | Hallo-object dat Hallo eindpunt definieert. |
| Filter | object | Een optioneel veld voor het filteren van Hallo typen gebeurtenissen. |

### <a name="destination-object"></a>doelobject

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| endpointType | Tekenreeks | Hallo-type van het eindpunt voor Hallo-abonnement (webhook/HTTP, Event Hub of wachtrij). | 
| bij voor endpointUrl | Tekenreeks |  | 

### <a name="filter-object"></a>Filter-object

| Eigenschap | Type | Beschrijving |
| -------- | ---- | ----------- |
| includedEventTypes | matrix | Komt overeen wanneer Hallo gebeurtenistype in gebeurtenis het Hallo-bericht een exacte overeenkomst tooone van deze gebeurtenis type-namen is. Er wordt een fout bij het gebeurtenisnaam komt niet overeen met de namen van gebeurtenis Hallo geregistreerd voor de gebeurtenisbron Hallo. Standaard komt overeen met alle types van gebeurtenissen. |
| subjectBeginsWith | Tekenreeks | Een voorvoegsel-match toohello onderwerp filterveld in gebeurtenis het Hallo-bericht. Hallo standaardwaarde of een lege tekenreeks komt overeen met alle. | 
| subjectEndsWith | Tekenreeks | Een achtervoegsel-match toohello onderwerp filterveld in gebeurtenis het Hallo-bericht. Hallo standaardwaarde of een lege tekenreeks komt overeen met alle. |
| subjectIsCaseSensitive | Tekenreeks | Hoofdlettergevoelige die overeenkomt met filters voor besturingselementen. |


## <a name="example-subscription-schema"></a>Voorbeeld abonnement schema

```json
{
  "properties": {
    "destination": {
      "endpointType": "webhook",
      "properties": {
          "endpointUrl": "https://example.azurewebsites.net/api/HttpTriggerCSharp1?code=VXbGWce53l48Mt8wuotr0GPmyJ/nDT4hgdFj9DpBiRt38qqnnm5OFg=="
      }
    },
    "filter": {
      "includedEventTypes": [ "blobCreated", "blobDeleted" ],
      "subjectBeginsWith": "blobServices/default/containers/mycontainer/log",
      "subjectEndsWith": ".jpg",
      "subjectIsCaseSensitive": "true"
    }
  }
}
```

## <a name="next-steps"></a>Volgende stappen

* Zie voor een inleiding-tooEvent raster [wat gebeurtenis raster is?](overview.md)
