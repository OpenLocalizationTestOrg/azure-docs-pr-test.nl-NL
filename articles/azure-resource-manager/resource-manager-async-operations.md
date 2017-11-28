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
# <a name="track-asynchronous-azure-operations"></a><span data-ttu-id="161cc-103">Asynchrone bewerkingen voor Azure bijhouden</span><span class="sxs-lookup"><span data-stu-id="161cc-103">Track asynchronous Azure operations</span></span>
<span data-ttu-id="161cc-104">Sommige Azure REST-bewerkingen asynchroon uitgevoerd omdat het Hallo-bewerking snel kan niet worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="161cc-104">Some Azure REST operations run asynchronously because hello operation cannot be completed quickly.</span></span> <span data-ttu-id="161cc-105">Dit onderwerp wordt beschreven hoe tootrack Hallo status van asynchrone bewerkingen via waarden geretourneerd in antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="161cc-105">This topic describes how tootrack hello status of asynchronous operations through values returned in hello response.</span></span>  

## <a name="status-codes-for-asynchronous-operations"></a><span data-ttu-id="161cc-106">Statuscodes voor asynchrone bewerkingen</span><span class="sxs-lookup"><span data-stu-id="161cc-106">Status codes for asynchronous operations</span></span>
<span data-ttu-id="161cc-107">Een asynchrone bewerking retourneert in eerste instantie een HTTP-statuscode van een van beide:</span><span class="sxs-lookup"><span data-stu-id="161cc-107">An asynchronous operation initially returns an HTTP status code of either:</span></span>

* <span data-ttu-id="161cc-108">201 (gemaakt)</span><span class="sxs-lookup"><span data-stu-id="161cc-108">201 (Created)</span></span>
* <span data-ttu-id="161cc-109">202 (geaccepteerde)</span><span class="sxs-lookup"><span data-stu-id="161cc-109">202 (Accepted)</span></span> 

<span data-ttu-id="161cc-110">Wanneer Hallo-bewerking is voltooid, wordt een:</span><span class="sxs-lookup"><span data-stu-id="161cc-110">When hello operation successfully completes, it returns either:</span></span>

* <span data-ttu-id="161cc-111">200 (OK)</span><span class="sxs-lookup"><span data-stu-id="161cc-111">200 (OK)</span></span>
* <span data-ttu-id="161cc-112">204 (geen inhoud)</span><span class="sxs-lookup"><span data-stu-id="161cc-112">204 (No Content)</span></span> 

<span data-ttu-id="161cc-113">Raadpleeg toohello [REST API-documentatie](/rest/api/) toosee Hallo-antwoorden voor Hallo-bewerking die u uitvoert.</span><span class="sxs-lookup"><span data-stu-id="161cc-113">Refer toohello [REST API documentation](/rest/api/) toosee hello responses for hello operation you are executing.</span></span> 

## <a name="monitor-status-of-operation"></a><span data-ttu-id="161cc-114">Monitor status van bewerking</span><span class="sxs-lookup"><span data-stu-id="161cc-114">Monitor status of operation</span></span>
<span data-ttu-id="161cc-115">Hallo asynchrone REST operations return headerwaarden, waarin u toodetermine Hallo status van Hallo bewerking.</span><span class="sxs-lookup"><span data-stu-id="161cc-115">hello asynchronous REST operations return header values, which you use toodetermine hello status of hello operation.</span></span> <span data-ttu-id="161cc-116">Er worden mogelijk tooexamine van koptekst van drie waarden:</span><span class="sxs-lookup"><span data-stu-id="161cc-116">There are potentially three header values tooexamine:</span></span>

* <span data-ttu-id="161cc-117">`Azure-AsyncOperation`-URL voor de controle op Hallo actieve status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="161cc-117">`Azure-AsyncOperation` - URL for checking hello ongoing status of hello operation.</span></span> <span data-ttu-id="161cc-118">Als de bewerking voor deze waarde retourneert, gebruik altijd it (in plaats van locatie) tootrack Hallo status van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="161cc-118">If your operation returns this value, always use it (instead of Location) tootrack hello status of hello operation.</span></span>
* <span data-ttu-id="161cc-119">`Location`-URL om te bepalen wanneer een bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="161cc-119">`Location` - URL for determining when an operation has completed.</span></span> <span data-ttu-id="161cc-120">Gebruik deze waarde alleen als Azure-asynchrone bewerking wordt niet geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="161cc-120">Use this value only when Azure-AsyncOperation is not returned.</span></span>
* <span data-ttu-id="161cc-121">`Retry-After`-het aantal seconden toowait voordat het controleren van de status van de asynchrone bewerking Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="161cc-121">`Retry-After` - hello number of seconds toowait before checking hello status of hello asynchronous operation.</span></span>

<span data-ttu-id="161cc-122">Niet elke asynchrone bewerking retourneert echter al deze waarden.</span><span class="sxs-lookup"><span data-stu-id="161cc-122">However, not every asynchronous operation returns all these values.</span></span> <span data-ttu-id="161cc-123">Bijvoorbeeld, moet u mogelijk tooevaluate hello Azure-asynchrone bewerking headerwaarde voor één bewerking en Hallo locatie header-waarde voor een andere bewerking.</span><span class="sxs-lookup"><span data-stu-id="161cc-123">For example, you may need tooevaluate hello Azure-AsyncOperation header value for one operation, and hello Location header value for another operation.</span></span> 

<span data-ttu-id="161cc-124">U haalt Hallo headerwaarden zoals u zou een headerwaarde voor een aanvraag voor ophalen.</span><span class="sxs-lookup"><span data-stu-id="161cc-124">You retrieve hello header values as you would retrieve any header value for a request.</span></span> <span data-ttu-id="161cc-125">In C#, ophalen u bijvoorbeeld Hallo header-waarde van een `HttpWebResponse` object met de naam `response` Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="161cc-125">For example, in C#, you retrieve hello header value from an `HttpWebResponse` object named `response` with hello following code:</span></span>

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a><span data-ttu-id="161cc-126">Azure-asynchrone bewerking aanvraag en -antwoord</span><span class="sxs-lookup"><span data-stu-id="161cc-126">Azure-AsyncOperation request and response</span></span>

<span data-ttu-id="161cc-127">tooget hello status van de asynchrone bewerking hello, een GET-aanvraag-toohello-URL in Azure-asynchrone bewerking headerwaarde verzenden.</span><span class="sxs-lookup"><span data-stu-id="161cc-127">tooget hello status of hello asynchronous operation, send a GET request toohello URL in Azure-AsyncOperation header value.</span></span>

<span data-ttu-id="161cc-128">Hallo-hoofdtekst van het Hallo-antwoord van deze bewerking bevat informatie over het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="161cc-128">hello body of hello response from this operation contains information about hello operation.</span></span> <span data-ttu-id="161cc-129">Hallo toont volgende voorbeeld de mogelijke waarden Hallo geretourneerd van Hallo-bewerking:</span><span class="sxs-lookup"><span data-stu-id="161cc-129">hello following example shows hello possible values returned from hello operation:</span></span>

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

<span data-ttu-id="161cc-130">Alleen `status` wordt geretourneerd voor alle antwoorden op.</span><span class="sxs-lookup"><span data-stu-id="161cc-130">Only `status` is returned for all responses.</span></span> <span data-ttu-id="161cc-131">Hallo error-object wordt geretourneerd wanneer het Hallo-status is mislukt of geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="161cc-131">hello error object is returned when hello status is Failed or Canceled.</span></span> <span data-ttu-id="161cc-132">Alle andere waarden zijn optioneel. Daarom antwoord Hallo die u ontvangt mogelijk anders zijn dan Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="161cc-132">All other values are optional; therefore, hello response you receive may look different than hello example.</span></span>

## <a name="provisioningstate-values"></a><span data-ttu-id="161cc-133">provisioningState waarden</span><span class="sxs-lookup"><span data-stu-id="161cc-133">provisioningState values</span></span>

<span data-ttu-id="161cc-134">Bewerkingen die maken, bijwerken of verwijderen (PUT, PATCH, verwijderen) een resource doorgaans retourneren een `provisioningState` waarde.</span><span class="sxs-lookup"><span data-stu-id="161cc-134">Operations that create, update, or delete (PUT, PATCH, DELETE) a resource typically return a `provisioningState` value.</span></span> <span data-ttu-id="161cc-135">Wanneer een bewerking is voltooid, wordt de volgende drie waarden geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="161cc-135">When an operation has completed, one of following three values is returned:</span></span> 

* <span data-ttu-id="161cc-136">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="161cc-136">Succeeded</span></span>
* <span data-ttu-id="161cc-137">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="161cc-137">Failed</span></span>
* <span data-ttu-id="161cc-138">Geannuleerd</span><span class="sxs-lookup"><span data-stu-id="161cc-138">Canceled</span></span>

<span data-ttu-id="161cc-139">Alle andere waarden geven Hallo-bewerking wordt nog steeds uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="161cc-139">All other values indicate hello operation is still running.</span></span> <span data-ttu-id="161cc-140">Hallo resourceprovider kan een aangepaste waarde die aangeeft van de status geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="161cc-140">hello resource provider can return a customized value that indicates its state.</span></span> <span data-ttu-id="161cc-141">Bijvoorbeeld, krijgt u **geaccepteerde** wanneer Hallo-aanvraag is ontvangen en wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="161cc-141">For example, you may receive **Accepted** when hello request is received and running.</span></span>

## <a name="example-requests-and-responses"></a><span data-ttu-id="161cc-142">Voorbeeld aanvragen en antwoorden</span><span class="sxs-lookup"><span data-stu-id="161cc-142">Example requests and responses</span></span>

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a><span data-ttu-id="161cc-143">Start de virtuele machine (202 met Azure-asynchrone bewerking)</span><span class="sxs-lookup"><span data-stu-id="161cc-143">Start virtual machine (202 with Azure-AsyncOperation)</span></span>
<span data-ttu-id="161cc-144">Dit voorbeeld ziet u hoe toodetermine status van Hallo **start** bewerking voor virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="161cc-144">This example shows how toodetermine hello status of **start** operation for virtual machines.</span></span> <span data-ttu-id="161cc-145">de eerste aanvraag Hallo heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="161cc-145">hello initial request is in hello following format:</span></span>

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

<span data-ttu-id="161cc-146">Deze retourneert statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="161cc-146">It returns status code 202.</span></span> <span data-ttu-id="161cc-147">U ziet tussen de headerwaarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="161cc-147">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="161cc-148">toocheck hello status van de asynchrone bewerking hello, het verzenden van een andere aanvraag toothat-URL.</span><span class="sxs-lookup"><span data-stu-id="161cc-148">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

<span data-ttu-id="161cc-149">antwoordtekst Hallo bevat Hallo status van Hallo-bewerking:</span><span class="sxs-lookup"><span data-stu-id="161cc-149">hello response body contains hello status of hello operation:</span></span>

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a><span data-ttu-id="161cc-150">Resources (201 met Azure-asynchrone bewerking) implementeren</span><span class="sxs-lookup"><span data-stu-id="161cc-150">Deploy resources (201 with Azure-AsyncOperation)</span></span>

<span data-ttu-id="161cc-151">Dit voorbeeld ziet u hoe toodetermine status van Hallo **implementaties** bewerking voor het implementeren van resources tooAzure.</span><span class="sxs-lookup"><span data-stu-id="161cc-151">This example shows how toodetermine hello status of **deployments** operation for deploying resources tooAzure.</span></span> <span data-ttu-id="161cc-152">de eerste aanvraag Hallo heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="161cc-152">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

<span data-ttu-id="161cc-153">Deze retourneert statuscode 201.</span><span class="sxs-lookup"><span data-stu-id="161cc-153">It returns status code 201.</span></span> <span data-ttu-id="161cc-154">Hallo-hoofdtekst van antwoord Hallo omvat:</span><span class="sxs-lookup"><span data-stu-id="161cc-154">hello body of hello response includes:</span></span>

```json
"provisioningState":"Accepted",
```

<span data-ttu-id="161cc-155">U ziet tussen de headerwaarden Hallo:</span><span class="sxs-lookup"><span data-stu-id="161cc-155">Among hello header values, you see:</span></span>

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="161cc-156">toocheck hello status van de asynchrone bewerking hello, het verzenden van een andere aanvraag toothat-URL.</span><span class="sxs-lookup"><span data-stu-id="161cc-156">toocheck hello status of hello asynchronous operation, sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

<span data-ttu-id="161cc-157">antwoordtekst Hallo bevat Hallo status van Hallo-bewerking:</span><span class="sxs-lookup"><span data-stu-id="161cc-157">hello response body contains hello status of hello operation:</span></span>

```json
{"status":"Running"}
```

<span data-ttu-id="161cc-158">Wanneer het Hallo-implementatie is voltooid, bevat het antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="161cc-158">When hello deployment is finished, hello response contains:</span></span>

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a><span data-ttu-id="161cc-159">Storage-account (202 met locatie en probeer het opnieuw na) maken</span><span class="sxs-lookup"><span data-stu-id="161cc-159">Create storage account (202 with Location and Retry-After)</span></span>

<span data-ttu-id="161cc-160">Dit voorbeeld ziet u hoe toodetermine status Hallo Hallo **maken** bewerking voor storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="161cc-160">This example shows how toodetermine hello status of hello **create** operation for storage accounts.</span></span> <span data-ttu-id="161cc-161">de eerste aanvraag Hallo heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="161cc-161">hello initial request is in hello following format:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

<span data-ttu-id="161cc-162">En Hallo aanvraagtekst bevat eigenschappen voor het Hallo-opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="161cc-162">And hello request body contains properties for hello storage account:</span></span>

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

<span data-ttu-id="161cc-163">Deze retourneert statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="161cc-163">It returns status code 202.</span></span> <span data-ttu-id="161cc-164">Tussen headerwaarden hello ziet u Hallo na twee waarden:</span><span class="sxs-lookup"><span data-stu-id="161cc-164">Among hello header values, you see hello following two values:</span></span>

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

<span data-ttu-id="161cc-165">Na een wachttijd voor het aantal seconden opgegeven in het opnieuw proberen na, Hallo status van de asynchrone bewerking Hallo controleren door het verzenden van een andere aanvraag toothat-URL.</span><span class="sxs-lookup"><span data-stu-id="161cc-165">After waiting for number of seconds specified in Retry-After, check hello status of hello asynchronous operation by sending another request toothat URL.</span></span>

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

<span data-ttu-id="161cc-166">Als het Hallo-aanvraag wordt nog steeds uitgevoerd, ontvangt u een statuscode 202.</span><span class="sxs-lookup"><span data-stu-id="161cc-166">If hello request is still running, you receive a status code 202.</span></span> <span data-ttu-id="161cc-167">Als het Hallo-aanvraag is voltooid, het ontvangen van een statuscode 200 en Hallo hoofdtekst van antwoord Hallo bevat Hallo eigenschappen van Hallo storage-account dat is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="161cc-167">If hello request has completed, your receive a status code 200, and hello body of hello response contains hello properties of hello storage account that has been created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="161cc-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="161cc-168">Next steps</span></span>

* <span data-ttu-id="161cc-169">Zie voor documentatie over elke REST-bewerking [REST API-documentatie](/rest/api/).</span><span class="sxs-lookup"><span data-stu-id="161cc-169">For documentation about each REST operation, see [REST API documentation](/rest/api/).</span></span>
* <span data-ttu-id="161cc-170">Zie voor meer informatie over het beheren van resources via de REST-API van Resource Manager Hallo [Using Hallo REST-API van Resource Manager](resource-manager-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="161cc-170">For information about managing resources through hello Resource Manager REST API, see [Using hello Resource Manager REST API](resource-manager-rest-api.md).</span></span>
* <span data-ttu-id="161cc-171">Zie voor meer informatie over het implementeren van sjablonen via Hallo REST-API van Resource Manager [resources met Resource Manager-sjablonen en REST-API van Resource Manager implementeren](resource-group-template-deploy-rest.md).</span><span class="sxs-lookup"><span data-stu-id="161cc-171">for information about deploying templates through hello Resource Manager REST API, see [Deploy resources with Resource Manager templates and Resource Manager REST API](resource-group-template-deploy-rest.md).</span></span>
