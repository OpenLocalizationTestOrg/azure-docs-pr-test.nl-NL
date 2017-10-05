---
title: Chaos veroorzaken in Service Fabric-clusters | Microsoft Docs
description: Fout injectie en Cluster Analysis Service-API's gebruiken voor het beheren van Chaos in het cluster.
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 3b3b93bc9ec5ecdcfc289e5b62e84de6aa4172ed
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="b51f1-103">Veroorzaken gecontroleerde Chaos in Service Fabric-clusters</span><span class="sxs-lookup"><span data-stu-id="b51f1-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="b51f1-104">Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden.</span><span class="sxs-lookup"><span data-stu-id="b51f1-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="b51f1-105">Azure Service Fabric kunnen ontwikkelaars schrijven betrouwbare gedistribueerde services op een onbetrouwbaar-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="b51f1-105">Azure Service Fabric enables developers to write reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="b51f1-106">Ontwikkelaars moeten kunnen testen van de stabiliteit van hun services terwijl de onderliggende infrastructuur onbetrouwbaar wordt verzonden via ingewikkeld statusovergangen als gevolg van fouten voor het schrijven van robuuste gedistribueerde services op een onbetrouwbaar-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="b51f1-106">To write robust distributed services on top of an unreliable infrastructure, developers need to be able to test the stability of their services while the underlying unreliable infrastructure is going through complicated state transitions due to faults.</span></span>

<span data-ttu-id="b51f1-107">De [fout injectie en analyse van de clusterservice](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (ook wel bekend als de fout Analysis Service) biedt ontwikkelaars de mogelijkheid om te veroorzaken fouten voor het testen van hun services.</span><span class="sxs-lookup"><span data-stu-id="b51f1-107">The [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as the Fault Analysis Service) gives developers the ability to induce faults to test their services.</span></span> <span data-ttu-id="b51f1-108">Deze gericht fouten, zoals gesimuleerde [opnieuw starten van een partitie](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), kunt u de meest voorkomende statusovergangen uitoefenen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise the most common state transitions.</span></span> <span data-ttu-id="b51f1-109">Echter fouten gerichte gesimuleerde fouten per definitie zijn gericht en dus mist mogelijk die weergeven van alleen in moeilijk te voorspellen, lang en gecompliceerd reeks statusovergangen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="b51f1-110">Voor een zuivere testen, kunt u Chaos.</span><span class="sxs-lookup"><span data-stu-id="b51f1-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="b51f1-111">Chaos simuleert periodieke, interleaved fouten (correcte en geforceerde afsluiting) in het cluster gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="b51f1-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="b51f1-112">Wanneer u Chaos met de frequentie en het soort fouten hebt geconfigureerd, kunt u beginnen Chaos via C# of Powershell API om te beginnen met het genereren van fouten in het cluster en in uw services.</span><span class="sxs-lookup"><span data-stu-id="b51f1-112">Once you have configured Chaos with the rate and the kind of faults, you can start Chaos through C# or Powershell API to start generating faults in the cluster and in your services.</span></span> <span data-ttu-id="b51f1-113">U kunt Chaos om uit te voeren voor een opgegeven periode (bijvoorbeeld: voor één uur) automatisch na waarbij stopt Chaos configureren of u StopChaos API (C# of Powershell) om deze te stoppen op elk gewenst moment kunt aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-113">You can configure Chaos to run for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) to stop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="b51f1-114">In de huidige vorm induceert Chaos alleen veilige fouten die impliceert dat bij gebrek aan externe fouten een quorumverlies of verlies van gegevens nooit plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="b51f1-114">In its current form, Chaos induces only safe faults, which implies that in the absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="b51f1-115">Terwijl Chaos wordt uitgevoerd, is het resultaat van andere gebeurtenissen die de status van de uitvoeren op het moment dat vastleggen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-115">While Chaos is running, it produces different events that capture the state of the run at the moment.</span></span> <span data-ttu-id="b51f1-116">Een ExecutingFaultsEvent bevat bijvoorbeeld de fouten die Chaos heeft besloten uit te voeren in die iteratie.</span><span class="sxs-lookup"><span data-stu-id="b51f1-116">For example, an ExecutingFaultsEvent contains all the faults that Chaos has decided to execute in that iteration.</span></span> <span data-ttu-id="b51f1-117">Een ValidationFailedEvent bevat de details van een mislukte validatie (health of stabiliteit problemen) die tijdens de validatie van het cluster is gevonden.</span><span class="sxs-lookup"><span data-stu-id="b51f1-117">A ValidationFailedEvent contains the details of a validation failure (health or stability issues) that was found during the validation of the cluster.</span></span> <span data-ttu-id="b51f1-118">U kunt de API GetChaosReport (C# of Powershell) als u het rapport over de uitgevoerde Chaos aanroepen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-118">You can invoke the GetChaosReport API (C# or Powershell) to get the report of Chaos runs.</span></span> <span data-ttu-id="b51f1-119">Deze gebeurtenissen ophalen permanent in een [betrouwbare woordenlijst](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), heeft een beleid moet worden afgekapt is bepaald door twee configuraties: **MaxStoredChaosEventCount** (de standaardwaarde is 25000) en  **StoredActionCleanupIntervalInSeconds** (de standaardwaarde is 3600).</span><span class="sxs-lookup"><span data-stu-id="b51f1-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="b51f1-120">Elke *StoredActionCleanupIntervalInSeconds* Chaos controles en alle maar het meest recente *MaxStoredChaosEventCount* gebeurtenissen, permanent worden verwijderd van het betrouwbare woordenboek.</span><span class="sxs-lookup"><span data-stu-id="b51f1-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but the most recent *MaxStoredChaosEventCount* events, are purged from the reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="b51f1-121">Fouten worden bewerkstelligd in Chaos</span><span class="sxs-lookup"><span data-stu-id="b51f1-121">Faults induced in Chaos</span></span>
<span data-ttu-id="b51f1-122">Chaos genereert fouten over de hele Service Fabric-cluster en comprimeert fouten die zijn zichtbaar in maanden of jaren in een paar uur.</span><span class="sxs-lookup"><span data-stu-id="b51f1-122">Chaos generates faults across the entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="b51f1-123">De combinatie van interleaved fouten met de snelheid van hoge fouttolerantie vindt hoek aanvragen die mogelijk anders worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-123">The combination of interleaved faults with the high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="b51f1-124">In deze oefening dank leidt tot een aanzienlijke verbetering van de kwaliteit van de code van de service.</span><span class="sxs-lookup"><span data-stu-id="b51f1-124">This exercise of Chaos leads to a significant improvement in the code quality of the service.</span></span>

<span data-ttu-id="b51f1-125">Chaos induceert fouten uit de volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="b51f1-125">Chaos induces faults from the following categories:</span></span>

* <span data-ttu-id="b51f1-126">Een knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="b51f1-126">Restart a node</span></span>
* <span data-ttu-id="b51f1-127">Een geïmplementeerde codepakket niet opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="b51f1-127">Restart a deployed code package</span></span>
* <span data-ttu-id="b51f1-128">Een replica verwijderen</span><span class="sxs-lookup"><span data-stu-id="b51f1-128">Remove a replica</span></span>
* <span data-ttu-id="b51f1-129">Een replica starten</span><span class="sxs-lookup"><span data-stu-id="b51f1-129">Restart a replica</span></span>
* <span data-ttu-id="b51f1-130">Verplaatsen van een primaire replica (configureren)</span><span class="sxs-lookup"><span data-stu-id="b51f1-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="b51f1-131">Verplaatsen van een secundaire replica (configureren)</span><span class="sxs-lookup"><span data-stu-id="b51f1-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="b51f1-132">Chaos in meerdere pogingen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b51f1-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="b51f1-133">Elke herhaling bestaat uit de fouten en clustervalidatie voor de opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="b51f1-133">Each iteration consists of faults and cluster validation for the specified period.</span></span> <span data-ttu-id="b51f1-134">De tijd voor het cluster stabiel en voor de validatie mislukt, kunt u configureren.</span><span class="sxs-lookup"><span data-stu-id="b51f1-134">You can configure the time spent for the cluster to stabilize and for validation to succeed.</span></span> <span data-ttu-id="b51f1-135">Als een fout in validatie wordt gevonden, wordt Chaos genereert en een ValidationFailedEvent met de UTC-timestamp en de foutdetails zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with the UTC timestamp and the failure details.</span></span> <span data-ttu-id="b51f1-136">Neem bijvoorbeeld een exemplaar dank dat is ingesteld op een uur worden uitgevoerd met een maximum van drie gelijktijdige fouten.</span><span class="sxs-lookup"><span data-stu-id="b51f1-136">For example, consider an instance of Chaos that is set to run for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="b51f1-137">Chaos induceert drie fouten en vervolgens valideert de status van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b51f1-137">Chaos induces three faults, and then validates the cluster health.</span></span> <span data-ttu-id="b51f1-138">Doorlopen de vorige stap totdat deze expliciet gestopt via de API StopChaosAsync of één uur wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="b51f1-138">It iterates through the previous step until it is explicitly stopped through the StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="b51f1-139">Als het cluster in elke iteratie slecht (dat wil zeggen, het heeft geen regulering binnen de MaxClusterStabilizationTimeout doorgegeven), Chaos genereert een ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="b51f1-139">If the cluster becomes unhealthy in any iteration (that is, it does not stabilize within the passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="b51f1-140">Deze gebeurtenis geeft aan dat er iets een opgetreden fout is en verder onderzoek moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="b51f1-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="b51f1-141">Als u welke fouten Chaos wordt veroorzaakt, kunt u GetChaosReport API (powershell of C#).</span><span class="sxs-lookup"><span data-stu-id="b51f1-141">To get which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="b51f1-142">De API Hiermee haalt u het volgende segment van het Chaos rapport op basis van de doorgegeven vervolgtoken of doorgegeven in een tijd-bereik.</span><span class="sxs-lookup"><span data-stu-id="b51f1-142">The API gets the next segment of the Chaos report based on the passed-in continuation token or the passed-in time-range.</span></span> <span data-ttu-id="b51f1-143">Kunt u de ContinuationToken als u het volgende segment van het rapport Chaos opgeven of u kunt het tijdsbereik via StartTimeUtc en EndTimeUtc opgeven, maar u niet zowel de ContinuationToken als het tijdsbereik opgeven in dezelfde aanroep.</span><span class="sxs-lookup"><span data-stu-id="b51f1-143">You can either specify the ContinuationToken to get the next segment of the Chaos report or you can specify the time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both the ContinuationToken and the time-range in the same call.</span></span> <span data-ttu-id="b51f1-144">Wanneer er meer dan 100 Chaos gebeurtenissen, wordt het rapport Chaos geretourneerd in segmenten waarbij een segment niet meer dan 100 Chaos gebeurtenissen bevat.</span><span class="sxs-lookup"><span data-stu-id="b51f1-144">When there are more than 100 Chaos events, the Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="b51f1-145">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="b51f1-145">Important configuration options</span></span>
* <span data-ttu-id="b51f1-146">**TimeToRun**: totale tijd die Chaos wordt uitgevoerd voordat het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b51f1-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="b51f1-147">U kunt Chaos stoppen voordat deze is uitgevoerd voor de periode TimeToRun via de API StopChaos.</span><span class="sxs-lookup"><span data-stu-id="b51f1-147">You can stop Chaos before it has run for the TimeToRun period through the StopChaos API.</span></span>

* <span data-ttu-id="b51f1-148">**MaxClusterStabilizationTimeout**: de maximale hoeveelheid wachttijd voor het cluster wordt omgezet in orde voordat het opstellen van een ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="b51f1-148">**MaxClusterStabilizationTimeout**: The maximum amount of time to wait for the cluster to become healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="b51f1-149">Deze wachttijd is het verminderen van de belasting op het cluster, terwijl deze wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="b51f1-149">This wait is to reduce the load on the cluster while it is recovering.</span></span> <span data-ttu-id="b51f1-150">De controles uitgevoerd worden:</span><span class="sxs-lookup"><span data-stu-id="b51f1-150">The checks performed are:</span></span>
  * <span data-ttu-id="b51f1-151">Als de status van het cluster OK is</span><span class="sxs-lookup"><span data-stu-id="b51f1-151">If the cluster health is OK</span></span>
  * <span data-ttu-id="b51f1-152">Als de servicestatus van de OK is</span><span class="sxs-lookup"><span data-stu-id="b51f1-152">If the service health is OK</span></span>
  * <span data-ttu-id="b51f1-153">Als de doelreplica grootte ingesteld wordt voor de partitie van de service bereikt</span><span class="sxs-lookup"><span data-stu-id="b51f1-153">If the target replica set size is achieved for the service partition</span></span>
  * <span data-ttu-id="b51f1-154">Dat er geen InBuild-replica's bestaan</span><span class="sxs-lookup"><span data-stu-id="b51f1-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="b51f1-155">**MaxConcurrentFaults**: het maximum aantal gelijktijdige fouten die in elke iteratie veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="b51f1-155">**MaxConcurrentFaults**: The maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="b51f1-156">De hoger het getal, hoe meer agressieve Chaos is en de failovers en de status overgang combinaties die het cluster doorloopt zijn ook complexere.</span><span class="sxs-lookup"><span data-stu-id="b51f1-156">The higher the number, the more aggressive Chaos is and the failovers and the state transition combinations that the cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="b51f1-157">Ongeacht hoe hoge waarde *MaxConcurrentFaults* heeft, Chaos garandeert - bij gebrek aan externe fouten - er is geen quorumverlies of verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="b51f1-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in the absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="b51f1-158">**EnableMoveReplicaFaults**: Hiermee schakelt u de fouten die ertoe leiden de primaire of secundaire replica's dat te verplaatsen of uit.</span><span class="sxs-lookup"><span data-stu-id="b51f1-158">**EnableMoveReplicaFaults**: Enables or disables the faults that cause the primary or secondary replicas to move.</span></span> <span data-ttu-id="b51f1-159">Deze fouten worden standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="b51f1-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="b51f1-160">**WaitTimeBetweenIterations**: de hoeveelheid tijd moet worden gewacht tussen pogingen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-160">**WaitTimeBetweenIterations**: The amount of time to wait between iterations.</span></span> <span data-ttu-id="b51f1-161">Dat wil zeggen, wordt de hoeveelheid tijd Chaos onderbroken na het uitvoeren van een ronde van fouten en de bijbehorende validatie van de status van het cluster hebben voltooid.</span><span class="sxs-lookup"><span data-stu-id="b51f1-161">That is, the amount of time Chaos will pause after having executed a round of faults and having finished the corresponding validation of the health of the cluster.</span></span> <span data-ttu-id="b51f1-162">Hoe hoger de waarde des te lager is de frequentie van de gemiddelde paginafouten injectie.</span><span class="sxs-lookup"><span data-stu-id="b51f1-162">The higher the value, the lower is the average fault injection rate.</span></span>
* <span data-ttu-id="b51f1-163">**WaitTimeBetweenFaults**: de hoeveelheid tijd moet worden gewacht tussen twee opeenvolgende fouten in een enkel iteratie.</span><span class="sxs-lookup"><span data-stu-id="b51f1-163">**WaitTimeBetweenFaults**: The amount of time to wait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="b51f1-164">Hoe hoger de waarde, hoe lager de gelijktijdigheid van (of de overlapping tussen) bedrijfsstoringen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-164">The higher the value, the lower the concurrency of (or the overlap between) faults.</span></span>
* <span data-ttu-id="b51f1-165">**ClusterHealthPolicy**: Cluster statusbeleid wordt gebruikt voor het valideren van de status van het cluster Between Chaos iteraties.</span><span class="sxs-lookup"><span data-stu-id="b51f1-165">**ClusterHealthPolicy**: Cluster health policy is used to validate the health of the cluster in between Chaos iterations.</span></span> <span data-ttu-id="b51f1-166">Als de status van het cluster onjuist is of als een onverwachte uitzondering tijdens het uitvoeren van de fout gebeurt, wacht u totdat 30 minuten voordat de volgende-statuscontrole - om te voorzien van het cluster enige tijd recuperate Chaos.</span><span class="sxs-lookup"><span data-stu-id="b51f1-166">If the cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before the next health-check - to provide the cluster with some time to recuperate.</span></span>
* <span data-ttu-id="b51f1-167">**Context**: een verzameling van (string, string) typt u sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="b51f1-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="b51f1-168">De kaart kan worden gebruikt voor het vastleggen van informatie over het Chaos-run.</span><span class="sxs-lookup"><span data-stu-id="b51f1-168">The map can be used to record information about the Chaos run.</span></span> <span data-ttu-id="b51f1-169">Er mag niet meer dan 100 dergelijke paren en elke tekenreeks (sleutel of waarde) mag hoogstens 4095 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="b51f1-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="b51f1-170">Deze kaart is ingesteld door de starter de dank uitvoeren voor het opslaan van de context over de specifieke uitvoeren (optioneel).</span><span class="sxs-lookup"><span data-stu-id="b51f1-170">This map is set by the starter of the Chaos run to optionally store the context about the specific run.</span></span>

## <a name="how-to-run-chaos"></a><span data-ttu-id="b51f1-171">Het uitvoeren van Chaos</span><span class="sxs-lookup"><span data-stu-id="b51f1-171">How to run Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in the cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit the loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
