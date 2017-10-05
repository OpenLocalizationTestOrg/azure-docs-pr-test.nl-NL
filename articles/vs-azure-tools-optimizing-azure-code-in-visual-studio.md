---
title: Optimaliseren van uw Azure-code in Visual Studio | Microsoft Docs
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
ms.openlocfilehash: 8f145502a856798d6e69ac11f324c72fa23f938e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="a4c64-103">Optimaliseren van uw Azure-Code</span><span class="sxs-lookup"><span data-stu-id="a4c64-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="a4c64-104">Wanneer u apps die gebruikmaken van Microsoft Azure programmeren, zijn er enkele codering procedures die u volgen moet om te voorkomen dat u problemen met app-schaalbaarheid, werking en prestaties in een cloudomgeving.</span><span class="sxs-lookup"><span data-stu-id="a4c64-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="a4c64-105">Microsoft biedt een analyseprogramma Azure Code die wordt herkend en identificeert diverse van deze problemen meestal aangetroffen en kunt u deze kunt oplossen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="a4c64-106">U kunt het hulpprogramma in Visual Studio via NuGet downloaden.</span><span class="sxs-lookup"><span data-stu-id="a4c64-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="a4c64-107">Azure Code Analysis-regels</span><span class="sxs-lookup"><span data-stu-id="a4c64-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="a4c64-108">Het hulpmiddel Azure Code maakt gebruik van de volgende regels automatisch uw Azure code markeren wanneer er bekende problemen met prestaties beïnvloeden.</span><span class="sxs-lookup"><span data-stu-id="a4c64-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="a4c64-109">Gevonden problemen worden weergegeven als een waarschuwingen of compilatiefouten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="a4c64-110">Code-oplossingen of suggesties om op te lossen waarschuwingen of fouten zijn vaak door middel van een gloeilampje opgegeven.</span><span class="sxs-lookup"><span data-stu-id="a4c64-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="a4c64-111">Vermijd het gebruik van standaard (in-process) sessiestatusmodus gebruiken</span><span class="sxs-lookup"><span data-stu-id="a4c64-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-112">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-112">ID</span></span>
<span data-ttu-id="a4c64-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="a4c64-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-114">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-114">Description</span></span>
<span data-ttu-id="a4c64-115">Als u de sessiestatusmodus (in-process) standaard voor cloud-toepassingen gebruikt, kunt u de sessiestatus kunt verliezen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="a4c64-116">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-117">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-117">Reason</span></span>
<span data-ttu-id="a4c64-118">De sessiestatusmodus in het web.config-bestand opgegeven is in-process standaard.</span><span class="sxs-lookup"><span data-stu-id="a4c64-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="a4c64-119">Als u geen vermelding in het configuratiebestand is opgegeven, moet de modus voor sessiestatus standaard ook in-process.</span><span class="sxs-lookup"><span data-stu-id="a4c64-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="a4c64-120">De modus in-process sessiestatus in geheugen opgeslagen op de webserver.</span><span class="sxs-lookup"><span data-stu-id="a4c64-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="a4c64-121">Wanneer een exemplaar opnieuw is opgestart of een nieuw exemplaar wordt gebruikt voor de load balancer of failover-ondersteuning, wordt de sessiestatus opgeslagen in het geheugen op de webserver is niet opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="a4c64-122">Deze situatie wordt voorkomen dat de toepassing wordt schaalbare in de cloud.</span><span class="sxs-lookup"><span data-stu-id="a4c64-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="a4c64-123">ASP.NET-sessiestatus ondersteunt verschillende verschillende opslagopties voor sessiestatusgegevens: InProc, StateServer, SQL Server, aangepast, en uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="a4c64-124">Het verdient aanbeveling dat u aangepaste modus als host voor gegevens op een externe sessiestatus-winkel, zoals gebruiken [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="a4c64-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-125">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-125">Solution</span></span>
<span data-ttu-id="a4c64-126">Een aanbevolen methode is dat de sessiestatus wordt opgeslagen op een beheerde cacheservice.</span><span class="sxs-lookup"><span data-stu-id="a4c64-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="a4c64-127">Informatie over het gebruik [Azure Session State-provider voor Redis](http://go.microsoft.com/fwlink/?LinkId=401521) voor het opslaan van de sessiestatus.</span><span class="sxs-lookup"><span data-stu-id="a4c64-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="a4c64-128">U kunt de sessiestatus ook opslaan in andere locaties om te controleren of uw toepassing schaalbare in de cloud.</span><span class="sxs-lookup"><span data-stu-id="a4c64-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="a4c64-129">Voor meer informatie over alternatieve oplossingen Lees [sessie status modi](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="a4c64-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="a4c64-130">Voer methode mag geen asynchrone</span><span class="sxs-lookup"><span data-stu-id="a4c64-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-131">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-131">ID</span></span>
<span data-ttu-id="a4c64-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="a4c64-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-133">Description</span></span>
<span data-ttu-id="a4c64-134">Maken van asynchrone methoden (zoals [await](https://msdn.microsoft.com/library/hh156528.aspx)) buiten de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en roept u de async-methoden van [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="a4c64-135">Het declareren van de [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode als asynchroon zorgt ervoor dat de werkrol een lus opnieuw invoeren.</span><span class="sxs-lookup"><span data-stu-id="a4c64-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="a4c64-136">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-137">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-137">Reason</span></span>
<span data-ttu-id="a4c64-138">Het aanroepen van asynchrone methoden in de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode zorgt ervoor dat de runtime cloud service wilt recyclen van de werkrol.</span><span class="sxs-lookup"><span data-stu-id="a4c64-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="a4c64-139">Wanneer een werkrol wordt gestart, alle programma-uitvoering vindt plaats in de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="a4c64-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a4c64-140">Afsluiten van de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode zorgt ervoor dat de werkrol om opnieuw te starten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="a4c64-141">Wanneer de runtime worker-rol bij de async-methode aankomt, verzendt alle bewerkingen na de async-methode en vervolgens terugkeert.</span><span class="sxs-lookup"><span data-stu-id="a4c64-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="a4c64-142">Dit zorgt ervoor dat de werkrol om af te sluiten van de [ [ [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode en start deze opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a4c64-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="a4c64-143">In de volgende herhaling van de uitvoering van de werkrol de async-methode opnieuw treffers en opnieuw is opgestart, waardoor de werkrol wilt recyclen ook opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a4c64-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-144">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-144">Solution</span></span>
<span data-ttu-id="a4c64-145">Plaats alle asynchrone bewerkingen buiten de [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="a4c64-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="a4c64-146">Roep vervolgens de geherstructureerd async-methode van binnen de [ [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) methode, zoals RunAsync () .wait.</span><span class="sxs-lookup"><span data-stu-id="a4c64-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="a4c64-147">Het hulpmiddel Azure Code kunt u kunt dit probleem oplossen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="a4c64-148">Het volgende codefragment wordt getoond hoe de code-oplossing voor dit probleem:</span><span class="sxs-lookup"><span data-stu-id="a4c64-148">The following code snippet demonstrates the code fix for this issue:</span></span>

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

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="a4c64-149">Service Bus Shared Access Signature-verificatie gebruiken</span><span class="sxs-lookup"><span data-stu-id="a4c64-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-150">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-150">ID</span></span>
<span data-ttu-id="a4c64-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="a4c64-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-152">Description</span></span>
<span data-ttu-id="a4c64-153">Shared Access Signature (SAS) gebruiken voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="a4c64-154">Access Control Service (ACS) wordt voor service bus-verificatie afgeschaft.</span><span class="sxs-lookup"><span data-stu-id="a4c64-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="a4c64-155">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-156">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-156">Reason</span></span>
<span data-ttu-id="a4c64-157">Voor een betere beveiliging vervangt Azure Active Directory authentication ACS door de SAS-verificatie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="a4c64-158">Zie [Azure Active Directory is de toekomst van ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) voor meer informatie over het plan overgang.</span><span class="sxs-lookup"><span data-stu-id="a4c64-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-159">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-159">Solution</span></span>
<span data-ttu-id="a4c64-160">De SAS-verificatie gebruiken in uw apps.</span><span class="sxs-lookup"><span data-stu-id="a4c64-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="a4c64-161">Het volgende voorbeeld ziet hoe u een bestaande SAS-token gebruikt voor toegang tot een service bus-naamruimte of entiteit.</span><span class="sxs-lookup"><span data-stu-id="a4c64-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="a4c64-162">Zie de volgende onderwerpen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-162">See the following topics for more information.</span></span>

* <span data-ttu-id="a4c64-163">Zie voor een overzicht [Shared Access Signature-verificatie met Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="a4c64-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="a4c64-164">Het gebruik van Shared Access Signature-verificatie met Service Bus</span><span class="sxs-lookup"><span data-stu-id="a4c64-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="a4c64-165">Zie voor een voorbeeldproject [met behulp van Shared Access Signature (SAS)-verificatie met Service Bus-abonnementen](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="a4c64-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="a4c64-166">Overweeg het gebruik van OnMessage methode om te voorkomen dat 'ontvangen lus'</span><span class="sxs-lookup"><span data-stu-id="a4c64-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-167">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-167">ID</span></span>
<span data-ttu-id="a4c64-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="a4c64-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-169">Description</span></span>
<span data-ttu-id="a4c64-170">Om te voorkomen dat momenteel in een 'ontvangen lus,' aanroepen van de **OnMessage** methode is een betere oplossing voor het ontvangen van berichten dan aanroepen de **ontvangen** methode.</span><span class="sxs-lookup"><span data-stu-id="a4c64-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="a4c64-171">Echter, als u moet de **ontvangen** methode en u geeft de wachttijd van een niet-standaard-server, controleert u de wachttijd van de server is meer dan één minuut.</span><span class="sxs-lookup"><span data-stu-id="a4c64-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="a4c64-172">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-173">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-173">Reason</span></span>
<span data-ttu-id="a4c64-174">Bij het aanroepen van **OnMessage**, de client wordt gestart van een interne bericht pomp die voortdurend de wachtrij of abonnement peilt.</span><span class="sxs-lookup"><span data-stu-id="a4c64-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="a4c64-175">Deze pomp bericht bevat een oneindige lus die problemen met een aanroep om berichten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="a4c64-176">Als de aanroep van een optreedt time-out, moet deze een nieuwe aanroep uitgeeft.</span><span class="sxs-lookup"><span data-stu-id="a4c64-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="a4c64-177">De time-outinterval wordt bepaald door de waarde van de [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) eigenschap van de [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a4c64-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="a4c64-178">Het voordeel van **OnMessage** vergeleken met **ontvangen** is dat gebruikers niet handmatig poll-frequentie voor berichten, uitzonderingen, meerdere berichten parallel verwerken en de berichten te voltooien.</span><span class="sxs-lookup"><span data-stu-id="a4c64-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="a4c64-179">Als u aanroept **ontvangen** zonder de standaardwaarde wordt gebruikt, moet u de *ServerWaitTime* waarde is meer dan één minuut.</span><span class="sxs-lookup"><span data-stu-id="a4c64-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="a4c64-180">Instelling *ServerWaitTime* met meer dan één minuut voorkomt u dat de server een time-out opgetreden voordat het bericht volledig is ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-181">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-181">Solution</span></span>
<span data-ttu-id="a4c64-182">Zie de volgende codevoorbeelden voor het gebruik van aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="a4c64-183">Zie voor meer informatie [QueueClient.OnMessage methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)en [QueueClient.Receive methode (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="a4c64-184">Om te verbeteren de prestaties van de Azure messaging-infrastructuur, Zie het ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="a4c64-185">Hieronder volgt een voorbeeld van het gebruik van **OnMessage** om berichten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="a4c64-186">Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met de standaardserver wachttijd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-186">The following is an example of using **Receive** with the default server wait time.</span></span>

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

<span data-ttu-id="a4c64-187">Hieronder volgt een voorbeeld van het gebruik van **ontvangen** met een niet-standaard server wachttijd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

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
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="a4c64-188">Overweeg het gebruik van asynchrone Service Bus-methoden</span><span class="sxs-lookup"><span data-stu-id="a4c64-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-189">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-189">ID</span></span>
<span data-ttu-id="a4c64-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="a4c64-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-191">Description</span></span>
<span data-ttu-id="a4c64-192">Asynchrone Service Bus-methoden gebruiken voor het verbeteren de prestaties met brokered messaging.</span><span class="sxs-lookup"><span data-stu-id="a4c64-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="a4c64-193">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-194">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-194">Reason</span></span>
<span data-ttu-id="a4c64-195">Met asynchrone methoden kunt toepassing programma gelijktijdigheid omdat de hoofdthread uitvoeren van elke aanroep niet blokkeert.</span><span class="sxs-lookup"><span data-stu-id="a4c64-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="a4c64-196">Wanneer u Service Bus messaging-methoden, uitvoeren van een bewerking (verzenden, ontvangen, verwijderen, enz.) tijd in beslag neemt.</span><span class="sxs-lookup"><span data-stu-id="a4c64-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="a4c64-197">Deze tijd bevat de verwerking van de bewerking door de Service Bus-service naast de latentie van de aanvraag en het antwoord.</span><span class="sxs-lookup"><span data-stu-id="a4c64-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="a4c64-198">Voor een verhoging van het aantal bewerkingen per keer moeten worden operations gelijktijdig worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="a4c64-199">Raadpleeg voor meer informatie [aanbevolen procedures voor prestaties verbeteringen met behulp van Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-200">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-200">Solution</span></span>
<span data-ttu-id="a4c64-201">Zie [QueueClient klasse (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) voor informatie over het gebruik van de aanbevolen asynchrone methode.</span><span class="sxs-lookup"><span data-stu-id="a4c64-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="a4c64-202">Om te verbeteren de prestaties van de Azure messaging-infrastructuur, Zie het ontwerppatroon [asynchrone Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="a4c64-203">U kunt partitionering Service Bus-wachtrijen en onderwerpen</span><span class="sxs-lookup"><span data-stu-id="a4c64-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-204">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-204">ID</span></span>
<span data-ttu-id="a4c64-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="a4c64-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-206">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-206">Description</span></span>
<span data-ttu-id="a4c64-207">Partitie Service Bus-wachtrijen en onderwerpen voor betere prestaties bij het Service Bus-berichtenservice.</span><span class="sxs-lookup"><span data-stu-id="a4c64-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="a4c64-208">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-209">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-209">Reason</span></span>
<span data-ttu-id="a4c64-210">Service Bus-wachtrijen en onderwerpen partitioneren verhoogt de doorvoer en de service de beschikbaarheid van prestaties omdat de totale doorvoer van een gepartitioneerde wachtrij of onderwerp niet langer door de prestaties van een enkel bericht broker of berichten-store beperkt is.</span><span class="sxs-lookup"><span data-stu-id="a4c64-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="a4c64-211">Bovendien een tijdelijke onderbreking van berichten-store betekent niet dat een gepartitioneerde wachtrij of onderwerp niet beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="a4c64-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="a4c64-212">Zie voor meer informatie [Messaging Entities partitioneren](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-213">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-213">Solution</span></span>
<span data-ttu-id="a4c64-214">Het volgende codefragment laat zien hoe voor het partitioneren van berichtentiteiten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="a4c64-215">Zie voor meer informatie [gepartitioneerd Service Bus-wachtrijen en onderwerpen | Microsoft Azure-Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) en bekijk de [Microsoft Azure Service Bus gepartitioneerd wachtrij](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="a4c64-216">Stel geen SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="a4c64-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-217">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-217">ID</span></span>
<span data-ttu-id="a4c64-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="a4c64-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-219">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-219">Description</span></span>
<span data-ttu-id="a4c64-220">Vermijd het gebruik van SharedAccessStartTimeset aan de huidige tijd om direct te starten het beleid voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="a4c64-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="a4c64-221">Alleen moet u deze eigenschap instellen als u wilt het beleid voor gedeelde toegang op een later tijdstip te starten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="a4c64-222">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-223">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-223">Reason</span></span>
<span data-ttu-id="a4c64-224">Synchronisatie van computerklok zorgt ervoor dat een lichte tijdsverschil tussen datacenters.</span><span class="sxs-lookup"><span data-stu-id="a4c64-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="a4c64-225">Bijvoorbeeld, logisch daar de begintijd van een SAS-beveiligingsbeleid van de opslag aan het huidige tijdstip instellen met behulp van DateTime.Now of een vergelijkbare manier, zal het SAS-beleid wordt onmiddellijk van kracht.</span><span class="sxs-lookup"><span data-stu-id="a4c64-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="a4c64-226">Echter, het lichte tijdsverschil tussen datacentra kunnen problemen veroorzaken met dit omdat een aantal keren datacenter mogelijk enigszins hoger is dan de begintijd, terwijl andere voor deze.</span><span class="sxs-lookup"><span data-stu-id="a4c64-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="a4c64-227">Als gevolg hiervan het SAS-beleid kunt verloopt snel (of zelfs onmiddellijk) als de levensduur van het beleid te kort is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="a4c64-228">Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update voor Blob-SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-229">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-229">Solution</span></span>
<span data-ttu-id="a4c64-230">Verwijder de instructie die de begintijd van het beleid voor gedeelde toegang ingesteld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="a4c64-231">Het hulpmiddel Azure Code biedt een oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="a4c64-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="a4c64-232">Zie voor meer informatie over beveiligingsbeheer het ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a4c64-233">Het volgende codefragment bevat de code-oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="a4c64-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="a4c64-234">Gedeeld toegangsbeleid verlooptijdstip meer dan vijf minuten moet</span><span class="sxs-lookup"><span data-stu-id="a4c64-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-235">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-235">ID</span></span>
<span data-ttu-id="a4c64-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="a4c64-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-237">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-237">Description</span></span>
<span data-ttu-id="a4c64-238">Er kunnen zich als een vijf minuten verschil in klokken tussen datacenters op verschillende locaties als gevolg van een voorwaarde bekend als "tijdsverschil."</span><span class="sxs-lookup"><span data-stu-id="a4c64-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="a4c64-239">Om te voorkomen dat de SAS instellen-token verloopt beleid eerdere versies dan gepland, het verlooptijdstip moet meer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="a4c64-240">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-241">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-241">Reason</span></span>
<span data-ttu-id="a4c64-242">Datacenters op verschillende locaties wereldwijd synchroniseren met een kloksignaal.</span><span class="sxs-lookup"><span data-stu-id="a4c64-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="a4c64-243">Omdat het duurt voor kloksignaal naar verschillende locaties reizen, kan er een verschil tijd tussen datacenters op verschillende geografische locaties Hoewel alles zogenaamd is gesynchroniseerd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="a4c64-244">Deze tijdsverschil kan invloed hebben op de toegang tot gedeelde policy start tijd en verlooptijd-interval.</span><span class="sxs-lookup"><span data-stu-id="a4c64-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="a4c64-245">Daarom om ervoor te zorgen gedeeld toegangsbeleid wordt direct van kracht, geeft u de begintijd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="a4c64-246">Bovendien moet dat de vervaltijd is langer dan vijf minuten om te voorkomen dat eerdere time-out.</span><span class="sxs-lookup"><span data-stu-id="a4c64-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="a4c64-247">Zie voor meer informatie over het gebruik van Shared Access Signature op Azure-opslag [introductie van tabel SAS (Shared Access Signature), wachtrij SAS en update voor Blob-SAS - Team Blog van Microsoft Azure Storage - Site-MSDN-Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-248">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-248">Solution</span></span>
<span data-ttu-id="a4c64-249">Zie voor meer informatie over beveiligingsbeheer het ontwerppatroon [Valet sleutel patroon](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="a4c64-250">Hier volgt een voorbeeld van een begintijd voor toegang tot gedeelde beleid niet op te geven.</span><span class="sxs-lookup"><span data-stu-id="a4c64-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a4c64-251">Hier volgt een voorbeeld van het opgeven van een begintijd voor toegang tot gedeelde beleid met een duur van de beleid-vervaldatum langer dan vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="a4c64-252">Zie voor meer informatie [maken en gebruiken van een Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="a4c64-253">Gebruik CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a4c64-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-254">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-254">ID</span></span>
<span data-ttu-id="a4c64-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="a4c64-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-256">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-256">Description</span></span>
<span data-ttu-id="a4c64-257">Met behulp van de [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) klasse voor projecten, zoals Azure-Website en Azure mobile services won't introduceren runtime-problemen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="a4c64-258">Als een best practice, het is echter een goed idee om te gebruiken Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) uniforme wijze van het beheren van configuraties voor alle Azure-Cloud-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="a4c64-259">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-260">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-260">Reason</span></span>
<span data-ttu-id="a4c64-261">CloudConfigurationManager leest het configuratiebestand dat geschikt is voor de omgeving van toepassing.</span><span class="sxs-lookup"><span data-stu-id="a4c64-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="a4c64-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a4c64-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="a4c64-263">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-263">Solution</span></span>
<span data-ttu-id="a4c64-264">Opsplitsen van uw code te gebruiken de [klasse CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="a4c64-265">Een code-oplossing voor dit probleem wordt geleverd door het hulpmiddel Azure Code.</span><span class="sxs-lookup"><span data-stu-id="a4c64-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="a4c64-266">Het volgende codefragment bevat de code-oplossing voor dit probleem.</span><span class="sxs-lookup"><span data-stu-id="a4c64-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="a4c64-267">Vervangen</span><span class="sxs-lookup"><span data-stu-id="a4c64-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="a4c64-268">met</span><span class="sxs-lookup"><span data-stu-id="a4c64-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="a4c64-269">Hier volgt een voorbeeld van het opslaan van de configuratie-instelling in een App.config- of Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="a4c64-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="a4c64-270">De instellingen toevoegen aan de sectie appSettings van het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="a4c64-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="a4c64-271">Hieronder volgt het bestand Web.config voor het vorige codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="a4c64-272">Vermijd het gebruik van vastgelegde verbindingsreeksen</span><span class="sxs-lookup"><span data-stu-id="a4c64-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-273">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-273">ID</span></span>
<span data-ttu-id="a4c64-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="a4c64-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-275">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-275">Description</span></span>
<span data-ttu-id="a4c64-276">Als u vastgelegde verbindingsreeksen en moet u deze later bijwerken, hebt u wijzigingen aanbrengen in de broncode en de toepassing opnieuw te compileren.</span><span class="sxs-lookup"><span data-stu-id="a4c64-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="a4c64-277">Echter, als u de verbindingstekenreeksen in een configuratiebestand opslaat, u kunt ze later wijzigen door simpelweg bijwerken van het configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="a4c64-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="a4c64-278">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-279">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-279">Reason</span></span>
<span data-ttu-id="a4c64-280">Hard-coding van verbindingsreeksen is een ongeldige procedure omdat hierdoor problemen wanneer verbindingsreeksen moeten snel worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="a4c64-281">Bovendien, als het project worden gecontroleerd moet om verbinding met broncodebeheer, vastgelegde verbindingsreeksen leiden tot beveiligingsproblemen omdat de tekenreeksen kunnen worden weergegeven in de broncode.</span><span class="sxs-lookup"><span data-stu-id="a4c64-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-282">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-282">Solution</span></span>
<span data-ttu-id="a4c64-283">Verbindingsreeksen worden opgeslagen in configuratiebestanden of Azure-omgevingen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="a4c64-284">Voor zelfstandige toepassingen app.config te gebruiken voor het opslaan van verbindingstekenreeksinstellingen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="a4c64-285">Gebruik web.config voor het opslaan van verbindingsreeksen voor IIS gehoste webtoepassingen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="a4c64-286">Gebruik voor ASP.NET-toepassingen vNext configuration.json voor het opslaan van verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="a4c64-287">Zie voor meer informatie over het gebruik van configuraties bestanden zoals web.config of app.config [ASP.NET Web configuratie-instructies](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="a4c64-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="a4c64-288">Zie voor informatie over hoe Azure-omgeving variabelen werken, [Azure websites: tekenreeksen van toepassingen en verbinding tekenreeksen werken](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="a4c64-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="a4c64-289">Zie voor meer informatie over het opslaan van de verbindingsreeks in broncodebeheer [te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in de bron code opslagplaats](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="a4c64-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="a4c64-290">Diagnostische gegevens configuratiebestand gebruiken</span><span class="sxs-lookup"><span data-stu-id="a4c64-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-291">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-291">ID</span></span>
<span data-ttu-id="a4c64-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="a4c64-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-293">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-293">Description</span></span>
<span data-ttu-id="a4c64-294">In plaats van de diagnostische instellingen configureren in uw code zoals met behulp van de API programming Microsoft.WindowsAzure.Diagnostics, moet u de diagnostische instellingen configureren in het bestand diagnostics.wadcfg.</span><span class="sxs-lookup"><span data-stu-id="a4c64-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="a4c64-295">(Of diagnostics.wadcfgx als u gebruikmaakt van Azure SDK 2.5).</span><span class="sxs-lookup"><span data-stu-id="a4c64-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="a4c64-296">Op deze manier kunt u de diagnostische instellingen kunt wijzigen zonder de code compileren.</span><span class="sxs-lookup"><span data-stu-id="a4c64-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="a4c64-297">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-298">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-298">Reason</span></span>
<span data-ttu-id="a4c64-299">Voordat u Azure SDK 2,5 (die gebruikmaakt van Azure diagnostics 1.3), Azure Diagnostics (af) kan worden geconfigureerd met behulp van verschillende methoden gebruiken: toe te voegen aan de configuratie-blob in de opslag, via imperatieve code, declaratieve configuratie of de standaardwaarde de configuratie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="a4c64-300">De beste manier voor het configureren van diagnostische gegevens is echter een XML-configuratiebestand (diagnostics.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger) in het toepassingsproject gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4c64-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="a4c64-301">In deze benadering, kan het bestand diagnostics.wadcfg volledig definieert de configuratie en worden bijgewerkt en geïmplementeerd op wordt.</span><span class="sxs-lookup"><span data-stu-id="a4c64-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="a4c64-302">Het gebruik van het configuratiebestand diagnostics.wadcfg combineren met de programmatische methoden voor het instellen van configuraties met behulp van de [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)of [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)klassen kunnen tot verwarring leiden.</span><span class="sxs-lookup"><span data-stu-id="a4c64-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="a4c64-303">Zie [initialiseren of Azure Diagnostics-configuratie wijzigen](https://msdn.microsoft.com/library/azure/hh411537.aspx) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="a4c64-304">Beginnend met af 1.3 (opgenomen in de Azure SDK 2.5), is het niet meer code gebruiken voor het configureren van diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="a4c64-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="a4c64-305">Als gevolg hiervan kunt u alleen de configuratie tijdens het toepassen van of bijwerken van de extensie voor diagnostische gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="a4c64-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-306">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-306">Solution</span></span>
<span data-ttu-id="a4c64-307">Gebruik de ontwerpfunctie van de configuratie van diagnostische gegevens te verplaatsen van diagnostische instellingen voor het configuratiebestand van diagnostische gegevens (diagnositcs.wadcfg of diagnositcs.wadcfgx voor SDK 2.5 en hoger).</span><span class="sxs-lookup"><span data-stu-id="a4c64-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="a4c64-308">Ook wordt aanbevolen dat u installeert [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) en de meest recente diagnostics-functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4c64-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="a4c64-309">In het snelmenu voor de rol die u wilt configureren, kiest u eigenschappen en kies vervolgens het tabblad configuratie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="a4c64-310">In de **Diagnostics** sectie, zorg ervoor dat de **diagnostische gegevens inschakelen** selectievakje is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a4c64-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="a4c64-311">Kies de **configureren** knop.</span><span class="sxs-lookup"><span data-stu-id="a4c64-311">Choose the **Configure** button.</span></span>

   ![Toegang tot de optie diagnostische gegevens inschakelen](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="a4c64-313">Zie [diagnostische gegevens configureren voor Azure Cloud Services en virtuele Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a4c64-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="a4c64-314">Vermijd DbContext-objecten als statische declareren</span><span class="sxs-lookup"><span data-stu-id="a4c64-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="a4c64-315">Id</span><span class="sxs-lookup"><span data-stu-id="a4c64-315">ID</span></span>
<span data-ttu-id="a4c64-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="a4c64-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="a4c64-317">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a4c64-317">Description</span></span>
<span data-ttu-id="a4c64-318">Vermijd DBContext-objecten als statische declareren voor het opslaan van geheugen.</span><span class="sxs-lookup"><span data-stu-id="a4c64-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="a4c64-319">Deel uw ideeën en feedback op [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="a4c64-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="a4c64-320">Reden</span><span class="sxs-lookup"><span data-stu-id="a4c64-320">Reason</span></span>
<span data-ttu-id="a4c64-321">DBContext-objecten bevatten van elke aanroep van de queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="a4c64-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="a4c64-322">Statische DBContext-objecten zijn niet verwijderd totdat het toepassingsdomein verwijderd is.</span><span class="sxs-lookup"><span data-stu-id="a4c64-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="a4c64-323">Een statisch DBContext-object kan daarom grote hoeveelheden geheugen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4c64-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="a4c64-324">Oplossing</span><span class="sxs-lookup"><span data-stu-id="a4c64-324">Solution</span></span>
<span data-ttu-id="a4c64-325">DBContext declareren als een lokale variabele of een van de niet-statisch exemplaarveld, gebruiken voor een taak en vervolgens laat u dit na gebruik worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a4c64-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="a4c64-326">Het volgende voorbeeld MVC-controllerklasse laat zien hoe de DBContext-object te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a4c64-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
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

## <a name="next-steps"></a><span data-ttu-id="a4c64-327">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4c64-327">Next steps</span></span>
<span data-ttu-id="a4c64-328">Zie voor meer informatie over het optimaliseren van en probleemoplossing van apps van Azure [een web-app in Azure App Service met behulp van Visual Studio oplossen](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="a4c64-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
