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
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="d50b5-103">Gebeurtenis raster abonnement schema</span><span class="sxs-lookup"><span data-stu-id="d50b5-103">Event Grid subscription schema</span></span>

<span data-ttu-id="d50b5-104">een abonnement gebeurtenis raster toocreate, verzendt u een aanvraag toohello maken gebeurtenis abonnement opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d50b5-104">toocreate an Event Grid subscription, you send a request toohello Create Event subscription operation.</span></span> <span data-ttu-id="d50b5-105">Gebruik Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d50b5-105">Use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="d50b5-106">Bijvoorbeeld, een gebeurtenisabonnement voor een opslagaccount met de naam toocreate `examplestorage` in een resourcegroep met de naam `examplegroup`, gebruik Hallo volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="d50b5-106">For example, toocreate an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use hello following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="d50b5-107">Hallo beschreven Hallo eigenschappen en het schema voor Hallo hoofdtekst van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d50b5-107">hello article describes hello properties and schema for hello body of hello request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="d50b5-108">Eigenschappen van gebeurtenis abonnement</span><span class="sxs-lookup"><span data-stu-id="d50b5-108">Event subscription properties</span></span>

| <span data-ttu-id="d50b5-109">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d50b5-109">Property</span></span> | <span data-ttu-id="d50b5-110">Type</span><span class="sxs-lookup"><span data-stu-id="d50b5-110">Type</span></span> | <span data-ttu-id="d50b5-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d50b5-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="d50b5-112">Bestemming</span><span class="sxs-lookup"><span data-stu-id="d50b5-112">destination</span></span> | <span data-ttu-id="d50b5-113">object</span><span class="sxs-lookup"><span data-stu-id="d50b5-113">object</span></span> | <span data-ttu-id="d50b5-114">Hallo-object dat Hallo eindpunt definieert.</span><span class="sxs-lookup"><span data-stu-id="d50b5-114">hello object that defines hello endpoint.</span></span> |
| <span data-ttu-id="d50b5-115">Filter</span><span class="sxs-lookup"><span data-stu-id="d50b5-115">filter</span></span> | <span data-ttu-id="d50b5-116">object</span><span class="sxs-lookup"><span data-stu-id="d50b5-116">object</span></span> | <span data-ttu-id="d50b5-117">Een optioneel veld voor het filteren van Hallo typen gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="d50b5-117">An optional field for filtering hello types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="d50b5-118">doelobject</span><span class="sxs-lookup"><span data-stu-id="d50b5-118">destination object</span></span>

| <span data-ttu-id="d50b5-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d50b5-119">Property</span></span> | <span data-ttu-id="d50b5-120">Type</span><span class="sxs-lookup"><span data-stu-id="d50b5-120">Type</span></span> | <span data-ttu-id="d50b5-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d50b5-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="d50b5-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="d50b5-122">endpointType</span></span> | <span data-ttu-id="d50b5-123">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d50b5-123">string</span></span> | <span data-ttu-id="d50b5-124">Hallo-type van het eindpunt voor Hallo-abonnement (webhook/HTTP, Event Hub of wachtrij).</span><span class="sxs-lookup"><span data-stu-id="d50b5-124">hello type of endpoint for hello subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="d50b5-125">bij voor endpointUrl</span><span class="sxs-lookup"><span data-stu-id="d50b5-125">endpointUrl</span></span> | <span data-ttu-id="d50b5-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d50b5-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="d50b5-127">Filter-object</span><span class="sxs-lookup"><span data-stu-id="d50b5-127">filter object</span></span>

| <span data-ttu-id="d50b5-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d50b5-128">Property</span></span> | <span data-ttu-id="d50b5-129">Type</span><span class="sxs-lookup"><span data-stu-id="d50b5-129">Type</span></span> | <span data-ttu-id="d50b5-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d50b5-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="d50b5-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="d50b5-131">includedEventTypes</span></span> | <span data-ttu-id="d50b5-132">matrix</span><span class="sxs-lookup"><span data-stu-id="d50b5-132">array</span></span> | <span data-ttu-id="d50b5-133">Komt overeen wanneer Hallo gebeurtenistype in gebeurtenis het Hallo-bericht een exacte overeenkomst tooone van deze gebeurtenis type-namen is.</span><span class="sxs-lookup"><span data-stu-id="d50b5-133">Match when hello event type in hello event message is an exact match tooone of these event type names.</span></span> <span data-ttu-id="d50b5-134">Er wordt een fout bij het gebeurtenisnaam komt niet overeen met de namen van gebeurtenis Hallo geregistreerd voor de gebeurtenisbron Hallo.</span><span class="sxs-lookup"><span data-stu-id="d50b5-134">Raises an error when event name does not match hello registered event type names for hello event source.</span></span> <span data-ttu-id="d50b5-135">Standaard komt overeen met alle types van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="d50b5-135">Default matches all event types.</span></span> |
| <span data-ttu-id="d50b5-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="d50b5-136">subjectBeginsWith</span></span> | <span data-ttu-id="d50b5-137">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d50b5-137">string</span></span> | <span data-ttu-id="d50b5-138">Een voorvoegsel-match toohello onderwerp filterveld in gebeurtenis het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="d50b5-138">A prefix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="d50b5-139">Hallo standaardwaarde of een lege tekenreeks komt overeen met alle.</span><span class="sxs-lookup"><span data-stu-id="d50b5-139">hello default or empty string matches all.</span></span> | 
| <span data-ttu-id="d50b5-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="d50b5-140">subjectEndsWith</span></span> | <span data-ttu-id="d50b5-141">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d50b5-141">string</span></span> | <span data-ttu-id="d50b5-142">Een achtervoegsel-match toohello onderwerp filterveld in gebeurtenis het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="d50b5-142">A suffix-match filter toohello subject field in hello event message.</span></span> <span data-ttu-id="d50b5-143">Hallo standaardwaarde of een lege tekenreeks komt overeen met alle.</span><span class="sxs-lookup"><span data-stu-id="d50b5-143">hello default or empty string matches all.</span></span> |
| <span data-ttu-id="d50b5-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="d50b5-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="d50b5-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="d50b5-145">string</span></span> | <span data-ttu-id="d50b5-146">Hoofdlettergevoelige die overeenkomt met filters voor besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="d50b5-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="d50b5-147">Voorbeeld abonnement schema</span><span class="sxs-lookup"><span data-stu-id="d50b5-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d50b5-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d50b5-148">Next steps</span></span>

* <span data-ttu-id="d50b5-149">Zie voor een inleiding-tooEvent raster [wat gebeurtenis raster is?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="d50b5-149">For an introduction tooEvent Grid, see [What is Event Grid?](overview.md)</span></span>
