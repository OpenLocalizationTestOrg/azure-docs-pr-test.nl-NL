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
# <a name="create-your-first-service-fabric-container-application-on-windows"></a><span data-ttu-id="de9d5-104">Uw eerste Service Fabric-containertoepassing maken in Windows</span><span class="sxs-lookup"><span data-stu-id="de9d5-104">Create your first Service Fabric container application on Windows</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="de9d5-105">Windows</span><span class="sxs-lookup"><span data-stu-id="de9d5-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="de9d5-106">Linux</span><span class="sxs-lookup"><span data-stu-id="de9d5-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="de9d5-107">Een bestaande toepassing in een Windows-container uitgevoerd op een Service Fabric-cluster nodig niet alle wijzigingen tooyour toepassingen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-107">Running an existing application in a Windows container on a Service Fabric cluster doesn't require any changes tooyour application.</span></span> <span data-ttu-id="de9d5-108">Dit artikel begeleidt u bij het maken van een Docker-afbeelding met een Python [Flask](http://flask.pocoo.org/) web-toepassing en deze tooa Service Fabric-cluster is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it tooa Service Fabric cluster.</span></span>  <span data-ttu-id="de9d5-109">U gaat uw containertoepassing ook delen via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="de9d5-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="de9d5-110">In dit artikel wordt ervan uitgegaan dat u de basisbeginselen kent van Docker.</span><span class="sxs-lookup"><span data-stu-id="de9d5-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="de9d5-111">U kunt meer informatie over Docker door Hallo lezen [Docker-overzicht](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="de9d5-111">You can learn about Docker by reading hello [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de9d5-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="de9d5-112">Prerequisites</span></span>
<span data-ttu-id="de9d5-113">Een ontwikkelcomputer waarop wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="de9d5-113">A development computer running:</span></span>
* <span data-ttu-id="de9d5-114">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="de9d5-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="de9d5-115">[Service Fabric SDK en hulpprogramma's](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-115">[Service Fabric SDK and tools](service-fabric-get-started.md).</span></span>
*  <span data-ttu-id="de9d5-116">Docker voor Windows.</span><span class="sxs-lookup"><span data-stu-id="de9d5-116">Docker for Windows.</span></span>  <span data-ttu-id="de9d5-117">[Download Docker CE voor Windows (stabiel)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span><span class="sxs-lookup"><span data-stu-id="de9d5-117">[Get Docker CE for Windows (stable)](https://store.docker.com/editions/community/docker-ce-desktop-windows?tab=description).</span></span> <span data-ttu-id="de9d5-118">Na het installeren en starten van Docker, met de rechtermuisknop op het pictogram in systeemvak voor Hallo en selecteer **tooWindows containers overschakelen**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-118">After installing and starting Docker, right-click on hello tray icon and select **Switch tooWindows containers**.</span></span> <span data-ttu-id="de9d5-119">Dit is vereiste toorun Docker-installatiekopieën op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="de9d5-119">This is required toorun Docker images based on Windows.</span></span>

<span data-ttu-id="de9d5-120">Een Windows-cluster met drie of meer knooppunten die worden uitgevoerd op Windows Server 2016 met containers - [Een cluster maken](service-fabric-cluster-creation-via-portal.md) of [Service Fabric gratis uitproberen](https://aka.ms/tryservicefabric).</span><span class="sxs-lookup"><span data-stu-id="de9d5-120">A Windows cluster with three or more nodes running on Windows Server 2016 with Containers- [Create a cluster](service-fabric-cluster-creation-via-portal.md) or [try Service Fabric for free](https://aka.ms/tryservicefabric).</span></span>

<span data-ttu-id="de9d5-121">Een register in Azure Container Registry - [Een containerregister maken](../container-registry/container-registry-get-started-portal.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="de9d5-121">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span>

## <a name="define-hello-docker-container"></a><span data-ttu-id="de9d5-122">Hallo Docker-container definiëren</span><span class="sxs-lookup"><span data-stu-id="de9d5-122">Define hello Docker container</span></span>
<span data-ttu-id="de9d5-123">Maken van een installatiekopie op basis van Hallo [Python installatiekopie](https://hub.docker.com/_/python/) zich bevinden op Docker-Hub.</span><span class="sxs-lookup"><span data-stu-id="de9d5-123">Build an image based on hello [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span>

<span data-ttu-id="de9d5-124">Definieer uw Docker-container in een Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="de9d5-124">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="de9d5-125">Hallo Dockerfile bevat instructies voor het instellen van Hallo-omgeving in de container, Hallo-toepassing die u wilt dat toorun laden en poorten toewijzen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-125">hello Dockerfile contains instructions for setting up hello environment inside your container, loading hello application you want toorun, and mapping ports.</span></span> <span data-ttu-id="de9d5-126">Hallo Dockerfile is Hallo invoer toohello `docker build` opdracht, waarbij Hallo installatiekopie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de9d5-126">hello Dockerfile is hello input toohello `docker build` command, which creates hello image.</span></span>

<span data-ttu-id="de9d5-127">Maken van een lege map en het Hallo-bestand maken *Dockerfile* (met zonder extensie).</span><span class="sxs-lookup"><span data-stu-id="de9d5-127">Create an empty directory and create hello file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="de9d5-128">Hallo te volgende toevoegen*Dockerfile* en sla de wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="de9d5-128">Add hello following too*Dockerfile* and save your changes:</span></span>

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

<span data-ttu-id="de9d5-129">Lees Hallo [Dockerfile verwijzing](https://docs.docker.com/engine/reference/builder/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="de9d5-129">Read hello [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="de9d5-130">Een eenvoudige webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="de9d5-130">Create a simple web application</span></span>
<span data-ttu-id="de9d5-131">Maak een Flask-toepassing die luistert op poort 80 en 'Hallo Wereld!' retourneert.</span><span class="sxs-lookup"><span data-stu-id="de9d5-131">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="de9d5-132">In dezelfde map Hallo, Hallo-bestand maken *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="de9d5-132">In hello same directory, create hello file *requirements.txt*.</span></span>  <span data-ttu-id="de9d5-133">Voeg de volgende Hallo en sla de wijzigingen:</span><span class="sxs-lookup"><span data-stu-id="de9d5-133">Add hello following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="de9d5-134">Maak ook Hallo *app.py* -bestand en voeg de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="de9d5-134">Also create hello *app.py* file and add hello following:</span></span>

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
## <a name="build-hello-image"></a><span data-ttu-id="de9d5-135">Hallo installatiekopie maken</span><span class="sxs-lookup"><span data-stu-id="de9d5-135">Build hello image</span></span>
<span data-ttu-id="de9d5-136">Voer Hallo `docker build` toocreate Hallo de afbeelding die wordt uitgevoerd van uw webtoepassing.</span><span class="sxs-lookup"><span data-stu-id="de9d5-136">Run hello `docker build` command toocreate hello image that runs your web application.</span></span> <span data-ttu-id="de9d5-137">Open een PowerShell-venster en ga toohello map waarin zich Hallo Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="de9d5-137">Open a PowerShell window and navigate toohello directory containing hello Dockerfile.</span></span> <span data-ttu-id="de9d5-138">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="de9d5-138">Run hello following command:</span></span>

```
docker build -t helloworldapp .
```

<span data-ttu-id="de9d5-139">Met deze opdracht builds Hallo nieuwe installatiekopie met Hallo-instructies in uw Dockerfile naming (-t tagging) Hallo installatiekopie 'helloworldapp'.</span><span class="sxs-lookup"><span data-stu-id="de9d5-139">This command builds hello new image using hello instructions in your Dockerfile, naming (-t tagging) hello image "helloworldapp".</span></span> <span data-ttu-id="de9d5-140">Voor het bouwen van een installatiekopie van een Hallo basisinstallatiekopie omlaag ophaalt uit Docker-Hub en maakt een nieuwe installatiekopie waarmee uw toepassing boven op Hallo basisinstallatiekopie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-140">Building an image pulls hello base image down from Docker Hub and creates a new image that adds your application on top of hello base image.</span></span>  

<span data-ttu-id="de9d5-141">Uitvoeren zodra Hallo build-opdracht is voltooid, Hallo `docker images` toosee informatie over de nieuwe installatiekopie Hallo opdracht:</span><span class="sxs-lookup"><span data-stu-id="de9d5-141">Once hello build command completes, run hello `docker images` command toosee information on hello new image:</span></span>

```
$ docker images

REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              8ce25f5d6a79        2 minutes ago       10.4 GB
```

## <a name="run-hello-application-locally"></a><span data-ttu-id="de9d5-142">Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="de9d5-142">Run hello application locally</span></span>
<span data-ttu-id="de9d5-143">Controleer of uw installatiekopie lokaal voordat u het register van Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="de9d5-143">Verify your image locally before pushing it hello container registry.</span></span>  

<span data-ttu-id="de9d5-144">Hallo-toepassing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="de9d5-144">Run hello application:</span></span>

```
docker run -d --name my-web-site helloworldapp
```

<span data-ttu-id="de9d5-145">*naam* geeft een naam toohello container (in plaats van de container-ID Hallo) uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-145">*name* gives a name toohello running container (instead of hello container ID).</span></span>

<span data-ttu-id="de9d5-146">Eenmaal Hallo container wordt gestart, het IP-adres zoeken, zodat u verbinding kunt maken met container uitgevoerd vanuit een browser tooyour:</span><span class="sxs-lookup"><span data-stu-id="de9d5-146">Once hello container starts, find its IP address so that you can connect tooyour running container from a browser:</span></span>
```
docker inspect -f "{{ .NetworkSettings.Networks.nat.IPAddress }}" my-web-site
```

<span data-ttu-id="de9d5-147">Verbinding maken met container toohello.</span><span class="sxs-lookup"><span data-stu-id="de9d5-147">Connect toohello running container.</span></span>  <span data-ttu-id="de9d5-148">Open een webbrowser toohello geretourneerde IP-adres, bijvoorbeeld 'http://172.31.194.61' aan te wijzen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-148">Open a web browser pointing toohello IP address returned, for example "http://172.31.194.61".</span></span> <span data-ttu-id="de9d5-149">U ziet Hallo kop "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="de9d5-149">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="de9d5-150">in de browser Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="de9d5-150">display in hello browser.</span></span>

<span data-ttu-id="de9d5-151">toostop uw container, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="de9d5-151">toostop your container, run:</span></span>

```
docker stop my-web-site
```

<span data-ttu-id="de9d5-152">Hallo-container uit uw ontwikkelcomputer verwijderen:</span><span class="sxs-lookup"><span data-stu-id="de9d5-152">Delete hello container from your development machine:</span></span>

```
docker rm my-web-site
```

<a id="Push-Containers"></a>
## <a name="push-hello-image-toohello-container-registry"></a><span data-ttu-id="de9d5-153">Push Hallo installatiekopie toohello container register</span><span class="sxs-lookup"><span data-stu-id="de9d5-153">Push hello image toohello container registry</span></span>
<span data-ttu-id="de9d5-154">Nadat u hebt gecontroleerd dat die Hallo-container wordt uitgevoerd op uw ontwikkelcomputer, push-Hallo installatiekopie tooyour register in Azure Container register.</span><span class="sxs-lookup"><span data-stu-id="de9d5-154">After you verify that hello container runs on your development machine, push hello image tooyour registry in Azure Container Registry.</span></span>

<span data-ttu-id="de9d5-155">Voer ``docker login`` toolog in tooyour container register met uw [register referenties](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-155">Run ``docker login`` toolog in tooyour container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="de9d5-156">Hallo volgende voorbeeld wordt doorgegeven Hallo-ID en wachtwoord van een Azure Active Directory [service-principal](../active-directory/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-156">hello following example passes hello ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="de9d5-157">Bijvoorbeeld, u mogelijk hebt toegewezen een register van de service principal tooyour voor een scenario voor automatisering.</span><span class="sxs-lookup"><span data-stu-id="de9d5-157">For example, you might have assigned a service principal tooyour registry for an automation scenario.</span></span> <span data-ttu-id="de9d5-158">Of u kunt zich aanmelden met uw gebruikersnaam en wachtwoord van het register.</span><span class="sxs-lookup"><span data-stu-id="de9d5-158">Or, you could login using your registry username and password.</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="de9d5-159">Hallo volgende opdracht maakt u een label of alias van de afbeelding hello, met een volledig gekwalificeerde pad tooyour-register.</span><span class="sxs-lookup"><span data-stu-id="de9d5-159">hello following command creates a tag, or alias, of hello image, with a fully qualified path tooyour registry.</span></span> <span data-ttu-id="de9d5-160">In dit voorbeeld plaatsen Hallo-installatiekopie in Hallo ```samples``` naamruimte tooavoid vol in de hoofdmap Hallo van Hallo-register.</span><span class="sxs-lookup"><span data-stu-id="de9d5-160">This example places hello image in hello ```samples``` namespace tooavoid clutter in hello root of hello registry.</span></span>

```
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="de9d5-161">Push Hallo installatiekopie tooyour container register:</span><span class="sxs-lookup"><span data-stu-id="de9d5-161">Push hello image tooyour container registry:</span></span>

```
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="create-hello-containerized-service-in-visual-studio"></a><span data-ttu-id="de9d5-162">Hallo beperkte service in Visual Studio maken</span><span class="sxs-lookup"><span data-stu-id="de9d5-162">Create hello containerized service in Visual Studio</span></span>
<span data-ttu-id="de9d5-163">Hallo Service Fabric SDK en hulpprogramma's bieden een toohelp service-sjabloon maken van een beperkte toepassing.</span><span class="sxs-lookup"><span data-stu-id="de9d5-163">hello Service Fabric SDK and tools provide a service template toohelp you create a containerized application.</span></span>

1. <span data-ttu-id="de9d5-164">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="de9d5-164">Start Visual Studio.</span></span>  <span data-ttu-id="de9d5-165">Selecteer **Bestand** > **Nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-165">Select **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="de9d5-166">Selecteer **Service Fabric-toepassing**, geef deze de naam MyFirstContainer en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-166">Select **Service Fabric application**, name it "MyFirstContainer", and click **OK**.</span></span>
3. <span data-ttu-id="de9d5-167">Selecteer **Gast Container** uit Hallo lijst met **servicesjablonen**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-167">Select **Guest Container** from hello list of **service templates**.</span></span>
4. <span data-ttu-id="de9d5-168">In **Installatiekopienaam** 'myregistry.azurecr.io/samples/helloworldapp', Hallo installatiekopie gepusht van tooyour container opslagplaats invoeren.</span><span class="sxs-lookup"><span data-stu-id="de9d5-168">In **Image Name** enter "myregistry.azurecr.io/samples/helloworldapp", hello image you pushed tooyour container repository.</span></span>
5. <span data-ttu-id="de9d5-169">Geef de service een naam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-169">Give your service a name, and click **OK**.</span></span>

## <a name="configure-communication"></a><span data-ttu-id="de9d5-170">Communicatie configureren</span><span class="sxs-lookup"><span data-stu-id="de9d5-170">Configure communication</span></span>
<span data-ttu-id="de9d5-171">beperkte Hallo-service moet een eindpunt voor communicatie.</span><span class="sxs-lookup"><span data-stu-id="de9d5-171">hello containerized service needs an endpoint for communication.</span></span> <span data-ttu-id="de9d5-172">Voeg een `Endpoint` element met het Hallo-protocol en poort type toohello ServiceManifest.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="de9d5-172">Add an `Endpoint` element with hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="de9d5-173">Voor dit artikel luistert Hallo beperkte service op poort 8081.</span><span class="sxs-lookup"><span data-stu-id="de9d5-173">For this article, hello containerized service listens on port 8081.</span></span>  <span data-ttu-id="de9d5-174">In dit voorbeeld wordt een ingestelde poort 8081 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de9d5-174">In this example, a fixed port 8081 is used.</span></span>  <span data-ttu-id="de9d5-175">Als er geen poort is opgegeven, wordt een willekeurige poort van Hallo toepassingspoortbereik gekozen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-175">If no port is specified, a random port from hello application port range is chosen.</span></span>  

```xml
<Resources>
  <Endpoints>
    <Endpoint Name="Guest1TypeEndpoint" UriScheme="http" Port="8081" Protocol="http"/>
  </Endpoints>
</Resources>
```

<span data-ttu-id="de9d5-176">Als u een eindpunt, publiceert Service Fabric Hallo eindpunt toohello Naming service.</span><span class="sxs-lookup"><span data-stu-id="de9d5-176">By defining an endpoint, Service Fabric publishes hello endpoint toohello Naming service.</span></span>  <span data-ttu-id="de9d5-177">Deze container kunnen worden opgelost door andere services in Hallo cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-177">Other services running in hello cluster can resolve this container.</span></span>  <span data-ttu-id="de9d5-178">U kunt ook de container-container-communicatie met Hallo uitvoeren [omgekeerde proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-178">You can also perform container-to-container communication using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span>  <span data-ttu-id="de9d5-179">Communicatie wordt uitgevoerd door Hallo omgekeerde proxy HTTP-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt.</span><span class="sxs-lookup"><span data-stu-id="de9d5-179">Communication is performed by providing hello reverse proxy HTTP listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="de9d5-180">Omgevingsvariabelen configureren en instellen</span><span class="sxs-lookup"><span data-stu-id="de9d5-180">Configure and set environment variables</span></span>
<span data-ttu-id="de9d5-181">Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="de9d5-181">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="de9d5-182">Deze functie is beschikbaar voor alle services, ongeacht of ze zijn geïmplementeerd als containers, processen of uitvoerbare gastbestanden.</span><span class="sxs-lookup"><span data-stu-id="de9d5-182">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="de9d5-183">U kunt de omgevingsvariabele waarden in de toepassing hello manifest of geef ze tijdens de implementatie als toepassingsparameters overschrijven.</span><span class="sxs-lookup"><span data-stu-id="de9d5-183">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="de9d5-184">Hallo volgende service manifest XML-fragment toont een voorbeeld van hoe de omgevingsvariabelen toospecify voor een codepakket:</span><span class="sxs-lookup"><span data-stu-id="de9d5-184">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>
```xml
<CodePackage Name="Code" Version="1.0.0">
  ...
  <EnvironmentVariables>
    <EnvironmentVariable Name="HttpGatewayPort" Value=""/>    
  </EnvironmentVariables>
</CodePackage>
```

<span data-ttu-id="de9d5-185">Deze omgevingsvariabelen kunnen worden genegeerd in het toepassingsmanifest Hallo:</span><span class="sxs-lookup"><span data-stu-id="de9d5-185">These environment variables can be overridden in hello application manifest:</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
  </EnvironmentOverrides>
  ...
</ServiceManifestImport>
```

## <a name="configure-container-port-to-host-port-mapping-and-container-to-container-discovery"></a><span data-ttu-id="de9d5-186">Poort-naar-host-toewijzing voor containers en container-naar-container-detectie configureren</span><span class="sxs-lookup"><span data-stu-id="de9d5-186">Configure container port-to-host port mapping and container-to-container discovery</span></span>
<span data-ttu-id="de9d5-187">Configureer een toocommunicate host-poort die wordt gebruikt met Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="de9d5-187">Configure a host port used toocommunicate  with hello container.</span></span> <span data-ttu-id="de9d5-188">Hallo-poortbinding maps Hallo poort welke Hallo service binnen Hallo container tooa poort op Hallo host luistert.</span><span class="sxs-lookup"><span data-stu-id="de9d5-188">hello port binding maps hello port on which hello service is listening inside hello container tooa port on hello host.</span></span> <span data-ttu-id="de9d5-189">Voeg een `PortBinding` -element in `ContainerHostPolicies` element van Hallo ApplicationManifest.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="de9d5-189">Add a `PortBinding` element in `ContainerHostPolicies` element of hello ApplicationManifest.xml file.</span></span>  <span data-ttu-id="de9d5-190">Voor dit artikel `ContainerPort` 80 (Hallo container wordt poort 80, als de opgegeven in de Hallo Dockerfile) en `EndpointRef` is 'Guest1TypeEndpoint' (Hallo eindpunt dat eerder is gedefinieerd in Hallo servicemanifest).</span><span class="sxs-lookup"><span data-stu-id="de9d5-190">For this article, `ContainerPort` is 80 (hello container exposes port 80, as specified in hello Dockerfile) and `EndpointRef` is "Guest1TypeEndpoint" (hello endpoint previously defined in hello service manifest).</span></span>  <span data-ttu-id="de9d5-191">Inkomende aanvragen toohello-service op poort 8081 zijn toegewezen tooport 80 op Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="de9d5-191">Incoming requests toohello service on port 8081 are mapped tooport 80 on hello container.</span></span>

```xml
<Policies>
  <ContainerHostPolicies CodePackageRef="Code">
    <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
  </ContainerHostPolicies>
</Policies>
```

## <a name="configure-container-registry-authentication"></a><span data-ttu-id="de9d5-192">Verificatie containerregister configureren</span><span class="sxs-lookup"><span data-stu-id="de9d5-192">Configure container registry authentication</span></span>
<span data-ttu-id="de9d5-193">Container register verificatie configureren door toe te voegen `RepositoryCredentials` te`ContainerHostPolicies` van Hallo ApplicationManifest.xml bestand.</span><span class="sxs-lookup"><span data-stu-id="de9d5-193">Configure container registry authentication by adding `RepositoryCredentials` too`ContainerHostPolicies` of hello ApplicationManifest.xml file.</span></span> <span data-ttu-id="de9d5-194">Hallo-account en wachtwoord voor Hallo myregistry.azurecr.io container register, waardoor Hallo service toodownload Hallo container de installatiekopie van het Hallo-opslagplaats toevoegen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-194">Add hello account and password for hello myregistry.azurecr.io container registry, which allows hello service toodownload hello container image from hello repository.</span></span>

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="Guest1TypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

<span data-ttu-id="de9d5-195">Het is raadzaam dat u Hallo opslagplaats wachtwoord versleutelen met behulp van een certificaat uitwisselen die tooall knooppunten van het Hallo-cluster is geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-195">We recommend that you encrypt hello repository password by using an encipherment certificate that's deployed tooall nodes of hello cluster.</span></span> <span data-ttu-id="de9d5-196">Wanneer het Service Fabric Hallo service pakket toohello-cluster implementeert, is Hallo uitwisselen certificaat gebruikte toodecrypt Hallo gecodeerde tekst.</span><span class="sxs-lookup"><span data-stu-id="de9d5-196">When Service Fabric deploys hello service package toohello cluster, hello encipherment certificate is used toodecrypt hello cipher text.</span></span>  <span data-ttu-id="de9d5-197">Hallo Invoke ServiceFabricEncryptText cmdlet is gebruikte toocreate Hallo gecodeerde tekst hello wachtwoord toohello ApplicationManifest.xml bestand wordt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-197">hello Invoke-ServiceFabricEncryptText cmdlet is used toocreate hello cipher text for hello password, which is added toohello ApplicationManifest.xml file.</span></span>

<span data-ttu-id="de9d5-198">Hallo volgende script maakt een nieuw zelfondertekend certificaat en exporteert het tooa PFX-bestand.</span><span class="sxs-lookup"><span data-stu-id="de9d5-198">hello following script creates a new self-signed certificate and exports it tooa PFX file.</span></span>  <span data-ttu-id="de9d5-199">Hallo-certificaat wordt geïmporteerd in een bestaande sleutelkluis en vervolgens geïmplementeerd toohello Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="de9d5-199">hello certificate is imported into an existing key vault and then deployed toohello Service Fabric cluster.</span></span>

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
<span data-ttu-id="de9d5-200">Hallo-wachtwoord met behulp van Hallo versleutelen [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="de9d5-200">Encrypt hello password using hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet.</span></span>

```powershell
$text = "=P==/==/=8=/=+u4lyOB=+=nWzEeRfF="
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint $cer.Thumbprint -Text $text -StoreLocation Local -StoreName My
```

<span data-ttu-id="de9d5-201">Vervang Hallo wachtwoord door Hallo gecodeerde tekst die wordt geretourneerd door Hallo [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet en stel `PasswordEncrypted` te 'true'.</span><span class="sxs-lookup"><span data-stu-id="de9d5-201">Replace hello password with hello cipher text returned by hello [Invoke-ServiceFabricEncryptText](/powershell/module/servicefabric/Invoke-ServiceFabricEncryptText?view=azureservicefabricps) cmdlet and set `PasswordEncrypted` too"true".</span></span>

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

## <a name="configure-isolation-mode"></a><span data-ttu-id="de9d5-202">Isolatiemodus configureren</span><span class="sxs-lookup"><span data-stu-id="de9d5-202">Configure isolation mode</span></span>
<span data-ttu-id="de9d5-203">Windows ondersteunt twee isolatiemodi voor containers: proces en Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="de9d5-203">Windows supports two isolation modes for containers: process and Hyper-V.</span></span> <span data-ttu-id="de9d5-204">Met isolatiemodus voor Hallo Hallo alle Hallo containers die worden uitgevoerd op dezelfde host machine share Hallo kernel met Hallo host.</span><span class="sxs-lookup"><span data-stu-id="de9d5-204">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="de9d5-205">Hallo kernels zijn met de isolatiemodus Hallo Hyper-V, tussen elke Hyper-V-container en Hallo containerhost geïsoleerd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-205">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="de9d5-206">Hallo isolatiemodus is opgegeven in Hallo `ContainerHostPolicies` -element in het manifestbestand van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="de9d5-206">hello isolation mode is specified in hello `ContainerHostPolicies` element in hello application manifest file.</span></span> <span data-ttu-id="de9d5-207">Hallo isolatie modi die kunnen worden opgegeven `process`, `hyperv`, en `default`.</span><span class="sxs-lookup"><span data-stu-id="de9d5-207">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="de9d5-208">Hallo standaardisolatiemodus standaardwaarden te`process` op Windows-Server fungeert als host en de standaardinstellingen te`hyperv` op hosts met Windows 10.</span><span class="sxs-lookup"><span data-stu-id="de9d5-208">hello default isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span> <span data-ttu-id="de9d5-209">Hallo volgende fragment toont hoe Hallo isolatiemodus is opgegeven in het manifestbestand van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="de9d5-209">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
<ContainerHostPolicies CodePackageRef="Code" Isolation="hyperv">
```

## <a name="configure-resource-governance"></a><span data-ttu-id="de9d5-210">Resourcebeheer configureren</span><span class="sxs-lookup"><span data-stu-id="de9d5-210">Configure resource governance</span></span>
<span data-ttu-id="de9d5-211">[Resource governance](service-fabric-resource-governance.md) beperkt Hallo resources die container Hallo op Hallo host kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de9d5-211">[Resource governance](service-fabric-resource-governance.md) restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="de9d5-212">Hallo `ResourceGovernancePolicy` element, dat is opgegeven in het toepassingsmanifest hello, gebruikte toodeclare limieten voor een service-codepakket is.</span><span class="sxs-lookup"><span data-stu-id="de9d5-212">hello `ResourceGovernancePolicy` element, which is specified in hello application manifest, is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="de9d5-213">Limieten kunnen worden ingesteld voor Hallo volgende resources: geheugen, MemorySwap, CpuShares (CPU relatieve gewicht), MemoryReservationInMB, BlkioWeight (BlockIO relatieve gewicht).</span><span class="sxs-lookup"><span data-stu-id="de9d5-213">Resource limits can be set for hello following resources: Memory, MemorySwap, CpuShares (CPU relative weight), MemoryReservationInMB, BlkioWeight (BlockIO relative weight).</span></span>  <span data-ttu-id="de9d5-214">In dit voorbeeld servicepakket Guest1Pkg één kern opgehaald op Hallo clusterknooppunten waar het wordt geplaatst.</span><span class="sxs-lookup"><span data-stu-id="de9d5-214">In this example, service package Guest1Pkg gets one core on hello cluster nodes where it is placed.</span></span>  <span data-ttu-id="de9d5-215">Geheugenlimieten absoluut zijn dus Hallo codepakket beperkt too1024 is MB aan geheugen (en een voorlopig garantie reservering van dezelfde Hallo).</span><span class="sxs-lookup"><span data-stu-id="de9d5-215">Memory limits are absolute, so hello code package is limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="de9d5-216">Code-pakketten (containers of processen) zijn niet kunnen tooallocate meer geheugen dan deze limiet en probeert toodo dus in een out-geheugen-uitzondering resulteert.</span><span class="sxs-lookup"><span data-stu-id="de9d5-216">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="de9d5-217">Voor de resource limiet afdwinging toowork hebben alle code pakketten binnen een servicepakket geheugenlimieten opgegeven.</span><span class="sxs-lookup"><span data-stu-id="de9d5-217">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="Guest1Pkg" ServiceManifestVersion="1.0.0" />
  <Policies>
    <ServicePackageResourceGovernancePolicy CpuCores="1"/>
    <ResourceGovernancePolicy CodePackageRef="Code" MemoryInMB="1024"  />
  </Policies>
</ServiceManifestImport>
```

## <a name="deploy-hello-container-application"></a><span data-ttu-id="de9d5-218">Hallo containertoepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="de9d5-218">Deploy hello container application</span></span>
<span data-ttu-id="de9d5-219">Al uw wijzigingen opslaan en Hallo toepassing bouwen.</span><span class="sxs-lookup"><span data-stu-id="de9d5-219">Save all your changes and build hello application.</span></span> <span data-ttu-id="de9d5-220">toopublish uw toepassing, met de rechtermuisknop op **MyFirstContainer** in Solution Explorer en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-220">toopublish your application, right-click on **MyFirstContainer** in Solution Explorer and select **Publish**.</span></span>

<span data-ttu-id="de9d5-221">In **verbindingseindpunt**, Voer Hallo eindpunt voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="de9d5-221">In **Connection Endpoint**, enter hello management endpoint for hello cluster.</span></span>  <span data-ttu-id="de9d5-222">Bijvoorbeeld: 'containercluster.westus2.cloudapp.azure.com:19000'.</span><span class="sxs-lookup"><span data-stu-id="de9d5-222">For example, "containercluster.westus2.cloudapp.azure.com:19000".</span></span> <span data-ttu-id="de9d5-223">U vindt de clientverbinding Hallo eindpunt in Hallo overzichtsblade voor uw cluster in Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="de9d5-223">You can find hello client connection endpoint in hello Overview blade for your cluster in hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="de9d5-224">Klik op **Publish**.</span><span class="sxs-lookup"><span data-stu-id="de9d5-224">Click **Publish**.</span></span>

<span data-ttu-id="de9d5-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is een webhulpprogramma voor het inspecteren en beheren van toepassingen en knooppunten in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="de9d5-225">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a web-based tool for inspecting and managing applications and nodes in a Service Fabric cluster.</span></span> <span data-ttu-id="de9d5-226">Open een browser en ga toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/en volgt u de implementatie van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="de9d5-226">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:19080/Explorer/ and follow hello application deployment.</span></span>  <span data-ttu-id="de9d5-227">Hallo-toepassing wordt geïmplementeerd maar bevindt zich in een foutstatus totdat Hallo installatiekopie gedownload op de clusterknooppunten hello (dit kunnen enige tijd duren, afhankelijk van de grootte van de installatiekopie Hallo): ![fout][1]</span><span class="sxs-lookup"><span data-stu-id="de9d5-227">hello application deploys but is in an error state until hello image is downloaded on hello cluster nodes (which can take some time, depending on hello image size): ![Error][1]</span></span>

<span data-ttu-id="de9d5-228">Hallo toepassing gereed is wanneer deze ```Ready``` status: ![gereed][2]</span><span class="sxs-lookup"><span data-stu-id="de9d5-228">hello application is ready when it's in ```Ready``` state: ![Ready][2]</span></span>

<span data-ttu-id="de9d5-229">Open een browser en ga toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span><span class="sxs-lookup"><span data-stu-id="de9d5-229">Open a browser and navigate toohttp://containercluster.westus2.cloudapp.azure.com:8081.</span></span> <span data-ttu-id="de9d5-230">U ziet Hallo kop "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="de9d5-230">You should see hello heading "Hello World!"</span></span> <span data-ttu-id="de9d5-231">in de browser Hallo weergeven.</span><span class="sxs-lookup"><span data-stu-id="de9d5-231">display in hello browser.</span></span>

## <a name="clean-up"></a><span data-ttu-id="de9d5-232">Opruimen</span><span class="sxs-lookup"><span data-stu-id="de9d5-232">Clean up</span></span>
<span data-ttu-id="de9d5-233">U tooincur kosten doorgaan terwijl Hallo cluster wordt uitgevoerd, kunt u [verwijderen van uw cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span><span class="sxs-lookup"><span data-stu-id="de9d5-233">You continue tooincur charges while hello cluster is running, consider [deleting your cluster](service-fabric-get-started-azure-cluster.md#remove-the-cluster).</span></span>  <span data-ttu-id="de9d5-234">[Party-clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) worden na een paar uur automatisch verwijderd.</span><span class="sxs-lookup"><span data-stu-id="de9d5-234">[Party clusters](http://tryazureservicefabric.westus.cloudapp.azure.com/) are automatically deleted after a few hours.</span></span>

<span data-ttu-id="de9d5-235">Wanneer u push-Hallo installatiekopie toohello container register kunt u Hallo-afbeelding voor lokaal verwijderen vanaf de ontwikkelcomputer:</span><span class="sxs-lookup"><span data-stu-id="de9d5-235">After you push hello image toohello container registry you can delete hello local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="de9d5-236">Volledig voorbeeld van de manifesten voor de Fabric Service-toepassing en -service</span><span class="sxs-lookup"><span data-stu-id="de9d5-236">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="de9d5-237">Hier volgen Hallo volledige service en Toepassingsmanifesten in dit artikel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="de9d5-237">Here are hello complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="de9d5-238">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="de9d5-238">ServiceManifest.xml</span></span>
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
### <a name="applicationmanifestxml"></a><span data-ttu-id="de9d5-239">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="de9d5-239">ApplicationManifest.xml</span></span>
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

## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="de9d5-240">Tijdsinterval configureren voor geforceerd beëindigen van container</span><span class="sxs-lookup"><span data-stu-id="de9d5-240">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="de9d5-241">U kunt een tijdsinterval voor Hallo runtime toowait configureren voordat Hallo container wordt verwijderd nadat hello service verwijderen (of een knooppunt van de tooanother verplaatsen) is gestart.</span><span class="sxs-lookup"><span data-stu-id="de9d5-241">You can configure a time interval for hello runtime toowait before hello container is removed after hello service deletion (or a move tooanother node) has started.</span></span> <span data-ttu-id="de9d5-242">Configureren Hallo tijdsinterval verzendt Hallo `docker stop <time in seconds>` opdracht toohello container.</span><span class="sxs-lookup"><span data-stu-id="de9d5-242">Configuring hello time interval sends hello `docker stop <time in seconds>` command toohello container.</span></span>   <span data-ttu-id="de9d5-243">Zie [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="de9d5-243">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="de9d5-244">Hallo tijd interval toowait is opgegeven bij Hallo `Hosting` sectie.</span><span class="sxs-lookup"><span data-stu-id="de9d5-244">hello time interval toowait is specified under hello `Hosting` section.</span></span> <span data-ttu-id="de9d5-245">Hallo na cluster manifest codefragment ziet u hoe tooset Hallo Wacht-interval:</span><span class="sxs-lookup"><span data-stu-id="de9d5-245">hello following cluster manifest snippet shows how tooset hello wait interval:</span></span>

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
<span data-ttu-id="de9d5-246">Hallo standaardtijdsinterval is ingesteld too10 seconden.</span><span class="sxs-lookup"><span data-stu-id="de9d5-246">hello default time interval is set too10 seconds.</span></span> <span data-ttu-id="de9d5-247">Omdat deze configuratie dynamisch is, wordt een config alleen bijwerken op Hallo cluster updates Hallo time-out.</span><span class="sxs-lookup"><span data-stu-id="de9d5-247">Since this configuration is dynamic, a config only upgrade on hello cluster updates hello timeout.</span></span> 


## <a name="configure-hello-runtime-tooremove-unused-container-images"></a><span data-ttu-id="de9d5-248">Hallo runtime tooremove configureren ongebruikte container installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="de9d5-248">Configure hello runtime tooremove unused container images</span></span>

<span data-ttu-id="de9d5-249">U kunt configureren Hallo Service Fabric-cluster tooremove ongebruikte container installatiekopieën van het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="de9d5-249">You can configure hello Service Fabric cluster tooremove unused container images from hello node.</span></span> <span data-ttu-id="de9d5-250">Deze configuratie kunt schijfruimte toobe opnieuw vastgelegd als te veel container afbeeldingen op Hallo knooppunt aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="de9d5-250">This configuration allows disk space toobe recaptured if too many container images are present on hello node.</span></span>  <span data-ttu-id="de9d5-251">tooenable deze functie, de update Hallo `Hosting` sectie in het clustermanifest hello, zoals wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="de9d5-251">tooenable this feature, update hello `Hosting` section in hello cluster manifest as shown in hello following snippet:</span></span> 


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

<span data-ttu-id="de9d5-252">Voor installatiekopieën die niet worden verwijderd, kunt u ze onder Hallo `ContainerImagesToSkip` parameter.</span><span class="sxs-lookup"><span data-stu-id="de9d5-252">For images that should not be deleted, you can specify them under hello `ContainerImagesToSkip` parameter.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="de9d5-253">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de9d5-253">Next steps</span></span>
* <span data-ttu-id="de9d5-254">Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-254">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="de9d5-255">Lees Hallo [implementeren van een .NET-toepassing in een container](service-fabric-host-app-in-a-container.md) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="de9d5-255">Read hello [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="de9d5-256">Meer informatie over Service Fabric Hallo [toepassing levenscyclus](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="de9d5-256">Learn about hello Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="de9d5-257">Afhandeling Hallo [codevoorbeelden Service Fabric-container](https://github.com/Azure-Samples/service-fabric-dotnet-containers) op GitHub.</span><span class="sxs-lookup"><span data-stu-id="de9d5-257">Checkout hello [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[1]: ./media/service-fabric-get-started-containers/MyFirstContainerError.png
[2]: ./media/service-fabric-get-started-containers/MyFirstContainerReady.png
