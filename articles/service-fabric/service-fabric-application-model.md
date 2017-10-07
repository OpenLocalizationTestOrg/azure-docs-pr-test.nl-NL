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
# <a name="model-an-application-in-service-fabric"></a><span data-ttu-id="22936-103">Model van een toepassing in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="22936-103">Model an application in Service Fabric</span></span>
<span data-ttu-id="22936-104">Dit artikel bevat een overzicht van Azure Service Fabric-toepassingsmodel Hallo en hoe toodefine een toepassing en service via bestanden manifest.</span><span class="sxs-lookup"><span data-stu-id="22936-104">This article provides an overview of hello Azure Service Fabric application model and how toodefine an application and service via manifest files.</span></span>

## <a name="understand-hello-application-model"></a><span data-ttu-id="22936-105">Hallo toepassingsmodel begrijpen</span><span class="sxs-lookup"><span data-stu-id="22936-105">Understand hello application model</span></span>
<span data-ttu-id="22936-106">Een toepassing is een verzameling van de services die een bepaalde functie of functies uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="22936-106">An application is a collection of constituent services that perform a certain function or functions.</span></span> <span data-ttu-id="22936-107">Een service kunt vervult een functie die volledig en zelfstandig starten en onafhankelijk van andere services worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="22936-107">A service performs a complete and standalone function and can start and run independently of other services.</span></span>  <span data-ttu-id="22936-108">Een service bestaat uit code, configuratie en gegevens.</span><span class="sxs-lookup"><span data-stu-id="22936-108">A service is composed of code, configuration, and data.</span></span> <span data-ttu-id="22936-109">Voor elke service code bestaat uit Hallo uitvoerbare binaire bestanden, configuratie bestaat uit de service-instellingen die kunnen worden geladen tijdens runtime en gegevens bestaan uit willekeurige statische gegevens toobe verbruikt door Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="22936-109">For each service, code consists of hello executable binaries, configuration consists of service settings that can be loaded at run time, and data consists of arbitrary static data toobe consumed by hello service.</span></span> <span data-ttu-id="22936-110">Elk onderdeel in dit toepassingsmodel hiërarchische kan worden samengesteld en bijgewerkte onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="22936-110">Each component in this hierarchical application model can be versioned and upgraded independently.</span></span>

![Hallo Service Fabric-toepassingsmodel][appmodel-diagram]

<span data-ttu-id="22936-112">Een toepassingstype een categorisatie van een toepassing is en bestaat uit een bundel van servicetypen.</span><span class="sxs-lookup"><span data-stu-id="22936-112">An application type is a categorization of an application and consists of a bundle of service types.</span></span> <span data-ttu-id="22936-113">Een service is een categorisatie van een service.</span><span class="sxs-lookup"><span data-stu-id="22936-113">A service type is a categorization of a service.</span></span> <span data-ttu-id="22936-114">Hallo categorisatie kan hebben verschillende instellingen en configuraties, maar Hallo core functionaliteit blijft Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="22936-114">hello categorization can have different settings and configurations, but hello core functionality remains hello same.</span></span> <span data-ttu-id="22936-115">Hallo exemplaren van een service zijn Hallo andere service configuration variaties Hallo dezelfde servicetype.</span><span class="sxs-lookup"><span data-stu-id="22936-115">hello instances of a service are hello different service configuration variations of hello same service type.</span></span>  

<span data-ttu-id="22936-116">Klassen (of 'typen') van toepassingen en services via XML-bestanden (Toepassingsmanifesten en service manifesten) worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="22936-116">Classes (or "types") of applications and services are described through XML files (application manifests and service manifests).</span></span>  <span data-ttu-id="22936-117">Hallo manifesten zijn Hallo-sjablonen op basis waarvan toepassingen uit de installatiekopieopslag Hallo-cluster kunnen worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="22936-117">hello manifests are hello templates against which applications can be instantiated from hello cluster's image store.</span></span> <span data-ttu-id="22936-118">Hallo schemadefinitie voor Hallo ServiceManifest.xml en ApplicationManifest.xml bestand is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="22936-118">hello schema definition for hello ServiceManifest.xml and ApplicationManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

<span data-ttu-id="22936-119">Hallo-code voor exemplaren van een andere toepassing zoals afzonderlijke processen, zelfs wanneer deze wordt gehost door Hallo dezelfde Service Fabric-knooppunt worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="22936-119">hello code for different application instances run as separate processes even when hosted by hello same Service Fabric node.</span></span> <span data-ttu-id="22936-120">Bovendien Hallo levenscyclus van elk toepassingsexemplaar kan worden beheerd (bijvoorbeeld een bijgewerkt) onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="22936-120">Furthermore, hello lifecycle of each application instance can be managed (for example, upgraded) independently.</span></span> <span data-ttu-id="22936-121">Hallo volgende diagram toont hoe toepassingstypen servicetype die op zijn beurt bestaan uit code, configuratie en gegevenspakketten zijn samengesteld.</span><span class="sxs-lookup"><span data-stu-id="22936-121">hello following diagram shows how application types are composed of service types, which in turn are composed of code, configuration, and data packages.</span></span> <span data-ttu-id="22936-122">toosimplify hello diagram alleen hello-pakketten config-code-gegevens voor `ServiceType4` worden weergegeven, hoewel elk servicetype u enkele vindt zou of alle pakkettypen.</span><span class="sxs-lookup"><span data-stu-id="22936-122">toosimplify hello diagram, only hello code/config/data packages for `ServiceType4` are shown, though each service type would include some or all those package types.</span></span>

![Service Fabric-toepassing waardetypen en servicetypen][cluster-imagestore-apptypes]

<span data-ttu-id="22936-124">Er zijn twee verschillende manifest bestanden gebruikte toodescribe toepassingen en services: Hallo servicemanifest en manifest van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="22936-124">Two different manifest files are used toodescribe applications and services: hello service manifest and application manifest.</span></span> <span data-ttu-id="22936-125">Manifesten worden in detail in Hallo volgende secties besproken.</span><span class="sxs-lookup"><span data-stu-id="22936-125">Manifests are covered in detail in hello following sections.</span></span>

<span data-ttu-id="22936-126">Er kan een of meer exemplaren van een servicetype actief zijn in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="22936-126">There can be one or more instances of a service type active in hello cluster.</span></span> <span data-ttu-id="22936-127">Bijvoorbeeld, bereiken stateful service-exemplaren of replica's hoge betrouwbaarheid status repliceren tussen replica's zich bevinden op andere knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="22936-127">For example, stateful service instances, or replicas, achieve high reliability by replicating state between replicas located on different nodes in hello cluster.</span></span> <span data-ttu-id="22936-128">Replicatie biedt in wezen redundantie voor Hallo service toobe beschikbaar, zelfs als een knooppunt in een cluster is mislukt.</span><span class="sxs-lookup"><span data-stu-id="22936-128">Replication essentially provides redundancy for hello service toobe available even if one node in a cluster fails.</span></span> <span data-ttu-id="22936-129">A [service gepartitioneerd](service-fabric-concepts-partitioning.md) verder delen de status (en toegangsstatus patronen toothat) tussen knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="22936-129">A [partitioned service](service-fabric-concepts-partitioning.md) further divides its state (and access patterns toothat state) across nodes in hello cluster.</span></span>

<span data-ttu-id="22936-130">Hallo toont volgende diagram Hallo relatie tussen toepassingen en service-exemplaren, partities en replica's.</span><span class="sxs-lookup"><span data-stu-id="22936-130">hello following diagram shows hello relationship between applications and service instances, partitions, and replicas.</span></span>

![Partities en replica's binnen een service][cluster-application-instances]

> [!TIP]
> <span data-ttu-id="22936-132">U kunt Hallo lay-out van toepassingen weergeven in een cluster met behulp van hulpprogramma voor Service Fabric Explorer Hallo beschikbaar op http://&lt;yourclusteraddress&gt;: 19080/Explorer.</span><span class="sxs-lookup"><span data-stu-id="22936-132">You can view hello layout of applications in a cluster using hello Service Fabric Explorer tool available at http://&lt;yourclusteraddress&gt;:19080/Explorer.</span></span> <span data-ttu-id="22936-133">Zie voor meer informatie [uw cluster visualiseren met Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="22936-133">For more information, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
> 
> 

## <a name="describe-a-service"></a><span data-ttu-id="22936-134">Een service omschrijven</span><span class="sxs-lookup"><span data-stu-id="22936-134">Describe a service</span></span>
<span data-ttu-id="22936-135">Hallo servicemanifest definieert declaratief Hallo servicetype en versie.</span><span class="sxs-lookup"><span data-stu-id="22936-135">hello service manifest declaratively defines hello service type and version.</span></span> <span data-ttu-id="22936-136">Hiermee wordt de metagegevens zoals servicetype, eigenschappen van health-taakverdeling metrische gegevens, de binaire bestanden en configuratiebestanden.</span><span class="sxs-lookup"><span data-stu-id="22936-136">It specifies service metadata such as service type, health properties, load-balancing metrics, service binaries, and configuration files.</span></span>  <span data-ttu-id="22936-137">Anders gezegd, Hallo code, configuratie en gegevens pakketten waaruit een service pakket toosupport beschrijft een of meer servicetypen.</span><span class="sxs-lookup"><span data-stu-id="22936-137">Put another way, it describes hello code, configuration, and data packages that compose a service package toosupport one or more service types.</span></span> <span data-ttu-id="22936-138">Dit is een eenvoudig voorbeeld servicemanifest:</span><span class="sxs-lookup"><span data-stu-id="22936-138">Here is a simple example service manifest:</span></span>

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

<span data-ttu-id="22936-139">**Versie** kenmerken ongestructureerde tekenreeksen zijn en niet worden geparseerd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="22936-139">**Version** attributes are unstructured strings and not parsed by hello system.</span></span> <span data-ttu-id="22936-140">Versie kenmerken zijn gebruikte tooversion elk onderdeel voor upgrades.</span><span class="sxs-lookup"><span data-stu-id="22936-140">Version attributes are used tooversion each component for upgrades.</span></span>

<span data-ttu-id="22936-141">**ServiceTypes** wordt gedeclareerd welke servicetypen worden ondersteund door **CodePackages** in dit manifest.</span><span class="sxs-lookup"><span data-stu-id="22936-141">**ServiceTypes** declares what service types are supported by **CodePackages** in this manifest.</span></span> <span data-ttu-id="22936-142">Wanneer een service met een van deze servicetypen wordt gestart, worden alle code pakketten die zijn gedefinieerd in deze manifest geactiveerd door het uitvoeren van hun toegangspunten.</span><span class="sxs-lookup"><span data-stu-id="22936-142">When a service is instantiated against one of these service types, all code packages declared in this manifest are activated by running their entry points.</span></span> <span data-ttu-id="22936-143">Hallo resulterende processen zijn servicetypen van verwachte tooregister Hallo ondersteund tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="22936-143">hello resulting processes are expected tooregister hello supported service types at run time.</span></span> <span data-ttu-id="22936-144">Service-typen zijn gedeclareerd op Hallo manifest niveau en niet Hallo code pakket.</span><span class="sxs-lookup"><span data-stu-id="22936-144">Service types are declared at hello manifest level and not hello code package level.</span></span> <span data-ttu-id="22936-145">Dus als er meerdere code pakketten, worden alle geactiveerd wanneer hello wordt gezocht naar een Hallo servicetypen gedeclareerd.</span><span class="sxs-lookup"><span data-stu-id="22936-145">So when there are multiple code packages, they are all activated whenever hello system looks for any one of hello declared service types.</span></span>

<span data-ttu-id="22936-146">**Entrypoint** is een bevoorrechte toegangspunt dat wordt uitgevoerd met dezelfde referenties als Service Fabric hello (meestal Hallo *LocalSystem* account) voordat andere toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="22936-146">**SetupEntryPoint** is a privileged entry point that runs with hello same credentials as Service Fabric (typically hello *LocalSystem* account) before any other entry point.</span></span> <span data-ttu-id="22936-147">Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** is doorgaans Hallo langlopende ServiceHost.</span><span class="sxs-lookup"><span data-stu-id="22936-147">hello executable specified by **EntryPoint** is typically hello long-running service host.</span></span> <span data-ttu-id="22936-148">Hallo aanwezigheid van een toegangspunt voor de afzonderlijke instellingen zo voorkomt u dat toorun Hallo ServiceHost met hoge bevoegdheden voor langere tijd.</span><span class="sxs-lookup"><span data-stu-id="22936-148">hello presence of a separate setup entry point avoids having toorun hello service host with high privileges for extended periods of time.</span></span> <span data-ttu-id="22936-149">Hallo uitvoerbaar bestand dat is opgegeven door **EntryPoint** wordt uitgevoerd na **entrypoint** is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="22936-149">hello executable specified by **EntryPoint** is run after **SetupEntryPoint** exits successfully.</span></span> <span data-ttu-id="22936-150">Als Hallo proces beëindigt ooit of vastloopt, Hallo resulterende proces wordt bewaakt en opnieuw opgestart (opnieuw vanaf **entrypoint**).</span><span class="sxs-lookup"><span data-stu-id="22936-150">If hello process ever terminates or crashes, hello resulting process is monitored and restarted (beginning again with **SetupEntryPoint**).</span></span>  

<span data-ttu-id="22936-151">Typische scenario's voor het gebruik van **entrypoint** zijn bij het uitvoeren van een uitvoerbaar bestand voordat Hallo-service wordt gestart of het uitvoeren van een bewerking met verhoogde bevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="22936-151">Typical scenarios for using **SetupEntryPoint** are when you run an executable before hello service starts or you perform an operation with elevated privileges.</span></span> <span data-ttu-id="22936-152">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="22936-152">For example:</span></span>

* <span data-ttu-id="22936-153">In te stellen en het initialiseren van omgevingsvariabelen die Hallo service uitvoerbare behoeften.</span><span class="sxs-lookup"><span data-stu-id="22936-153">Setting up and initializing environment variables that hello service executable needs.</span></span> <span data-ttu-id="22936-154">Dit is niet beperkt tooonly uitvoerbare bestanden via Hallo Service Fabric-programmeermodellen geschreven.</span><span class="sxs-lookup"><span data-stu-id="22936-154">This is not limited tooonly executables written via hello Service Fabric programming models.</span></span> <span data-ttu-id="22936-155">Npm.exe moet bijvoorbeeld een aantal omgevingsvariabelen die is geconfigureerd voor het implementeren van een node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="22936-155">For example, npm.exe needs some environment variables configured for deploying a node.js application.</span></span>
* <span data-ttu-id="22936-156">Instellen van toegangsbeheer door beveiligingscertificaten te installeren.</span><span class="sxs-lookup"><span data-stu-id="22936-156">Setting up access control by installing security certificates.</span></span>

<span data-ttu-id="22936-157">Voor meer informatie over het tooconfigure hello **entrypoint** Zie [Hallo beleid configureren voor een service-instelling toegangspunt.](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="22936-157">For more details on how tooconfigure hello **SetupEntryPoint** see [Configure hello policy for a service setup entry point](service-fabric-application-runas-security.md)</span></span>

<span data-ttu-id="22936-158">**Omgevingsvariabelen** geeft een lijst van omgevingsvariabelen die zijn ingesteld voor dit codepakket.</span><span class="sxs-lookup"><span data-stu-id="22936-158">**EnvironmentVariables** provides a list of environment variables that are set for this code package.</span></span> <span data-ttu-id="22936-159">Environmentment variabelen kunnen worden overschreven in Hallo `ApplicationManifest.xml` tooprovide verschillende waarden voor verschillende service-exemplaren.</span><span class="sxs-lookup"><span data-stu-id="22936-159">Environmentment variables can be overridden in hello `ApplicationManifest.xml` tooprovide different values for different service instances.</span></span> 

<span data-ttu-id="22936-160">**Gegevenspakket** declareert een map met de naam door Hallo **naam** kenmerk met willekeurige statische gegevens toobe verbruikt door Hallo proces tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="22936-160">**DataPackage** declares a folder, named by hello **Name** attribute, that contains arbitrary static data toobe consumed by hello process at run time.</span></span>

<span data-ttu-id="22936-161">**ConfigPackage** declareert een map met de naam door Hallo **naam** kenmerk dat bevat een *Settings.xml* bestand.</span><span class="sxs-lookup"><span data-stu-id="22936-161">**ConfigPackage** declares a folder, named by hello **Name** attribute, that contains a *Settings.xml* file.</span></span> <span data-ttu-id="22936-162">Hallo instellingenbestand bevat secties van de gebruiker gedefinieerde, sleutel / waarde-paar-instellingen die Hallo proces tijdens de uitvoering leest.</span><span class="sxs-lookup"><span data-stu-id="22936-162">hello settings file contains sections of user-defined, key-value pair settings that hello process reads back at run time.</span></span> <span data-ttu-id="22936-163">Tijdens een upgrade als alleen Hallo **ConfigPackage** **versie** is gewijzigd, en vervolgens Hallo process uitgevoerd niet opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="22936-163">During an upgrade, if only hello **ConfigPackage** **version** has changed, then hello running process is not restarted.</span></span> <span data-ttu-id="22936-164">In plaats daarvan waarschuwt een retouraanroep Hallo-proces dat configuratie-instellingen hebt gewijzigd zodat ze opnieuw kunnen worden geladen dynamisch.</span><span class="sxs-lookup"><span data-stu-id="22936-164">Instead, a callback notifies hello process that configuration settings have changed so they can be reloaded dynamically.</span></span> <span data-ttu-id="22936-165">Hier volgt een voorbeeld *Settings.xml* bestand:</span><span class="sxs-lookup"><span data-stu-id="22936-165">Here is an example *Settings.xml* file:</span></span>

```xml
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MyConfigurationSection">
    <Parameter Name="MySettingA" Value="Example1" />
    <Parameter Name="MySettingB" Value="Example2" />
  </Section>
</Settings>
```

> [!NOTE]
> <span data-ttu-id="22936-166">Een servicemanifest kan meerdere code, configuratie en gegevenspakketten bevatten.</span><span class="sxs-lookup"><span data-stu-id="22936-166">A service manifest can contain multiple code, configuration, and data packages.</span></span> <span data-ttu-id="22936-167">Elk van deze kan worden samengesteld onafhankelijk.</span><span class="sxs-lookup"><span data-stu-id="22936-167">Each of those can be versioned independently.</span></span>
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

## <a name="describe-an-application"></a><span data-ttu-id="22936-168">Een toepassing beschrijven</span><span class="sxs-lookup"><span data-stu-id="22936-168">Describe an application</span></span>
<span data-ttu-id="22936-169">Hallo-toepassingsmanifest beschrijft declaratief Hallo toepassingstype en -versie.</span><span class="sxs-lookup"><span data-stu-id="22936-169">hello application manifest declaratively describes hello application type and version.</span></span> <span data-ttu-id="22936-170">Deze geeft service samenstelling metagegevens zoals stabiele namen, partitioneren schema, exemplaar count/replicatie factor/isolatie-beleid, plaatsingsbeperkingen, configuratie onderdrukkingen en samenstellende servicetypen.</span><span class="sxs-lookup"><span data-stu-id="22936-170">It specifies service composition metadata such as stable names, partitioning scheme, instance count/replication factor, security/isolation policy, placement constraints, configuration overrides, and constituent service types.</span></span> <span data-ttu-id="22936-171">Hallo-taakverdeling domeinen waarin de toepassing hello is geplaatst, worden ook beschreven.</span><span class="sxs-lookup"><span data-stu-id="22936-171">hello load-balancing domains into which hello application is placed are also described.</span></span>

<span data-ttu-id="22936-172">Dus een toepassingsmanifest worden elementen op toepassingsniveau Hallo beschreven en verwijst naar een of meer service-manifesten toocompose een toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22936-172">Thus, an application manifest describes elements at hello application level and references one or more service manifests toocompose an application type.</span></span> <span data-ttu-id="22936-173">Dit is een eenvoudig voorbeeld toepassingsmanifest:</span><span class="sxs-lookup"><span data-stu-id="22936-173">Here is a simple example application manifest:</span></span>

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

<span data-ttu-id="22936-174">Service manifesten, zoals **versie** kenmerken ongestructureerde tekenreeksen zijn en niet worden geparseerd door Hallo-systeem.</span><span class="sxs-lookup"><span data-stu-id="22936-174">Like service manifests, **Version** attributes are unstructured strings and are not parsed by hello system.</span></span> <span data-ttu-id="22936-175">Versie kenmerken zijn ook gebruikte tooversion elk onderdeel voor upgrades.</span><span class="sxs-lookup"><span data-stu-id="22936-175">Version attributes are also used tooversion each component for upgrades.</span></span>

<span data-ttu-id="22936-176">**ServiceManifestImport** bevat verwijzingen tooservice manifesten waaruit dit toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22936-176">**ServiceManifestImport** contains references tooservice manifests that compose this application type.</span></span> <span data-ttu-id="22936-177">Geïmporteerde service manifesten bepalen welke servicetypen zijn geldig binnen dit toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22936-177">Imported service manifests determine what service types are valid within this application type.</span></span> <span data-ttu-id="22936-178">Binnen Hallo ServiceManifestImport, moet u configuratiewaarden in Settings.xml en omgevingsvariabelen in ServiceManifest.xml bestanden overschrijven.</span><span class="sxs-lookup"><span data-stu-id="22936-178">Within hello ServiceManifestImport, you override configuration values in Settings.xml and environment variables in ServiceManifest.xml files.</span></span> 


<span data-ttu-id="22936-179">**DefaultServices** declareert service-exemplaren die automatisch worden gemaakt wanneer een toepassing wordt gestart op basis van dit toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="22936-179">**DefaultServices** declares service instances that are automatically created whenever an application is instantiated against this application type.</span></span> <span data-ttu-id="22936-180">Standaardservices zijn alleen gemakkelijker te maken en zich gedragen als normale services in elke opzicht nadat ze zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="22936-180">Default services are just a convenience and behave like normal services in every respect after they have been created.</span></span> <span data-ttu-id="22936-181">Deze samen met andere services in het toepassingsexemplaar Hallo zijn bijgewerkt en kunnen ook worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="22936-181">They are upgraded along with any other services in hello application instance and can be removed as well.</span></span>

> [!NOTE]
> <span data-ttu-id="22936-182">Een toepassingsmanifest kan meerdere service manifest invoer en standaardservices bevatten.</span><span class="sxs-lookup"><span data-stu-id="22936-182">An application manifest can contain multiple service manifest imports and default services.</span></span> <span data-ttu-id="22936-183">Elke manifestimport service kan onafhankelijk samengestelde zijn.</span><span class="sxs-lookup"><span data-stu-id="22936-183">Each service manifest import can be versioned independently.</span></span>
> 
> 

<span data-ttu-id="22936-184">hoe toomaintain andere toepassing en serviceparameters voor afzonderlijke omgevingen, Zie toolearn [beheren voor omgevingen met meerdere parameters voor de toepassing](service-fabric-manage-multiple-environment-app-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="22936-184">toolearn how toomaintain different application and service parameters for individual environments, see [Managing application parameters for multiple environments](service-fabric-manage-multiple-environment-app-configuration.md).</span></span>

<!--
For more information about other features supported by application manifests, refer toohello following articles:

*TODO: Application parameters
*TODO: Security, Principals, RunAs, SecurityAccessPolicy
*TODO: Service Templates
-->



## <a name="next-steps"></a><span data-ttu-id="22936-185">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="22936-185">Next steps</span></span>
<span data-ttu-id="22936-186">[Een toepassing van het pakket](service-fabric-package-apps.md) , waardoor het toodeploy gereed.</span><span class="sxs-lookup"><span data-stu-id="22936-186">[Package an application](service-fabric-package-apps.md) and make it ready toodeploy.</span></span>

<span data-ttu-id="22936-187">[Implementeren en toepassingen verwijderen] [ 10] wordt beschreven hoe toouse PowerShell toomanage toepassingsexemplaren.</span><span class="sxs-lookup"><span data-stu-id="22936-187">[Deploy and remove applications][10] describes how toouse PowerShell toomanage application instances.</span></span>

<span data-ttu-id="22936-188">[Het beheren van parameters voor de toepassing voor omgevingen met meerdere] [ 11] wordt beschreven hoe tooconfigure parameters en variabelen voor exemplaren van een andere toepassing.</span><span class="sxs-lookup"><span data-stu-id="22936-188">[Managing application parameters for multiple environments][11] describes how tooconfigure parameters and environment variables for different application instances.</span></span>

<span data-ttu-id="22936-189">[Beveiligingsbeleid voor uw toepassing configureert] [ 12] wordt beschreven hoe toorun services onder beveiligingstoegang beleid toorestrict.</span><span class="sxs-lookup"><span data-stu-id="22936-189">[Configure security policies for your application][12] describes how toorun services under security policies toorestrict access.</span></span>

<span data-ttu-id="22936-190">[Toepassing hosten modellen] [ 13] beschrijven de relatie tussen de replica's (of exemplaren) van een geïmplementeerde service en de ServiceHost proces.</span><span class="sxs-lookup"><span data-stu-id="22936-190">[Application hosting models][13] describe relationship between replicas (or instances) of a deployed service and service-host process.</span></span>

<!--Image references-->
[appmodel-diagram]: ./media/service-fabric-application-model/application-model.png
[cluster-imagestore-apptypes]: ./media/service-fabric-application-model/cluster-imagestore-apptypes.png
[cluster-application-instances]: media/service-fabric-application-model/cluster-application-instances.png

<!--Link references--In actual articles, you only need a single period before hello slash-->
[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-manage-multiple-environment-app-configuration.md
[12]: service-fabric-application-runas-security.md
[13]: service-fabric-hosting-model.md
