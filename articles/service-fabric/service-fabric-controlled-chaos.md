---
title: aaaInduce Chaos in Service Fabric-clusters | Microsoft Docs
description: Met behulp van fouttolerantie injectie en Cluster Analysis Service-API's toomanage Chaos in Hallo-cluster.
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
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="7db67-103">Veroorzaken gecontroleerde Chaos in Service Fabric-clusters</span><span class="sxs-lookup"><span data-stu-id="7db67-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="7db67-104">Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden.</span><span class="sxs-lookup"><span data-stu-id="7db67-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="7db67-105">Azure Service Fabric kunnen ontwikkelaars toowrite betrouwbare gedistribueerde services op een onbetrouwbaar-infrastructuur.</span><span class="sxs-lookup"><span data-stu-id="7db67-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="7db67-106">toowrite robuuste gedistribueerde services op een onbetrouwbaar-infrastructuur, ontwikkelaars moeten toobe kunnen tootest Hallo stabiliteit van hun services terwijl Hallo onderliggende onbetrouwbaar infrastructuur wordt verzonden via ingewikkeld statusovergangen vanwege toofaults.</span><span class="sxs-lookup"><span data-stu-id="7db67-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="7db67-107">Hallo [fout injectie en analyse van de clusterservice](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (ook wel bekend als hello veroorzaakt Analysis Service) biedt ontwikkelaars de mogelijkheid Hallo tooinduce bedrijfsstoringen tootest hun services.</span><span class="sxs-lookup"><span data-stu-id="7db67-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="7db67-108">Deze gericht fouten, zoals gesimuleerde [opnieuw starten van een partitie](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), kunt u de meest voorkomende statusovergangen Hallo uitoefenen.</span><span class="sxs-lookup"><span data-stu-id="7db67-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="7db67-109">Echter fouten gerichte gesimuleerde fouten per definitie zijn gericht en dus mist mogelijk die weergeven van alleen in moeilijk te voorspellen, lang en gecompliceerd reeks statusovergangen.</span><span class="sxs-lookup"><span data-stu-id="7db67-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="7db67-110">Voor een zuivere testen, kunt u Chaos.</span><span class="sxs-lookup"><span data-stu-id="7db67-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="7db67-111">Periodieke, interleaved fouten (correcte en geforceerde afsluiting) in de cluster Hallo simuleert chaos gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="7db67-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="7db67-112">Nadat u Chaos met Hallo frequentie en het soort fouten Hallo hebt geconfigureerd, kunt u Chaos starten via de C# of Powershell API toostart genereren van fouten in de cluster hello en in uw services.</span><span class="sxs-lookup"><span data-stu-id="7db67-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="7db67-113">U kunt Chaos toorun configureren voor een opgegeven periode (bijvoorbeeld: voor één uur), waarna Chaos automatisch wordt gestopt, of u kunt StopChaos API (C# of Powershell) toostop aanroepen op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="7db67-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="7db67-114">In de huidige vorm induceert Chaos alleen veilige fouten, wat betekent dat dat Hallo ontbreken van een externe fouten een quorumverlies of verlies van gegevens nooit plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="7db67-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="7db67-115">Terwijl Chaos wordt uitgevoerd, is het resultaat van andere gebeurtenissen die status Hallo Hallo uitgevoerd op moment Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="7db67-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="7db67-116">Een ExecutingFaultsEvent bevat bijvoorbeeld alle Hallo gebreken Chaos besloten tooexecute in die iteratie.</span><span class="sxs-lookup"><span data-stu-id="7db67-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="7db67-117">Een ValidationFailedEvent bevat Hallo details van een mislukte validatie (health of stabiliteit problemen) die tijdens de validatie van de cluster Hallo Hallo is gevonden.</span><span class="sxs-lookup"><span data-stu-id="7db67-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="7db67-118">U kunt aanroepen Hallo GetChaosReport API (C# of Powershell) tooget Hallo rapport van Chaos wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7db67-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="7db67-119">Deze gebeurtenissen ophalen permanent in een [betrouwbare woordenlijst](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), heeft een beleid moet worden afgekapt is bepaald door twee configuraties: **MaxStoredChaosEventCount** (de standaardwaarde is 25000) en  **StoredActionCleanupIntervalInSeconds** (de standaardwaarde is 3600).</span><span class="sxs-lookup"><span data-stu-id="7db67-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="7db67-120">Elke *StoredActionCleanupIntervalInSeconds* Chaos controles en alle maar Hallo meest recente *MaxStoredChaosEventCount* gebeurtenissen van betrouwbare woordenboek Hallo worden opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="7db67-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="7db67-121">Fouten worden bewerkstelligd in Chaos</span><span class="sxs-lookup"><span data-stu-id="7db67-121">Faults induced in Chaos</span></span>
<span data-ttu-id="7db67-122">Chaos fouten over de hele Service Fabric-cluster Hallo genereert en comprimeert fouten die zijn zichtbaar in maanden of jaren in een paar uur.</span><span class="sxs-lookup"><span data-stu-id="7db67-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="7db67-123">Hallo combinatie van interleaved fouten met Hallo hoge fouttolerantie tarief vindt hoek aanvragen die mogelijk anders worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7db67-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="7db67-124">In deze oefening dank leidt tooa aanzienlijke verbetering in Hallo code servicekwaliteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="7db67-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="7db67-125">Chaos induceert fouten van Hallo volgende categorieën:</span><span class="sxs-lookup"><span data-stu-id="7db67-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="7db67-126">Een knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="7db67-126">Restart a node</span></span>
* <span data-ttu-id="7db67-127">Een geïmplementeerde codepakket niet opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="7db67-127">Restart a deployed code package</span></span>
* <span data-ttu-id="7db67-128">Een replica verwijderen</span><span class="sxs-lookup"><span data-stu-id="7db67-128">Remove a replica</span></span>
* <span data-ttu-id="7db67-129">Een replica starten</span><span class="sxs-lookup"><span data-stu-id="7db67-129">Restart a replica</span></span>
* <span data-ttu-id="7db67-130">Verplaatsen van een primaire replica (configureren)</span><span class="sxs-lookup"><span data-stu-id="7db67-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="7db67-131">Verplaatsen van een secundaire replica (configureren)</span><span class="sxs-lookup"><span data-stu-id="7db67-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="7db67-132">Chaos in meerdere pogingen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7db67-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="7db67-133">Elke herhaling bestaat uit de fouten en clustervalidatie voor Hallo opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="7db67-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="7db67-134">U kunt Hallo tijd voor Hallo cluster toostabilize en voor validatie toosucceed configureren.</span><span class="sxs-lookup"><span data-stu-id="7db67-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="7db67-135">Als een fout in validatie wordt gevonden, wordt Chaos genereert en een ValidationFailedEvent met de UTC-timestamp Hallo en foutdetails Hallo zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="7db67-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="7db67-136">Neem bijvoorbeeld een exemplaar dank die toorun is ingesteld voor een uur met een maximum van drie gelijktijdige fouten.</span><span class="sxs-lookup"><span data-stu-id="7db67-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="7db67-137">Chaos induceert drie fouten en controleert vervolgens Hallo cluster health.</span><span class="sxs-lookup"><span data-stu-id="7db67-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="7db67-138">Doorlopen Hallo vorige stap totdat deze expliciet gestopt via Hallo StopChaosAsync API of één uur wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="7db67-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="7db67-139">Als het cluster Hallo slecht in elke iteratie (dat wil zeggen, het heeft geen regulering binnen Hallo doorgegeven in MaxClusterStabilizationTimeout), Chaos genereert een ValidationFailedEvent.</span><span class="sxs-lookup"><span data-stu-id="7db67-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="7db67-140">Deze gebeurtenis geeft aan dat er iets een opgetreden fout is en verder onderzoek moet mogelijk.</span><span class="sxs-lookup"><span data-stu-id="7db67-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="7db67-141">tooget die Chaos wordt veroorzaakt bedrijfsstoringen, kunt u GetChaosReport API (powershell of C#).</span><span class="sxs-lookup"><span data-stu-id="7db67-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="7db67-142">Hallo API opgehaald Hallo volgende segment van Hallo Chaos rapport op basis van Hallo doorgegeven vervolgtoken of Hallo doorgegeven-tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="7db67-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="7db67-143">Kunt u opgeven ContinuationToken tooget Hallo volgende segment van Hallo Chaos rapport Hallo of kunt u Hallo-tijdsbereik via StartTimeUtc en EndTimeUtc opgeven, maar u niet zowel Hallo ContinuationToken Hallo tijdsbereik opgeven in Hallo dezelfde aanroep.</span><span class="sxs-lookup"><span data-stu-id="7db67-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="7db67-144">Wanneer er meer dan 100 Chaos gebeurtenissen, wordt Hallo Chaos rapport geretourneerd in segmenten waarbij een segment niet meer dan 100 Chaos gebeurtenissen bevat.</span><span class="sxs-lookup"><span data-stu-id="7db67-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="7db67-145">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="7db67-145">Important configuration options</span></span>
* <span data-ttu-id="7db67-146">**TimeToRun**: totale tijd die Chaos wordt uitgevoerd voordat het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7db67-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="7db67-147">U kunt Chaos stoppen voordat deze is uitgevoerd gedurende TimeToRun Hallo via Hallo StopChaos API.</span><span class="sxs-lookup"><span data-stu-id="7db67-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="7db67-148">**MaxClusterStabilizationTimeout**: Hallo maximale hoeveelheid tijd toowait voor Hallo cluster toobecome voordat het opstellen van een ValidationFailedEvent in orde.</span><span class="sxs-lookup"><span data-stu-id="7db67-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="7db67-149">Deze wachttijd is de tooreduce Hallo belasting op Hallo cluster terwijl deze wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="7db67-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="7db67-150">Hallo-controles uitgevoerd worden:</span><span class="sxs-lookup"><span data-stu-id="7db67-150">hello checks performed are:</span></span>
  * <span data-ttu-id="7db67-151">Als de status van de cluster Hallo is OK</span><span class="sxs-lookup"><span data-stu-id="7db67-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="7db67-152">Als het Hallo-service de status is OK</span><span class="sxs-lookup"><span data-stu-id="7db67-152">If hello service health is OK</span></span>
  * <span data-ttu-id="7db67-153">Als Hallo doelreplica grootte ingesteld wordt voor Hallo service partitie bereikt</span><span class="sxs-lookup"><span data-stu-id="7db67-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="7db67-154">Dat er geen InBuild-replica's bestaan</span><span class="sxs-lookup"><span data-stu-id="7db67-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="7db67-155">**MaxConcurrentFaults**: Hallo maximum aantal gelijktijdige fouten die in elke iteratie veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="7db67-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="7db67-156">Hallo hoger Hallo getal, Hallo agressievere Chaos is en Hallo failovers en Hallo status overgang combinaties van die cluster Hallo doorloopt NTDS zijn ook complexere.</span><span class="sxs-lookup"><span data-stu-id="7db67-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="7db67-157">Ongeacht hoe hoge waarde *MaxConcurrentFaults* heeft, Chaos garandeert - Hallo ontbreken van een externe fouten - er is geen quorumverlies of verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="7db67-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="7db67-158">**EnableMoveReplicaFaults**: Hiermee schakelt u Hallo fouten waardoor Hallo primaire of secundaire replica's toomove of uit.</span><span class="sxs-lookup"><span data-stu-id="7db67-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="7db67-159">Deze fouten worden standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="7db67-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="7db67-160">**WaitTimeBetweenIterations**: Hallo hoeveelheid tijd toowait tussen iteraties.</span><span class="sxs-lookup"><span data-stu-id="7db67-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="7db67-161">Dat wil zeggen, Hallo tijdsduur die chaos onderbroken na het uitvoeren van een ronde van fouten en de bijbehorende validatie Hallo Hallo gezondheidstoestand van Hallo cluster hebben voltooid.</span><span class="sxs-lookup"><span data-stu-id="7db67-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="7db67-162">hogere Hallo waarde Hallo Hallo lager is Hallo gemiddelde veroorzaakt injectie snelheid.</span><span class="sxs-lookup"><span data-stu-id="7db67-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="7db67-163">**WaitTimeBetweenFaults**: Hallo hoeveelheid tijd toowait tussen twee opeenvolgende fouten in een enkel iteratie.</span><span class="sxs-lookup"><span data-stu-id="7db67-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="7db67-164">Hallo hogere Hallo-waarde, lagere Hallo gelijktijdigheid van hello (of Hallo overlapping tussen) fouten.</span><span class="sxs-lookup"><span data-stu-id="7db67-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="7db67-165">**ClusterHealthPolicy**: Cluster statusbeleid is gebruikte toovalidate Hallo status van de cluster Hallo Between Chaos iteraties.</span><span class="sxs-lookup"><span data-stu-id="7db67-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="7db67-166">Als Hallo cluster health onjuist is of als een onverwachte uitzondering tijdens het uitvoeren van de fout gebeurt, Chaos gedurende 30 minuten Hallo volgende-statuscontrole - tooprovide Hallo cluster met een aantal toorecuperate tijd wacht.</span><span class="sxs-lookup"><span data-stu-id="7db67-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="7db67-167">**Context**: een verzameling van (string, string) typt u sleutel-waardeparen.</span><span class="sxs-lookup"><span data-stu-id="7db67-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="7db67-168">Hallo-kaart kan worden gebruikt toorecord informatie over Hallo Chaos uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7db67-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="7db67-169">Er mag niet meer dan 100 dergelijke paren en elke tekenreeks (sleutel of waarde) mag hoogstens 4095 tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="7db67-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="7db67-170">Deze kaart is ingesteld door Hallo starter van Hallo Chaos uitvoeren toooptionally store Hallo context over Hallo specifieke uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="7db67-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="7db67-171">Hoe toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="7db67-171">How toorun Chaos</span></span>

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
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
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
                // If a StoppedEvent is found, exit hello loop.
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
