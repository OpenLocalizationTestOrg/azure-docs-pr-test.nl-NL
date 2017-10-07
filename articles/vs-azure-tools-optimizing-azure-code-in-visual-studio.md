---
title: uw Azure in Visual Studio code aaaOptimizing | Microsoft Docs
description: Meer informatie over hoe Azure code optimalisatie hulpprogramma's in Visual Studio zorgt u ervoor dat uw code krachtigere en meer.
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="28f41-103">Optimaliseren van uw Azure-Code</span><span class="sxs-lookup"><span data-stu-id="28f41-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="28f41-104">Wanneer u apps die gebruikmaken van Microsoft Azure programmeren, er zijn enkele codering procedures die u moet volgen toohelp voorkoming van problemen met app-schaalbaarheid, werking en prestaties in een cloudomgeving.</span><span class="sxs-lookup"><span data-stu-id="28f41-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="28f41-105">Microsoft biedt een analyseprogramma Azure Code die wordt herkend en identificeert diverse van deze problemen meestal aangetroffen en kunt u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="28f41-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="28f41-106">Hallo-hulpprogramma in Visual Studio via NuGet, kunt u downloaden.</span><span class="sxs-lookup"><span data-stu-id="28f41-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="28f41-107">Azure Code Analysis-regels</span><span class="sxs-lookup"><span data-stu-id="28f41-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="28f41-108">Hello Azure Code analysehulpprogramma gebruikt Hallo volgens de regels voor tooautomatically vlag uw Azure code wanneer er bekende problemen met prestaties beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="28f41-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="28f41-109">Gevonden problemen worden weergegeven als een waarschuwingen of compilatiefouten.</span><span class="sxs-lookup"><span data-stu-id="28f41-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="28f41-110">Code correcties of suggesties tooresolve Hallo waarschuwingen of fouten zijn vaak door een gloeilampje voorzien.</span><span class="sxs-lookup"><span data-stu-id="28f41-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="28f41-111">Vermijd het gebruik van standaard (in-process) sessiestatusmodus gebruiken</span><span class="sxs-lookup"><span data-stu-id="28f41-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="28f41-112">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-112">ID</span></span>
<span data-ttu-id="28f41-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="28f41-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-114">Description</span></span>
<span data-ttu-id="28f41-115">Als u Hallo standaard (in-process) sessiestatusmodus voor cloud-toepassingen gebruikt, kunt u de sessiestatus kunt verliezen.</span><span class="sxs-lookup"><span data-stu-id="28f41-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="28f41-116">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-117">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-117">Reason</span></span>
<span data-ttu-id="28f41-118">Hallo sessiestatusmodus in Hallo web.config-bestand opgegeven is in-process standaard.</span><span class="sxs-lookup"><span data-stu-id="28f41-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="28f41-119">Als er geen vermelding is opgegeven in configuratiebestand hello, standaard Hallo sessiestatus modus tooin-process.</span><span class="sxs-lookup"><span data-stu-id="28f41-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="28f41-120">Hallo-in-process-modus wordt de sessiestatus opgeslagen in het geheugen op Hallo-webserver.</span><span class="sxs-lookup"><span data-stu-id="28f41-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="28f41-121">Wanneer een exemplaar opnieuw is opgestart of een nieuw exemplaar wordt gebruikt voor de load balancer of failover-ondersteuning, wordt niet Hallo sessiestatus opgeslagen in het geheugen op de webserver Hallo opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="28f41-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="28f41-122">Deze situatie wordt voorkomen dat Hallo toepassing wordt schaalbare op Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="28f41-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="28f41-123">ASP.NET-sessiestatus ondersteunt verschillende verschillende opslagopties voor sessiestatusgegevens: InProc, StateServer, SQL Server, aangepast, en uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="28f41-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="28f41-124">Het verdient aanbeveling dat u aangepaste modus toohost gegevens op een externe sessiestatus-winkel, zoals [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="28f41-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-125">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-125">Solution</span></span>
<span data-ttu-id="28f41-126">Een aanbevolen oplossing is de sessiestatus toostore op een beheerde cacheservice.</span><span class="sxs-lookup"><span data-stu-id="28f41-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="28f41-127">Meer informatie over hoe toouse [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore de sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="28f41-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="28f41-128">U kunt ook de store-sessie aangeven in andere locaties tooensure uw toepassing schaalbare op Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="28f41-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="28f41-129">meer informatie over alternatieve oplossingen Lees toolearn [sessie status modi](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="28f41-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="28f41-130">Voer methode mag geen asynchrone</span><span class="sxs-lookup"><span data-stu-id="28f41-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="28f41-131">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-131">ID</span></span>
<span data-ttu-id="28f41-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="28f41-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-133">Description</span></span>
<span data-ttu-id="28f41-134">Maken van asynchrone methoden (zoals [await](https://msdn.microsoft.com/library/hh156528.aspx)) buiten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en vervolgens aanroep Hallo async-methoden van [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="28f41-135">Hallo declareren [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode als asynchroon zorgt ervoor dat Hallo worker rol tooenter een lus opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="28f41-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="28f41-136">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-137">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-137">Reason</span></span>
<span data-ttu-id="28f41-138">Het aanroepen van asynchrone methoden binnen Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode zorgt ervoor dat Hallo cloud service runtime toorecycle Hallo worker-rol.</span><span class="sxs-lookup"><span data-stu-id="28f41-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="28f41-139">Wanneer een werkrol wordt gestart, alle programma-uitvoering plaatsvindt binnen Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="28f41-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="28f41-140">Afgesloten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode veroorzaakt Hallo worker rol toorestart.</span><span class="sxs-lookup"><span data-stu-id="28f41-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="28f41-141">Wanneer Hallo worker-rol runtime Hallo async-methode raakt, verzendt alle bewerkingen na Hallo async-methode en vervolgens terugkeert.</span><span class="sxs-lookup"><span data-stu-id="28f41-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="28f41-142">Dit zorgt ervoor dat Hallo worker rol tooexit van Hallo [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en start deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="28f41-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="28f41-143">In de volgende herhaling van de uitvoering van Hallo treffers in de werkrol Hallo Hallo async-methode opnieuw en opnieuw is opgestart, waardoor Hallo worker rol toorecycle ook opnieuw.</span><span class="sxs-lookup"><span data-stu-id="28f41-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-144">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-144">Solution</span></span>
<span data-ttu-id="28f41-145">Plaats alle asynchrone bewerkingen buiten Hallo [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="28f41-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="28f41-146">Roep vervolgens Hallo geherstructureerd async-methode van binnen Hallo [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode, zoals RunAsync () .wait.</span><span class="sxs-lookup"><span data-stu-id="28f41-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="28f41-147">Hello Azure Code analysehulpprogramma kunt u kunt dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="28f41-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="28f41-148">Hallo volgende codefragment wordt getoond hoe Hallo code oplossing voor dit probleem:</span><span class="sxs-lookup"><span data-stu-id="28f41-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="28f41-149">Service Bus Shared Access Signature-verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="28f41-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="28f41-150">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-150">ID</span></span>
<span data-ttu-id="28f41-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="28f41-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-152">Description</span></span>
<span data-ttu-id="28f41-153">Shared Access Signature (SAS) gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="28f41-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="28f41-154">Access Control Service (ACS) wordt voor service bus-verificatie afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="28f41-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="28f41-155">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-156">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-156">Reason</span></span>
<span data-ttu-id="28f41-157">Voor een betere beveiliging vervangt Azure Active Directory authentication ACS door de SAS-verificatie.</span><span class="sxs-lookup"><span data-stu-id="28f41-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="28f41-158">Zie [Azure Active Directory is Hallo toekomstige van ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) voor informatie over het Hallo overgang plan.</span><span class="sxs-lookup"><span data-stu-id="28f41-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-159">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-159">Solution</span></span>
<span data-ttu-id="28f41-160">De SAS-verificatie gebruiken in uw apps.</span><span class="sxs-lookup"><span data-stu-id="28f41-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="28f41-161">Hallo volgende voorbeeld ziet u hoe toouse een bestaande SAS-token tooaccess een service bus-naamruimte of entiteit.</span><span class="sxs-lookup"><span data-stu-id="28f41-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="28f41-162">Zie Hallo volgende onderwerpen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="28f41-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="28f41-163">Zie voor een overzicht [Shared Access Signature-verificatie met Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="28f41-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="28f41-164">Hoe toouse Shared Access Signature-verificatie met Service Bus</span><span class="sxs-lookup"><span data-stu-id="28f41-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="28f41-165">Zie voor een voorbeeldproject [met behulp van Shared Access Signature (SAS)-verificatie met Service Bus-abonnementen](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="28f41-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="28f41-166">Overweeg het gebruik van OnMessage methode tooavoid 'ontvangen lus'</span><span class="sxs-lookup"><span data-stu-id="28f41-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="28f41-167">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-167">ID</span></span>
<span data-ttu-id="28f41-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="28f41-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="28f41-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-169">Description</span></span>
<span data-ttu-id="28f41-170">bij een 'ontvangen lus,' tooavoid aanroepen Hallo **OnMessage** methode is een betere oplossing voor het ontvangen van berichten dan aanroepen Hallo **ontvangen** methode.</span><span class="sxs-lookup"><span data-stu-id="28f41-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="28f41-171">Echter, als u Hallo gebruiken moet **ontvangen** methode en u geeft de wachttijd van een niet-standaard-server, controleert u Hallo server wachttijd is meer dan één minuut.</span><span class="sxs-lookup"><span data-stu-id="28f41-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="28f41-172">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-173">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-173">Reason</span></span>
<span data-ttu-id="28f41-174">Bij het aanroepen van **OnMessage**, Hallo-client wordt gestart van een interne bericht pomp die voortdurend worden opgevraagd Hallo wachtrij of abonnement.</span><span class="sxs-lookup"><span data-stu-id="28f41-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="28f41-175">Deze pomp bericht bevat een oneindige lus die problemen met een aanroep van tooreceive berichten.</span><span class="sxs-lookup"><span data-stu-id="28f41-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="28f41-176">Als er is een time-out opgetreden bij het Hallo-aanroep, moet deze een nieuwe aanroep uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="28f41-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="28f41-177">Hallo-time-outinterval wordt bepaald door de waarde Hallo Hallo [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) eigenschap Hallo [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="28f41-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="28f41-178">Hallo voordeel van **OnMessage** te vergeleken**ontvangen** is dat gebruikers geen toomanually poll-frequentie voor berichten hoeven, uitzonderingen, meerdere berichten tegelijkertijd verwerken en Hallo voltooien berichten.</span><span class="sxs-lookup"><span data-stu-id="28f41-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="28f41-179">Als u aanroept **ontvangen** zonder gebruik van de standaardwaarde worden ervoor Hallo *ServerWaitTime* waarde is meer dan één minuut.</span><span class="sxs-lookup"><span data-stu-id="28f41-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="28f41-180">Instelling *ServerWaitTime* toomore dan één minuut voorkomt u dat Hallo server een time-out opgetreden voordat het Hallo-bericht volledig is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="28f41-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-181">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-181">Solution</span></span>
<span data-ttu-id="28f41-182">Zie Hallo volgen voorbeelden van code voor het gebruik van aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="28f41-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="28f41-183">Zie voor meer informatie [QueueClient.OnMessage methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)en [QueueClient.Receive methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="28f41-184">tooimprove hello prestaties van hello Azure messaging-infrastructuur, Zie Hallo ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="28f41-185">Hallo Hieronder volgt een voorbeeld van het gebruik van **OnMessage** tooreceive berichten.</span><span class="sxs-lookup"><span data-stu-id="28f41-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="28f41-186">Hallo Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met Hallo standaardserver wachttijd.</span><span class="sxs-lookup"><span data-stu-id="28f41-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="28f41-187">Hallo Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met een niet-standaard server wachttijd.</span><span class="sxs-lookup"><span data-stu-id="28f41-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="28f41-188">Overweeg het gebruik van asynchrone Service Bus-methoden</span><span class="sxs-lookup"><span data-stu-id="28f41-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="28f41-189">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-189">ID</span></span>
<span data-ttu-id="28f41-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="28f41-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="28f41-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-191">Description</span></span>
<span data-ttu-id="28f41-192">Gebruik asynchrone methoden tooimprove-prestaties van Service Bus brokered Messaging.</span><span class="sxs-lookup"><span data-stu-id="28f41-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="28f41-193">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-194">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-194">Reason</span></span>
<span data-ttu-id="28f41-195">Met asynchrone methoden kunt toepassing programma gelijktijdigheid omdat elke aanroep uitvoeren Hallo hoofdthread niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="28f41-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="28f41-196">Wanneer u Service Bus messaging-methoden, uitvoeren van een bewerking (verzenden, ontvangen, verwijderen, enz.) tijd in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="28f41-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="28f41-197">Deze tijd bevat Hallo verwerking van Hallo bewerking door Hallo Service Bus-service in toevoeging toohello latentie van Hallo-aanvraag en Hallo-antwoorden.</span><span class="sxs-lookup"><span data-stu-id="28f41-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="28f41-198">tooincrease hello aantal bewerkingen per keer, moeten bewerkingen tegelijkertijd uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="28f41-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="28f41-199">Voor meer informatie raadpleegt u te[aanbevolen procedures voor prestaties verbeteringen met behulp van Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-200">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-200">Solution</span></span>
<span data-ttu-id="28f41-201">Zie [QueueClient klasse (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) voor meer informatie over hoe toouse Hallo asynchrone methode aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="28f41-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="28f41-202">tooimprove hello prestaties van hello Azure messaging-infrastructuur, Zie Hallo ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="28f41-203">U kunt partitionering Service Bus-wachtrijen en onderwerpen</span><span class="sxs-lookup"><span data-stu-id="28f41-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="28f41-204">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-204">ID</span></span>
<span data-ttu-id="28f41-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="28f41-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="28f41-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-206">Description</span></span>
<span data-ttu-id="28f41-207">Partitie Service Bus-wachtrijen en onderwerpen voor betere prestaties bij het Service Bus-berichtenservice.</span><span class="sxs-lookup"><span data-stu-id="28f41-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="28f41-208">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-209">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-209">Reason</span></span>
<span data-ttu-id="28f41-210">Service Bus-wachtrijen en onderwerpen partitioneren verhoogt de doorvoer en de service de beschikbaarheid van prestaties omdat hello totale doorvoer van een gepartitioneerde wachtrij of onderwerp is niet langer door Hallo-prestaties van een enkel bericht broker of berichten-store beperkt.</span><span class="sxs-lookup"><span data-stu-id="28f41-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="28f41-211">Bovendien een tijdelijke onderbreking van berichten-store betekent niet dat een gepartitioneerde wachtrij of onderwerp niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="28f41-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="28f41-212">Zie voor meer informatie [Messaging Entities partitioneren](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-213">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-213">Solution</span></span>
<span data-ttu-id="28f41-214">Hallo code codefragment wordt getoond hoe na toopartition berichtentiteiten.</span><span class="sxs-lookup"><span data-stu-id="28f41-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="28f41-215">Zie voor meer informatie [gepartitioneerd Service Bus-wachtrijen en onderwerpen | Microsoft Azure-Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) en bekijk Hallo [Microsoft Azure Service Bus gepartitioneerd wachtrij](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="28f41-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="28f41-216">Stel geen SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="28f41-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="28f41-217">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-217">ID</span></span>
<span data-ttu-id="28f41-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="28f41-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="28f41-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-219">Description</span></span>
<span data-ttu-id="28f41-220">Vermijd het gebruik van SharedAccessStartTimeset toohello huidige tijd tooimmediately start Hallo beleid voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="28f41-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="28f41-221">U hoeft alleen tooset deze eigenschap als u wilt dat toostart Hallo gedeeld toegangsbeleid op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="28f41-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="28f41-222">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-223">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-223">Reason</span></span>
<span data-ttu-id="28f41-224">Synchronisatie van computerklok zorgt ervoor dat een lichte tijdsverschil tussen datacenters.</span><span class="sxs-lookup"><span data-stu-id="28f41-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="28f41-225">U zou bijvoorbeeld logisch instelling Hallo-begintijd van een opslag-SAS-beleid zien als hello huidige tijd met behulp van DateTime.Now of een vergelijkbare manier Hallo SAS beleid tootake effect onmiddellijk zullen.</span><span class="sxs-lookup"><span data-stu-id="28f41-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="28f41-226">Hallo lichte tijdsverschil tussen datacenters kunnen echter problemen met dit veroorzaken omdat een aantal keren datacenter mogelijk enigszins hoger is dan de begintijd hello, terwijl andere voor het.</span><span class="sxs-lookup"><span data-stu-id="28f41-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="28f41-227">Als gevolg hiervan Hallo SAS-beleid kunt verloopt snel (of zelfs onmiddellijk) als Hallo beleid levensduur te kort is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="28f41-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="28f41-228">Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update tooBlob SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-229">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-229">Solution</span></span>
<span data-ttu-id="28f41-230">Hiermee stelt u de begintijd Hallo van Hallo gedeeld toegangsbeleid Hallo-instructie verwijderd.</span><span class="sxs-lookup"><span data-stu-id="28f41-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="28f41-231">Hello Azure Code analysehulpprogramma biedt een oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="28f41-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="28f41-232">Zie voor meer informatie over beveiligingsbeheer Hallo ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="28f41-233">Hallo volgende codefragment demonstreert Hallo code oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="28f41-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="28f41-234">Gedeeld toegangsbeleid verlooptijdstip meer dan vijf minuten moet</span><span class="sxs-lookup"><span data-stu-id="28f41-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="28f41-235">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-235">ID</span></span>
<span data-ttu-id="28f41-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="28f41-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="28f41-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-237">Description</span></span>
<span data-ttu-id="28f41-238">Er kunnen zich als een vijf minuten verschil in klokken tussen datacenters op verschillende locaties vanwege tooa staat bekend als "tijdsverschil."</span><span class="sxs-lookup"><span data-stu-id="28f41-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="28f41-239">tooprevent hello SAS beleid-token verloopt ingesteld Hallo verstrijken tijd toobe eerder dan gepland, meer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="28f41-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="28f41-240">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-241">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-241">Reason</span></span>
<span data-ttu-id="28f41-242">Datacenters op verschillende locaties Hallo wereld synchroniseren met een kloksignaal.</span><span class="sxs-lookup"><span data-stu-id="28f41-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="28f41-243">Omdat het duurt voor klok signaal tootravel toodifferent locaties, kan er een verschil tijd tussen datacenters op verschillende geografische locaties Hoewel alles zogenaamd is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="28f41-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="28f41-244">Deze tijdsverschil kan invloed hebben op hello toegang tot gedeelde beleid start tijd en verlooptijd-interval.</span><span class="sxs-lookup"><span data-stu-id="28f41-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="28f41-245">Daarom tooensure gedeeld toegangsbeleid wordt direct van kracht, is geen begintijd Hallo opgeeft.</span><span class="sxs-lookup"><span data-stu-id="28f41-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="28f41-246">Zorg Daarnaast Hallo verlooptijd is meer dan 5 minuten tooprevent vroege time-out.</span><span class="sxs-lookup"><span data-stu-id="28f41-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="28f41-247">Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update tooBlob SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-248">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-248">Solution</span></span>
<span data-ttu-id="28f41-249">Zie voor meer informatie over beveiligingsbeheer Hallo ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="28f41-250">Hallo Hier volgt een voorbeeld van een begintijd voor toegang tot gedeelde beleid niet op te geven.</span><span class="sxs-lookup"><span data-stu-id="28f41-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="28f41-251">Hallo Hieronder volgt een voorbeeld van het opgeven van een begintijd voor toegang tot gedeelde beleid met een duur van de beleid-vervaldatum langer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="28f41-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="28f41-252">Zie voor meer informatie [maken en gebruiken van een Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="28f41-253">Gebruik CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="28f41-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="28f41-254">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-254">ID</span></span>
<span data-ttu-id="28f41-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="28f41-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-256">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-256">Description</span></span>
<span data-ttu-id="28f41-257">Met behulp van Hallo [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) klasse voor projecten, zoals Azure-Website en Azure mobile services won't introduceren runtime-problemen.</span><span class="sxs-lookup"><span data-stu-id="28f41-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="28f41-258">Als een best practice, het is echter een goed idee toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) uniforme wijze van het beheren van configuraties voor alle Azure-Cloud-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="28f41-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="28f41-259">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-260">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-260">Reason</span></span>
<span data-ttu-id="28f41-261">CloudConfigurationManager leest Hallo configuratie bestand juiste toohello toepassing-omgeving.</span><span class="sxs-lookup"><span data-stu-id="28f41-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="28f41-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="28f41-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="28f41-263">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-263">Solution</span></span>
<span data-ttu-id="28f41-264">Uw code toouse Hallo opsplitsen [klasse CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="28f41-265">Een code-oplossing voor dit probleem wordt verstrekt door hello Azure Code analysehulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="28f41-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="28f41-266">Hallo volgende codefragment demonstreert Hallo code oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="28f41-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="28f41-267">Vervangen</span><span class="sxs-lookup"><span data-stu-id="28f41-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="28f41-268">met</span><span class="sxs-lookup"><span data-stu-id="28f41-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="28f41-269">Hier volgt een voorbeeld van hoe toostore Hallo configuratie-instelling in een App.config- of Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="28f41-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="28f41-270">Hallo instellingen toohello appSettings sectie van het configuratiebestand Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="28f41-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="28f41-271">Hallo volgt Hallo Web.config-bestand voor het vorige codevoorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="28f41-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="28f41-272">Vermijd het gebruik van vastgelegde verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="28f41-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="28f41-273">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-273">ID</span></span>
<span data-ttu-id="28f41-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="28f41-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="28f41-275">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-275">Description</span></span>
<span data-ttu-id="28f41-276">Als u gebruik verbindingsreeksen met vastgelegde en u tooupdate moet ze later kunt u toomake wijzigingen tooyour broncode hebben en Hallo toepassing opnieuw te compileren.</span><span class="sxs-lookup"><span data-stu-id="28f41-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="28f41-277">Echter, als u de verbindingstekenreeksen in een configuratiebestand opslaat, u kunt ze later wijzigen door simpelweg bijwerken Hallo-configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="28f41-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="28f41-278">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-279">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-279">Reason</span></span>
<span data-ttu-id="28f41-280">Hard-coding van verbindingsreeksen is een ongeldige procedure omdat hierdoor problemen wanneer verbindingsreeksen moeten toobe snel worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="28f41-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="28f41-281">Bovendien als Hallo project toobe toosource besturingselement ingecheckt moet, vastgelegde verbindingsreeksen leiden tot beveiligingsproblemen omdat Hallo tekenreeksen kunnen worden weergegeven in de broncode Hallo.</span><span class="sxs-lookup"><span data-stu-id="28f41-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-282">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-282">Solution</span></span>
<span data-ttu-id="28f41-283">Verbindingsreeksen opslaan in Hallo-configuratiebestanden of Azure-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="28f41-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="28f41-284">Gebruiken voor zelfstandige toepassingen, instellingen voor app.config toostore verbindingstekenreeks.</span><span class="sxs-lookup"><span data-stu-id="28f41-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="28f41-285">Gebruik web.config toostore verbindingsreeksen voor IIS gehoste webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="28f41-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="28f41-286">Gebruik voor ASP.NET-toepassingen vNext configuration.json toostore verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="28f41-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="28f41-287">Zie voor meer informatie over het gebruik van configuraties bestanden zoals web.config of app.config [ASP.NET Web configuratie-instructies](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="28f41-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="28f41-288">Zie voor informatie over hoe Azure-omgeving variabelen werken, [Azure websites: tekenreeksen van toepassingen en verbinding tekenreeksen werken](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="28f41-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="28f41-289">Zie voor meer informatie over het opslaan van de verbindingsreeks in broncodebeheer [te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in de bron code opslagplaats](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="28f41-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="28f41-290">Diagnostische gegevens configuratiebestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="28f41-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="28f41-291">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-291">ID</span></span>
<span data-ttu-id="28f41-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="28f41-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-293">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-293">Description</span></span>
<span data-ttu-id="28f41-294">In plaats van de diagnostische instellingen configureren in uw code zoals met behulp van Hallo Microsoft.WindowsAzure.Diagnostics programming API, moet u de diagnostische instellingen configureren in Hallo diagnostics.wadcfg-bestand.</span><span class="sxs-lookup"><span data-stu-id="28f41-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="28f41-295">(Of diagnostics.wadcfgx als u gebruikmaakt van Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="28f41-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="28f41-296">Op deze manier kunt u instellingen voor diagnostische gegevens zonder toorecompile uw code.</span><span class="sxs-lookup"><span data-stu-id="28f41-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="28f41-297">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-298">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-298">Reason</span></span>
<span data-ttu-id="28f41-299">Voordat u Azure SDK 2,5 (die gebruikmaakt van Azure diagnostics 1.3), Azure Diagnostics (af) kan worden geconfigureerd met behulp van verschillende methoden gebruiken: toe te voegen toohello configuratie blob in de opslag, via imperatieve code, declaratieve configuratie of Hallo-standaard de configuratie.</span><span class="sxs-lookup"><span data-stu-id="28f41-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="28f41-300">Hallo voorkeur echter manier tooconfigure diagnostische gegevens is een XML-configuratiebestand (diagnostics.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger) in het toepassingsproject Hallo toouse.</span><span class="sxs-lookup"><span data-stu-id="28f41-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="28f41-301">In deze benadering kan Hallo diagnostics.wadcfg bestand volledig Hallo-configuratie is gedefinieerd en worden bijgewerkt en geïmplementeerd op wordt.</span><span class="sxs-lookup"><span data-stu-id="28f41-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="28f41-302">Een combinatie van Hallo gebruik van Hallo diagnostics.wadcfg configuratiebestand Hello programmatische methoden voor het instellen van configuraties met behulp van Hallo [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)of [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) klassen kunnen tooconfusion leiden.</span><span class="sxs-lookup"><span data-stu-id="28f41-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="28f41-303">Zie [initialiseren of Azure Diagnostics-configuratie wijzigen](https://msdn.microsoft.com/library/azure/hh411537.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="28f41-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="28f41-304">Beginnend met af 1.3 (opgenomen in de Azure SDK 2.5), is niet meer mogelijk toouse code tooconfigure diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="28f41-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="28f41-305">Als gevolg hiervan kunt u alleen Hallo configuratie tijdens het toepassen van of bijwerken van Hallo-extensie voor diagnostische gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="28f41-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-306">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-306">Solution</span></span>
<span data-ttu-id="28f41-307">Gebruik Hallo diagnostics configuration designer toomove diagnostische instellingen toohello diagnostics configuratiebestand (diagnositcs.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger).</span><span class="sxs-lookup"><span data-stu-id="28f41-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="28f41-308">Ook wordt aanbevolen dat u installeert [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) en de meest recente diagnostics functie Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="28f41-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="28f41-309">Kies Eigenschappen in het snelmenu Hallo voor dat u wilt dat tooconfigure Hallo-rol, en kies vervolgens tabblad Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="28f41-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="28f41-310">In Hallo **Diagnostics** sectie, zorg ervoor dat Hallo **diagnostische gegevens inschakelen** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="28f41-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="28f41-311">Kies Hallo **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="28f41-311">Choose hello **Configure** button.</span></span>

   ![Toegang tot de optie voor Hallo diagnostische gegevens inschakelen](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="28f41-313">Zie [diagnostische gegevens configureren voor Azure Cloud Services en virtuele Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="28f41-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="28f41-314">Vermijd DbContext-objecten als statische declareren</span><span class="sxs-lookup"><span data-stu-id="28f41-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="28f41-315">Id</span><span class="sxs-lookup"><span data-stu-id="28f41-315">ID</span></span>
<span data-ttu-id="28f41-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="28f41-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="28f41-317">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="28f41-317">Description</span></span>
<span data-ttu-id="28f41-318">toosave geheugen, DBContext-objecten als statische declareren voorkomen.</span><span class="sxs-lookup"><span data-stu-id="28f41-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="28f41-319">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="28f41-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="28f41-320">Reden</span><span class="sxs-lookup"><span data-stu-id="28f41-320">Reason</span></span>
<span data-ttu-id="28f41-321">Objecten van de DBContext houdt Hallo queryresultaten vanuit elke aanroep.</span><span class="sxs-lookup"><span data-stu-id="28f41-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="28f41-322">Statische DBContext-objecten zijn niet verwijderd totdat Hallo toepassingsdomein verwijderd is.</span><span class="sxs-lookup"><span data-stu-id="28f41-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="28f41-323">Een statisch DBContext-object kan daarom grote hoeveelheden geheugen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="28f41-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="28f41-324">Oplossing</span><span class="sxs-lookup"><span data-stu-id="28f41-324">Solution</span></span>
<span data-ttu-id="28f41-325">DBContext declareren als een lokale variabele of een van de niet-statisch exemplaarveld, gebruiken voor een taak en vervolgens laat u dit na gebruik worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="28f41-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="28f41-326">Hallo volgende voorbeeldklasse MVC-controller ziet u hoe toouse Hallo DBContext-object.</span><span class="sxs-lookup"><span data-stu-id="28f41-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="28f41-327">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28f41-327">Next steps</span></span>
<span data-ttu-id="28f41-328">toolearn meer informatie over het optimaliseren van en probleemoplossing van apps van Azure, Zie [een web-app in Azure App Service met behulp van Visual Studio oplossen](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="28f41-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
