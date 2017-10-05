---
title: Azure Resource Manager-aanvraaglimieten | Microsoft Docs
description: Beschrijft hoe u met Azure Resource Manager-aanvragen beperking als abonnementen hebt bereikt.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: 6d7eeaf460674c3ab98425a5412ffa465b9ffd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="a92e4-103">Beperking van Resource Manager-aanvragen</span><span class="sxs-lookup"><span data-stu-id="a92e4-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="a92e4-104">Voor elk abonnement en de tenant Resource Manager-limieten aanvragen voor 15.000 per uur lezen en schrijven van aanvragen naar 1200 per uur.</span><span class="sxs-lookup"><span data-stu-id="a92e4-104">For each subscription and tenant, Resource Manager limits read requests to 15,000 per hour and write requests to 1,200 per hour.</span></span> <span data-ttu-id="a92e4-105">Deze limieten gelden voor elk exemplaar van Azure Resource Manager; Er zijn meerdere exemplaren in elke Azure-regio en Azure Resource Manager wordt geïmplementeerd op alle Azure-regio's.</span><span class="sxs-lookup"><span data-stu-id="a92e4-105">These limits apply to each Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed to all Azure regions.</span></span>  <span data-ttu-id="a92e4-106">Dus in de praktijk limieten effectief veel hoger dan de zijn hierboven vermelde, als gebruiker worden aanvragen doorgaans afgehandeld door veel verschillende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="a92e4-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="a92e4-107">Als uw toepassing of het script is deze limiet bereikt, moet u uw verzoeken om te beperken.</span><span class="sxs-lookup"><span data-stu-id="a92e4-107">If your application or script reaches these limits, you need to throttle your requests.</span></span> <span data-ttu-id="a92e4-108">In dit onderwerp leest u het bepalen van de resterende aanvragen voordat de limiet bereikt, en hoe moet worden gereageerd wanneer u hebt de limiet bereikt.</span><span class="sxs-lookup"><span data-stu-id="a92e4-108">This topic shows you how to determine the remaining requests you have before reaching the limit, and how to respond when you have reached the limit.</span></span>

<span data-ttu-id="a92e4-109">Wanneer u de limiet bereikt, wordt de HTTP-statuscode **429 te veel aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="a92e4-109">When you reach the limit, you receive the HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="a92e4-110">Het aantal aanvragen is afgestemd op uw abonnement of uw tenant.</span><span class="sxs-lookup"><span data-stu-id="a92e4-110">The number of requests is scoped to either your subscription or your tenant.</span></span> <span data-ttu-id="a92e4-111">Als er meerdere, gelijktijdige toepassingen voor aanvragen die in uw abonnement, het aanvragen van deze toepassingen worden toegevoegd samen om te bepalen het aantal resterende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-111">If you have multiple, concurrent applications making requests in your subscription, the requests from those applications are added together to determine the number of remaining requests.</span></span>

<span data-ttu-id="a92e4-112">Verzoeken om abonnementen binnen het bereik zijn die de betrokken bij het doorgeven van uw abonnement-id, zoals bij het ophalen van de resource-in uw abonnement groepen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-112">Subscription scoped requests are ones the involve passing your subscription id, such as retrieving the resource groups in your subscription.</span></span> <span data-ttu-id="a92e4-113">Aanvragen van de tenant die binnen het bereik van opnemen uw abonnements-id, zoals bij het ophalen van geldige Azure locaties niet.</span><span class="sxs-lookup"><span data-stu-id="a92e4-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="a92e4-114">Overige aanvragen</span><span class="sxs-lookup"><span data-stu-id="a92e4-114">Remaining requests</span></span>
<span data-ttu-id="a92e4-115">U kunt het aantal resterende aanvragen door te onderzoeken antwoordheaders bepalen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-115">You can determine the number of remaining requests by examining response headers.</span></span> <span data-ttu-id="a92e4-116">Elke aanvraag bevat de waarden voor het aantal resterende lees- en schrijfaanvragen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-116">Each request includes values for the number of remaining read and write requests.</span></span> <span data-ttu-id="a92e4-117">De volgende tabel beschrijft de antwoordheaders die u voor deze waarden controleren kunt:</span><span class="sxs-lookup"><span data-stu-id="a92e4-117">The following table describes the response headers you can examine for those values:</span></span>

| <span data-ttu-id="a92e4-118">Reactieheader</span><span class="sxs-lookup"><span data-stu-id="a92e4-118">Response header</span></span> | <span data-ttu-id="a92e4-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a92e4-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a92e4-120">x-MS-ratelimit-Remaining-Subscription-reads</span><span class="sxs-lookup"><span data-stu-id="a92e4-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="a92e4-121">Abonnement bereik leest resterende</span><span class="sxs-lookup"><span data-stu-id="a92e4-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="a92e4-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="a92e4-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="a92e4-123">Abonnement bereik schrijft resterende</span><span class="sxs-lookup"><span data-stu-id="a92e4-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="a92e4-124">x-MS-ratelimit-Remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="a92e4-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="a92e4-125">Tenant bereik leest resterende</span><span class="sxs-lookup"><span data-stu-id="a92e4-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="a92e4-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="a92e4-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="a92e4-127">Tenant bereik schrijft resterende</span><span class="sxs-lookup"><span data-stu-id="a92e4-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="a92e4-128">x-MS-ratelimit-Remaining-Subscription-resource-Requests</span><span class="sxs-lookup"><span data-stu-id="a92e4-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="a92e4-129">Abonnement binnen het bereik van aanvragen van het type resource resterende.</span><span class="sxs-lookup"><span data-stu-id="a92e4-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="a92e4-130">Deze headerwaarde wordt alleen geretourneerd als een service de standaardlimiet is genegeerd.</span><span class="sxs-lookup"><span data-stu-id="a92e4-130">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="a92e4-131">Resource Manager wordt toegevoegd voor deze waarde in plaats van het abonnement lees- of schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-131">Resource Manager adds this value instead of the subscription reads or writes.</span></span> |
| <span data-ttu-id="a92e4-132">x-MS-ratelimit-Remaining-Subscription-resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="a92e4-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="a92e4-133">Abonnement resource type verzameling aanvragen resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="a92e4-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="a92e4-134">Deze headerwaarde wordt alleen geretourneerd als een service de standaardlimiet is genegeerd.</span><span class="sxs-lookup"><span data-stu-id="a92e4-134">This header value is only returned if a service has overridden the default limit.</span></span> <span data-ttu-id="a92e4-135">Deze waarde geeft het aantal resterende verzameling aanvragen (lijst met resources).</span><span class="sxs-lookup"><span data-stu-id="a92e4-135">This value provides the number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="a92e4-136">x-MS-ratelimit-Remaining-tenant-resource-Requests</span><span class="sxs-lookup"><span data-stu-id="a92e4-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="a92e4-137">Tenant aanvragen van het type resource resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="a92e4-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="a92e4-138">Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet overschreven.</span><span class="sxs-lookup"><span data-stu-id="a92e4-138">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> <span data-ttu-id="a92e4-139">Resource Manager wordt toegevoegd voor deze waarde in plaats van de tenant lees- of schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a92e4-139">Resource Manager adds this value instead of the tenant reads or writes.</span></span> |
| <span data-ttu-id="a92e4-140">x-MS-ratelimit-Remaining-tenant-resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="a92e4-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="a92e4-141">Tenant resource type verzameling aanvragen resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="a92e4-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="a92e4-142">Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet overschreven.</span><span class="sxs-lookup"><span data-stu-id="a92e4-142">This header is only added for requests at tenant level, and only if a service has overridden the default limit.</span></span> |

## <a name="retrieving-the-header-values"></a><span data-ttu-id="a92e4-143">De headerwaarden worden opgehaald</span><span class="sxs-lookup"><span data-stu-id="a92e4-143">Retrieving the header values</span></span>
<span data-ttu-id="a92e4-144">Bij het ophalen van deze headerwaarden in uw code of het script is niet anders dan bij het ophalen van een headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="a92e4-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="a92e4-145">Bijvoorbeeld in **C#**, ophalen van de waarde van de header van een **HttpWebResponse** object met de naam **antwoord** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="a92e4-145">For example, in **C#**, you retrieve the header value from an **HttpWebResponse** object named **response** with the following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="a92e4-146">In **PowerShell**, voor het ophalen van de waarde van de header van een bewerking Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="a92e4-146">In **PowerShell**, you retrieve the header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="a92e4-147">Of wilt zien van de resterende aanvragen voor foutopsporing, kunt u opgeven als de **-Debug** parameter op uw **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a92e4-147">Or, if want to see the remaining requests for debugging, you can provide the **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="a92e4-148">Die veel waarden, inclusief de waarde van de volgende antwoord geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a92e4-148">Which returns many values, including the following response value:</span></span>

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

<span data-ttu-id="a92e4-149">In **Azure CLI**, voor het ophalen van de waarde van de header met de uitgebreidere optie.</span><span class="sxs-lookup"><span data-stu-id="a92e4-149">In **Azure CLI**, you retrieve the header value by using the more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="a92e4-150">Die veel waarden, met inbegrip van de volgende object geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="a92e4-150">Which returns many values, including the following object:</span></span>

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="a92e4-151">Wacht voordat het volgende aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="a92e4-151">Waiting before sending next request</span></span>
<span data-ttu-id="a92e4-152">Wanneer u de aanvraaglimiet heeft bereikt, Resource Manager retourneert de **429** HTTP-statuscode en een **opnieuw proberen na** waarde in de header.</span><span class="sxs-lookup"><span data-stu-id="a92e4-152">When you reach the request limit, Resource Manager returns the **429** HTTP status code and a **Retry-After** value in the header.</span></span> <span data-ttu-id="a92e4-153">De **opnieuw proberen na** waarde geeft het aantal seconden dat uw toepassing moet wachten (of slaapstand) voordat u de volgende aanvraag verzendt.</span><span class="sxs-lookup"><span data-stu-id="a92e4-153">The **Retry-After** value specifies the number of seconds your application should wait (or sleep) before sending the next request.</span></span> <span data-ttu-id="a92e4-154">Als u een aanvraag verzenden voordat de waarde voor opnieuw proberen is verstreken, wordt uw aanvraag is niet verwerkt en wordt een nieuwe retry-waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="a92e4-154">If you send a request before the retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a92e4-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a92e4-155">Next steps</span></span>

* <span data-ttu-id="a92e4-156">Zie voor meer informatie over limieten en quota's [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="a92e4-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="a92e4-157">Zie voor meer informatie over het verwerken van asynchrone REST-aanvragen, [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="a92e4-157">To learn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
