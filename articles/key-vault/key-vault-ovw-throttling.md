---
ms.assetid: 
title: Azure Sleutelkluis richtlijnen beperking | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: fe700e22c5323c2a0bdc315e349cd119798bcf40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="71faa-102">Azure Sleutelkluis richtlijnen beperking</span><span class="sxs-lookup"><span data-stu-id="71faa-102">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="71faa-103">Beperking is een proces dat u starten die het aantal gelijktijdige aanroepen naar de Azure-service beperkt om te voorkomen dat overmatig gebruik van bronnen.</span><span class="sxs-lookup"><span data-stu-id="71faa-103">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="71faa-104">Azure-kluis (Azure sleutel Sleutelkluis) is ontworpen voor het verwerken van een groot aantal aanvragen.</span><span class="sxs-lookup"><span data-stu-id="71faa-104">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="71faa-105">Als er een groot aantal aanvragen optreedt, kunt beperking van de client aanvragen onderhouden voor optimale prestaties en betrouwbaarheid van de Azure Sleutelkluis-service.</span><span class="sxs-lookup"><span data-stu-id="71faa-105">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="71faa-106">Limieten voor bandbreedteregeling variëren, afhankelijk van het scenario.</span><span class="sxs-lookup"><span data-stu-id="71faa-106">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="71faa-107">Bijvoorbeeld, als u een groot aantal schrijfbewerkingen uitvoert, is de mogelijkheid voor beperking hoger dan als u alleen leesbewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="71faa-107">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="71faa-108">Hoe wordt de grenzen in Sleutelkluis verwerkt?</span><span class="sxs-lookup"><span data-stu-id="71faa-108">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="71faa-109">Er zijn er Servicelimieten in Sleutelkluis te voorkomen dat misbruik van resources en ervoor zorgen dat quality of service voor alle clients van de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="71faa-109">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="71faa-110">Wanneer een service-drempelwaarde wordt overschreden, beperkt Sleutelkluis alle verdere aanvragen van die client voor een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="71faa-110">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="71faa-111">Als dit gebeurt, Sleutelkluis retourneert HTTP-statuscode 429 (te veel aanvragen), en de aanvragen mislukken.</span><span class="sxs-lookup"><span data-stu-id="71faa-111">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="71faa-112">Ook mislukte aanvragen die resulteren in een 429 telling voor de versnelling limieten bijgehouden door de Sleutelkluis.</span><span class="sxs-lookup"><span data-stu-id="71faa-112">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="71faa-113">Als u een geldige business case voor hogere versnelling limieten hebt, neem dan contact met ons.</span><span class="sxs-lookup"><span data-stu-id="71faa-113">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="71faa-114">Hoe uw app in reactie op Servicelimieten beperken</span><span class="sxs-lookup"><span data-stu-id="71faa-114">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="71faa-115">Hieronder vindt u **aanbevolen procedures** voor beperking van uw app:</span><span class="sxs-lookup"><span data-stu-id="71faa-115">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="71faa-116">Verminder het aantal bewerkingen per aanvraag.</span><span class="sxs-lookup"><span data-stu-id="71faa-116">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="71faa-117">Verlaag de frequentie van aanvragen.</span><span class="sxs-lookup"><span data-stu-id="71faa-117">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="71faa-118">Vermijd directe nieuwe pogingen.</span><span class="sxs-lookup"><span data-stu-id="71faa-118">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="71faa-119">Alle aanvragen samenvoegen op basis van uw gebruikslimieten.</span><span class="sxs-lookup"><span data-stu-id="71faa-119">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="71faa-120">Wanneer u uw app foutafhandeling implementeert, moet u de HTTP-foutcode 429 gebruiken voor het detecteren van de client-side '-beperking.</span><span class="sxs-lookup"><span data-stu-id="71faa-120">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="71faa-121">Als de aanvraag opnieuw met een foutcode HTTP 429 mislukt, doe u nog steeds een limiet voor de Azure-service.</span><span class="sxs-lookup"><span data-stu-id="71faa-121">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="71faa-122">Blijven gebruiken van de aanbevolen clientzijde methode beperken, de aanvraag opnieuw proberen totdat dit is gelukt.</span><span class="sxs-lookup"><span data-stu-id="71faa-122">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="71faa-123">Aanbevolen bandbreedteregeling client-side '-methode</span><span class="sxs-lookup"><span data-stu-id="71faa-123">Recommended client-side throttling method</span></span>

<span data-ttu-id="71faa-124">In de HTTP-foutcode 429 beginnen met beperking van de client met een benadering exponentieel uitstel:</span><span class="sxs-lookup"><span data-stu-id="71faa-124">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="71faa-125">Wacht 1 seconde, de aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="71faa-125">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="71faa-126">Als u nog steeds beperkt 2 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="71faa-126">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="71faa-127">Als u nog steeds beperkt wacht 4 seconden, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="71faa-127">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="71faa-128">Als u nog steeds beperkt 8 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="71faa-128">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="71faa-129">Als u nog steeds beperkt 16 seconden wachten, aanvraag opnieuw proberen</span><span class="sxs-lookup"><span data-stu-id="71faa-129">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="71faa-130">Op dit moment moet u niet worden opgehaald HTTP 429 responscodes.</span><span class="sxs-lookup"><span data-stu-id="71faa-130">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="71faa-131">Zie ook</span><span class="sxs-lookup"><span data-stu-id="71faa-131">See also</span></span>

<span data-ttu-id="71faa-132">Zie voor een beter afdrukstand van beperking op de Microsoft Cloud [patroon beperking](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="71faa-132">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

