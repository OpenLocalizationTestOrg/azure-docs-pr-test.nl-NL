---
ms.assetid: 
title: aaaAzure Sleutelkluis bandbreedteregeling richtlijnen | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="b9bdb-102">Azure Sleutelkluis richtlijnen beperking</span><span class="sxs-lookup"><span data-stu-id="b9bdb-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="b9bdb-103">Beperking is een proces dat u starten dat het aantal gelijktijdige aanroepen toohello Azure service tooprevent overmatig gebruik van bronnen Hallo beperkt.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-103">Throttling is a process you initiate that limits hello number of concurrent calls toohello Azure service tooprevent overuse of resources.</span></span> <span data-ttu-id="b9bdb-104">Azure-kluis (Azure sleutel Sleutelkluis) is ontworpen toohandle een groot aantal aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-104">Azure Key Vault (AKV) is designed toohandle a high volume of requests.</span></span> <span data-ttu-id="b9bdb-105">Als er een groot aantal aanvragen optreedt, kunt beperking van de client aanvragen onderhouden voor optimale prestaties en betrouwbaarheid van hello Azure Sleutelkluis-service.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of hello AKV service.</span></span>

<span data-ttu-id="b9bdb-106">Limieten voor bandbreedteregeling variëren, afhankelijk van het Hallo-scenario.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-106">Throttling limits vary based on hello scenario.</span></span> <span data-ttu-id="b9bdb-107">Bijvoorbeeld, als u een groot aantal schrijfbewerkingen uitvoert, is Hallo mogelijkheid voor beperking hoger dan als u alleen leesbewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-107">For example, if you are performing a large volume of writes, hello possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="b9bdb-108">Hoe wordt de grenzen in Sleutelkluis verwerkt?</span><span class="sxs-lookup"><span data-stu-id="b9bdb-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="b9bdb-109">Servicelimieten in Sleutelkluis zijn er tooprevent misbruik van resources en controleer quality of service voor alle clients van de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-109">Service limits in Key Vault are there tooprevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="b9bdb-110">Wanneer een service-drempelwaarde wordt overschreden, beperkt Sleutelkluis alle verdere aanvragen van die client voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="b9bdb-111">Als dit gebeurt, Sleutelkluis retourneert HTTP-statuscode 429 (te veel aanvragen), en het Hallo-aanvragen mislukken.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and hello requests fail.</span></span> <span data-ttu-id="b9bdb-112">Ook mislukte aanvragen die 429 geteld naar Hallo versnelling limieten bijgehouden door de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-112">Also, failed requests that return a 429 count towards hello throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="b9bdb-113">Als u een geldige business case voor hogere versnelling limieten hebt, neem dan contact met ons.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a><span data-ttu-id="b9bdb-114">Hoe toothrottle uw app in het antwoord tooservice beperkt</span><span class="sxs-lookup"><span data-stu-id="b9bdb-114">How toothrottle your app in response tooservice limits</span></span>

<span data-ttu-id="b9bdb-115">Hallo volgen **aanbevolen procedures** voor beperking van uw app:</span><span class="sxs-lookup"><span data-stu-id="b9bdb-115">hello following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="b9bdb-116">Verminder het aantal bewerkingen per aanvraag Hallo.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-116">Reduce hello number of operations per request.</span></span>
- <span data-ttu-id="b9bdb-117">Verlaag de frequentie Hallo van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-117">Reduce hello frequency of requests.</span></span>
- <span data-ttu-id="b9bdb-118">Vermijd directe nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="b9bdb-119">Alle aanvragen samenvoegen op basis van uw gebruikslimieten.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="b9bdb-120">Wanneer u uw app foutafhandeling implementeert, moet gebruik Hallo HTTP fout code 429 toodetect Hallo voor client-side '-beperking.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-120">When you implement your app's error handling, use hello HTTP error code 429 toodetect hello need for client-side throttling.</span></span> <span data-ttu-id="b9bdb-121">Als Hallo aanvraag opnieuw met een 429 HTTP-foutcode mislukt, doe u nog steeds een limiet voor de Azure-service.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-121">If hello request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="b9bdb-122">Blijven toouse Hallo aanbevolen clientzijde bandbreedteregeling methode, Hallo aanvraag opnieuw proberen totdat dit is gelukt.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-122">Continue toouse hello recommended client-side throttling method, retrying hello request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="b9bdb-123">Aanbevolen bandbreedteregeling client-side '-methode</span><span class="sxs-lookup"><span data-stu-id="b9bdb-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="b9bdb-124">In de HTTP-foutcode 429 beginnen met beperking van de client met een benadering exponentieel uitstel:</span><span class="sxs-lookup"><span data-stu-id="b9bdb-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="b9bdb-125">Wacht 1 seconde, de aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="b9bdb-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="b9bdb-126">Als u nog steeds beperkt 2 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="b9bdb-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="b9bdb-127">Als u nog steeds beperkt wacht 4 seconden, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="b9bdb-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="b9bdb-128">Als u nog steeds beperkt 8 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="b9bdb-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="b9bdb-129">Als u nog steeds beperkt 16 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="b9bdb-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="b9bdb-130">Op dit moment moet u niet worden opgehaald HTTP 429 responscodes.</span><span class="sxs-lookup"><span data-stu-id="b9bdb-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="b9bdb-131">Zie ook</span><span class="sxs-lookup"><span data-stu-id="b9bdb-131">See also</span></span>

<span data-ttu-id="b9bdb-132">Zie voor een beter afdrukstand van de beperking op Hallo Microsoft Cloud [patroon beperking](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="b9bdb-132">For a deeper orientation of throttling on hello Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

