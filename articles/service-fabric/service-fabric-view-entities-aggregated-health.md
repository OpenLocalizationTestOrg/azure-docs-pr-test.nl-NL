---
title: aaaHow tooview Azure Service Fabric entiteiten geaggregeerd health | Microsoft Docs
description: Hierin wordt beschreven hoe u tooquery, bekijken en evalueren van de Azure Service Fabric-entiteiten geaggregeerde status, door middel van statusquery's en algemene query's.
services: service-fabric
documentationcenter: .net
author: oanapl
manager: timlt
editor: 
ms.assetid: fa34c52d-3a74-4b90-b045-ad67afa43fe5
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: oanapl
ms.openlocfilehash: add810551cac26d2b4ff81b57d94ddd780c2cc2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="view-service-fabric-health-reports"></a>Service Fabric-statusrapporten weergeven
Azure Service Fabric introduceert een [statusmodel](service-fabric-health-introduction.md) met health entiteiten op welke onderdelen van het systeem en watchdogs kunt rapport lokale voorwaarden die ze bewaken. Hallo [health store](service-fabric-health-introduction.md#health-store) alle health gegevens toodetermine aggregeert of entiteiten zijn in orde.

Hallo-cluster wordt automatisch gevuld met statusrapporten dat is verzonden door de onderdelen van het systeem Hallo. Meer informatie op [gebruik systeemstatusrapporten tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md).

Service Fabric bevat meerdere manieren tooget Hallo geaggregeerd health Hallo entiteiten:

* [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) of andere visualisatie hulpprogramma's
* Statusquery's (via PowerShell, API of REST)
* Algemene query's dat retourneren een lijst van entiteiten die status als een van de eigenschappen hello (via PowerShell, API of REST hebben)

Deze opties we toodemonstrate gebruik van een lokaal cluster met vijf knooppunten en Hallo [fabric: / WordCount-toepassing](http://aka.ms/servicefabric-wordcountapp). Hallo **fabric: / WordCount** toepassing bevat twee standaardservices, een stateful service van het type `WordCountServiceType`, en een stateless service van het type `WordCountWebServiceType`. Ik heb Hallo gewijzigd `ApplicationManifest.xml` toorequire zeven doel replica's voor Hallo stateful service en een partitie. Omdat er slechts vijf knooppunten in cluster hello, rapporteren Hallo-systeemonderdelen een waarschuwing op Hallo service partitie omdat deze lager dan Hallo doel count is.

```xml
<Service Name="WordCountService">
<<<<<<< HEAD
    <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="3">
      <UniformInt64Partition PartitionCount="1" LowKey="1" HighKey="26" />
    </StatefulService>
=======
  <StatefulService ServiceTypeName="WordCountServiceType" TargetReplicaSetSize="7" MinReplicaSetSize="2">
    <UniformInt64Partition PartitionCount="[WordCountService_PartitionCount]" LowKey="1" HighKey="26" />
  </StatefulService>
>>>>>>> 5e84dbdd8e45a5d6b36f435a550b7433b873bf11
</Service>
```

## <a name="health-in-service-fabric-explorer"></a>Status in Service Fabric Explorer
Service Fabric Explorer biedt een visuele weergave van Hallo-cluster. In onderstaande Hallo afbeelding, kunt u zien dat:

* toepassing Hello **fabric: / WordCount** is rood (fout) omdat er een foutgebeurtenis gemeld door **MyWatchdog** voor de eigenschap Hallo **beschikbaarheid**.
* Een van de services ontvangt, **fabric: / WordCount/WordCountService** geel gekleurd (in de waarschuwing). Hallo-service is geconfigureerd met zeven replica's en Hallo cluster heeft vijf knooppunten, zodat er twee repicas kan niet worden geplaatst. Hoewel dit niet wordt weergegeven hier, Hallo service partitie geel is vanwege een rapport van `System.FM` mededeling dat `Partition is below target replica or instance count`. Hallo gele partitie triggers Hallo gele service.
* Hallo-cluster is rood vanwege Hallo rode toepassing.

Hallo evaluatie gebruikt standaardbeleidsregels van clustermanifest hello en manifest van de toepassing. Strikte beleidsregels zijn en niet een storing kan tolereren.

Weergave van Hallo-cluster met Service Fabric Explorer:

![Weergave van Hallo-cluster met Service Fabric Explorer.][1]

[1]: ./media/service-fabric-view-entities-aggregated-health/servicefabric-explorer-cluster-health.png


> [!NOTE]
> Lees meer over [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
>
>

## <a name="health-queries"></a>Statusquery 's
Service Fabric statusquery's beschrijft voor elk ondersteund Hallo [Entiteitstypen](service-fabric-health-introduction.md#health-entities-and-hierarchy). Toegankelijk zijn via API, met behulp van methoden op Hallo [FabricClient.HealthManager](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthmanager?view=azure-dotnet), PowerShell-cmdlets en REST. Deze query's retourneren voltooid statusinformatie over Hallo entiteit: Hallo geaggregeerd status, entiteit health gebeurtenissen onderliggende statussen (indien van toepassing), slecht evaluaties (wanneer Hallo entiteit is niet in orde) en onderliggende items health statistieken (wanneer van toepassing).

> [!NOTE]
> Een health-entiteit wordt geretourneerd wanneer het volledig is gevuld in Hallo health store. Hallo-entiteit moet actief zijn (geen verwijderd) en een rapport. De bovenliggende entiteiten van Hallo hiërarchie keten moeten ook systeemrapporten hebben. Als een van deze voorwaarden niet wordt voldaan, Hallo health return vraagt een [FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception) met [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode) `FabricHealthEntityNotFound` die ziet waarom Hallo entiteit wordt niet geretourneerd.
>
>

Hallo statusquery's moeten in Hallo entiteits-id, die afhankelijk van het entiteitstype Hallo is doorgeven. Hallo-query's accepteren optionele health beleidsparameters. Als er geen statusbeleid worden opgegeven, Hallo [statusbeleid](service-fabric-health-introduction.md#health-policies) van het cluster of toepassingsmanifest hello worden gebruikt voor evaluatie. Als Hallo manifesten geen definitie voor statusbeleid bevatten, gebruikt Hallo standaard statusbeleid voor evaluatie. Hallo standaard statusbeleid komen niet zonder fouten. Hallo-query's ook filters voor het retourneren van alleen gedeeltelijke onderliggende accepteren of gebeurtenissen--Hallo waarden die respecteren Hallo opgegeven filters. Een ander filter kunt exclusief Hallo kinderen statistieken.

> [!NOTE]
> Hallo uitvoerfilters worden toegepast aan serverzijde hello, zodat het Hallo-bericht beantwoorden grootte wordt verkleind. Het is raadzaam Hallo uitvoerfilters toolimit Hallo gegevens geretourneerd, in plaats van filters toepassen op de client hello te gebruiken.
>
>

De status van de entiteit bevat:

* status van entiteit Hallo Hallo geaggregeerd. Door Hallo health store op basis van entiteit statusrapporten, onderliggende statussen (indien van toepassing) en statusbeleid wordt berekend. Lees meer over [entiteit de statusevaluatie](service-fabric-health-introduction.md#health-evaluation).  
* Hallo health gebeurtenissen op Hallo entiteit.
* Hallo-verzameling van de status van alle onderliggende items voor Hallo entiteiten die onderliggende elementen kunnen hebben. Hallo-statussen entiteit-id's bevatten en Hallo geaggregeerde status. tooget status voor een kind Hallo query health aanroepen voor Hallo onderliggende entiteitstype en Hallo onderliggende id doorgeven.
* Hallo slecht evaluaties dat punt toohello rapporteren die geactiveerd Hallo-status van het Hallo-entiteit als Hallo entiteit is niet in orde. Hallo-beoordelingen zijn recursieve, met Hallo kinderen health evaluaties waarmee huidige status is geactiveerd. Bijvoorbeeld, een watchdog een fout op basis van een replica gemeld. Hallo toepassingsstatus toont een slecht evaluatie vanwege tooan slecht service; Hallo-service is beschadigd vanwege tooa partitie in error; Hallo-partitie is beschadigd vanwege tooa replica in een fout. Hallo-replica is beschadigd vanwege toohello watchdog foutenrapport health.
* Hallo health statistieken voor alle typen voor onderliggende elementen van Hallo entiteiten die onderliggende elementen hebben. Bijvoorbeeld, cluster health toont Hallo totale aantal toepassingen, services, partities, replica's en entiteiten in de cluster Hallo geïmplementeerd. Status van de service bevat Hallo kunt u het totale aantal partities en replica's onder Hallo opgegeven service.

## <a name="get-cluster-health"></a>Status van de cluster ophalen
Retourneert Hallo health van Hallo cluster entiteit en Hallo statussen van toepassingen en knooppunten (kinderen van Hallo cluster) bevat. Invoer:

* [Optioneel] Hallo cluster statusbeleid gebruikt tooevaluate Hallo knooppunten en Hallo Clustergebeurtenissen.
* [Optioneel] Hallo application health beleid kaart gebruikt toooverride Hallo application manifest beleid met Hallo statusbeleid.
* [Optioneel] Filters voor gebeurtenissen, knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen, knooppunten en toepassingen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.
* [Optioneel] Filter tooexclude health statistieken.
* [Optioneel] Filteren tooinclude fabric: / System health statistieken in Hallo health statistieken. Alleen van toepassing als Hallo health statistieken niet worden weggelaten. Standaard bevatten Hallo health statistieken alleen statistieken voor toepassingen en niet Hallo-toepassing.

### <a name="api"></a>API
tooget cluster health, maak een `FabricClient` en aanroep Hallo [GetClusterHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthasync) methode op de **HealthManager**.

Hallo volgende oproep verzenden opgehaald Hallo cluster health:

```csharp
ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync();
```

Hallo volgende code Hallo cluster health opgehaald met behulp van een aangepaste cluster statusbeleid en filters voor knooppunten en toepassingen. Hiermee geeft u dat Hallo health statistieken Hallo fabric bevatten: / statistieken van het systeem. Het maken van [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthquerydescription), die Hallo invoergegevens bevat.

```csharp
var policy = new ClusterHealthPolicy()
{
    MaxPercentUnhealthyNodes = 20
};
var nodesFilter = new NodeHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error | HealthStateFilter.Warning
};
var applicationsFilter = new ApplicationHealthStatesFilter()
{
    HealthStateFilterValue = HealthStateFilter.Error
};
var healthStatisticsFilter = new ClusterHealthStatisticsFilter()
{
    ExcludeHealthStatistics = false,
    IncludeSystemApplicationHealthStatistics = true
};
var queryDescription = new ClusterHealthQueryDescription()
{
    HealthPolicy = policy,
    ApplicationsFilter = applicationsFilter,
    NodesFilter = nodesFilter,
    HealthStatisticsFilter = healthStatisticsFilter
};

ClusterHealth clusterHealth = await fabricClient.HealthManager.GetClusterHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo cluster status is [Get-ServiceFabricClusterHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo status van de cluster Hallo is vijf knooppunten Hallo systeemtoepassing en fabric: / WordCount geconfigureerd zoals wordt beschreven.

Hallo volgende cmdlet haalt status van de cluster met behulp van standaard statusbeleid. Hallo geaggregeerde status is waarschuwing, omdat Hallo fabric: / WordCount-toepassing bevindt zich in de waarschuwing. Houd er rekening mee hoe Hallo slecht evaluaties gedetailleerde informatie bevat over Hallo voorwaarden waarmee Hallo geaggregeerd status is geactiveerd.

```xml
PS D:\ServiceFabric> Get-ServiceFabricClusterHealth


AggregatedHealthState   : Warning
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Warning'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                          
                          
NodeHealthStates        : 
                          NodeName              : _Node_4
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_3
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_2
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_1
                          AggregatedHealthState : Ok
                          
                          NodeName              : _Node_0
                          AggregatedHealthState : Ok
                          
ApplicationHealthStates : 
                          ApplicationName       : fabric:/System
                          AggregatedHealthState : Ok
                          
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Warning
                          
HealthEvents            : None
HealthStatistics        : 
                          Node                  : 5 Ok, 0 Warning, 0 Error
                          Replica               : 6 Ok, 0 Warning, 0 Error
                          Partition             : 1 Ok, 1 Warning, 0 Error
                          Service               : 1 Ok, 1 Warning, 0 Error
                          DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                          DeployedApplication   : 5 Ok, 0 Warning, 0 Error
                          Application           : 0 Ok, 1 Warning, 0 Error
```

Hallo haalt volgende PowerShell-cmdlet Hallo-status van het Hallo-cluster met behulp van een aangepaste toepassingenbeleid. Deze filtert de resultaten tooget alleen toepassingen en knooppunten in de fout of waarschuwing. Als gevolg hiervan worden geen knooppunten geretourneerd, omdat ze allemaal in orde. Alleen Hallo fabric: / WordCount-toepassing hello toepassingen filter respecteert. Omdat Hallo aangepaste beleid tooconsider waarschuwingen als fouten voor Hallo fabric bepaalt: / WordCount-toepassing hello toepassing wordt geëvalueerd als in de fout en is daarom Hallo-cluster.

```powershell
PS D:\ServiceFabric> $appHealthPolicy = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicy
$appHealthPolicy.ConsiderWarningAsError = $true
$appHealthPolicyMap = New-Object -TypeName System.Fabric.Health.ApplicationHealthPolicyMap
$appUri1 = New-Object -TypeName System.Uri -ArgumentList "fabric:/WordCount"
$appHealthPolicyMap.Add($appUri1, $appHealthPolicy)
Get-ServiceFabricClusterHealth -ApplicationHealthPolicyMap $appHealthPolicyMap -ApplicationsFilter "Warning,Error" -NodesFilter "Warning,Error" -ExcludeHealthStatistics


AggregatedHealthState   : Error
UnhealthyEvaluations    : 
                          Unhealthy applications: 100% (1/1), MaxPercentUnhealthyApplications=0%.
                          
                          Unhealthy application: ApplicationName='fabric:/WordCount', AggregatedHealthState='Error'.
                          
                            Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                          
                            Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                          
                                Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                          
                                Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                          
                                    Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                          
                          
NodeHealthStates        : None
ApplicationHealthStates : 
                          ApplicationName       : fabric:/WordCount
                          AggregatedHealthState : Error
                          
HealthEvents            : None
```

### <a name="rest"></a>REST
U kunt de status van de cluster met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-node-health"></a>Ophalen van de gezondheid van knooppunt
Retourneert Hallo status van de entiteit van een knooppunt en bevat Hallo health gebeurtenissen die zijn gerapporteerd op Hallo-knooppunt. Invoer:

* [Vereist] Hallo knooppuntnaam die Hallo knooppunt aangeeft.
* [Optioneel] Hallo cluster health beleidsinstellingen tooevaluate health gebruikt.
* [Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.

### <a name="api"></a>API
tooget knooppunt health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetNodeHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getnodehealthasync) methode op de HealthManager.

Hallo haalt volgende code Hallo knooppunt status voor naam van het opgegeven knooppunt Hallo:

```csharp
NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(nodeName);
```

Hallo volgende code haalt Hallo knooppunt health voor Hallo node name en geeft gebeurtenissen filteren en aangepast beleid via opgegeven [NodeHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.nodehealthquerydescription):

```csharp
var queryDescription = new NodeHealthQueryDescription(nodeName)
{
    HealthPolicy = new ClusterHealthPolicy() {  ConsiderWarningAsError = true },
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.Warning },
};

NodeHealth nodeHealth = await fabricClient.HealthManager.GetNodeHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo de status van knooppunt is [Get-ServiceFabricNodeHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricnodehealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.
Hallo knooppunt health Hallo volgende cmdlet opgehaald met behulp van standaard statusbeleid:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNodeHealth _Node_1


NodeName              : _Node_1
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 3
                        SentAt                : 7/13/2017 4:39:23 PM
                        ReceivedAt            : 7/13/2017 4:40:47 PM
                        TTL                   : Infinite
                        Description           : Fabric node is up.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 4:40:47 PM, LastWarning = 1/1/0001 12:00:00 AM
```

Hallo volgende cmdlet wordt opgehaald Hallo status van alle knooppunten in cluster Hallo:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricNode | Get-ServiceFabricNodeHealth | select NodeName, AggregatedHealthState | ft -AutoSize

NodeName AggregatedHealthState
-------- ---------------------
_Node_4                     Ok
_Node_3                     Ok
_Node_2                     Ok
_Node_1                     Ok
_Node_0                     Ok
```

### <a name="rest"></a>REST
U krijgt de gezondheid van knooppunt met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-node-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-application-health"></a>Toepassingsstatus ophalen
Retourneert Hallo de status van een Toepassingsentiteit. Het bevat Hallo-statussen van Hallo geïmplementeerd toepassing en service onderliggende items. Invoer:

* [Vereist] Hallo toepassingsnaam (URI) die de toepassing hello identificeert.
* [Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen, services en geïmplementeerde toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen, services en geïmplementeerde toepassingen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.
* [Optioneel] Filter tooexclude Hallo health statistieken. Als niet wordt opgegeven, Hallo health statistieken Hallo ok, waarschuwing en fout aantal voor alle onderliggende objecten van toepassing zijn: services, partities, replica's, geïmplementeerde toepassingen en geïmplementeerde servicepakketten.

### <a name="api"></a>API
tooget toepassingsstatus, maak een `FabricClient` en aanroep Hallo [GetApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getapplicationhealthasync) methode op de HealthManager.

Hallo haalt volgende code de toepassingsstatus Hallo voor Hallo opgegeven toepassingsnaam (URI):

```csharp
ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(applicationName);
```

Hallo volgende code haalt Hallo toepassingsstatus voor Hallo opgegeven toepassingsnaam (URI), met filters en aangepaste beleidsregels opgegeven via [ApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.applicationhealthquerydescription).

```csharp
HealthStateFilter warningAndErrors = HealthStateFilter.Error | HealthStateFilter.Warning;
var serviceTypePolicy = new ServiceTypeHealthPolicy()
{
    MaxPercentUnhealthyPartitionsPerService = 0,
    MaxPercentUnhealthyReplicasPerPartition = 5,
    MaxPercentUnhealthyServices = 0,
};
var policy = new ApplicationHealthPolicy()
{
    ConsiderWarningAsError = false,
    DefaultServiceTypeHealthPolicy = serviceTypePolicy,
    MaxPercentUnhealthyDeployedApplications = 0,
};

var queryDescription = new ApplicationHealthQueryDescription(applicationName)
{
    HealthPolicy = policy,
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = warningAndErrors },
    ServicesFilter = new ServiceHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
    DeployedApplicationsFilter = new DeployedApplicationHealthStatesFilter() { HealthStateFilterValue = warningAndErrors },
};

ApplicationHealth applicationHealth = await fabricClient.HealthManager.GetApplicationHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo de status van toepassing is [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo volgende cmdlet retourneert Hallo health Hallo **fabric: / WordCount** toepassing:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Warning
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Warning'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountWebService
                                  AggregatedHealthState : Ok
                                  
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Warning
                                  
DeployedApplicationHealthStates : 
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_4
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_3
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_0
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_2
                                  AggregatedHealthState : Ok
                                  
                                  ApplicationName       : fabric:/WordCount
                                  NodeName              : _Node_1
                                  AggregatedHealthState : Ok
                                  
HealthEvents                    : 
                                  SourceId              : System.CM
                                  Property              : State
                                  HealthState           : Ok
                                  SequenceNumber        : 282
                                  SentAt                : 7/13/2017 5:57:05 PM
                                  ReceivedAt            : 7/13/2017 5:57:05 PM
                                  TTL                   : Infinite
                                  Description           : Application has been created.
                                  RemoveWhenExpired     : False
                                  IsExpired             : False
                                  Transitions           : Error->Ok = 7/13/2017 5:57:05 PM, LastWarning = 1/1/0001 12:00:00 AM
                                  
HealthStatistics                : 
                                  Replica               : 6 Ok, 0 Warning, 0 Error
                                  Partition             : 1 Ok, 1 Warning, 0 Error
                                  Service               : 1 Ok, 1 Warning, 0 Error
                                  DeployedServicePackage : 6 Ok, 0 Warning, 0 Error
                                  DeployedApplication   : 5 Ok, 0 Warning, 0 Error
```

Hallo volgende PowerShell-cmdlet geeft in het aangepaste beleid. Deze filters ook onderliggende elementen en gebeurtenissen.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth -ApplicationName fabric:/WordCount -ConsiderWarningAsError $true -ServicesFilter Error -EventsFilter Error -DeployedApplicationsFilter Error -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=true.
                                  
ServiceHealthStates             : 
                                  ServiceName           : fabric:/WordCount/WordCountService
                                  AggregatedHealthState : Error
                                  
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

### <a name="rest"></a>REST
U krijgt toepassingsstatus met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-an-application-by-using-an-application-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-service-health"></a>Servicestatus ophalen
Retourneert Hallo de status van een service-entiteit. Het bevat Hallo partitie statussen. Invoer:

* [Vereist] Hallo servicenaam (URI) dat Hallo service identificeert.
* [Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen en partities die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen en partities zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.
* [Optioneel] Filter tooexclude health statistieken. Als niet wordt opgegeven, Hallo health statistieken weergeven Hallo ok, waarschuwing en fout tellen voor alle partities en replica's van Hallo-service.

### <a name="api"></a>API
servicestatus tooget via Hallo-API maken een `FabricClient` en aanroep Hallo [GetServiceHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getservicehealthasync) methode op de HealthManager.

Hallo wordt volgende voorbeeld Hallo status van een service met de opgegeven service-naam (URI):

```charp
ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(serviceName);
```

Hallo volgende code haalt Hallo servicestatus voor de opgegeven servicenaam hello (URI), filters en aangepast beleid via geven [ServiceHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.servicehealthquerydescription):

```csharp
var queryDescription = new ServiceHealthQueryDescription(serviceName)
{
    EventsFilter = new HealthEventsFilter() { HealthStateFilterValue = HealthStateFilter.All },
    PartitionsFilter = new PartitionHealthStatesFilter() { HealthStateFilterValue = HealthStateFilter.Error },
};

ServiceHealth serviceHealth = await fabricClient.HealthManager.GetServiceHealthAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo-servicestatus is [Get-ServiceFabricServiceHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricservicehealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo-servicestatus Hallo volgende cmdlet opgehaald met behulp van standaard statusbeleid:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricServiceHealth -ServiceName fabric:/WordCount/WordCountService


ServiceName           : fabric:/WordCount/WordCountService
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                        
                        Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Warning'.
                        
                            Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
PartitionHealthStates : 
                        PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                        AggregatedHealthState : Warning
                        
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 15
                        SentAt                : 7/13/2017 5:57:05 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Service has been created.
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
                        Partition             : 0 Ok, 1 Warning, 0 Error
```

### <a name="rest"></a>REST
U krijgt de status van de service met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-partition-health"></a>Status van de partitie ophalen
Retourneert Hallo de status van een entiteit van de partitie. Het bevat Hallo replica statussen. Invoer:

* [Vereist] Hallo partitie-ID (GUID) die Hallo partitie identificeert.
* [Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen en replica's die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen en replica's zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.
* [Optioneel] Filter tooexclude health statistieken. Als niet wordt opgegeven, wordt Hallo health statistieken weergeven hoeveel replica's in ok, waarschuwing en fout statussen.

### <a name="api"></a>API
tooget partitie health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetPartitionHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getpartitionhealthasync) methode op de HealthManager. maken van de volgende optionele parameters toospecify, [PartitionHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.partitionhealthquerydescription).

```csharp
PartitionHealth partitionHealth = await fabricClient.HealthManager.GetPartitionHealthAsync(partitionId);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo partitie status is [Get-ServiceFabricPartitionHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricpartitionhealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo volgende cmdlet opgehaald Hallo status voor alle partities van Hallo **fabric: / WordCount/WordCountService** -service en uitsluit replica statussen:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricPartitionHealth -ReplicasFilter None

PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
AggregatedHealthState : Warning
UnhealthyEvaluations  : 
                        Unhealthy event: SourceId='System.FM', Property='State', HealthState='Warning', ConsiderWarningAsError=false.
                        
ReplicaHealthStates   : None
HealthEvents          : 
                        SourceId              : System.FM
                        Property              : State
                        HealthState           : Warning
                        SequenceNumber        : 72
                        SentAt                : 7/13/2017 5:57:29 PM
                        ReceivedAt            : 7/13/2017 5:57:48 PM
                        TTL                   : Infinite
                        Description           : Partition is below target replica or instance count.
                        fabric:/WordCount/WordCountService 7 2 af2e3e44-a8f8-45ac-9f31-4093eb897600
                          N/P RD _Node_2 Up 131444422260002646
                          N/S RD _Node_4 Up 131444422293113678
                          N/S RD _Node_3 Up 131444422293113679
                          N/S RD _Node_1 Up 131444422293118720
                          N/S RD _Node_0 Up 131444422293118721
                          (Showing 5 out of 5 replicas. Total available replicas: 5.)
                        
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Ok->Warning = 7/13/2017 5:57:48 PM, LastError = 1/1/0001 12:00:00 AM
                        
                        SourceId              : System.PLB
                        Property              : ServiceReplicaUnplacedHealth_Secondary_af2e3e44-a8f8-45ac-9f31-4093eb897600
                        HealthState           : Warning
                        SequenceNumber        : 131444445174851664
                        SentAt                : 7/13/2017 6:35:17 PM
                        ReceivedAt            : 7/13/2017 6:35:18 PM
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
                        FaultDomain:fd:/1 NodeName:_Node_1 NodeType:NodeType1 UpgradeDomain:1 UpgradeDomain: ud:/1 Deactivation Intent/Status: None/None
                        FaultDomain:fd:/0 NodeName:_Node_0 NodeType:NodeType0 UpgradeDomain:0 UpgradeDomain: ud:/0 Deactivation Intent/Status: None/None
                        
                        Existing Primary Replica -- Nodes with Partition's Existing Primary Replica or Secondary Replicas:
                        --
                        FaultDomain:fd:/2 NodeName:_Node_2 NodeType:NodeType2 UpgradeDomain:2 UpgradeDomain: ud:/2 Deactivation Intent/Status: None/None
                        
                        
                        RemoveWhenExpired     : True
                        IsExpired             : False
                        Transitions           : Error->Warning = 7/13/2017 5:57:48 PM, LastOk = 1/1/0001 12:00:00 AM
                        
HealthStatistics      : 
                        Replica               : 5 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
U kunt de status van de partitie met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-partition-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-replica-health"></a>De status replica ophalen
Hallo-status van de replica van een stateful service of een staatloze service-exemplaar geretourneerd. Invoer:

* [Vereist] Hallo partitie-ID (GUID) en de replica-ID die Hallo replica identificeert.
* [Optioneel] Hallo application health beleidsparameters gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.

### <a name="api"></a>API
tooget hello replica health via Hallo-API maken een `FabricClient` en aanroep Hallo [GetReplicaHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getreplicahealthasync) methode op de HealthManager. geavanceerde parameters, gebruik toospecify [ReplicaHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.replicahealthquerydescription).

```csharp
ReplicaHealth replicaHealth = await fabricClient.HealthManager.GetReplicaHealthAsync(partitionId, replicaId);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo replica de status is [Get-ServiceFabricReplicaHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricreplicahealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo volgende cmdlet opgehaald Hallo status van de primaire replica Hallo voor alle partities van Hallo-service:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricPartition fabric:/WordCount/WordCountService | Get-ServiceFabricReplica | where {$_.ReplicaRole -eq "Primary"} | Get-ServiceFabricReplicaHealth


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Ok
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
U krijgt de status replica met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-replica-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-deployed-application-health"></a>Status van de geïmplementeerde toepassing ophalen
Retourneert Hallo de status van een toepassing is geïmplementeerd op een knooppunt-entiteit. Het bevat Hallo geïmplementeerd service pakket statussen. Invoer:

* Naam van de toepassing [vereist] hello (URI) en knooppuntnaam (tekenreeks) die Hallo identificeren toepassing geïmplementeerd.
* [Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen en geïmplementeerde servicepakketten die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen en geïmplementeerde servicepakketten zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.
* [Optioneel] Filter tooexclude health statistieken. Als niet wordt opgegeven, weergeven Hallo health statistieken Hallo aantal geïmplementeerde servicepakketten in de status ok, waarschuwing en fout.

### <a name="api"></a>API
tooget hello status van een toepassing is geïmplementeerd op een knooppunt via Hallo-API maken een `FabricClient` en aanroep Hallo [GetDeployedApplicationHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedapplicationhealthasync) methode op de HealthManager. optionele parameters toospecify, gebruik [DeployedApplicationHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedapplicationhealthquerydescription).

```csharp
DeployedApplicationHealth health = await fabricClient.HealthManager.GetDeployedApplicationHealthAsync(
    new DeployedApplicationHealthQueryDescription(applicationName, nodeName));
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo geïmplementeerd toepassingsstatus is [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toofind uit waarop een toepassing wordt geïmplementeerd, voeren [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en bekijkt hello kinderen toepassing geïmplementeerd.

Hallo volgende cmdlet opgehaald Hallo health Hallo **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplicationHealth -ApplicationName fabric:/WordCount -NodeName _Node_0


ApplicationName                    : fabric:/WordCount
NodeName                           : _Node_0
AggregatedHealthState              : Ok
DeployedServicePackageHealthStates : 
                                     ServiceManifestName   : WordCountServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
                                     ServiceManifestName   : WordCountWebServicePkg
                                     ServicePackageActivationId : 
                                     NodeName              : _Node_0
                                     AggregatedHealthState : Ok
                                     
HealthEvents                       : 
                                     SourceId              : System.Hosting
                                     Property              : Activation
                                     HealthState           : Ok
                                     SequenceNumber        : 131444422261848308
                                     SentAt                : 7/13/2017 5:57:06 PM
                                     ReceivedAt            : 7/13/2017 5:57:17 PM
                                     TTL                   : Infinite
                                     Description           : hello application was activated successfully.
                                     RemoveWhenExpired     : False
                                     IsExpired             : False
                                     Transitions           : Error->Ok = 7/13/2017 5:57:17 PM, LastWarning = 1/1/0001 12:00:00 AM
                                     
HealthStatistics                   : 
                                     DeployedServicePackage : 2 Ok, 0 Warning, 0 Error
```

### <a name="rest"></a>REST
U krijgt de status geïmplementeerde toepassing met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-deployed-application-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="get-deployed-service-package-health"></a>Status van geïmplementeerde service pakket ophalen
Retourneert Hallo status van een geïmplementeerde service pakket entiteit. Invoer:

* [Vereist] Hallo toepassingsnaam (URI), knooppuntnaam (tekenreeks) en manifest servicenaam (tekenreeks) die Hallo identificeren geïmplementeerd servicepakket.
* [Optioneel] Hallo statusbeleid voor de toepassing gebruikt toooverride Hallo application manifest-beleid.
* [Optioneel] Filters voor gebeurtenissen die aangeven welke posten van belang zijn en moeten worden geretourneerd in Hallo resultaat (bijvoorbeeld alleen, fouten of waarschuwingen en fouten). Alle gebeurtenissen zijn gebruikte tooevaluate Hallo geaggregeerd entiteitsstatus, ongeacht het Hallo-filter.

### <a name="api"></a>API
tooget hello status van een geïmplementeerde servicepakket via Hallo-API maken een `FabricClient` en aanroep Hallo [GetDeployedServicePackageHealthAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getdeployedservicepackagehealthasync) methode op de HealthManager. optionele parameters toospecify, gebruik [DeployedServicePackageHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.deployedservicepackagehealthquerydescription).

```csharp
DeployedServicePackageHealth health = await fabricClient.HealthManager.GetDeployedServicePackageHealthAsync(
    new DeployedServicePackageHealthQueryDescription(applicationName, nodeName, serviceManifestName));
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo geïmplementeerd servicestatus-pakket is [Get-ServiceFabricDeployedServicePackageHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricdeployedservicepackagehealth). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet. toosee waarop een toepassing wordt geïmplementeerd, voeren [Get-ServiceFabricApplicationHealth](/powershell/module/servicefabric/get-servicefabricapplicationhealth?view=azureservicefabricps) en bekijkt hello geïmplementeerde toepassingen. toosee die servicepakketten in een toepassing, zoekt u naar op Hallo geïmplementeerd service pakket kinderen in Hallo [Get-ServiceFabricDeployedApplicationHealth](/powershell/module/servicefabric/get-servicefabricdeployedapplicationhealth?view=azureservicefabricps) uitvoer.

Hallo volgende cmdlet opgehaald Hallo health Hallo **WordCountServicePkg** servicepakket Hallo **fabric: / WordCount** toepassing geïmplementeerd op **_Node_2**. Hallo entiteit heeft **System.Hosting** rapporten voor geslaagde pakket service en ingangspunt activering en succesvolle registratie van het type van de service.

```powershell
PS D:\ServiceFabric> Get-ServiceFabricDeployedApplication -ApplicationName fabric:/WordCount -NodeName _Node_2 | Get-ServiceFabricDeployedServicePackageHealth -ServiceManifestName WordCountServicePkg


ApplicationName            : fabric:/WordCount
ServiceManifestName        : WordCountServicePkg
ServicePackageActivationId : 
NodeName                   : _Node_2
AggregatedHealthState      : Ok
HealthEvents               : 
                             SourceId              : System.Hosting
                             Property              : Activation
                             HealthState           : Ok
                             SequenceNumber        : 131444422267693359
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServicePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : CodePackageActivation:Code:EntryPoint
                             HealthState           : Ok
                             SequenceNumber        : 131444422267903345
                             SentAt                : 7/13/2017 5:57:06 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello CodePackage was activated successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                             
                             SourceId              : System.Hosting
                             Property              : ServiceTypeRegistration:WordCountServiceType
                             HealthState           : Ok
                             SequenceNumber        : 131444422272458374
                             SentAt                : 7/13/2017 5:57:07 PM
                             ReceivedAt            : 7/13/2017 5:57:18 PM
                             TTL                   : Infinite
                             Description           : hello ServiceType was registered successfully.
                             RemoveWhenExpired     : False
                             IsExpired             : False
                             Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
```

### <a name="rest"></a>REST
U kunt de status van de geïmplementeerde service pakket met krijgen een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-service-package-by-using-a-health-policy) die statusbeleid dat wordt beschreven in de hoofdtekst van het Hallo bevat.

## <a name="health-chunk-queries"></a>Health chunk query 's
Hallo health chunk query's kunnen cluster met meerdere niveaus van kinderen (recursief) per invoer filters worden geretourneerd. Ondersteunt geavanceerde filters waarmee een grote flexibiliteit bij het kiezen van de onderliggende hello toobe geretourneerd. Hallo filters kunnen onderliggende items met de unieke id Hallo of door andere groeps-id's en/of de statussen opgeven. Geen onderliggende elementen zijn standaard opgenomen als tegengestelde toohealth-opdrachten die altijd eerste niveau onderliggende elementen bevatten.

Hallo [statusquery's](service-fabric-view-entities-aggregated-health.md#health-queries) return alleen eerste niveau kinderen Hallo opgegeven entiteit per vereist filters. tooget hello kinderen van onderliggende items hello, moet u extra health API's voor elke entiteit van belang aanroepen. Op deze manier tooget Hallo status van specifieke entiteiten, moet u aanroepen één health API voor elke gewenste entiteit. Hallo chunk geavanceerde filteren kunt u query toorequest meerdere items in één query op het Hallo-berichtgrootte en Hallo aantal berichten voor het minimaliseren van belang.

Hallo-waarde van Hallo chunk query is dat u de status voor meer cluster entiteiten (mogelijk alle cluster entiteiten starten in de hoofdmap van de vereiste) kunt krijgen in één aanroep. U kunt de gezondheid van complexe query zoals express:

* Retour alleen toepassingen in de fout en voor die toepassingen bevatten alle services in waarschuwing of fout. Voor de geretourneerde services omvatten alle partities.
* Alleen Hallo status van de opgegeven door de namen van de vier toepassingen retourneren.
* Alleen Hallo status van toepassingen van een type van de gewenste toepassing retourneren.
* Retourneert alle geïmplementeerde entiteiten op een knooppunt. Retourneert alle toepassingen, alle geïmplementeerde toepassingen op Hallo opgegeven knooppunt en alle Hallo geïmplementeerde servicepakketten op dat knooppunt.
* Alle replica's in een fout geretourneerd. Retourneert alle toepassingen, services, partities en alleen replica's in de fout.
* Retourneren van alle toepassingen. Voor een opgegeven service omvatten alle partities.

Hallo health chunk query is momenteel toegankelijk alleen voor Hallo cluster entiteit. Een cluster health chunk, waarin wordt:

* Hallo cluster geaggregeerd status.
* Hallo health status chunk lijst met knooppunten die fungeren als invoer filters respecteren.
* Hallo health status chunk lijst met toepassingen die invoer filters respecteren. Elk segment application health-status bevat een lijst chunk met alle services die respecteren invoer filters en een chunk-lijst met alle geïmplementeerde toepassingen die Hallo filters respecteren. Hetzelfde voor Hallo onderliggende elementen van services en geïmplementeerde toepassingen. Op deze manier alle entiteiten in Hallo cluster kunnen worden mogelijk geretourneerd als in een hiërarchische aangevraagd.

### <a name="cluster-health-chunk-query"></a>Cluster health chunk query
Retourneert Hallo health van Hallo cluster entiteit en Hallo hiërarchische health status segmenten van vereiste onderliggende items bevat. Invoer:

* [Optioneel] Hallo cluster statusbeleid gebruikt tooevaluate Hallo knooppunten en Hallo Clustergebeurtenissen.
* [Optioneel] Hallo application health beleid kaart gebruikt toooverride Hallo application manifest beleid met Hallo statusbeleid.
* [Optioneel] Filters voor knooppunten en toepassingen die welke vermeldingen opgeeft van belang zijn en moeten worden geretourneerd in Hallo resultaat. Hallo filters specifieke tooan entiteit of groep van entiteiten zijn of zijn van toepassing tooall entiteiten op dat niveau. lijst met filters Hallo kan bevatten één algemene filter en/of filters voor specifieke id's toofine-gebruikerssegmentatie entiteiten die door Hallo query zijn geretourneerd. Als u niets opgeeft, worden niet Hallo kinderen standaard geretourneerd.
  Meer informatie over filters op Hallo [NodeHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.nodehealthstatefilter) en [ApplicationHealthStateFilter](https://docs.microsoft.com/dotnet/api/system.fabric.health.applicationhealthstatefilter). Hallo toepassing filters kunnen recursief geavanceerde filters voor kinderen opgeven.

Hallo chunk resultaat bevat Hallo onderliggende items waarvan Hallo filters respecteren.

Hallo chunk query retourneert op dit moment geen slechte evaluaties of entiteit gebeurtenissen. Deze extra informatie kan worden verkregen met behulp van Hallo bestaande cluster health query.

### <a name="api"></a>API
tooget cluster health Segmentselectie, maakt u een `FabricClient` en aanroep Hallo [GetClusterHealthChunkAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.healthclient.getclusterhealthchunkasync) methode op de **HealthManager**. U kunt doorgeven [ClusterHealthQueryDescription](https://docs.microsoft.com/dotnet/api/system.fabric.description.clusterhealthchunkquerydescription) toodescribe statusbeleid en geavanceerde filters.

Hallo haalt volgende code cluster health chunk met geavanceerde filters.

```csharp
var queryDescription = new ClusterHealthChunkQueryDescription();
queryDescription.ApplicationFilters.Add(new ApplicationHealthStateFilter()
    {
        // Return applications only if they are in error
        HealthStateFilter = HealthStateFilter.Error
    });

// Return all replicas
var wordCountServiceReplicaFilter = new ReplicaHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };

// Return all replicas and all partitions
var wordCountServicePartitionFilter = new PartitionHealthStateFilter()
    {
        HealthStateFilter = HealthStateFilter.All
    };
wordCountServicePartitionFilter.ReplicaFilters.Add(wordCountServiceReplicaFilter);

// For specific service, return all partitions and all replicas
var wordCountServiceFilter = new ServiceHealthStateFilter()
{
    ServiceNameFilter = new Uri("fabric:/WordCount/WordCountService"),
};
wordCountServiceFilter.PartitionFilters.Add(wordCountServicePartitionFilter);

// Application filter: for specific application, return no services except hello ones of interest
var wordCountApplicationFilter = new ApplicationHealthStateFilter()
    {
        // Always return fabric:/WordCount application
        ApplicationNameFilter = new Uri("fabric:/WordCount"),
    };
wordCountApplicationFilter.ServiceFilters.Add(wordCountServiceFilter);

queryDescription.ApplicationFilters.Add(wordCountApplicationFilter);

var result = await fabricClient.HealthManager.GetClusterHealthChunkAsync(queryDescription);
```

### <a name="powershell"></a>PowerShell
Hallo cmdlet tooget Hallo cluster status is [Get-ServiceFabricClusterChunkHealth](https://docs.microsoft.com/powershell/module/servicefabric/get-servicefabricclusterhealthchunk). Toohello cluster eerst verbinding te maken met behulp van Hallo [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet.

Hallo haalt volgende code knooppunten alleen als deze fout, met uitzondering van een specifiek knooppunt dat moet altijd worden geretourneerd.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$nodeFilter1 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{HealthStateFilter=$errorFilter}
$nodeFilter2 = New-Object System.Fabric.Health.NodeHealthStateFilter -Property @{NodeNameFilter="_Node_1";HealthStateFilter=$allFilter}
# Create node filter list that will be passed in hello cmdlet
$nodeFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.NodeHealthStateFilter]
$nodeFilters.Add($nodeFilter1)
$nodeFilters.Add($nodeFilter2)

Get-ServiceFabricClusterHealthChunk -NodeFilters $nodeFilters


HealthState                  : Warning
NodeHealthStateChunks        : 
                               TotalCount            : 1
                               
                               NodeName              : _Node_1
                               HealthState           : Ok
                               
ApplicationHealthStateChunks : None
```

Hallo volgende cmdlet haalt cluster chunk met toepassingsfilters.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

# All replicas
$replicaFilter = New-Object System.Fabric.Health.ReplicaHealthStateFilter -Property @{HealthStateFilter=$allFilter}

# All partitions
$partitionFilter = New-Object System.Fabric.Health.PartitionHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$partitionFilter.ReplicaFilters.Add($replicaFilter)

# For WordCountService, return all partitions and all replicas
$svcFilter1 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{ServiceNameFilter="fabric:/WordCount/WordCountService"}
$svcFilter1.PartitionFilters.Add($partitionFilter)

$svcFilter2 = New-Object System.Fabric.Health.ServiceHealthStateFilter -Property @{HealthStateFilter=$errorFilter}

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{ApplicationNameFilter="fabric:/WordCount"}
$appFilter.ServiceFilters.Add($svcFilter1)
$appFilter.ServiceFilters.Add($svcFilter2)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)

Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 1
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               ServiceHealthStateChunks : 
                                TotalCount            : 1
                               
                                ServiceName           : fabric:/WordCount/WordCountService
                                HealthState           : Error
                                PartitionHealthStateChunks : 
                                    TotalCount            : 1
                               
                                    PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
                                    HealthState           : Error
                                    ReplicaHealthStateChunks : 
                                        TotalCount            : 5
                               
                                        ReplicaOrInstanceId   : 131444422293118720
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293118721
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113678
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422293113679
                                        HealthState           : Ok
                               
                                        ReplicaOrInstanceId   : 131444422260002646
                                        HealthState           : Error
```

Hallo retourneert volgende cmdlet alle geïmplementeerde entiteiten op een knooppunt.

```xml
PS D:\ServiceFabric> $errorFilter = [System.Fabric.Health.HealthStateFilter]::Error;
$allFilter = [System.Fabric.Health.HealthStateFilter]::All;

$dspFilter = New-Object System.Fabric.Health.DeployedServicePackageHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$daFilter =  New-Object System.Fabric.Health.DeployedApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter;NodeNameFilter="_Node_2"}
$daFilter.DeployedServicePackageFilters.Add($dspFilter)

$appFilter = New-Object System.Fabric.Health.ApplicationHealthStateFilter -Property @{HealthStateFilter=$allFilter}
$appFilter.DeployedApplicationFilters.Add($daFilter)

$appFilters = New-Object System.Collections.Generic.List[System.Fabric.Health.ApplicationHealthStateFilter]
$appFilters.Add($appFilter)
Get-ServiceFabricClusterHealthChunk -ApplicationFilters $appFilters


HealthState                  : Error
NodeHealthStateChunks        : None
ApplicationHealthStateChunks : 
                               TotalCount            : 2
                               
                               ApplicationName       : fabric:/System
                               HealthState           : Ok
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : FAS
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
                               
                               
                               
                               ApplicationName       : fabric:/WordCount
                               ApplicationTypeName   : WordCount
                               HealthState           : Error
                               DeployedApplicationHealthStateChunks : 
                                TotalCount            : 1
                               
                                NodeName              : _Node_2
                                HealthState           : Ok
                                DeployedServicePackageHealthStateChunks :
                                    TotalCount            : 1
                               
                                    ServiceManifestName   : WordCountServicePkg
                                    ServicePackageActivationId : 
                                    HealthState           : Ok
```

### <a name="rest"></a>REST
U krijgt cluster health chunk gevonden met een [GET-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/get-the-health-of-a-cluster-using-health-chunks) of een [POST-aanvraag](https://docs.microsoft.com/rest/api/servicefabric/health-of-cluster) die statusbeleid en geavanceerde filters beschreven in de hoofdtekst van het Hallo bevat.

## <a name="general-queries"></a>Algemene query 's
Algemene query's retourneren een lijst met Service Fabric-entiteiten van een bepaald type. Ze worden weergegeven via Hallo API (via de methoden op Hallo **FabricClient.QueryManager**), PowerShell-cmdlets en REST. Deze query's samenvoegen subquery's uit meerdere onderdelen. Een van beide is Hallo [health store](service-fabric-health-introduction.md#health-store), de status voor elke queryresultaat die Hallo gevuld geaggregeerd.  

> [!NOTE]
> Algemene query's terug Hallo geaggregeerd status van de entiteit Hallo en bevatten geen uitgebreide statusgegevens. Als u een entiteit is niet in orde, kunt u volgen met health-query's tooget alle de health-gegevens, inclusief gebeurtenissen, onderliggende statussen en slecht evaluaties.
>
>

Als algemene query's een onbekende status voor een entiteit retourneren, is het mogelijk dat Hallo health store bevat geen volledige gegevens over Hallo entiteit. Het is ook mogelijk dat een subquery toohello health store niet geslaagd is (bijvoorbeeld: Er is een communicatiefout opgetreden of Hallo health store is beperkt). Een health-query voor de entiteit Hallo opvolgen. Als de subquery Hallo tijdelijke fouten, zoals netwerkproblemen optreden, kan deze vervolgzelfstudie query slagen. Ook kan geven u meer informatie uit health store Hallo over waarom Hallo entiteit is niet beschikbaar gemaakt.

query's met Hallo **HealthState** voor entiteiten zijn:

* Lijst met knooppunten: retourneert Hallo lijst met knooppunten in Hallo-cluster (wisselbare).
  * API: [FabricClient.QueryClient.GetNodeListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getnodelistasync)
  * PowerShell: Get-ServiceFabricNode
* Lijst met toepassingen: retourneert Hallo lijst met toepassingen in Hallo-cluster (wisselbare).
  * API: [FabricClient.QueryClient.GetApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getapplicationlistasync)
  * PowerShell: Get-ServiceFabricApplication
* Lijst met Services: retourneert Hallo lijst met services in een toepassing (wisselbare).
  * API: [FabricClient.QueryClient.GetServiceListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getservicelistasync)
  * PowerShell: Get-ServiceFabricService
* Lijst met partitie: retourneert Hallo lijst met partities in een service (wisselbare).
  * API: [FabricClient.QueryClient.GetPartitionListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getpartitionlistasync)
  * PowerShell: Get-ServiceFabricPartition
* Lijst met replica's: retourneert Hallo lijst met replica's in een partitie (wisselbare).
  * API: [FabricClient.QueryClient.GetReplicaListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getreplicalistasync)
  * PowerShell: Get-ServiceFabricReplica
* Lijst met toepassingen geïmplementeerd: retourneert Hallo lijst met geïmplementeerde toepassingen op een knooppunt.
  * API: [FabricClient.QueryClient.GetDeployedApplicationListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedapplicationlistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication
* De lijst van de service-pakket wordt geïmplementeerd: retourneert Hallo lijst met servicepakketten in een geïmplementeerde toepassing.
  * API: [FabricClient.QueryClient.GetDeployedServicePackageListAsync](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient.getdeployedservicepackagelistasync)
  * PowerShell: Get-ServiceFabricDeployedApplication

> [!NOTE]
> Hallo zoekopdrachten wisselbare resultaten geretourneerd. Hallo retourtype van deze query's is een lijst die is afgeleid van [PagedList<T>](https://docs.microsoft.com/dotnet/api/system.fabric.query.pagedlist-1). Hallo resultaten een bericht niet passen, alleen een pagina wordt geretourneerd als een ContinuationToken die houdt waarin de opsomming is gestopt. Blijven toocall Hallo dezelfde query- en in vervolgtoken Hallo van Hallo vorige tooget volgende queryresultaten.
>
>

### <a name="examples"></a>Voorbeelden
Hallo volgende code wordt opgehaald Hallo slecht toepassingen in Hallo-cluster:

```csharp
var applications = fabricClient.QueryManager.GetApplicationListAsync().Result.Where(
  app => app.HealthState == HealthState.Error);
```

Hallo volgende cmdlet opgehaald Hallo toepassingsgegevens voor Hallo fabric: / WordCount-toepassing. U ziet dat de status op de waarschuwing.

```powershell
PS C:\> Get-ServiceFabricApplication -ApplicationName fabric:/WordCount

ApplicationName        : fabric:/WordCount
ApplicationTypeName    : WordCount
ApplicationTypeVersion : 1.0.0
ApplicationStatus      : Ready
HealthState            : Warning
ApplicationParameters  : { "WordCountWebService_InstanceCount" = "1";
                         "_WFDebugParams_" = "[{"ServiceManifestName":"WordCountWebServicePkg","CodePackageName":"Code","EntryPointType":"Main","Debug
                         ExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {74f7e5d5-71a9-47e2-a8cd-1878ec4734f1} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"},{"ServiceManifestName":"WordCountServicePkg","CodeP
                         ackageName":"Code","EntryPointType":"Main","DebugExePath":"C:\\Program Files (x86)\\Microsoft Visual Studio
                         14.0\\Common7\\Packages\\Debugger\\VsDebugLaunchNotify.exe","DebugArguments":" {2ab462e6-e0d1-4fda-a844-972f561fe751} -p
                         [ProcessId] -tid [ThreadId]","EnvironmentBlock":"_NO_DEBUG_HEAP=1\u0000"}]" }
```

Hallo volgende cmdlet opgehaald Hallo services met een status van de fout:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplication | Get-ServiceFabricService | where {$_.HealthState -eq "Error"}


ServiceName            : fabric:/WordCount/WordCountService
ServiceKind            : Stateful
ServiceTypeName        : WordCountServiceType
IsServiceGroup         : False
ServiceManifestVersion : 1.0.0
HasPersistedState      : True
ServiceStatus          : Active
HealthState            : Error
```

## <a name="cluster-and-application-upgrades"></a>Cluster en de toepassing upgrades
Tijdens een bewaakte upgrade van het Hallo-cluster en de toepassing controleert Service Fabric health tooensure dat alles in orde blijft. Als een entiteit niet in orde is als geëvalueerd met behulp van de geconfigureerde statusbeleid, geldt Hallo upgrade upgrade-specifiek beleid toodetermine Hallo volgende actie. Hallo upgrade mogelijk onderbroken tooallow gebruikersinteractie (zoals de vaststelling van de fout of wijzigen van beleid) of het mogelijk automatisch terugdraaien toohello vorige goede versie.

Tijdens een *cluster* bijwerkt, kunt u Hallo cluster upgradestatus krijgen. Hallo upgradestatus omvat slecht evaluaties, welke toowhat punt niet in orde in Hallo-cluster is. Als het Hallo-upgrade is teruggedraaid vanwege toohealth problemen, onthoudt upgradestatus Hallo Hallo laatste slecht redenen. Deze informatie kunt beheerders onderzoeken wat er mis ging nadat het Hallo-upgrade is teruggedraaid of gestopt.

Op deze manier tijdens een *toepassing* bijwerkt, alle slechte beoordelingen zijn opgenomen in upgradestatus Hallo-toepassing.

Hallo hieronder vindt u upgradestatus Hallo-toepassing voor een gewijzigde fabric: / WordCount-toepassing. Een watchdog heeft een fout gerapporteerd op een van de replica's. Hallo upgrade ongedaan omdat Hallo statuscontroles niet worden nageleefd.

```powershell
PS C:\> Get-ServiceFabricApplicationUpgrade fabric:/WordCount

ApplicationName               : fabric:/WordCount
ApplicationTypeName           : WordCount
TargetApplicationTypeVersion  : 1.0.0.0
ApplicationParameters         : {}
StartTimestampUtc             : 4/21/2017 5:23:26 PM
FailureTimestampUtc           : 4/21/2017 5:23:37 PM
FailureReason                 : HealthCheck
UpgradeState                  : RollingBackInProgress
UpgradeDuration               : 00:00:23
CurrentUpgradeDomainDuration  : 00:00:00
CurrentUpgradeDomainProgress  : UD1

                                NodeName            : _Node_1
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_2
                                UpgradePhase        : Upgrading

                                NodeName            : _Node_3
                                UpgradePhase        : PreUpgradeSafetyCheck
                                PendingSafetyChecks :
                                EnsurePartitionQuorum - PartitionId: 30db5be6-4e20-4698-8185-4bd7ca744020
NextUpgradeDomain             : UD2
UpgradeDomainsStatus          : { "UD1" = "Completed";
                                "UD2" = "Pending";
                                "UD3" = "Pending";
                                "UD4" = "Pending" }
UnhealthyEvaluations          :
                                Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.

                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.

                                      Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.

                                      Unhealthy partition: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b', AggregatedHealthState='Error'.

                                          Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.

                                          Unhealthy replica: PartitionId='a1f83a35-d6bf-4d39-b90d-28d15f39599b',
                                  ReplicaOrInstanceId='131031502346844058', AggregatedHealthState='Error'.

                                              Error event: SourceId='DiskWatcher', Property='Disk'.

UpgradeKind                   : Rolling
RollingUpgradeMode            : UnmonitoredAuto
ForceRestart                  : False
UpgradeReplicaSetCheckTimeout : 00:15:00
```

Lees meer over Hallo [upgrade van de Service Fabric-toepassing](service-fabric-application-upgrade.md).

## <a name="use-health-evaluations-tootroubleshoot"></a>Gebruik health evaluaties tootroubleshoot
Wanneer er een probleem met het Hallo-cluster of een toepassing, bekijkt hello cluster of de toepassing health toopinpoint wat is het probleem. Hallo slecht evaluaties bieden informatie over welke triggered Hallo huidige slecht. Als u wilt, kunt u inzoomen op Hallo hoofdoorzaak voor beschadigde onderliggende entiteiten tooidentify.

Neem bijvoorbeeld een toepassing slecht omdat er een foutenrapport op een van de replica's. Hallo toont volgende Powershell-cmdlet Hallo slecht evaluaties:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricApplicationHealth fabric:/WordCount -EventsFilter None -ServicesFilter None -DeployedApplicationsFilter None -ExcludeHealthStatistics


ApplicationName                 : fabric:/WordCount
AggregatedHealthState           : Error
UnhealthyEvaluations            : 
                                  Unhealthy services: 100% (1/1), ServiceType='WordCountServiceType', MaxPercentUnhealthyServices=0%.
                                  
                                  Unhealthy service: ServiceName='fabric:/WordCount/WordCountService', AggregatedHealthState='Error'.
                                  
                                    Unhealthy partitions: 100% (1/1), MaxPercentUnhealthyPartitionsPerService=0%.
                                  
                                    Unhealthy partition: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', AggregatedHealthState='Error'.
                                  
                                        Unhealthy replicas: 20% (1/5), MaxPercentUnhealthyReplicasPerPartition=0%.
                                  
                                        Unhealthy replica: PartitionId='af2e3e44-a8f8-45ac-9f31-4093eb897600', ReplicaOrInstanceId='131444422260002646', AggregatedHealthState='Error'.
                                  
                                            Error event: SourceId='MyWatchdog', Property='Memory'.
                                  
ServiceHealthStates             : None
DeployedApplicationHealthStates : None
HealthEvents                    : None
```

U kunt bekijkt hello replica tooget meer informatie:

```powershell
PS D:\ServiceFabric> Get-ServiceFabricReplicaHealth -ReplicaOrInstanceId 131444422260002646 -PartitionId af2e3e44-a8f8-45ac-9f31-4093eb897600


PartitionId           : af2e3e44-a8f8-45ac-9f31-4093eb897600
ReplicaId             : 131444422260002646
AggregatedHealthState : Error
UnhealthyEvaluations  : 
                        Error event: SourceId='MyWatchdog', Property='Memory'.
                        
HealthEvents          : 
                        SourceId              : System.RA
                        Property              : State
                        HealthState           : Ok
                        SequenceNumber        : 131444422263668344
                        SentAt                : 7/13/2017 5:57:06 PM
                        ReceivedAt            : 7/13/2017 5:57:18 PM
                        TTL                   : Infinite
                        Description           : Replica has been created._Node_2
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Error->Ok = 7/13/2017 5:57:18 PM, LastWarning = 1/1/0001 12:00:00 AM
                        
                        SourceId              : MyWatchdog
                        Property              : Memory
                        HealthState           : Error
                        SequenceNumber        : 131444451657749403
                        SentAt                : 7/13/2017 6:46:05 PM
                        ReceivedAt            : 7/13/2017 6:46:05 PM
                        TTL                   : Infinite
                        Description           : 
                        RemoveWhenExpired     : False
                        IsExpired             : False
                        Transitions           : Warning->Error = 7/13/2017 6:46:05 PM, LastOk = 1/1/0001 12:00:00 AM
```

> [!NOTE]
> Hallo slecht evaluaties weergeven Hallo eerste reden Hallo entiteit is geëvalueerd toocurrent status heeft. Mogelijk zijn er meerdere andere gebeurtenissen die deze status activeren, maar worden ze niet worden doorgevoerd in Hallo evaluaties. tooget zoomen op Hallo health entiteiten toofigure uit alle slechte Hallo-rapporten in Hallo-cluster met meer informatie.
>
>

## <a name="next-steps"></a>Volgende stappen
[Gebruik system health rapporten tootroubleshoot](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)

[Aangepaste Service Fabric-statusrapporten toevoegen](service-fabric-report-health.md)

[Hoe tooreport en controleer health service](service-fabric-diagnostics-how-to-report-and-check-service-health.md)

[Controle en diagnose van lokaal services](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[Upgrade van de service Fabric-toepassing](service-fabric-application-upgrade.md)
