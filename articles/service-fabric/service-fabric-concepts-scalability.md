---
title: aaaScalability van Service Fabric-services | Microsoft Docs
description: Hierin wordt beschreven hoe tooscale Service Fabric-services
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: ed324f23-242f-47b7-af1a-e55c839e7d5d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 5af06f8f71ad5dee32ba115b922842684867e654
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-in-service-fabric"></a>Schalen in Service Fabric
Azure Service Fabric maakt het eenvoudig toobuild schaalbare toepassingen door het beheer van services hello, partities en replica's op Hallo knooppunten van een cluster. Veel werkbelastingen uitgevoerd op dezelfde hardware schakelt maximale Resourcegebruik hello, maar ook biedt flexibiliteit in termen van hoe u tooscale uw werkbelastingen kiezen. 

In Service Fabric schalen, is het moet worden uitgevoerd op verschillende manieren:

1. Schalen door te maken of te verwijderen van staatloze service-exemplaren
2. Schalen door te maken of verwijderen van nieuwe services met de naam
3. Schalen door te maken of te verwijderen, nieuwe exemplaren van een toepassing met de naam
4. Met behulp van gepartitioneerde services schalen
5. Schalen door toevoegen en verwijderen van knooppunten uit Hallo-cluster 
6. Schalen met behulp van de Cluster Resource Manager metrische gegevens

## <a name="scaling-by-creating-or-removing-stateless-service-instances"></a>Schalen door te maken of te verwijderen van staatloze service-exemplaren
Een van de meest eenvoudige manieren tooscale in Service Fabric Hallo werkt met stateless services. Als u een stateless service maakt, krijgt u een toodefine kans op een `InstanceCount`. `InstanceCount`Hiermee definieert u hoeveel actieve exemplaren van de code van de service worden gemaakt wanneer het Hallo-service wordt gestart. Stel bijvoorbeeld dat er 100 knooppunten beschikbaar in Hallo-cluster zijn. Stel dat een service hebt gemaakt met een `InstanceCount` van 10. Tijdens runtime, die 10 actieve exemplaren van Hallo code zou kunnen alle worden bezet (of kunnen niet genoeg bezet). Eenzijdige tooscale werkbelasting toochange Hallo aantal exemplaren is. Bijvoorbeeld een blok van code voor bewaking of management Hallo bestaande aantal exemplaren too50 of too5 wijzigen, afhankelijk van of Hallo werkbelasting tooscale in- of uitzoomen op basis van Hallo moet worden geladen. 

C#:

```csharp
StatelessServiceUpdateDescription updateDescription = new StatelessServiceUpdateDescription(); 
updateDescription.InstanceCount = 50;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/app/service"), updateDescription);
```

PowerShell:

```posh
Update-ServiceFabricService -Stateless -ServiceName $serviceName -InstanceCount 50
```
### <a name="using-dynamic-instance-count"></a>Met behulp van dynamische exemplaren
Service Fabric biedt een automatische manier toochange Hallo-exemplaren specifiek voor stateless services. Hierdoor Hallo service tooscale dynamisch met Hallo aantal knooppunten die beschikbaar zijn. Hallo manier tooopt in dit gedrag is tooset Hallo exemplaren = -1. InstanceCount = -1 is een instructie tooService Fabric met de tekst 'Deze staatloze service uitvoeren op elk knooppunt'. Als het aantal knooppunten hello wordt gewijzigd, Service Fabric automatisch gewijzigd Hallo exemplaar aantal toomatch ervoor te zorgen dat Hallo-service wordt uitgevoerd op alle geldige knooppunten. 

C#:

```csharp
StatelessServiceDescription serviceDescription = new StatelessServiceDescription();
//Set other service properties necessary for creation....
serviceDescription.InstanceCount = -1;
await fc.ServiceManager.CreateServiceAsync(serviceDescription);
```

PowerShell:

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName -Stateless -PartitionSchemeSingleton -InstanceCount "-1"
```

## <a name="scaling-by-creating-or-removing-new-named-services"></a>Schalen door te maken of verwijderen van nieuwe services met de naam
Een benoemd exemplaar van een specifiek exemplaar van een servicetype is (Zie [levenscyclus van de Service Fabric-toepassing](service-fabric-application-lifecycle.md)) binnen een aantal benoemde toepassingsexemplaar in Hallo-cluster. 

Nieuwe benoemde service-exemplaren kunnen worden gemaakt (of verwijderd) als services komen meer of minder bezet. Hierdoor worden aanvragen toobe verdeeld over meer service-exemplaren, meestal waardoor de belasting van bestaande services toodecrease. Bij het maken van services, plaatst Hallo Service Fabric-Cluster Resource Manager Hallo services in een gedistribueerde wijze Hallo cluster. Hallo exacte beslissingen vallen Hallo [metrische gegevens](service-fabric-cluster-resource-manager-metrics.md) in Hallo-cluster en andere plaatsingsregels. Services kunnen op verschillende manieren worden gemaakt, maar hello meest voorkomende zijn via beheeracties als iemand het aanroepen van [ `New-ServiceFabricService` ](https://docs.microsoft.com/en-us/powershell/module/servicefabric/new-servicefabricservice?view=azureservicefabricps), of door code aanroepen [ `CreateServiceAsync` ](https://docs.microsoft.com/en-us/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync?view=azure-dotnet). `CreateServiceAsync`kan zelfs worden aangeroepen vanuit binnen andere services in Hallo cluster wordt uitgevoerd.

Maken van services dynamisch kunnen worden gebruikt in allerlei scenario's en is een algemene patroon. Neem bijvoorbeeld een stateful service die staat voor een bepaalde workflow. Aanroepen werk die gaat tooshow toothis service en deze service is momenteel tooexecute Hallo stappen toothat werkstroom en record uitgevoerd. 

Hoe wilt u deze schaal bepaalde service maken Hallo-service kan multitenant in een vorm en accepteert aanroepen en ere van stappen voor veel verschillende exemplaren van Hallo dezelfde werkstroom in één keer. Dat kan nog wel Hallo code complexere sinds nu deze tooworry over veel verschillende exemplaren van Hallo heeft dezelfde werkstroom, allemaal in verschillende stadia en van verschillende klanten. Afhandeling van meerdere werkstromen op hetzelfde moment niet wordt opgelost Hallo Hallo ook scale probleem. Dit is omdat op een bepaald moment deze service te veel resources toofit op een bepaalde computer verbruikt. Veel services niet zijn ingebouwd voor dit patroon in de eerste plaats Hallo ook ondervindt vervaldatum toosome inherente knelpunt of vertraging in de code. Dit soort problemen veroorzaken Hallo-service niet toowork ook wanneer het aantal gelijktijdige werkstromen, die is het bijhouden Hallo groter opgehaald.  

Een oplossing is toocreate een exemplaar van deze service voor elk ander exemplaar van de werkstroom Hallo gewenste tootrack. Dit is een uitstekende patroon en of Hallo service stateless of stateful werkt. Er is meestal een andere service die als een 'van Workload Manager-Service fungeert' voor deze toowork patroon. Hallo-taak van deze service is tooreceive aanvragen en tooroute die aanvragen tooother-services. Hallo manager kan een exemplaar van Hallo werkbelasting service dynamisch maken wanneer het Hallo-bericht ontvangt en geeft u op aanvragen toothose services. Hallo manager-service kan ook retouraanroepen ontvangen wanneer een bepaalde workflow-service de taak is voltooid. Wanneer Hallo manager de retouraanroepen ontvangt kan het verwijderen van dit exemplaar van Hallo workflowservice of laat het als aanroepen meer verwacht. 

Advanced-versie van dit type manager kunnen zelfs pools van Hallo-services die deze beheert maken. Hallo-groep zorgt ervoor dat wanneer een nieuwe aanvraag wordt geleverd geen toowait voor Hallo service toospin up heeft. In plaats daarvan kan Hallo manager alleen kiezen van een werkstroomservice die niet uit de groep Hallo is momenteel bezet of routeren willekeurig. Een pool van services beschikbaar te houden kunt u nieuwe aanvragen voor de verwerking sneller, omdat het minder waarschijnlijk dat Hallo-aanvraag heeft toowait voor een nieuwe service toobe ingezet. Maken van nieuwe services is snel, maar niet beschikbaar of momentopname. Hallo groep helpt te beperken Hallo tijdsduur Hallo-aanvraag toowait heeft voordat het wordt onderhouden. Vaak ziet u dit patroon manager en de pool wanneer reactietijden Hallo belangrijkst. Queuing Hallo-aanvraag en maken Hallo-service op de achtergrond Hallo en _vervolgens_ doorgeeft op is ook een patroon populaire manager maken en-services op basis van bepaalde bijhouden van Hallo hoeveelheid werk die service momenteel verwijderen is in behandeling. 

## <a name="scaling-by-creating-or-removing-new-named-application-instances"></a>Schalen door te maken of te verwijderen, nieuwe exemplaren van een toepassing met de naam
Maken en het verwijderen van de hele toepassingsexemplaren is vergelijkbaar toohello patroon van het maken en -services verwijderen. Er is deel van de service manager die Hallo besluit op basis van Hallo-aanvragen die deze ziet aan te brengen en Hallo informatie deze ontvangt van andere services binnen het cluster Hallo Hallo voor dit patroon. 

Wanneer u een nieuw toepassingsexemplaar van de benoemde moet worden gebruikt in plaats van een nieuwe benoemde service-exemplaren in een reeds bestaande toepassingen maken? Er is een enkele gevallen:

  * Nieuwe toepassingsexemplaar Hallo is voor een klant waarvan de code toorun onder een bepaalde identiteit of beveiligingsinstellingen moet.
    * Service Fabric Hiermee kunt u andere code pakketten toorun onder bepaalde identiteiten definiëren. In de volgorde toolaunch hello dezelfde codepakket onder verschillende id's, Hallo activeringen moeten toooccur in exemplaren van een andere toepassing. U kunt een aanvraag waarin het hebben van een bestaande klant werkbelastingen die zijn geïmplementeerd. Deze kunnen worden uitgevoerd onder een bepaalde identiteit zodat u kunt bewaken en beheren van hun toegang tooother-resources, zoals externe databases of andere systemen. In dit geval als een nieuwe klant zich aanmeldt, u waarschijnlijk niet wilt dat tooactivate hun code in Hallo dezelfde context (procesruimte). Terwijl u kan wordt hierdoor het moeilijker voor uw service code tooact in Hallo context van een bepaalde identiteit. Normaal gesproken moet u meer beveiliging, isolatie- en identity management-code hebben. In plaats van het gebruik van verschillende service benoemde exemplaren binnen hetzelfde toepassingsexemplaar hello en daarom Hallo dezelfde procesruimte, kunt u verschillende benoemde exemplaren van Service Fabric-toepassing. Dit maakt het eenvoudiger toodefine andere identiteit contexten.
  * Nieuwe toepassingsexemplaar Hallo fungeert ook als een middel van configuratie
    * Standaard wordt alle Hallo benoemde exemplaren van een bepaalde servicetype binnen een exemplaar van de service uitgevoerd in dezelfde op een bepaald knooppunt verwerken Hallo. Dit betekent dat terwijl u elk service-exemplaar anders configureren kunt, orde ingewikkeld is. Sommige token die ze gebruiken toolook hun Configuration binnen een configuratiepakket hebben. Meestal is dit alleen de naam van het Hallo-service. Dit werkt prima, maar Hallo configuratienamen toohello van Hallo afzonderlijke benoemde service-exemplaren in dat toepassingsexemplaar worden gekoppeld. Dit kan verwarrend en vaste toomanage sinds de configuratie is meestal een artefact ontwerp tijd met specifieke waarden van toepassing exemplaar. Meer services maakt altijd, meer toepassingsupgrades toochange Hallo informatie binnen Hallo config pakketten of toodeploy nieuwe zodat Hallo nieuwe services kunnen worden opgezocht hun specifieke informatie. Het is vaak eenvoudiger toocreate een geheel nieuw benoemde exemplaar. Vervolgens kunt u Hallo toepassing parameters tooset welke configuratie is noodzakelijk voor Hallo-services. Op deze manier alle Hallo-services die in die zijn gemaakt met de naam toepassingsexemplaar kan bepaalde configuratie-instellingen overnemen. Bijvoorbeeld, in plaats van een enkel configuratiebestand met Hallo-instellingen en aanpassingen voor elke klant, zoals geheimen of per klant limieten, hebt in plaats daarvan u een exemplaar van de verschillende groepen van toepassingen voor elke klant met deze instellingen overschreven. 
  * de nieuwe toepassing Hello fungeert als een grens voor upgrade
    * In Service Fabric fungeren exemplaren van een andere benoemde toepassing als grenzen voor de upgrade. Hallo-code die een ander toepassingsexemplaar van de benoemde wordt uitgevoerd heeft geen invloed op een upgrade van een benoemde exemplaar. Hallo verschillende toepassingen uiteindelijk met verschillende versies van dezelfde code Hallo op Hallo dezelfde knooppunten. Dit kan een factor zijn wanneer u toomake een vergroten/verkleinen beslissing nodig omdat u kiezen kunt dat of nieuwe code Hallo Hallo moet volgen hetzelfde als een andere service upgrades of niet. Stel dat een aanroep van Hallo manager-service die verantwoordelijk is voor het schalen van een bepaalde klant werkbelastingen door te maken en verwijderen van services dynamisch aankomt. In dit geval echter Hallo-aanroep is voor een werkbelasting die is gekoppeld aan een _nieuwe_ klant. De meeste klanten dat ze van elkaar zijn afgezonderd niet alleen omwille van de Hallo beveiliging en configuratie dat eerder is vermeld, maar omdat deze biedt meer flexibiliteit in termen van met specifieke versies van het Hallo-software en kiezen wanneer ze ophalen bijgewerkt. U kunt ook een nieuw exemplaar van de toepassing en Hallo service maken er gewoon toofurther partitie Hallo bedrag van de services die elk één upgrade blijven. Exemplaren van een afzonderlijke toepassing groter granulariteit bieden bij het uitvoeren van toepassingsupgrades en ook inschakelen A / B-tests en blauw/groen-implementaties. 
  * Hallo bestaande toepassingsexemplaar is vol
    * In Service Fabric [toepassing capaciteit](service-fabric-cluster-resource-manager-application-groups.md) een concept is dat u toocontrol Hallo hoeveelheid beschikbare bronnen voor exemplaren van een bepaalde toepassing kunt gebruiken. U kunt bijvoorbeeld besluiten dat een bepaalde service toohave een ander exemplaar in volgorde tooscale gemaakt moet. Dit toepassingsexemplaar valt echter buiten capaciteit voor een bepaalde waarde. Als deze specifieke klant of de werkbelasting moet nog steeds worden toegekend meer resources, kan klikt u vervolgens u bestaande capaciteit voor die toepassing hello verhogen of maak een nieuwe toepassing. 

## <a name="scaling-at-hello-partition-level"></a>Schalen op Hallo partitie niveau
Service Fabric ondersteunt partitionering. Partitioneren van splitst een service in meerdere logische en fysieke secties, die elk onafhankelijk werkt. Dit is handig voor stateful services, omdat er geen ingesteld van replica's heeft toohandle alle Hallo aanroepen en het bewerken van alle Hallo status in één keer. Hallo [overzicht partitioneren](service-fabric-concepts-partitioning.md) bevat informatie over Hallo typen partitionering schema's die worden ondersteund. Hallo-replica's van elke partitie worden verdeeld over Hallo-knooppunten in een cluster, het distribueren van die service laden en ervoor te zorgen dat geen van beide Hallo-service in zijn geheel of elke partitie een potentieel risico heeft. 

Houd rekening met een service die gebruikmaakt van een ranged partitieschema met een lage sleutel van 0, een hoge sleutel 99, en een aantal partities van 4. In een cluster met drie knooppunten mogelijk Hallo-service worden ingedeeld met vier replica's die Hallo bronnen op elk knooppunt delen als volgt te werk:

<center>
![Partitie-indeling met drie knooppunten](./media/service-fabric-concepts-scalability/layout-three-nodes.png)
</center>

Als u het aantal knooppunten Hallo verhoogt, wordt het Service Fabric enkele Hallo bestaande replica's er verplaatsen. Stel dat bijvoorbeeld het aantal knooppunten Hallo verhoogt toofour en Hallo replica's ophalen gedistribueerd. Nu Hallo-service heeft nu de drie replica's die worden uitgevoerd op elk knooppunt, elk die deel uitmaken van toodifferent partities. Hiermee kunt beter brongebruik omdat Hallo nieuw knooppunt wordt niet koude. Normaal gesproken ook verbetert de prestaties als elke service meer resources beschikbaar tooit heeft.

<center>
![Partitie-indeling met vier knooppunten](./media/service-fabric-concepts-scalability/layout-four-nodes.png)
</center>

## <a name="scaling-by-using-hello-service-fabric-cluster-resource-manager-and-metrics"></a>Schalen met behulp van Hallo Service Fabric-Cluster Resource Manager en metrische gegevens
[Metrische gegevens](service-fabric-cluster-resource-manager-metrics.md) hoe services hun resource verbruik tooService Fabric express zijn. Met metrische gegevens Hallo Cluster Resource Manager biedt een kans tooreorganize en optimaliseren Hallo lay-out van Hallo-cluster. Bijvoorbeeld, kunnen er voldoende bronnen in Hallo-cluster, maar ze niet toohello-services die momenteel werk doen worden toegewezen. Hallo Cluster Resource Manager tooreorganize Hallo cluster tooensure dat services toegang hebben met metrische gegevens kunt toohello beschikbare bronnen. 


## <a name="scaling-by-adding-and-removing-nodes-from-hello-cluster"></a>Schalen door toevoegen en verwijderen van knooppunten uit Hallo-cluster 
Een andere optie voor schaling mogelijk met Service Fabric is toochange Hallo grootte van Hallo-cluster. Hallo grootte wijzigen van de cluster Hallo betekent toevoegen of verwijderen van knooppunten voor een of meer van de knooppunttypen Hallo in Hallo-cluster. Neem bijvoorbeeld een aanvraag waarin alle knooppunten in cluster Hallo Hallo hot zijn. Dit betekent dat Hallo clusterbronnen bijna alle verbruikt zijn. In dit geval is toe te voegen meer knooppunten toohello-cluster de beste manier tooscale Hallo. Zodra nieuwe knooppunten Hallo join Hallo cluster Hallo verplaatst Service Fabric-Cluster Resource Manager services toothem, wat resulteert in minder totale belasting van bestaande Hallo-knooppunten. Voor stateless services met het aantal exemplaren =-1, meer service exemplaren automatisch worden gemaakt. Hierdoor kunnen sommige toomove aanroepen van Hallo bestaande knooppunten toohello nieuwe knooppunten. 

Toevoegen en verwijderen van knooppunten toohello kan cluster via Hallo Service Fabric Azure Resource Manager PowerShell-module worden uitgevoerd.

```posh
Add-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName  -NumberOfNodesToAdd 5 
Remove-AzureRmServiceFabricNode -ResourceGroupName $resourceGroupName -Name $clusterResourceName -NodeType $nodeTypeName -NumberOfNodesToRemove 5
```

## <a name="putting-it-all-together"></a>Kort samengevat
U gaat nu alle Hallo ideeën hebt die hier worden besproken en communiceren via een voorbeeld. Overweeg Hallo volgende service: u toobuild een service die fungeert als een adresboek probeert op toonames-en contactgegevens te houden. 

Rechts vooraf hebt u een aantal vragen gerelateerde tooscale: hoeveel gebruikers zijn u gaat toohave? Hoeveel contactpersonen slaat elke gebruiker? Toofigure probeert dit alle af is wanneer u zijn permanent van uw service voor Hallo eerst moeilijk. Stel dat u toogo met een enkele statische service met een specifieke partitie telling ging. Hallo gevolgen van het verzamelen van onjuist aantal partities kan ervoor zorgen dat u toohave hello later schalen van problemen. Op dezelfde manier, zelfs als u kiest Hallo rechts aantal die u niet bent mogelijk alle Hallo informatie moet u. Bijvoorbeeld, hebben u ook toodecide Hallo grootte van Hallo cluster vooraf, zowel op het gebied Hallo aantal knooppunten en de grootte. De meestal harde toopredict hoeveel resources een service gaat tooconsume tijdens zijn levensduur. Het kan ook worden vaste tooknow tevoren tijd Hallo verkeer patroon Hallo service daadwerkelijk ziet. Bijvoorbeeld, mogelijk mensen toevoegen en verwijderen van hun contactpersonen alleen eerst te beginnen in Hallo ochtend of mogelijk deze wordt evenredig verdeeld in de loop Hallo van Hallo dag. Op basis hiervan u tooscale out en in dynamisch moet mogelijk. U leert toopredict mogelijk wanneer u gaat tooneed tooscale out en in, maar in beide gevallen u waarschijnlijk tooneed tooreact toochanging verbruik door uw service gaat. Dit kan betrekking hebben op Hallo grootte wijzigen van Hallo-cluster in volgorde tooprovide meer bronnen bij het gebruik van bestaande resources opnieuw indelen niet voldoende. 

Maar zelfs probeer waarom toopick geen enkele partitieschema uit voor alle gebruikers? Waarom beperken zelf tooone service en een statische cluster? Hallo echte situatie is meestal meer dynamische. 

Wanneer u voor schaal, overweeg Hallo dynamische patroon volgen. Mogelijk moet u tooadapt deze tooyour situatie:

1. In plaats van probeert toopick een partitieschema voor iedereen vooraf, bouwt u een 'manager-service'.
2. Hallo-taak van de service manager Hallo is toolook op klantgegevens wanneer ze zich registreren voor uw service. Vervolgens, afhankelijk van deze informatie Hallo manager-service geen exemplaar maken van uw _werkelijke_ Neem contact op met storage-service _alleen voor die klant_. Als ze specifieke configuratie-, isolatie- of upgrades vereist, kunt u ook toospin van instantie van een toepassing bepalen voor de klant. 

Het maken van deze dynamische patroon veel voordelen:

  - U probeert niet tooguess Hallo juiste partitie aantal voor alle gebruikers van tevoren of bouwen van een service waarmee is oneindig schaalbare alle op zichzelf. 
  - Andere gebruikers hoeven geen toohave Hallo dezelfde partitie aantal, aantal replica's, plaatsingsbeperkingen, metrische gegevens, standaard laadt, servicenamen, DNS-instellingen of een van de Hallo andere eigenschappen gespecificeerd worden op Hallo service- of toepassingsniveau. 
  - Krijgt u extra gegevens segmentering. Elke klant heeft een eigen kopie van het Hallo-service
    - Elke klantenservice worden anders geconfigureerd en meer of minder bronnen, met meer of minder partities of replica's zo nodig op basis van hun verwachte schaal verleend.
      - Bijvoorbeeld, Hallo klant betaald Hallo 'Gold' laag: ze meer replica's of een groter aantal van de partities kunnen ophalen en mogelijk resources tootheir services via de metrische gegevens en toepassingen capaciteit toegewezen.
      - Of spreek ze opgegeven informatie die aangeeft Hallo aantal contactpersonen die ze nodig zijn, is 'Klein' - ze krijgt alleen enkele partities of zelfs in een pool gedeelde service met andere klanten kunnen worden geplaatst.
  - Een aantal service-exemplaren of replica's zijn niet worden uitgevoerd terwijl u voor klanten tooshow up wacht
  - Als een klant ooit verlaat, is hun gegevens van uw service verwijderen net zo eenvoudig als bestanden met Hallo manager verwijderen die service of toepassing dat is gemaakt.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over Service Fabric-concepten Hallo artikelen te volgen:

* [Beschikbaarheid van Service Fabric-services](service-fabric-availability-services.md)
* [Partitionering Service Fabric-services](service-fabric-concepts-partitioning.md)
