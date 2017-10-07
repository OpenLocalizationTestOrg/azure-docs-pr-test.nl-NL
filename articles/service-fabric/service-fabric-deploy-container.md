---
title: aaaService Fabric en containers implementeren | Microsoft Docs
description: Service Fabric en Hallo gebruik van containers toodeploy microservice-toepassingen. In dit artikel beschrijft Hallo mogelijkheden waarmee u het Service Fabric-containers en hoe toodeploy een Windows-container installatiekopie in een cluster.
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 799cc9ad-32fd-486e-a6b6-efff6b13622d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 5/16/2017
ms.author: msfussell
ms.openlocfilehash: 8b6540579641474f21b8712b56049c7d177bec26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-windows-container-tooservice-fabric"></a>Een Windows-container tooService Fabric implementeren
> [!div class="op_single_selector"]
> * [Windows-Container implementeren](service-fabric-deploy-container.md)
> * [Docker-Container implementeren](service-fabric-deploy-container-linux.md)
> 
> 

In dit artikel begeleidt u bij Hallo proces van het bouwen van beperkte services in Windows-containers.

Service Fabric heeft verschillende mogelijkheden die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices in containers wordt uitgevoerd. 

Hallo-mogelijkheden zijn:

* Implementatie van de container en activeren
* Resource governance
* Verificatie van de opslagplaats
* Poorttoewijzing container poort-naar-host
* Container voor container detectie en communicatie
* Mogelijkheid tooconfigure en omgevingsvariabelen worden ingesteld

Bekijk hoe elk van de mogelijkheden werkt wanneer u een beperkte service toobe opgenomen in uw toepassing inpakt.

## <a name="package-a-windows-container"></a>Pakket met een Windows-container
Wanneer u een container van het pakket, kunt u kiezen toouse ofwel een Visual Studio-projectsjabloon of [handmatig maken van het toepassingspakket Hallo](#manually).  Wanneer u Visual Studio, Hallo toepassing pakketstructuur en manifest-bestanden voor u gemaakt door Hallo nieuw Project-sjabloon.

> [!TIP]
> Hallo gemakkelijkste manier toopackage een installatiekopie van een bestaande container in een service is toouse Visual Studio.

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a>Visual Studio toopackage een installatiekopie van een bestaande container gebruiken
Visual Studio biedt een Service Fabric service sjabloon toohelp implementeren van een container tooa Service Fabric-cluster.

1. Kies **bestand** > **nieuw Project**, en maak een Service Fabric-toepassing.
2. Kies **Gast Container** als Hallo-servicesjabloon.
3. Kies **Installatiekopienaam** en mogelijk Hallo pad toohello installatiekopie in de container-opslagplaats. Bijvoorbeeld: `myrepo/myimage:v1` in https://hub.docker.com
4. Geef de service een naam en klik op **OK**.
5. Als uw beperkte service een eindpunt voor communicatie moet, kunt u nu Hallo-protocol en poort type toohello ServiceManifest.xml bestand toevoegen. Bijvoorbeeld: 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    Dankzij de Hallo `UriScheme`, Service Fabric Hallo container eindpunt wordt automatisch wordt geregistreerd bij Hallo Naming service voor detectie. Hallo-poort kan worden opgelost (zoals weergegeven in het voorgaande voorbeeld Hallo) of dynamisch toegewezen. Als u een poort niet opgeeft, wordt het dynamisch toegewezen van Hallo toepassingspoortbereik (zoals met een service gebeuren zou).
    U moet ook tooconfigure Hallo container toohost-poorttoewijzing door te geven een `PortBinding` beleid in het toepassingsmanifest Hallo. Zie voor meer informatie [container toohost poorttoewijzing configureren](#Portsection).
6. Als uw container moet resource governance en vervolgens voegt u een `ResourceGovernancePolicy`.
8. Als uw container tooauthenticate met een persoonlijke opslagplaats moet, voegt u `RepositoryCredentials`.
7. Als u op een Windows Server 2016-machine met de ondersteuning van de container is ingeschakeld uitvoert, kunt u Hallo pakket gebruiken en publiceren actie toodeploy tooyour lokale cluster. 
8. Wanneer u klaar bent, kunt u Hallo toepassing tooa extern clusterbeheer publiceren of inchecken Hallo oplossing toosource besturingselement. 

Voor een voorbeeld: Bekijk Hallo [Service Fabric-container codevoorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="creating-a-windows-server-2016-cluster"></a>Maken van een cluster met Windows Server 2016
toodeploy uw beperkte toepassing, moet u een cluster met Windows Server 2016 met ondersteuning voor de container ingeschakeld toocreate. Uw cluster lokaal worden uitgevoerd of geïmplementeerd via Azure Resource Manager in Azure. 

een cluster met Azure Resource Manager toodeploy kiezen Hallo **Windows Server 2016 met Containers** installatiekopie optie in Azure. Zie het artikel Hallo [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md). Zorg ervoor dat u hello Azure Resource Manager-instellingen te volgen:

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
U kunt ook Hallo [vijf knooppunt Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate een cluster. U kunt ook een community lezen [blogbericht](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) over het gebruik van Service Fabric- en Windows-containers.

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

Kunt u optionele opdrachten toorun bij het starten van de container onder Hallo Hallo `Commands` element. Voor meerdere opdrachten komma-beperken ze. 

## <a name="understand-resource-governance"></a>Resource governance begrijpen
Resource governance is een functie van Hallo-container die beperkt Hallo-resources die container Hallo kunt gebruiken op Hallo host. Hallo `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest Hallo gebruikte toodeclare limieten voor een service-codepakket is. Limieten kunnen worden ingesteld voor Hallo resources te volgen:

* Geheugen
* MemorySwap
* CpuShares (CPU relatieve gewicht)
* MemoryReservationInMB  
* BlkioWeight (BlockIO relatieve gewicht).

> [!NOTE]
> Ondersteuning voor het opgeven van specifieke blokkeren i/o-limieten, zoals IOP's, lezen/schrijven BPS en andere zijn gepland voor een toekomstige release.
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

## <a name ="Portsection"></a>Container toohost poorttoewijzing configureren
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
U kunt Hallo `PortBinding` element toomap een eindpunt van de container poort tooan in Hallo servicemanifest. Hallo in Hallo voorbeeld te volgen, eindpunt `Endpoint1` geeft een vaste poort, 8905. Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van toepassingspoortbereik Hallo-cluster wordt gekozen voor u.


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
Als u een eindpunt opgeeft, met behulp van Hallo `Endpoint` tag op in Hallo servicemanifest van een gast-container, Service Fabric kan automatisch publiceren van dit eindpunt toohello Naming service. Andere services die worden uitgevoerd in de cluster Hallo kunnen dus deze container Hallo REST-query's gebruiken voor het oplossen van detecteren.

Registreert Hello Naming service, kunt u container-container-communicatie uitvoeren binnen uw container via Hallo [omgekeerde proxy](service-fabric-reverseproxy.md). Communicatie wordt uitgevoerd door Hallo omgekeerde proxy http-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt. Zie de volgende sectie Hallo voor meer informatie. 

## <a name="configure-and-set-environment-variables"></a>Omgevingsvariabelen configureren en instellen
Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in Hallo servicemanifest. Deze functie is beschikbaar voor alle services, ongeacht of ze zijn geïmplementeerd als containers, processen of uitvoerbare gastbestanden. U kunt de omgevingsvariabele waarden in de toepassing hello manifest of geef ze tijdens de implementatie als toepassingsparameters overschrijven.

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

## <a name="configure-isolation-mode"></a>Isolatiemodus configureren

Windows ondersteunt twee isolatiemodi voor containers - proces en Hyper-V.  Met isolatiemodus voor Hallo Hallo alle Hallo containers die worden uitgevoerd op dezelfde host machine share Hallo kernel met Hallo host. Hallo kernels zijn met de isolatiemodus Hallo Hyper-V, tussen elke Hyper-V-container en Hallo containerhost geïsoleerd. Hallo isolatiemodus is opgegeven in Hallo `ContainerHostPolicies` -tag in het manifestbestand van de toepassing hello.  Hallo isolatie modi die kunnen worden opgegeven `process`, `hyperv`, en `default`. Hallo `default` isolatiemodus standaardwaarden te`process` op Windows-Server fungeert als host en de standaardinstellingen te`hyperv` op hosts met Windows 10.  Hallo volgende fragment toont hoe Hallo isolatiemodus is opgegeven in het manifestbestand van de toepassing hello.

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


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
* Voor een voorbeeld afhandeling [Service Fabric-container codevoorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
