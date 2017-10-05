---
title: Azure asynchrone bewerkingen | Microsoft Docs
description: Beschrijving van het bijhouden van asynchrone bewerkingen in Azure.
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
ms.openlocfilehash: 9fe3d98cd345aae45722295b6c1b7fc3e9036e95
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="5bc87-103">Asynchrone bewerkingen voor Azure bijhouden</span><span class="sxs-lookup"><span data-stu-id="5bc87-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="5bc87-104">Sommige Azure REST-bewerkingen asynchroon uitgevoerd omdat de bewerking kan niet snel worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="5bc87-104">Some Azure REST operations run asynchronously because the operation cannot be completed quickly.</span></span> <span data-ttu-id="5bc87-105">In dit onderwerp wordt beschreven hoe de status van asynchrone bewerkingen via waarden in het antwoord geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5bc87-105">This topic describes how to track the status of asynchronous operations through values returned in the response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="5bc87-106">Statuscodes voor asynchrone bewerkingen</span><span class="sxs-lookup"><span data-stu-id="5bc87-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="5bc87-107">Een asynchrone bewerking retourneert in eerste instantie een HTTP-statuscode van een van beide:</span><span class="sxs-lookup"><span data-stu-id="5bc87-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="5bc87-108">201 (gemaakt)</span><span class="sxs-lookup"><span data-stu-id="5bc87-108">201 (Created)</span></span>
* <span data-ttu-id="5bc87-109">202 (geaccepteerde)</span><span class="sxs-lookup"><span data-stu-id="5bc87-109">202 (Accepted)</span></span> 

<span data-ttu-id="5bc87-110">Wanneer de bewerking is voltooid, wordt een:</span><span class="sxs-lookup"><span data-stu-id="5bc87-110">When the operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="5bc87-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="5bc87-111">200 (OK)</span></span>
* <span data-ttu-id="5bc87-112">204 (geen inhoud)</span><span class="sxs-lookup"><span data-stu-id="5bc87-112">204 (No Content)</span></span> 

<span data-ttu-id="5bc87-113">Raadpleeg de [REST API-documentatie](/rest/api/) om te zien van de antwoorden voor de bewerking die u uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5bc87-113">Refer to the [REST API documentation](/rest/api/) to see the responses for the operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="5bc87-114">Monitor status van bewerking</span><span class="sxs-lookup"><span data-stu-id="5bc87-114">Monitor status of operation</span></span>
<span data-ttu-id="5bc87-115">De asynchrone REST-bewerkingen retourwaarden header die u gebruikt om de status van de bewerking te bepalen.</span><span class="sxs-lookup"><span data-stu-id="5bc87-115">The asynchronous REST operations return header values, which you use to determine the status of the operation.</span></span> <span data-ttu-id="5bc87-116">Er zijn mogelijk drie headerwaarden om te controleren:</span><span class="sxs-lookup"><span data-stu-id="5bc87-116">There are potentially three header values to examine:</span></span>

* <span data-ttu-id="5bc87-117">`Azure-AsyncOperation`-URL voor het controleren van de actieve status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="5bc87-117">`Azure-AsyncOperation` - URL for checking the ongoing status of the operation.</span></span> <span data-ttu-id="5bc87-118">Als de bewerking voor deze waarde retourneert, gebruik altijd het (in plaats van locatie) de status van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="5bc87-118">If your operation returns this value, always use it (instead of Location) to track the status of the operation.</span></span>
* <span data-ttu-id="5bc87-119">`Location`-URL om te bepalen wanneer een bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="5bc87-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="5bc87-120">Gebruik deze waarde alleen als Azure-asynchrone bewerking wordt niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5bc87-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="5bc87-121">`Retry-After`-Het aantal seconden moet worden gewacht voordat de status van de asynchrone bewerking.</span><span class="sxs-lookup"><span data-stu-id="5bc87-121">`Retry-After` - The number of seconds to wait before checking the status of the asynchronous operation.</span></span>

<span data-ttu-id="5bc87-122">Niet elke asynchrone bewerking retourneert echter al deze waarden.</span><span class="sxs-lookup"><span data-stu-id="5bc87-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="5bc87-123">U wilt bijvoorbeeld de waarde van de Azure-asynchrone bewerking header voor één bewerking en de waarde van de locatie-header voor een andere bewerking evalueren.</span><span class="sxs-lookup"><span data-stu-id="5bc87-123">For example, you may need to evaluate the Azure-AsyncOperation header value for one operation, and the Location header value for another operation.</span></span> 

<span data-ttu-id="5bc87-124">U haalt u de waarden van de koptekst als u een headerwaarde voor een aanvraag wilt ophalen.</span><span class="sxs-lookup"><span data-stu-id="5bc87-124">You retrieve the header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="5bc87-125">In C#, ophalen u bijvoorbeeld de waarde van de header van een `HttpWebResponse` object met de naam `response` met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="5bc87-125">For example, in C#, you retrieve the header value from an `HttpWebResponse` object named `response` with the following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="5bc87-126">Azure-asynchrone bewerking aanvraag en -antwoord</span><span class="sxs-lookup"><span data-stu-id="5bc87-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="5bc87-127">Als u de status van de asynchrone bewerking, een GET-aanvraag te verzenden naar de URL in de kopwaarde Azure-asynchrone bewerking.</span><span class="sxs-lookup"><span data-stu-id="5bc87-127">To get the status of the asynchronous operation, send a GET request to the URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="5bc87-128">De hoofdtekst van het antwoord van deze bewerking bevat informatie over het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="5bc87-128">The body of the response from this operation contains information about the operation.</span></span> <span data-ttu-id="5bc87-129">Het volgende voorbeeld ziet u de mogelijke waarden geretourneerd van de bewerking:</span><span class="sxs-lookup"><span data-stu-id="5bc87-129">The following example shows the possible values returned from the operation:</span></span>

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

<span data-ttu-id="5bc87-130">Alleen `status` wordt geretourneerd voor alle antwoorden op.</span><span class="sxs-lookup"><span data-stu-id="5bc87-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="5bc87-131">Het foutobject wordt geretourneerd wanneer de status mislukt of geannuleerd is.</span><span class="sxs-lookup"><span data-stu-id="5bc87-131">The error object is returned when the status is Failed or Canceled.</span></span> <span data-ttu-id="5bc87-132">Alle andere waarden zijn optioneel. daarom het antwoord dat u ontvangt zien er mogelijk anders dan in het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5bc87-132">All other values are optional; therefore, the response you receive may look different than the example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="5bc87-133">provisioningState waarden</span><span class="sxs-lookup"><span data-stu-id="5bc87-133">provisioningState values</span></span>

<span data-ttu-id="5bc87-134">Bewerkingen die maken, bijwerken of verwijderen (PUT, PATCH, verwijderen) een resource doorgaans retourneren een `provisioningState` waarde.</span><span class="sxs-lookup"><span data-stu-id="5bc87-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="5bc87-135">Wanneer een bewerking is voltooid, wordt de volgende drie waarden geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="5bc87-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="5bc87-136">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="5bc87-136">Succeeded</span></span>
* <span data-ttu-id="5bc87-137">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="5bc87-137">Failed</span></span>
* <span data-ttu-id="5bc87-138">Geannuleerd</span><span class="sxs-lookup"><span data-stu-id="5bc87-138">Canceled</span></span>

<span data-ttu-id="5bc87-139">Alle andere waarden geven dat de bewerking wordt nog steeds uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bc87-139">All other values indicate the operation is still running.</span></span> <span data-ttu-id="5bc87-140">De resourceprovider kan een aangepaste waarde die aangeeft van de status retourneren.</span><span class="sxs-lookup"><span data-stu-id="5bc87-140">The resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="5bc87-141">Bijvoorbeeld, krijgt u **geaccepteerde** wanneer de aanvraag is ontvangen en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5bc87-141">For example, you may receive **Accepted** when the request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="5bc87-142">Voorbeeld aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="5bc87-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="5bc87-143">Start de virtuele machine (202 met Azure-asynchrone bewerking)</span><span class="sxs-lookup"><span data-stu-id="5bc87-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="5bc87-144">Dit voorbeeld ziet u hoe u bepaalt de status van **start** bewerking voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="5bc87-144">This example shows how to determine the status of **start** operation for virtual machines.</span></span> <span data-ttu-id="5bc87-145">De eerste aanvraag is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="5bc87-145">The initial request is in the following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="5bc87-146">Deze retourneert statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="5bc87-146">It returns status code 202.</span></span> <span data-ttu-id="5bc87-147">U ziet tussen de headerwaarden:</span><span class="sxs-lookup"><span data-stu-id="5bc87-147">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="5bc87-148">Controleer de status van de asynchrone bewerking, een andere aanvraag verzenden naar deze URL.</span><span class="sxs-lookup"><span data-stu-id="5bc87-148">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="5bc87-149">Hoofdtekst van de reactie bevat de status van de bewerking:</span><span class="sxs-lookup"><span data-stu-id="5bc87-149">The response body contains the status of the operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="5bc87-150">Resources (201 met Azure-asynchrone bewerking) implementeren</span><span class="sxs-lookup"><span data-stu-id="5bc87-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="5bc87-151">Dit voorbeeld ziet u hoe u bepaalt de status van **implementaties** bewerking voor het implementeren van resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="5bc87-151">This example shows how to determine the status of **deployments** operation for deploying resources to Azure.</span></span> <span data-ttu-id="5bc87-152">De eerste aanvraag is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="5bc87-152">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="5bc87-153">Deze retourneert statuscode 201.</span><span class="sxs-lookup"><span data-stu-id="5bc87-153">It returns status code 201.</span></span> <span data-ttu-id="5bc87-154">De hoofdtekst van het antwoord bevat:</span><span class="sxs-lookup"><span data-stu-id="5bc87-154">The body of the response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="5bc87-155">U ziet tussen de headerwaarden:</span><span class="sxs-lookup"><span data-stu-id="5bc87-155">Among the header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="5bc87-156">Controleer de status van de asynchrone bewerking, een andere aanvraag verzenden naar deze URL.</span><span class="sxs-lookup"><span data-stu-id="5bc87-156">To check the status of the asynchronous operation, sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="5bc87-157">Hoofdtekst van de reactie bevat de status van de bewerking:</span><span class="sxs-lookup"><span data-stu-id="5bc87-157">The response body contains the status of the operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="5bc87-158">Wanneer de implementatie is voltooid, wordt het antwoord bevat:</span><span class="sxs-lookup"><span data-stu-id="5bc87-158">When the deployment is finished, the response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="5bc87-159">Storage-account (202 met locatie en probeer het opnieuw na) maken</span><span class="sxs-lookup"><span data-stu-id="5bc87-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="5bc87-160">Dit voorbeeld ziet u hoe u bepaalt de status van de **maken** bewerking voor storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="5bc87-160">This example shows how to determine the status of the **create** operation for storage accounts.</span></span> <span data-ttu-id="5bc87-161">De eerste aanvraag is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="5bc87-161">The initial request is in the following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="5bc87-162">En de hoofdtekst van de aanvraag bevat de eigenschappen voor het opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="5bc87-162">And the request body contains properties for the storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="5bc87-163">Deze retourneert statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="5bc87-163">It returns status code 202.</span></span> <span data-ttu-id="5bc87-164">Tussen de headerwaarden ziet u de volgende twee waarden:</span><span class="sxs-lookup"><span data-stu-id="5bc87-164">Among the header values, you see the following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="5bc87-165">Nadat het wachten op aantal seconden zijn opgegeven in de nieuwe poging na, Controleer de status van de asynchrone bewerking door een andere aanvraag verzenden naar deze URL.</span><span class="sxs-lookup"><span data-stu-id="5bc87-165">After waiting for number of seconds specified in Retry-After, check the status of the asynchronous operation by sending another request to that URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="5bc87-166">Als de aanvraag wordt nog steeds uitgevoerd, ontvangt u een statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="5bc87-166">If the request is still running, you receive a status code 202.</span></span> <span data-ttu-id="5bc87-167">Als de aanvraag is voltooid, de statuscode 200 ontvangt en de hoofdtekst van het antwoord bevat de eigenschappen van het opslagaccount dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5bc87-167">If the request has completed, your receive a status code 200, and the body of the response contains the properties of the storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5bc87-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5bc87-168">Next steps</span></span>

* <span data-ttu-id="5bc87-169">Zie voor documentatie over elke REST-bewerking [REST API-documentatie](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="5bc87-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="5bc87-170">Zie voor meer informatie over het beheren van resources via de REST-API van Resource Manager [met de REST-API van Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="5bc87-170">For information about managing resources through the Resource Manager REST API, see [Using the Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="5bc87-171">Zie voor meer informatie over het implementeren van sjablonen met de REST-API van Resource Manager [resources met Resource Manager-sjablonen en REST-API van Resource Manager implementeren](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="5bc87-171">for information about deploying templates through the Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>