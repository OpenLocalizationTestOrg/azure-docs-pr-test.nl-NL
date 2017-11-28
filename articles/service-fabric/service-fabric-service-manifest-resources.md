---
title: Service Fabric-service-eindpunten geven | Microsoft Docs
description: Het eindpunt resources in een servicemanifest van de, inclusief het instellen van HTTPS-eindpunten beschrijven
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
ms.openlocfilehash: 08141edfbc8be9bf7bf303419e1e482d5f884860
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="specify-resources-in-a-service-manifest"></a><span data-ttu-id="17c57-103">Resources specificeren in een servicemanifest</span><span class="sxs-lookup"><span data-stu-id="17c57-103">Specify resources in a service manifest</span></span>
## <a name="overview"></a><span data-ttu-id="17c57-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="17c57-104">Overview</span></span>
<span data-ttu-id="17c57-105">Het servicemanifest kunt resources die worden gebruikt door de service worden gedeclareerd of gewijzigd zonder de gecompileerde code te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="17c57-105">The service manifest allows resources that are used by the service to be declared/changed without changing the compiled code.</span></span> <span data-ttu-id="17c57-106">Azure Service Fabric ondersteunt de configuratie van endpoint-resources voor de service.</span><span class="sxs-lookup"><span data-stu-id="17c57-106">Azure Service Fabric supports configuration of endpoint resources for the service.</span></span> <span data-ttu-id="17c57-107">De toegang tot de resources die zijn opgegeven in het servicemanifest kan worden beheerd via de beveiligingsgroep in het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="17c57-107">The access to the resources that are specified in the service manifest can be controlled via the SecurityGroup in the application manifest.</span></span> <span data-ttu-id="17c57-108">De declaratie van resources kunt deze resources worden gewijzigd tijdens de implementatie, wat betekent dat de service niet hoeft te introduceren een nieuwe configuratie-mechanisme.</span><span class="sxs-lookup"><span data-stu-id="17c57-108">The declaration of resources allows these resources to be changed at deployment time, meaning the service doesn't need to introduce a new configuration mechanism.</span></span> <span data-ttu-id="17c57-109">De schemadefinitie voor het bestand ServiceManifest.xml is geïnstalleerd met de Service Fabric SDK en hulpprogramma's voor *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span><span class="sxs-lookup"><span data-stu-id="17c57-109">The schema definition for the ServiceManifest.xml file is installed with the Service Fabric SDK and tools to *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.</span></span>

## <a name="endpoints"></a><span data-ttu-id="17c57-110">Eindpunten</span><span class="sxs-lookup"><span data-stu-id="17c57-110">Endpoints</span></span>
<span data-ttu-id="17c57-111">Als een resource van het eindpunt is gedefinieerd in het servicemanifest, wijst Service Fabric de poorten van de gereserveerde toepassingspoortbereik wanneer een poort expliciet is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="17c57-111">When an endpoint resource is defined in the service manifest, Service Fabric assigns ports from the reserved application port range when a port isn't specified explicitly.</span></span> <span data-ttu-id="17c57-112">Zoek bijvoorbeeld naar op het eindpunt *ServiceEndpoint1* opgegeven in het manifest codefragment die na dit lid.</span><span class="sxs-lookup"><span data-stu-id="17c57-112">For example, look at the endpoint *ServiceEndpoint1* specified in the manifest snippet provided after this paragraph.</span></span> <span data-ttu-id="17c57-113">Services kunnen bovendien ook aanvragen voor een specifieke poort in een resource.</span><span class="sxs-lookup"><span data-stu-id="17c57-113">Additionally, services can also request a specific port in a resource.</span></span> <span data-ttu-id="17c57-114">Service-replica's uitgevoerd op verschillende knooppunten kunnen worden toegewezen worden andere poortnummers, terwijl de replica's van een service die wordt uitgevoerd op hetzelfde knooppunt poort delen.</span><span class="sxs-lookup"><span data-stu-id="17c57-114">Service replicas running on different cluster nodes can be assigned different port numbers, while replicas of a service running on the same node share the port.</span></span> <span data-ttu-id="17c57-115">De service-replica's kunnen deze poorten vervolgens naar wens gebruiken voor replicatie en luistert naar aanvragen van clients.</span><span class="sxs-lookup"><span data-stu-id="17c57-115">The service replicas can then use these ports as needed for replication and listening for client requests.</span></span>

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="17c57-116">Raadpleeg [configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md) meer informatie over die verwijzen naar de eindpunten van de instellingen van de config-pakket (settings.xml) bestand lezen.</span><span class="sxs-lookup"><span data-stu-id="17c57-116">Refer to [Configuring stateful Reliable Services](service-fabric-reliable-services-configuration.md) to read more about referencing endpoints from the config package settings file (settings.xml).</span></span>

## <a name="example-specifying-an-http-endpoint-for-your-service"></a><span data-ttu-id="17c57-117">Voorbeeld: een HTTP-eindpunt voor uw service opgeven</span><span class="sxs-lookup"><span data-stu-id="17c57-117">Example: specifying an HTTP endpoint for your service</span></span>
<span data-ttu-id="17c57-118">De volgende servicemanifest definieert één resource voor TCP-eindpunt en twee HTTP-eindpunt bronnen in de &lt;Resources&gt; element.</span><span class="sxs-lookup"><span data-stu-id="17c57-118">The following service manifest defines one TCP endpoint resource and two HTTP endpoint resources in the &lt;Resources&gt; element.</span></span>

<span data-ttu-id="17c57-119">HTTP-eindpunten worden automatisch dat ACL zou door Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="17c57-119">HTTP endpoints are automatically ACL'd by Service Fabric.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Stateful1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         This name must match the string used in the RegisterServiceType call in Program.cs. -->
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

  <!-- Config package is the contents of the Config directoy under PackageRoot that contains an
       independently updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port number on which to
           listen. Note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
      <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
      <Endpoint Name="ServiceEndpoint3" Protocol="https"/>

      <!-- This endpoint is used by the replicator for replicating the state of your service.
           This endpoint is configured through the ReplicatorSettings config section in the Settings.xml
           file under the ConfigPackage. -->
      <Endpoint Name="ReplicatorEndpoint" />
    </Endpoints>
  </Resources>
</ServiceManifest>
```

## <a name="example-specifying-an-https-endpoint-for-your-service"></a><span data-ttu-id="17c57-120">Voorbeeld: een HTTPS-eindpunt voor uw service opgeven</span><span class="sxs-lookup"><span data-stu-id="17c57-120">Example: specifying an HTTPS endpoint for your service</span></span>
<span data-ttu-id="17c57-121">Het HTTPS-protocol biedt verificatie van de server en wordt ook gebruikt voor het versleutelen van de client-servercommunicatie.</span><span class="sxs-lookup"><span data-stu-id="17c57-121">The HTTPS protocol provides server authentication and is also used for encrypting client-server communication.</span></span> <span data-ttu-id="17c57-122">Geef het protocol in voor het HTTPS inschakelen voor uw Service Fabric-service, de *Resources-eindpunten > -> Endpoint* sectie van de servicemanifest, zoals eerder besproken voor het eindpunt *ServiceEndpoint3*.</span><span class="sxs-lookup"><span data-stu-id="17c57-122">To enable HTTPS on your Service Fabric service, specify the protocol in the *Resources -> Endpoints -> Endpoint* section of the service manifest, as shown earlier for the endpoint *ServiceEndpoint3*.</span></span>

> [!NOTE]
> <span data-ttu-id="17c57-123">Een service-protocol kan niet worden gewijzigd tijdens de upgrade van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="17c57-123">A service’s protocol cannot be changed during application upgrade.</span></span> <span data-ttu-id="17c57-124">Als deze is gewijzigd tijdens de upgrade, is een belangrijke wijziging.</span><span class="sxs-lookup"><span data-stu-id="17c57-124">If it is changed during upgrade, it is a breaking change.</span></span>
> 
> 

<span data-ttu-id="17c57-125">Hier volgt een voorbeeld ApplicationManifest die u nodig hebt om in te stellen voor HTTPS.</span><span class="sxs-lookup"><span data-stu-id="17c57-125">Here is an example ApplicationManifest that you need to set for HTTPS.</span></span> <span data-ttu-id="17c57-126">De vingerafdruk van het certificaat moet worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="17c57-126">The thumbprint for your certificate must be provided.</span></span> <span data-ttu-id="17c57-127">De EndpointRef is een verwijzing naar EndpointResource in ServiceManifest, waarvoor u het HTTPS-protocol hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="17c57-127">The EndpointRef is a reference to EndpointResource in ServiceManifest, for which you set the HTTPS protocol.</span></span> <span data-ttu-id="17c57-128">U kunt meer dan één EndpointCertificate toevoegen.</span><span class="sxs-lookup"><span data-stu-id="17c57-128">You can add more than one EndpointCertificate.</span></span>  

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
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion
       should match the Name and Version attributes of the ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <EndpointBindingPolicy CertificateRef="TestCert1" EndpointRef="ServiceEndpoint3"/>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- The section below creates instances of service types when an instance of this
         application type is created. You can also create one or more instances of service type by using the
         Service Fabric PowerShell module.

         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
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

## <a name="overriding-endpoints-in-servicemanifestxml"></a><span data-ttu-id="17c57-129">Eindpunten in ServiceManifest.xml overschrijven</span><span class="sxs-lookup"><span data-stu-id="17c57-129">Overriding Endpoints in ServiceManifest.xml</span></span>

<span data-ttu-id="17c57-130">In de ApplicationManifest toevoegen een sectie ResourceOverrides die op hetzelfde niveau ConfigOverrides gedeelte.</span><span class="sxs-lookup"><span data-stu-id="17c57-130">In the ApplicationManifest add a ResourceOverrides section which will be a sibling to ConfigOverrides section.</span></span> <span data-ttu-id="17c57-131">In deze sectie kunt u de onderdrukking voor de sectie eindpunten in de bronnensectie is opgegeven in het manifest van de Service.</span><span class="sxs-lookup"><span data-stu-id="17c57-131">In this section you can specify the override for the Endpoints section in the resources section specified in the Service manifest.</span></span>

<span data-ttu-id="17c57-132">Om te overschrijven eindpunt in ServiceManifest ApplicationParameters wijzigen de ApplicationManifest als volgt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="17c57-132">In order to override EndPoint in ServiceManifest using ApplicationParameters change the ApplicationManifest as following:</span></span>

<span data-ttu-id="17c57-133">Voeg een nieuwe sectie 'ResourceOverrides' in de sectie ServiceManifestImport</span><span class="sxs-lookup"><span data-stu-id="17c57-133">In the ServiceManifestImport section add a new section "ResourceOverrides"</span></span>

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

<span data-ttu-id="17c57-134">In de Parameters die hieronder worden toevoegen:</span><span class="sxs-lookup"><span data-stu-id="17c57-134">In the Parameters add below:</span></span>

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

<span data-ttu-id="17c57-135">Tijdens de implementatie van de toepassing nu kunt u doorgeven in deze waarden als ApplicationParameters bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17c57-135">While deploying the application now you can pass in these values as ApplicationParameters for example:</span></span>

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

<span data-ttu-id="17c57-136">Opmerking: Als de waarden voor de ApplicationParameters leeg is bieden we Ga terug naar de standaardwaarde opgegeven in de ServiceManifest voor de bijbehorende EndPointName.</span><span class="sxs-lookup"><span data-stu-id="17c57-136">Note: If the values provide for the ApplicationParameters is empty we go back to the default value provided in the ServiceManifest for the corresponding EndPointName.</span></span>

<span data-ttu-id="17c57-137">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="17c57-137">For example:</span></span>

<span data-ttu-id="17c57-138">Als in de ServiceManifest die u hebt opgegeven</span><span class="sxs-lookup"><span data-stu-id="17c57-138">If in the ServiceManifest you specified</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

<span data-ttu-id="17c57-139">En de waarde voor Port1 en Protocol1 voor parameters van toepassing is null of leeg.</span><span class="sxs-lookup"><span data-stu-id="17c57-139">And the Port1 and Protocol1 value for Application parameters is null or empty.</span></span> <span data-ttu-id="17c57-140">De poort wordt nog steeds bepaald door ServiceFabric.</span><span class="sxs-lookup"><span data-stu-id="17c57-140">The port is still decided by ServiceFabric.</span></span> <span data-ttu-id="17c57-141">En de TCP-Protocol wordt.</span><span class="sxs-lookup"><span data-stu-id="17c57-141">And the Protocol will tcp.</span></span>

<span data-ttu-id="17c57-142">Stel dat u een onjuiste waarde opgeven.</span><span class="sxs-lookup"><span data-stu-id="17c57-142">Suppose you specify a wrong value.</span></span> <span data-ttu-id="17c57-143">Net als voor de poort u hebt opgegeven een tekenreekswaarde "Foo" in plaats van een int.  Nieuwe ServiceFabricApplication opdracht mislukt met een fout opgetreden: de overrideparameter met de naam 'ServiceEndpoint1' kenmerk 'Port1' in sectie 'ResourceOverrides' is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="17c57-143">Like for Port you specified a string value "Foo" instead of an int.  New-ServiceFabricApplication command will fail with an error : The override parameter with name 'ServiceEndpoint1' attribute 'Port1' in section 'ResourceOverrides' is invalid.</span></span> <span data-ttu-id="17c57-144">De opgegeven waarde is 'Foo' en 'integer' vereist is.</span><span class="sxs-lookup"><span data-stu-id="17c57-144">The value specified is 'Foo' and required is 'int'.</span></span>
