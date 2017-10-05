---
title: Problemen oplossen met systeemstatusrapporten | Microsoft Docs
description: Hierin wordt beschreven in de statusrapporten dat is verzonden door Azure Service Fabric-onderdelen en hun gebruik voor het oplossen van problemen cluster of problemen met de toepassing.
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
ms.openlocfilehash: 54e20146b2f1e0ca6153b66319be70c6f7c2fb59
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-system-health-reports-to-troubleshoot"></a>Systeemstatusrapporten gebruiken om fouten op te lossen
Azure Service Fabric-onderdelen rapport gebruiksklaar op alle entiteiten in het cluster. De [health store](service-fabric-health-introduction.md#health-store) maken en verwijderen van de entiteiten die zijn gebaseerd op systeemrapporten van het. Ook ordent ze in een hiërarchie die entiteit interacties worden vastgelegd.

> [!NOTE]
> Om te begrijpen health-gerelateerde begrippen, leest u meer op [Service Fabric-statusmodel](service-fabric-health-introduction.md).
> 
> 

Systeemstatusrapporten bieden inzicht in het cluster en de functionaliteit van de toepassing en de vlag problemen via health. Voor toepassingen en services controleren systeemstatusrapporten of entiteiten worden geïmplementeerd en correct vanuit het perspectief van de Service Fabric werkt zijn. De rapporten bieden een statuscontrole van de zakelijke logica van de service of detectie van vastgelopen processen. Services van de gebruiker kunnen de health-gegevens met informatie die specifiek zijn voor hun logica aanvullen.

> [!NOTE]
> Statusrapporten watchdogs zijn alleen zichtbaar *nadat* Maak een entiteit van de onderdelen van het systeem. Wanneer een entiteit wordt verwijderd, worden alle statusrapporten gekoppeld in de health store automatisch verwijderd. Geldt ook wanneer een nieuw exemplaar van de entiteit is gemaakt (bijvoorbeeld een nieuw exemplaar van de service voor stateful persistente-replica is gemaakt). Alle rapporten die zijn gekoppeld aan het oude exemplaar worden verwijderd en opgeschoond vanuit de store.
> 
> 

Het systeemonderdeel rapporten zijn geïdentificeerd door de bron die met begint de '**System.**' voorvoegsel. Watchdogs niet hetzelfde voorvoegsel gebruiken voor hun bronnen, zoals rapporten met ongeldige parameters worden afgewezen.
Bekijken we enkele systeemrapporten om te begrijpen wat ze activeert en hoe u de mogelijke problemen die ze vertegenwoordigen te corrigeren.

> [!NOTE]
> Service Fabric blijft rapporten van de voorwaarden van belang ter verbetering van de zichtbaarheid van wat in het cluster en de toepassing gebeurt er toevoegen. Bestaande rapporten kunnen ook worden uitgebreid met meer details bij het oplossen van het probleem sneller.
> 
> 

## <a name="cluster-system-health-reports"></a>Systeemstatusrapporten cluster
De entiteit van de health cluster wordt automatisch gemaakt in de health store. Als alles goed werkt, heeft geen system-rapport.

### <a name="neighborhood-loss"></a>Verlies van groep
**System.Federation** meldt fout wanneer er een groep verlies wordt gedetecteerd. Het rapport is van afzonderlijke knooppunten en de knooppunt-ID is opgenomen in de eigenschapsnaam. Als een groep in de hele Service Fabric-ring verbroken is, kunt u doorgaans twee gebeurtenissen (beide zijden van het rapport gap) verwachten. Als er meer groepen verloren gaan, moet u er meer gebeurtenissen zijn.

Het rapport geeft de algemene lease time-out als time to live. Het rapport opnieuw elke helft van de duur van de TTL voor verzonden als de voorwaarde actief blijft. De gebeurtenis wordt automatisch verwijderd wanneer het verloopt. Verwijder wanneer verlopen gedrag zorgt ervoor dat het rapport wordt opgeschoond van de health store correct, zelfs als het reporting knooppunt niet actief is.

* **SourceId**: System.Federation
* **De eigenschap**: begint met **groep** en bevat knooppuntgegevens
* **Volgende stappen**: onderzoeken waarom de groep wordt verbroken (bijvoorbeeld de communicatie tussen clusterknooppunten controleren).

## <a name="node-system-health-reports"></a>Systeemstatusrapporten knooppunt
**System.FM**, die staat voor de Failover Manager service, wordt de instantie die het beheer van informatie over de clusterknooppunten. Elk knooppunt moet één rapport van System.FM met de status hebben. De knooppunt-entiteiten worden verwijderd wanneer de knooppuntstatus wordt verwijderd (Zie [RemoveNodeStateAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.clustermanagementclient.removenodestateasync)).

### <a name="node-updown"></a>Knooppunt omhoog/omlaag
System.FM rapporteert als OK als lid van het knooppunt de ring (dit is actief en werkend). Een fout gemeld wanneer het knooppunt de ring vertrekt (service niet actief is, ofwel voor het upgraden of gewoon omdat deze is mislukt). De health-hiërarchie gebouwd door de health store neemt actie geïmplementeerde entiteiten in correlatie met System.FM knooppunt rapporten. Er vanuit het knooppunt een bovenliggende virtuele van alle geïmplementeerde entiteiten. De geïmplementeerde entiteiten op dat knooppunt worden weergegeven via query's of het knooppunt als bedrijfs is gemeld door System.FM met hetzelfde exemplaar als de instantie die is gekoppeld aan de entiteiten. Wanneer System.FM meldt dat het knooppunt niet beschikbaar is of opnieuw opgestart (een nieuw exemplaar), de health store de geïmplementeerde entiteiten die kunnen bestaan alleen op het knooppunt omlaag of op het vorige exemplaar van het knooppunt automatisch opgeruimd.

* **SourceId**: System.FM
* **De eigenschap**: status
* **Volgende stappen**: als het knooppunt niet actief voor een upgrade is, deze moet terugkeren nadat de upgrade is voltooid. In dit geval wordt moet de status overschakelen naar OK. Als het knooppunt niet u terug keert of deze is mislukt, moet het probleem meer onderzoek.

Het volgende voorbeeld ziet de gebeurtenis System.FM met een status OK voor knooppunt:

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
**System.FabricNode** rapporten van een waarschuwing wanneer certificaten worden gebruikt door het knooppunt bijna is verlopen zijn. Er zijn drie certificaten per knooppunt: **Certificate_cluster**, **Certificate_server**, en **Certificate_default_client**. Wanneer de vervaldatum ten minste twee weken is, is de status van het rapport OK. Wanneer de vervaldatum binnen twee weken is, is het rapporttype dat een waarschuwing. TTL van deze gebeurtenissen is oneindig, en ze worden verwijderd wanneer een knooppunt de cluster verlaat.

* **SourceId**: System.FabricNode
* **De eigenschap**: begint met **certificaat** en bevat meer informatie over het certificaattype
* **Volgende stappen**: bijwerken van de certificaten als ze bijna is verlopen zijn.

### <a name="load-capacity-violation"></a>Schending van de Load-capaciteit
De Service Fabric Load Balancer rapporten in een waarschuwing wanneer er een schending van de capaciteit knooppunt wordt gedetecteerd.

* **SourceId**: System.PLB
* **De eigenschap**: begint met **capaciteit**
* **Volgende stappen**: Controleer of de opgegeven metrische gegevens en de huidige capaciteit op het knooppunt.

## <a name="application-system-health-reports"></a>Systeemstatusrapporten toepassing
**System.CM**, die staat voor de Cluster Manager-service, wordt de instantie van die gegevens over een toepassing beheert.

### <a name="state"></a>Status
System.CM rapporteert als OK wanneer de toepassing heeft gemaakt of bijgewerkt. Informeert de health store wanneer de toepassing is verwijderd, zodat het kan worden verwijderd uit de store.

* **SourceId**: System.CM
* **De eigenschap**: status
* **Volgende stappen**: als de toepassing is gemaakt of bijgewerkt, moet deze het statusrapport Clusterbeheer opnemen. Bekijk anders de status van de toepassing door uitgifte van een query (bijvoorbeeld de PowerShell-cmdlet **Get-ServiceFabricApplication - ApplicationName *applicationName***).

Het volgende voorbeeld ziet u de gebeurtenis status op de **fabric: / WordCount** toepassing:

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
**System.FM**, die staat voor de service Failover Manager is de instantie die informatie over services beheert.

### <a name="state"></a>Status
System.FM rapporteert als OK wanneer de service is gemaakt. Worden verwijderd de entiteit van de health store wanneer de service is verwijderd.

* **SourceId**: System.FM
* **De eigenschap**: status

Het volgende voorbeeld ziet u de gebeurtenis status van de service **fabric: / WordCount/WordCountWebService**:

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
**System.PLB** meldt fout wanneer er wordt gedetecteerd dat een affiniteitsketen bijwerken van een service worden gecorreleerd met een andere service maakt. Het rapport wordt gewist wanneer geslaagde update gebeurt.

* **SourceId**: System.PLB
* **De eigenschap**: ServiceDescription
* **Volgende stappen**: Controleer de servicebeschrijvingen van gecorreleerde.

## <a name="partition-system-health-reports"></a>Systeemstatusrapporten partitie
**System.FM**, die staat voor de service Failover Manager is de instantie die informatie over servicepartities beheert.

### <a name="state"></a>Status
System.FM rapporteert als OK wanneer de partitie is gemaakt en is in orde. Worden verwijderd de entiteit van de health store wanneer de partitie wordt verwijderd.

Als de partitie lager dan het aantal minimale replica is, is een fout rapporteert. Als de partitie niet lager dan het aantal minimale replica is, maar dit lager dan het aantal replica's van doel is, wordt een waarschuwing. Als de partitie is sprake van quorumverlies, rapporteert System.FM een fout opgetreden.

Andere belangrijke gebeurtenissen bevatten een waarschuwing wanneer de herconfiguratie langer duurt dan verwacht en wanneer de build langer duurt dan verwacht. De verwachte tijden voor de build en herconfiguratie geconfigureerd worden op basis van de service-scenario's. Bijvoorbeeld, als een service een terabyte van status, zoals SQL-Database heeft, duurt de build langer dan voor een service met een kleine hoeveelheid staat.

* **SourceId**: System.FM
* **De eigenschap**: status
* **Volgende stappen**: als de status niet OK is, is het mogelijk dat sommige replica's niet zijn gemaakt, geopend, of juist gepromoveerd tot primaire of secundaire site. In veel gevallen is de hoofdoorzaak een service-fout in de implementatie open of rol wijzigen.

Het volgende voorbeeld ziet u een partitie in orde:

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

Het volgende voorbeeld toont de status van een partitie die lager is dan het aantal doel-replica's. De volgende stap is om op te halen van de Partitiebeschrijving, waarin configuratie: **MinReplicaSetSize** is drie en **TargetReplicaSetSize** zeven. Haal vervolgens het aantal knooppunten in het cluster: vijf. Dus in dit geval kunnen niet twee replica's worden geplaatst, omdat het doelaantal replica's hoger dan het aantal knooppunten beschikbaar is.

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
                        Description           : The Load Balancer was unable to find a placement for one or more of the Service's Replicas:
                        Secondary replica could not be placed due to the following constraints and properties:  
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
**System.PLB** rapporteert een waarschuwing als het een overtreding van een replica wordt gedetecteerd en alle replica's van partitie kan niet worden geplaatst. Details van het rapport weergeven welke beperkingen en eigenschappen te voorkomen dat de replica-plaatsing.

* **SourceId**: System.PLB
* **De eigenschap**: begint met **ReplicaConstraintViolation**

## <a name="replica-system-health-reports"></a>Systeemstatusrapporten replica
**System.RA**, die staat voor het onderdeel reconfiguration agent is de instantie voor de replicastatus van de.

### <a name="state"></a>Status
**System.RA** OK rapporten wanneer de replica is gemaakt.

* **SourceId**: System.RA
* **De eigenschap**: status

Het volgende voorbeeld ziet u een replica in orde:

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
De beschrijving van dit statusrapport bevat de begintijd (Coordinated Universal Time) toen de API-aanroep werd aangeroepen.

**System.RA** rapporten van een waarschuwing als de replica open langer dan de geconfigureerde periode duurt (standaard: 30 minuten). Als de API heeft impact op de beschikbaarheid van de service, wordt het rapport is veel sneller uitgegeven (een configureerbare interval, met een standaard 30 seconden). De tijd gemeten bevat de benodigde tijd voor de replicator-openen en het openen van de service. De eigenschap wordt gewijzigd op OK als u de open is voltooid.

* **SourceId**: System.RA
* **De eigenschap**: **ReplicaOpenStatus**
* **Volgende stappen**: als de status niet OK is, onderzoekt waarom de geopende replica duurt langer dan verwacht.

### <a name="slow-service-api-call"></a>Trage service API-aanroep
**System.RAP** en **System.Replicator** rapporteren van een waarschuwing als een aanroep van de code van de gebruiker langer dan de geconfigureerde tijd duurt. De waarschuwing wordt gewist wanneer de aanroep is voltooid.

* **SourceId**: System.RAP of System.Replicator
* **De eigenschap**: de naam van de langzaam API. De beschrijving biedt meer informatie over de tijd die de API in behandeling is.
* **Volgende stappen**: onderzoeken waarom de aanroep duurt langer dan verwacht.

Het volgende voorbeeld ziet een partitie in quorumverlies en de onderzoek stappen om erachter te komen waarom gedaan. Een van de replica's heeft een waarschuwingsstatus zodat u de status downloaden. Er wordt weergegeven dat de servicebewerking langer duurt dan verwacht, een gebeurtenis die is gerapporteerd door System.RAP. Nadat deze informatie is ontvangen, wordt de volgende stap is om te kijken naar de code en er onderzoeken. Voor deze aanvraag de **RunAsync** implementatie van de stateful service genereert een onverwerkte uitzondering. De replica's zijn recyclen, zodat alle replica's in de waarschuwingsstatus mogelijk niet weergegeven. U kunt proberen het ophalen van de status en zoekt u naar eventuele verschillen in de replica-ID. In bepaalde gevallen, kunnen de nieuwe pogingen geven u aanwijzingen.

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

Wanneer u de defecte toepassing onder het foutopsporingsprogramma start, geven de diagnostische gebeurtenissen van windows de uitzondering gegenereerd vanuit RunAsync:

![Visual Studio 2015 diagnostische gebeurtenissen: RunAsync-fout in de fabric: / HelloWorldStatefulApplication.][1]

Visual Studio 2015 diagnostische gebeurtenissen: fout in RunAsync **fabric: / HelloWorldStatefulApplication**.

[1]: ./media/service-fabric-understand-and-troubleshoot-with-system-health-reports/servicefabric-health-vs-runasync-exception.png


### <a name="replication-queue-full"></a>Volledige replicatiewachtrij
**System.Replicator** rapporten van een waarschuwing wanneer de replicatiewachtrij vol is. Op de primaire raakt wachtrij voor replicatie staan doorgaans vol omdat een of meer secundaire replica's zijn trage operations bevestigen. Op de secundaire, dit gebeurt meestal wanneer de service langzaam is worden de bewerkingen toepassen. De waarschuwing wordt gewist wanneer de wachtrij vol is.

* **SourceId**: System.Replicator
* **De eigenschap**: **PrimaryReplicationQueueStatus** of **SecondaryReplicationQueueStatus**, afhankelijk van de replicarol

### <a name="slow-naming-operations"></a>Trage Naming bewerkingen
**System.NamingService** rapporteert de status op de primaire replica wanneer u een naam geven bewerking duurt langer dan de aanvaardbare. Voorbeelden van Naming bewerkingen zijn [CreateServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync) of [DeleteServiceAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.deleteserviceasync). Meer methoden kunnen u vinden onder FabricClient, bijvoorbeeld onder [service beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient) of [eigenschap beheermethoden](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.propertymanagementclient).

> [!NOTE]
> De service Naming servicenamen worden omgezet in een locatie in het cluster en kan gebruikers beheren servicenamen en eigenschappen. Het is een Service Fabric gepartitioneerd persistent service. Een van de partities vertegenwoordigt een eigenaar van de instantie die de metagegevens over alle Service Fabric-namen en -services bevat. De Service Fabric-namen worden toegewezen aan verschillende partities, genaamd Name Owner partities, zodat de service kan uitgebreid worden. Lees meer over [Naming service](service-fabric-architecture.md).
> 
> 

Wanneer een Naming bewerking langer duurt dan verwacht, de bewerking is gemarkeerd met een rapport waarschuwing op het *primaire replica van de Naming service partitie die de bewerking fungeert*. Als de bewerking voltooid is, wordt de waarschuwing is uitgeschakeld. Als de bewerking is voltooid met een fout, bevat het statusrapport meer informatie over de fout.

* **SourceId**: System.NamingService
* **De eigenschap**: begint met het voorvoegsel **Duration_** en identificeert de trage bewerking en de Service Fabric-naam waarop de bewerking wordt toegepast. Bijvoorbeeld, als service maken op de naam van fabric: / MyApp/MijnService is te lang duurt, is de eigenschap Duration_AOCreateService.fabric:/MyApp/MyService. AO verwijst naar de rol van de partitie Naming voor deze naam en het opnieuw.
* **Volgende stappen**: selectievakje waarom de Naming-bewerking is mislukt. Elke bewerking kan verschillende oorzaken hebben. Bijvoorbeeld verwijderen service kan blijven steken op een knooppunt omdat toepassingshost op een knooppunt als gevolg van een gebruiker fout in de servicecode vastlopen houdt.

Het volgende voorbeeld ziet een servicebewerking maken. De bewerking duurt langer dan de geconfigureerde duur. AO pogingen en werk verzendt op Nee. NIET de laatste bewerking met time-out voltooid. In dit geval is de dezelfde replica primaire voor zowel de AO en er zijn geen rollen.

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
                        Description           : The AOCreateService started at 2016-04-29 20:39:08.677 is taking longer than 30.000.
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
                        Description           : The NOCreateService started at 2016-04-29 20:39:08.689 completed with FABRIC_E_TIMEOUT in more than 30.000.
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 4/29/2016 8:39:38 PM, LastOk = 1/1/0001 12:00:00 AM
```

## <a name="deployedapplication-system-health-reports"></a>Systeemstatusrapporten DeployedApplication
**System.Hosting** is de instantie voor geïmplementeerde entiteiten.

### <a name="activation"></a>activering
System.Hosting rapporteert als OK als u een toepassing is geactiveerd op het knooppunt. Anders wordt een fout opgetreden.

* **SourceId**: System.Hosting
* **De eigenschap**: activering, waaronder de implementatie-versie
* **Volgende stappen**: als de toepassing niet in orde is, moet u onderzoeken waarom de activering is mislukt.

Het volgende voorbeeld ziet u geslaagde activering:

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
                                     Description           : The application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Downloaden
**System.Hosting** een fout gemeld als het pakket downloaden van de toepassing is mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**:  **downloaden:*RolloutVersion***
* **Volgende stappen**: onderzoeken waarom het downloaden is mislukt op het knooppunt.

## <a name="deployedservicepackage-system-health-reports"></a>Systeemstatusrapporten DeployedServicePackage
**System.Hosting** is de instantie voor geïmplementeerde entiteiten.

### <a name="service-package-activation"></a>Het activeren van service
System.Hosting rapporten als OK als de activering van de service-pakket op het knooppunt geslaagd is. Anders wordt een fout opgetreden.

* **SourceId**: System.Hosting
* **De eigenschap**: activering
* **Volgende stappen**: onderzoeken waarom de activering is mislukt.

### <a name="code-package-activation"></a>Pakket-codeactivering
**System.Hosting** rapporteert als OK voor elk codepakket als de activering geslaagd is. Als de activering mislukt, wordt een waarschuwing weergegeven zoals geconfigureerd. Als **CodePackage** niet kan activeren of eindigt met een groter is dan de geconfigureerde fout **CodePackageHealthErrorThreshold**, die als host fungeert een fout gemeld. Als een servicepakket meerdere code pakketten bevat, wordt een rapport activering gegenereerd voor elk criterium.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van het voorvoegsel **CodePackageActivation** en bevat de naam van het codepakket en het toegangspunt dat als  **CodePackageActivation:*CodePackageName* :*Entrypoint/EntryPoint*** (bijvoorbeeld **CodePackageActivation:Code:SetupEntryPoint**)

### <a name="service-type-registration"></a>Service type is geregistreerd
**System.Hosting** rapporteert als OK als het servicetype is geregistreerd. Een fout gemeld. Als de registratie is niet uitgevoerd in de tijd (zoals deze is geconfigureerd met behulp van **ServiceTypeRegistrationTimeout**). Als de runtime is gesloten, type van de service niet is geregistreerd in het knooppunt en Hosting rapporteert een waarschuwing.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van het voorvoegsel **ServiceTypeRegistration** en bevat de naam van het servicetype (bijvoorbeeld **ServiceTypeRegistration:FileStoreServiceType**)

Het volgende voorbeeld ziet u een gezonde geïmplementeerd servicepakket:

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
                             Description           : The ServicePackage was activated successfully.
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
                             Description           : The CodePackage was activated successfully.
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
                             Description           : The ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/14/2017 4:55:14 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="download"></a>Downloaden
**System.Hosting** een fout gemeld als het downloaden van het service-pakket is mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**:  **downloaden:*RolloutVersion***
* **Volgende stappen**: onderzoeken waarom het downloaden is mislukt op het knooppunt.

### <a name="upgrade-validation"></a>Validatie van upgrade
**System.Hosting** meldt fout als validatie tijdens de upgrade mislukt of als de upgrade op het knooppunt mislukt.

* **SourceId**: System.Hosting
* **De eigenschap**: maakt gebruik van het voorvoegsel **FabricUpgradeValidation** en bevat de upgrade-versie
* **Beschrijving**: verwijst naar de opgetreden fout

## <a name="next-steps"></a>Volgende stappen
[Service Fabric-statusrapporten weergeven](service-fabric-view-entities-aggregated-health.md)

[Het rapport en controleer de servicestatus van de](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Controle en diagnose van lokaal services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)

