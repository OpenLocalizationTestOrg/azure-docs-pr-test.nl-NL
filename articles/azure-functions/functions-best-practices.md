---
title: aaaBest procedures voor Azure Functions | Microsoft Docs
description: Informatie over aanbevolen procedures en patronen voor Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure functions, patronen, best practices, functies, gebeurtenisverwerking webhooks, dynamische compute, zonder server-architectuur
ms.assetid: 9058fb2f-8a93-4036-a921-97a0772f503c
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/13/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bd3d826b75267a740e355b008943a48f71ebd339
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hello-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="2af6e-104">Hallo prestaties en betrouwbaarheid van Azure Functions optimaliseren</span><span class="sxs-lookup"><span data-stu-id="2af6e-104">Optimize hello performance and reliability of Azure Functions</span></span>

<span data-ttu-id="2af6e-105">Dit artikel bevat richtlijnen tooimprove Hallo prestaties en betrouwbaarheid van uw apps functie.</span><span class="sxs-lookup"><span data-stu-id="2af6e-105">This article provides guidance tooimprove hello performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="2af6e-106">Vermijd langlopende functies</span><span class="sxs-lookup"><span data-stu-id="2af6e-106">Avoid long running functions</span></span>

<span data-ttu-id="2af6e-107">Grote, langlopende functies kunnen onverwachte time-out problemen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="2af6e-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="2af6e-108">Een functie kan worden grote vanwege toomany Node.js-afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="2af6e-108">A function can become large due toomany Node.js dependencies.</span></span> <span data-ttu-id="2af6e-109">Afhankelijkheden importeren kan ook leiden tot verhoogde laadtijden die tot onverwachte time-outs leiden.</span><span class="sxs-lookup"><span data-stu-id="2af6e-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="2af6e-110">Afhankelijkheden zijn beide expliciet en impliciet geladen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="2af6e-111">Een enkele module geladen door uw code kan zijn eigen aanvullende modules worden geladen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="2af6e-112">Indien mogelijk wordt Verander grote functies in kleinere functie ingesteld die werken samen en snel antwoorden retourneren.</span><span class="sxs-lookup"><span data-stu-id="2af6e-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="2af6e-113">Bijvoorbeeld, een webhook of HTTP-trigger functie mogelijk een bevestiging van de reactie binnen een bepaalde tijd; het is gebruikelijk voor webhooks toorequire direct een reactie.</span><span class="sxs-lookup"><span data-stu-id="2af6e-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks toorequire an immediate response.</span></span> <span data-ttu-id="2af6e-114">U kunt Hallo HTTP-trigger nettolading doorgeven in een wachtrij toobe verwerkt door een functie van de trigger wachtrij.</span><span class="sxs-lookup"><span data-stu-id="2af6e-114">You can pass hello HTTP trigger payload into a queue toobe processed by a queue trigger function.</span></span> <span data-ttu-id="2af6e-115">Deze aanpak kunt u toodefer Hallo echte werk en direct een reactie terug.</span><span class="sxs-lookup"><span data-stu-id="2af6e-115">This approach allows you toodefer hello actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="2af6e-116">Cross-functie communicatie</span><span class="sxs-lookup"><span data-stu-id="2af6e-116">Cross function communication</span></span>

<span data-ttu-id="2af6e-117">Bij het integreren van meerdere functies, maar het is doorgaans een best practice toouse opslagwachtrijen voor cross-functie communicatie.</span><span class="sxs-lookup"><span data-stu-id="2af6e-117">When integrating multiple functions, it is generally a best practice toouse storage queues for cross function communication.</span></span>  <span data-ttu-id="2af6e-118">de belangrijkste reden Hallo is opslagwachtrijen zijn goedkoper en veel eenvoudiger tooprovision.</span><span class="sxs-lookup"><span data-stu-id="2af6e-118">hello main reason is storage queues are cheaper and much easier tooprovision.</span></span> 

<span data-ttu-id="2af6e-119">Afzonderlijke berichten in een opslagwachtrij zijn beperkt in grootte too64 KB.</span><span class="sxs-lookup"><span data-stu-id="2af6e-119">Individual messages in a storage queue are limited in size too64 KB.</span></span> <span data-ttu-id="2af6e-120">Als u nodig hebt toopass grotere berichten tussen de functies, kan een Azure Service Bus-wachtrij gebruikte toosupport berichtgrootten up too256 KB zijn.</span><span class="sxs-lookup"><span data-stu-id="2af6e-120">If you need toopass larger messages between functions, an Azure Service Bus queue could be used toosupport message sizes up too256 KB.</span></span>

<span data-ttu-id="2af6e-121">Service Bus-onderwerpen zijn handig als u nodig hebt bericht filteren voordat ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="2af6e-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="2af6e-122">Event hubs zijn nuttig toosupport hoog volume communicatie.</span><span class="sxs-lookup"><span data-stu-id="2af6e-122">Event hubs are useful toosupport high volume communications.</span></span>


## <a name="write-functions-toobe-stateless"></a><span data-ttu-id="2af6e-123">Schrijven van functies toobe staatloze</span><span class="sxs-lookup"><span data-stu-id="2af6e-123">Write functions toobe stateless</span></span> 

<span data-ttu-id="2af6e-124">Functies moet staatloze en idempotent indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="2af6e-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="2af6e-125">Eventuele vereiste statusgegevens koppelen aan uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="2af6e-125">Associate any required state information with your data.</span></span> <span data-ttu-id="2af6e-126">Bijvoorbeeld, een bestelling wordt verwerkt waarschijnlijk heeft een bijbehorende `state` lid.</span><span class="sxs-lookup"><span data-stu-id="2af6e-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="2af6e-127">Een functie kan een volgorde die op basis van die status terwijl Hallo functie zelf staatloze blijft verwerken.</span><span class="sxs-lookup"><span data-stu-id="2af6e-127">A function could process an order based on that state while hello function itself remains stateless.</span></span> 

<span data-ttu-id="2af6e-128">De Idempotent-functies zijn vooral aanbevolen met timer triggers.</span><span class="sxs-lookup"><span data-stu-id="2af6e-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="2af6e-129">Bijvoorbeeld, als er iets dat absoluut moet één keer per dag worden uitgevoerd, schrijven zodat deze tijdens Hallo dag Hello dezelfde resultaten uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="2af6e-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during hello day with hello same results.</span></span> <span data-ttu-id="2af6e-130">Hallo-functie kunt afsluiten wanneer er geen werk voor een bepaalde dag.</span><span class="sxs-lookup"><span data-stu-id="2af6e-130">hello function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="2af6e-131">Ook als een eerder uitgevoerde is mislukt toocomplete, Hallo een volgende keer uitvoert moet kunnen worden opgepikt waar deze gebleven was.</span><span class="sxs-lookup"><span data-stu-id="2af6e-131">Also if a previous run failed toocomplete, hello next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="2af6e-132">Defensive functies schrijven</span><span class="sxs-lookup"><span data-stu-id="2af6e-132">Write defensive functions</span></span>

<span data-ttu-id="2af6e-133">Stel dat uw-functie kan een uitzondering op elk gewenst moment optreden.</span><span class="sxs-lookup"><span data-stu-id="2af6e-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="2af6e-134">Ontwerp dat uw functies met Hallo mogelijkheid toocontinue van een eerder punt mislukt tijdens het Hallo volgende uitvoering.</span><span class="sxs-lookup"><span data-stu-id="2af6e-134">Design your functions with hello ability toocontinue from a previous fail point during hello next execution.</span></span> <span data-ttu-id="2af6e-135">Houd rekening met een scenario waarbij Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="2af6e-135">Consider a scenario that requires hello following actions:</span></span>

1. <span data-ttu-id="2af6e-136">De query voor 10.000 rijen in een database.</span><span class="sxs-lookup"><span data-stu-id="2af6e-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="2af6e-137">Maak een wachtrijbericht voor elk van deze rijen tooprocess verdere Hallo regel omlaag.</span><span class="sxs-lookup"><span data-stu-id="2af6e-137">Create a queue message for each of those rows tooprocess further down hello line.</span></span>
 
<span data-ttu-id="2af6e-138">Afhankelijk van hoe complexe uw systeem is, moet u wellicht: downstream betrokken services naar behoren werkt, netwerken uitval of quotum beperkt bereikt, enzovoort. Al deze waarden kunnen invloed hebben op de functie op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="2af6e-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="2af6e-139">U moet uw functies toobe voorbereid voor het toodesign.</span><span class="sxs-lookup"><span data-stu-id="2af6e-139">You need toodesign your functions toobe prepared for it.</span></span>

<span data-ttu-id="2af6e-140">Hoe uw code reageren als er een fout optreedt nadat 5.000 van deze items in een wachtrij voor verwerking invoegen?</span><span class="sxs-lookup"><span data-stu-id="2af6e-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="2af6e-141">Bijhouden van items in een verzameling die u hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="2af6e-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="2af6e-142">Anders wordt u mogelijk plaats ze opnieuw zodra.</span><span class="sxs-lookup"><span data-stu-id="2af6e-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="2af6e-143">Dit kan ernstige gevolgen hebben op uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="2af6e-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="2af6e-144">Als een wachtrij-item al verwerkt is, kunt u de functie toobe geen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-144">If a queue item was already processed, allow your function toobe a no-op.</span></span>

<span data-ttu-id="2af6e-145">Profiteren van beschermingsmaatregelen reeds wordt geboden voor onderdelen die u in hello Azure Functions-platform gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2af6e-145">Take advantage of defensive measures already provided for components you use in hello Azure Functions platform.</span></span> <span data-ttu-id="2af6e-146">Zie bijvoorbeeld **verwerken van verontreinigde berichten** in de documentatie voor Hallo [Azure-Opslagwachtrij activeert](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="2af6e-146">For example, see **Handling poison queue messages** in hello documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-hello-same-function-app"></a><span data-ttu-id="2af6e-147">Geen combinatie test en productie code in Hallo dezelfde functie-app</span><span class="sxs-lookup"><span data-stu-id="2af6e-147">Don't mix test and production code in hello same function app</span></span>

<span data-ttu-id="2af6e-148">Functies binnen een functie-app bronnen delen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-148">Functions within a function app share resources.</span></span> <span data-ttu-id="2af6e-149">Bijvoorbeeld: geheugen wordt gedeeld.</span><span class="sxs-lookup"><span data-stu-id="2af6e-149">For example, memory is shared.</span></span> <span data-ttu-id="2af6e-150">Als u een functie-app in productie, niet test-gerelateerde functies en bronnen tooit toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-150">If you're using a function app in production, don't add test-related functions and resources tooit.</span></span> <span data-ttu-id="2af6e-151">Tijdens de uitvoering van de productie-code kan dit leiden tot onverwachte overhead.</span><span class="sxs-lookup"><span data-stu-id="2af6e-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="2af6e-152">Zorg ervoor dat u in uw productie-functie apps laden.</span><span class="sxs-lookup"><span data-stu-id="2af6e-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="2af6e-153">Geheugen wordt gemiddeld over elke functie in het Hallo-app.</span><span class="sxs-lookup"><span data-stu-id="2af6e-153">Memory is averaged across each function in hello app.</span></span>

<span data-ttu-id="2af6e-154">Als u een gedeelde assembly waarnaar wordt verwezen in meerdere .net-functies hebt, kunt u deze in een gemeenschappelijke gedeelde map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="2af6e-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="2af6e-155">Verwijzing Hallo assembly met een instructie vergelijkbare toohello voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="2af6e-155">Reference hello assembly with a statement similar toohello following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="2af6e-156">Anders is het eenvoudig tooaccidentally implementeren meerdere testversies Hallo binaire die zich tussen anders gedragen fungeert.</span><span class="sxs-lookup"><span data-stu-id="2af6e-156">Otherwise, it is easy tooaccidentally deploy multiple test versions of hello same binary that behave differently between functions.</span></span>

<span data-ttu-id="2af6e-157">Gebruik geen uitgebreide logboekregistratie in productiecode.</span><span class="sxs-lookup"><span data-stu-id="2af6e-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="2af6e-158">Er is een negatief prestatieresultaat.</span><span class="sxs-lookup"><span data-stu-id="2af6e-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="2af6e-159">Asynchrone code gebruiken, maar geen aanroepen blokkeren</span><span class="sxs-lookup"><span data-stu-id="2af6e-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="2af6e-160">Asynchrone programmering is een aanbevolen procedure.</span><span class="sxs-lookup"><span data-stu-id="2af6e-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="2af6e-161">Echter altijd voorkomen die verwijzen naar Hallo `Result` eigenschap of aanroepen `Wait` methode op een `Task` exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2af6e-161">However, always avoid referencing hello `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="2af6e-162">Deze aanpak kunt toothread uitputting leiden.</span><span class="sxs-lookup"><span data-stu-id="2af6e-162">This approach can lead toothread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="2af6e-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2af6e-163">Next steps</span></span>
<span data-ttu-id="2af6e-164">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="2af6e-164">For more information, see hello following resources:</span></span>

<span data-ttu-id="2af6e-165">Omdat Azure Functions maakt gebruik van Azure App Service, dient u zich bewust bent van App Service-richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="2af6e-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="2af6e-166">Prestatieoptimalisaties patterns and practice HTTP</span><span class="sxs-lookup"><span data-stu-id="2af6e-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

