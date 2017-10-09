---
title: Service Fabric host Model aaaAzure | Microsoft Docs
description: "Beschrijft de relatie tussen de replica's (of exemplaren) van een geïmplementeerde Servic Fabric-service en de ServiceHost proces."
services: service-fabric
documentationcenter: .net
author: harahma
manager: timlt
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/15/2017
ms.author: harahma
ms.openlocfilehash: 30e0ba19cd672a722f76477a311ecef7c213b055
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-hosting-model"></a>Service Fabric-hostingmodel
In dit artikel biedt een overzicht van modellen die worden geleverd door de Service Fabric-toepassing en Hallo worden verschillen beschreven tussen Hallo **gedeeld proces** en **exclusieve proces** modellen. Hierin wordt beschreven hoe een geïmplementeerde toepassing eruitziet op een Service Fabric-knooppunt en de relatie tussen de replica's (of exemplaren) van Hallo-service en Hallo ServiceHost proces.

Voordat u doorgaat, zorg ervoor dat u bekend met bent [Service Fabric-toepassingsmodel] [ a1] en verschillende concepten en relatie ertussen begrijpen. 

> [!NOTE]
> In dit artikel, ter vereenvoudiging tenzij expliciet wordt vermeld:
>
> - Al het gebruik van word *replica* tooboth een replica van een stateful service of een exemplaar van een service statless verwijst.
> - *CodePackage* is behandeld equivalent te*ServiceHost* proces dat registreert een *ServiceType* en hosts replica's van services van die *ServiceType*.
>

toounderstand Hallo hostingmodel, doorlopen we een voorbeeld. Laat het ons spreken we hebben een *ApplicationType* MyAppType' met een *ServiceType* MyServiceType' die wordt geleverd door *ServicePackage* MyServicePackage' met een *CodePackage* MyCodePackage, waardoor wordt geregistreerd *ServiceType* MyServiceType wanneer deze wordt uitgevoerd.

Stel dat we hebben een cluster met 3 knooppunten en maken we een *toepassing* **fabric: / App1** van het type 'MyAppType'. In dit *toepassing* **fabric: / App1** maken we een service **fabric: / App1/ServiceA** van het type MyServiceType' dat 2 partities is (spreken **P1** & **P2**) en 3 replica's per partitie. Hallo volgende diagram toont Hallo-weergave van deze toepassing zoals deze belandt geïmplementeerd op een knooppunt.

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-one]
</center>

Service Fabric geactiveerd MyServicePackage' die gestart MyCodePackage' die als host voor replica's van de partities van beide Hallo dat wil zeggen fungeert **P1** & **P2**. Houd er rekening mee dat alle Hallo knooppunten in cluster Hallo dezelfde weergave heeft omdat we het aantal replica's per partitie gelijk toonumber van knooppunten in cluster Hallo hebt gekozen. We gaan maken van een andere service **fabric: / App1/ServiceB** in toepassing **fabric: / App1** die 1 partitie heeft (spreken **P3**) en 3 replica's per partitie. Volgende diagram toont de nieuwe weergave Hallo op Hallo-knooppunt:

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-two]
</center>

Zoals we zien Service Fabric Hallo nieuwe replica voor partitie geplaatst **P3** van service **fabric: / App1/XPb** in bestaande activering van 'MyServicePackage' Hallo. Nu kunt maken van een andere *toepassing* **fabric: / App2** van het type 'MyAppType' en binnen **fabric: / App2** service maken **fabric: / App2/ServiceA** die 2 partities heeft (spreken **P4** & **P5**) en 3 replica's per partitie. Diagrammen, ziet u het nieuwe knooppunt weergave Hallo in:

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-three]
</center>

Deze tijd Service Fabric is geactiveerd op een nieuw exemplaar van MyServicePackage' die wordt gestart van een nieuw exemplaar van 'MyCodePackage' en replica's van beide partities van de service **fabric: / App2/ServiceA** (dat wil zeggen **P4** & **P5**) in deze nieuwe kopie 'MyCodePackage' worden geplaatst.

## <a name="shared-process-model"></a>Gedeelde procesmodel
Wat we zagen hierboven Hallo standaard hostingmodel geleverd door de Service Fabric en is bedoeld tooas **gedeeld proces** model. In dit model voor een gegeven *toepassing*, slechts één exemplaar van een opgegeven *ServicePackage* is geactiveerd op een *knooppunt* (Hiermee start u alle Hallo *CodePackages* die dit) en alle replica's van alle services van Hallo een bepaalde *ServiceType* worden geplaatst in Hallo *CodePackage* die wordt geregistreerd dat *ServiceType*. Met andere woorden, alle Hallo replica's van alle services van een bepaalde *ServiceType* delen hetzelfde proces Hallo.

## <a name="exclusive-process-model"></a>Exclusieve procesmodel
Hallo andere hostingmodel geleverd door de Service Fabric is **exclusieve proces** model. In dit model op een gegeven *knooppunt*, voor de plaatsing van elke replica Service Fabric Hiermee activeert u een nieuw exemplaar van *ServicePackage* (Hiermee start u alle Hallo *CodePackages* die dit ) en replica wordt geplaatst in Hallo *CodePackage* die geregistreerde Hallo *ServiceType* van Hallo service toowhich replica behoort. Met andere woorden, woont elke replica in een eigen toegewezen proces. 

Dit model wordt ondersteund vanaf versie 5.6 van Service Fabric. **Exclusieve proces** model kan worden gekozen op Hallo-tijd van het Hallo-service maakt (met behulp van [PowerShell][p1], [REST] [ r1]of [FabricClient][c1]) door te geven **ServicePackageActivationMode** als 'ExclusiveProcess'.

```powershell
PS C:\>New-ServiceFabricService -ApplicationName "fabric:/App1" -ServiceName "fabric:/App1/ServiceA" -ServiceTypeName "MyServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1 -ServicePackageActivationMode "ExclusiveProcess"
```

```csharp
var serviceDescription = new StatelessServiceDescription
{
    ApplicationName = new Uri("fabric:/App1"),
    ServiceName = new Uri("fabric:/App1/ServiceA"),
    ServiceTypeName = "MyServiceType",
    PartitionSchemeDescription = new SingletonPartitionSchemeDescription(),
    InstanceCount = -1,
    ServicePackageActivationMode = ServicePackageActivationMode.ExclusiveProcess
};

var fabricClient = new FabricClient(clusterEndpoints);
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

Als u een standaardservice in het manifest van uw toepassing hebt, kunt u kiezen **exclusieve proces** model door op te geven **ServicePackageActivationMode** kenmerk zoals hieronder wordt weergegeven:

```xml
<DefaultServices>
  <Service Name="MyService" ServicePackageActivationMode="ExclusiveProcess">
    <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
      <SingletonPartition/>
    </StatelessService>
  </Service>
</DefaultServices>
```
U kunt doorgaan met het bovenstaande voorbeeld, kunt maken van een andere service **fabric: / App1/ServiceC** in toepassing **fabric: / App1** die 2 partities heeft (spreken **P6**  &  **P7**) en 3 replica's per partitie met **ServicePackageActivationMode** too'ExclusiveProcess ingesteld. Volgende diagram toont de nieuwe weergave op Hallo-knooppunt:

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-four]
</center>

Zoals u ziet, Service Fabric twee nieuwe exemplaren van 'MyServicePackage' geactiveerd (één voor elke replica van partitie **P6** & **P7**) en elke replica geplaatst in een speciale van *CodePackage*. Een andere ding toonote hier is als **exclusieve proces** model wordt gebruikt, voor een bepaalde *toepassing*, meerdere exemplaren van een bepaalde *ServicePackage* actief zijn op een  *Knooppunt*. In bovenstaande voorbeeld zien we drie kopieën van 'MyServicePackage' zijn actief voor **fabric: / App1**. Elk van deze actieve kopieën van 'MyServicePackage' heeft een **ServicePackageAtivationId** gekoppeld waarmee wordt aangegeven dat exemplaar binnen *toepassing* **fabric: / App1**.

Wanneer alleen **gedeeld proces** model wordt gebruikt voor een *toepassing*, bijvoorbeeld **fabric: / App2** in bovenstaande voorbeeld is slechts één actieve kopie van *ServicePackage* op een *knooppunt* en **ServicePackageAtivationId** voor deze activering van *ServicePackage* ' lege tekenreeks '.

> [!NOTE]
>- **Gedeeld proces** te hostingmodel correspondeert**ServicePackageAtivationMode** gelijk **SharedProcess**. Dit is Hallo standaard hostingmodel en **ServicePackageAtivationMode** niet gelijktijdig Hallo met maken van Hallo-service moet worden opgegeven.
>
>- **Exclusieve proces** te hostingmodel correspondeert**ServicePackageAtivationMode** gelijk **ExclusiveProcess** en moeten expliciet worden opgegeven tijdens het Hallo van het maken van Hallo toobe de service. 
>
>- HostingModel van een service kan worden herkend door het uitvoeren van query's Hallo [servicebeschrijving] [ p2] en waarde van kijken **ServicePackageAtivationMode**.
>
>

## <a name="working-with-deployed-service-package"></a>Werken met geïmplementeerd servicepakket
Een actieve kopie van een *ServicePackage* op een knooppunt wordt aangeduid als [geïmplementeerd servicepakket][p3]. Zoals eerder opgemerkt hierboven, wanneer **exclusieve proces** model wordt gebruikt voor het maken van services voor een bepaalde *toepassing*, er zijn meerdere geïmplementeerde service pakketten voor Hallo dezelfde  *ServicePackage*. Tijdens het uitvoeren van bewerkingen servicepakket specifieke toodeployed zoals [status van een pakket geïmplementeerde service reporting] [ p4] of [codepakket van een geïmplementeerde servicepakketopnieuwtestarten] [ p5] enz., **ServicePackageActivationId** behoeften toobe opgegeven tooidentify een specifiek geïmplementeerd servicepakket.

 **ServicePackageActivationId** van een geïmplementeerde service pakket kan worden verkregen door het uitvoeren van query's Hallo lijst met [geïmplementeerde servicepakketten] [ p3] op een knooppunt. Tijdens het opvragen van [geïmplementeerd servicetypen][p6], [replica's geïmplementeerd] [ p7] en [geïmplementeerd code pakketten] [ p8] op een knooppunt bevat Hallo queryresultaat ook Hallo **ServicePackageActivationId** van pakket met de bovenliggende geïmplementeerde service.

> [!NOTE]
>- Onder **gedeeld proces** hostingmodel, op een gegeven *knooppunt*, voor een bepaalde *toepassing*, slechts één exemplaar van een *ServicePackage* is geactiveerd. Deze heeft **ServicePackageActivationId** gelijk zijn aan te*lege tekenreeks* en moet niet worden opgegeven tijdens bewerkingen met betrekking tot presterende geïmplementeerd servicepakket. 
>
> - Onder **exclusieve proces** hostingmodel, op een gegeven *knooppunt*, voor een bepaalde *toepassing*, een of meer exemplaren van een *ServicePackage* kan actief zijn. Elke activering heeft een *niet-lege* **ServicePackageActivationId** en moet toobe opgegeven terwijl de presterende geïmplementeerd servicepakket gerelateerde bewerkingen. 
>
> - Als **ServicePackageActivationId** ommited too'empty tekenreeks is de standaardwaarde is'. Als u een geïmplementeerde service die het pakket is geactiveerd onder **gedeeld proces** model aanwezig is, wordt de bewerking wordt uitgevoerd, anders Hallo-bewerking mislukt.
>
> - Het wordt niet aangeraden tooquery eenmaal en cache **ServicePackageActivationId** naar dynamisch wordt gegenereerd en om verschillende redenen kunt wijzigen. Voordat u een bewerking die behoeften uitvoert **ServicePackageActivationId**, u moet eerst een Hallo lijst met query [geïmplementeerde servicepakketten] [ p3] op een knooppunt en gebruik vervolgens  *ServicePackageActivationId** van resultaat tooperform Hallo oorspronkelijke querybewerking.
>
>

## <a name="guest-executable-and-container-applications"></a>Het uitvoerbare bestand en de container toepassingen Gast
Service Fabric behandelt [Gast uitvoerbaar bestand] [ a2] en [container] [ a3] toepassingen als statless services die ingesloten zijn dus er is geen Service Fabric-runtime in *ServiceHost* (een proces of container). Aangezien deze services zelfstandig zijn, aantal replica's per *ServiceHost* is niet van toepassing voor deze services. Hallo meest voorkomende configuratie gebruikt in combinatie met deze services is één partitie met [InstanceCount] [ c2] gelijk te-1 (dat wil zeggen een kopie van Hallo servicecode die wordt uitgevoerd op elk knooppunt van het cluster). 

Standaard Hallo **ServicePackageActivationMode** is voor deze services **SharedProcess** Service Fabric activeert in dat geval slechts één exemplaar van *ServicePackage* op een *Knooppunt* voor een bepaalde *toepassing* wat betekent dat slechts één exemplaar van de servicecode wordt uitgevoerd een *knooppunt*. Als u wilt dat meerdere exemplaren van uw service code toorun op een *knooppunt* wanneer u meerdere services maakt (*Service1* te*ServiceN*) van *ServiceType* (opgegeven in *ServiceManifest*) of als uw service multi gepartitioneerd, moet u **ServicePackageActivationMode** als **ExclusiveProcess**bij Hallo Hallo service maken.

## <a name="changing-hosting-model-of-an-existing-service"></a>HostingModel van een bestaande service wijzigen
HostingModel van een bestaande service vanuit wijzigen **gedeeld proces** te**exclusieve proces** en vice versa via upgraden of bijwerken mechanisme (of in service-specificatie in de toepassing manifest) is momenteel niet ondersteund. Ondersteuning voor deze functie wordt geleverd in toekomstige versies.

## <a name="choosing-between-shared-process-and-exclusive-process-model"></a>Kiezen tussen gedeeld proces en exclusieve procesmodel
Zowel deze modellen die als host fungeert de voor- en nadelen hebben als gebruiker moet tooevaluate waarvoor een beste hun behoeften past. **Gedeeld proces** model stelt beter gebruik van de OS-bronnen omdat er minder processen worden geïnitieerd, meerdere replica's in dezelfde Hallo proces kan delen poorten, enzovoort. Echter, als een van de replica's Hallo foutbericht waarin deze toobring omlaag Hallo ServiceHost moet raakt, dat invloed op alle andere replica's in hetzelfde proces.

 **Exclusieve proces** model voorziet in betere isolatie met elke replica in een eigen proces en andere replica's heeft geen invloed op een replica zich niet normaal gedraagt. Deze goed van pas komt voor gevallen waarin delen van de poort wordt niet ondersteund door Hallo communicatieprotocol. Dit vergemakkelijkt Hallo mogelijkheid tooapply resource governance op niveau van de replica. Op Hallo daarentegen **exclusieve proces** verbruikt meer OS bronnen als deze een proces voor elke replica op Hallo knooppunt gestart.

## <a name="exclusive-process-model-and-application-model-considerations"></a>Exclusieve procesmodel en toepassing modelleren overwegingen
Hallo aanbevolen manier toomodel uw toepassing in Service Fabric is tookeep een *ServiceType* per *ServicePackage* en dit model geschikt is voor de meeste Hallo-toepassingen. 

Echter speciale tooenable-scenario's waarin een *ServiceType* per *ServicePackage* niet wenselijk, functioneel, Service Fabric kunt toohave meer dan een *ServiceType* per *ServicePackage* (één *CodePackage* kunt registreren meer dan één *ServiceType*). Hieronder volgen enkele Hallo scenario's waar deze configuraties nuttig kunnen zijn:

- Wilt u toooptimize OS Resourcegebruik door minder processen te starten en met hogere replica dichtheid per proces.
- Replica's van verschillende ServiceTypes moeten tooshare enkele algemene gegevens met een hoge initialisatie of kosten geheugen.
- U hebt een vrije serviceaanbieding en gewenste tooput een limiet van Resourcegebruik door de gegevens van alle replica's van de service Hallo in hetzelfde proces.

**Exclusieve proces** hostingmodel is geen samenhangende met meerdere toepassingsmodel *ServiceTypes* per *ServicePackage*. Dit komt doordat meerdere *ServiceTypes* per *ServicePackage* ontworpen tooachieve hogere resource delen van replica's en hogere replica dichtheid per proces mogelijk maakt. Dit is strijdig toowhat **exclusieve proces** model is ontworpen tooachieve.

Neem Hallo geval van meerdere *ServiceTypes* per *ServicePackage* met andere *CodePackage* registreren van elk *ServiceType*. Laten we een *ServicePackage* MultiTypeServicePackge' met twee *CodePackages*:

- MyCodePackageA, waardoor wordt geregistreerd *ServiceType* 'MyServiceTypeA'.
- MyCodePackageB, waardoor wordt geregistreerd *ServiceType* 'MyServiceTypeB'.

Nu kunt spreken, maken we een *toepassing* **fabric: / SpecialApp** en binnen **fabric: / SpecialApp** maken we de volgende twee services met **exclusieve proces** model:

- Service **fabric: / SpecialApp/ServiceA** van het type 'MyServiceTypeA' met twee partities (spreken **P1** en **P2**) en 3 replica's per partitie.
- Service **fabric: / SpecialApp/ServiceB** van het type 'MyServiceTypeB' met twee partities (spreken **P3** en **P4**) en 3 replica's per partitie.

Op een bepaald knooppunt moet beide services Hallo elke twee replica's. Aangezien we gebruikt **exclusieve proces** model toocreate Hallo-services, Service Fabric een nieuw exemplaar van 'MyServicePackge' voor elke replica worden geactiveerd. Elke activering van 'MultiTypeServicePackge' wordt een kopie van 'MyCodePackageA' en 'MyCodePackageB' gestart. Echter, host slechts één van de 'MyCodePackageA' of 'MyCodePackageB' hello replica waarvoor 'MultiTypeServicePackge' is geactiveerd. Volgende diagram toont Hallo knooppunt weergeven:

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-five]
</center>

 Zoals we in Hallo activering van 'MultiTypeServicePackge' voor de replica van partitie zien kunt **P1** van service **fabric: / SpecialApp/ServiceA**, 'MyCodePackageA' hello replica wordt gehost en ' MyCodePackageB' net actief is. Op deze manier bij activering van 'MultiTypeServicePackge' voor de replica van partitie **P3** van service **fabric: / SpecialApp/XPb**, 'MyCodePackageB' hello replica wordt gehost en 'MyCodePackageA' is alleen actief en werkend enzovoort. Aantal daarom meer Hallo *CodePackages* (registreren verschillende *ServiceTypes*) per *ServicePackage*, hogere worden redundante Resourcegebruik. 
 
 Anderzijds op Hallo als we services maakt **fabric: / SpecialApp/ServiceA** en **fabric: / SpecialApp/ServiceB** met **gedeeld proces** licentiemodel, Service Fabric activeren van slechts één exemplaar van 'MultiTypeServicePackge' voor *toepassing* **fabric: / SpecialApp** (zoals u hebt gezien eerder). Alle replica's voor service fungeert als host voor 'MyCodePackageA' **fabric: / SpecialApp/ServiceA** (of een service van het type 'MyServiceTypeA' toobe nauwkeurigere) en 'MyCodePackageB' fungeert als host voor alle replica's voor service **fabric: / SpecialApp/XPb** (of een service van het type 'MyServiceTypeB' toobe nauwkeurigere). Hallo knooppunt weergave toont volgende diagram deze instelling: 

<center>
![Knooppunt-weergave van geïmplementeerde toepassing][node-view-six]
</center>

In Hallo hierboven voorbeeld, u kunt overwegen als 'MyCodePackageA' zowel 'MyServiceTypeA' en 'MyServiceTypeB registreert' en er is geen 'MyCodePackageB', dan zal er geen redundante *CodePackage* uitgevoerd. Dit klopt, echter, zoals eerder vermeld, dit toepassingsmodel komt niet overeen met **exclusieve proces** hostingmodel. Als het doel is tooput elke replica in een eigen proces registreren, zowel toegewezen *ServiceTypes* van dezelfde *CodePackage* is niet nodig en stellen elke *ServiceType* in een eigen *ServicePacakge* is een natuurlijke keuze.

## <a name="next-steps"></a>Volgende stappen
[Een toepassing van het pakket] [ a4] en deze gereed toodeploy.

[Implementeren en toepassingen verwijderen] [ a5] wordt beschreven hoe toouse PowerShell toomanage toepassingsexemplaren.

<!--Image references-->
[node-view-one]: ./media/service-fabric-hosting-model/node-view-one.png
[node-view-two]: ./media/service-fabric-hosting-model/node-view-two.png
[node-view-three]: ./media/service-fabric-hosting-model/node-view-three.png
[node-view-four]: ./media/service-fabric-hosting-model/node-view-four.png
[node-view-five]: ./media/service-fabric-hosting-model/node-view-five.png
[node-view-six]: ./media/service-fabric-hosting-model/node-view-six.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[a1]: service-fabric-application-model.md
[a2]: service-fabric-deploy-existing-app.md
[a3]: service-fabric-containers-overview.md
[a4]: service-fabric-package-apps.md
[a5]: service-fabric-deploy-remove-applications.md

[r1]: https://docs.microsoft.com/rest/api/servicefabric/sfclient-api-createservice

[c1]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.servicemanagementclient.createserviceasync
[c2]: https://docs.microsoft.com/dotnet/api/system.fabric.description.statelessservicedescription.instancecount

[p1]: https://docs.microsoft.com/powershell/servicefabric/vlatest/new-servicefabricservice
[p2]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricservicedescription
[p3]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicePackage
[p4]: https://docs.microsoft.com/powershell/servicefabric/vlatest/send-servicefabricdeployedservicepackagehealthreport
[p5]: https://docs.microsoft.com/powershell/servicefabric/vlatest/restart-servicefabricdeployedcodepackage
[p6]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedservicetype
[p7]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedreplica
[p8]: https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricdeployedcodepackage