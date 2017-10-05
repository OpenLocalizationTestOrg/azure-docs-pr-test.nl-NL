---
title: Aanbevolen procedures voor Azure Functions | Microsoft Docs
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
ms.openlocfilehash: 645a5dd16e72619e7c2470ab8f03098f0fa6c7f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="optimize-the-performance-and-reliability-of-azure-functions"></a><span data-ttu-id="c8802-104">De prestaties en betrouwbaarheid van Azure Functions optimaliseren</span><span class="sxs-lookup"><span data-stu-id="c8802-104">Optimize the performance and reliability of Azure Functions</span></span>

<span data-ttu-id="c8802-105">Dit artikel bevat richtlijnen voor het verbeteren van de prestaties en betrouwbaarheid van uw apps functie.</span><span class="sxs-lookup"><span data-stu-id="c8802-105">This article provides guidance to improve the performance and reliability of your function apps.</span></span> 


## <a name="avoid-long-running-functions"></a><span data-ttu-id="c8802-106">Vermijd langlopende functies</span><span class="sxs-lookup"><span data-stu-id="c8802-106">Avoid long running functions</span></span>

<span data-ttu-id="c8802-107">Grote, langlopende functies kunnen onverwachte time-out problemen veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="c8802-107">Large, long-running functions can cause unexpected timeout issues.</span></span> <span data-ttu-id="c8802-108">Een functie kan groot zijn als gevolg van Node.js methode veel afhankelijkheden worden.</span><span class="sxs-lookup"><span data-stu-id="c8802-108">A function can become large due to many Node.js dependencies.</span></span> <span data-ttu-id="c8802-109">Afhankelijkheden importeren kan ook leiden tot verhoogde laadtijden die tot onverwachte time-outs leiden.</span><span class="sxs-lookup"><span data-stu-id="c8802-109">Importing dependencies can also cause increased load times that result in unexpected timeouts.</span></span> <span data-ttu-id="c8802-110">Afhankelijkheden zijn beide expliciet en impliciet geladen.</span><span class="sxs-lookup"><span data-stu-id="c8802-110">Dependencies are loaded both explicitly and implicitly.</span></span> <span data-ttu-id="c8802-111">Een enkele module geladen door uw code kan zijn eigen aanvullende modules worden geladen.</span><span class="sxs-lookup"><span data-stu-id="c8802-111">A single module loaded by your code may load its own additional modules.</span></span>  

<span data-ttu-id="c8802-112">Indien mogelijk wordt Verander grote functies in kleinere functie ingesteld die werken samen en snel antwoorden retourneren.</span><span class="sxs-lookup"><span data-stu-id="c8802-112">Whenever possible, refactor large functions into smaller function sets that work together and return responses fast.</span></span> <span data-ttu-id="c8802-113">Bijvoorbeeld, een webhook of HTTP-trigger functie mogelijk een bevestiging van de reactie binnen een bepaalde tijd; het is gebruikelijk voor webhooks voor een onmiddellijke actie nodig.</span><span class="sxs-lookup"><span data-stu-id="c8802-113">For example, a webhook or HTTP trigger function might require an acknowledgment response within a certain time limit; it is common for webhooks to require an immediate response.</span></span> <span data-ttu-id="c8802-114">U kunt de nettolading van de HTTP-trigger doorgeven in een wachtrij moeten worden verwerkt door een functie van de trigger wachtrij.</span><span class="sxs-lookup"><span data-stu-id="c8802-114">You can pass the HTTP trigger payload into a queue to be processed by a queue trigger function.</span></span> <span data-ttu-id="c8802-115">Deze aanpak kunt u het echte werk uit te stellen en direct een reactie terug te keren.</span><span class="sxs-lookup"><span data-stu-id="c8802-115">This approach allows you to defer the actual work and return an immediate response.</span></span>


## <a name="cross-function-communication"></a><span data-ttu-id="c8802-116">Cross-functie communicatie</span><span class="sxs-lookup"><span data-stu-id="c8802-116">Cross function communication</span></span>

<span data-ttu-id="c8802-117">Bij het integreren van meerdere functies, maar het is doorgaans beste gebruikmaken van opslagwachtrijen voor cross-functie communicatie.</span><span class="sxs-lookup"><span data-stu-id="c8802-117">When integrating multiple functions, it is generally a best practice to use storage queues for cross function communication.</span></span>  <span data-ttu-id="c8802-118">De belangrijkste reden is opslagwachtrijen zijn goedkoper en eenvoudiger te richten.</span><span class="sxs-lookup"><span data-stu-id="c8802-118">The main reason is storage queues are cheaper and much easier to provision.</span></span> 

<span data-ttu-id="c8802-119">Afzonderlijke berichten in een opslagwachtrij zijn in grootte beperkt tot 64 KB.</span><span class="sxs-lookup"><span data-stu-id="c8802-119">Individual messages in a storage queue are limited in size to 64 KB.</span></span> <span data-ttu-id="c8802-120">Als u doorgeven grotere berichten tussen de functies wilt, het formaat van een Azure Service Bus-wachtrij kan worden gebruikt ter ondersteuning van bericht tot 256 KB.</span><span class="sxs-lookup"><span data-stu-id="c8802-120">If you need to pass larger messages between functions, an Azure Service Bus queue could be used to support message sizes up to 256 KB.</span></span>

<span data-ttu-id="c8802-121">Service Bus-onderwerpen zijn handig als u nodig hebt bericht filteren voordat ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c8802-121">Service Bus topics are useful if you require message filtering before processing.</span></span>

<span data-ttu-id="c8802-122">Event hubs zijn handig voor de ondersteuning voor grote volumes communicatie.</span><span class="sxs-lookup"><span data-stu-id="c8802-122">Event hubs are useful to support high volume communications.</span></span>


## <a name="write-functions-to-be-stateless"></a><span data-ttu-id="c8802-123">Schrijven van functies om te worden staatloze</span><span class="sxs-lookup"><span data-stu-id="c8802-123">Write functions to be stateless</span></span> 

<span data-ttu-id="c8802-124">Functies moet staatloze en idempotent indien mogelijk.</span><span class="sxs-lookup"><span data-stu-id="c8802-124">Functions should be stateless and idempotent if possible.</span></span> <span data-ttu-id="c8802-125">Eventuele vereiste statusgegevens koppelen aan uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="c8802-125">Associate any required state information with your data.</span></span> <span data-ttu-id="c8802-126">Bijvoorbeeld, een bestelling wordt verwerkt waarschijnlijk heeft een bijbehorende `state` lid.</span><span class="sxs-lookup"><span data-stu-id="c8802-126">For example, an order being processed would likely have an associated `state` member.</span></span> <span data-ttu-id="c8802-127">Een functie kan een volgorde die op basis van die status terwijl de functie zelf staatloze blijft verwerken.</span><span class="sxs-lookup"><span data-stu-id="c8802-127">A function could process an order based on that state while the function itself remains stateless.</span></span> 

<span data-ttu-id="c8802-128">De Idempotent-functies zijn vooral aanbevolen met timer triggers.</span><span class="sxs-lookup"><span data-stu-id="c8802-128">Idempotent functions are especially recommended with timer triggers.</span></span> <span data-ttu-id="c8802-129">Bijvoorbeeld, als er iets dat absoluut moet één keer per dag worden uitgevoerd, schrijven zodat elk gewenst moment tijdens de dag kan worden uitgevoerd met hetzelfde resultaat.</span><span class="sxs-lookup"><span data-stu-id="c8802-129">For example, if you have something that absolutely must run once a day, write it so it can run any time during the day with the same results.</span></span> <span data-ttu-id="c8802-130">De functie kunt afsluiten wanneer er geen werk voor een bepaalde dag.</span><span class="sxs-lookup"><span data-stu-id="c8802-130">The function can exit when there is no work for a particular day.</span></span> <span data-ttu-id="c8802-131">Ook als een eerdere mislukte voltooid uitvoert, de volgende keer uitvoeren moet kunnen worden opgepikt waar deze gebleven was.</span><span class="sxs-lookup"><span data-stu-id="c8802-131">Also if a previous run failed to complete, the next run should pick up where it left off.</span></span>


## <a name="write-defensive-functions"></a><span data-ttu-id="c8802-132">Defensive functies schrijven</span><span class="sxs-lookup"><span data-stu-id="c8802-132">Write defensive functions</span></span>

<span data-ttu-id="c8802-133">Stel dat uw-functie kan een uitzondering op elk gewenst moment optreden.</span><span class="sxs-lookup"><span data-stu-id="c8802-133">Assume your function could encounter an exception at any time.</span></span> <span data-ttu-id="c8802-134">Ontwerp uw functies met de mogelijkheid om door te gaan van een vorige fouten dat tijdens de volgende uitvoering.</span><span class="sxs-lookup"><span data-stu-id="c8802-134">Design your functions with the ability to continue from a previous fail point during the next execution.</span></span> <span data-ttu-id="c8802-135">Houd rekening met een scenario waarin de volgende acties vereist:</span><span class="sxs-lookup"><span data-stu-id="c8802-135">Consider a scenario that requires the following actions:</span></span>

1. <span data-ttu-id="c8802-136">De query voor 10.000 rijen in een database.</span><span class="sxs-lookup"><span data-stu-id="c8802-136">Query for 10,000 rows in a db.</span></span>
2. <span data-ttu-id="c8802-137">Maken van een wachtrijbericht voor elk van deze rijen verder omlaag in de regel.</span><span class="sxs-lookup"><span data-stu-id="c8802-137">Create a queue message for each of those rows to process further down the line.</span></span>
 
<span data-ttu-id="c8802-138">Afhankelijk van hoe complexe uw systeem is, moet u wellicht: downstream betrokken services naar behoren werkt, netwerken uitval of quotum beperkt bereikt, enzovoort. Al deze waarden kunnen invloed hebben op de functie op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="c8802-138">Depending on how complex your system is, you may have: involved downstream services behaving badly, networking outages, or quota limits reached, etc. All of these can affect your function at any time.</span></span> <span data-ttu-id="c8802-139">U moet uw functies worden voorbereid op het ontwerp.</span><span class="sxs-lookup"><span data-stu-id="c8802-139">You need to design your functions to be prepared for it.</span></span>

<span data-ttu-id="c8802-140">Hoe uw code reageren als er een fout optreedt nadat 5.000 van deze items in een wachtrij voor verwerking invoegen?</span><span class="sxs-lookup"><span data-stu-id="c8802-140">How does your code react if a failure occurs after inserting 5,000 of those items into a queue for processing?</span></span> <span data-ttu-id="c8802-141">Bijhouden van items in een verzameling die u hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="c8802-141">Track items in a set that you’ve completed.</span></span> <span data-ttu-id="c8802-142">Anders wordt u mogelijk plaats ze opnieuw zodra.</span><span class="sxs-lookup"><span data-stu-id="c8802-142">Otherwise, you might insert them again next time.</span></span> <span data-ttu-id="c8802-143">Dit kan ernstige gevolgen hebben op uw werkstroom.</span><span class="sxs-lookup"><span data-stu-id="c8802-143">This can have a serious impact on your work flow.</span></span> 

<span data-ttu-id="c8802-144">Als een wachtrij-item al verwerkt is, kunt u de functie moet geen.</span><span class="sxs-lookup"><span data-stu-id="c8802-144">If a queue item was already processed, allow your function to be a no-op.</span></span>

<span data-ttu-id="c8802-145">Profiteren van beschermingsmaatregelen reeds wordt geboden voor onderdelen die u in de Azure Functions-platform gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c8802-145">Take advantage of defensive measures already provided for components you use in the Azure Functions platform.</span></span> <span data-ttu-id="c8802-146">Zie bijvoorbeeld **verwerken van verontreinigde berichten** in de documentatie voor [Azure-Opslagwachtrij activeert](functions-bindings-storage-queue.md#trigger).</span><span class="sxs-lookup"><span data-stu-id="c8802-146">For example, see **Handling poison queue messages** in the documentation for [Azure Storage Queue triggers](functions-bindings-storage-queue.md#trigger).</span></span>
 

## <a name="dont-mix-test-and-production-code-in-the-same-function-app"></a><span data-ttu-id="c8802-147">Combineer geen test en productie-code in dezelfde functie-app</span><span class="sxs-lookup"><span data-stu-id="c8802-147">Don't mix test and production code in the same function app</span></span>

<span data-ttu-id="c8802-148">Functies binnen een functie-app bronnen delen.</span><span class="sxs-lookup"><span data-stu-id="c8802-148">Functions within a function app share resources.</span></span> <span data-ttu-id="c8802-149">Bijvoorbeeld: geheugen wordt gedeeld.</span><span class="sxs-lookup"><span data-stu-id="c8802-149">For example, memory is shared.</span></span> <span data-ttu-id="c8802-150">Als u een functie-app in productie, niet test-gerelateerde functies en bronnen aan toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c8802-150">If you're using a function app in production, don't add test-related functions and resources to it.</span></span> <span data-ttu-id="c8802-151">Tijdens de uitvoering van de productie-code kan dit leiden tot onverwachte overhead.</span><span class="sxs-lookup"><span data-stu-id="c8802-151">It can cause unexpected overhead during production code execution.</span></span>

<span data-ttu-id="c8802-152">Zorg ervoor dat u in uw productie-functie apps laden.</span><span class="sxs-lookup"><span data-stu-id="c8802-152">Be careful what you load in your production function apps.</span></span> <span data-ttu-id="c8802-153">Geheugen wordt gemiddeld over elke functie in de app.</span><span class="sxs-lookup"><span data-stu-id="c8802-153">Memory is averaged across each function in the app.</span></span>

<span data-ttu-id="c8802-154">Als u een gedeelde assembly waarnaar wordt verwezen in meerdere .net-functies hebt, kunt u deze in een gemeenschappelijke gedeelde map geplaatst.</span><span class="sxs-lookup"><span data-stu-id="c8802-154">If you have a shared assembly referenced in multiple .Net functions, put it in a common shared folder.</span></span> <span data-ttu-id="c8802-155">Verwijzen naar de assembly met een instructie die vergelijkbaar is met het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c8802-155">Reference the assembly with a statement similar to the following example:</span></span> 

    #r "..\Shared\MyAssembly.dll". 

<span data-ttu-id="c8802-156">Anders is het eenvoudig te implementeren per ongeluk meerdere testversies van dezelfde binaire die zich anders tussen functies gedragen.</span><span class="sxs-lookup"><span data-stu-id="c8802-156">Otherwise, it is easy to accidentally deploy multiple test versions of the same binary that behave differently between functions.</span></span>

<span data-ttu-id="c8802-157">Gebruik geen uitgebreide logboekregistratie in productiecode.</span><span class="sxs-lookup"><span data-stu-id="c8802-157">Don't use verbose logging in production code.</span></span> <span data-ttu-id="c8802-158">Er is een negatief prestatieresultaat.</span><span class="sxs-lookup"><span data-stu-id="c8802-158">It has a negative performance impact.</span></span>



## <a name="use-async-code-but-avoid-blocking-calls"></a><span data-ttu-id="c8802-159">Asynchrone code gebruiken, maar geen aanroepen blokkeren</span><span class="sxs-lookup"><span data-stu-id="c8802-159">Use async code but avoid blocking calls</span></span>

<span data-ttu-id="c8802-160">Asynchrone programmering is een aanbevolen procedure.</span><span class="sxs-lookup"><span data-stu-id="c8802-160">Asynchronous programming is a recommended best practice.</span></span> <span data-ttu-id="c8802-161">Echter altijd voorkomen die verwijzen naar de `Result` eigenschap of aanroepen `Wait` methode op een `Task` exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c8802-161">However, always avoid referencing the `Result` property or calling `Wait` method on a `Task` instance.</span></span> <span data-ttu-id="c8802-162">Deze methode kan leiden tot uitputting van de thread.</span><span class="sxs-lookup"><span data-stu-id="c8802-162">This approach can lead to thread exhaustion.</span></span>


[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

## <a name="next-steps"></a><span data-ttu-id="c8802-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8802-163">Next steps</span></span>
<span data-ttu-id="c8802-164">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c8802-164">For more information, see the following resources:</span></span>

<span data-ttu-id="c8802-165">Omdat Azure Functions maakt gebruik van Azure App Service, dient u zich bewust bent van App Service-richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="c8802-165">Because Azure Functions uses Azure App Service, you should also be aware of  App Service guidelines.</span></span>
* [<span data-ttu-id="c8802-166">Prestatieoptimalisaties patterns and practice HTTP</span><span class="sxs-lookup"><span data-stu-id="c8802-166">Patterns and Practices HTTP Performance Optimizations</span></span>](https://docs.microsoft.com/azure/architecture/antipatterns/improper-instantiation/)

