---
title: een toepassing Azure Service Fabric-container aaaCreate | Microsoft Docs
description: Maak uw eerste Windows-containertoepassing in Azure Service Fabric.  Een Docker-installatiekopie aan een Python-toepassing bouwen, push Hallo installatiekopie tooa container register, bouwen en implementeren van een container Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: vturecek
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 07/18/2017
ms.author: ryanwi
ms.openlocfilehash: b79d3a41eb2da5f7791266588fe9ea7becb0e58f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-windows"></a>Uw eerste Service Fabric-containertoepassing maken in Windows
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Een bestaande toepassing in een Windows-container uitgevoerd op een Service Fabric-cluster nodig niet alle wijzigingen tooyour toepassingen. Dit artikel begeleidt u bij het maken van een Docker-afbeelding met een Python [Flask](http://flask.pocoo.org/) web-toepassing en deze tooa Service Fabric-cluster is geïmplementeerd.  U gaat uw containertoepassing ook delen via [Azure Container Registry](/azure/container-registry/).  In dit artikel wordt ervan uitgegaan dat u de basisbeginselen kent van Docker. U kunt meer informatie over Docker door Hallo lezen [Docker-overzicht](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Vereisten
Een ontwikkelcomputer waarop wordt uitgevoerd:
* Visual Studio 2015 of Visual Studio 2017.
* [Service Fabric SDK en hulpprogramma's](service-fabric-get-started.md).
*  Docker voor Windows.  [Download Docker CE voor Windows (stabiel)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description). Na het installeren en starten van Docker, met de rechtermuisknop op het pictogram in systeemvak voor Hallo en selecteer **tooWindows containers overschakelen**. Dit is vereiste toorun Docker-installatiekopieën op basis van Windows.

Een Windows-cluster met drie of meer knooppunten die worden uitgevoerd op Windows Server 2016 met containers - [Een cluster maken](service-fabric-cluster-creation-via-portal.md) of [Service Fabric gratis uitproberen](https://aka.ms/tryservicefabric).

Een register in Azure Container Registry - [Een containerregister maken](../container-registry/container-registry-get-started-portal.md) in uw Azure-abonnement.

## <a name="define-hello-docker-container"></a>Hallo Docker-container definiëren
Maken van een installatiekopie op basis van Hallo [Python installatiekopie](https://hub.docker.com/_/python/) zich bevinden op Docker-Hub.

Definieer uw Docker-container in een Dockerfile. Hallo Dockerfile bevat instructies voor het instellen van Hallo-omgeving in de container, Hallo-toepassing die u wilt dat toorun laden en poorten toewijzen. Hallo Dockerfile is Hallo invoer toohello `docker build` opdracht, waarbij Hallo installatiekopie wordt gemaakt.

Maken van een lege map en het Hallo-bestand maken *Dockerfile* (met zonder extensie). Hallo te volgende toevoegen*Dockerfile* en sla de wijzigingen:

```
# Use an official Python runtime as a base image
FROM python:2.7-windowsservercore

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available toohello world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when hello container launches
CMD ["python", "app.py"]
```

Lees Hallo [Dockerfile verwijzing](https://docs.docker.com/engine/reference/builder/) voor meer informatie.

## <a name="create-a-simple-web-application"></a>Een eenvoudige webtoepassing maken
Maak een Flask-toepassing die luistert op poort 80 en 'Hallo Wereld!' retourneert.  In dezelfde map Hallo, Hallo-bestand maken *requirements.txt*.  Voeg de volgende Hallo en sla de wijzigingen:
```
Flask
```

Maak ook Hallo *app.py* -bestand en voeg de volgende Hallo:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():

    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

<a id="Build-Containers"></a>
## <a name="build-hello-image"></a>Hallo installatiekopie maken
Voer Hallo `docker build` toocreate Hallo de afbeelding die wordt uitgevoerd van uw webtoepassing. Open een PowerShell-venster en ga toohello map waarin zich Hallo Dockerfile. Hallo volgende opdracht uitvoeren:

```
docker build -t helloworldapp .
```

Met deze opdracht builds Hallo nieuwe installatiekopie met Hallo-instructies in uw Dockerfile naming (-t tagging) Hallo installatiekopie 'helloworldapp'. Voor het bouwen van een installatiekopie van een Hallo basisinstallatiekopie omlaag ophaalt uit Docker-Hub en maakt een nieuwe installatiekopie waarmee uw toepassing boven op Hallo basisinstallatiekopie worden toegevoegd.  

Uitvoeren zodra Hallo build-opdracht is voltooid, Hallo `docker images` toosee informatie over de nieuwe installatiekopie Hallo opdracht:

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
Controleer of uw installatiekopie lokaal voordat u het register van Hallo-container.  

Hallo-toepassing uitvoeren:

```
docker run -d --name my-web-site helloworldapp
```

*naam* geeft een naam toohello container (in plaats van de container-ID Hallo) uitgevoerd.

Eenmaal Hallo container wordt gestart, het IP-adres zoeken, zodat u verbinding kunt maken met container uitgevoerd vanuit een browser tooyour:
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

Verbinding maken met container toohello.  Open een webbrowser toohello geretourneerde IP-adres, bijvoorbeeld 'http://172.31.194.61' aan te wijzen. U ziet Hallo kop "Hello World!" in de browser Hallo weergeven.

toostop uw container, uitvoeren:

```
docker stop my-web-site
```

Hallo-container uit uw ontwikkelcomputer verwijderen:

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a>Push Hallo installatiekopie toohello container register
Nadat u hebt gecontroleerd dat die Hallo-container wordt uitgevoerd op uw ontwikkelcomputer, push-Hallo installatiekopie tooyour register in Azure Container register.

Voer ``docker login`` toolog in tooyour container register met uw [register referenties](../container-registry/container-registry-authentication.md).

Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md). Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering. Of u kunt zich aanmelden met uw gebruikersnaam en wachtwoord van het register.

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hallo volgende opdracht maakt u een label of alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register. In dit voorbeeld plaatsen Hallo-installatiekopie in Hallo ```samples``` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Push Hallo installatiekopie tooyour container register:

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a>Hallo beperkte service in Visual Studio maken
Hallo Service Fabric SDK en hulpprogramma's bieden een toohelp service-sjabloon maken van een beperkte toepassing.

1. Start Visual Studio.  Selecteer **Bestand** > **Nieuw** > **Project**.
2. Selecteer **Service Fabric-toepassing**, geef deze de naam MyFirstContainer en klik op **OK**.
3. Selecteer **Gast Container** uit Hallo lijst met **servicesjablonen**.
4. In **Installatiekopienaam** 'myregistry.azurecr.io/samples/helloworldapp', Hallo installatiekopie gepusht van tooyour container opslagplaats invoeren.
5. Geef de service een naam en klik op **OK**.

## <a name="configure-communication"></a>Communicatie configureren
beperkte Hallo-service moet een eindpunt voor communicatie. Voeg een `Endpoint` element met het Hallo-protocol en poort type toohello ServiceManifest.xml bestand. Voor dit artikel luistert Hallo beperkte service op poort 8081.  In dit voorbeeld wordt een ingestelde poort 8081 gebruikt.  Als er geen poort is opgegeven, wordt een willekeurige poort van Hallo toepassingspoortbereik gekozen.  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

Als u een eindpunt, publiceert Service Fabric Hallo eindpunt toohello Naming service.  Deze container kunnen worden opgelost door andere services in Hallo cluster wordt uitgevoerd.  U kunt ook de container-container-communicatie met Hallo uitvoeren [omgekeerde proxy](service-fabric-reverseproxy.md).  Communicatie wordt uitgevoerd door Hallo omgekeerde proxy HTTP-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt.

## <a name="configure-and-set-environment-variables"></a>Omgevingsvariabelen configureren en instellen
Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in Hallo servicemanifest. Deze functie is beschikbaar voor alle services, ongeacht of ze zijn geïmplementeerd als containers, processen of uitvoerbare gastbestanden. U kunt de omgevingsvariabele waarden in de toepassing hello manifest of geef ze tijdens de implementatie als toepassingsparameters overschrijven.

Hallo volgende service manifest XML-fragment toont een voorbeeld van hoe de omgevingsvariabelen toospecify voor een codepakket:
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

Deze omgevingsvariabelen kunnen worden genegeerd in het toepassingsmanifest Hallo:

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a>Poort-naar-host-toewijzing voor containers en container-naar-container-detectie configureren
Configureer een toocommunicate host-poort die wordt gebruikt met Hallo-container. Hallo-poortbinding maps Hallo poort welke Hallo service binnen Hallo container tooa poort op Hallo host luistert. Voeg een `PortBinding` -element in `ContainerHostPolicies` element van Hallo ApplicationManifest.xml bestand.  Voor dit artikel `ContainerPort` 80 (Hallo container wordt poort 80, als de opgegeven in de Hallo Dockerfile) en `EndpointRef` is 'Guest1TypeEndpoint' (Hallo eindpunt dat eerder is gedefinieerd in Hallo servicemanifest).  Inkomende aanvragen toohello-service op poort 8081 zijn toegewezen tooport 80 op Hallo-container.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a>Verificatie containerregister configureren
Container register verificatie configureren door toe te voegen `RepositoryCredentials` te`ContainerHostPolicies` van Hallo ApplicationManifest.xml bestand. Hallo-account en wachtwoord voor Hallo myregistry.azurecr.io container register, waardoor Hallo service toodownload Hallo container de installatiekopie van het Hallo-opslagplaats toevoegen.

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

Het is raadzaam dat u Hallo opslagplaats wachtwoord versleutelen met behulp van een certificaat uitwisselen die tooall knooppunten van het Hallo-cluster is geïmplementeerd. Wanneer het Service Fabric Hallo service pakket toohello-cluster implementeert, is Hallo uitwisselen certificaat gebruikte toodecrypt Hallo gecodeerde tekst.  Hallo Invoke ServiceFabricEncryptText cmdlet is gebruikte toocreate Hallo gecodeerde tekst hello wachtwoord toohello ApplicationManifest.xml bestand wordt toegevoegd.

Hallo volgende script maakt een nieuw zelfondertekend certificaat en exporteert het tooa PFX-bestand.  Hallo-certificaat wordt geïmporteerd in een bestaande sleutelkluis en vervolgens geïmplementeerd toohello Service Fabric-cluster.

```powershell
# Variables.
$certpwd = ConvertTo-SecureString -String "Pa$$word321!" -Force -AsPlainText
$filepath = "C:\MyCertificates\dataenciphermentcert.pfx"
$subjectname = "dataencipherment"
$vaultname = "mykeyvault"
$certificateName = "dataenciphermentcert"
$groupname="myclustergroup"
$clustername = "mycluster"

$subscriptionId = "subscription ID"

Login-AzureRmAccount

Select-AzureRmSubscription -SubscriptionId $subscriptionId

# Create a self signed cert, export tooPFX file.
New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject $subjectname -Provider 'Microsoft Enhanced Cryptographic Provider v1.0' `
| Export-PfxCertificate -FilePath $filepath -Password $certpwd

# Import hello certificate tooan existing key vault.  hello key vault must be enabled for deployment.
$cer = Import-AzureKeyVaultCertificate -VaultName $vaultName -Name $certificateName -FilePath $filepath -Password $certpwd

Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $groupname -EnabledForDeployment

# Add hello certificate tooall hello VMs in hello cluster.
Add-AzureRmServiceFabricApplicationCertificate -ResourceGroupName $groupname -Name $clustername -SecretIdentifier $cer.SecretId
```
Hallo-wachtwoord met behulp van Hallo versleutelen [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

Vervang Hallo wachtwoord door Hallo gecodeerde tekst die wordt geretourneerd door Hallo [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet en stel `PasswordEncrypted` te 'true'.

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-isolation-mode"></a>Isolatiemodus configureren
Windows ondersteunt twee isolatiemodi voor containers: proces en Hyper-V. Met isolatiemodus voor Hallo Hallo alle Hallo containers die worden uitgevoerd op dezelfde host machine share Hallo kernel met Hallo host. Hallo kernels zijn met de isolatiemodus Hallo Hyper-V, tussen elke Hyper-V-container en Hallo containerhost geïsoleerd. Hallo isolatiemodus is opgegeven in Hallo `ContainerHostPolicies` -element in het manifestbestand van de toepassing hello. Hallo isolatie modi die kunnen worden opgegeven `process`, `hyperv`, en `default`. Hallo standaardisolatiemodus standaardwaarden te`process` op Windows-Server fungeert als host en de standaardinstellingen te`hyperv` op hosts met Windows 10. Hallo volgende fragment toont hoe Hallo isolatiemodus is opgegeven in het manifestbestand van de toepassing hello.

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a>Resourcebeheer configureren
[Resource governance](service-fabric-resource-governance.md) beperkt Hallo resources die container Hallo op Hallo host kunnen gebruiken. Hallo `ResourceGovernancePolicy` element, dat is opgegeven in het toepassingsmanifest hello, gebruikte toodeclare limieten voor een service-codepakket is. Limieten kunnen worden ingesteld voor Hallo volgende resources: geheugen, MemorySwap, CpuShares (CPU relatieve gewicht), MemoryReservationInMB, BlkioWeight (BlockIO relatieve gewicht).  In dit voorbeeld servicepakket Guest1Pkg één kern opgehaald op Hallo clusterknooppunten waar het wordt geplaatst.  Geheugenlimieten absoluut zijn dus Hallo codepakket beperkt too1024 is MB aan geheugen (en een voorlopig garantie reservering van dezelfde Hallo). Code-pakketten (containers of processen) zijn niet kunnen tooallocate meer geheugen dan deze limiet en probeert toodo dus in een out-geheugen-uitzondering resulteert. Voor de resource limiet afdwinging toowork hebben alle code pakketten binnen een servicepakket geheugenlimieten opgegeven.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a>Hallo containertoepassing implementeren
Al uw wijzigingen opslaan en Hallo toepassing bouwen. toopublish uw toepassing, met de rechtermuisknop op **MyFirstContainer** in Solution Explorer en selecteer **publiceren**.

In **verbindingseindpunt**, Voer Hallo eindpunt voor Hallo-cluster.  Bijvoorbeeld: 'containercluster.westus2.cloudapp.azure.com:19000'. U vindt de clientverbinding Hallo eindpunt in Hallo overzichtsblade voor uw cluster in Hallo [Azure-portal](https://portal.azure.com).

Klik op **Publish**.

[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een webhulpprogramma voor het inspecteren en beheren van toepassingen en knooppunten in een Service Fabric-cluster. Open een browser en ga toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/en volgt u de implementatie van de toepassing hello.  Hallo-toepassing wordt geïmplementeerd maar bevindt zich in een foutstatus totdat Hallo installatiekopie gedownload op de clusterknooppunten hello (dit kunnen enige tijd duren, afhankelijk van de grootte van de installatiekopie Hallo): ![fout][1]

Hallo toepassing gereed is wanneer deze ```Ready``` status: ![gereed][2]

Open een browser en ga toohttp://containercluster.westus2.cloudapp.azure.com:8081. U ziet Hallo kop "Hello World!" in de browser Hallo weergeven.

## <a name="clean-up"></a>Opruimen
U tooincur kosten doorgaan terwijl Hallo cluster wordt uitgevoerd, kunt u [verwijderen van uw cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).  [Party-clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) worden na een paar uur automatisch verwijderd.

Wanneer u push-Hallo installatiekopie toohello container register kunt u Hallo-afbeelding voor lokaal verwijderen vanaf de ontwikkelcomputer:

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a>Volledig voorbeeld van de manifesten voor de Fabric Service-toepassing en -service
Hier volgen Hallo volledige service en Toepassingsmanifesten in dit artikel gebruikt.

### <a name="servicemanifestxml"></a>ServiceManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="Guest1Pkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="Guest1Type" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->    
    <EnvironmentVariables>
      <EnvironmentVariable Name="HttpGatewayPort" Value=""/>
      <EnvironmentVariable Name="BackendServiceName" Value=""/>
    </EnvironmentVariables>

  </CodePackage>

  <!-- Config package is hello contents of hello Config directoy under PackageRoot that contains an
       independently-updateable and versioned set of custom configuration settings for your service. -->
  <ConfigPackage Name="Config" Version="1.0.0" />

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which to
           listen. Please note that if your service is partitioned, this port is shared with
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="MyFirstContainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Parameters>
    <Parameter Name="Guest1_InstanceCount" DefaultValue="-1" />
  </Parameters>
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion
       should match hello Name and Version attributes of hello ServiceManifest element defined in the
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="FrontendService.Code">
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentOverrides>
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="MIIB6QYJKoZIhvcNAQcDoIIB2jCCAdYCAQAxggFRMIIBTQIBADA1MCExHzAdBgNVBAMMFnJ5YW53aWRhdGFlbmNpcGhlcm1lbnQCEFfyjOX/17S6RIoSjA6UZ1QwDQYJKoZIhvcNAQEHMAAEg
gEAS7oqxvoz8i6+8zULhDzFpBpOTLU+c2mhBdqXpkLwVfcmWUNA82rEWG57Vl1jZXe7J9BkW9ly4xhU8BbARkZHLEuKqg0saTrTHsMBQ6KMQDotSdU8m8Y2BR5Y100wRjvVx3y5+iNYuy/JmM
gSrNyyMQ/45HfMuVb5B4rwnuP8PAkXNT9VLbPeqAfxsMkYg+vGCDEtd8m+bX/7Xgp/kfwxymOuUCrq/YmSwe9QTG3pBri7Hq1K3zEpX4FH/7W2Zb4o3fBAQ+FuxH4nFjFNoYG29inL0bKEcTX
yNZNKrvhdM3n1Uk/8W2Hr62FQ33HgeFR1yxQjLsUu800PrYcR5tLfyTB8BgkqhkiG9w0BBwEwHQYJYIZIAWUDBAEqBBBybgM5NUV8BeetUbMR8mJhgFBrVSUsnp9B8RyebmtgU36dZiSObDsI
NtTvlzhk11LIlae/5kjPv95r3lw6DHmV4kXLwiCNlcWPYIWBGIuspwyG+28EWSrHmN7Dt2WqEWqeNQ==" PasswordEncrypted="true"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
      </ContainerHostPolicies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this
         application type is created. You can also create one or more instances of service type using the
         ServiceFabric PowerShell module.

         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="Guest1">
      <StatelessService ServiceTypeName="Guest1Type" InstanceCount="[Guest1_InstanceCount]">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```

## <a name="configure-time-interval-before-container-is-force-terminated"></a>Tijdsinterval configureren voor geforceerd beëindigen van container

U kunt een tijdsinterval voor Hallo runtime toowait configureren voordat Hallo container wordt verwijderd nadat hello service verwijderen (of een knooppunt van de tooanother verplaatsen) is gestart. Configureren Hallo tijdsinterval verzendt Hallo `docker stop <time in seconds>` opdracht toohello container.   Zie [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) voor meer informatie. Hallo tijd interval toowait is opgegeven bij Hallo `Hosting` sectie. Hallo na cluster manifest codefragment ziet u hoe tooset Hallo Wacht-interval:

```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "ContainerDeactivationTimeout": "10",
          ...
          }
        ]
}
```
Hallo standaardtijdsinterval is ingesteld too10 seconden. Omdat deze configuratie dynamisch is, wordt een config alleen bijwerken op Hallo cluster updates Hallo time-out. 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a>Hallo runtime tooremove configureren ongebruikte container installatiekopieën

U kunt configureren Hallo Service Fabric-cluster tooremove ongebruikte container installatiekopieën van het Hallo-knooppunt. Deze configuratie kunt schijfruimte toobe opnieuw vastgelegd als te veel container afbeeldingen op Hallo knooppunt aanwezig zijn.  tooenable deze functie, de update Hallo `Hosting` sectie in het clustermanifest hello, zoals wordt weergegeven in het volgende codefragment Hallo: 


```xml
{
        "name": "Hosting",
        "parameters": [
          {
            "PruneContainerImages": “True”,
            "ContainerImagesToSkip": "microsoft/windowsservercore|microsoft/nanoserver|…",
          ...
          }
        ]
} 
```

Voor installatiekopieën die niet worden verwijderd, kunt u ze onder Hallo `ContainerImagesToSkip` parameter. 



## <a name="next-steps"></a>Volgende stappen
* Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-containers-overview.md).
* Lees Hallo [implementeren van een .NET-toepassing in een container](service-fabric-host-app-in-a-container.md) zelfstudie.
* Meer informatie over Service Fabric Hallo [toepassing levenscyclus](service-fabric-application-lifecycle.md).
* Afhandeling Hallo [codevoorbeelden Service Fabric-container](https://github.com/Azure-Samples/service-fabric-dotnet-containers) op GitHub.

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
