---
title: Maken van chaos en failover testen voor Azure microservices | Microsoft Docs
description: Met behulp van de Service Fabric testen chaos test en failover-scenario's te veroorzaken fouten en controleer of de betrouwbaarheid van uw services.
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
ms.openlocfilehash: d06026c750e01ad5825338a78d9af331265f434a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="e0e82-103">Testbaarheid scenario 's</span><span class="sxs-lookup"><span data-stu-id="e0e82-103">Testability scenarios</span></span>
<span data-ttu-id="e0e82-104">Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden.</span><span class="sxs-lookup"><span data-stu-id="e0e82-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="e0e82-105">Azure Service Fabric biedt ontwikkelaars de mogelijkheid om services voor uitvoering op onbetrouwbare infrastructuren.</span><span class="sxs-lookup"><span data-stu-id="e0e82-105">Azure Service Fabric gives developers the ability to write services to run on top of unreliable infrastructures.</span></span> <span data-ttu-id="e0e82-106">Ontwikkelaars moeten kunnen veroorzaken dergelijke onbetrouwbaar infrastructuur voor het testen van de stabiliteit van hun services om te schrijven van hoge kwaliteit services.</span><span class="sxs-lookup"><span data-stu-id="e0e82-106">In order to write high-quality services, developers need to be able to induce such unreliable infrastructure to test the stability of their services.</span></span>

<span data-ttu-id="e0e82-107">De fout Analysis Services biedt ontwikkelaars de mogelijkheid om te veroorzaken acties voor het testen van services in geval van problemen veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="e0e82-107">The Fault Analysis Service gives developers the ability to induce fault actions to test services in the presence of failures.</span></span> <span data-ttu-id="e0e82-108">Echter krijgt gerichte gesimuleerde fouten u alleen tot nu toe.</span><span class="sxs-lookup"><span data-stu-id="e0e82-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="e0e82-109">Als u wilt de tests meer, kunt u de test-scenario's in Service Fabric: een test chaos en een failover uit.</span><span class="sxs-lookup"><span data-stu-id="e0e82-109">To take the testing further, you can use the test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="e0e82-110">Deze scenario's simuleren continue interleaved fouten correcte en geforceerde afsluiting in het cluster gedurende langere perioden.</span><span class="sxs-lookup"><span data-stu-id="e0e82-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout the cluster over extended periods of time.</span></span> <span data-ttu-id="e0e82-111">Wanneer een test is geconfigureerd met de frequentie en het soort fouten, kan het kan worden gestart via C#-API's of PowerShell, voor het genereren van fouten in het cluster en de service.</span><span class="sxs-lookup"><span data-stu-id="e0e82-111">Once a test is configured with the rate and kind of faults, it can be started through either C# APIs or PowerShell, to generate faults in the cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="e0e82-112">ChaosTestScenario wordt vervangen door een Chaos toleranter, op basis van een service.</span><span class="sxs-lookup"><span data-stu-id="e0e82-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="e0e82-113">Raadpleeg het nieuwe artikel [Chaos beheerd](service-fabric-controlled-chaos.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e0e82-113">Please refer to the new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="e0e82-114">Chaos test</span><span class="sxs-lookup"><span data-stu-id="e0e82-114">Chaos test</span></span>
<span data-ttu-id="e0e82-115">Het scenario chaos genereert fouten over de hele Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="e0e82-115">The chaos scenario generates faults across the entire Service Fabric cluster.</span></span> <span data-ttu-id="e0e82-116">Het scenario comprimeren fouten in het algemeen gezien in maanden of jaren tot enkele uren.</span><span class="sxs-lookup"><span data-stu-id="e0e82-116">The scenario compresses faults generally seen in months or years to a few hours.</span></span> <span data-ttu-id="e0e82-117">De combinatie van interleaved fouten met de snelheid van hoge fouttolerantie vindt complexere cases die anders zijn gemist.</span><span class="sxs-lookup"><span data-stu-id="e0e82-117">The combination of interleaved faults with the high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="e0e82-118">Dit leidt tot een aanzienlijke verbetering van de kwaliteit van de code van de service.</span><span class="sxs-lookup"><span data-stu-id="e0e82-118">This leads to a significant improvement in the code quality of the service.</span></span>

### <a name="faults-simulated-in-the-chaos-test"></a><span data-ttu-id="e0e82-119">Fouten in de test chaos gesimuleerde</span><span class="sxs-lookup"><span data-stu-id="e0e82-119">Faults simulated in the chaos test</span></span>
* <span data-ttu-id="e0e82-120">Een knooppunt opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="e0e82-120">Restart a node</span></span>
* <span data-ttu-id="e0e82-121">Een geïmplementeerde codepakket niet opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="e0e82-121">Restart a deployed code package</span></span>
* <span data-ttu-id="e0e82-122">Een replica verwijderen</span><span class="sxs-lookup"><span data-stu-id="e0e82-122">Remove a replica</span></span>
* <span data-ttu-id="e0e82-123">Een replica starten</span><span class="sxs-lookup"><span data-stu-id="e0e82-123">Restart a replica</span></span>
* <span data-ttu-id="e0e82-124">Verplaatsen van een primaire replica (optioneel)</span><span class="sxs-lookup"><span data-stu-id="e0e82-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="e0e82-125">Verplaatsen van een secundaire replica (optioneel)</span><span class="sxs-lookup"><span data-stu-id="e0e82-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="e0e82-126">De chaos-test meerdere herhalingen van de fouten en cluster validaties worden uitgevoerd voor de opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="e0e82-126">The chaos test runs multiple iterations of faults and cluster validations for the specified period of time.</span></span> <span data-ttu-id="e0e82-127">De tijd voor het cluster stabiel en voor de validatie mislukt, kan ook worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="e0e82-127">The time spent for the cluster to stabilize and for validation to succeed is also configurable.</span></span> <span data-ttu-id="e0e82-128">Het scenario mislukt wanneer u een storing in clustervalidatie bereikt.</span><span class="sxs-lookup"><span data-stu-id="e0e82-128">The scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="e0e82-129">Neem bijvoorbeeld een test te worden uitgevoerd voor één uur met een maximum van drie gelijktijdige fouten.</span><span class="sxs-lookup"><span data-stu-id="e0e82-129">For example, consider a test set to run for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="e0e82-130">De test drie fouten veroorzaken en vervolgens de status van het cluster te valideren.</span><span class="sxs-lookup"><span data-stu-id="e0e82-130">The test will induce three faults, and then validate the cluster health.</span></span> <span data-ttu-id="e0e82-131">De test wordt de vorige stap doorlopen tot het cluster slecht wordt of één uur wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e0e82-131">The test will iterate through the previous step till the cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="e0e82-132">Als het cluster slecht functioneert in elke iteratie, dat wil zeggen het niet binnen een geconfigureerde tijd biedt regulering, mislukt de test met een uitzondering.</span><span class="sxs-lookup"><span data-stu-id="e0e82-132">If the cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, the test will fail with an exception.</span></span> <span data-ttu-id="e0e82-133">Deze uitzondering geeft aan dat er iets een opgetreden fout is en verder onderzoek.</span><span class="sxs-lookup"><span data-stu-id="e0e82-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="e0e82-134">De engine voor het genereren van fouten in de test chaos induceert in de huidige vorm alleen veilige fouten.</span><span class="sxs-lookup"><span data-stu-id="e0e82-134">In its current form, the fault generation engine in the chaos test induces only safe faults.</span></span> <span data-ttu-id="e0e82-135">Dit betekent dat bij gebrek aan externe fouten een quorum of verlies van gegevens nooit plaats.</span><span class="sxs-lookup"><span data-stu-id="e0e82-135">This means that in the absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="e0e82-136">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="e0e82-136">Important configuration options</span></span>
* <span data-ttu-id="e0e82-137">**TimeToRun**: totale tijd die de test uitgevoerd voordat het met succes is voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0e82-137">**TimeToRun**: Total time that the test will run before finishing with success.</span></span> <span data-ttu-id="e0e82-138">De test kan eerder in plaats van een mislukte validatie worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="e0e82-138">The test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="e0e82-139">**MaxClusterStabilizationTimeout**: maximumhoeveelheid wachttijd voor het cluster wordt omgezet in orde voordat het mislukken van de test.</span><span class="sxs-lookup"><span data-stu-id="e0e82-139">**MaxClusterStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="e0e82-140">Controles zijn of de status van de cluster OK is, de servicestatus van de is OK en de doelgrootte van replicaset is bereikt voor de partitie van de service geen InBuild-replica's bestaan.</span><span class="sxs-lookup"><span data-stu-id="e0e82-140">The checks performed are whether cluster health is OK, service health is OK, the target replica set size is achieved for the service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="e0e82-141">**MaxConcurrentFaults**: maximumaantal gelijktijdige fouten die in elke iteratie.</span><span class="sxs-lookup"><span data-stu-id="e0e82-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="e0e82-142">Hoe hoger het getal, de agressievere de test, waardoor daarom complexere failovers en overgang combinaties.</span><span class="sxs-lookup"><span data-stu-id="e0e82-142">The higher the number, the more aggressive the test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="e0e82-143">De test wordt gegarandeerd dat afwezigheid van externe fouten er wordt automatisch een quorum of verlies van gegevens, ongeacht hoe hoog deze configuratie is.</span><span class="sxs-lookup"><span data-stu-id="e0e82-143">The test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="e0e82-144">**EnableMoveReplicaFaults**: Hiermee schakelt u de fouten die worden veroorzaakt door de verplaatsing van de primaire of secundaire replica's of uit.</span><span class="sxs-lookup"><span data-stu-id="e0e82-144">**EnableMoveReplicaFaults**: Enables or disables the faults that are causing the move of the primary or secondary replicas.</span></span> <span data-ttu-id="e0e82-145">Deze fouten worden standaard uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="e0e82-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="e0e82-146">**WaitTimeBetweenIterations**: tijd moet worden gewacht tussen iteraties, dat wil zeggen na een ronde van fouten en bijbehorende validatie.</span><span class="sxs-lookup"><span data-stu-id="e0e82-146">**WaitTimeBetweenIterations**: Amount of time to wait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-to-run-the-chaos-test"></a><span data-ttu-id="e0e82-147">Het uitvoeren van de test chaos</span><span class="sxs-lookup"><span data-stu-id="e0e82-147">How to run the chaos test</span></span>
<span data-ttu-id="e0e82-148">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e0e82-148">C# sample</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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

<span data-ttu-id="e0e82-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0e82-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="e0e82-150">Failover testen</span><span class="sxs-lookup"><span data-stu-id="e0e82-150">Failover test</span></span>
<span data-ttu-id="e0e82-151">Het scenario voor het testen van failover is een versie van het scenario voor het testen van chaos die gericht is op een specifieke service-partitie.</span><span class="sxs-lookup"><span data-stu-id="e0e82-151">The failover test scenario is a version of the chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="e0e82-152">Deze test het effect van failover op een specifieke service partitie terwijl de andere services niet is beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="e0e82-152">It tests the effect of failover on a specific service partition while leaving the other services unaffected.</span></span> <span data-ttu-id="e0e82-153">Zodra deze geconfigureerd met de doel-partitiegegevens en andere parameters, deze wordt uitgevoerd als een client-side '-hulpprogramma dat gebruikmaakt van C#-API's of PowerShell voor het genereren van fouten voor de partitie van een service.</span><span class="sxs-lookup"><span data-stu-id="e0e82-153">Once it's configured with the target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell to generate faults for a service partition.</span></span> <span data-ttu-id="e0e82-154">Het scenario doorlopen een reeks gesimuleerde fouten en servicevalidatie tijdens het uitvoeren van uw bedrijfslogica op de zijde bieden een werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="e0e82-154">The scenario iterates through a sequence of simulated faults and service validation while your business logic runs on the side to provide a workload.</span></span> <span data-ttu-id="e0e82-155">Een fout in servicevalidatie geeft een probleem dat verder onderzoek moet.</span><span class="sxs-lookup"><span data-stu-id="e0e82-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-the-failover-test"></a><span data-ttu-id="e0e82-156">Fouten in de test failover gesimuleerde</span><span class="sxs-lookup"><span data-stu-id="e0e82-156">Faults simulated in the failover test</span></span>
* <span data-ttu-id="e0e82-157">Een geïmplementeerd codepakket waarop de partitie wordt gehost opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="e0e82-157">Restart a deployed code package where the partition is hosted</span></span>
* <span data-ttu-id="e0e82-158">Een primaire en secundaire replica of stateless exemplaar verwijderen</span><span class="sxs-lookup"><span data-stu-id="e0e82-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="e0e82-159">Een primaire, secundaire replica opnieuw opstarten (indien een permanente service)</span><span class="sxs-lookup"><span data-stu-id="e0e82-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="e0e82-160">Verplaatsen van een primaire replica</span><span class="sxs-lookup"><span data-stu-id="e0e82-160">Move a primary replica</span></span>
* <span data-ttu-id="e0e82-161">Verplaatsen van een secundaire replica</span><span class="sxs-lookup"><span data-stu-id="e0e82-161">Move a secondary replica</span></span>
* <span data-ttu-id="e0e82-162">De partitie opnieuw starten</span><span class="sxs-lookup"><span data-stu-id="e0e82-162">Restart the partition</span></span>

<span data-ttu-id="e0e82-163">De failover-test induceert een gekozen veroorzaakt en validatie wordt uitgevoerd op de service om te controleren of de stabiliteit.</span><span class="sxs-lookup"><span data-stu-id="e0e82-163">The failover test induces a chosen fault and then runs validation on the service to ensure its stability.</span></span> <span data-ttu-id="e0e82-164">De failover-test induceert slechts één fout tegelijk in plaats van mogelijk meerdere fouten in de test chaos.</span><span class="sxs-lookup"><span data-stu-id="e0e82-164">The failover test induces only one fault at a time, as opposed to possible multiple faults in the chaos test.</span></span> <span data-ttu-id="e0e82-165">Als de service-partitie heeft niet binnen de geconfigureerde time-out regulering na elke fout, mislukt de test.</span><span class="sxs-lookup"><span data-stu-id="e0e82-165">If the service partition does not stabilize within the configured timeout after each fault, the test fails.</span></span> <span data-ttu-id="e0e82-166">De test induceert alleen veilige fouten.</span><span class="sxs-lookup"><span data-stu-id="e0e82-166">The test induces only safe faults.</span></span> <span data-ttu-id="e0e82-167">Dit betekent dat geen externe fouten, een quorum of verlies van gegevens wordt niet uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e0e82-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="e0e82-168">Belangrijke configuratie-opties</span><span class="sxs-lookup"><span data-stu-id="e0e82-168">Important configuration options</span></span>
* <span data-ttu-id="e0e82-169">**PartitionSelector**: Selector-object waarmee de partitie die moet worden toegepast.</span><span class="sxs-lookup"><span data-stu-id="e0e82-169">**PartitionSelector**: Selector object that specifies the partition that needs to be targeted.</span></span>
* <span data-ttu-id="e0e82-170">**TimeToRun**: totale tijd dat de test wordt uitgevoerd voordat u voltooit.</span><span class="sxs-lookup"><span data-stu-id="e0e82-170">**TimeToRun**: Total time that the test will run before finishing.</span></span>
* <span data-ttu-id="e0e82-171">**MaxServiceStabilizationTimeout**: maximumhoeveelheid wachttijd voor het cluster wordt omgezet in orde voordat het mislukken van de test.</span><span class="sxs-lookup"><span data-stu-id="e0e82-171">**MaxServiceStabilizationTimeout**: Maximum amount of time to wait for the cluster to become healthy before failing the test.</span></span> <span data-ttu-id="e0e82-172">De controles uitgevoerd worden of servicestatus OK is, de doelgrootte van replicaset is bereikt voor alle partities en geen InBuild-replica's bestaan.</span><span class="sxs-lookup"><span data-stu-id="e0e82-172">The checks performed are whether service health is OK, the target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="e0e82-173">**WaitTimeBetweenFaults**: tijd moet worden gewacht tussen elke cyclus veroorzaakt en validatie.</span><span class="sxs-lookup"><span data-stu-id="e0e82-173">**WaitTimeBetweenFaults**: Amount of time to wait between every fault and validation cycle.</span></span>

### <a name="how-to-run-the-failover-test"></a><span data-ttu-id="e0e82-174">Het uitvoeren van de failover-test</span><span class="sxs-lookup"><span data-stu-id="e0e82-174">How to run the failover test</span></span>
<span data-ttu-id="e0e82-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="e0e82-175">**C#**</span></span>

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

        // The chaos test scenario should run at least 60 minutes or until it fails.
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

        // Create the scenario class and execute it asynchronously.
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


<span data-ttu-id="e0e82-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e0e82-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
