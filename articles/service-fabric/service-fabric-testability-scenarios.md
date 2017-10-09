---
title: aaaCreate chaos en failover testen voor Azure microservices | Microsoft Docs
description: Met behulp van Service Fabric Hallo chaos test- en failover-scenario's tooinduce fouten testen en controleren van Hallo betrouwbaarheid van uw services.
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="9fe3b-103">Testbaarheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="9fe3b-103">Testability scenarios</span></span>
<span data-ttu-id="9fe3b-104">Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="9fe3b-105">Azure Service Fabric biedt ontwikkelaars Hallo mogelijkheid toowrite services toorun boven op onbetrouwbare infrastructuren.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="9fe3b-106">Ontwikkelaars moeten kunnen tooinduce toobe dergelijke onbetrouwbaar infrastructuur tootest Hallo stabiliteit van hun services in de volgorde toowrite hoogwaardige services.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="9fe3b-107">Hallo-fout Analysis Service biedt ontwikkelaars Hallo mogelijkheid tooinduce veroorzaakt acties tootest services in Hallo aanwezigheid van fouten.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="9fe3b-108">Echter krijgt gerichte gesimuleerde fouten u alleen tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="9fe3b-109">tootake hello verder testen kunt u Hallo Testscenario's in Service Fabric: een test chaos en een failover uit.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="9fe3b-110">Deze scenario's simuleren continue interleaved fouten correcte en geforceerde afsluiting in de cluster Hallo gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="9fe3b-111">Wanneer een test met Hallo frequentie en het soort fouten is geconfigureerd, kan het kan worden gestart via C# API's of PowerShell, toogenerate fouten in de cluster Hallo en uw service.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="9fe3b-112">ChaosTestScenario wordt vervangen door een Chaos toleranter, op basis van een service.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="9fe3b-113">Raadpleeg toohello nieuw artikel [Chaos beheerd](service-fabric-controlled-chaos.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="9fe3b-114">Chaos test</span><span class="sxs-lookup"><span data-stu-id="9fe3b-114">Chaos test</span></span>
<span data-ttu-id="9fe3b-115">Hallo chaos scenario genereert fouten over de hele Service Fabric-cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="9fe3b-116">Hallo scenario comprimeren fouten in het algemeen gezien in maanden of jaren tooa enkele uren.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="9fe3b-117">Hallo combinatie van interleaved fouten met Hallo hoge fouttolerantie tarief vindt complexere cases die anders zijn gemist.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="9fe3b-118">Dit leidt tooa aanzienlijke verbetering in Hallo code servicekwaliteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="9fe3b-119">Fouten in Hallo chaos test gesimuleerde</span><span class="sxs-lookup"><span data-stu-id="9fe3b-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="9fe3b-120">Een knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="9fe3b-120">Restart a node</span></span>
* <span data-ttu-id="9fe3b-121">Een geïmplementeerde codepakket niet opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="9fe3b-121">Restart a deployed code package</span></span>
* <span data-ttu-id="9fe3b-122">Een replica verwijderen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-122">Remove a replica</span></span>
* <span data-ttu-id="9fe3b-123">Een replica starten</span><span class="sxs-lookup"><span data-stu-id="9fe3b-123">Restart a replica</span></span>
* <span data-ttu-id="9fe3b-124">Verplaatsen van een primaire replica (optioneel)</span><span class="sxs-lookup"><span data-stu-id="9fe3b-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="9fe3b-125">Verplaatsen van een secundaire replica (optioneel)</span><span class="sxs-lookup"><span data-stu-id="9fe3b-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="9fe3b-126">Hallo chaos test wordt uitgevoerd voor meerdere pogingen storingen en cluster validaties voor Hallo opgegeven tijdsperiode.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="9fe3b-127">Hallo tijd voor Hallo cluster toostabilize en voor validatie toosucceed kan ook worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="9fe3b-128">Hallo scenario mislukt wanneer u een storing in clustervalidatie bereikt.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="9fe3b-129">Neem bijvoorbeeld dat een test toorun gedurende één uur met een maximum van drie gelijktijdige fouten ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="9fe3b-130">Hallo test drie fouten veroorzaken en Hallo cluster health vervolgens te valideren.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="9fe3b-131">Hallo-test wordt de vorige stap Hallo doorlopen totdat het Hallo-cluster wordt slecht of één uur wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="9fe3b-132">Als in elke iteratie slecht functioneert Hallo-cluster, dat wil zeggen het niet binnen een geconfigureerde tijd biedt regulering, Hallo test mislukt met een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="9fe3b-133">Deze uitzondering geeft aan dat er iets een opgetreden fout is en verder onderzoek.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="9fe3b-134">In de huidige vorm induceert Hallo veroorzaakt generatie engine Hallo chaos test alleen veilige fouten.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="9fe3b-135">Dit betekent dat Hallo geen externe fouten, een quorum of verlies van gegevens nooit plaats.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="9fe3b-136">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="9fe3b-136">Important configuration options</span></span>
* <span data-ttu-id="9fe3b-137">**TimeToRun**: totale tijd Hallo test wordt uitgevoerd voordat het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="9fe3b-138">Hallo test kan eerder in plaats van een mislukte validatie worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="9fe3b-139">**MaxClusterStabilizationTimeout**: maximumhoeveelheid tijd toowait voor Hallo cluster toobecome voordat het Hallo-test mislukt in orde.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="9fe3b-140">Hello controles uitgevoerd worden Hiermee wordt aangegeven of de status van de cluster OK is, de servicestatus van de is OK, hello doelgrootte van replicaset bereikt voor Hallo service partitie en geen InBuild-replica's bestaan.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="9fe3b-141">**MaxConcurrentFaults**: maximumaantal gelijktijdige fouten die in elke iteratie.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="9fe3b-142">Hallo hoger Hallo nummer, Hallo agressievere Hallo-test, daarom resulteert in meer complexe failovers en overgang combinaties.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="9fe3b-143">Hallo-test wordt gegarandeerd dat afwezigheid van externe fouten er wordt automatisch een quorum of verlies van gegevens, ongeacht hoe hoog deze configuratie is.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="9fe3b-144">**EnableMoveReplicaFaults**: Hiermee schakelt u Hallo-fouten dat Hallo verplaatsing van Hallo primaire of secundaire replica's veroorzaken of uit.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="9fe3b-145">Deze fouten worden standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="9fe3b-146">**WaitTimeBetweenIterations**: hoeveelheid tijd toowait tussen iteraties, dat wil zeggen na een ronde van fouten en bijbehorende validatie.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="9fe3b-147">Hoe toorun Hallo chaos testen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-147">How toorun hello chaos test</span></span>
<span data-ttu-id="9fe3b-148">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9fe3b-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="9fe3b-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9fe3b-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="9fe3b-150">Failover testen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-150">Failover test</span></span>
<span data-ttu-id="9fe3b-151">Hallo failover Testscenario is een versie van Hallo chaos Testscenario die gericht is op een specifieke service-partitie.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="9fe3b-152">Deze test Hallo effect van failover op een specifieke service partitie terwijl Hallo andere services niet is beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="9fe3b-153">Zodra deze geconfigureerd met Hallo doel partitiegegevens en andere parameters, deze wordt uitgevoerd als een client-side '-hulpprogramma dat gebruikmaakt van C#-API's of PowerShell toogenerate fouten voor de partitie van een service.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="9fe3b-154">een reeks gesimuleerde fouten en servicevalidatie doorlopen Hallo scenario terwijl uw bedrijfslogica wordt uitgevoerd op Hallo side tooprovide een werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="9fe3b-155">Een fout in servicevalidatie geeft een probleem dat verder onderzoek moet.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="9fe3b-156">Fouten die zijn geëmuleerd in Hallo failover testen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="9fe3b-157">Een geïmplementeerd codepakket waar Hallo partitie wordt gehost opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="9fe3b-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="9fe3b-158">Een primaire en secundaire replica of stateless exemplaar verwijderen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="9fe3b-159">Een primaire, secundaire replica opnieuw opstarten (indien een permanente service)</span><span class="sxs-lookup"><span data-stu-id="9fe3b-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="9fe3b-160">Verplaatsen van een primaire replica</span><span class="sxs-lookup"><span data-stu-id="9fe3b-160">Move a primary replica</span></span>
* <span data-ttu-id="9fe3b-161">Verplaatsen van een secundaire replica</span><span class="sxs-lookup"><span data-stu-id="9fe3b-161">Move a secondary replica</span></span>
* <span data-ttu-id="9fe3b-162">Hallo-partitie opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="9fe3b-162">Restart hello partition</span></span>

<span data-ttu-id="9fe3b-163">Hallo failover uit een gekozen fout induceert en voert validatie op Hallo service tooensure de stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="9fe3b-164">Hallo failover testen induceert alleen een fault op een tijd, in tegenstelling tot toopossible meerdere fouten in Hallo chaos test.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="9fe3b-165">Als Hallo service partitie heeft niet binnen de time-out Hallo geconfigureerd regulering na elke fout, mislukt de Hallo test.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="9fe3b-166">Hallo test induceert alleen veilige fouten.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-166">hello test induces only safe faults.</span></span> <span data-ttu-id="9fe3b-167">Dit betekent dat geen externe fouten, een quorum of verlies van gegevens wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="9fe3b-168">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="9fe3b-168">Important configuration options</span></span>
* <span data-ttu-id="9fe3b-169">**PartitionSelector**: Selector-object dat Hiermee geeft u Hallo partitie die gericht toobe nodig.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="9fe3b-170">**TimeToRun**: totale tijd die Hallo-test wordt uitgevoerd voordat u voltooit.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="9fe3b-171">**MaxServiceStabilizationTimeout**: maximumhoeveelheid tijd toowait voor Hallo cluster toobecome voordat het Hallo-test mislukt in orde.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="9fe3b-172">Hallo controles uitgevoerd zijn of de servicestatus OK is, wordt hello doelgrootte van replicaset bereikt voor alle partities en geen InBuild-replica's bestaan.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="9fe3b-173">**WaitTimeBetweenFaults**: hoeveelheid toowait tijd tussen elke cyclus veroorzaakt en validatie.</span><span class="sxs-lookup"><span data-stu-id="9fe3b-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="9fe3b-174">Hoe toorun Hallo failover testen</span><span class="sxs-lookup"><span data-stu-id="9fe3b-174">How toorun hello failover test</span></span>
<span data-ttu-id="9fe3b-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="9fe3b-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="9fe3b-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="9fe3b-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
