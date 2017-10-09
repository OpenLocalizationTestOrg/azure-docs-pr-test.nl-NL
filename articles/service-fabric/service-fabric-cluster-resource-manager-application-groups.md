---
title: aaaService Fabric Cluster Resource Manager - toepassingsgroepen | Microsoft Docs
description: Overzicht van Hallo functionaliteit van de groep toepassingen in Hallo Service Fabric-Cluster Resource Manager
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a>Inleiding tooApplication groepen
Service-Fabric Cluster Resource Manager beheert doorgaans clusterbronnen door te spreiden Hallo load (vertegenwoordigd [metrische gegevens](service-fabric-cluster-resource-manager-metrics.md)) gelijkmatig in Hallo-cluster. Service Fabric beheert Hallo capaciteit van Hallo knooppunten in het Hallo en Hallo cluster als geheel via [capaciteit](service-fabric-cluster-resource-manager-cluster-description.md). Metrische gegevens en capaciteit werken geweldig voor veel werkbelastingen, maar de patronen die maken intensief gebruik van verschillende exemplaren van Service Fabric-toepassing soms Breng in aanvullende vereisten. U kunt bijvoorbeeld naar:

- Sommige capaciteit op Hallo knooppunten in cluster Hallo voor Hallo services binnen een exemplaar van de benoemde reserveren
- Totale aantal knooppunten dat Hallo services binnen een benoemd exemplaar op worden uitgevoerd (in plaats van ze uit te spreiden over het hele cluster Hallo) Hallo beperken
- Capaciteit op Hallo benoemde toepassingsexemplaar zelf toolimit Hallo aantal services of totaal resourceverbruik van Hallo services erin definiëren

toomeet deze vereisten, Hallo Service Fabric-Cluster Resource Manager ondersteunt de functie toepassingsgroepen.

## <a name="limiting-hello-maximum-number-of-nodes"></a>Maximum aantal knooppunten Hallo beperken
Hallo eenvoudigste gebruiksvoorbeeld capaciteit van de toepassing is wanneer een toepassingsexemplaar moet toobe beperkt tooa bepaalde maximum aantal knooppunten. Dit consolideert alle services in dat toepassingsexemplaar naar een bepaald aantal machines. Consolidatie is nuttig wanneer u toopredict probeert of fysieke resource gebruik cap door Hallo services binnen die benoemde exemplaar. 

Hallo volgende afbeelding ziet u de instantie van een toepassing met en zonder een maximum aantal knooppunten gedefinieerd:

<center>
![Toepassingsexemplaar Maximum aantal knooppunten definiëren][Image1]
</center>

In Hallo links bijvoorbeeld Hallo toepassing geen een maximum aantal knooppunten dat is gedefinieerd en hieraan de drie services. Hallo Cluster Resource Manager heeft alle replica's over verspreid zes beschikbare knooppunten tooachieve Hallo beste balans in Hallo-cluster (Hallo standaardgedrag). In de juiste Hallo voorbeeld zien we Hallo dezelfde toepassing beperkt toothree knooppunten.

Hallo-parameter die dit gedrag bepaalt wordt MaximumNodes genoemd. Deze parameter worden ingesteld tijdens het maken van de toepassing of bijgewerkt in verband met de instantie van een toepassing die al wordt uitgevoerd.

PowerShell

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

C#

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

Geen binnen Hallo set knooppunten garantie Hallo Cluster Resource Manager welke serviceobjecten samen worden geplaatst of welke knooppunten ophalen gebruikt.

## <a name="application-metrics-load-and-capacity"></a>Metrische gegevens van toepassing, laden en capaciteit
Toepassingsgroepen kunnen u ook toodefine metrische gegevens die zijn gekoppeld aan een bepaalde toepassing van de benoemde exemplaar, en die van het toepassingsexemplaar capaciteit voor deze metrische gegevens. Toepassing metrische gegevens kunt u tootrack, reserveren en limiet Hallo resourceverbruik van Hallo services binnen dat toepassingsexemplaar.

Er zijn twee waarden kunnen worden ingesteld voor elke metriek toepassing:

- **Totale capaciteit van de toepassing** – deze instelling geeft Hallo totale capaciteit van de Hallo-toepassing voor een bepaalde waarde. Hallo Cluster Resource Manager Hallo maken van de nieuwe services binnen deze toepassingsexemplaar die totale belasting tooexceed deze waarde veroorzaken is niet toegestaan. Stel dat bijvoorbeeld Hallo toepassingsexemplaar had een capaciteit van 10 en laden van vijf al had. Hallo maken van een service met een totale standaard belasting van 10 zou niet worden toegestaan.
- **Maximale capaciteit van het knooppunt** – deze instelling bepaalt u Hallo maximale totale belasting voor de toepassing hello op één knooppunt. Als de belasting toeneemt via deze capaciteit, verplaatst u Hallo Cluster Resource Manager replica's tooother knooppunten zodat hello belasting afneemt.


PowerShell:

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

C#:

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a>Capaciteit reserveren
Er wordt een andere vaak gebruikt voor toepassingsgroepen tooensure dat resources binnen een cluster Hallo zijn gereserveerd voor het exemplaar van een bepaalde toepassing. Hallo-ruimte is altijd gereserveerd wanneer Hallo toepassingsexemplaar wordt gemaakt.

Ruimte in de cluster Hallo reserveren voor toepassing hello onmiddellijk gebeurt ook wanneer:
- Hallo-toepassingsexemplaar is gemaakt, maar geen binnen deze services nog
- aantal services binnen het toepassingsexemplaar Hallo Hallo verandert telkens wanneer 
- Hallo-services bestaat, maar worden niet Hallo resources verbruikt 

Resources worden gereserveerd voor een toepassingsexemplaar vereist twee extra parameters opgeven: *MinimumNodes* en *NodeReservationCapacity*

- **MinimumNodes** -bepaalt het minimumaantal Hallo van knooppunten die toepassing hello exemplaar mag worden uitgevoerd op.  
- **NodeReservationCapacity** -deze instelling is per metrische gegevens voor de toepassing hello. Hallo-waarde is Hallo hoeveelheid die metriek gereserveerd voor de toepassing hello op elk knooppunt waar dat Hallo services in de desbetreffende toepassing uitvoeren.

Combineren **MinimumNodes** en **NodeReservationCapacity** wordt gegarandeerd dat een minimale belasting reservering voor de toepassing hello binnen Hallo-cluster. Als er minder resterende capaciteit in Hallo cluster dan de totale reservering Hallo vereist, mislukt het maken van de toepassing hello. 

Bekijk een voorbeeld van capaciteitsreservering:

<center>
![Exemplaren van een toepassing gereserveerde capaciteit definiëren][Image2]
</center>

In Hallo links bijvoorbeeld hoeft toepassingen niet elke toepassing capaciteit gedefinieerd. Alles op basis van regels toonormal compromis tussen de Hallo Cluster Resource Manager.

Stel de dat Toepassing1 is gemaakt met de Hallo instellingen te volgen in voorbeeld Hallo op Hallo rechts:

- MinimumNodes instellen tootwo
- Een waarde die is gedefinieerd met de van toepassing
  - NodeReservationCapacity van 20

PowerShell

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

C#

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

Service Fabric reserveert capaciteit op twee knooppunten voor Toepassing1 en niet-services toestaan van Toepassing2 tooconsume die capaciteit zelfs als er dat geen load wordt verbruikt door Hallo services binnen Toepassing1 Hallo tegelijk. Deze toepassing gereserveerde capaciteit wordt beschouwd als verbruikt en wordt in mindering gebracht op Hallo resterende capaciteit op dat knooppunt en binnen Hallo-cluster.  Hallo-reservering wordt afgetrokken van de capaciteit van het cluster onmiddellijk resterende hello, maar Hallo gereserveerd verbruik wordt afgetrokken van Hallo-capaciteit van een specifiek knooppunt alleen als er ten minste één service-object is geplaatst op het. Deze reservering hoger kunt u flexibiliteit en beter brongebruik omdat alleen de bronnen worden gereserveerd op de knooppunten wanneer deze nodig is.

## <a name="obtaining-hello-application-load-information"></a>Hallo toepassing werklast informatie verkrijgen
U kunt voor elke toepassing met een capaciteit van toepassingen gedefinieerd voor een of meer waarden Hallo informatie over Hallo cumulatieve load gerapporteerd door de replica's van de services verkrijgen.

PowerShell:

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

C#

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

Hallo ApplicationLoad query retourneert Hallo algemene informatie over de capaciteit van de toepassingen die is opgegeven voor de toepassing hello. Deze informatie omvat het Hallo-knooppunten van de Minimum en maximum aantal knooppunten info en Hallo nummer Hallo toepassing momenteel wordt ingenomen. Dit omvat ook informatie over elke toepassing werklast metriek, met inbegrip van:

* Metrische naam: Naam van Hallo metriek.
* Reserveringscapaciteit: Cluster de capaciteit die is gereserveerd in Hallo cluster voor deze toepassing.
* Laden van toepassingen: Totale belasting van deze toepassing onderliggende replica's.
* Capaciteit van de toepassing: De maximaal toegestane waarde van het laden van toepassingen.

## <a name="removing-application-capacity"></a>Capaciteit van de toepassing verwijderen
Zodra Hallo toepassing capaciteit parameters zijn ingesteld voor een toepassing, kunnen ze worden verwijderd met behulp van de Update toepassing API's of PowerShell-cmdlets. Bijvoorbeeld:

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

Deze opdracht verwijdert u alle management parameters van de toepassing capaciteit van het toepassingsexemplaar Hallo. Dit omvat MinimumNodes, MaximumNodes en metrische gegevens van de toepassing hello, indien van toepassing. Hallo effect van Hallo-opdracht is direct. Nadat u deze opdracht is voltooid, Hallo Cluster Resource Manager Hallo standaardgedrag gebruikt voor het beheren van toepassingen. Capaciteit parameters voor de toepassing opnieuw kunnen worden opgegeven `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.

### <a name="restrictions-on-application-capacity"></a>Beperkingen voor de capaciteit van toepassingen
Er zijn enkele beperkingen van toepassing capaciteit parameters die moeten worden voldaan. Als er validatiefouten zijn plaatsvinden geen wijzigingen.

- Alle parameters van geheel getal moet niet-negatieve getallen.
- Nooit moet MinimumNodes groter zijn dan MaximumNodes.
- Als de capaciteit voor een load-metriek zijn gedefinieerd, moeten ze deze regels volgen:
  - Knooppunt Reserveringscapaciteit mag niet groter zijn dan de maximale capaciteit van het knooppunt zijn. U kan bijvoorbeeld Hallo capaciteit voor Hallo metriek 'CPU' op Hallo knooppunt tootwo eenheden beperken en probeer de drie eenheden tooreserve op elk knooppunt.
  - Als MaximumNodes is opgegeven, vervolgens moet Hallo product van MaximumNodes en de maximale capaciteit van het knooppunt niet groter dan de totale capaciteit van de toepassing. Stel bijvoorbeeld Hallo maximumcapaciteit knooppunt voor load metriek 'CPU' tooeight is ingesteld. Stel ook dat u Hallo too10 maximum aantal knooppunten. In dit geval moet totale capaciteit van de toepassing groter zijn dan 80 voor deze metriek laden.

Hallo-beperkingen afgedwongen zowel tijdens het maken van de toepassing en updates.

## <a name="how-not-toouse-application-capacity"></a>Hoe niet toouse capaciteit van toepassingen
- Probeer niet toouse Hallo toepassingsgroep functies tooconstrain Hallo toepassing tooa _specifieke_ deelverzameling met knooppunten. Met andere woorden, u kunt opgeven dat Hallo toepassing wordt uitgevoerd op maximaal vijf knooppunten, maar niet welke specifieke vijf knooppunten in cluster Hallo. Een toepassing toospecific met beperkingen kunnen knooppunten worden bereikt met plaatsingsbeperkingen voor services.
- Probeer niet toouse Hallo toepassing capaciteit tooensure dat twee services van dezelfde toepassing worden geplaatst op Hallo Hallo dezelfde knooppunten. Gebruik in plaats daarvan [affiniteit](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) of [plaatsingsbeperkingen](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).

## <a name="next-steps"></a>Volgende stappen
- Voor meer informatie over het configureren van services, [meer informatie over het configureren van Services](service-fabric-cluster-resource-manager-configure-services.md)
- toofind uit over hoe Hallo Cluster Resource Manager beheert en een compromis tussen de werklast van de cluster Hallo, bekijk Hallo artikel op [load balancing](service-fabric-cluster-resource-manager-balancing.md)
- Vanaf Hallo begin starten en [ophalen van een inleiding toohello Service Fabric-Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)
- Voor meer informatie over de werking metrische gegevens over het algemeen tot lezen op [Service Fabric Load metrische gegevens](service-fabric-cluster-resource-manager-metrics.md)
- Hallo Cluster Resource Manager heeft veel opties voor het beschrijven van Hallo-cluster. toofind voor meer informatie over deze Raadpleeg dit artikel op [met een beschrijving van een Service Fabric-cluster](service-fabric-cluster-resource-manager-cluster-description.md)

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
