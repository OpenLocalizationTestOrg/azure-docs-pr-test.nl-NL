---
title: Azure Event raster abonnement schema
description: Beschrijft de eigenschappen voor het abonneren op een gebeurtenis met gebeurtenis raster van Azure.
services: event-grid
author: banisadr
manager: timlt
ms.service: event-grid
ms.topic: article
ms.date: 08/17/2017
ms.author: babanisa
ms.openlocfilehash: eff2352066a76010d6d882a7b7e1961870cd2d46
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="event-grid-subscription-schema"></a><span data-ttu-id="c2d08-103">Gebeurtenis raster abonnement schema</span><span class="sxs-lookup"><span data-stu-id="c2d08-103">Event Grid subscription schema</span></span>

<span data-ttu-id="c2d08-104">Voor het maken van een gebeurtenis raster-abonnement, kunt u een aanvraag verzendt naar het maken van de gebeurtenis abonnement opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c2d08-104">To create an Event Grid subscription, you send a request to the Create Event subscription operation.</span></span> <span data-ttu-id="c2d08-105">Gebruik de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="c2d08-105">Use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/{group-name}/providers/{resource-provider}/{resource-type}/{resource-name}/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="c2d08-106">Bijvoorbeeld, een gebeurtenisabonnement voor een opslagaccount maken met de naam `examplestorage` in een resourcegroep met de naam `examplegroup`, gebruik de volgende notatie:</span><span class="sxs-lookup"><span data-stu-id="c2d08-106">For example, to create an event subscription for a storage account named `examplestorage` in a resource group named `examplegroup`, use the following format:</span></span>

```
PUT /subscriptions/{subscription-id}/resourceGroups/examplegroup/providers/Microsoft.Storage/storageaccounts/examplestorage/Microsoft.EventGrid/eventSubscriptions/{event-type-definitions}?api-version=2017-06-15-preview
``` 

<span data-ttu-id="c2d08-107">Het artikel beschrijft de eigenschappen en het schema voor de hoofdtekst van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c2d08-107">The article describes the properties and schema for the body of the request.</span></span>
 
## <a name="event-subscription-properties"></a><span data-ttu-id="c2d08-108">Eigenschappen van gebeurtenis abonnement</span><span class="sxs-lookup"><span data-stu-id="c2d08-108">Event subscription properties</span></span>

| <span data-ttu-id="c2d08-109">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c2d08-109">Property</span></span> | <span data-ttu-id="c2d08-110">Type</span><span class="sxs-lookup"><span data-stu-id="c2d08-110">Type</span></span> | <span data-ttu-id="c2d08-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2d08-111">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c2d08-112">Bestemming</span><span class="sxs-lookup"><span data-stu-id="c2d08-112">destination</span></span> | <span data-ttu-id="c2d08-113">object</span><span class="sxs-lookup"><span data-stu-id="c2d08-113">object</span></span> | <span data-ttu-id="c2d08-114">Het object dat het eindpunt definieert.</span><span class="sxs-lookup"><span data-stu-id="c2d08-114">The object that defines the endpoint.</span></span> |
| <span data-ttu-id="c2d08-115">Filter</span><span class="sxs-lookup"><span data-stu-id="c2d08-115">filter</span></span> | <span data-ttu-id="c2d08-116">object</span><span class="sxs-lookup"><span data-stu-id="c2d08-116">object</span></span> | <span data-ttu-id="c2d08-117">Een optioneel veld voor het filteren van de typen gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c2d08-117">An optional field for filtering the types of events.</span></span> |

### <a name="destination-object"></a><span data-ttu-id="c2d08-118">doelobject</span><span class="sxs-lookup"><span data-stu-id="c2d08-118">destination object</span></span>

| <span data-ttu-id="c2d08-119">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c2d08-119">Property</span></span> | <span data-ttu-id="c2d08-120">Type</span><span class="sxs-lookup"><span data-stu-id="c2d08-120">Type</span></span> | <span data-ttu-id="c2d08-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2d08-121">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c2d08-122">endpointType</span><span class="sxs-lookup"><span data-stu-id="c2d08-122">endpointType</span></span> | <span data-ttu-id="c2d08-123">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c2d08-123">string</span></span> | <span data-ttu-id="c2d08-124">Het type van het eindpunt voor het abonnement (webhook/HTTP, Event Hub of wachtrij).</span><span class="sxs-lookup"><span data-stu-id="c2d08-124">The type of endpoint for the subscription (webhook/HTTP, Event Hub, or queue).</span></span> | 
| <span data-ttu-id="c2d08-125">bij voor endpointUrl</span><span class="sxs-lookup"><span data-stu-id="c2d08-125">endpointUrl</span></span> | <span data-ttu-id="c2d08-126">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c2d08-126">string</span></span> |  | 

### <a name="filter-object"></a><span data-ttu-id="c2d08-127">Filter-object</span><span class="sxs-lookup"><span data-stu-id="c2d08-127">filter object</span></span>

| <span data-ttu-id="c2d08-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c2d08-128">Property</span></span> | <span data-ttu-id="c2d08-129">Type</span><span class="sxs-lookup"><span data-stu-id="c2d08-129">Type</span></span> | <span data-ttu-id="c2d08-130">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c2d08-130">Description</span></span> |
| -------- | ---- | ----------- |
| <span data-ttu-id="c2d08-131">includedEventTypes</span><span class="sxs-lookup"><span data-stu-id="c2d08-131">includedEventTypes</span></span> | <span data-ttu-id="c2d08-132">matrix</span><span class="sxs-lookup"><span data-stu-id="c2d08-132">array</span></span> | <span data-ttu-id="c2d08-133">Treffer wanneer het gebeurtenistype bericht in de gebeurtenis is een exacte overeenkomst voor een van deze gebeurtenis type-namen.</span><span class="sxs-lookup"><span data-stu-id="c2d08-133">Match when the event type in the event message is an exact match to one of these event type names.</span></span> <span data-ttu-id="c2d08-134">Er wordt een fout bij het gebeurtenisnaam komt niet overeen met de namen van het type geregistreerde gebeurtenis voor de gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="c2d08-134">Raises an error when event name does not match the registered event type names for the event source.</span></span> <span data-ttu-id="c2d08-135">Standaard komt overeen met alle types van gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="c2d08-135">Default matches all event types.</span></span> |
| <span data-ttu-id="c2d08-136">subjectBeginsWith</span><span class="sxs-lookup"><span data-stu-id="c2d08-136">subjectBeginsWith</span></span> | <span data-ttu-id="c2d08-137">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c2d08-137">string</span></span> | <span data-ttu-id="c2d08-138">Een voorvoegsel-overeenkomst filteren op het onderwerpveld in de gebeurtenisstroom bericht.</span><span class="sxs-lookup"><span data-stu-id="c2d08-138">A prefix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="c2d08-139">De standaard- of lege tekenreeks komt overeen met alle.</span><span class="sxs-lookup"><span data-stu-id="c2d08-139">The default or empty string matches all.</span></span> | 
| <span data-ttu-id="c2d08-140">subjectEndsWith</span><span class="sxs-lookup"><span data-stu-id="c2d08-140">subjectEndsWith</span></span> | <span data-ttu-id="c2d08-141">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c2d08-141">string</span></span> | <span data-ttu-id="c2d08-142">Een achtervoegsel-overeenkomst filteren op het onderwerpveld in de gebeurtenisstroom bericht.</span><span class="sxs-lookup"><span data-stu-id="c2d08-142">A suffix-match filter to the subject field in the event message.</span></span> <span data-ttu-id="c2d08-143">De standaard- of lege tekenreeks komt overeen met alle.</span><span class="sxs-lookup"><span data-stu-id="c2d08-143">The default or empty string matches all.</span></span> |
| <span data-ttu-id="c2d08-144">subjectIsCaseSensitive</span><span class="sxs-lookup"><span data-stu-id="c2d08-144">subjectIsCaseSensitive</span></span> | <span data-ttu-id="c2d08-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c2d08-145">string</span></span> | <span data-ttu-id="c2d08-146">Hoofdlettergevoelige die overeenkomt met filters voor besturingselementen.</span><span class="sxs-lookup"><span data-stu-id="c2d08-146">Controls case-sensitive matching for filters.</span></span> |


## <a name="example-subscription-schema"></a><span data-ttu-id="c2d08-147">Voorbeeld abonnement schema</span><span class="sxs-lookup"><span data-stu-id="c2d08-147">Example subscription schema</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="c2d08-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c2d08-148">Next steps</span></span>

* <span data-ttu-id="c2d08-149">Zie voor een inleiding tot gebeurtenis raster, [wat gebeurtenis raster is?](overview.md)</span><span class="sxs-lookup"><span data-stu-id="c2d08-149">For an introduction to Event Grid, see [What is Event Grid?](overview.md)</span></span>