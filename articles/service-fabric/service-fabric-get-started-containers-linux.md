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
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="bb961-104">Uw eerste Service Fabric-containertoepassing maken in Linux</span><span class="sxs-lookup"><span data-stu-id="bb961-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb961-105">Windows</span><span class="sxs-lookup"><span data-stu-id="bb961-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="bb961-106">Linux</span><span class="sxs-lookup"><span data-stu-id="bb961-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="bb961-107">Een bestaande toepassing in een container Linux uitgevoerd op een Service Fabric-cluster nodig niet alle wijzigingen tooyour toepassingen.</span><span class="sxs-lookup"><span data-stu-id="bb961-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="bb961-108">Dit artikel begeleidt u bij het maken van een Docker-afbeelding met een Python [Flask](http://flask.pocoo.org/) web-toepassing en deze tooa Service Fabric-cluster is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="bb961-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="bb961-109">U gaat uw containertoepassing ook delen via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="bb961-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="bb961-110">In dit artikel wordt ervan uitgegaan dat u de basisbeginselen kent van Docker.</span><span class="sxs-lookup"><span data-stu-id="bb961-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="bb961-111">U kunt meer informatie over Docker door Hallo lezen [Docker-overzicht](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="bb961-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb961-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="bb961-112">Prerequisites</span></span>
* <span data-ttu-id="bb961-113">Een ontwikkelcomputer waarop wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="bb961-113">A development computer running:</span></span>
  * <span data-ttu-id="bb961-114">[Service Fabric SDK en hulpprogramma's](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="bb961-115">[Docker CE voor Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="bb961-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="bb961-116">Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="bb961-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="bb961-117">Een register in Azure Container Registry - [Een containerregister maken](../container-registry/container-registry-get-started-portal.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="bb961-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-hello-docker-container"></a><span data-ttu-id="bb961-118">Hallo Docker-container definiëren</span><span class="sxs-lookup"><span data-stu-id="bb961-118">Define hello Docker container</span></span>
<span data-ttu-id="bb961-119">Maken van een installatiekopie op basis van Hallo [Python installatiekopie](https://hub.docker.com/_/python/) zich bevinden op Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="bb961-119">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="bb961-120">Definieer uw Docker-container in een Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="bb961-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="bb961-121">Hallo Dockerfile bevat instructies voor het instellen van Hallo-omgeving in de container, Hallo-toepassing die u wilt dat toorun laden en poorten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="bb961-121">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="bb961-122">Hallo Dockerfile is Hallo invoer toohello `docker build` opdracht, waarbij Hallo installatiekopie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bb961-122">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span> 

<span data-ttu-id="bb961-123">Maken van een lege map en het Hallo-bestand maken *Dockerfile* (met zonder extensie).</span><span class="sxs-lookup"><span data-stu-id="bb961-123">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="bb961-124">Hallo te volgende toevoegen*Dockerfile* en sla de wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="bb961-124">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="bb961-125">Lees Hallo [Dockerfile verwijzing](https://docs.docker.com/engine/reference/builder/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bb961-125">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="bb961-126">Een eenvoudige webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="bb961-126">Create a simple web application</span></span>
<span data-ttu-id="bb961-127">Maak een Flask-toepassing die luistert op poort 80 en 'Hallo Wereld!' retourneert.</span><span class="sxs-lookup"><span data-stu-id="bb961-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="bb961-128">In dezelfde map Hallo, Hallo-bestand maken *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="bb961-128">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="bb961-129">Voeg de volgende Hallo en sla de wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="bb961-129">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="bb961-130">Maak ook Hallo *app.py* -bestand en voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb961-130">Also create hello *app.py* file and add hello following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-hello-image"></a><span data-ttu-id="bb961-131">Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="bb961-131">Build hello image</span></span>
<span data-ttu-id="bb961-132">Voer Hallo `docker build` toocreate Hallo de afbeelding die wordt uitgevoerd van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="bb961-132">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="bb961-133">Open een PowerShell-venster en te navigeren*c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="bb961-133">Open a PowerShell window and navigate too*c:\temp\helloworldapp*.</span></span> <span data-ttu-id="bb961-134">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bb961-134">Run hello following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="bb961-135">Met deze opdracht builds Hallo nieuwe installatiekopie met Hallo-instructies in uw Dockerfile naming (-t tagging) Hallo installatiekopie 'helloworldapp'.</span><span class="sxs-lookup"><span data-stu-id="bb961-135">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="bb961-136">Voor het bouwen van een installatiekopie van een Hallo basisinstallatiekopie omlaag ophaalt uit Docker-Hub en maakt een nieuwe installatiekopie waarmee uw toepassing boven op Hallo basisinstallatiekopie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bb961-136">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="bb961-137">Uitvoeren zodra Hallo build-opdracht is voltooid, Hallo `docker images` toosee informatie over de nieuwe installatiekopie Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="bb961-137">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="bb961-138">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bb961-138">Run hello application locally</span></span>
<span data-ttu-id="bb961-139">Controleer of dat uw beperkte toepassing lokaal voordat u het Hallo-container register wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb961-139">Verify that your containerized application runs locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="bb961-140">Hallo toepassing uitvoert, toewijzing van uw computer poort 4000 toohello container van poort 80 weergegeven:</span><span class="sxs-lookup"><span data-stu-id="bb961-140">Run hello application, mapping your computer's port 4000 toohello container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="bb961-141">*naam* geeft een naam toohello container (in plaats van de container-ID Hallo) uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bb961-141">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="bb961-142">Verbinding maken met container toohello.</span><span class="sxs-lookup"><span data-stu-id="bb961-142">Connect toohello running container.</span></span>  <span data-ttu-id="bb961-143">Open een webbrowser die wijst toohello IP-adres op poort 4000, bijvoorbeeld 'http://localhost:4000' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bb961-143">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="bb961-144">U ziet Hallo kop "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="bb961-144">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="bb961-145">in de browser Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="bb961-145">display in hello browser.</span></span>

![Hallo wereld!][hello-world]

<span data-ttu-id="bb961-147">toostop uw container, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bb961-147">toostop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="bb961-148">Hallo-container uit uw ontwikkelcomputer verwijderen:</span><span class="sxs-lookup"><span data-stu-id="bb961-148">Delete hello container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="bb961-149">Push Hallo installatiekopie toohello container register</span><span class="sxs-lookup"><span data-stu-id="bb961-149">Push hello image toohello container registry</span></span>
<span data-ttu-id="bb961-150">Nadat u hebt gecontroleerd dat Hallo toepassing wordt uitgevoerd in Docker, push-Hallo installatiekopie tooyour register in Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="bb961-150">After you verify that hello application runs in Docker, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="bb961-151">Voer `docker login` toolog in tooyour container register met uw [register referenties](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-151">Run `docker login` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="bb961-152">Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-152">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="bb961-153">Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering.</span><span class="sxs-lookup"><span data-stu-id="bb961-153">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span>  <span data-ttu-id="bb961-154">Of u kunt zich aanmelden met uw gebruikersnaam en wachtwoord van het register.</span><span class="sxs-lookup"><span data-stu-id="bb961-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="bb961-155">Hallo volgende opdracht maakt u een label of alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register.</span><span class="sxs-lookup"><span data-stu-id="bb961-155">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="bb961-156">In dit voorbeeld plaatsen Hallo-installatiekopie in Hallo `samples` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="bb961-156">This example places hello image in hello `samples` namespace tooavoid clutter in hello root of hello registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="bb961-157">Push Hallo installatiekopie tooyour container register:</span><span class="sxs-lookup"><span data-stu-id="bb961-157">Push hello image tooyour container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-hello-docker-image-with-yeoman"></a><span data-ttu-id="bb961-158">Installatiekopie van pakket Hallo Docker met Yeoman</span><span class="sxs-lookup"><span data-stu-id="bb961-158">Package hello Docker image with Yeoman</span></span>
<span data-ttu-id="bb961-159">Hallo Service Fabric SDK voor Linux bevat een [Yeoman](http://yeoman.io/) generator waardoor u eenvoudig toocreate uw toepassing en een installatiekopie van de container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="bb961-159">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="bb961-160">We gebruiken Yeoman toocreate aangeroepen voor een toepassing met een enkele Docker-container *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="bb961-160">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="bb961-161">toocreate een container Service Fabric-toepassing, open een terminalvenster en voer `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="bb961-161">toocreate a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="bb961-162">Naam van uw toepassing (bijvoorbeeld 'mycontainer').</span><span class="sxs-lookup"><span data-stu-id="bb961-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="bb961-163">Hallo-URL opgeven voor Hallo container installatiekopie in een register container (bijvoorbeeld, "").</span><span class="sxs-lookup"><span data-stu-id="bb961-163">Provide hello URL for hello container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="bb961-164">Deze installatiekopie is een werkbelasting ingangspunt gedefinieerd, dus moet tooexplicitly invoer-opdrachten opgeven (opdrachten binnen het Hallo-container die behoudt Hallo container uitgevoerd na het opstarten worden uitgevoerd).</span><span class="sxs-lookup"><span data-stu-id="bb961-164">This image has a workload entry-point defined, so need tooexplicitly specify input commands (commands run inside hello container, which will keep hello container running after startup).</span></span> 

<span data-ttu-id="bb961-165">Geef '1' exemplaar op.</span><span class="sxs-lookup"><span data-stu-id="bb961-165">Specify an instance count of "1".</span></span>

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="bb961-167">Poorttoewijzing en containeropslagplaatsverificatie configureren</span><span class="sxs-lookup"><span data-stu-id="bb961-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="bb961-168">Uw containerservice heeft een eindpunt voor communicatie nodig.</span><span class="sxs-lookup"><span data-stu-id="bb961-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="bb961-169">Voeg nu Hallo-protocol, poort en het type tooan `Endpoint` in Hallo ServiceManifest.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="bb961-169">Now add hello protocol, port, and type tooan `Endpoint` in hello ServiceManifest.xml file.</span></span> <span data-ttu-id="bb961-170">Voor dit artikel luistert Hallo beperkte service op poort 4000:</span><span class="sxs-lookup"><span data-stu-id="bb961-170">For this article, hello containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="bb961-171">Hallo bieden `UriScheme` automatisch registers container eindpunt Hallo Hello naamgeving van Service Fabric-service voor detectie.</span><span class="sxs-lookup"><span data-stu-id="bb961-171">Providing hello `UriScheme` automatically registers hello container endpoint with hello Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="bb961-172">Een volledige ServiceManifest.xml voorbeeld van een bestand wordt op Hallo einde van dit artikel aangeboden.</span><span class="sxs-lookup"><span data-stu-id="bb961-172">A full ServiceManifest.xml example file is provided at hello end of this article.</span></span> 

<span data-ttu-id="bb961-173">Hallo-poorttoewijzing container poort-naar-host configureren door te geven een `PortBinding` beleid in `ContainerHostPolicies` van Hallo ApplicationManifest.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="bb961-173">Configure hello container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="bb961-174">Voor dit artikel `ContainerPort` 80 (Hallo container wordt poort 80, als de opgegeven in de Hallo Dockerfile) en `EndpointRef` is 'myserviceTypeEndpoint' (Hallo eindpunt gedefinieerd in Hallo servicemanifest).</span><span class="sxs-lookup"><span data-stu-id="bb961-174">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (hello endpoint defined in hello service manifest).</span></span>  <span data-ttu-id="bb961-175">Inkomende aanvragen toohello-service op poort 4000 zijn toegewezen tooport 80 op Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="bb961-175">Incoming requests toohello service on port 4000 are mapped tooport 80 on hello container.</span></span>  <span data-ttu-id="bb961-176">Als uw container tooauthenticate met een persoonlijke opslagplaats moet, voegt u `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="bb961-176">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="bb961-177">Voor dit artikel toevoegen Hallo-accountnaam en wachtwoord voor Hallo myregistry.azurecr.io container register.</span><span class="sxs-lookup"><span data-stu-id="bb961-177">For this article, add hello account name and password for hello myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-hello-service-fabric-application"></a><span data-ttu-id="bb961-178">Build en pakket Hallo Service Fabric-toepassing</span><span class="sxs-lookup"><span data-stu-id="bb961-178">Build and package hello Service Fabric application</span></span>
<span data-ttu-id="bb961-179">Hallo Service Fabric Yeoman sjablonen bevatten een build script voor [Gradle](https://gradle.org/), waardoor u toobuild Hallo toepassing hello terminal kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bb961-179">hello Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use toobuild hello application from hello terminal.</span></span> <span data-ttu-id="bb961-180">toobuild en pakket Hallo-toepassing hello volgende uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="bb961-180">toobuild and package hello application, run hello following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-hello-application"></a><span data-ttu-id="bb961-181">Hallo-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="bb961-181">Deploy hello application</span></span>
<span data-ttu-id="bb961-182">Als de toepassing hello is gebouwd, kunt u deze lokale toohello-cluster met behulp van Service Fabric CLI Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="bb961-182">Once hello application is built, you can deploy it toohello local cluster using hello Service Fabric CLI.</span></span>

<span data-ttu-id="bb961-183">Verbinding maken met toohello lokale Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="bb961-183">Connect toohello local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="bb961-184">Gebruik Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype Hallo en op een exemplaar van de toepassing hello maken.</span><span class="sxs-lookup"><span data-stu-id="bb961-184">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="bb961-185">Open een browser en ga tooService Fabric Explorer op http://localhost: 19080/Explorer (localhost vervangen met particuliere IP-Hallo Hallo VM als Vagrant op Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="bb961-185">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="bb961-186">Hallo toepassingen knooppunt uitvouwen en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type.</span><span class="sxs-lookup"><span data-stu-id="bb961-186">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>

<span data-ttu-id="bb961-187">Verbinding maken met container toohello.</span><span class="sxs-lookup"><span data-stu-id="bb961-187">Connect toohello running container.</span></span>  <span data-ttu-id="bb961-188">Open een webbrowser die wijst toohello IP-adres op poort 4000, bijvoorbeeld 'http://localhost:4000' geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="bb961-188">Open a web browser pointing toohello IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="bb961-189">U ziet Hallo kop "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="bb961-189">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="bb961-190">in de browser Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="bb961-190">display in hello browser.</span></span>

![Hallo wereld!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="bb961-192">Opruimen</span><span class="sxs-lookup"><span data-stu-id="bb961-192">Clean up</span></span>
<span data-ttu-id="bb961-193">Gebruik Hallo uninstall-script in Hallo sjabloon toodelete Hallo toepassingsexemplaar van Hallo lokaal ontwikkelcluster en registratie van toepassingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="bb961-193">Use hello uninstall script provided in hello template toodelete hello application instance from hello local development cluster and unregister hello application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="bb961-194">Wanneer u push-Hallo installatiekopie toohello container register kunt u Hallo-afbeelding voor lokaal verwijderen vanaf de ontwikkelcomputer:</span><span class="sxs-lookup"><span data-stu-id="bb961-194">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="bb961-195">Volledig voorbeeld van de manifesten voor de Fabric Service-toepassing en -service</span><span class="sxs-lookup"><span data-stu-id="bb961-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="bb961-196">Hier volgen Hallo volledige service en Toepassingsmanifesten in dit artikel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="bb961-196">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="bb961-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="bb961-197">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="bb961-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="bb961-198">ApplicationManifest.xml</span></span>
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
## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="bb961-199">Meer services tooan bestaande toepassing toe te voegen</span><span class="sxs-lookup"><span data-stu-id="bb961-199">Adding more services tooan existing application</span></span>

<span data-ttu-id="bb961-200">tooadd uitvoeren van een andere container service tooan toepassing al is gemaakt met behulp van yeoman, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="bb961-200">tooadd another container service tooan application already created using yeoman, perform hello following steps:</span></span>

1. <span data-ttu-id="bb961-201">Toohello hoofdmap van de bestaande toepassing hello wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bb961-201">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="bb961-202">Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="bb961-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="bb961-203">Voer `yo azuresfcontainer:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="bb961-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="bb961-204">Tijdsinterval configureren voor geforceerd beëindigen van container</span><span class="sxs-lookup"><span data-stu-id="bb961-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="bb961-205">U kunt een tijdsinterval voor Hallo runtime toowait configureren voordat Hallo container wordt verwijderd nadat hello service verwijderen (of een knooppunt van de tooanother verplaatsen) is gestart.</span><span class="sxs-lookup"><span data-stu-id="bb961-205">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="bb961-206">Configureren Hallo tijdsinterval verzendt Hallo `docker stop <time in seconds>` opdracht toohello container.</span><span class="sxs-lookup"><span data-stu-id="bb961-206">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="bb961-207">Zie [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bb961-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="bb961-208">Hallo tijd interval toowait is opgegeven bij Hallo `Hosting` sectie.</span><span class="sxs-lookup"><span data-stu-id="bb961-208">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="bb961-209">Hallo na cluster manifest codefragment ziet u hoe tooset Hallo Wacht-interval:</span><span class="sxs-lookup"><span data-stu-id="bb961-209">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="bb961-210">Hallo standaardtijdsinterval is ingesteld too10 seconden.</span><span class="sxs-lookup"><span data-stu-id="bb961-210">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="bb961-211">Omdat deze configuratie dynamisch is, wordt een config alleen bijwerken op Hallo cluster updates Hallo time-out.</span><span class="sxs-lookup"><span data-stu-id="bb961-211">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="bb961-212">Hallo runtime tooremove configureren ongebruikte container installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="bb961-212">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="bb961-213">U kunt configureren Hallo Service Fabric-cluster tooremove ongebruikte container installatiekopieën van het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="bb961-213">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="bb961-214">Deze configuratie kunt schijfruimte toobe opnieuw vastgelegd als te veel container afbeeldingen op Hallo knooppunt aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="bb961-214">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="bb961-215">tooenable deze functie, de update Hallo `Hosting` sectie in het clustermanifest hello, zoals wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="bb961-215">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="bb961-216">Voor installatiekopieën die niet worden verwijderd, kunt u ze onder Hallo `ContainerImagesToSkip` parameter.</span><span class="sxs-lookup"><span data-stu-id="bb961-216">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="bb961-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bb961-217">Next steps</span></span>
* <span data-ttu-id="bb961-218">Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="bb961-219">Lees Hallo [implementeren van een .NET-toepassing in een container](service-fabric-host-app-in-a-container.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="bb961-219">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="bb961-220">Meer informatie over Service Fabric Hallo [toepassing levenscyclus](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="bb961-220">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="bb961-221">Afhandeling Hallo [codevoorbeelden Service Fabric-container](https://github.com/Azure-Samples/service-fabric-dotnet-containers) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="bb961-221">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
