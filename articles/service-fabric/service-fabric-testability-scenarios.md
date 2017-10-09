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
# <a name="testability-scenarios"></a>Testbaarheid scenario 's
Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden. Azure Service Fabric biedt ontwikkelaars Hallo mogelijkheid toowrite services toorun boven op onbetrouwbare infrastructuren. Ontwikkelaars moeten kunnen tooinduce toobe dergelijke onbetrouwbaar infrastructuur tootest Hallo stabiliteit van hun services in de volgorde toowrite hoogwaardige services.

Hallo-fout Analysis Service biedt ontwikkelaars Hallo mogelijkheid tooinduce veroorzaakt acties tootest services in Hallo aanwezigheid van fouten. Echter krijgt gerichte gesimuleerde fouten u alleen tot nu toe. tootake hello verder testen kunt u Hallo Testscenario's in Service Fabric: een test chaos en een failover uit. Deze scenario's simuleren continue interleaved fouten correcte en geforceerde afsluiting in de cluster Hallo gedurende langere perioden. Wanneer een test met Hallo frequentie en het soort fouten is geconfigureerd, kan het kan worden gestart via C# API's of PowerShell, toogenerate fouten in de cluster Hallo en uw service.

> [!WARNING]
> ChaosTestScenario wordt vervangen door een Chaos toleranter, op basis van een service. Raadpleeg toohello nieuw artikel [Chaos beheerd](service-fabric-controlled-chaos.md) voor meer informatie.
> 
> 

## <a name="chaos-test"></a>Chaos test
Hallo chaos scenario genereert fouten over de hele Service Fabric-cluster Hallo. Hallo scenario comprimeren fouten in het algemeen gezien in maanden of jaren tooa enkele uren. Hallo combinatie van interleaved fouten met Hallo hoge fouttolerantie tarief vindt complexere cases die anders zijn gemist. Dit leidt tooa aanzienlijke verbetering in Hallo code servicekwaliteit Hallo.

### <a name="faults-simulated-in-hello-chaos-test"></a>Fouten in Hallo chaos test gesimuleerde
* Een knooppunt opnieuw opstarten
* Een geïmplementeerde codepakket niet opnieuw starten
* Een replica verwijderen
* Een replica starten
* Verplaatsen van een primaire replica (optioneel)
* Verplaatsen van een secundaire replica (optioneel)

Hallo chaos test wordt uitgevoerd voor meerdere pogingen storingen en cluster validaties voor Hallo opgegeven tijdsperiode. Hallo tijd voor Hallo cluster toostabilize en voor validatie toosucceed kan ook worden geconfigureerd. Hallo scenario mislukt wanneer u een storing in clustervalidatie bereikt.

Neem bijvoorbeeld dat een test toorun gedurende één uur met een maximum van drie gelijktijdige fouten ingesteld. Hallo test drie fouten veroorzaken en Hallo cluster health vervolgens te valideren. Hallo-test wordt de vorige stap Hallo doorlopen totdat het Hallo-cluster wordt slecht of één uur wordt doorgegeven. Als in elke iteratie slecht functioneert Hallo-cluster, dat wil zeggen het niet binnen een geconfigureerde tijd biedt regulering, Hallo test mislukt met een uitzondering. Deze uitzondering geeft aan dat er iets een opgetreden fout is en verder onderzoek.

In de huidige vorm induceert Hallo veroorzaakt generatie engine Hallo chaos test alleen veilige fouten. Dit betekent dat Hallo geen externe fouten, een quorum of verlies van gegevens nooit plaats.

### <a name="important-configuration-options"></a>Belangrijke configuratie-opties
* **TimeToRun**: totale tijd Hallo test wordt uitgevoerd voordat het met succes is voltooid. Hallo test kan eerder in plaats van een mislukte validatie worden voltooid.
* **MaxClusterStabilizationTimeout**: maximumhoeveelheid tijd toowait voor Hallo cluster toobecome voordat het Hallo-test mislukt in orde. Hello controles uitgevoerd worden Hiermee wordt aangegeven of de status van de cluster OK is, de servicestatus van de is OK, hello doelgrootte van replicaset bereikt voor Hallo service partitie en geen InBuild-replica's bestaan.
* **MaxConcurrentFaults**: maximumaantal gelijktijdige fouten die in elke iteratie. Hallo hoger Hallo nummer, Hallo agressievere Hallo-test, daarom resulteert in meer complexe failovers en overgang combinaties. Hallo-test wordt gegarandeerd dat afwezigheid van externe fouten er wordt automatisch een quorum of verlies van gegevens, ongeacht hoe hoog deze configuratie is.
* **EnableMoveReplicaFaults**: Hiermee schakelt u Hallo-fouten dat Hallo verplaatsing van Hallo primaire of secundaire replica's veroorzaken of uit. Deze fouten worden standaard uitgeschakeld.
* **WaitTimeBetweenIterations**: hoeveelheid tijd toowait tussen iteraties, dat wil zeggen na een ronde van fouten en bijbehorende validatie.

### <a name="how-toorun-hello-chaos-test"></a>Hoe toorun Hallo chaos testen
C#-voorbeeld

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

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Failover testen
Hallo failover Testscenario is een versie van Hallo chaos Testscenario die gericht is op een specifieke service-partitie. Deze test Hallo effect van failover op een specifieke service partitie terwijl Hallo andere services niet is beïnvloed. Zodra deze geconfigureerd met Hallo doel partitiegegevens en andere parameters, deze wordt uitgevoerd als een client-side '-hulpprogramma dat gebruikmaakt van C#-API's of PowerShell toogenerate fouten voor de partitie van een service. een reeks gesimuleerde fouten en servicevalidatie doorlopen Hallo scenario terwijl uw bedrijfslogica wordt uitgevoerd op Hallo side tooprovide een werkbelasting. Een fout in servicevalidatie geeft een probleem dat verder onderzoek moet.

### <a name="faults-simulated-in-hello-failover-test"></a>Fouten die zijn geëmuleerd in Hallo failover testen
* Een geïmplementeerd codepakket waar Hallo partitie wordt gehost opnieuw starten
* Een primaire en secundaire replica of stateless exemplaar verwijderen
* Een primaire, secundaire replica opnieuw opstarten (indien een permanente service)
* Verplaatsen van een primaire replica
* Verplaatsen van een secundaire replica
* Hallo-partitie opnieuw starten

Hallo failover uit een gekozen fout induceert en voert validatie op Hallo service tooensure de stabiliteit. Hallo failover testen induceert alleen een fault op een tijd, in tegenstelling tot toopossible meerdere fouten in Hallo chaos test. Als Hallo service partitie heeft niet binnen de time-out Hallo geconfigureerd regulering na elke fout, mislukt de Hallo test. Hallo test induceert alleen veilige fouten. Dit betekent dat geen externe fouten, een quorum of verlies van gegevens wordt niet uitgevoerd.

### <a name="important-configuration-options"></a>Belangrijke configuratie-opties
* **PartitionSelector**: Selector-object dat Hiermee geeft u Hallo partitie die gericht toobe nodig.
* **TimeToRun**: totale tijd die Hallo-test wordt uitgevoerd voordat u voltooit.
* **MaxServiceStabilizationTimeout**: maximumhoeveelheid tijd toowait voor Hallo cluster toobecome voordat het Hallo-test mislukt in orde. Hallo controles uitgevoerd zijn of de servicestatus OK is, wordt hello doelgrootte van replicaset bereikt voor alle partities en geen InBuild-replica's bestaan.
* **WaitTimeBetweenFaults**: hoeveelheid toowait tijd tussen elke cyclus veroorzaakt en validatie.

### <a name="how-toorun-hello-failover-test"></a>Hoe toorun Hallo failover testen
**C#**

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


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
