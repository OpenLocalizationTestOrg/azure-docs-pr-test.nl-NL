---
title: Resource Manager-aanvraaglimieten aaaAzure | Microsoft Docs
description: Hierin wordt beschreven hoe toouse beperking met Azure Resource Manager vraagt als abonnementen is bereikt.
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
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a><span data-ttu-id="45b39-103">Beperking van Resource Manager-aanvragen</span><span class="sxs-lookup"><span data-stu-id="45b39-103">Throttling Resource Manager requests</span></span>
<span data-ttu-id="45b39-104">Voor elk abonnement en de tenant, limieten voor Resource Manager aanvragen too15, 000 per uur lezen en schrijven aanvragen too1, 200 per uur.</span><span class="sxs-lookup"><span data-stu-id="45b39-104">For each subscription and tenant, Resource Manager limits read requests too15,000 per hour and write requests too1,200 per hour.</span></span> <span data-ttu-id="45b39-105">Deze limieten gelden tooeach Azure Resource Manager-instantie; Er zijn meerdere exemplaren in elke Azure-regio en Azure Resource Manager geïmplementeerde tooall Azure is regio's.</span><span class="sxs-lookup"><span data-stu-id="45b39-105">These limits apply tooeach Azure Resource Manager instance; there are multiple instances in every Azure region, and Azure Resource Manager is deployed tooall Azure regions.</span></span>  <span data-ttu-id="45b39-106">Dus in de praktijk limieten effectief veel hoger dan de zijn hierboven vermelde, als gebruiker worden aanvragen doorgaans afgehandeld door veel verschillende exemplaren.</span><span class="sxs-lookup"><span data-stu-id="45b39-106">So, in practice, limits are effectively much higher than those listed above, as user requests are generally serviced by many different instances.</span></span>

<span data-ttu-id="45b39-107">Als uw toepassing of het script is deze limiet bereikt, moet u toothrottle uw aanvragen.</span><span class="sxs-lookup"><span data-stu-id="45b39-107">If your application or script reaches these limits, you need toothrottle your requests.</span></span> <span data-ttu-id="45b39-108">Dit onderwerp leest u hoe toodetermine Hallo resterende aanvragen voordat het Hallo-limiet bereikt, en hoe toorespond wanneer u Hallo limiet hebt bereikt.</span><span class="sxs-lookup"><span data-stu-id="45b39-108">This topic shows you how toodetermine hello remaining requests you have before reaching hello limit, and how toorespond when you have reached hello limit.</span></span>

<span data-ttu-id="45b39-109">Wanneer u Hallo-limiet bereikt, ontvangt u Hallo HTTP-statuscode **429 te veel aanvragen**.</span><span class="sxs-lookup"><span data-stu-id="45b39-109">When you reach hello limit, you receive hello HTTP status code **429 Too many requests**.</span></span>

<span data-ttu-id="45b39-110">het aantal aanvragen Hallo bereik tooeither is uw abonnement of uw tenant.</span><span class="sxs-lookup"><span data-stu-id="45b39-110">hello number of requests is scoped tooeither your subscription or your tenant.</span></span> <span data-ttu-id="45b39-111">Als er meerdere, gelijktijdige toepassingen voor aanvragen die in uw abonnement Hallo aanvragen van deze toepassingen opgeteld toodetermine Hallo aantal resterende aanvragen.</span><span class="sxs-lookup"><span data-stu-id="45b39-111">If you have multiple, concurrent applications making requests in your subscription, hello requests from those applications are added together toodetermine hello number of remaining requests.</span></span>

<span data-ttu-id="45b39-112">Verzoeken om abonnementen binnen het bereik zijn toepassingsgroepen Hallo betrekking hebben op uw abonnements-id, zoals bij het ophalen van Hallo resourcegroepen in uw abonnement wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="45b39-112">Subscription scoped requests are ones hello involve passing your subscription id, such as retrieving hello resource groups in your subscription.</span></span> <span data-ttu-id="45b39-113">Aanvragen van de tenant die binnen het bereik van opnemen uw abonnements-id, zoals bij het ophalen van geldige Azure locaties niet.</span><span class="sxs-lookup"><span data-stu-id="45b39-113">Tenant scoped requests do not include your subscription id, such as retrieving valid Azure locations.</span></span>

## <a name="remaining-requests"></a><span data-ttu-id="45b39-114">Overige aanvragen</span><span class="sxs-lookup"><span data-stu-id="45b39-114">Remaining requests</span></span>
<span data-ttu-id="45b39-115">Het aantal resterende aanvragen Hallo kunt u bepalen aan de hand van antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="45b39-115">You can determine hello number of remaining requests by examining response headers.</span></span> <span data-ttu-id="45b39-116">Elke aanvraag bevat de waarden voor Hallo aantal resterende lees- en schrijfaanvragen.</span><span class="sxs-lookup"><span data-stu-id="45b39-116">Each request includes values for hello number of remaining read and write requests.</span></span> <span data-ttu-id="45b39-117">Hallo staan volgende tabel Hallo antwoordheaders die u voor deze waarden kunt controleren:</span><span class="sxs-lookup"><span data-stu-id="45b39-117">hello following table describes hello response headers you can examine for those values:</span></span>

| <span data-ttu-id="45b39-118">Reactieheader</span><span class="sxs-lookup"><span data-stu-id="45b39-118">Response header</span></span> | <span data-ttu-id="45b39-119">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="45b39-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45b39-120">x-MS-ratelimit-Remaining-Subscription-reads</span><span class="sxs-lookup"><span data-stu-id="45b39-120">x-ms-ratelimit-remaining-subscription-reads</span></span> |<span data-ttu-id="45b39-121">Abonnement bereik leest resterende</span><span class="sxs-lookup"><span data-stu-id="45b39-121">Subscription scoped reads remaining</span></span> |
| <span data-ttu-id="45b39-122">x-MS-ratelimit-Remaining-Subscription-Writes</span><span class="sxs-lookup"><span data-stu-id="45b39-122">x-ms-ratelimit-remaining-subscription-writes</span></span> |<span data-ttu-id="45b39-123">Abonnement bereik schrijft resterende</span><span class="sxs-lookup"><span data-stu-id="45b39-123">Subscription scoped writes remaining</span></span> |
| <span data-ttu-id="45b39-124">x-MS-ratelimit-Remaining-tenant-reads</span><span class="sxs-lookup"><span data-stu-id="45b39-124">x-ms-ratelimit-remaining-tenant-reads</span></span> |<span data-ttu-id="45b39-125">Tenant bereik leest resterende</span><span class="sxs-lookup"><span data-stu-id="45b39-125">Tenant scoped reads remaining</span></span> |
| <span data-ttu-id="45b39-126">x-MS-ratelimit-Remaining-tenant-Writes</span><span class="sxs-lookup"><span data-stu-id="45b39-126">x-ms-ratelimit-remaining-tenant-writes</span></span> |<span data-ttu-id="45b39-127">Tenant bereik schrijft resterende</span><span class="sxs-lookup"><span data-stu-id="45b39-127">Tenant scoped writes remaining</span></span> |
| <span data-ttu-id="45b39-128">x-MS-ratelimit-Remaining-Subscription-resource-Requests</span><span class="sxs-lookup"><span data-stu-id="45b39-128">x-ms-ratelimit-remaining-subscription-resource-requests</span></span> |<span data-ttu-id="45b39-129">Abonnement binnen het bereik van aanvragen van het type resource resterende.</span><span class="sxs-lookup"><span data-stu-id="45b39-129">Subscription scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="45b39-130">Deze headerwaarde wordt alleen geretourneerd als een service Hallo standaardlimiet is genegeerd.</span><span class="sxs-lookup"><span data-stu-id="45b39-130">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="45b39-131">Resource Manager wordt toegevoegd voor deze waarde in plaats van Hallo abonnement lees- of schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="45b39-131">Resource Manager adds this value instead of hello subscription reads or writes.</span></span> |
| <span data-ttu-id="45b39-132">x-MS-ratelimit-Remaining-Subscription-resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="45b39-132">x-ms-ratelimit-remaining-subscription-resource-entities-read</span></span> |<span data-ttu-id="45b39-133">Abonnement resource type verzameling aanvragen resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="45b39-133">Subscription scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="45b39-134">Deze headerwaarde wordt alleen geretourneerd als een service Hallo standaardlimiet is genegeerd.</span><span class="sxs-lookup"><span data-stu-id="45b39-134">This header value is only returned if a service has overridden hello default limit.</span></span> <span data-ttu-id="45b39-135">Deze waarde biedt Hallo aantal aanvragen voor resterende (lijst met resources).</span><span class="sxs-lookup"><span data-stu-id="45b39-135">This value provides hello number of remaining collection requests (list resources).</span></span> |
| <span data-ttu-id="45b39-136">x-MS-ratelimit-Remaining-tenant-resource-Requests</span><span class="sxs-lookup"><span data-stu-id="45b39-136">x-ms-ratelimit-remaining-tenant-resource-requests</span></span> |<span data-ttu-id="45b39-137">Tenant aanvragen van het type resource resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="45b39-137">Tenant scoped resource type requests remaining.</span></span><br /><br /><span data-ttu-id="45b39-138">Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet hallo overschreven.</span><span class="sxs-lookup"><span data-stu-id="45b39-138">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> <span data-ttu-id="45b39-139">Resource Manager wordt toegevoegd voor deze waarde in plaats van Hallo tenant lees- of schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="45b39-139">Resource Manager adds this value instead of hello tenant reads or writes.</span></span> |
| <span data-ttu-id="45b39-140">x-MS-ratelimit-Remaining-tenant-resource-ENTITIES-Read</span><span class="sxs-lookup"><span data-stu-id="45b39-140">x-ms-ratelimit-remaining-tenant-resource-entities-read</span></span> |<span data-ttu-id="45b39-141">Tenant resource type verzameling aanvragen resterende binnen het bereik.</span><span class="sxs-lookup"><span data-stu-id="45b39-141">Tenant scoped resource type collection requests remaining.</span></span><br /><br /><span data-ttu-id="45b39-142">Deze header alleen voor aanvragen op niveau van de tenant is toegevoegd en alleen als een service heeft de standaardlimiet hallo overschreven.</span><span class="sxs-lookup"><span data-stu-id="45b39-142">This header is only added for requests at tenant level, and only if a service has overridden hello default limit.</span></span> |

## <a name="retrieving-hello-header-values"></a><span data-ttu-id="45b39-143">Hallo-headerwaarden ophalen</span><span class="sxs-lookup"><span data-stu-id="45b39-143">Retrieving hello header values</span></span>
<span data-ttu-id="45b39-144">Bij het ophalen van deze headerwaarden in uw code of het script is niet anders dan bij het ophalen van een headerwaarde.</span><span class="sxs-lookup"><span data-stu-id="45b39-144">Retrieving these header values in your code or script is no different than retrieving any header value.</span></span> 

<span data-ttu-id="45b39-145">Bijvoorbeeld in **C#**, ophalen van Hallo header-waarde van een **HttpWebResponse** object met de naam **antwoord** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="45b39-145">For example, in **C#**, you retrieve hello header value from an **HttpWebResponse** object named **response** with hello following code:</span></span>

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

<span data-ttu-id="45b39-146">In **PowerShell**, u Hallo header-waarde wordt opgehaald uit een bewerking Invoke-WebRequest.</span><span class="sxs-lookup"><span data-stu-id="45b39-146">In **PowerShell**, you retrieve hello header value from an Invoke-WebRequest operation.</span></span>

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

<span data-ttu-id="45b39-147">Of, indien het gewenste toosee Hallo resterende aanvragen voor foutopsporing, kunt u Hallo bieden **-Debug** parameter op uw **PowerShell** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="45b39-147">Or, if want toosee hello remaining requests for debugging, you can provide hello **-Debug** parameter on your **PowerShell** cmdlet.</span></span>

```powershell
Get-AzureRmResourceGroup -Debug
```

<span data-ttu-id="45b39-148">Die veel waarden, waaronder Hallo na antwoord-waarde geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="45b39-148">Which returns many values, including hello following response value:</span></span>

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

<span data-ttu-id="45b39-149">In **Azure CLI**, u Hallo headerwaarde ophalen met behulp van Hallo uitgebreidere optie.</span><span class="sxs-lookup"><span data-stu-id="45b39-149">In **Azure CLI**, you retrieve hello header value by using hello more verbose option.</span></span>

```azurecli
azure group list -vv --json
```

<span data-ttu-id="45b39-150">Die veel waarden, waaronder Hallo na-object geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="45b39-150">Which returns many values, including hello following object:</span></span>

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

## <a name="waiting-before-sending-next-request"></a><span data-ttu-id="45b39-151">Wacht voordat het volgende aanvraag verzenden</span><span class="sxs-lookup"><span data-stu-id="45b39-151">Waiting before sending next request</span></span>
<span data-ttu-id="45b39-152">Wanneer u Hallo aanvraaglimiet heeft bereikt, Resource Manager Hallo retourneert **429** HTTP-statuscode en een **opnieuw proberen na** waarde in Hallo-header.</span><span class="sxs-lookup"><span data-stu-id="45b39-152">When you reach hello request limit, Resource Manager returns hello **429** HTTP status code and a **Retry-After** value in hello header.</span></span> <span data-ttu-id="45b39-153">Hallo **opnieuw proberen na** waarde geeft Hallo aantal seconden dat uw toepassing moet wachten (of slaapstand) voordat u de volgende aanvraag Hallo verzendt.</span><span class="sxs-lookup"><span data-stu-id="45b39-153">hello **Retry-After** value specifies hello number of seconds your application should wait (or sleep) before sending hello next request.</span></span> <span data-ttu-id="45b39-154">Als u een aanvraag verzenden voordat het Hallo-waarde voor opnieuw proberen is verstreken, wordt uw aanvraag is niet verwerkt en wordt een nieuwe retry-waarde geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="45b39-154">If you send a request before hello retry value has elapsed, your request is not processed and a new retry value is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45b39-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="45b39-155">Next steps</span></span>

* <span data-ttu-id="45b39-156">Zie voor meer informatie over limieten en quota's [Azure-abonnement en Servicelimieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="45b39-156">For more information about limits and quotas, see [Azure subscription and service limits, quotas, and constraints](../azure-subscription-service-limits.md).</span></span>
* <span data-ttu-id="45b39-157">toolearn over het verwerken van aanvragen voor asynchrone REST, Zie [bijhouden asynchrone Azure bewerkingen](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="45b39-157">toolearn about handling asynchronous REST requests, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
