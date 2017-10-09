---
title: aaaManage Azure microservice load met metrische gegevens | Microsoft Docs
description: Meer informatie over hoe tooconfigure en gebruik metrische gegevens in Service Fabric toomanage brongebruik service.
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 0d622ea6-a7c7-4bef-886b-06e6b85a97fb
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 592dc749ce30683a1e439a702b7d0dc0a638276f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="managing-resource-consumption-and-load-in-service-fabric-with-metrics"></a>Het beheren van het brongebruik en de belasting in Service Fabric met metrische gegevens
*Metrische gegevens* Hallo-resources die uw services voorzichtig over en die worden geleverd door Hallo knooppunten in cluster Hallo zijn. Een metriek is iets dat u wilt dat toomanage in de volgorde tooimprove of monitor Hallo prestaties van uw services. U kunt bijvoorbeeld geheugen verbruik tooknow bekijken als uw service is overbelast. Gebruik een andere is toofigure out of Hallo-service kan verplaatsen elders waarbij geheugen is dat minder beperkt in volgorde tooget betere prestaties.

Items zoals geheugen, schijf- en CPU-gebruik zijn voorbeelden van metrische gegevens. Deze metrische gegevens zijn fysieke metrische gegevens en bronnen die overeenkomen met resources op Hallo-knooppunt dat moet worden beheerd toobe toophysical. Metrische gegevens kan ook worden (en meestal zijn) logische metrische gegevens. Logische metrische gegevens zijn bijvoorbeeld 'MyWorkQueueDepth' of 'MessagesToProcess' of 'TotalRecords'. Logische metrische gegevens zijn toepassingsspecifieke en indirect overeen toosome fysieke resourceverbruik. Logische metrische gegevens zijn algemene omdat het vaste toomeasure en het verbruik van rapport van fysieke resources op basis van de per-service kan zijn. Hallo complexiteit van het meten van en rapportage van uw eigen fysieke metrische gegevens is ook waarom Service Fabric sommige standaard metrische gegevens bevat.

## <a name="default-metrics"></a>Standaard metrische gegevens
Stel dat u wilt dat tooget schrijven en implementeren van uw service is gestart. Op dit moment weet niet welk fysieke of logische resources verbruikt. Dat is geen probleem! Hallo Service Fabric-Cluster Resource Manager maakt gebruik van bepaalde standaard metrische gegevens wanneer er geen andere waarden zijn opgegeven. Ze zijn:

  - PrimaryCount - telling van de primaire replica's op Hallo-knooppunt 
  - ReplicaCount - telling van de totale stateful replica's op Hallo-knooppunt
  - Aantal - telling van alle service-objecten (stateless en stateful) op Hallo-knooppunt

| Gegevens | Staatloze exemplaar laden | Stateful secundaire laden | Stateful primaire laden |
| --- | --- | --- | --- |
| PrimaryCount |0 |0 |1 |
| ReplicaCount |0 |1 |1 |
| Count |1 |1 |1 |

Voor algemene werkbelastingen bestaan Hallo standaard metrische gegevens uit een goede verdeling van het werk in het Hallo-cluster. In de Hallo voorbeeld te volgen, gaan we kijken wat er gebeurt als er twee services en zijn afhankelijk van Hallo standaard metrische gegevens voor netwerktaakverdeling. Hallo eerste is een stateful service met drie partities en een grootte van de drie doel replicaset. tweede Hallo-service is een staatloze met één partitie en drie exemplaren.

Dit is wat u krijgt:

<center>
![Cluster-indeling met standaard metrische gegevens][Image1]
</center>

Sommige toonote dingen:
  - Primaire replica's voor stateful service Hallo zijn verdeeld over meerdere knooppunten
  - Replica's voor dezelfde partitie worden op verschillende knooppunten Hallo
  - Hallo totale aantal primaire en secundaire replica's wordt gedistribueerd in het Hallo-cluster
  - Totaal aantal serviceobjecten Hallo worden gelijkmatig op elk knooppunt toegewezen

Goede!

Hallo standaard metrische gegevens werken geweldig als een begin. Echter worden Hallo standaard metrische gegevens alleen uitvoeren u tot nu toe. Bijvoorbeeld: Wat is er kans op Hallo Hallo partitioneren schema dat u resultaten opgenomen in perfect zelfs-gebruik door alle partities? Wat is er Hallo kans dat de belasting voor een bepaalde service Hallo constant is gedurende een bepaalde periode of zelfs Hallo dezelfde over meerdere partities nu?

U kunt uitvoeren met NET Hallo standaard metrische gegevens. Dit leidt meestal betekent echter dat het clustergebruik van uw is korter en meer ongelijke dan u wilt. Dit is omdat Hallo standaard metrische gegevens zijn niet adaptieve en wordt ervan uitgegaan dat alles is gelijk. Bijvoorbeeld, bijdragen een primaire die bezig is en één die niet beide '1' toohello PrimaryCount metriek. In het ergste geval hello, kan met alleen Hallo standaard metrische gegevens ook leiden tot overscheduled knooppunten, wat leidt tot prestatieproblemen. Als u geïnteresseerd bent in Hallo meeste uit uw cluster ophalen en prestatieproblemen te voorkomen, moet u toouse aangepaste metrische gegevens en rapportage van de dynamische belasting bij.

## <a name="custom-metrics"></a>Aangepaste metrische gegevens
Metrische gegevens zijn geconfigureerd op basis van de per-met de naam-service-exemplaar bij het maken van Hallo-service.

Een metriek heeft enkele eigenschappen beschrijving van het: een naam, een gewicht en een werklast (standaard).

* Metrische naam: naam van Hallo van Hallo metriek. Hallo metrische naam is een unieke id voor de metriek Hallo binnen Hallo cluster vanuit perspectief Hallo Resource Manager.
* Gewicht: Metrische gewicht definieert hoe belangrijk deze waarde is relatief toohello andere metrische gegevens voor deze service.
* Werklast (standaard): Hallo standaard load is verschillend, afhankelijk van de service Hallo stateless of stateful weergegeven.
  * Voor stateless services heeft elke metriek één eigenschap met de naam DefaultLoad
  * U definieert voor stateful services:
    * PrimaryDefaultLoad: de standaardhoeveelheid Hallo van deze metrische gegevens van deze service verbruikt wanneer het een primaire
    * SecondaryDefaultLoad: Hallo standaardhoeveelheid van deze metrische gegevens van deze service verbruikt wanneer deze een secundair

> [!NOTE]
> Als u aangepaste metrische gegevens definiëren en too_also_ gebruik Hallo standaard metrische gegevens gewenste, moet u too_explicitly_ Hallo standaard metrische gegevens back- en gewicht en waarden definiëren voor hen toevoegen. Dit is omdat moet u Hallo relatie tussen Hallo standaard metrische gegevens en uw aangepaste metrische gegevens definiëren. Bijvoorbeeld, misschien u het belangrijkst ConnectionCount of WorkQueueDepth meer dan primaire distributie. Standaard Hallo gewicht van Hallo PrimaryCount metriek is hoog, zodat u wilt dat tooreduce het tooMedium wanneer u andere tooensure van metrische gegevens hebben voorrang toevoegt.
>

### <a name="defining-metrics-for-your-service---an-example"></a>Metrische gegevens voor uw service - een voorbeeld definiëren
Stel dat u wilt dat Hallo na configuratie:

  - Een waarde met de naam 'ConnectionCount' uw service-rapporten
  - Wilt u er ook toouse Hallo standaard metrische gegevens 
  - U hebt gedaan sommige metingen en weten dat een primaire replica van die service gewoonlijk 20 eenheden van 'ConnectionCount duurt'
  - Secundaire replica's gebruiken "ConnectionCount" 5-eenheden
  - Weet u dat 'ConnectionCount' hello belangrijkste metrische gegevens in termen van Hallo prestaties van deze bepaalde service beheren
  - U wilt nog steeds primaire replica's met gelijke taakverdeling. Taakverdeling van de primaire replica's wordt doorgaans een goed idee ongeacht wat. Dit helpt voorkomen dat Hallo verlies van een knooppunt of fault-domein die invloed hebben op het grootste deel van de primaire replica's samen met het. 
  - Anders zijn Hallo standaard metrische gegevens fijn

Dit is Hallo code dat u toocreate een service met deze configuratie schrijven wilt:

Code:

```csharp
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
StatefulServiceLoadMetricDescription connectionMetric = new StatefulServiceLoadMetricDescription();
connectionMetric.Name = "ConnectionCount";
connectionMetric.PrimaryDefaultLoad = 20;
connectionMetric.SecondaryDefaultLoad = 5;
connectionMetric.Weight = ServiceLoadMetricWeight.High;

StatefulServiceLoadMetricDescription primaryCountMetric = new StatefulServiceLoadMetricDescription();
primaryCountMetric.Name = "PrimaryCount";
primaryCountMetric.PrimaryDefaultLoad = 1;
primaryCountMetric.SecondaryDefaultLoad = 0;
primaryCountMetric.Weight = ServiceLoadMetricWeight.Medium;

StatefulServiceLoadMetricDescription replicaCountMetric = new StatefulServiceLoadMetricDescription();
replicaCountMetric.Name = "ReplicaCount";
replicaCountMetric.PrimaryDefaultLoad = 1;
replicaCountMetric.SecondaryDefaultLoad = 1;
replicaCountMetric.Weight = ServiceLoadMetricWeight.Low;

StatefulServiceLoadMetricDescription totalCountMetric = new StatefulServiceLoadMetricDescription();
totalCountMetric.Name = "Count";
totalCountMetric.PrimaryDefaultLoad = 1;
totalCountMetric.SecondaryDefaultLoad = 1;
totalCountMetric.Weight = ServiceLoadMetricWeight.Low;

serviceDescription.Metrics.Add(connectionMetric);
serviceDescription.Metrics.Add(primaryCountMetric);
serviceDescription.Metrics.Add(replicaCountMetric);
serviceDescription.Metrics.Add(totalCountMetric);

await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("ConnectionCount,High,20,5”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

> [!NOTE]
> Hallo bovenstaande voorbeelden en hello rest van dit document worden beschreven van het beheren van metrische gegevens op basis van de per-met de naam-service. Het is ook mogelijk toodefine metrische gegevens voor uw services op Hallo service _type_ niveau. Dit wordt bereikt door op te geven ze in de manifesten voor uw service. Type niveau metrische gegevens definiëren wordt niet aanbevolen om verschillende redenen. Hallo eerste reden is dat de namen van de metrische vaak omgevingspecifiek zijn. Tenzij er een vast contract aanwezig is, mag u niet zeker dat die metriek Hallo 'Kernen' in een omgeving geen 'MiliCores' of 'Kernen' in andere gevallen. Als uw metrische gegevens zijn gedefinieerd in uw manifest moet u de nieuwe manifesten toocreate per omgeving. Dit leidt meestal tooa verspreiding van verschillende manifesten met slechts kleine verschillen, wat toomanagement problemen leiden kunnen.  
>
> Metrische belasting zijn vaak op basis van de per-met de naam-service-exemplaar toegewezen. Bijvoorbeeld, Stel dat u één exemplaar van Hallo maken voor service CustomerA toouse zal deze alleen licht. Stel ook dat u een andere maken voor CustomerB die een grotere werkbelasting heeft. In dit geval zou wilt u waarschijnlijk tootweak Hallo standaard wordt geladen voor deze services. Als u metrische gegevens laadt gedefinieerd via manifesten en u wilt dat toosupport dit scenario, vereist deze verschillende groepen van toepassingen en servicetypen voor elke klant. Hallo waarden gedefinieerd tijdens het maken van service overschrijven die zijn gedefinieerd in het manifest hello, zodat u die tooset Hallo specifieke standaardwaarden kan gebruiken. Echter dat zorgt ervoor dat Hallo-waarden die zijn gedeclareerd in Hallo manifesten toonot overeenkomen met die service Hallo daadwerkelijk wordt uitgevoerd met. Dit kan leiden tooconfusion. 
>

Als een herinnering: als u alleen toouse Hallo standaard metrische gegevens wilt, of u kunt geen tootouch Hallo metrische gegevens verzameling helemaal iets speciale doen bij het maken van uw service. Hallo standaard metrische gegevens ophalen automatisch gebruikt wanneer er geen andere worden bepaald. 

Nu gaan we door elk van deze instellingen in meer detail en bespreken Hallo gedrag op dat dit van invloed is.

## <a name="load"></a>Belasting
Hallo hele punt voor het definiëren van metrische gegevens is de toorepresent sommige belasting. *Load* hoeveel van een metriek is verbruikt door sommige service-exemplaar of de replica op een bepaald knooppunt is. Belasting kan worden geconfigureerd op bijna elk gewenst moment. Bijvoorbeeld:

  - Laden kan worden gedefinieerd als een service wordt gemaakt. Dit heet _standaard load_.
  - Hallo metrische gegevens, waaronder de standaard wordt geladen voor een service kunnen worden bijgewerkt nadat het Hallo-service wordt gemaakt. Dit heet _een service bijwerken_. 
  - Hallo belasting voor een bepaalde partitie mag reset toohello standaardwaarden voor de service. Dit heet _opnieuw instellen van belasting van partitie_.
  - Load worden gerapporteerd op een per per service object dynamisch tijdens runtime. Dit heet _reporting load_. 
  
Alle deze strategieën kan worden gebruikt binnen dezelfde service tijdens zijn levensduur Hallo. 

## <a name="default-load"></a>Werklast (standaard)
*Standaard load* hoeveel Hallo metriek elke serviceobject (stateless exemplaar of stateful replica) van deze service verbruikt is. Hallo Cluster Resource Manager gebruikt dit nummer voor Hallo belasting van de service-object Hallo totdat het andere informatie, zoals een rapport van de dynamische belasting bij ontvangt. Voor eenvoudiger services is Hallo standaard load een statische definitie. Hallo standaard load nooit is bijgewerkt en wordt gebruikt voor het Hallo-levensduur van het Hallo-service. Standaard wordt geladen works ideaal voor eenvoudige scenario's waarbij bepaalde hoeveelheden resources werkbelastingen zijn speciale toodifferent en niet wijzigen voor capaciteitsplanning.

> [!NOTE]
> Zie voor meer informatie over management capaciteit en het definiëren van capaciteit voor Hallo knooppunten in het cluster [in dit artikel](service-fabric-cluster-resource-manager-cluster-description.md#capacity).
> 

Hallo Cluster Resource Manager kunt stateful services toospecify een andere standaard belasting voor hun primaire en secundaire replica's. Stateless services kunnen slechts één waarde die van toepassing tooall exemplaren is opgeven. Voor stateful services zijn Hallo standaard load voor primaire en secundaire replica's doorgaans verschillend, omdat de replica's kunnen verschillende soorten werk in elke rol. Bijvoorbeeld primaire meestal fungeren lees- en schrijfbewerkingen en de meeste Hallo rekenkundige last, verwerken en secundaire replica's niet. Meestal is Hallo standaard load voor een primaire replica hoger dan Hallo standaard load voor secundaire replica's. Hallo echte getallen moet afhankelijk van uw eigen metingen.

## <a name="dynamic-load"></a>Dynamische belasting bij
Stel dat u uw service een tijdje hebt actief. U hebt die opgemerkt met sommige bewaking:

1. Sommige partities of verschillende exemplaren van een bepaalde service meer bronnen dan andere gebruiken
2. Sommige services een belasting die gedurende een bepaalde periode varieert.

Er is een groot aantal dingen die dergelijke fluctuaties load kunnen veroorzaken. Bijvoorbeeld, zijn verschillende services of partities gekoppeld aan verschillende klanten met verschillende vereisten. Load kan ook niet wijzigen omdat Hallo hoeveelheid werk Hallo service in de loop Hallo van Hallo dag varieert. Ongeacht of andere reden hello is er meestal geen enkel getal die u voor standaard gebruiken kunt. Dit geldt vooral als u wilt dat tooget Hallo meeste gebruik buiten het Hallo-cluster. Een waarde die u voor de werklast (standaard kiest) is onjuist aantal Hallo tijd. Onjuiste standaardinstellingen laadt leiden tot een Cluster Resource Manager Hallo boven of onder het toewijzen van resources. Als gevolg hiervan hebt u knooppunten die boven of onder benut worden Hoewel Hallo Cluster Resource Manager denkt dat het Hallo-cluster is verdeeld. Standaard laadt zijn nog steeds goed, omdat ze bepaalde informatie voor de eerste positie bieden, maar ze nog niet voltooid verhaal voor echte werkbelastingen. tooaccurately vastleggen wijzigen bronvereisten, Hallo Cluster Resource Manager kunt elke service object tooupdate eigen load tijdens runtime. Dit de dynamische belasting bij reporting wordt genoemd.

Rapporten van de dynamische belasting bij toestaan replica's of exemplaren tooadjust hun toewijzing/gerapporteerd belasting van metrische gegevens gedurende hun levensduur. Meestal rapporteren dat het lage hoeveelheden een metriek is geïnstalleerd via een replica van de service of het exemplaar dat koude en niet doen. Een bezet replica of instance rapporteren dat ze meer gebruiken.

Reporting load per replica of het exemplaar, kunnen Hallo Cluster Resource Manager tooreorganize Hallo afzonderlijke serviceobjecten in Hallo-cluster. Hallo-services opnieuw indelen, kunt ervoor zorgen dat ze Hallo-resources die ze nodig hebben. Bezet krijgen effectief te 'vrijmaken' bronnen van andere replica's of exemplaren die momenteel koude of minder werk te doen.

Binnen Reliable Services uitziet Hallo code tooreport load dynamisch:

Code:

```csharp
this.Partition.ReportLoad(new List<LoadMetric> { new LoadMetric("CurrentConnectionCount", 1234), new LoadMetric("metric1", 42) });
```

Een service kan rapporteren dat op een van de Hallo metrische gegevens die zijn gedefinieerd tijdens het maken. Als een service-rapporten belasting voor een waarde die het is niet geconfigureerd toouse, negeert Service Fabric die rapporteren. Als er andere metrische gegevens gerapporteerd op Hallo dezelfde tijd die geldig zijn, die rapporten worden geaccepteerd. Service-code kunt meten en rapporteren alle Hallo metrische gegevens die deze procedures, en operators Hallo configuratie toouse zonder toochange Hallo servicecode kunnen opgeven. 

### <a name="updating-a-services-metric-configuration"></a>Configuratie van een service bijwerken
Hallo-lijst van metrische gegevens die zijn gekoppeld aan Hallo-service en Hallo eigenschappen van deze metrische gegevens kunnen dynamisch worden bijgewerkt terwijl Hallo service live. Hiermee om te experimenteren en flexibiliteit. Enkele voorbeelden van wanneer dit handig is zijn:

  - een metriek met een buggy rapport voor een bepaalde service uitschakelen
  - Hallo-gewicht van de metrische gegevens op basis van het gewenste gedrag opnieuw configureren
  - inschakelen van een nieuwe waarde pas nadat Hallo code al is geïmplementeerd en gevalideerd via andere methoden
  - Hallo standaard load voor een service op basis van waargenomen gedrag en het verbruik van wijzigen

Hallo belangrijkste API's voor het wijzigen van de configuratie zijn `FabricClient.ServiceManagementClient.UpdateServiceAsync` in C# en `Update-ServiceFabricService` in PowerShell. Welke informatie u met deze API's opgeeft vervangt bestaande Hallo metrische gegevens voor Hallo service onmiddellijk. 

## <a name="mixing-default-load-values-and-dynamic-load-reports"></a>De combinatie van waarden van standaard load en rapporten van de dynamische belasting bij
Standaard-belasting en de dynamische belasting kunnen worden gebruikt voor Hallo dezelfde service. Wanneer een service maakt gebruik van zowel de werklast (standaard) en de dynamische belasting bij rapporten, wordt standaard load fungeert als een schatting totdat u dynamische rapporten worden weergegeven. Standaard load is goed, omdat dit Hallo Cluster Resource Manager is er iets toowork met biedt. Hallo standaard load kunt Hallo Cluster Resource Manager tooplace Hallo-objecten in goede locaties wanneer ze worden gemaakt. Als er geen standaard-informatie laden is opgegeven, wordt een effectief willekeurige plaatsing van services. Bij het ontvangen van load-rapporten later Hallo initiële willekeurige plaatsing is vaak verkeerde en Hallo Cluster Resource Manager toomove services heeft.

We nemen van het vorige voorbeeld en zien wat er gebeurt wanneer we enkele aangepaste metrische gegevens en de dynamische belasting bij reporting toevoegt. In dit voorbeeld gebruiken we 'MemoryInMb' als een voorbeeld van de meting.

> [!NOTE]
> Geheugen is een Hallo system metrische gegevens die Service Fabric kunt [resource reguleren](service-fabric-resource-governance.md), en uzelf reporting is doorgaans moeilijk. We niet daadwerkelijk verwacht dat u tooreport op geheugenverbruik; Geheugen wordt gebruikt als een toolearning hulp over de mogelijkheden van Hallo Hallo Cluster Resource Manager hier.
>

We gaan ervan uit dat we in eerste instantie Hallo stateful service gemaakt met de volgende opdracht Hallo:

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton –Metric @("MemoryInMb,High,21,11”,"PrimaryCount,Medium,1,0”,"ReplicaCount,Low,1,1”,"Count,Low,1,1”)
```

Deze syntaxis is als een herinnering (MetricName, MetricWeight, PrimaryDefaultLoad, SecondaryDefaultLoad').

Kijken wat een mogelijke cluster indeling kan er als volgt uitzien:

<center>
![Cluster Gebalanceerd met zowel standaard als aangepaste metrische gegevens][Image2]
</center>

Een aantal zaken die opgemerkt zijn:

* Secundaire replica's binnen een partitie kunnen hebben hun eigen laden
* De algemene zoek Hallo metrische gegevens taakverdeling. Hallo voor geheugen, de verhouding tussen Hallo maximale en minimale belasting is 1,75 (Hallo knooppunt Hello meeste load is N3, Hallo minste N2 en 28/16 = 1,75).

Er zijn wordt nog steeds tooexplain moet een aantal zaken:

* Wat bepaald of een ratio van 1,75 redelijke of niet is? Hoe weet Hallo Cluster Resource Manager als die voldoende is of als er meer werk toodo?
* Wanneer balancing treedt?
* Wat betekent dit dat geheugen 'Hoog' werd gewogen?

## <a name="metric-weights"></a>Metrische gewichten
Bijhouden Hallo dezelfde metrische gegevens naar verschillende services is belangrijk. Globale weergave is wat Hallo Cluster Resource Manager tootrack verbruik in Hallo cluster en zorg ervoor dat de knooppunten niet gaan over capaciteit verbruik op alle knooppunten in balans is toegestaan. Services kunnen echter verschillende weergaven hebben als de urgentie toohello Hallo dezelfde metrische gegevens. Ook in een cluster met veel metrische gegevens en partijen van services, perfect taakverdeling oplossingen bestaat mogelijk niet voor alle metrische gegevens. Hoe moet Hallo Cluster Resource Manager in deze situaties verwerken?

Metrische gewichten toestaan Hallo Cluster Resource Manager toodecide hoe toobalance Hallo cluster wanneer er wordt niet perfect opgenomen. Metrische gewichten ook de mogelijkheid Hallo Cluster Resource Manager toobalance specifieke services anders. Metrische gegevens kunt laten vier verschillende gewicht niveaus: nul, laag, gemiddeld en hoog. Een metriek met een gewicht van nul bijdraagt niets wanneer u overweegt of dingen of niet evenwicht zijn. De belasting wordt echter nog steeds bij toocapacity management. Metrische gegevens met nul gewicht zijn nog steeds nuttig en worden vaak gebruikt als onderdeel van het servicegedrag en prestatiebewaking. [In dit artikel](service-fabric-diagnostics-event-generation-infra.md) bevat meer informatie over het gebruik van metrische gegevens voor het bewaken van Hallo en diagnostische gegevens van uw services. 

Hallo heeft echte verschillende metrische gewichten in Hallo cluster dat verschillende oplossingen die Hallo Cluster Resource Manager worden gegenereerd. Metrische gewichten Vertel Hallo Cluster Resource Manager dat bepaalde metrische gegevens belangrijker dan andere zijn. Wanneer er geen Hallo ideale oplossing Cluster Resource Manager kunt geven de voorkeur oplossingen die Hallo hoger gewogen metrische gegevens beter kan worden verdeeld. Als een service denkt een bepaalde waarde is niet belangrijk is dat, dat kan dit het gebruik van deze metrische gegevens van imbalanced vinden. Hierdoor kan een gelijke verdeling van sommige metrische gegevens die belangrijk tooit van een andere service tooget.

Bekijk een voorbeeld van sommige rapporten laden en hoe verschillende metriek gewicht resulteert in een andere toewijzingen aan in het Hallo-cluster. In dit voorbeeld zien we dat relatieve gewicht van metrische gegevens Hallo Hallo overschakelen zorgt ervoor Hallo Cluster Resource Manager toocreate verschillende regelingen van services dat.

<center>
![Voorbeeld van de metrische gewicht en de invloed ervan op oplossingen Netwerktaakverdeling][Image3]
</center>

In dit voorbeeld zijn er vier verschillende services, alle reporting verschillende waarden voor twee verschillende maatstaven voor MetricA en MetricB. In één geval alle Hallo services definiëren MetricA is Hallo belangrijkste (gewicht = hoog) en MetricB als niet belangrijk (gewicht = laag). Als gevolg hiervan zien we dat Hallo Cluster Resource Manager Hallo services plaatst zodat MetricA beter dan MetricB taakverdeling is. 'Beter taakverdeling' betekent dat MetricA een lagere heeft heeft een lagere standaarddeviatie dan MetricB. In het tweede geval Hallo omkeren we Hallo metrische gewichten. Als gevolg hiervan wisselt Hallo Cluster Resource Manager services A en B toocome up met een-toewijzing waar MetricB is een betere taakverdeling dan MetricA.

> [!NOTE]
> Metrische gewichten bepalen hoe Hallo Cluster Resource Manager moet worden verdeeld, maar niet wanneer balancing moet gebeuren. Bekijk voor meer informatie over Netwerktaakverdeling, [in dit artikel](service-fabric-cluster-resource-manager-balancing.md)
>

### <a name="global-metric-weights"></a>Globale metrische gewichten
Stel dat ServiceA definieert MetricA zoals hoge gewicht en XPb stelt Hallo gewicht voor MetricA tooLow of nul. Wat is Hallo werkelijke gewicht dat belandt ophalen gebruikt?

Er zijn meerdere gewichten die worden voor elke metriek bijgehouden. de eerste gewicht Hallo is Hallo een gedefinieerd voor de metriek Hallo wanneer Hallo-service wordt gemaakt. Hallo is andere gewicht een globale gewicht, wordt automatisch berekend. Hallo Cluster Resource Manager gebruikt deze beide gewichten wanneer score berekenen voor oplossingen. Het is belangrijk rekening houdend met beide gewichten. Hierdoor kan Hallo Cluster Resource Manager toobalance elke service volgens tooits prioriteiten eigenaar en zorg er ook dat cluster Hallo als geheel juist is toegewezen.

Wat er gebeurt als Hallo Cluster Resource Manager globale en lokale saldo niet interesseren? Het is ook eenvoudig tooconstruct oplossingen die globaal in evenwicht zijn, maar die leiden tot slechte resourceverdeling voor afzonderlijke services. In Hallo voorbeeld te volgen, gaan we kijken naar een service die is geconfigureerd met NET Hallo standaard metrische gegevens en kijk wat er gebeurt wanneer alleen globale saldo wordt beschouwd als:

<center>
![Hallo gevolgen van een globale oplossing alleen][Image4]
</center>

Hallo cluster als geheel wordt in Hallo bovenste bijvoorbeeld op basis van de globale saldo inderdaad verdeeld. Alle knooppunten hebben Hallo dezelfde primaire aantal en dezelfde Hallo number totaal aantal replica's. Echter, als u hello werkelijke gevolgen van deze toewijzing bekijkt is het niet zo goed: Hallo verlies van een willekeurig knooppunt van invloed is op een bepaalde belasting, omdat het duurt alle van de primaire voordat. Bijvoorbeeld, als het eerste knooppunt Hallo Hallo drie primaire voor drie verschillende partities Hallo Hallo cirkel-service mislukt is alle verbroken. Als u daarentegen hebben Hallo driehoek en zeshoek services hun partities verliezen van een replica. Dit zorgt ervoor dat behalve toorecover Hallo omlaag replica wordt niet onderbroken.

Hallo Cluster Resource Manager heeft Hallo onder bijvoorbeeld Hallo replica's op basis van beide Hallo globale en per service saldo gedistribueerd. Dit biedt de meeste Hallo gewicht toohello globale oplossing en een tooindividual (configureerbaar) gedeelte services bij het berekenen van de score van de oplossing Hallo Hallo. Globale verdelen voor een waarde wordt berekend op basis van gemiddelde Hallo van Hallo metrische gewicht van elke service. Elke service, wordt volgens tooits eigen gedefinieerde metrische gewichten verdeeld. Dit zorgt ervoor dat Hallo-services worden afgewogen tegen binnen zelf volgens tootheir eigen behoeften. Als gevolg hiervan wordt als hello dezelfde eerste knooppunt Hallo fout mislukt verdeeld over alle partities van alle services. Hallo impact tooeach is dezelfde Hallo.

## <a name="next-steps"></a>Volgende stappen
- Voor meer informatie over het configureren van services, [informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)(service-fabric-cluster-resource-manager-configure-services.md)
- Defragmentatie metrische gegevens definiëren is eenrichtingssessie tooconsolidate belasting van de knooppunten in plaats van af te spreiden. toolearn hoe tooconfigure defragmentatie, raadpleeg dan te[in dit artikel](service-fabric-cluster-resource-manager-defragmentation-metrics.md)
- toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)
- Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)
- Verplaatsingkosten is één manier toohello Cluster Resource Manager-signalering dat bepaalde services zijn duurder toomove dan andere. toolearn meer informatie over verplaatsingskosten, Raadpleeg te[in dit artikel](service-fabric-cluster-resource-manager-movement-cost.md)

[Image1]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-cluster-layout-with-default-metrics.png
[Image2]:./media/service-fabric-cluster-resource-manager-metrics/Service-Fabric-Resource-Manager-Dynamic-Load-Reports.png
[Image3]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-metric-weights-impact.png
[Image4]:./media/service-fabric-cluster-resource-manager-metrics/cluster-resource-manager-global-vs-local-balancing.png
