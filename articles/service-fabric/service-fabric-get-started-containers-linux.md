---
title: een toepassing van de Azure Service Fabric-container op Linux aaaCreate | Microsoft Docs
description: Maak uw eerste Linux-containertoepassing in Azure Service Fabric.  Een Docker-afbeelding met uw toepassing bouwen, push Hallo installatiekopie tooa container register, bouwen en implementeren van een container Service Fabric-toepassing.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/28/2017
ms.author: ryanwi
ms.openlocfilehash: 348dbcbaa1a534fb2808450e4c2d5f9acc7c7b35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a>Uw eerste Service Fabric-containertoepassing maken in Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started-containers.md)
> * [Linux](service-fabric-get-started-containers-linux.md)

Een bestaande toepassing in een container Linux uitgevoerd op een Service Fabric-cluster nodig niet alle wijzigingen tooyour toepassingen. Dit artikel begeleidt u bij het maken van een Docker-afbeelding met een Python [Flask](http://flask.pocoo.org/) web-toepassing en deze tooa Service Fabric-cluster is geïmplementeerd.  U gaat uw containertoepassing ook delen via [Azure Container Registry](/azure/container-registry/).  In dit artikel wordt ervan uitgegaan dat u de basisbeginselen kent van Docker. U kunt meer informatie over Docker door Hallo lezen [Docker-overzicht](https://docs.docker.com/engine/understanding-docker/).

## <a name="prerequisites"></a>Vereisten
* Een ontwikkelcomputer waarop wordt uitgevoerd:
  * [Service Fabric SDK en hulpprogramma's](service-fabric-get-started-linux.md).
  * [Docker CE voor Linux](https://docs.docker.com/engine/installation/#prior-releases). 
  * [Service Fabric-CLI](service-fabric-cli.md)

* Een register in Azure Container Registry - [Een containerregister maken](../container-registry/container-registry-get-started-portal.md) in uw Azure-abonnement. 

## <a name="define-hello-docker-container"></a>Hallo Docker-container definiëren
Maken van een installatiekopie op basis van Hallo [Python installatiekopie](https://hub.docker.com/_/python/) zich bevinden op Docker-Hub. 

Definieer uw Docker-container in een Dockerfile. Hallo Dockerfile bevat instructies voor het instellen van Hallo-omgeving in de container, Hallo-toepassing die u wilt dat toorun laden en poorten toewijzen. Hallo Dockerfile is Hallo invoer toohello `docker build` opdracht, waarbij Hallo installatiekopie wordt gemaakt. 

Maken van een lege map en het Hallo-bestand maken *Dockerfile* (met zonder extensie). Hallo te volgende toevoegen*Dockerfile* en sla de wijzigingen:

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set hello working directory too/app
WORKDIR /app

# Copy hello current directory contents into hello container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
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

## <a name="build-hello-image"></a>Hallo installatiekopie maken
Voer Hallo `docker build` toocreate Hallo de afbeelding die wordt uitgevoerd van uw webtoepassing. Open een PowerShell-venster en te navigeren*c:\temp\helloworldapp*. Hallo volgende opdracht uitvoeren:

```bash
docker build -t helloworldapp .
```

Met deze opdracht builds Hallo nieuwe installatiekopie met Hallo-instructies in uw Dockerfile naming (-t tagging) Hallo installatiekopie 'helloworldapp'. Voor het bouwen van een installatiekopie van een Hallo basisinstallatiekopie omlaag ophaalt uit Docker-Hub en maakt een nieuwe installatiekopie waarmee uw toepassing boven op Hallo basisinstallatiekopie worden toegevoegd.  

Uitvoeren zodra Hallo build-opdracht is voltooid, Hallo `docker images` toosee informatie over de nieuwe installatiekopie Hallo opdracht:

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a>Hallo-toepassing lokaal uitvoeren
Controleer of dat uw beperkte toepassing lokaal voordat u het Hallo-container register wordt uitgevoerd.  

Hallo toepassing uitvoert, toewijzing van uw computer poort 4000 toohello container van poort 80 weergegeven:

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

*naam* geeft een naam toohello container (in plaats van de container-ID Hallo) uitgevoerd.

Verbinding maken met container toohello.  Open een webbrowser die wijst toohello IP-adres op poort 4000, bijvoorbeeld 'http://localhost:4000' geretourneerd. U ziet Hallo kop "Hello World!" in de browser Hallo weergeven.

![Hallo wereld!][hello-world]

toostop uw container, uitvoeren:

```bash
docker stop my-web-site
```

Hallo-container uit uw ontwikkelcomputer verwijderen:

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a>Push Hallo installatiekopie toohello container register
Nadat u hebt gecontroleerd dat Hallo toepassing wordt uitgevoerd in Docker, push-Hallo installatiekopie tooyour register in Azure Container register.

Voer `docker login` toolog in tooyour container register met uw [register referenties](../container-registry/container-registry-authentication.md).

Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md). Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering.  Of u kunt zich aanmelden met uw gebruikersnaam en wachtwoord van het register.

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

Hallo volgende opdracht maakt u een label of alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register. In dit voorbeeld plaatsen Hallo-installatiekopie in Hallo `samples` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

Push Hallo installatiekopie tooyour container register:

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a>Installatiekopie van pakket Hallo Docker met Yeoman
Hallo Service Fabric SDK voor Linux bevat een [Yeoman](http://yeoman.io/) generator waardoor u eenvoudig toocreate uw toepassing en een installatiekopie van de container toevoegen. We gebruiken Yeoman toocreate aangeroepen voor een toepassing met een enkele Docker-container *SimpleContainerApp*.

toocreate een container Service Fabric-toepassing, open een terminalvenster en voer `yo azuresfcontainer`.  

Naam van uw toepassing (bijvoorbeeld 'mycontainer'). 

Hallo-URL opgeven voor Hallo container installatiekopie in een register container (bijvoorbeeld, ""). 

Deze installatiekopie is een werkbelasting ingangspunt gedefinieerd, dus moet tooexplicitly invoer-opdrachten opgeven (opdrachten binnen het Hallo-container die behoudt Hallo container uitgevoerd na het opstarten worden uitgevoerd). 

Geef '1' exemplaar op.

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a>Poorttoewijzing en containeropslagplaatsverificatie configureren
Uw containerservice heeft een eindpunt voor communicatie nodig.  Voeg nu Hallo-protocol, poort en het type tooan `Endpoint` in Hallo ServiceManifest.xml-bestand. Voor dit artikel luistert Hallo beperkte service op poort 4000: 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
Hallo bieden `UriScheme` automatisch registers container eindpunt Hallo Hello naamgeving van Service Fabric-service voor detectie. Een volledige ServiceManifest.xml voorbeeld van een bestand wordt op Hallo einde van dit artikel aangeboden. 

Hallo-poorttoewijzing container poort-naar-host configureren door te geven een `PortBinding` beleid in `ContainerHostPolicies` van Hallo ApplicationManifest.xml bestand.  Voor dit artikel `ContainerPort` 80 (Hallo container wordt poort 80, als de opgegeven in de Hallo Dockerfile) en `EndpointRef` is 'myserviceTypeEndpoint' (Hallo eindpunt gedefinieerd in Hallo servicemanifest).  Inkomende aanvragen toohello-service op poort 4000 zijn toegewezen tooport 80 op Hallo-container.  Als uw container tooauthenticate met een persoonlijke opslagplaats moet, voegt u `RepositoryCredentials`.  Voor dit artikel toevoegen Hallo-accountnaam en wachtwoord voor Hallo myregistry.azurecr.io container register. 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a>Build en pakket Hallo Service Fabric-toepassing
Hallo Service Fabric Yeoman sjablonen bevatten een build script voor [Gradle](https://gradle.org/), waardoor u toobuild Hallo toepassing hello terminal kunt gebruiken. toobuild en pakket Hallo-toepassing hello volgende uitvoeren:

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a>Hallo-toepassing implementeren
Als de toepassing hello is gebouwd, kunt u deze lokale toohello-cluster met behulp van Service Fabric CLI Hallo implementeren.

Verbinding maken met toohello lokale Service Fabric-cluster.

```bash
sfctl cluster select --endpoint http://localhost:19080
```

Gebruik Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype Hallo en op een exemplaar van de toepassing hello maken.

```bash
./install.sh
```

Open een browser en ga tooService Fabric Explorer op http://localhost: 19080/Explorer (localhost vervangen met particuliere IP-Hallo Hallo VM als Vagrant op Mac OS X). Hallo toepassingen knooppunt uitvouwen en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type.

Verbinding maken met container toohello.  Open een webbrowser die wijst toohello IP-adres op poort 4000, bijvoorbeeld 'http://localhost:4000' geretourneerd. U ziet Hallo kop "Hello World!" in de browser Hallo weergeven.

![Hallo wereld!][hello-world]

## <a name="clean-up"></a>Opruimen
Gebruik Hallo uninstall-script in Hallo sjabloon toodelete Hallo toepassingsexemplaar van Hallo lokaal ontwikkelcluster en registratie van toepassingstype Hallo.

```bash
./uninstall.sh
```

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
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is hello name of your ServiceType.
         hello UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      tooService Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables tooyour container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a>ApplicationManifest.xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import hello ServiceManifest from hello ServicePackage. hello ServiceManifestName and ServiceManifestVersion 
       should match hello Name and Version attributes of hello ServiceManifest element defined in hello 
       ServiceManifest.xml file. -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="myservicePkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides />
    <Policies>
      <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
      </ContainerHostPolicies>
    </Policies>
  </ServiceManifestImport>
  <DefaultServices>
    <!-- hello section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using hello 
         ServiceFabric PowerShell module.
         
         hello attribute ServiceTypeName below must match hello name defined in hello imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount too1.  On a multi-node production 
      cluster, set InstanceCount too-1 for hello container service toorun on every node in 
      hello cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-tooan-existing-application"></a>Meer services tooan bestaande toepassing toe te voegen

tooadd uitvoeren van een andere container service tooan toepassing al is gemaakt met behulp van yeoman, Hallo volgende stappen:

1. Toohello hoofdmap van de bestaande toepassing hello wijzigen.  Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.
2. Voer `yo azuresfcontainer:AddService` uit.

<a id="manually"></a>


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

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
