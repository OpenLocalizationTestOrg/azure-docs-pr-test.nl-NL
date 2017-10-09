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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Veroorzaken gecontroleerde Chaos in Service Fabric-clusters
Grote gedistribueerde systemen zoals cloudinfrastructuren inherent onbetrouwbaar worden. Azure Service Fabric kunnen ontwikkelaars toowrite betrouwbare gedistribueerde services op een onbetrouwbaar-infrastructuur. toowrite robuuste gedistribueerde services op een onbetrouwbaar-infrastructuur, ontwikkelaars moeten toobe kunnen tootest Hallo stabiliteit van hun services terwijl Hallo onderliggende onbetrouwbaar infrastructuur wordt verzonden via ingewikkeld statusovergangen vanwege toofaults.

Hallo [fout injectie en analyse van de clusterservice](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (ook wel bekend als hello veroorzaakt Analysis Service) biedt ontwikkelaars de mogelijkheid Hallo tooinduce bedrijfsstoringen tootest hun services. Deze gericht fouten, zoals gesimuleerde [opnieuw starten van een partitie](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), kunt u de meest voorkomende statusovergangen Hallo uitoefenen. Echter fouten gerichte gesimuleerde fouten per definitie zijn gericht en dus mist mogelijk die weergeven van alleen in moeilijk te voorspellen, lang en gecompliceerd reeks statusovergangen. Voor een zuivere testen, kunt u Chaos.

Periodieke, interleaved fouten (correcte en geforceerde afsluiting) in de cluster Hallo simuleert chaos gedurende langere perioden. Nadat u Chaos met Hallo frequentie en het soort fouten Hallo hebt geconfigureerd, kunt u Chaos starten via de C# of Powershell API toostart genereren van fouten in de cluster hello en in uw services. U kunt Chaos toorun configureren voor een opgegeven periode (bijvoorbeeld: voor één uur), waarna Chaos automatisch wordt gestopt, of u kunt StopChaos API (C# of Powershell) toostop aanroepen op elk gewenst moment.

> [!NOTE]
> In de huidige vorm induceert Chaos alleen veilige fouten, wat betekent dat dat Hallo ontbreken van een externe fouten een quorumverlies of verlies van gegevens nooit plaatsvindt.
>

Terwijl Chaos wordt uitgevoerd, is het resultaat van andere gebeurtenissen die status Hallo Hallo uitgevoerd op moment Hallo vastleggen. Een ExecutingFaultsEvent bevat bijvoorbeeld alle Hallo gebreken Chaos besloten tooexecute in die iteratie. Een ValidationFailedEvent bevat Hallo details van een mislukte validatie (health of stabiliteit problemen) die tijdens de validatie van de cluster Hallo Hallo is gevonden. U kunt aanroepen Hallo GetChaosReport API (C# of Powershell) tooget Hallo rapport van Chaos wordt uitgevoerd. Deze gebeurtenissen ophalen permanent in een [betrouwbare woordenlijst](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), heeft een beleid moet worden afgekapt is bepaald door twee configuraties: **MaxStoredChaosEventCount** (de standaardwaarde is 25000) en  **StoredActionCleanupIntervalInSeconds** (de standaardwaarde is 3600). Elke *StoredActionCleanupIntervalInSeconds* Chaos controles en alle maar Hallo meest recente *MaxStoredChaosEventCount* gebeurtenissen van betrouwbare woordenboek Hallo worden opgeschoond.

## <a name="faults-induced-in-chaos"></a>Fouten worden bewerkstelligd in Chaos
Chaos fouten over de hele Service Fabric-cluster Hallo genereert en comprimeert fouten die zijn zichtbaar in maanden of jaren in een paar uur. Hallo combinatie van interleaved fouten met Hallo hoge fouttolerantie tarief vindt hoek aanvragen die mogelijk anders worden overgeslagen. In deze oefening dank leidt tooa aanzienlijke verbetering in Hallo code servicekwaliteit Hallo.

Chaos induceert fouten van Hallo volgende categorieën:

* Een knooppunt opnieuw opstarten
* Een geïmplementeerde codepakket niet opnieuw starten
* Een replica verwijderen
* Een replica starten
* Verplaatsen van een primaire replica (configureren)
* Verplaatsen van een secundaire replica (configureren)

Chaos in meerdere pogingen uitgevoerd. Elke herhaling bestaat uit de fouten en clustervalidatie voor Hallo opgegeven periode. U kunt Hallo tijd voor Hallo cluster toostabilize en voor validatie toosucceed configureren. Als een fout in validatie wordt gevonden, wordt Chaos genereert en een ValidationFailedEvent met de UTC-timestamp Hallo en foutdetails Hallo zich blijft voordoen. Neem bijvoorbeeld een exemplaar dank die toorun is ingesteld voor een uur met een maximum van drie gelijktijdige fouten. Chaos induceert drie fouten en controleert vervolgens Hallo cluster health. Doorlopen Hallo vorige stap totdat deze expliciet gestopt via Hallo StopChaosAsync API of één uur wordt doorgegeven. Als het cluster Hallo slecht in elke iteratie (dat wil zeggen, het heeft geen regulering binnen Hallo doorgegeven in MaxClusterStabilizationTimeout), Chaos genereert een ValidationFailedEvent. Deze gebeurtenis geeft aan dat er iets een opgetreden fout is en verder onderzoek moet mogelijk.

tooget die Chaos wordt veroorzaakt bedrijfsstoringen, kunt u GetChaosReport API (powershell of C#). Hallo API opgehaald Hallo volgende segment van Hallo Chaos rapport op basis van Hallo doorgegeven vervolgtoken of Hallo doorgegeven-tijdsbereik. Kunt u opgeven ContinuationToken tooget Hallo volgende segment van Hallo Chaos rapport Hallo of kunt u Hallo-tijdsbereik via StartTimeUtc en EndTimeUtc opgeven, maar u niet zowel Hallo ContinuationToken Hallo tijdsbereik opgeven in Hallo dezelfde aanroep. Wanneer er meer dan 100 Chaos gebeurtenissen, wordt Hallo Chaos rapport geretourneerd in segmenten waarbij een segment niet meer dan 100 Chaos gebeurtenissen bevat.

## <a name="important-configuration-options"></a>Belangrijke configuratie-opties
* **TimeToRun**: totale tijd die Chaos wordt uitgevoerd voordat het met succes is voltooid. U kunt Chaos stoppen voordat deze is uitgevoerd gedurende TimeToRun Hallo via Hallo StopChaos API.

* **MaxClusterStabilizationTimeout**: Hallo maximale hoeveelheid tijd toowait voor Hallo cluster toobecome voordat het opstellen van een ValidationFailedEvent in orde. Deze wachttijd is de tooreduce Hallo belasting op Hallo cluster terwijl deze wordt hersteld. Hallo-controles uitgevoerd worden:
  * Als de status van de cluster Hallo is OK
  * Als het Hallo-service de status is OK
  * Als Hallo doelreplica grootte ingesteld wordt voor Hallo service partitie bereikt
  * Dat er geen InBuild-replica's bestaan
* **MaxConcurrentFaults**: Hallo maximum aantal gelijktijdige fouten die in elke iteratie veroorzaakt. Hallo hoger Hallo getal, Hallo agressievere Chaos is en Hallo failovers en Hallo status overgang combinaties van die cluster Hallo doorloopt NTDS zijn ook complexere. 

> [!NOTE]
> Ongeacht hoe hoge waarde *MaxConcurrentFaults* heeft, Chaos garandeert - Hallo ontbreken van een externe fouten - er is geen quorumverlies of verlies van gegevens.
>

* **EnableMoveReplicaFaults**: Hiermee schakelt u Hallo fouten waardoor Hallo primaire of secundaire replica's toomove of uit. Deze fouten worden standaard uitgeschakeld.
* **WaitTimeBetweenIterations**: Hallo hoeveelheid tijd toowait tussen iteraties. Dat wil zeggen, Hallo tijdsduur die chaos onderbroken na het uitvoeren van een ronde van fouten en de bijbehorende validatie Hallo Hallo gezondheidstoestand van Hallo cluster hebben voltooid. hogere Hallo waarde Hallo Hallo lager is Hallo gemiddelde veroorzaakt injectie snelheid.
* **WaitTimeBetweenFaults**: Hallo hoeveelheid tijd toowait tussen twee opeenvolgende fouten in een enkel iteratie. Hallo hogere Hallo-waarde, lagere Hallo gelijktijdigheid van hello (of Hallo overlapping tussen) fouten.
* **ClusterHealthPolicy**: Cluster statusbeleid is gebruikte toovalidate Hallo status van de cluster Hallo Between Chaos iteraties. Als Hallo cluster health onjuist is of als een onverwachte uitzondering tijdens het uitvoeren van de fout gebeurt, Chaos gedurende 30 minuten Hallo volgende-statuscontrole - tooprovide Hallo cluster met een aantal toorecuperate tijd wacht.
* **Context**: een verzameling van (string, string) typt u sleutel-waardeparen. Hallo-kaart kan worden gebruikt toorecord informatie over Hallo Chaos uitvoeren. Er mag niet meer dan 100 dergelijke paren en elke tekenreeks (sleutel of waarde) mag hoogstens 4095 tekens bevatten. Deze kaart is ingesteld door Hallo starter van Hallo Chaos uitvoeren toooptionally store Hallo context over Hallo specifieke uitvoeren.

## <a name="how-toorun-chaos"></a>Hoe toorun Chaos

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
