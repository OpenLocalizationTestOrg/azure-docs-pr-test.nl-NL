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
# <a name="specify-resources-in-a-service-manifest"></a>Resources specificeren in een servicemanifest
## <a name="overview"></a>Overzicht
Hallo servicemanifest kan resources die worden gebruikt door Hallo service toobe gedeclareerd of gewijzigd zonder Hallo gecompileerde code te wijzigen. Azure Service Fabric ondersteunt de configuratie van endpoint-resources voor Hallo-service. Hallo toegang toohello resources die zijn opgegeven in het Hallo-servicemanifest kunnen worden beheerd via Hallo beveiligingsgroep in het toepassingsmanifest Hallo. Hallo-declaratie van resources kunt deze resources toobe gewijzigd tijdens de implementatie, wat betekent dat Hallo service hoeft niet toointroduce een nieuw configuratie-mechanisme. Hallo schemadefinitie voor Hallo ServiceManifest.xml bestand is geïnstalleerd met Hallo Service Fabric SDK en hulpprogramma's te*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

## <a name="endpoints"></a>Eindpunten
Als endpoint-bron is gedefinieerd in het manifest voor Hallo-service, wijst Service Fabric de poorten van Hallo gereserveerd toepassingspoortbereik wanneer een poort expliciet is niet opgegeven. Zoek bijvoorbeeld naar op Hallo eindpunt *ServiceEndpoint1* opgegeven in het manifest Hallo-codefragment die na dit lid. Services kunnen bovendien ook aanvragen voor een specifieke poort in een resource. Service-replica's uitgevoerd op verschillende knooppunten kunnen worden toegewezen worden andere poortnummers, terwijl de replica's van een service die wordt uitgevoerd op hetzelfde knooppunt share Hallo poort Hallo. Hallo service replica's kunnen deze poorten vervolgens naar wens gebruiken voor replicatie en luistert naar aanvragen van clients.

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="ServiceEndpoint1" Protocol="http"/>
    <Endpoint Name="ServiceEndpoint2" Protocol="http" Port="80"/>
    <Endpoint Name="ServiceEndpoint3" Protocol="https"/>
  </Endpoints>
</Resources>
```

Raadpleeg te[configureren van stateful Reliable Services](service-fabric-reliable-services-configuration.md) tooread meer informatie over die verwijzen naar eindpunten vanuit Hallo configuratie-instellingen pakketbestand (settings.xml).

## <a name="example-specifying-an-http-endpoint-for-your-service"></a>Voorbeeld: een HTTP-eindpunt voor uw service opgeven
Hallo volgende servicemanifest definieert één resource voor TCP-eindpunt en bronnen van twee HTTP-eindpunt op Hallo &lt;Resources&gt; element.

HTTP-eindpunten worden automatisch dat ACL zou door Service Fabric.

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

## <a name="example-specifying-an-https-endpoint-for-your-service"></a>Voorbeeld: een HTTPS-eindpunt voor uw service opgeven
Hallo HTTPS-protocol biedt verificatie van de server en wordt ook gebruikt voor het versleutelen van de client-servercommunicatie. tooenable HTTPS op uw Service Fabric-service, Hallo protocol opgeven in Hallo *Resources-eindpunten > Endpoint ->* sectie van Hallo servicemanifest, zoals eerder besproken voor het eindpunt Hallo *ServiceEndpoint3* .

> [!NOTE]
> Een service-protocol kan niet worden gewijzigd tijdens de upgrade van de toepassing. Als deze is gewijzigd tijdens de upgrade, is een belangrijke wijziging.
> 
> 

Hier volgt een voorbeeld ApplicationManifest moet u tooset voor HTTPS. Hallo vingerafdruk voor het certificaat moet worden opgegeven. Hallo EndpointRef is een verwijzing tooEndpointResource in ServiceManifest, waarvoor u de HTTPS-protocol Hallo ingesteld. U kunt meer dan één EndpointCertificate toevoegen.  

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

## <a name="overriding-endpoints-in-servicemanifestxml"></a>Eindpunten in ServiceManifest.xml overschrijven

Voeg een sectie ResourceOverrides die als een lid op hetzelfde niveau tooConfigOverrides sectie Hallo ApplicationManifest. In deze sectie kunt u Hallo onderdrukking voor Hallo eindpunten in de sectie van Hallo resources die zijn opgegeven in het Hallo-servicemanifest.

Hallo in volgorde toooverride eindpunt in ServiceManifest ApplicationParameters wijzigen met ApplicationManifest als volgt:

Voeg een nieuwe sectie 'ResourceOverrides' in hello ServiceManifestImport sectie

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

In de Hallo die parameters hieronder toevoegen:

```xml
  <Parameters>
    <Parameter Name="Port" DefaultValue="" />
    <Parameter Name="Protocol" DefaultValue="" />
    <Parameter Name="Type" DefaultValue="" />
    <Parameter Name="Port1" DefaultValue="" />
    <Parameter Name="Protocol1" DefaultValue="" />
  </Parameters>
```

Tijdens de implementatie van de toepassing nu Hallo kunt u deze waarden als doorgeven ApplicationParameters bijvoorbeeld:

```powershell
PS C:\> New-ServiceFabricApplication -ApplicationName fabric:/myapp -ApplicationTypeName "AppType" -ApplicationTypeVersion "1.0.0" -ApplicationParameter @{Port='1001'; Protocol='https'; Type='Input'; Port1='2001'; Protocol='http'}
```

Opmerking: Als Hallo waarden opgeven voor Hallo ApplicationParameters leeg is we gaat u terug toohello standaard waarde die is opgegeven in Hallo ServiceManifest voor Hallo EndPointName overeenkomt.

Bijvoorbeeld:

Indien in Hallo ServiceManifest die u hebt opgegeven

```xml
  <Resources>
    <Endpoints>
      <Endpoint Name="ServiceEndpoint1" Protocol="tcp"/>
    </Endpoints>
  </Resources>
```

Hallo Port1 en Protocol1 waarde voor de parameters voor de toepassing is null of leeg. Hallo-poort wordt nog steeds bepaald door ServiceFabric. En Hallo Protocol tcp wordt.

Stel dat u een onjuiste waarde opgeven. Net als voor de poort u hebt opgegeven een tekenreekswaarde "Foo" in plaats van een int.  Nieuwe ServiceFabricApplication opdracht mislukt met een fout opgetreden: Hallo overrideparameter met de 'ServiceEndpoint1' naamkenmerk 'Port1' in sectie 'ResourceOverrides' is ongeldig. Hallo waarde die is opgegeven is 'Foo' en 'integer' vereist is.
