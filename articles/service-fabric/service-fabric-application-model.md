---
title: Service Fabric-toepassingsmodel aaaAzure | Microsoft Docs
description: Hoe toomodel en toepassingen en services in Service Fabric beschreven.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: mani-ramaswamy
ms.assetid: 17a99380-5ed8-4ed9-b884-e9b827431b02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: ryanwi
ms.openlocfilehash: 54c4d026e7d556be5f697d4a6f2ee886687e1c35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="model-an-application-in-service-fabric"></a>Model van een toepassing in Service Fabric
Dit artikel bevat een overzicht van Azure Service Fabric-toepassingsmodel Hallo en hoe toodefine een toepassing en service via bestanden manifest.

## <a name="understand-hello-application-model"></a>Hallo toepassingsmodel begrijpen
Een toepassing is een verzameling van de services die een bepaalde functie of functies uitvoeren. Een service kunt vervult een functie die volledig en zelfstandig starten en onafhankelijk van andere services worden uitgevoerd.  Een service bestaat uit code, configuratie en gegevens. Voor elke service code bestaat uit Hallo uitvoerbare binaire bestanden, configuratie bestaat uit de service-instellingen die kunnen worden geladen tijdens runtime en gegevens bestaan uit willekeurige statische gegevens toobe verbruikt door Hallo-service. Elk onderdeel in dit toepassingsmodel hiërarchische kan worden samengesteld en bijgewerkte onafhankelijk.

![Hallo Service Fabric-toepassingsmodel][appmodel-diagram]

Een toepassingstype een categorisatie van een toepassing is en bestaat uit een bundel van servicetypen. Een service is een categorisatie van een service. Hallo categorisatie kan hebben verschillende instellingen en configuraties, maar Hallo core functionaliteit blijft Hallo dezelfde. Hallo exemplaren van een service zijn Hallo andere service configuration variaties Hallo dezelfde servicetype.  

Klassen (of 'typen') van toepassingen en services via XML-bestanden (Toepassingsmanifesten en service manifesten) worden beschreven.  Hallo manifesten zijn Hallo-sjablonen op basis waarvan toepassingen uit de installatiekopieopslag Hallo-cluster kunnen worden gemaakt. Hallo schemadefinitie voor Hallo ServiceManifest.xml en ApplicationManifest.xml bestand is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

Hallo-code voor exemplaren van een andere toepassing zoals afzonderlijke processen, zelfs wanneer deze wordt gehost door Hallo dezelfde Service Fabric-knooppunt worden uitgevoerd. Bovendien Hallo levenscyclus van elk toepassingsexemplaar kan worden beheerd (bijvoorbeeld een bijgewerkt) onafhankelijk. Hallo volgende diagram toont hoe toepassingstypen servicetype die op zijn beurt bestaan uit code, configuratie en gegevenspakketten zijn samengesteld. toosimplify hello diagram alleen hello-pakketten config-code-gegevens voor `ServiceType4` worden weergegeven, hoewel elk servicetype u enkele vindt zou of alle pakkettypen.

![Service Fabric-toepassing waardetypen en servicetypen][cluster-imagestore-apptypes]

Er zijn twee verschillende manifest bestanden gebruikte toodescribe toepassingen en services: Hallo servicemanifest en manifest van de toepassing. Manifesten worden in detail in Hallo volgende secties besproken.

Er kan een of meer exemplaren van een servicetype actief zijn in Hallo-cluster. Bijvoorbeeld, bereiken stateful service-exemplaren of replica's hoge betrouwbaarheid status repliceren tussen replica's zich bevinden op andere knooppunten in het Hallo-cluster. Replicatie biedt in wezen redundantie voor Hallo service toobe beschikbaar, zelfs als een knooppunt in een cluster is mislukt. A [service gepartitioneerd](service-fabric-concepts-partitioning.md) verder delen de status (en toegangsstatus patronen toothat) tussen knooppunten in het Hallo-cluster.

Hallo toont volgende diagram Hallo relatie tussen toepassingen en service-exemplaren, partities en replica's.

![Partities en replica's binnen een service][cluster-application-instances]

> [!TIP]
> U kunt Hallo lay-out van toepassingen weergeven in een cluster met behulp van hulpprogramma voor Service Fabric Explorer Hallo beschikbaar op http://&lt;yourclusteraddress&gt;: 19080/Explorer. Zie voor meer informatie [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).
> 
> 

## <a name="describe-a-service"></a>Een service omschrijven
Hallo servicemanifest definieert declaratief Hallo servicetype en versie. Hiermee wordt de metagegevens zoals servicetype, eigenschappen van health-taakverdeling metrische gegevens, de binaire bestanden en configuratiebestanden.  Anders gezegd, Hallo code, configuratie en gegevens pakketten waaruit een service pakket toosupport beschrijft een of meer servicetypen. Dit is een eenvoudig voorbeeld servicemanifest:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```

**Versie** kenmerken ongestructureerde tekenreeksen zijn en niet worden geparseerd door Hallo-systeem. Versie kenmerken zijn gebruikte tooversion elk onderdeel voor upgrades.

**ServiceTypes** wordt gedeclareerd welke servicetypen worden ondersteund door **CodePackages** in dit manifest. Wanneer een service met een van deze servicetypen wordt gestart, worden alle code pakketten die zijn gedefinieerd in deze manifest geactiveerd door het uitvoeren van hun toegangspunten. Hallo resulterende processen zijn servicetypen van verwachte tooregister Hallo ondersteund tijdens runtime. Service-typen zijn gedeclareerd op Hallo manifest niveau en niet Hallo code pakket. Dus als er meerdere code pakketten, worden alle geactiveerd wanneer hello wordt gezocht naar een Hallo servicetypen gedeclareerd.

**Entrypoint** is een bevoorrechte toegangspunt dat wordt uitgevoerd met dezelfde referenties als Service Fabric hello (meestal Hallo *LocalSystem* account) voordat andere toegangspunt. Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** is doorgaans Hallo langlopende ServiceHost. Hallo aanwezigheid van een toegangspunt voor de afzonderlijke instellingen zo voorkomt u dat toorun Hallo ServiceHost met hoge bevoegdheden voor langere tijd. Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** wordt uitgevoerd na **entrypoint** is afgesloten. Als Hallo proces beëindigt ooit of vastloopt, Hallo resulterende proces wordt bewaakt en opnieuw opgestart (opnieuw vanaf **entrypoint**).  

Typische scenario's voor het gebruik van **entrypoint** zijn bij het uitvoeren van een uitvoerbaar bestand voordat Hallo-service wordt gestart of het uitvoeren van een bewerking met verhoogde bevoegdheden. Bijvoorbeeld:

* In te stellen en het initialiseren van omgevingsvariabelen die Hallo service uitvoerbare behoeften. Dit is niet beperkt tooonly uitvoerbare bestanden via Hallo Service Fabric-programmeermodellen geschreven. Npm.exe moet bijvoorbeeld een aantal omgevingsvariabelen die is geconfigureerd voor het implementeren van een node.js-toepassing.
* Instellen van toegangsbeheer door beveiligingscertificaten te installeren.

Voor meer informatie over het tooconfigure hello **entrypoint** Zie [Hallo beleid configureren voor een service-instelling toegangspunt.](service-fabric-application-runas-security.md)

**Omgevingsvariabelen** geeft een lijst van omgevingsvariabelen die zijn ingesteld voor dit codepakket. Environmentment variabelen kunnen worden overschreven in Hallo `ApplicationManifest.xml` tooprovide verschillende waarden voor verschillende service-exemplaren. 

**Gegevenspakket** declareert een map met de naam door Hallo **naam** kenmerk met willekeurige statische gegevens toobe verbruikt door Hallo proces tijdens runtime.

**ConfigPackage** declareert een map met de naam door Hallo **naam** kenmerk dat bevat een *Settings.xml* bestand. Hallo instellingenbestand bevat secties van de gebruiker gedefinieerde, sleutel / waarde-paar-instellingen die Hallo proces tijdens de uitvoering leest. Tijdens een upgrade als alleen Hallo **ConfigPackage** **versie** is gewijzigd, en vervolgens Hallo process uitgevoerd niet opnieuw wordt opgestart. In plaats daarvan waarschuwt een retouraanroep Hallo-proces dat configuratie-instellingen hebt gewijzigd zodat ze opnieuw kunnen worden geladen dynamisch. Hier volgt een voorbeeld *Settings.xml* bestand:

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> Een servicemanifest kan meerdere code, configuratie en gegevenspakketten bevatten. Elk van deze kan worden samengesteld onafhankelijk.
> 
> 

<!--
For more information about other features supported by service manifests, refer toohello following articles:

*TODO: LoadMetrics, PlacementConstraints, ServicePlacementPolicies
*TODO: Resources
*TODO: Health properties
*TODO: Trace filters
*TODO: Configuration overrides
-->

## <a name="describe-an-application"></a>Een toepassing beschrijven
Hallo-toepassingsmanifest beschrijft declaratief Hallo toepassingstype en -versie. Deze geeft service samenstelling metagegevens zoals stabiele namen, partitioneren schema, exemplaar count/replicatie factor/isolatie-beleid, plaatsingsbeperkingen, configuratie onderdrukkingen en samenstellende servicetypen. Hallo-taakverdeling domeinen waarin de toepassing hello is geplaatst, worden ook beschreven.

Dus een toepassingsmanifest worden elementen op toepassingsniveau Hallo beschreven en verwijst naar een of meer service-manifesten toocompose een toepassingstype. Dit is een eenvoudig voorbeeld toepassingsmanifest:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ApplicationManifest
      ApplicationTypeName="MyApplicationType"
      ApplicationTypeVersion="AppManifestVersion1"
      xmlns="http://schemas.microsoft.com/2011/01/fabric"
      xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example application manifest</Description>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="MyServiceManifest" ServiceManifestVersion="SvcManifestVersion1"/>
    <ConfigOverrides/>
    <EnvironmentOverrides CodePackageRef="MyCode"/>
  </ServiceManifestImport>
  <DefaultServices>
     <Service Name="MyService">
         <StatelessService ServiceTypeName="MyServiceType" InstanceCount="1">
             <SingletonPartition/>
         </StatelessService>
     </Service>
  </DefaultServices>
</ApplicationManifest>
```

Service manifesten, zoals **versie** kenmerken ongestructureerde tekenreeksen zijn en niet worden geparseerd door Hallo-systeem. Versie kenmerken zijn ook gebruikte tooversion elk onderdeel voor upgrades.

**ServiceManifestImport** bevat verwijzingen tooservice manifesten waaruit dit toepassingstype. Geïmporteerde service manifesten bepalen welke servicetypen zijn geldig binnen dit toepassingstype. Binnen Hallo ServiceManifestImport, moet u configuratiewaarden in Settings.xml en omgevingsvariabelen in ServiceManifest.xml bestanden overschrijven. 


**DefaultServices** declareert service-exemplaren die automatisch worden gemaakt wanneer een toepassing wordt gestart op basis van dit toepassingstype. Standaardservices zijn alleen gemakkelijker te maken en zich gedragen als normale services in elke opzicht nadat ze zijn gemaakt. Deze samen met andere services in het toepassingsexemplaar Hallo zijn bijgewerkt en kunnen ook worden verwijderd.

> [!NOTE]
> Een toepassingsmanifest kan meerdere service manifest invoer en standaardservices bevatten. Elke manifestimport service kan onafhankelijk samengestelde zijn.
> 
> 

hoe toomaintain andere toepassing en serviceparameters voor afzonderlijke omgevingen, Zie toolearn [beheren voor omgevingen met meerdere parameters voor de toepassing](service-fabric-manage-multiple-environment-app-configuration.md).

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a>Volgende stappen
[Een toepassing van het pakket](service-fabric-package-apps.md) , waardoor het toodeploy gereed.

[Implementeren en toepassingen verwijderen] [ 10] wordt beschreven hoe toouse PowerShell toomanage toepassingsexemplaren.

[Het beheren van parameters voor de toepassing voor omgevingen met meerdere] [ 11] wordt beschreven hoe tooconfigure parameters en variabelen voor exemplaren van een andere toepassing.

[Beveiligingsbeleid voor uw toepassing configureert] [ 12] wordt beschreven hoe toorun services onder beveiligingstoegang beleid toorestrict.

[Toepassing hosten modellen] [ 13] beschrijven de relatie tussen de replica's (of exemplaren) van een geïmplementeerde service en de ServiceHost proces.

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
