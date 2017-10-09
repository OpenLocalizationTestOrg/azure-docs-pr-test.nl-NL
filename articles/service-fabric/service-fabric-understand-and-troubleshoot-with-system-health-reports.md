---
title: aaaTroubleshoot met systeemstatusrapporten | Microsoft Docs
description: Hierin wordt beschreven Hallo statusrapporten verzonden door Azure Service Fabric-onderdelen en hun gebruik voor het oplossen van problemen cluster of problemen met de toepassing.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: 52574ea7-eb37-47e0-a20a-101539177625
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: c77a6cdd0440ce5d354cd8760f40151f674a3529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-system-health-reports-tootroubleshoot"></a>Gebruik system health rapporten tootroubleshoot
Azure Service Fabric-onderdelen rapport out of box Hallo op alle entiteiten in Hallo-cluster. Hallo [health store](service-fabric-health-introduction.md#health-store) maken en verwijderen van de entiteiten die zijn gebaseerd op rapporten van Hallo-systeem. Ook ordent ze in een hiërarchie die entiteit interacties worden vastgelegd.

> [!NOTE]
> toounderstand health-gerelateerde begrippen meer informatie op [Service Fabric-statusmodel](service-fabric-health-introduction.md).
> 
> 

Systeemstatusrapporten bieden inzicht in het cluster en de functionaliteit van de toepassing en de vlag problemen via health. Voor toepassingen en services controleren systeemstatusrapporten of entiteiten worden geïmplementeerd en correct van Hallo Service Fabric-perspectief zich gedragen. Hallo rapporten bieden een statuscontrole van de bedrijfslogica Hallo van Hallo service of detectie van vastgelopen processen. Gebruiker services kunnen Hallo statusgegevens met informatie specifieke tootheir logica aanvullen.

> [!NOTE]
> Statusrapporten watchdogs zijn alleen zichtbaar *nadat* Hallo-systeemonderdelen maken van een entiteit. Wanneer een entiteit wordt verwijderd, worden alle statusrapporten gekoppeld in Hallo health store automatisch verwijderd. Hallo geldt ook wanneer een nieuw exemplaar van Hallo entiteit is gemaakt (bijvoorbeeld een nieuw exemplaar van de service voor stateful persistente-replica is gemaakt). Alle rapporten die zijn gekoppeld aan de oude exemplaar Hallo worden verwijderd en wordt opgeschoond van Hallo store.
> 
> 

Hallo zijn rapporten van system component geïdentificeerd door Hallo bron, die met de Hallo begint '**System.**' voorvoegsel. Watchdogs niet Hallo hetzelfde voorvoegsel voor hun bronnen gebruiken, zoals rapporten met ongeldige parameters worden afgewezen.
Laten we kijken sommige system rapporten toounderstand wat ze activeert en hoe toocorrect Hallo mogelijke problemen staan.

> [!NOTE]
> Service Fabric blijft tooadd rapporten van de voorwaarden van belang ter verbetering van de zichtbaarheid van wat in Hallo-cluster en de toepassing gebeurt er. Bestaande rapporten kunnen ook worden uitgebreid met meer details toohelp Hallo probleem sneller kan oplossen.
> 
> 

## <a name="cluster-system-health-reports"></a>Systeemstatusrapporten cluster
Hallo cluster health entiteit wordt automatisch gemaakt in Hallo health store. Als alles goed werkt, heeft geen system-rapport.

### <a name="neighborhood-loss"></a>Verlies van groep
**System.Federation** meldt fout wanneer er een groep verlies wordt gedetecteerd. Hallo-rapport is van afzonderlijke knooppunten en Hallo knooppunt-ID is opgenomen in de naam van de eigenschap Hallo. Als een groep in de hele Service Fabric-ring Hallo verbroken is, kunt u doorgaans twee gebeurtenissen (beide zijden van Hallo hiaat rapport) verwachten. Als er meer groepen verloren gaan, moet u er meer gebeurtenissen zijn.

Hallo-rapport geeft Hallo globale lease time-out Hallo tijd toolive. Hallo rapport opnieuw verzonden elke helft van de duur van de TTL Hallo voor zolang Hallo voorwaarde actief blijft. Hallo-gebeurtenis wordt automatisch verwijderd wanneer het verloopt. Verwijder wanneer verlopen gedrag zorgt ervoor dat Hallo rapport wordt opgeschoond uit Hallo health store correct, zelfs als Hallo reporting knooppunt niet actief is.

* **SourceId**: System.Federation
* **De eigenschap**: begint met **groep** en bevat knooppuntgegevens
* **Volgende stappen**: onderzoeken waarom Hallo-groep is verbroken (bijvoorbeeld selectievakje Hallo communicatie tussen clusterknooppunten).

## <a name="node-system-health-reports"></a>Systeemstatusrapporten knooppunt
**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, is Hallo-instantie die het beheer van informatie over de clusterknooppunten. Elk knooppunt moet één rapport van System.FM met de status hebben. Hallo knooppunt entiteiten worden verwijderd wanneer de status van knooppunt hello wordt verwijderd (Zie [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Knooppunt omhoog/omlaag
System.FM rapporteert als OK als lid van knooppunt Hallo Hallo ring (dit is actief en werkend). Een fout gemeld wanneer Hallo knooppunt Hallo ring vertrekt (service niet actief is, ofwel voor het upgraden of gewoon omdat deze is mislukt). Hallo health hiërarchie gebouwd door Hallo health store neemt actie geïmplementeerde entiteiten in correlatie met System.FM knooppunt rapporten. Het beschouwt Hallo-knooppunt een bovenliggende virtuele van alle geïmplementeerde entiteiten. Hallo geïmplementeerd entiteiten op dat knooppunt worden query's via als Hallo-knooppunt wordt gerapporteerd als up door System.FM, hello hetzelfde exemplaar als Hallo-exemplaar gekoppeld aan het Hallo-entiteiten. Wanneer System.FM meldt dat Hallo-knooppunt is niet beschikbaar of opnieuw opgestart (een nieuw exemplaar), Hallo health store Hallo geïmplementeerd entiteiten die kunnen bestaan alleen op Hallo omlaag knooppunt of op het vorige exemplaar van knooppunt Hallo Hallo automatisch opgeruimd.

* **SourceId**: System.FM
* **De eigenschap**: status
* **Volgende stappen**: als het Hallo-knooppunt niet actief is voor een upgrade, deze moet terugkeren nadat de upgrade is voltooid. Hallo-status moet in dit geval back tooOK overschakelen. Als Hallo knooppunt niet u terug keert of deze is mislukt, moet Hallo probleem meer onderzoek.

Hallo volgende voorbeeld wordt weergegeven Hallo System.FM gebeurtenis met een status OK voor knooppunt:

```powershell
PS C:\> Get-ServiceFabricNodeHealth  _Node_0

NodeName              : _Node_0
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 8
                        SentAt                : 7/14/2017 4:54:51 PM
                        ReceivedAt            : 7/14/2017 4:55:14 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```


### <a name="certificate-expiration"></a>Vervaldatum van het certificaat
**System.FabricNode** rapporten van een waarschuwing wanneer certificaten worden gebruikt door Hallo-knooppunt bijna is verlopen zijn. Er zijn drie certificaten per knooppunt: **Certificate_cluster**, **Certificate_server**, en **Certificate_default_client**. Wanneer Hallo vervaldatum ten minste twee weken is, is Hallo rapport status in orde. Wanneer Hallo verloopt binnen twee weken is, is het rapporttype Hallo een waarschuwing. TTL van deze gebeurtenissen is oneindig en worden ze verwijderd wanneer een knooppunt Hallo-cluster verlaat.

* **SourceId**: System.FabricNode
* **De eigenschap**: begint met **certificaat** en bevat meer informatie over Hallo certificaattype
* **Volgende stappen**: Hallo certificaten bijwerken als ze bijna is verlopen zijn.

### <a name="load-capacity-violation"></a>Schending van de Load-capaciteit
Hallo Service Fabric Load Balancer rapporten in een waarschuwing wanneer er een schending van de capaciteit knooppunt wordt gedetecteerd.

* **SourceId**: System.PLB
* **De eigenschap**: begint met **capaciteit**
* **Volgende stappen**: selectievakje opgegeven metrische gegevens en bekijkt hello huidige capaciteit op Hallo-knooppunt.

## <a name="application-system-health-reports"></a>Systeemstatusrapporten toepassing
**System.CM**, waarop Hallo Cluster Manager-service vertegenwoordigt, Hallo-instantie die het beheer van informatie over een toepassing is.

### <a name="state"></a>Status
System.CM rapporteert als OK wanneer Hallo-toepassing heeft gemaakt of bijgewerkt. Informeert het Hallo health store wanneer de toepassing hello is verwijderd, zodat het kan worden verwijderd uit de store.

* **SourceId**: System.CM
* **De eigenschap**: status
* **Volgende stappen**: als Hallo-aanvraag is gemaakt of bijgewerkt, moet het Hallo Clusterbeheer statusrapport opnemen. Bekijk anders de status van de toepassing hello Hallo door uitgifte van een query (bijvoorbeeld Hallo PowerShell-cmdlet **Get-ServiceFabricApplication - ApplicationName *applicationName***).

Hallo volgende voorbeeld ziet u Hallo statussen van gebeurtenissen op Hallo **fabric: / WordCount** toepassing:

```powershell
PS C:\> Get-ServiceFabricApplicationHealth fabric:/WordCount -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics

ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Ok
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/14/2017 4:55:10 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
```

## <a name="service-system-health-reports"></a>Systeemstatusrapporten service
**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, Hallo-dienst die informatie over services beheert.

### <a name="state"></a>Status
System.FM rapporteert als OK wanneer Hallo-service is gemaakt. Worden verwijderd Hallo entiteit uit Hallo health store wanneer Hallo-service is verwijderd.

* **SourceId**: System.FM
* **De eigenschap**: status

Hallo volgende voorbeeld ziet u Hallo statussen van gebeurtenissen op Hallo service **fabric: / WordCount/WordCountWebService**:

```powershell
PS C:\> Get-ServiceFabricServiceHealth fabric:/WordCount/WordCountWebService -ExcludeHealthStatistics


ServiceName           : fabric:/WordCount/WordCountWebService
AggregatedHealthState : Ok
PartitionHealthStates : 
                        PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
                        AggregatedHealthState : Ok
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 14
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="service-correlation-error"></a>Fout van de correlatie-service
**System.PLB** meldt fout wanneer er wordt gedetecteerd dat een affiniteitsketen bijwerken van een service toobe gecorreleerd met een andere service maakt. Hallo-rapport wordt gewist wanneer geslaagde update gebeurt.

* **SourceId**: System.PLB
* **De eigenschap**: ServiceDescription
* **Volgende stappen**: selectievakje Hallo gecorreleerde servicebeschrijvingen.

## <a name="partition-system-health-reports"></a>Systeemstatusrapporten partitie
**System.FM**, waarop Hallo Failover Manager service vertegenwoordigt, Hallo-dienst die informatie over servicepartities beheert.

### <a name="state"></a>Status
System.FM rapporteert als OK wanneer Hallo partitie is gemaakt en is in orde. Worden verwijderd Hallo entiteit uit Hallo health store wanneer Hallo partitie wordt verwijderd.

Als het Hallo-partitie is lager dan het Hallo minimale replica aantal, is een fout rapporteert. Als Hallo partitie niet lager dan het aantal van Hallo minimale replica is, maar het is lager dan het Hallo doel replica aantal, wordt een waarschuwing. Als Hallo partitie is sprake van quorumverlies, rapporteert System.FM een fout opgetreden.

Andere belangrijke gebeurtenissen bevatten een waarschuwing wanneer Hallo herconfiguratie langer duurt dan verwacht en wanneer Hallo build langer duurt dan verwacht. Hallo verwacht tijden voor Hallo build en herconfiguratie worden geconfigureerd op basis van de service-scenario's. Bijvoorbeeld, als een service een terabyte van status, zoals SQL-Database heeft, duurt Hallo build langer dan voor een service met een kleine hoeveelheid staat.

* **SourceId**: System.FM
* **De eigenschap**: status
* **Volgende stappen**: als het Hallo-status is niet OK, is het mogelijk dat sommige replica's niet gemaakt, is geopend of gepromoveerde tooprimary of secundaire correct is. In veel gevallen is de hoofdoorzaak Hallo een service-fout in Hallo open of implementatie van rol wijzigen.

Hallo volgende voorbeeld ziet u een partitie in orde:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountWebService | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics -ReplicasFilter None

PartitionId           : 8bbcd03a-3a53-47ec-a5f1-9b77f73c53b2
AggregatedHealthState : Ok
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 70
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/14/2017 4:55:10 PM
                        TTL                   : Infinite
                        Description           : Partition is healthy.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hallo ziet volgende voorbeeld Hallo status van een partitie die lager is dan het aantal doel-replica's. de volgende stap Hallo is tooget Hallo Partitiebeschrijving, waarin configuratie: **MinReplicaSetSize** is drie en **TargetReplicaSetSize** zeven. Vervolgens Hallo aantal knooppunten in cluster Hallo ophalen: vijf. Dus in dit geval kunnen niet twee replica's worden geplaatst, omdat Hallo doelaantal replica's hoger dan het aantal knooppunten beschikbaar Hallo is.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None -ExcludeHealthStatistics


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 123
                        SentAt                : 7/14/2017 4:55:39 PM
                        ReceivedAt            : 7/14/2017 4:55:44 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/S RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/P RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:55:44 PM, LastOk = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131445250939703027
                        SentAt                : 7/14/2017 4:58:13 PM
                        ReceivedAt            : 7/14/2017 4:58:14 PM
                        TTL                   : 00:01:05
                        Description           : hello Load Balancer was unable toofind a placement for one or more of hello Service's Replicas:
                        Secondary replica could not be placed due toohello following constraints and properties:  
                        TargetReplicaSetSize: 7
                        Placement Constraint: N/A
                        Parent Service: N/A
                        
                        Constraint Elimination Sequence:
                        Existing Secondary Replicas eliminated 4 possible node(s) for placement -- 1/5 node(s) remain.
                        Existing Primary Replica eliminated 1 possible node(s) for placement -- 0/5 node(s) remain.
                        
                        Nodes Eliminated By Constraints:
                        
                        Existing Secondary Replicas -- Nodes with Partition's Existing Secondary Replicas/Instances:
                        --
                        FaultDomain:fd:/4 NodeName:_Node_4 NodeType:NodeType4 UpgradeDomain:4 UpgradeDomain: ud:/4 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/3 NodeName:_Node_3 NodeType:NodeType3 UpgradeDomain:3 UpgradeDomain: ud:/3 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/14/2017 4:56:14 PM, LastOk = 1/1/0001 12:00:00 AM

PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | select MinReplicaSetSize,TargetReplicaSetSize

MinReplicaSetSize TargetReplicaSetSize
----------------- --------------------
                2                    7                        

PS C:\> @(Get-ServiceFabricNode).Count
5
```

### <a name="replica-constraint-violation"></a>Replica-Beperkingsfout
**System.PLB** rapporteert een waarschuwing als het een overtreding van een replica wordt gedetecteerd en alle replica's van partitie kan niet worden geplaatst. Hallo rapportdetails weergeven welke beperkingen en eigenschappen Hallo replica plaatsing voorkomen.

* **SourceId**: System.PLB
* **De eigenschap**: begint met **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Systeemstatusrapporten replica
**System.RA**, die staat voor onderdeel van het Hallo reconfiguration agent Hallo autoriteit voor Hallo replica de status is.

### <a name="state"></a>Status
**System.RA** OK rapporten wanneer Hallo replica is gemaakt.

* **SourceId**: System.RA
* **De eigenschap**: status

Hallo volgende voorbeeld ziet u een replica in orde:

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422293118721
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131445248920273536
                        SentAt                : 7/14/2017 4:54:52 PM
                        ReceivedAt            : 7/14/2017 4:55:13 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_0
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/14/2017 4:55:13 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="replica-open-status"></a>Open status van replica
Hallo beschrijving van dit statusrapport bevat Hallo begintijd (Coordinated Universal Time) wanneer Hallo API-aanroep is aangeroepen.

**System.RA** rapporteert een waarschuwing als Hallo replica open langer dan de periode Hallo geconfigureerd duurt (standaard: 30 minuten). Als Hallo API heeft impact op de beschikbaarheid van de service, uitgegeven Hallo rapport is veel sneller (een configureerbare interval, met een standaard 30 seconden). Hallo-tijd gemeten omvat Hallo gebruikte tijd voor Hallo replicator openen en Hallo service openen. Hallo eigenschap wijzigingen tooOK als Hallo geopend is voltooid.

* **SourceId**: System.RA
* **De eigenschap**: **ReplicaOpenStatus**
* **Volgende stappen**: als het Hallo-status is niet OK, onderzoeken waarom Hallo replica open duurt langer dan verwacht.

### <a name="slow-service-api-call"></a>Trage service API-aanroep
**System.RAP** en **System.Replicator** rapporteren van een waarschuwing als een aanroep toohello gebruikerscode service langer dan de tijd Hallo geconfigureerd duurt. Hallo-waarschuwing wordt gewist wanneer het Hallo-aanroep is voltooid.

* **SourceId**: System.RAP of System.Replicator
* **De eigenschap**: Hallo-naam van trage Hallo-API. Hallo beschrijving biedt meer informatie over Hallo tijd Hallo API is in behandeling.
* **Volgende stappen**: onderzoeken waarom Hallo aanroep duurt langer dan verwacht.

Hallo volgende voorbeeld ziet u een partitie in quorumverlies en toofigure van Hallo onderzoek stappen uitgevoerd om de oorzaak. Een van de replica's Hallo heeft een waarschuwingsstatus zodat u beschikt over de status. Er wordt weergegeven dat de servicebewerking Hallo langer duurt dan verwacht, een gebeurtenis die is gerapporteerd door System.RAP. Nadat deze informatie is ontvangen, wordt de volgende stap Hallo toolook op Hallo servicecode is en er onderzoeken. Voor deze aanvraag Hallo **RunAsync** implementatie van de stateful service Hallo genereert een onverwerkte uitzondering. Hallo replica's zijn recyclen, zodat alle replica's in de waarschuwingsstatus Hallo mogelijk niet weergegeven. U kunt ophalen Hallo-status opnieuw en zoek naar eventuele verschillen in Hallo replica-ID. In bepaalde gevallen krijgt Hallo pogingen u aanwijzingen.

```powershell
PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful | Get-ServiceFabricPartitionHealth -ExcludeHealthStatistics

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
AggregatedHealthState : Error
UnhealthyEvaluations  :
                        Error event: SourceId='System.FM', Property='State'.

ReplicaHealthStates   :
                        ReplicaId             : 130743748372546446
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746168084332
                        AggregatedHealthState : Ok

                        ReplicaId             : 130743746195428808
                        AggregatedHealthState : Warning

                        ReplicaId             : 130743746195428807
                        AggregatedHealthState : Ok

HealthEvents          :
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Error
                        SequenceNumber        : 182
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:31 PM
                        TTL                   : Infinite
                        Description           : Partition is in quorum loss.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 4/24/2015 6:51:31 PM

PS C:\> Get-ServiceFabricPartition fabric:/HelloWorldStatefulApplication/HelloWorldStateful

PartitionId            : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
PartitionKind          : Int64Range
PartitionLowKey        : -9223372036854775808
PartitionHighKey       : 9223372036854775807
PartitionStatus        : InQuorumLoss
LastQuorumLossDuration : 00:00:13
MinReplicaSetSize      : 3
TargetReplicaSetSize   : 3
HealthState            : Error
DataLossNumber         : 130743746152927699
ConfigurationNumber    : 227633266688

PS C:\> Get-ServiceFabricReplica 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

ReplicaId           : 130743746195428808
ReplicaAddress      : PartitionId: 72a0fb3e-53ec-44f2-9983-2f272aca3e38, ReplicaId: 130743746195428808
ReplicaRole         : Primary
NodeName            : Node.3
ReplicaStatus       : Ready
LastInBuildDuration : 00:00:01
HealthState         : Warning

PS C:\> Get-ServiceFabricReplicaHealth 72a0fb3e-53ec-44f2-9983-2f272aca3e38 130743746195428808

PartitionId           : 72a0fb3e-53ec-44f2-9983-2f272aca3e38
ReplicaId             : 130743746195428808
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.RAP', Property='ServiceOpenOperationDuration', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 130743756170185892
                        SentAt                : 4/24/2015 7:00:17 PM
                        ReceivedAt            : 4/24/2015 7:00:33 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Ok = 4/24/2015 7:00:33 PM

                        SourceId              : System.RAP
                        Property              : ServiceOpenOperationDuration
                        HealthState           : Warning
                        SequenceNumber        : 130743756399407044
                        SentAt                : 4/24/2015 7:00:39 PM
                        ReceivedAt            : 4/24/2015 7:00:59 PM
                        TTL                   : Infinite
                        Description           : Start Time (UTC): 2015-04-24 19:00:17.019
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : ->Warning = 4/24/2015 7:00:59 PM
```

Wanneer u Hallo defecte toepassing onder Hallo foutopsporingsprogramma start, tonen Hallo diagnostische gebeurtenissen van windows hello uitzondering van RunAsync:

![Visual Studio 2015 diagnostische gebeurtenissen: RunAsync-fout in de fabric: / HelloWorldStatefulApplication.][1]

Visual Studio 2015 diagnostische gebeurtenissen: fout in RunAsync **fabric: / HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Volledige replicatiewachtrij
**System.Replicator** rapporten van een waarschuwing wanneer de replicatiewachtrij Hallo vol is. Op primaire Hallo raakt wachtrij voor replicatie staan doorgaans vol omdat een of meer secundaire replica's langzaam tooacknowledge bewerkingen zijn. Op Hallo secundaire, dit gebeurt meestal wanneer Hallo-service langzaam tooapply Hallo bewerkingen is. Hallo-waarschuwing wordt gewist wanneer Hallo wachtrij vol is.

* **SourceId**: System.Replicator
* **De eigenschap**: **PrimaryReplicationQueueStatus** of **SecondaryReplicationQueueStatus**, afhankelijk van de replicarol Hallo

### <a name="slow-naming-operations"></a>Trage Naming bewerkingen
**System.NamingService** rapporteert de status op de primaire replica wanneer u een naam geven bewerking duurt langer dan de aanvaardbare. Voorbeelden van Naming bewerkingen zijn [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) of [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Meer methoden kunnen u vinden onder FabricClient, bijvoorbeeld onder [service beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) of [eigenschap beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> Hallo Naming service namen tooa servicelocatie in Hallo-cluster wordt omgezet en kan gebruikers toomanage servicenamen en eigenschappen. Het is een Service Fabric gepartitioneerd persistent service. Een van de partities Hallo vertegenwoordigt Hallo Authority Owner, die de metagegevens over alle Service Fabric-namen en -services bevat. Hallo Service Fabric-namen zijn toegewezen toodifferent partities, genaamd Name Owner partities, zodat het Hallo-service kan worden uitgebreid. Lees meer over [Naming service](service-fabric-architecture.md).
> 
> 

Wanneer een Naming bewerking langer duurt dan verwacht, Hallo-bewerking is gemarkeerd met een rapport van de waarschuwing op Hallo *primaire replica van Hallo Naming service partitie die fungeert Hallo bewerking*. Als het Hallo-bewerking is voltooid, Hallo waarschuwing is uitgeschakeld. Als het Hallo-bewerking is voltooid met een fout, Hallo health rapport bevat details over Hallo-fout.

* **SourceId**: System.NamingService
* **De eigenschap**: begint met het voorvoegsel **Duration_** en identificeert Hallo langzame werking en Hallo Service Fabric-naam op welke Hallo bewerking wordt toegepast. Bijvoorbeeld, als service maken op de naam van fabric: / MyApp/MijnService is te lang duurt, Hallo eigenschap Duration_AOCreateService.fabric:/MyApp/MyService. AO punten toohello rol Hallo Naming partitie voor deze naam en het opnieuw.
* **Volgende stappen**: selectievakje waarom Hallo Naming-bewerking is mislukt. Elke bewerking kan verschillende oorzaken hebben. Bijvoorbeeld verwijderen service kan blijven steken op een knooppunt omdat Hallo toepassingshost houdt op een knooppunt vanwege tooa gebruiker fout in de servicecode Hallo gecrasht.

Hallo volgende voorbeeld toont een servicebewerking maken. Hallo bewerking duurt langer dan de duur Hallo geconfigureerd. AO pogingen en werk tooNO verzendt. Er is geen voltooide Hallo laatste bewerking met time-out. In dit geval is hello dezelfde replica de primaire voor Hallo AO en er zijn geen rollen.

```powershell
PartitionId           : 00000000-0000-0000-0000-000000001000
ReplicaId             : 131064359253133577
AggregatedHealthState : Warning
UnhealthyEvaluations  :
                        Unhealthy event: SourceId='System.NamingService', Property='Duration_AOCreateService.fabric:/MyApp/MyService', HealthState='Warning', ConsiderWarningAsError=false.

HealthEvents          :
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131064359308715535
                        SentAt                : 4/29/2016 8:38:50 PM
                        ReceivedAt            : 4/29/2016 8:39:08 PM
                        TTL                   : Infinite
                        Description           : Replica has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 4/29/2016 8:39:08 PM, LastWarning = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_AOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064359526778775
                        SentAt                : 4/29/2016 8:39:12 PM
                        ReceivedAt            : 4/29/2016 8:39:38 PM
                        TTL                   : 00:05:00
                        Description           : hello AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM

                        SourceId              : System.NamingService
                        Property              : Duration_NOCreateService.fabric:/MyApp/MyService
                        HealthState           : Warning
                        SequenceNumber        : 131064360657607311
                        SentAt                : 4/29/2016 8:41:05 PM
                        ReceivedAt            : 4/29/2016 8:41:08 PM
                        TTL                   : 00:00:15
                        Description           : hello NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Systeemstatusrapporten DeployedApplication
**System.Hosting** Hallo-instantie op geïmplementeerde entiteiten is.

### <a name="activation"></a>activering
System.Hosting rapporteert als OK als u een toepassing is geactiveerd op Hallo-knooppunt. Anders wordt een fout opgetreden.

* **SourceId**: System.Hosting
* **De eigenschap**: activering, waaronder Hallo implementatie versie
* **Volgende stappen**: als de toepassing hello niet in orde is, onderzoekt waarom Hallo-activering is mislukt.

Hallo toont volgende voorbeeld geslaagde activering:

```powershell
PS C:\> Get-ServiceFabricDeployedApplicationHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ExcludeHealthStatistics

ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_1
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_1
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131445249083836329
                                     SentAt                : 7/14/2017 4:55:08 PM
                                     ReceivedAt            : 7/14/2017 4:55:14 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Downloaden
**System.Hosting** een fout gemeld als het pakket downloaden van Hallo toepassing mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**:  **downloaden:*RolloutVersion***
* **Volgende stappen**: onderzoeken waarom Hallo downloaden is mislukt op Hallo-knooppunt.

## <a name="deployedservicepackage-system-health-reports"></a>Systeemstatusrapporten DeployedServicePackage
**System.Hosting** Hallo-instantie op geïmplementeerde entiteiten is.

### <a name="service-package-activation"></a>Het activeren van service
System.Hosting rapporteert als OK als Hallo service pakket activering op Hallo-knooppunt geslaagd is. Anders wordt een fout opgetreden.

* **SourceId**: System.Hosting
* **De eigenschap**: activering
* **Volgende stappen**: onderzoeken waarom Hallo-activering is mislukt.

### <a name="code-package-activation"></a>Pakket-codeactivering
**System.Hosting** rapporteert als OK voor elk codepakket als Hallo-activering geslaagd is. Als Hallo activering mislukt, wordt een waarschuwing zoals geconfigureerd. Als **CodePackage** tooactivate mislukt of eindigt met een fout die groter zijn dan Hallo geconfigureerd **CodePackageHealthErrorThreshold**, die als host fungeert een fout gemeld. Als een servicepakket meerdere code pakketten bevat, wordt een rapport activering gegenereerd voor elk criterium.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van Hallo voorvoegsel **CodePackageActivation** en bevat Hallo-naam van codepakket hello en Hallo toegangspunt als  **CodePackageActivation:* CodePackageName*:*entrypoint/EntryPoint*** (bijvoorbeeld **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Service type is geregistreerd
**System.Hosting** rapporteert als OK als Hallo servicetype is geregistreerd. Een fout gemeld. Als het Hallo-registratie is niet uitgevoerd in de tijd (zoals deze is geconfigureerd met behulp van **ServiceTypeRegistrationTimeout**). Als Hallo runtime is gesloten, Hallo servicetype is registratie van het Hallo-knooppunt en Hosting rapporteert een waarschuwing.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van Hallo voorvoegsel **ServiceTypeRegistration** en bevat de servicenaam type Hallo (bijvoorbeeld **ServiceTypeRegistration:FileStoreServiceType**)

Hallo volgende voorbeeld ziet u een gezonde geïmplementeerd servicepakket:

```powershell
PS C:\> Get-ServiceFabricDeployedServicePackageHealth -NodeName _Node_1 -ApplicationName fabric:/WordCount -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_1
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131445249084026346
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131445249084306362
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131445249088096842
                             SentAt                : 7/14/2017 4:55:08 PM
                             ReceivedAt            : 7/14/2017 4:55:14 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Downloaden
**System.Hosting** een fout gemeld als het pakket downloaden van Hallo service mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**:  **downloaden:*RolloutVersion***
* **Volgende stappen**: onderzoeken waarom Hallo downloaden is mislukt op Hallo-knooppunt.

### <a name="upgrade-validation"></a>Validatie van upgrade
**System.Hosting** meldt een fout als validatie tijdens Hallo upgrade mislukt of als hello upgrade op Hallo-knooppunt mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van Hallo voorvoegsel **FabricUpgradeValidation** en bevat Hallo upgrade-versie
* **Beschrijving**: verwijst toohello-fout opgetreden

## <a name="next-steps"></a>Volgende stappen
[Service Fabric-statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md)

[Hoe tooreport en controleer health service](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Controle en diagnose van lokaal services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

