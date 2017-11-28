---
title: aaaStart en stop cluster knooppunten tootest Azure microservices | Microsoft Docs
description: Meer informatie over hoe toouse fault injectie tootest Service Fabric-toepassing door starten en stoppen van de clusterknooppunten.
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="d9fee-103">Hallo knooppunt starten en stoppen knooppunt API's vervangen door Hallo knooppunt overgang API</span><span class="sxs-lookup"><span data-stu-id="d9fee-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="d9fee-104">Wat Hallo knooppunt stoppen en starten knooppunt API's doen?</span><span class="sxs-lookup"><span data-stu-id="d9fee-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="d9fee-105">Hallo knooppunt API stoppen (beheerd: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) stopt van een Service Fabric-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="d9fee-106">Een Service Fabric-knooppunt is niet een VM of de machine wordt – Hallo VM of machine wordt nog steeds worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9fee-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="d9fee-107">Voor de rest Hallo van Hallo document 'knooppunt' betekent dat deze Service Fabric-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="d9fee-108">Stoppen van een knooppunt, plaatst het in een *gestopt* status waarbij is geen lid van de cluster Hallo en kan geen host zijn services, dus simuleren een *omlaag* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="d9fee-109">Dit is handig voor het injecteren van fouten in Hallo system tootest uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="d9fee-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="d9fee-110">Hallo Start knooppunt API (beheerd: [StartNodeAsync()][startnode], PowerShell: [Start ServiceFabricNode][startnodeps]]) keert Hallo knooppunt API stoppen  Dit brengt Hallo knooppunt back tooa normale status.</span><span class="sxs-lookup"><span data-stu-id="d9fee-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="d9fee-111">Waarom zijn we deze vervangen?</span><span class="sxs-lookup"><span data-stu-id="d9fee-111">Why are we replacing these?</span></span>

<span data-ttu-id="d9fee-112">Zoals eerder beschreven, een *gestopt* Service Fabric-knooppunt is een knooppunt opzettelijk gericht Hallo stoppen knooppunt API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9fee-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="d9fee-113">Een *omlaag* knooppunt is een knooppunt dat is niet beschikbaar voor een andere reden (bijvoorbeeld Hallo VM of de machine is uitgeschakeld).</span><span class="sxs-lookup"><span data-stu-id="d9fee-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="d9fee-114">Met de Hallo knooppunt API stoppen, Hallo systeem niet beschikbaar toodifferentiate informatie tussen *gestopt* knooppunten en *omlaag* knooppunten.</span><span class="sxs-lookup"><span data-stu-id="d9fee-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="d9fee-115">Er zijn fouten geretourneerd door deze API's zijn niet als beschrijvende zoals ze zijn.</span><span class="sxs-lookup"><span data-stu-id="d9fee-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="d9fee-116">Bijvoorbeeld stoppen knooppunt API aanroepen Hallo op een al *gestopt* knooppunt retourneert fout Hallo *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="d9fee-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="d9fee-117">Deze ervaring kan worden verbeterd.</span><span class="sxs-lookup"><span data-stu-id="d9fee-117">This experience could be improved.</span></span>

<span data-ttu-id="d9fee-118">Hallo duur van die een knooppunt is gestopt voor is ook 'oneindig' tot Hallo die start knooppunt API wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d9fee-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="d9fee-119">We hebben dit kan problemen veroorzaken en gevoelig voor fouten kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="d9fee-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="d9fee-120">We zag bijvoorbeeld problemen waarbij een gebruiker aangeroepen Hallo knooppunt API stoppen op een knooppunt en vervolgens vergeten bent.</span><span class="sxs-lookup"><span data-stu-id="d9fee-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="d9fee-121">Later, was het niet duidelijk als Hallo knooppunt *omlaag* of *gestopt*.</span><span class="sxs-lookup"><span data-stu-id="d9fee-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="d9fee-122">Inleiding tot Hallo knooppunt overgang API 's</span><span class="sxs-lookup"><span data-stu-id="d9fee-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="d9fee-123">We hebt deze problemen boven in een nieuwe reeks API's opgelost.</span><span class="sxs-lookup"><span data-stu-id="d9fee-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="d9fee-124">het nieuwe knooppunt overgang API Hallo (beheerd: [StartNodeTransitionAsync()][snt]) mogelijk gebruikte tootransition een tooa Service Fabric-knooppunt *gestopt* status- of tootransition deze van een *gestopt* status tooa normale werking.</span><span class="sxs-lookup"><span data-stu-id="d9fee-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="d9fee-125">Houd er rekening mee dat Hallo 'Start' in de naam van de Hallo Hallo API verwijst niet toostarting een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="d9fee-126">Het toobeginning een asynchrone bewerking Hallo system uitvoering tootransition Hallo knooppunt tooeither verwijst *gestopt* of de status gestart.</span><span class="sxs-lookup"><span data-stu-id="d9fee-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="d9fee-127">**Gebruik**</span><span class="sxs-lookup"><span data-stu-id="d9fee-127">**Usage**</span></span>

<span data-ttu-id="d9fee-128">Hallo knooppunt overgang API heeft een uitzondering opgetreden bij het aanroepen niet genereren, vervolgens Hallo system Hallo asynchrone bewerking heeft geaccepteerd als deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d9fee-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="d9fee-129">Een geslaagde aanroepen betekent niet dat Hallo bewerking nog is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d9fee-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="d9fee-130">tooget informatie over de huidige status van Hallo bewerking aanroep Hallo knooppunt overgang voortgang API Hallo (beheerd: [GetNodeTransitionProgressAsync()][gntp]) met Hallo-guid die wordt gebruikt bij het aanroepen van knooppunt De API van de overgang voor deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="d9fee-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="d9fee-131">Hallo knooppunt overgang voortgang API retourneert een object NodeTransitionProgress.</span><span class="sxs-lookup"><span data-stu-id="d9fee-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="d9fee-132">Eigenschap van de status van dit object geeft de huidige status Hallo van Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d9fee-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="d9fee-133">Hallo-bewerking wordt uitgevoerd als Hallo status 'actief'.</span><span class="sxs-lookup"><span data-stu-id="d9fee-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="d9fee-134">Als deze is voltooid, wordt de Hallo opnieuw zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="d9fee-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="d9fee-135">Als deze fout is opgetreden, is er een probleem bij het Hallo-bewerking uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d9fee-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="d9fee-136">Hallo resultaat eigenschap uitzondering eigenschap wordt aangegeven welke Hallo uitgeven is.</span><span class="sxs-lookup"><span data-stu-id="d9fee-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="d9fee-137">Zie https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate voor meer informatie over de eigenschap State Hallo en Hallo 'Voorbeeldgebruik' hieronder voor codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d9fee-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="d9fee-138">**Verschillen tussen een gestopte knooppunt en een knooppunt omlaag** als een knooppunt *gestopt* knooppunt overgang API, Hallo-uitvoer van een query voor knooppunt met behulp van Hallo (beheerd: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) wordt aangegeven dat dit knooppunt heeft een *IsStopped* de eigenschapwaarde true.</span><span class="sxs-lookup"><span data-stu-id="d9fee-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="d9fee-139">Houd er rekening mee deze verschilt van de waarde van Hallo Hallo *NodeStatus* eigenschap dicteert *omlaag*.</span><span class="sxs-lookup"><span data-stu-id="d9fee-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="d9fee-140">Als hello *NodeStatus* eigenschap een waarde heeft van *omlaag*, maar *IsStopped* is ingesteld op false, en vervolgens het Hallo-knooppunt is niet gestopt met Hallo knooppunt overgang API en is  *Omlaag* vanwege een andere reden.</span><span class="sxs-lookup"><span data-stu-id="d9fee-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="d9fee-141">Als hello *IsStopped* eigenschap waar is en Hallo *NodeStatus* eigenschap is *omlaag*, en vervolgens deze wordt stilgelegd Hallo knooppunt overgang API gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9fee-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="d9fee-142">Starten van een *gestopt* Hallo knooppunt overgang API-knooppunt retourneert het toofunction als normale lid van de cluster Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d9fee-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="d9fee-143">Hallo uitvoer van Hallo knooppunt query API ziet *IsStopped* als onwaar, en *NodeStatus* als iets dat niet is niet beschikbaar (bijvoorbeeld omhoog).</span><span class="sxs-lookup"><span data-stu-id="d9fee-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="d9fee-144">**Beperkte duur** wanneer u Hallo knooppunt overgang API toostop een knooppunt, een Hallo vereiste parameters, *stopNodeDurationInSeconds*, vertegenwoordigt de hoeveelheid tijd in seconden tookeep Hallo knooppunt Hallo  *gestopt*.</span><span class="sxs-lookup"><span data-stu-id="d9fee-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="d9fee-145">Deze waarde moet liggen binnen het toegestane bereik, waarvoor minimaal 600 en een maximum van 14400 Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9fee-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="d9fee-146">Nadat deze tijd is verstreken, Hallo-knooppunt wordt automatisch opnieuw opgestart zelf in de status van.</span><span class="sxs-lookup"><span data-stu-id="d9fee-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="d9fee-147">Raadpleeg tooSample 1 hieronder voor een voorbeeld van gebruik.</span><span class="sxs-lookup"><span data-stu-id="d9fee-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="d9fee-148">Vermijd de combinatie van knooppunt overgang API's en Hallo knooppunt stoppen en starten knooppunt API's.</span><span class="sxs-lookup"><span data-stu-id="d9fee-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="d9fee-149">Hallo-aanbeveling is Hallo knooppunt overgang API alleen te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9fee-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="d9fee-150">> Als een knooppunt is al gestopt met Hallo knooppunt API stoppen, deze moet worden gestart met Hallo knooppunt API Start eerst voordat u Hallo > knooppunt overgang API's.</span><span class="sxs-lookup"><span data-stu-id="d9fee-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="d9fee-151">Meerdere knooppunt overgang API aanroepen kunnen niet worden doorgevoerd op hetzelfde knooppunt parallel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d9fee-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="d9fee-152">In een dergelijke situatie Hallo knooppunt overgang API wordt > genereert een FabricException met een eigenschapswaarde ErrorCode van NodeTransitionInProgress.</span><span class="sxs-lookup"><span data-stu-id="d9fee-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="d9fee-153">Zodra de overgang van een knooppunt op een specifiek knooppunt heeft > is gestart, moet u wachten totdat het Hallo-bewerking heeft een definitieve status (voltooid, Faulted of ForceCancelled) bereikt voordat u begint een > nieuwe overgang op Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="d9fee-154">Parallelle knooppunt overgang aanroepen op verschillende knooppunten zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="d9fee-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="d9fee-155">Voorbeeld van gebruik</span><span class="sxs-lookup"><span data-stu-id="d9fee-155">Sample Usage</span></span>


<span data-ttu-id="d9fee-156">**Voorbeeld 1** -Hallo volgende voorbeeld wordt Hallo knooppunt overgang API toostop een knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="d9fee-157">**Voorbeeld 2** - hello voorbeeld wordt gestart na een *gestopt* knooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="d9fee-158">Sommige Help-methoden van het eerste voorbeeld hello wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-158">It uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

<span data-ttu-id="d9fee-159">**Voorbeeld 3** - hello volgende voorbeeld toont onjuiste informatie over het gebruik.</span><span class="sxs-lookup"><span data-stu-id="d9fee-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="d9fee-160">Dit gebruik is onjuist omdat Hallo *stopDurationInSeconds* is groter dan het toegestane bereik Hallo biedt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="d9fee-161">Aangezien StartNodeTransitionAsync() met een onherstelbare fout mislukt, Hallo-bewerking is niet geaccepteerd en Hallo voortgang API moet niet worden aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="d9fee-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="d9fee-162">Dit voorbeeld wordt een aantal methoden van het eerste voorbeeld Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-162">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

<span data-ttu-id="d9fee-163">**Voorbeeld 4** - hello volgende voorbeeld toont Hallo foutgegevens die worden geretourneerd van Hallo knooppunt overgang voortgang API wanneer Hallo-bewerking gestart door Hallo knooppunt overgang API is geaccepteerd, maar later tijdens het uitvoeren is mislukt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="d9fee-164">In geval van hello mislukt dit omdat Hallo knooppunt overgang API probeert toostart een knooppunt dat niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="d9fee-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="d9fee-165">Dit voorbeeld wordt een aantal methoden van het eerste voorbeeld Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d9fee-165">This sample uses some helper methods from hello first sample.</span></span>

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
