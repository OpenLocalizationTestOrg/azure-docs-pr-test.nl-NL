---
title: aaaSimulate fouten in Azure microservices | Microsoft Docs
description: In dit artikel wordt gesproken over Hallo testbaarheid acties gevonden in Microsoft Azure Service Fabric.
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a>Testbaarheid acties
In volgorde toosimulate een onbetrouwbare infrastructuur biedt Azure Service Fabric u Hallo-ontwikkelaars met manieren toosimulate verschillende echte fouten en statusovergangen. Deze zijn beschikbaar als testbaarheid acties. Hallo acties zijn Hallo op laag niveau API's die ertoe leiden dat een specifieke fout injectie, statusovergang of validatie. U kunt uitgebreide Testscenario's voor uw services schrijven door een combinatie van deze acties.

Service Fabric bevat dat enkele algemene scenario's voor test bestaan uit deze acties. Het is raadzaam dat u gebruikmaken van deze ingebouwde scenario's, zorgvuldig worden gekozen tootest algemene statusovergangen en mislukte aanvragen. Acties kunnen echter aangepaste Testscenario's gebruikte toocreate zijn als u wilt dat tooadd dekking voor scenario's die zijn niet wordt gedekt door ingebouwde Hallo-scenario's nog of die aangepaste speciaal afgestemd op uw toepassing.

C#-implementaties van Hallo acties zijn gevonden in Hallo System.Fabric.dll assembly. Hallo System Fabric PowerShell-module is gevonden in Hallo Microsoft.ServiceFabric.Powershell.dll assembly. Hallo ServiceFabric PowerShell-module is als onderdeel van de runtime-installatie geïnstalleerde tooallow voor eenvoudig te gebruiken.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Correcte versus geforceerde afsluiting veroorzaakt acties
Testbaarheid acties worden ingedeeld in twee belangrijke buckets:

* Geforceerde afsluiting fouten: deze fouten simuleren fouten zoals machine opnieuw is opgestart en crashes verwerken. In dergelijke gevallen van fouten Hallo uitvoeringscontext van proces abrupt. Dit betekent dat er geen opschoning van Hallo staat kunt uitvoeren voordat de toepassing hello opnieuw is gestart.
* Correcte fouten: deze fouten simuleren correcte acties zoals replica wordt verplaatst en verwijdert geactiveerd door de taakverdeling. In dergelijke gevallen Hallo-service een melding van Hallo sluiten opgehaald en opschonen Hallo status voordat u afsluit.

Hallo-service voor betere validatie van de kwaliteit, uitvoeren en zakelijke werkbelasting bij verschillende systemen op correct wijze en geforceerde afsluiting fouten veroorzaken. Geforceerde afsluiting fouten oefenen scenario's waarbij Hallo-serviceproces in het midden van een werkstroom Hallo abrupt afgesloten. Deze tests Hallo herstelpad zodra de Hallo service replica is hersteld door de Service Fabric. Dit helpt testen gegevensconsistentie en of de servicestatus Hallo correct wordt bijgehouden na fouten. Hallo andere set van fouten (Hallo correcte fouten) testen dat Hallo-service juist wordt verplaatst op door de Service Fabric tooreplicas reageert. Dit webtests verwerking van de annulering op Hallo RunAsync-methode. Hallo-service moet toocheck voor Hallo annulering token wordt instellen, de status goed opslaan en sluiten Hallo RunAsync-methode.

## <a name="testability-actions-list"></a>Lijst van acties testbaarheid
| Actie | Beschrijving | Beheerde API | PowerShell-cmdlet | Correcte/geforceerde afsluiting fouten |
| --- | --- | --- | --- | --- |
| CleanTestState |Verwijdert alle Hallo teststatus van Hallo-cluster in geval van een onjuist afsluiten van het stuurprogramma voor Hallo-test. |CleanTestStateAsync |Remove-ServiceFabricTestState |Niet van toepassing |
| InvokeDataLoss |Induceert verlies van gegevens in een service-partitie. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Correcte |
| InvokeQuorumLoss |De partitie van een bepaalde stateful service plaatst in quorumverlies. |InvokeQuorumLossAsync |Aanroepen ServiceFabricQuorumLoss |Correcte |
| Primaire verplaatsen |Verplaatst Hallo opgegeven primaire replica van een clusterknooppunt stateful service toohello opgegeven. |MovePrimaryAsync |Verplaatsing ServiceFabricPrimaryReplica |Correcte |
| Secundaire verplaatsen |Hallo huidige secundaire replica van een stateful service tooa ander clusterknooppunt verplaatst. |MoveSecondaryAsync |Verplaatsing ServiceFabricSecondaryReplica |Correcte |
| RemoveReplica |Een replica-fout simuleert door het verwijderen van een replica van een cluster. Dit Hallo replica wordt gesloten en verandert deze toorole 'None', verwijderen van alle van de status van Hallo-cluster. |RemoveReplicaAsync |Verwijder ServiceFabricReplica |Correcte |
| RestartDeployedCodePackage |Simuleert een fout in het pakket code door een codepakket geïmplementeerd op een knooppunt in een cluster opnieuw te starten. Hiermee annuleert Hallo code pakket proces dat wordt alle Hallo gebruiker service replica's die worden gehost in het proces opnieuw opgestart. |RestartDeployedCodePackageAsync |Opnieuw opstarten ServiceFabricDeployedCodePackage |Geforceerde afsluiting |
| Restartnode uitgevoerd |Simuleert een knooppuntfout voor Service Fabric-cluster door een knooppunt opnieuw te starten. |RestartNodeAsync |Opnieuw opstarten ServiceFabricNode |Geforceerde afsluiting |
| RestartPartition |Simuleert een datacenter onleesbaar of cluster onleesbaar scenario door enkele of alle replica's van een partitie opnieuw te starten. |RestartPartitionAsync |Restart-ServiceFabricPartition |Correcte |
| RestartReplica |Simuleert een replica mislukt door een persistente replica opnieuw te starten in een cluster, Hallo replica sluiten en vervolgens opnieuw te openen. |RestartReplicaAsync |Opnieuw opstarten ServiceFabricReplica |Correcte |
| StartNode |Start een knooppunt in een cluster dat is al gestopt. |StartNodeAsync |Start-ServiceFabricNode |Niet van toepassing |
| StopNode |Simuleert een storing op een knooppunt door het stoppen van een knooppunt in een cluster. Hallo knooppunt blijft omlaag totdat beginknooppunt wordt aangeroepen. |StopNodeAsync |Stop-ServiceFabricNode |Geforceerde afsluiting |
| ValidateApplication |Hallo beschikbaarheid en de status van alle Service Fabric-services in een toepassing, meestal na een bepaalde fout veroorzaken in Hallo systeem gevalideerd. |ValidateApplicationAsync |Test ServiceFabricApplication |Niet van toepassing |
| ValidateService |Valideert Hallo beschikbaarheid en status van een Service Fabric-service, meestal na een bepaalde fout veroorzaken in Hallo-systeem. |ValidateServiceAsync |Test ServiceFabricService |Niet van toepassing |

## <a name="running-a-testability-action-using-powershell"></a>Uitvoeren van een testbaarheid actie met behulp van PowerShell
Deze zelfstudie leert u hoe toorun een actie testbaarheid met behulp van PowerShell. U leert hoe toorun een actie testbaarheid op basis van een lokaal (1-box)-cluster of een Azure-cluster. Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell-module wordt automatisch geïnstalleerd wanneer u Microsoft Service Fabric MSI Hallo installeert. Hallo-module wordt automatisch geladen wanneer u een PowerShell-prompt opent.

Zelfstudie segmenten:

* [Een actie uitvoeren op een cluster met één verpakking](#run-an-action-against-a-one-box-cluster)
* [Een actie uitvoeren op een Azure-cluster](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Een actie uitvoeren op een cluster met één verpakking
toorun een testbaarheid actie tegen een lokaal cluster voor de eerste verbinding toohello cluster en open Hallo PowerShell-prompt in de beheerdersmodus. Laat het ons bekijkt hello **herstart ServiceFabricNode** in te grijpen.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Hier Hallo actie **herstart ServiceFabricNode** wordt uitgevoerd op een knooppunt met de naam 'Knooppunt1'. Hallo voltooiing modus geeft aan dat deze niet controleren moet of Hallo herstart knooppunt actie daadwerkelijk is geslaagd. Geven Hallo voltooiing modus als 'Verifiëren' zal deze tooverify of actie Hallo daadwerkelijk is voltooid. In plaats van Hallo knooppunt direct met de naam op te geven, kunt u deze via een partitie sleutel en Hallo soort replica, als volgt opgeven:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Opnieuw opstarten ServiceFabricNode** gebruikte toorestart een Service Fabric-knooppunt in een cluster moet worden. Hiermee stopt u Hallo Fabric.exe proces, dat alle Hallo system service en de gebruiker service replica's die worden gehost op dat knooppunt wordt opnieuw opgestart. Met deze API tootest helpt uw service onthullen bugs langs Hallo failover herstel paden. Zo kunt u knooppuntfouten in Hallo cluster simuleren.

Hallo volgende schermafbeelding ziet u Hallo **herstart ServiceFabricNode** testbaarheid opdracht in te grijpen.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Hallo uitvoer Hallo eerst **Get-ServiceFabricNode** (een cmdlet uit Hallo Service Fabric PowerShell-module) wordt aangegeven dat Hallo lokale cluster bevat vijf knooppunten: Node.1 tooNode.5. Na Hallo testbaarheid actie (cmdlet) **herstart ServiceFabricNode** op Hallo-knooppunt wordt uitgevoerd met de naam Node.4, zien we dat Hallo-knooppunt bedrijfstijd is opnieuw ingesteld.

### <a name="run-an-action-against-an-azure-cluster"></a>Een actie uitvoeren op een Azure-cluster
Met het uitvoeren van een actie testbaarheid (via PowerShell) in een Azure-cluster is vergelijkbaar toorunning Hallo actie tegen een lokaal cluster. Hallo alleen verschil dat, is voordat u Hallo actie, in plaats van verbindende toohello lokale cluster uitvoeren kunt, moet u tooconnect toohello Azure eerst het cluster.

## <a name="running-a-testability-action-using-c35"></a>Uitvoeren van een testbaarheid actie met C &#35;
toorun een actie testbaarheid met behulp van C#, moet u eerst tooconnect toohello cluster met behulp van FabricClient. Zodoende Hallo parameters nodig toorun Hallo actie. Andere parameters kunnen worden gebruikt toorun Hallo dezelfde actie.
Kijken Hallo RestartServiceFabricNode actie eenrichtingssessie toorun is met behulp van Hallo knooppuntgegevens (naam van het knooppunt en knooppunt exemplaar-ID) in het Hallo-cluster.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Uitleg van de parameter:

* **CompleteMode** geeft die Hallo-modus niet moet controleren of Hallo herstart actie daadwerkelijk is geslaagd. Geven Hallo voltooiing modus als 'Verifiëren' zal deze tooverify of actie Hallo daadwerkelijk is voltooid.  
* **OperationTimeout** sets Hallo Hallo bewerking toofinish tijd voordat een TimeoutException-uitzondering is opgetreden.
* **CancellationToken** kunt u een aanroep van in behandeling toobe geannuleerd.

In plaats van Hallo knooppunt direct met de naam op te geven, kunt u dit via een partitie sleutel en Hallo soort replica opgeven.

Zie voor meer informatie [PartitionSelector en ReplicaSelector](#partition_replica_selector).

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector en ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector is een helper worden weergegeven in testbaarheid en is gebruikte tooselect een specifieke partitie op welke tooperform Hallo testbaarheid acties. Het zijn gebruikte tooselect een specifieke partitie als de partitie-ID Hallo vooraf bekend. Of, kunt u de partitiesleutel Hallo en Hallo bewerking intern Hallo partitie-ID wordt opgelost. U hebt ook Hallo-optie van het selecteren van een willekeurige partitie.

toouse deze helper Hallo PartitionSelector object maken en selecteer Hallo-partitie met behulp van een Hallo Select * methoden. Vervolgens worden doorgegeven in Hallo PartitionSelector object toohello API dat vereist is. Als geen optie is geselecteerd, wordt standaard tooa willekeurige partitie.

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector is een helper worden weergegeven in testbaarheid en is gebruikte toohelp selecteert u een replica op welke tooperform Hallo testbaarheid acties. Het zijn gebruikte tooselect een specifieke replica als de replica-ID Hallo vooraf bekend. Bovendien hebt u de optie Hallo van het selecteren van een primaire replica of een willekeurige secundaire site. ReplicaSelector is afgeleid van PartitionSelector, dus moet u tooselect Hallo beide replica en Hallo partitie waarop u wilt dat tooperform Hallo testbaarheid bewerking.

toouse deze helper maken van een object ReplicaSelector en Hallo gewenste tooselect Hallo replica en Hallo partitie ingesteld. U kunt deze vervolgens doorgeven in Hallo-API die dit vereist is. Als geen optie is geselecteerd, wordt het standaard tooa willekeurige replica en willekeurige partitie.

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a>Volgende stappen
* [Testbaarheid scenario 's](service-fabric-testability-scenarios.md)
* Hoe tootest uw service
  * [Fouten tijdens de service werkbelastingen simuleren](service-fabric-testability-workload-tests.md)
  * [Fouten in de service-naar-service](service-fabric-testability-scenarios-service-communication.md)

