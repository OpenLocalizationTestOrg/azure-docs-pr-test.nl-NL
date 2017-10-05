---
title: Service Fabric en implementatie Containers in Linux | Microsoft Docs
description: Service Fabric en het gebruik van Linux-containers microservice toepassingen implementeren. In dit artikel beschrijft de mogelijkheden met Service Fabric voor containers en hoe u een installatiekopie van de container Linux implementeert in een cluster
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4ba99103-6064-429d-ba17-82861b6ddb11
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 6/29/2017
ms.author: msfussell
ms.openlocfilehash: 9dcec753e5f999a1bac07276373c0c25f89ec58d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-linux-container-to-service-fabric"></a>Implementeren van een Linux-container voor Service Fabric
> [!div class="op_single_selector"]
> * [Windows-Container implementeren](service-fabric-deploy-container.md)
> * [Linux-Container implementeren](service-fabric-deploy-container-linux.md)
>
>

Dit artikel begeleidt u bij het ontwikkelen van beperkte services in Docker-containers op Linux.

Service Fabric heeft verschillende mogelijkheden voor de container die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices die beperkte zijn. Deze services worden beperkte services genoemd.

De mogelijkheden omvatten;

* Implementatie van de container en activeren
* Resource governance
* Verificatie van de opslagplaats
* Poort van de container voor poorttoewijzing host
* Container voor container detectie en communicatie
* Mogelijkheid om te configureren en de omgevingsvariabelen instellen

## <a name="packaging-a-docker-container-with-yeoman"></a>Een docker-container verpakking met yeoman
Als een container op Linux verpakking, kunt u ofwel een sjabloon yeoman gebruiken of [handmatig maken van het toepassingspakket](#manually).

Een Service Fabric-toepassing kan een of meer containers, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing bevatten. De Service Fabric-SDK voor Linux bevat een [Yeoman](http://yeoman.io/)-generator waarmee u gemakkelijk uw eerste toepassing kunt maken en een containerinstallatiekopie kunt toevoegen. We gebruiken Yeoman om een toepassing te maken met een enkele Docker-container genaamd *SimpleContainerApp*. U kunt toevoegen om dat meer services die zich later door te bewerken van de gegenereerde manifest bestanden.

## <a name="install-docker-on-your-development-box"></a>Docker installeren op de box ontwikkeling

Voer de volgende opdrachten voor het installeren van docker op de box Linux-ontwikkeling (als u de installatiekopie van het vagrant in OSX gebruikt, docker is al geïnstalleerd):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a>De toepassing maken
1. Typ in een terminal `yo azuresfcontainer`.
2. Naam van uw toepassing - bijvoorbeeld mycontainerap
3. Geef de URL voor de container-installatiekopie uit een DockerHub-opslagplaats. De parameter van de installatiekopie heeft de vorm [opslagplaats] / [naam afbeelding]
4. Als de installatiekopie geen een werkbelasting-toegangspunt gedefinieerd, heeft moet u opdrachten invoer expliciet opgeven met een door komma's gescheiden reeks opdrachten in de container, zodat de container uitgevoerd na het opstarten wordt behouden.

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="deploy-the-application"></a>De toepassing implementeren

### <a name="using-xplat-cli"></a>Met XPlat CLI
Als de toepassing is gemaakt, kunt u deze kunt implementeren in het lokale cluster met behulp van de Azure CLI.

1. Maak verbinding met het lokale cluster van Service Fabric.

    ```bash
    azure servicefabric cluster connect
    ```

2. Gebruik het installatiescript dat is opgegeven in de sjabloon om het toepassingspakket te kopiëren naar de installatiekopieopslag van het cluster, het toepassingstype te registreren en een exemplaar van de toepassing te maken.

    ```bash
    ./install.sh
    ```

3. Open een browser en navigeer naar de Service Fabric Explorer op http://localhost:19080/Explorer (vervang localhost door het privé IP-adres van de virtuele machine als u Vagrant in Mac OS X gebruikt).
4. Vouw het knooppunt Toepassingen uit. U ziet dat er nu een vermelding is voor uw toepassingstype en nog een voor het eerste exemplaar van dat type.
5. Het uninstall-script dat is opgegeven in de sjabloon gebruiken om te verwijderen van exemplaar van de toepassing en registratie van het toepassingstype.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Met Azure CLI 2.0

Zie het document naslaginformatie over het beheren van een [levenscyclus van de toepassing met de Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Voor een voorbeeldtoepassing [afhandeling van de code van de container Service Fabric-voorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-to-an-existing-application"></a>Meer services toevoegen aan een bestaande toepassing

Een andere containerservice toevoegen aan een toepassing die al is gemaakt met behulp van `yo`, voer de volgende stappen uit:

1. Stel de directory in op de hoofdmap van de bestaande toepassing.  Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.
2. Voer `yo azuresfcontainer:AddService` uit.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Handmatig van het pakket en een installatiekopie van een container implementeren
Het proces van het verpakken van handmatig een beperkte service is gebaseerd op de volgende stappen uit:

1. Publiceer de containers naar uw opslagplaats.
2. De mapstructuur pakket maken.
3. Bewerk het manifestbestand van de service.
4. Bewerk het manifestbestand van de toepassing.

## <a name="deploy-and-activate-a-container-image"></a>Implementeren en activeren van een installatiekopie van een container
In de Service Fabric [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst. Als u wilt implementeren en activeren van een container, plaatst u de naam van de container-installatiekopie in een `ContainerHost` element in het servicemanifest.

Voeg in het servicemanifest een `ContainerHost` voor het toegangspunt. Stel de `ImageName` moet de naam van de container-opslagplaats en de installatiekopie. Het volgende gedeeltelijke manifest toont een voorbeeld van het implementeren van de container aangeroepen `myimage:v1` vanuit een opslagplaats aangeroepen `myrepo`:

```xml
    <CodePackage Name="Code" Version="1.0">
        <EntryPoint>
          <ContainerHost>
            <ImageName>myrepo/myimage:v1</ImageName>
            <Commands></Commands>
          </ContainerHost>
        </EntryPoint>
    </CodePackage>
```

U kunt de opdrachten invoer opgeven door te geven de optionele `Commands` element met een door komma's gescheiden reeks opdrachten uitvoeren in de container.

> [!NOTE]
> Als de installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u expliciet opgeven van de opdrachten binnen invoer `Commands` element met een door komma's gescheiden reeks opdrachten uitvoeren in de container, zodat de container uitgevoerd na het opstarten wordt behouden.

## <a name="understand-resource-governance"></a>Resource governance begrijpen
Resource governance is een functie van de container die beperkt de resources die de container op de host gebruiken kunt. De `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest wordt gebruikt om te declareren limieten voor een service code-pakket. Limieten kunnen worden ingesteld voor de volgende bronnen:

* Geheugen
* MemorySwap
* CpuShares (CPU relatieve gewicht)
* MemoryReservationInMB  
* BlkioWeight (BlockIO relatieve gewicht).

> [!NOTE]
> In een toekomstige release, ondersteuning voor het opgeven van specifieke blok i/o-limieten zoals IOP's, lezen/schrijven BPS en anderen worden opgenomen.
>
>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ResourceGovernancePolicy CodePackageRef="FrontendService.Code" CpuShares="500"
            MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
        </Policies>
    </ServiceManifestImport>
```

## <a name="authenticate-a-repository"></a>Een opslagplaats verifiëren
Voor het downloaden van een container, kunt u wellicht aanmelden referenties aan de container-opslagplaats op te geven. De aanmeldingsreferenties, opgegeven in het toepassingsmanifest worden gebruikt om op te geven van de aanmeldingsgegevens of SSH-sleutel voor het downloaden van de container-installatiekopie uit de opslagplaats voor installatiekopieën. Het volgende voorbeeld ziet u een account met de naam *testgebruiker* samen met het wachtwoord in ongecodeerde tekst (*niet* aanbevolen):

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="12345" PasswordEncrypted="false"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Het is raadzaam dat u het wachtwoord versleutelen met behulp van een certificaat dat geïmplementeerd op de machine.

Het volgende voorbeeld ziet u een account met de naam *testgebruiker*, waar het wachtwoord is versleuteld met behulp van een certificaat genaamd *MyCert*. U kunt de `Invoke-ServiceFabricEncryptText` PowerShell-opdracht voor het maken van de geheime gecodeerde tekst voor het wachtwoord. Zie voor meer informatie het artikel [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md).

De persoonlijke sleutel van het certificaat dat wordt gebruikt voor het ontsleutelen van het wachtwoord moet worden geïmplementeerd op de lokale computer in een out-of-band-methode. (In Azure is deze methode Azure Resource Manager.) Wanneer het Service Fabric pakket met de service op de machine implementeert, kan deze het geheim decoderen. Met behulp van het geheim samen met de accountnaam vervolgens verificatie met de container-opslagplaats.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <RepositoryCredentials AccountName="TestUser" Password="[Put encrypted password here using MyCert certificate ]" PasswordEncrypted="true"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping"></a>Poorttoewijzing container poort-naar-host configureren
U kunt een hostpoort gebruikt voor communicatie met de container door te geven een `PortBinding` in het toepassingsmanifest. De poortbinding wijst de poort waarnaar de service binnen de container voor een poort op de host luistert.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

## <a name="configure-container-to-container-discovery-and-communication"></a>Container voor container detectie en communicatie configureren
Met behulp van de `PortBinding` beleid, kunt u een poort van de container voor toewijzen een `Endpoint` in het servicemanifest. Het eindpunt `Endpoint1` een vaste poort (bijvoorbeeld poort 80) kunt opgeven. Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van het cluster toepassingspoortbereik voor u is gekozen.

Als u een eindpunt opgeven, gebruikt de `Endpoint` -tag in het servicemanifest van een gast-container, Service Fabric automatisch dit eindpunt kunt publiceren naar de Naming service. Deze container met de REST-query's voor het oplossen van kunnen dus detecteren door andere services die worden uitgevoerd in het cluster.

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <Policies>
            <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
            </ContainerHostPolicies>
        </Policies>
    </ServiceManifestImport>
```

Registreert met de service Naming, hoeft u container-container-communicatie in de code in de container met behulp van de [omgekeerde proxy](service-fabric-reverseproxy.md). Communicatie wordt uitgevoerd door de http-luisterpoort omgekeerde proxy en de naam van de services die u communiceren wilt met als omgevingsvariabelen. Zie de volgende sectie voor meer informatie.

## <a name="configure-and-set-environment-variables"></a>Omgevingsvariabelen configureren en instellen
Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in het servicemanifest van de, zowel voor services die worden geïmplementeerd in containers of voor services die worden geïmplementeerd als gast-processen uitvoerbare bestanden. Deze variabele waarden voor omgevingsvariabelen worden genegeerd in het bijzonder in het toepassingsmanifest of opgegeven tijdens de implementatie als toepassingsparameters.

Het volgende XML-fragment voor het servicemanifest toont een voorbeeld van het opgeven van omgevingsvariabelen voor een codepakket:

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>a guest executable service in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
    </ServiceManifest>
```

Deze omgevingsvariabelen kunnen worden genegeerd op het niveau van manifest:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

In het vorige voorbeeld wordt een expliciete waarde opgegeven voor de `HttpGateway` omgevingsvariabele (19000), terwijl op de waarde voor `BackendServiceName` parameter via de `[BackendSvc]` parameter van de toepassing. Deze instellingen kunt u de waarde voor `BackendServiceName`waarde wanneer u de toepassing implementeren en geen vaste waarde in het manifest.

## <a name="complete-examples-for-application-and-service-manifest"></a>Voorbeelden voor de toepassing en servicemanifest voltooien

Hier volgt een voorbeeld-toepassingsmanifest:

```xml
    <ApplicationManifest ApplicationTypeName="SimpleContainerApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description>A simple service container application</Description>
        <Parameters>
            <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
            <Parameter Name="BackEndSvcName" DefaultValue="bkend"></Parameter>
        </Parameters>
        <ServiceManifestImport>
            <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
            <EnvironmentOverrides CodePackageRef="FrontendService.Code">
                <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvcName]"/>
                <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
            </EnvironmentOverrides>
            <Policies>
                <ResourceGovernancePolicy CodePackageRef="Code" CpuShares="500" MemoryInMB="1024" MemorySwapInMB="4084" MemoryReservationInMB="1024" />
                <ContainerHostPolicies CodePackageRef="FrontendService.Code">
                    <RepositoryCredentials AccountName="username" Password="****" PasswordEncrypted="true"/>
                    <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
                </ContainerHostPolicies>
            </Policies>
        </ServiceManifestImport>
    </ApplicationManifest>
```

Hier volgt een voorbeeld van de servicemanifest (opgegeven in het voorgaande toepassingsmanifest):

```xml
    <ServiceManifest Name="FrontendServicePackage" Version="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
        <Description> A service that implements a stateless front end in a container</Description>
        <ServiceTypes>
            <StatelessServiceType ServiceTypeName="StatelessFrontendService"  UseImplicitHost="true"/>
        </ServiceTypes>
        <CodePackage Name="FrontendService.Code" Version="1.0">
            <EntryPoint>
            <ContainerHost>
                <ImageName>myrepo/myimage:v1</ImageName>
                <Commands></Commands>
            </ContainerHost>
            </EntryPoint>
            <EnvironmentVariables>
                <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
                <EnvironmentVariable Name="BackendServiceName" Value=""/>
            </EnvironmentVariables>
        </CodePackage>
        <ConfigPackage Name="FrontendService.Config" Version="1.0" />
        <DataPackage Name="FrontendService.Data" Version="1.0" />
        <Resources>
            <Endpoints>
                <Endpoint Name="Endpoint1" UriScheme="http" Port="80" Protocol="http"/>
            </Endpoints>
        </Resources>
    </ServiceManifest>
```

## <a name="next-steps"></a>Volgende stappen
Nu dat u een beperkte service hebt geïmplementeerd, informatie over het beheren van de levenscyclus door te lezen [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md).

* [Overzicht van Service Fabric en containers](service-fabric-containers-overview.md)
* [Interactie aangaan met Service Fabric-clusters met de Azure-CLI](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Verwante artikelen:

* [Aan de slag met Service Fabric en Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Aan de slag met Service Fabric XPlat CLI](service-fabric-azure-cli.md)
