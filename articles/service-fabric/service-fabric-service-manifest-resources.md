---
title: Service Fabric-service-eindpunten aaaSpecifying | Microsoft Docs
description: Hoe toodescribe eindpunt resources in een service manifest, met inbegrip van hoe tooset HTTPS-eindpunten
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: da36cbdb-6531-4dae-88e8-a311ab71520d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: subramar
ms.openlocfilehash: a4ebee353ce5cf86583673674246094f03f368be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="dcb03-103">Resources specificeren in een servicemanifest</span><span class="sxs-lookup"><span data-stu-id="dcb03-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="dcb03-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="dcb03-104">Overview</span></span>
<span data-ttu-id="dcb03-105">Hallo servicemanifest kan resources die worden gebruikt door Hallo service toobe gedeclareerd of gewijzigd zonder Hallo gecompileerde code te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="dcb03-105">hello service manifest allows resources that are used by hello service toobe declared/changed without changing hello compiled code.</span></span> <span data-ttu-id="dcb03-106">Azure Service Fabric ondersteunt de configuratie van endpoint-resources voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="dcb03-106">Azure Service Fabric supports configuration of endpoint resources for hello service.</span></span> <span data-ttu-id="dcb03-107">Hallo toegang toohello resources die zijn opgegeven in het Hallo-servicemanifest kunnen worden beheerd via Hallo beveiligingsgroep in het toepassingsmanifest Hallo.</span><span class="sxs-lookup"><span data-stu-id="dcb03-107">hello access toohello resources that are specified in hello service manifest can be controlled via hello SecurityGroup in hello application manifest.</span></span> <span data-ttu-id="dcb03-108">Hallo-declaratie van resources kunt deze resources toobe gewijzigd tijdens de implementatie, wat betekent dat Hallo service hoeft niet toointroduce een nieuw configuratie-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="dcb03-108">hello declaration of resources allows these resources toobe changed at deployment time, meaning hello service doesn't need toointroduce a new configuration mechanism.</span></span> <span data-ttu-id="dcb03-109">Hallo schemadefinitie voor Hallo ServiceManifest.xml bestand is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="dcb03-109">hello schema definition for hello ServiceManifest.xml file is installed with hello Service Fabric SDK and tools too*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="dcb03-110">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="dcb03-110">Endpoints</span></span>
<span data-ttu-id="dcb03-111">Als endpoint-bron is gedefinieerd in het manifest voor Hallo-service, wijst Service Fabric de poorten van Hallo gereserveerd toepassingspoortbereik wanneer een poort expliciet is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dcb03-111">When an endpoint resource is defined in hello service manifest, Service Fabric assigns ports from hello reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="dcb03-112">Zoek bijvoorbeeld naar op Hallo eindpunt *ServiceEndpoint1* opgegeven in het manifest Hallo-codefragment die na dit lid.</span><span class="sxs-lookup"><span data-stu-id="dcb03-112">For example, look at hello endpoint *ServiceEndpoint1* specified in hello manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="dcb03-113">Services kunnen bovendien ook aanvragen voor een specifieke poort in een resource.</span><span class="sxs-lookup"><span data-stu-id="dcb03-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="dcb03-114">Service-replica's uitgevoerd op verschillende knooppunten kunnen worden toegewezen worden andere poortnummers, terwijl de replica's van een service die wordt uitgevoerd op hetzelfde knooppunt share Hallo poort Hallo.</span><span class="sxs-lookup"><span data-stu-id="dcb03-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on hello same node share hello port.</span></span> <span data-ttu-id="dcb03-115">Hallo service replica's kunnen deze poorten vervolgens naar wens gebruiken voor replicatie en luistert naar aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="dcb03-115">hello service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="dcb03-116">Raadpleeg te[configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread meer informatie over die verwijzen naar eindpunten vanuit Hallo configuratie-instellingen pakketbestand (settings.xml).</span><span class="sxs-lookup"><span data-stu-id="dcb03-116">Refer too[Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread more about referencing endpoints from hello config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="dcb03-117">Voorbeeld: een HTTP-eindpunt voor uw service opgeven</span><span class="sxs-lookup"><span data-stu-id="dcb03-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="dcb03-118">Hallo volgende servicemanifest definieert één resource voor TCP-eindpunt en bronnen van twee HTTP-eindpunt op Hallo &lt;Resources&gt; element.</span><span class="sxs-lookup"><span data-stu-id="dcb03-118">hello following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in hello &lt;Resources&gt; element.</span></span>

<span data-ttu-id="dcb03-119">HTTP-eindpunten worden automatisch dat ACL zou door Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="dcb03-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         This name must match hello string used in hello RegisterServiceType call in Program.cs. -->
    <StatefulServiceType ServiceTypeName="Stateful1Type" HasPersistedState="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <ExeHost>
        <Program>Stateful1.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by hello replicator for replicating hello state of your service.
           This endpoint is configured through hello ReplicatorSettings config section in hello Settings.xml
           file under hello ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="dcb03-120">Voorbeeld: een HTTPS-eindpunt voor uw service opgeven</span><span class="sxs-lookup"><span data-stu-id="dcb03-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="dcb03-121">Hallo HTTPS-protocol biedt verificatie van de server en wordt ook gebruikt voor het versleutelen van de client-servercommunicatie.</span><span class="sxs-lookup"><span data-stu-id="dcb03-121">hello HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="dcb03-122">tooenable HTTPS op uw Service Fabric-service, Hallo protocol opgeven in Hallo *Resources-eindpunten > Endpoint ->* sectie van Hallo servicemanifest, zoals eerder besproken voor het eindpunt Hallo *ServiceEndpoint3* .</span><span class="sxs-lookup"><span data-stu-id="dcb03-122">tooenable HTTPS on your Service Fabric service, specify hello protocol in hello *Resources -> Endpoints -> Endpoint* section of hello service manifest, as shown earlier for hello endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="dcb03-123">Een service-protocol kan niet worden gewijzigd tijdens de upgrade van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="dcb03-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="dcb03-124">Als deze is gewijzigd tijdens de upgrade, is een belangrijke wijziging.</span><span class="sxs-lookup"><span data-stu-id="dcb03-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="dcb03-125">Hier volgt een voorbeeld ApplicationManifest moet u tooset voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dcb03-125">Here is an example ApplicationManifest that you need tooset for HTTPS.</span></span> <span data-ttu-id="dcb03-126">Hallo vingerafdruk voor het certificaat moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dcb03-126">hello thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="dcb03-127">Hallo EndpointRef is een verwijzing tooEndpointResource in ServiceManifest, waarvoor u de HTTPS-protocol Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="dcb03-127">hello EndpointRef is a reference tooEndpointResource in ServiceManifest, for which you set hello HTTPS protocol.</span></span> <span data-ttu-id="dcb03-128">U kunt meer dan één EndpointCertificate toevoegen.</span><span class="sxs-lookup"><span data-stu-id="dcb03-128">You can add more than one EndpointCertificate.</span></span>  

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="Application1Type"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
    <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
    <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Stateful1">
      <StatefulService ServiceTypeName="Stateful1Type" TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]" MinReplicaSetSize="[Stateful1_ ]">
        <UniformInt64Partition PartitionCount="[Stateful1_PartitionCount]" LowKey="-9223372036854775808" HighKey="9223372036854775807" />
      </StatefulService>
    </Service>
  </DefaultServices>
  <Certificates>
    <EndpointCertificate Name="TestCert1" X509FindValue="FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF FF F0" X509StoreName="MY" />  
  </Certificates>
</ApplicationManifest>
```

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="dcb03-129">Eindpunten in ServiceManifest.xml overschrijven</span><span class="sxs-lookup"><span data-stu-id="dcb03-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="dcb03-130">Voeg een sectie ResourceOverrides die als een lid op hetzelfde niveau tooConfigOverrides sectie Hallo ApplicationManifest.</span><span class="sxs-lookup"><span data-stu-id="dcb03-130">In hello ApplicationManifest add a ResourceOverrides section which will be a sibling tooConfigOverrides section.</span></span> <span data-ttu-id="dcb03-131">In deze sectie kunt u Hallo onderdrukking voor Hallo eindpunten in de sectie van Hallo resources die zijn opgegeven in het Hallo-servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="dcb03-131">In this section you can specify hello override for hello Endpoints section in hello resources section specified in hello Service manifest.</span></span>

<span data-ttu-id="dcb03-132">Hallo in volgorde toooverride eindpunt in ServiceManifest ApplicationParameters wijzigen met ApplicationManifest als volgt:</span><span class="sxs-lookup"><span data-stu-id="dcb03-132">In order toooverride EndPoint in ServiceManifest using ApplicationParameters change hello ApplicationManifest as following:</span></span>

<span data-ttu-id="dcb03-133">Voeg een nieuwe sectie 'ResourceOverrides' in hello ServiceManifestImport sectie</span><span class="sxs-lookup"><span data-stu-id="dcb03-133">In hello ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

```xml
<ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <ResourceOverrides>
      <Endpoints>
        <Endpoint Name="ServiceEndpoint" Port="[Port]" Protocol="[Protocol]" Type="[Type]" />
        <Endpoint Name="ServiceEndpoint1" Port="[Port1]" Protocol="[Protocol1] "/>
      </Endpoints>
    </ResourceOverrides>
        <Policies>
           <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint"/>
        </Policies>
  </ServiceManifestImport>
```

<span data-ttu-id="dcb03-134">In de Hallo die parameters hieronder toevoegen:</span><span class="sxs-lookup"><span data-stu-id="dcb03-134">In hello Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="dcb03-135">Tijdens de implementatie van de toepassing nu Hallo kunt u deze waarden als doorgeven ApplicationParameters bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dcb03-135">While deploying hello application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="dcb03-136">Opmerking: Als Hallo waarden opgeven voor Hallo ApplicationParameters leeg is we gaat u terug toohello standaard waarde die is opgegeven in Hallo ServiceManifest voor Hallo EndPointName overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="dcb03-136">Note: If hello values provide for hello ApplicationParameters is empty we go back toohello default value provided in hello ServiceManifest for hello corresponding EndPointName.</span></span>

<span data-ttu-id="dcb03-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dcb03-137">For example:</span></span>

<span data-ttu-id="dcb03-138">Indien in Hallo ServiceManifest die u hebt opgegeven</span><span class="sxs-lookup"><span data-stu-id="dcb03-138">If in hello ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="dcb03-139">Hallo Port1 en Protocol1 waarde voor de parameters voor de toepassing is null of leeg.</span><span class="sxs-lookup"><span data-stu-id="dcb03-139">And hello Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="dcb03-140">Hallo-poort wordt nog steeds bepaald door ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="dcb03-140">hello port is still decided by ServiceFabric.</span></span> <span data-ttu-id="dcb03-141">En Hallo Protocol tcp wordt.</span><span class="sxs-lookup"><span data-stu-id="dcb03-141">And hello Protocol will tcp.</span></span>

<span data-ttu-id="dcb03-142">Stel dat u een onjuiste waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="dcb03-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="dcb03-143">Net als voor de poort u hebt opgegeven een tekenreekswaarde "Foo" in plaats van een int.  Nieuwe ServiceFabricApplication opdracht mislukt met een fout opgetreden: Hallo overrideparameter met de 'ServiceEndpoint1' naamkenmerk 'Port1' in sectie 'ResourceOverrides' is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="dcb03-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : hello override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="dcb03-144">Hallo waarde die is opgegeven is 'Foo' en 'integer' vereist is.</span><span class="sxs-lookup"><span data-stu-id="dcb03-144">hello value specified is 'Foo' and required is 'int'.</span></span>
