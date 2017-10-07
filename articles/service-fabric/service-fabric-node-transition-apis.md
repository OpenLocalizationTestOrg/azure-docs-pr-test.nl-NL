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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Hallo knooppunt starten en stoppen knooppunt API's vervangen door Hallo knooppunt overgang API

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Wat Hallo knooppunt stoppen en starten knooppunt API's doen?

Hallo knooppunt API stoppen (beheerd: [StopNodeAsync()][stopnode], PowerShell: [Stop ServiceFabricNode][stopnodeps]) stopt van een Service Fabric-knooppunt.  Een Service Fabric-knooppunt is niet een VM of de machine wordt – Hallo VM of machine wordt nog steeds worden uitgevoerd.  Voor de rest Hallo van Hallo document 'knooppunt' betekent dat deze Service Fabric-knooppunt.  Stoppen van een knooppunt, plaatst het in een *gestopt* status waarbij is geen lid van de cluster Hallo en kan geen host zijn services, dus simuleren een *omlaag* knooppunt.  Dit is handig voor het injecteren van fouten in Hallo system tootest uw toepassing.  Hallo Start knooppunt API (beheerd: [StartNodeAsync()][startnode], PowerShell: [Start ServiceFabricNode][startnodeps]]) keert Hallo knooppunt API stoppen  Dit brengt Hallo knooppunt back tooa normale status.

## <a name="why-are-we-replacing-these"></a>Waarom zijn we deze vervangen?

Zoals eerder beschreven, een *gestopt* Service Fabric-knooppunt is een knooppunt opzettelijk gericht Hallo stoppen knooppunt API gebruiken.  Een *omlaag* knooppunt is een knooppunt dat is niet beschikbaar voor een andere reden (bijvoorbeeld Hallo VM of de machine is uitgeschakeld).  Met de Hallo knooppunt API stoppen, Hallo systeem niet beschikbaar toodifferentiate informatie tussen *gestopt* knooppunten en *omlaag* knooppunten.

Er zijn fouten geretourneerd door deze API's zijn niet als beschrijvende zoals ze zijn.  Bijvoorbeeld stoppen knooppunt API aanroepen Hallo op een al *gestopt* knooppunt retourneert fout Hallo *InvalidAddress*.  Deze ervaring kan worden verbeterd.

Hallo duur van die een knooppunt is gestopt voor is ook 'oneindig' tot Hallo die start knooppunt API wordt aangeroepen.  We hebben dit kan problemen veroorzaken en gevoelig voor fouten kan worden gevonden.  We zag bijvoorbeeld problemen waarbij een gebruiker aangeroepen Hallo knooppunt API stoppen op een knooppunt en vervolgens vergeten bent.  Later, was het niet duidelijk als Hallo knooppunt *omlaag* of *gestopt*.


## <a name="introducing-hello-node-transition-apis"></a>Inleiding tot Hallo knooppunt overgang API 's

We hebt deze problemen boven in een nieuwe reeks API's opgelost.  het nieuwe knooppunt overgang API Hallo (beheerd: [StartNodeTransitionAsync()][snt]) mogelijk gebruikte tootransition een tooa Service Fabric-knooppunt *gestopt* status- of tootransition deze van een *gestopt* status tooa normale werking.  Houd er rekening mee dat Hallo 'Start' in de naam van de Hallo Hallo API verwijst niet toostarting een knooppunt.  Het toobeginning een asynchrone bewerking Hallo system uitvoering tootransition Hallo knooppunt tooeither verwijst *gestopt* of de status gestart.

**Gebruik**

Hallo knooppunt overgang API heeft een uitzondering opgetreden bij het aanroepen niet genereren, vervolgens Hallo system Hallo asynchrone bewerking heeft geaccepteerd als deze wordt uitgevoerd.  Een geslaagde aanroepen betekent niet dat Hallo bewerking nog is voltooid.  tooget informatie over de huidige status van Hallo bewerking aanroep Hallo knooppunt overgang voortgang API Hallo (beheerd: [GetNodeTransitionProgressAsync()][gntp]) met Hallo-guid die wordt gebruikt bij het aanroepen van knooppunt De API van de overgang voor deze bewerking.  Hallo knooppunt overgang voortgang API retourneert een object NodeTransitionProgress.  Eigenschap van de status van dit object geeft de huidige status Hallo van Hallo-bewerking.  Hallo-bewerking wordt uitgevoerd als Hallo status 'actief'.  Als deze is voltooid, wordt de Hallo opnieuw zonder fouten voltooid.  Als deze fout is opgetreden, is er een probleem bij het Hallo-bewerking uitvoeren.  Hallo resultaat eigenschap uitzondering eigenschap wordt aangegeven welke Hallo uitgeven is.  Zie https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate voor meer informatie over de eigenschap State Hallo en Hallo 'Voorbeeldgebruik' hieronder voor codevoorbeelden.


**Verschillen tussen een gestopte knooppunt en een knooppunt omlaag** als een knooppunt *gestopt* knooppunt overgang API, Hallo-uitvoer van een query voor knooppunt met behulp van Hallo (beheerd: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) wordt aangegeven dat dit knooppunt heeft een *IsStopped* de eigenschapwaarde true.  Houd er rekening mee deze verschilt van de waarde van Hallo Hallo *NodeStatus* eigenschap dicteert *omlaag*.  Als hello *NodeStatus* eigenschap een waarde heeft van *omlaag*, maar *IsStopped* is ingesteld op false, en vervolgens het Hallo-knooppunt is niet gestopt met Hallo knooppunt overgang API en is  *Omlaag* vanwege een andere reden.  Als hello *IsStopped* eigenschap waar is en Hallo *NodeStatus* eigenschap is *omlaag*, en vervolgens deze wordt stilgelegd Hallo knooppunt overgang API gebruiken.

Starten van een *gestopt* Hallo knooppunt overgang API-knooppunt retourneert het toofunction als normale lid van de cluster Hallo opnieuw.  Hallo uitvoer van Hallo knooppunt query API ziet *IsStopped* als onwaar, en *NodeStatus* als iets dat niet is niet beschikbaar (bijvoorbeeld omhoog).


**Beperkte duur** wanneer u Hallo knooppunt overgang API toostop een knooppunt, een Hallo vereiste parameters, *stopNodeDurationInSeconds*, vertegenwoordigt de hoeveelheid tijd in seconden tookeep Hallo knooppunt Hallo  *gestopt*.  Deze waarde moet liggen binnen het toegestane bereik, waarvoor minimaal 600 en een maximum van 14400 Hallo.  Nadat deze tijd is verstreken, Hallo-knooppunt wordt automatisch opnieuw opgestart zelf in de status van.  Raadpleeg tooSample 1 hieronder voor een voorbeeld van gebruik.

> [!WARNING]
> Vermijd de combinatie van knooppunt overgang API's en Hallo knooppunt stoppen en starten knooppunt API's.  Hallo-aanbeveling is Hallo knooppunt overgang API alleen te gebruiken.  > Als een knooppunt is al gestopt met Hallo knooppunt API stoppen, deze moet worden gestart met Hallo knooppunt API Start eerst voordat u Hallo > knooppunt overgang API's.

> [!WARNING]
> Meerdere knooppunt overgang API aanroepen kunnen niet worden doorgevoerd op hetzelfde knooppunt parallel Hallo.  In een dergelijke situatie Hallo knooppunt overgang API wordt > genereert een FabricException met een eigenschapswaarde ErrorCode van NodeTransitionInProgress.  Zodra de overgang van een knooppunt op een specifiek knooppunt heeft > is gestart, moet u wachten totdat het Hallo-bewerking heeft een definitieve status (voltooid, Faulted of ForceCancelled) bereikt voordat u begint een > nieuwe overgang op Hallo hetzelfde knooppunt.  Parallelle knooppunt overgang aanroepen op verschillende knooppunten zijn toegestaan.


#### <a name="sample-usage"></a>Voorbeeld van gebruik


**Voorbeeld 1** -Hallo volgende voorbeeld wordt Hallo knooppunt overgang API toostop een knooppunt.

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

**Voorbeeld 2** - hello voorbeeld wordt gestart na een *gestopt* knooppunt.  Sommige Help-methoden van het eerste voorbeeld hello wordt gebruikt.

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

**Voorbeeld 3** - hello volgende voorbeeld toont onjuiste informatie over het gebruik.  Dit gebruik is onjuist omdat Hallo *stopDurationInSeconds* is groter dan het toegestane bereik Hallo biedt.  Aangezien StartNodeTransitionAsync() met een onherstelbare fout mislukt, Hallo-bewerking is niet geaccepteerd en Hallo voortgang API moet niet worden aangeroepen.  Dit voorbeeld wordt een aantal methoden van het eerste voorbeeld Hallo gebruikt.

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

**Voorbeeld 4** - hello volgende voorbeeld toont Hallo foutgegevens die worden geretourneerd van Hallo knooppunt overgang voortgang API wanneer Hallo-bewerking gestart door Hallo knooppunt overgang API is geaccepteerd, maar later tijdens het uitvoeren is mislukt.  In geval van hello mislukt dit omdat Hallo knooppunt overgang API probeert toostart een knooppunt dat niet bestaat.  Dit voorbeeld wordt een aantal methoden van het eerste voorbeeld Hallo gebruikt.

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
