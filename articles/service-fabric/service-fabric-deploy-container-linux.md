---
title: aaaService Fabric en Containers implementeren in Linux | Microsoft Docs
description: Service Fabric en Hallo gebruik van Linux containers toodeploy microservice-toepassingen. In dit artikel beschrijft Hallo mogelijkheden waarmee u het Service Fabric-containers en hoe toodeploy een Linux-container installatiekopie in een cluster
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
ms.openlocfilehash: e28f99a145b0594d871b0ec0566233a7ad235ce8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-linux-container-tooservice-fabric"></a>Implementeren van een Linux-container tooService Fabric
> [!div class="op_single_selector"]
> * [Windows-Container implementeren](service-fabric-deploy-container.md)
> * [Linux-Container implementeren](service-fabric-deploy-container-linux.md)
>
>

Dit artikel begeleidt u bij het ontwikkelen van beperkte services in Docker-containers op Linux.

Service Fabric heeft verschillende mogelijkheden voor de container die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices die beperkte zijn. Deze services worden beperkte services genoemd.

Hallo-mogelijkheden zijn onder andere;

* Implementatie van de container en activeren
* Resource governance
* Verificatie van de opslagplaats
* Container toohost poort poorttoewijzing
* Container voor container detectie en communicatie
* Mogelijkheid tooconfigure en omgevingsvariabelen worden ingesteld

## <a name="packaging-a-docker-container-with-yeoman"></a>Een docker-container verpakking met yeoman
Als een container op Linux verpakking, kunt u beide toouse een sjabloon yeoman of [handmatig maken van het toepassingspakket Hallo](#manually).

Een Service Fabric-toepassing kan een of meer containers, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing hello bevatten. Hallo Service Fabric SDK voor Linux bevat een [Yeoman](http://yeoman.io/) generator waardoor u eenvoudig toocreate uw toepassing en een installatiekopie van de container toevoegen. We gebruiken Yeoman toocreate aangeroepen voor een toepassing met een enkele Docker-container *SimpleContainerApp*. U kunt later meer services toevoegen door Hallo gegenereerd manifest-bestanden te bewerken.

## <a name="install-docker-on-your-development-box"></a>Docker installeren op de box ontwikkeling

Voer Hallo deze opdrachten tooinstall docker op de box Linux-ontwikkeling (als u Hallo vagrant installatiekopie in OSX gebruikt, docker is al geïnstalleerd):

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a>Hallo-toepassing maken
1. Typ in een terminal `yo azuresfcontainer`.
2. Naam van uw toepassing - bijvoorbeeld mycontainerap
3. Hallo-URL opgeven voor Hallo container afbeelding uit een DockerHub-opslagplaats. Hallo installatiekopie parameter vergt Hallo formulier [opslagplaats] / [naam afbeelding]
4. Als Hallo installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u tooexplicitly invoer-opdrachten opgeven met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container die behoudt Hallo container uitgevoerd na het opstarten.

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="deploy-hello-application"></a>Hallo-toepassing implementeren

### <a name="using-xplat-cli"></a>Met XPlat CLI
Als de toepassing hello is gebouwd, kunt u deze toohello lokale cluster met behulp van Azure CLI Hallo implementeren.

1. Verbinding maken met toohello lokale Service Fabric-cluster.

    ```bash
    azure servicefabric cluster connect
    ```

2. Gebruik Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype Hallo en op een exemplaar van de toepassing hello maken.

    ```bash
    ./install.sh
    ```

3. Open een browser en ga tooService Fabric Explorer op http://localhost: 19080/Explorer (localhost vervangen met particuliere IP-Hallo Hallo VM als Vagrant op Mac OS X).
4. Hallo toepassingen knooppunt uitvouwen en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type.
5. Gebruik Hallo uninstall-script in Hallo toodelete Hallo toepassing sjabloonexemplaar en registratie van toepassingstype Hallo.

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a>Met Azure CLI 2.0

Zie Hallo verwijzing document over het beheren van een [gebruik van de levenscyclus van de toepassing hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).

Voor een voorbeeldtoepassing [afhandeling Hallo Service Fabric-containercode voorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="adding-more-services-tooan-existing-application"></a>Meer services tooan bestaande toepassing toe te voegen

tooadd een andere container servicetoepassing tooan al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren:

1. Toohello hoofdmap van de bestaande toepassing hello wijzigen.  Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.
2. Voer `yo azuresfcontainer:AddService` uit.

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a>Handmatig van het pakket en een installatiekopie van een container implementeren
Hallo-proces handmatig een beperkte service verpakt is gebaseerd op Hallo stappen te volgen:

1. Hallo containers tooyour opslagplaats publiceren.
2. Mapstructuur Hallo-pakket maken.
3. Servicemanifest Hallo bewerken.
4. Manifestbestand van de toepassing hello bewerken.

## <a name="deploy-and-activate-a-container-image"></a>Implementeren en activeren van een installatiekopie van een container
In Service Fabric Hallo [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst. toodeploy en activeren van een container, put Hallo-naam van Hallo container installatiekopie in een `ContainerHost` -element in Hallo servicemanifest.

Hallo servicemanifest, Voeg een `ContainerHost` voor Hallo toegangspunt. Vervolgens set Hallo `ImageName` toobe Hallo-naam van Hallo container opslagplaats en de installatiekopie. Hallo volgende gedeeltelijke manifest toont een voorbeeld van hoe toodeploy Hallo container aangeroepen `myimage:v1` vanuit een opslagplaats aangeroepen `myrepo`:

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

Kunt u opdrachten invoer bieden door te geven Hallo optionele `Commands` element met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container.

> [!NOTE]
> Als Hallo installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u tooexplicitly invoer-opdrachten binnen opgeven `Commands` element met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container die uitgevoerd behoudt na het Hallo-container opstarten.

## <a name="understand-resource-governance"></a>Resource governance begrijpen
Resource governance is een functie van Hallo-container die beperkt Hallo-resources die container Hallo kunt gebruiken op Hallo host. Hallo `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest Hallo gebruikte toodeclare limieten voor een service-codepakket is. Limieten kunnen worden ingesteld voor Hallo resources te volgen:

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
toodownload een container, moet u wellicht tooprovide aanmeldingsreferenties toohello container opslagplaats. Hallo aanmeldingsreferenties, opgegeven in het toepassingsmanifest hello, zijn gebruikte toospecify Hallo aanmelden informatie of SSH-sleutel voor het downloaden van Hallo container installatiekopie van het Hallo-opslagplaats voor installatiekopieën. Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker* samen met het wachtwoord in ongecodeerde tekst hello (*niet* aanbevolen):

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

Het is raadzaam dat u Hallo wachtwoord versleutelen met behulp van een certificaat dat is geïmplementeerd toohello machine.

Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker*, waarbij Hallo wachtwoord is versleuteld met behulp van een certificaat genaamd *MyCert*. U kunt Hallo `Invoke-ServiceFabricEncryptText` PowerShell-opdracht toocreate Hallo geheime gecodeerde tekst hello wachtwoord. Zie voor meer informatie artikel Hallo [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md).

Hallo persoonlijke sleutel van het Hallo-certificaat dat is gebruikt toodecrypt Hallo wachtwoord moet geïmplementeerde toohello lokale computer in een out-of-band-methode. (In Azure is deze methode Azure Resource Manager.) Wanneer het Service Fabric Hallo service pakket toohello machine implementeert, kan het Hallo-geheim decoderen. Met behulp van Hallo geheim samen met de accountnaam Hallo vervolgens verificatie met Hallo container opslagplaats.

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
U kunt een host gebruikt poort toocommunicate configureren met Hallo-container door te geven een `PortBinding` Hallo-toepassingsmanifest. Hallo poort binding maps Hallo poort toowhich Hallo service luistert binnen Hallo container tooa poort op Hallo host.

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
Met behulp van Hallo `PortBinding` beleid, kunt u een container poort tooan toewijzen `Endpoint` in Hallo servicemanifest. Hallo eindpunt `Endpoint1` een vaste poort (bijvoorbeeld poort 80) kunt opgeven. Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van toepassingspoortbereik Hallo-cluster wordt gekozen voor u.

Als u een eindpunt opgeeft, met behulp van Hallo `Endpoint` tag op in Hallo servicemanifest van een gast-container, Service Fabric kan automatisch publiceren van dit eindpunt toohello Naming service. Andere services die worden uitgevoerd in de cluster Hallo kunnen dus deze container Hallo REST-query's gebruiken voor het oplossen van detecteren.

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

Registreert Hello Naming service, hoeft u container-container-communicatie in Hallo code in de container met behulp van Hallo [omgekeerde proxy](service-fabric-reverseproxy.md). Communicatie wordt uitgevoerd door Hallo omgekeerde proxy http-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt. Zie de volgende sectie Hallo voor meer informatie.

## <a name="configure-and-set-environment-variables"></a>Omgevingsvariabelen configureren en instellen
Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in servicemanifest hello, zowel voor services die worden geïmplementeerd in containers of voor services die worden geïmplementeerd als gast-processen uitvoerbare bestanden. Deze variabele waarden voor omgevingsvariabelen worden genegeerd in het bijzonder in het toepassingsmanifest Hallo of opgegeven tijdens de implementatie als toepassingsparameters.

Hallo volgende service manifest XML-fragment toont een voorbeeld van hoe de omgevingsvariabelen toospecify voor een codepakket:

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

Deze omgevingsvariabelen kunnen worden genegeerd op toepassingsniveau voor Hallo-manifest:

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

In het vorige voorbeeld hello, we een expliciete waarde opgegeven voor Hallo `HttpGateway` omgevingsvariabele (19000), terwijl op Hallo-waarde voor `BackendServiceName` parameter via Hallo `[BackendSvc]` parameter van de toepassing. Deze instellingen kunt u toospecify Hallo waarde voor `BackendServiceName`wanneer u Hallo-toepassing implementeren en geen vaste waarde in het manifest Hallo waarde.

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

Hier volgt een voorbeeld van de servicemanifest (opgegeven in Hallo voorafgaand aan het toepassingsmanifest):

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
Nu u een beperkte service hebt geïmplementeerd, kunt u nagaan hoe toomanage levenscyclus door te lezen [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md).

* [Overzicht van Service Fabric en containers](service-fabric-containers-overview.md)
* [Interactie met Service Fabric-clusters met hello Azure CLI](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a>Verwante artikelen:

* [Aan de slag met Service Fabric en Azure CLI 2.0](service-fabric-azure-cli-2-0.md)
* [Aan de slag met Service Fabric XPlat CLI](service-fabric-azure-cli.md)
