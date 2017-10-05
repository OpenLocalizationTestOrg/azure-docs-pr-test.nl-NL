---
title: Een Azure Service Fabric-containertoepassing maken in Linux | Microsoft Docs
description: Maak uw eerste Linux-containertoepassing in Azure Service Fabric.  Bouw een Docker-installatiekopie met uw toepassing, push de installatiekopie naar een containerregister, en bouw en implementeer een Service Fabric-containertoepassing.
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
ms.openlocfilehash: 8355478cb2fff3a63bc4a9b359ec8e2b132c80f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-your-first-service-fabric-container-application-on-linux"></a><span data-ttu-id="0e3ad-104">Uw eerste Service Fabric-containertoepassing maken in Linux</span><span class="sxs-lookup"><span data-stu-id="0e3ad-104">Create your first Service Fabric container application on Linux</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e3ad-105">Windows</span><span class="sxs-lookup"><span data-stu-id="0e3ad-105">Windows</span></span>](service-fabric-get-started-containers.md)
> * [<span data-ttu-id="0e3ad-106">Linux</span><span class="sxs-lookup"><span data-stu-id="0e3ad-106">Linux</span></span>](service-fabric-get-started-containers-linux.md)

<span data-ttu-id="0e3ad-107">Er zijn geen wijzigingen in uw toepassing vereist om een bestaande toepassing in een Linux-container uit te voeren in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-107">Running an existing application in a Linux container on a Service Fabric cluster doesn't require any changes to your application.</span></span> <span data-ttu-id="0e3ad-108">Dit artikel helpt u bij het maken van een Docker-installatiekopie met een Python [Flask](http://flask.pocoo.org/)-webtoepassing en het implementeren ervan in een Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-108">This article walks you through creating a Docker image containing a Python [Flask](http://flask.pocoo.org/) web application and deploying it to a Service Fabric cluster.</span></span>  <span data-ttu-id="0e3ad-109">U gaat uw containertoepassing ook delen via [Azure Container Registry](/azure/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-109">You will also share your containerized application through [Azure Container Registry](/azure/container-registry/).</span></span>  <span data-ttu-id="0e3ad-110">In dit artikel wordt ervan uitgegaan dat u de basisbeginselen kent van Docker.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-110">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="0e3ad-111">Meer informatie over Docker kunt u lezen in het [Docker-overzicht](https://docs.docker.com/engine/understanding-docker/).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-111">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e3ad-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0e3ad-112">Prerequisites</span></span>
* <span data-ttu-id="0e3ad-113">Een ontwikkelcomputer waarop wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-113">A development computer running:</span></span>
  * <span data-ttu-id="0e3ad-114">[Service Fabric SDK en hulpprogramma's](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-114">[Service Fabric SDK and tools](service-fabric-get-started-linux.md).</span></span>
  * <span data-ttu-id="0e3ad-115">[Docker CE voor Linux](https://docs.docker.com/engine/installation/#prior-releases).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-115">[Docker CE for Linux](https://docs.docker.com/engine/installation/#prior-releases).</span></span> 
  * [<span data-ttu-id="0e3ad-116">Service Fabric-CLI</span><span class="sxs-lookup"><span data-stu-id="0e3ad-116">Service Fabric CLI</span></span>](service-fabric-cli.md)

* <span data-ttu-id="0e3ad-117">Een register in Azure Container Registry - [Een containerregister maken](../container-registry/container-registry-get-started-portal.md) in uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-117">A registry in Azure Container Registry - [Create a container registry](../container-registry/container-registry-get-started-portal.md) in your Azure subscription.</span></span> 

## <a name="define-the-docker-container"></a><span data-ttu-id="0e3ad-118">De Docker-container definiëren</span><span class="sxs-lookup"><span data-stu-id="0e3ad-118">Define the Docker container</span></span>
<span data-ttu-id="0e3ad-119">Bouw een installatiekopie op basis van de [Python-installatiekopie](https://hub.docker.com/_/python/) die zich in de Docker-hub bevindt.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-119">Build an image based on the [Python image](https://hub.docker.com/_/python/) located on Docker Hub.</span></span> 

<span data-ttu-id="0e3ad-120">Definieer uw Docker-container in een Dockerfile.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-120">Define your Docker container in a Dockerfile.</span></span> <span data-ttu-id="0e3ad-121">Het bestand Dockerfile bevat instructies voor het instellen van de omgeving in de container, het laden van de toepassing die u wilt uitvoeren en het toewijzen van poorten.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-121">The Dockerfile contains instructions for setting up the environment inside your container, loading the application you want to run, and mapping ports.</span></span> <span data-ttu-id="0e3ad-122">Het Dockerfile is de invoer van de opdracht `docker build` waarmee de installatiekopie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-122">The Dockerfile is the input to the `docker build` command, which creates the image.</span></span> 

<span data-ttu-id="0e3ad-123">Maak een lege map en maak het bestand *Dockerfile* (zonder extensie).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-123">Create an empty directory and create the file *Dockerfile* (with no file extension).</span></span> <span data-ttu-id="0e3ad-124">Voeg het volgende toe aan het bestand *Dockerfile* en sla de wijzigingen op:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-124">Add the following to *Dockerfile* and save your changes:</span></span>

```
# Use an official Python runtime as a base image
FROM python:2.7-slim

# Set the working directory to /app
WORKDIR /app

# Copy the current directory contents into the container at /app
ADD . /app

# Install any needed packages specified in requirements.txt
RUN pip install -r requirements.txt

# Make port 80 available outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

<span data-ttu-id="0e3ad-125">Lees het [Dockerfile-referentiemateriaal](https://docs.docker.com/engine/reference/builder/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-125">Read the [Dockerfile reference](https://docs.docker.com/engine/reference/builder/) for more information.</span></span>

## <a name="create-a-simple-web-application"></a><span data-ttu-id="0e3ad-126">Een eenvoudige webtoepassing maken</span><span class="sxs-lookup"><span data-stu-id="0e3ad-126">Create a simple web application</span></span>
<span data-ttu-id="0e3ad-127">Maak een Flask-toepassing die luistert op poort 80 en 'Hallo Wereld!' retourneert.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-127">Create a Flask web application listening on port 80 that returns "Hello World!".</span></span>  <span data-ttu-id="0e3ad-128">Maak in dezelfde map het bestand *requirements.txt*.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-128">In the same directory, create the file *requirements.txt*.</span></span>  <span data-ttu-id="0e3ad-129">Voeg het volgende toe en sla de wijzigingen op:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-129">Add the following and save your changes:</span></span>
```
Flask
```

<span data-ttu-id="0e3ad-130">Maak ook het bestand *app.py* en voeg het volgende toe:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-130">Also create the *app.py* file and add the following:</span></span>

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def hello():
    
    return 'Hello World!'

if __name__ == "__main__":
    app.run(host='0.0.0.0', port=80)
```

## <a name="build-the-image"></a><span data-ttu-id="0e3ad-131">De installatiekopie bouwen</span><span class="sxs-lookup"><span data-stu-id="0e3ad-131">Build the image</span></span>
<span data-ttu-id="0e3ad-132">Voer de opdracht `docker build` uit om de installatiekopie te maken waarmee de webtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-132">Run the `docker build` command to create the image that runs your web application.</span></span> <span data-ttu-id="0e3ad-133">Open een PowerShell-venster en ga naar *c:\temp\helloworldapp*.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-133">Open a PowerShell window and navigate to *c:\temp\helloworldapp*.</span></span> <span data-ttu-id="0e3ad-134">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-134">Run the following command:</span></span>

```bash
docker build -t helloworldapp .
```

<span data-ttu-id="0e3ad-135">Met deze opdracht wordt de nieuwe installatiekopie gebouwd met behulp van de instructies in het Dockerfile, en krijgt de installatiekopie de naam (-t tagging) \`hallowereldapp´.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-135">This command builds the new image using the instructions in your Dockerfile, naming (-t tagging) the image "helloworldapp".</span></span> <span data-ttu-id="0e3ad-136">Bij het bouwen van een installatiekopie wordt de basisinstallatiekopie uit de Docker-hub gehaald en wordt er een nieuwe installatiekopie gemaakt waarmee de toepassing wordt toegevoegd boven op de basisinstallatiekopie.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-136">Building an image pulls the base image down from Docker Hub and creates a new image that adds your application on top of the base image.</span></span>  

<span data-ttu-id="0e3ad-137">Nadat de buildopdracht is voltooid, voert u de opdracht `docker images` uit om de gegevens van de nieuwe installatiekopie te bekijken:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-137">Once the build command completes, run the `docker images` command to see information on the new image:</span></span>

```bash
$ docker images
    
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
helloworldapp                 latest              86838648aab6        2 minutes ago       194 MB
```

## <a name="run-the-application-locally"></a><span data-ttu-id="0e3ad-138">De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0e3ad-138">Run the application locally</span></span>
<span data-ttu-id="0e3ad-139">Controleer of de containertoepassing lokaal wordt uitgevoerd voordat u deze naar het containerregister pusht.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-139">Verify that your containerized application runs locally before pushing it the container registry.</span></span>  

<span data-ttu-id="0e3ad-140">Voer de toepassing uit en wijs poort 4000 van uw computer toe aan de door de container beschikbaar gestelde poort 80:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-140">Run the application, mapping your computer's port 4000 to the container's exposed port 80:</span></span>

```bash
docker run -d -p 4000:80 --name my-web-site helloworldapp
```

<span data-ttu-id="0e3ad-141">Bij *naam* kunt de actieve container een naam geven (in plaats van de container-id).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-141">*name* gives a name to the running container (instead of the container ID).</span></span>

<span data-ttu-id="0e3ad-142">Maak verbinding met de actieve container.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-142">Connect to the running container.</span></span>  <span data-ttu-id="0e3ad-143">Open een webbrowser en verwijs naar het IP-adres dat is geretourneerd op poort 4000, bijvoorbeeld http://localhost:4000.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-143">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="0e3ad-144">Als het goed is, ziet u de koptekst Hallo wereld!</span><span class="sxs-lookup"><span data-stu-id="0e3ad-144">You should see the heading "Hello World!"</span></span> <span data-ttu-id="0e3ad-145">weergegeven in de browser.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-145">display in the browser.</span></span>

![Hallo wereld!][hello-world]

<span data-ttu-id="0e3ad-147">Als u de container wilt stoppen, voert u dit uit:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-147">To stop your container, run:</span></span>

```bash
docker stop my-web-site
```

<span data-ttu-id="0e3ad-148">De container verwijderen van de ontwikkelcomputer:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-148">Delete the container from your development machine:</span></span>

```bash
docker rm my-web-site
```

## <a name="push-the-image-to-the-container-registry"></a><span data-ttu-id="0e3ad-149">De installatiekopie naar het containerregister pushen</span><span class="sxs-lookup"><span data-stu-id="0e3ad-149">Push the image to the container registry</span></span>
<span data-ttu-id="0e3ad-150">Nadat u hebt gecontroleerd of de toepassing wordt uitgevoerd in Docker, pusht u de installatiekopie naar het register in Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-150">After you verify that the application runs in Docker, push the image to your registry in Azure Container Registry.</span></span>

<span data-ttu-id="0e3ad-151">Voer `docker login` uit om u bij uw containerregister aan te melden met uw [registerreferenties](../container-registry/container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-151">Run `docker login` to log in to your container registry with your [registry credentials](../container-registry/container-registry-authentication.md).</span></span>

<span data-ttu-id="0e3ad-152">In het volgende voorbeeld worden de id en het wachtwoord van een [service-principal](../active-directory/active-directory-application-objects.md) van Azure Active Directory doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-152">The following example passes the ID and password of an Azure Active Directory [service principal](../active-directory/active-directory-application-objects.md).</span></span> <span data-ttu-id="0e3ad-153">U hebt bijvoorbeeld een service-principal aan uw register toegewezen voor een automatiseringsscenario.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-153">For example, you might have assigned a service principal to your registry for an automation scenario.</span></span>  <span data-ttu-id="0e3ad-154">Of u kunt zich aanmelden met uw gebruikersnaam en wachtwoord van het register.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-154">Or, you could login using your registry username and password.</span></span>

```bash
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="0e3ad-155">Met de volgende opdracht maakt u een tag (of alias) van de installatiekopie met een volledig gekwalificeerd pad naar uw register.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-155">The following command creates a tag, or alias, of the image, with a fully qualified path to your registry.</span></span> <span data-ttu-id="0e3ad-156">In dit voorbeeld wordt de installatiekopie in de naamruimte `samples` geplaatst om overbodige items in de hoofdmap van het register te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-156">This example places the image in the `samples` namespace to avoid clutter in the root of the registry.</span></span>

```bash
docker tag helloworldapp myregistry.azurecr.io/samples/helloworldapp
```

<span data-ttu-id="0e3ad-157">De installatiekopie naar het containerregister pushen:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-157">Push the image to your container registry:</span></span>

```bash
docker push myregistry.azurecr.io/samples/helloworldapp
```

## <a name="package-the-docker-image-with-yeoman"></a><span data-ttu-id="0e3ad-158">De Docker-installatiekopie inpakken met Yeoman</span><span class="sxs-lookup"><span data-stu-id="0e3ad-158">Package the Docker image with Yeoman</span></span>
<span data-ttu-id="0e3ad-159">De Service Fabric-SDK voor Linux bevat een [Yeoman](http://yeoman.io/)-generator waarmee u gemakkelijk uw eerste toepassing kunt maken en een containerinstallatiekopie kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-159">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="0e3ad-160">We gebruiken Yeoman om een toepassing te maken met een enkele Docker-container genaamd *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-160">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span>

<span data-ttu-id="0e3ad-161">Om een Service Fabric-containertoepassing te maken, opent u een terminalvenster en voert u `yo azuresfcontainer` uit.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-161">To create a Service Fabric container application, open a terminal window and run `yo azuresfcontainer`.</span></span>  

<span data-ttu-id="0e3ad-162">Naam van uw toepassing (bijvoorbeeld 'mycontainer').</span><span class="sxs-lookup"><span data-stu-id="0e3ad-162">Name your application (for example, "mycontainer").</span></span> 

<span data-ttu-id="0e3ad-163">Geef de URL op voor de containerinstallatiekopie in een containerregister (bijvoorbeeld '').</span><span class="sxs-lookup"><span data-stu-id="0e3ad-163">Provide the URL for the container image in a container registry (for example, "").</span></span> 

<span data-ttu-id="0e3ad-164">Voor deze installatiekopie is een invoerpunt voor werkbelasting gedefinieerd, dus moet u expliciet invoeropdrachten opgeven (opdrachten worden uitgevoerd in de container, zodat de container na het opstarten actief blijft).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-164">This image has a workload entry-point defined, so need to explicitly specify input commands (commands run inside the container, which will keep the container running after startup).</span></span> 

<span data-ttu-id="0e3ad-165">Geef '1' exemplaar op.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-165">Specify an instance count of "1".</span></span>

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="configure-port-mapping-and-container-repository-authentication"></a><span data-ttu-id="0e3ad-167">Poorttoewijzing en containeropslagplaatsverificatie configureren</span><span class="sxs-lookup"><span data-stu-id="0e3ad-167">Configure port mapping and container repository authentication</span></span>
<span data-ttu-id="0e3ad-168">Uw containerservice heeft een eindpunt voor communicatie nodig.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-168">Your containerized service needs an endpoint for communication.</span></span>  <span data-ttu-id="0e3ad-169">Voeg nu het protocol en de poort toe en typ naar een `Endpoint` in het bestand ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-169">Now add the protocol, port, and type to an `Endpoint` in the ServiceManifest.xml file.</span></span> <span data-ttu-id="0e3ad-170">Voor deze snelstartgids luistert de containerservice naar poort 4000:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-170">For this article, the containerized service listens on port 4000:</span></span> 

```xml
<Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
```
<span data-ttu-id="0e3ad-171">Door `UriScheme` op te geven wordt het eindpunt van de container automatisch geregistreerd bij de Service Fabric Naming-service voor meer zichtbaarheid.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-171">Providing the `UriScheme` automatically registers the container endpoint with the Service Fabric Naming service for discoverability.</span></span> <span data-ttu-id="0e3ad-172">Een volledig voorbeeld van een ServiceManifest.xml-bestand vindt u aan het einde van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-172">A full ServiceManifest.xml example file is provided at the end of this article.</span></span> 

<span data-ttu-id="0e3ad-173">Configureer de poorttoewijzing poort-naar-host voor de container door een `PortBinding`-beleid op te geven in `ContainerHostPolicies` van het bestand ApplicationManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-173">Configure the container port-to-host port mapping by specifying a `PortBinding` policy in `ContainerHostPolicies` of the ApplicationManifest.xml file.</span></span>  <span data-ttu-id="0e3ad-174">Voor dit artikel geldt: `ContainerPort` is 80 (de container gebruikt poort 80, zoals opgegeven in het Dockerfile) en `EndpointRef` is myserviceTypeEndpoint (het eindpunt dat is gedefinieerd in het servicemanifest).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-174">For this article, `ContainerPort` is 80 (the container exposes port 80, as specified in the Dockerfile) and `EndpointRef` is "myserviceTypeEndpoint" (the endpoint defined in the service manifest).</span></span>  <span data-ttu-id="0e3ad-175">Binnenkomende aanvragen naar de service op poort 4000 worden toegewezen aan poort 80 op de container.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-175">Incoming requests to the service on port 4000 are mapped to port 80 on the container.</span></span>  <span data-ttu-id="0e3ad-176">Als de container moet verifiëren bij een persoonlijke privéopslagplaats, voegt u `RepositoryCredentials` toe.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-176">If your container needs to authenticate with a private repository, then add `RepositoryCredentials`.</span></span>  <span data-ttu-id="0e3ad-177">Voeg voor dit artikel de accountnaam en het wachtwoord in voor het containerregister myregistry.azurecr.io.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-177">For this article, add the account name and password for the myregistry.azurecr.io container registry.</span></span> 

```xml
<Policies>
    <ContainerHostPolicies CodePackageRef="Code">
        <RepositoryCredentials AccountName="myregistry" Password="=P==/==/=8=/=+u4lyOB=+=nWzEeRfF=" PasswordEncrypted="false"/>
        <PortBinding ContainerPort="80" EndpointRef="myserviceTypeEndpoint"/>
    </ContainerHostPolicies>
</Policies>
```

## <a name="build-and-package-the-service-fabric-application"></a><span data-ttu-id="0e3ad-178">De Service Fabric-toepassing bouwen en inpakken</span><span class="sxs-lookup"><span data-stu-id="0e3ad-178">Build and package the Service Fabric application</span></span>
<span data-ttu-id="0e3ad-179">De Service Fabric Yeoman-sjablonen bevatten een bouwscript voor [Gradle](https://gradle.org/), dat u kunt gebruiken om de toepassing via de terminal te maken.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-179">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span> <span data-ttu-id="0e3ad-180">Ga als volgt te werk om de toepassing te maken en in te pakken:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-180">To build and package the application, run the following:</span></span>

```bash
cd mycontainer
gradle
```

## <a name="deploy-the-application"></a><span data-ttu-id="0e3ad-181">De toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="0e3ad-181">Deploy the application</span></span>
<span data-ttu-id="0e3ad-182">Als de toepassing is gemaakt, kunt u deze met behulp van de Service Fabric-CLI implementeren in het lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-182">Once the application is built, you can deploy it to the local cluster using the Service Fabric CLI.</span></span>

<span data-ttu-id="0e3ad-183">Maak verbinding met het lokale cluster van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-183">Connect to the local Service Fabric cluster.</span></span>

```bash
sfctl cluster select --endpoint http://localhost:19080
```

<span data-ttu-id="0e3ad-184">Gebruik het installatiescript dat is opgegeven in de sjabloon om het toepassingspakket te kopiëren naar de installatiekopieopslag van het cluster, het toepassingstype te registreren en een exemplaar van de toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-184">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

```bash
./install.sh
```

<span data-ttu-id="0e3ad-185">Open een browser en navigeer naar de Service Fabric Explorer op http://localhost:19080/Explorer (vervang localhost door het privé IP-adres van de virtuele machine als u Vagrant in Mac OS X gebruikt).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-185">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span> <span data-ttu-id="0e3ad-186">Vouw het knooppunt Toepassingen uit. U ziet dat er nu een vermelding is voor uw toepassingstype en nog een voor het eerste exemplaar van dat type.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-186">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

<span data-ttu-id="0e3ad-187">Maak verbinding met de actieve container.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-187">Connect to the running container.</span></span>  <span data-ttu-id="0e3ad-188">Open een webbrowser en verwijs naar het IP-adres dat is geretourneerd op poort 4000, bijvoorbeeld http://localhost:4000.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-188">Open a web browser pointing to the IP address returned on port 4000, for example "http://localhost:4000".</span></span> <span data-ttu-id="0e3ad-189">Als het goed is, ziet u de koptekst Hallo wereld!</span><span class="sxs-lookup"><span data-stu-id="0e3ad-189">You should see the heading "Hello World!"</span></span> <span data-ttu-id="0e3ad-190">weergegeven in de browser.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-190">display in the browser.</span></span>

![Hallo wereld!][hello-world]

## <a name="clean-up"></a><span data-ttu-id="0e3ad-192">Opruimen</span><span class="sxs-lookup"><span data-stu-id="0e3ad-192">Clean up</span></span>
<span data-ttu-id="0e3ad-193">Gebruik het uninstall-script dat is opgegeven in de sjabloon om het toepassingsexemplaar te verwijderen uit het lokale ontwikkelomgevingscluster en de registratie van het toepassingstype op te heffen.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-193">Use the uninstall script provided in the template to delete the application instance from the local development cluster and unregister the application type.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="0e3ad-194">Nadat u de installatiekopie naar het containerregister hebt gepusht, kunt u de lokale installatiekopie op de ontwikkelcomputer verwijderen:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-194">After you push the image to the container registry you can delete the local image from your development computer:</span></span>

```
docker rmi helloworldapp
docker rmi myregistry.azurecr.io/samples/helloworldapp
```

## <a name="complete-example-service-fabric-application-and-service-manifests"></a><span data-ttu-id="0e3ad-195">Volledig voorbeeld van de manifesten voor de Fabric Service-toepassing en -service</span><span class="sxs-lookup"><span data-stu-id="0e3ad-195">Complete example Service Fabric application and service manifests</span></span>
<span data-ttu-id="0e3ad-196">Dit zijn de volledige manifesten voor de service en toepassing die in dit artikel worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-196">Here are the complete service and application manifests used in this article.</span></span>

### <a name="servicemanifestxml"></a><span data-ttu-id="0e3ad-197">ServiceManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0e3ad-197">ServiceManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest Name="myservicePkg"
                 Version="1.0.0"
                 xmlns="http://schemas.microsoft.com/2011/01/fabric"
                 xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                 xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <ServiceTypes>
    <!-- This is the name of your ServiceType.
         The UseImplicitHost attribute indicates this is a guest service. -->
    <StatelessServiceType ServiceTypeName="myserviceType" UseImplicitHost="true" />
  </ServiceTypes>

  <!-- Code package is your service executable. -->
  <CodePackage Name="Code" Version="1.0.0">
    <EntryPoint>
      <!-- Follow this link for more information about deploying Windows containers 
      to Service Fabric: https://aka.ms/sfguestcontainers -->
      <ContainerHost>
        <ImageName>myregistry.azurecr.io/samples/helloworldapp</ImageName>
        <Commands></Commands>
      </ContainerHost>
    </EntryPoint>
    <!-- Pass environment variables to your container: -->
    
    <EnvironmentVariables>
      <!--
      <EnvironmentVariable Name="VariableName" Value="VariableValue"/>
      -->
    </EnvironmentVariables>
    
  </CodePackage>

  <Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="myserviceTypeEndpoint" UriScheme="http" Port="4000" Protocol="http"/>
    </Endpoints>
  </Resources>
</ServiceManifest>
```
### <a name="applicationmanifestxml"></a><span data-ttu-id="0e3ad-198">ApplicationManifest.xml</span><span class="sxs-lookup"><span data-stu-id="0e3ad-198">ApplicationManifest.xml</span></span>
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest ApplicationTypeName="mycontainerType"
                     ApplicationTypeVersion="1.0.0"
                     xmlns="http://schemas.microsoft.com/2011/01/fabric"
                     xmlns:xsd="http://www.w3.org/2001/XMLSchema"
                     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <!-- Import the ServiceManifest from the ServicePackage. The ServiceManifestName and ServiceManifestVersion 
       should match the Name and Version attributes of the ServiceManifest element defined in the 
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
    <!-- The section below creates instances of service types, when an instance of this 
         application type is created. You can also create one or more instances of service type using the 
         ServiceFabric PowerShell module.
         
         The attribute ServiceTypeName below must match the name defined in the imported ServiceManifest.xml file. -->
    <Service Name="myservice">
      <!-- On a local development cluster, set InstanceCount to 1.  On a multi-node production 
      cluster, set InstanceCount to -1 for the container service to run on every node in 
      the cluster.
      -->
      <StatelessService ServiceTypeName="myserviceType" InstanceCount="1">
        <SingletonPartition />
      </StatelessService>
    </Service>
  </DefaultServices>
</ApplicationManifest>
```
## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="0e3ad-199">Meer services toevoegen aan een bestaande toepassing</span><span class="sxs-lookup"><span data-stu-id="0e3ad-199">Adding more services to an existing application</span></span>

<span data-ttu-id="0e3ad-200">Voer de volgende stappen uit als u nog een containerservice wilt toevoegen aan een toepassing die al is gemaakt met yeoman:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-200">To add another container service to an application already created using yeoman, perform the following steps:</span></span>

1. <span data-ttu-id="0e3ad-201">Stel de directory in op de hoofdmap van de bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-201">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="0e3ad-202">Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-202">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="0e3ad-203">Voer `yo azuresfcontainer:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-203">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>


## <a name="configure-time-interval-before-container-is-force-terminated"></a><span data-ttu-id="0e3ad-204">Tijdsinterval configureren voor geforceerd beëindigen van container</span><span class="sxs-lookup"><span data-stu-id="0e3ad-204">Configure time interval before container is force terminated</span></span>

<span data-ttu-id="0e3ad-205">U kunt een tijdsinterval configureren, zodat de runtime die tijd wacht voordat de container wordt verwijderd nadat het verwijderen van een service (of het verplaatsen naar een ander knooppunt) is gestart.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-205">You can configure a time interval for the runtime to wait before the container is removed after the service deletion (or a move to another node) has started.</span></span> <span data-ttu-id="0e3ad-206">Als u een tijdsinterval configureert, wordt de `docker stop <time in seconds>` opdracht verzonden naar de container.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-206">Configuring the time interval sends the `docker stop <time in seconds>` command to the container.</span></span>   <span data-ttu-id="0e3ad-207">Zie [docker stop](https://docs.docker.com/engine/reference/commandline/stop/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-207">For more detail, see [docker stop](https://docs.docker.com/engine/reference/commandline/stop/).</span></span> <span data-ttu-id="0e3ad-208">Het tijdsinterval dat moet worden gewacht, kunt u opgeven in de sectie `Hosting`.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-208">The time interval to wait is specified under the `Hosting` section.</span></span> <span data-ttu-id="0e3ad-209">Het volgende fragment van een clustermanifest laat zien hoe u het wachtinterval instelt:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-209">The following cluster manifest snippet shows how to set the wait interval:</span></span>

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
<span data-ttu-id="0e3ad-210">Het standaardtijdsinterval is 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-210">The default time interval is set to 10 seconds.</span></span> <span data-ttu-id="0e3ad-211">Aangezien deze configuratie dynamisch is, wordt de time-out bijgewerkt bij een configuratie-upgrade van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-211">Since this configuration is dynamic, a config only upgrade on the cluster updates the timeout.</span></span> 


## <a name="configure-the-runtime-to-remove-unused-container-images"></a><span data-ttu-id="0e3ad-212">De runtime configureren voor het verwijderen van ongebruikte containerinstallatiekopieën</span><span class="sxs-lookup"><span data-stu-id="0e3ad-212">Configure the runtime to remove unused container images</span></span>

<span data-ttu-id="0e3ad-213">U kunt het Service Fabric-cluster configureren voor het verwijderen van ongebruikte containerinstallatiekopieën van het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-213">You can configure the Service Fabric cluster to remove unused container images from the node.</span></span> <span data-ttu-id="0e3ad-214">Met deze configuratie kunt u schijfruimte vrijmaken als er te veel containerinstallatiekopieën aanwezig zijn op het knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-214">This configuration allows disk space to be recaptured if too many container images are present on the node.</span></span>  <span data-ttu-id="0e3ad-215">Om deze functie in te schakelen, past u de sectie `Hosting` in het clustermanifest aan zoals wordt weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="0e3ad-215">To enable this feature, update the `Hosting` section in the cluster manifest as shown in the following snippet:</span></span> 


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

<span data-ttu-id="0e3ad-216">De installatiekopieën die niet moeten worden verwijderd, kunt u opgeven met de parameter `ContainerImagesToSkip`.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-216">For images that should not be deleted, you can specify them under the `ContainerImagesToSkip` parameter.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="0e3ad-217">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0e3ad-217">Next steps</span></span>
* <span data-ttu-id="0e3ad-218">Meer informatie over het uitvoeren van [containers in Service Fabric](service-fabric-containers-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-218">Learn more about running [containers on Service Fabric](service-fabric-containers-overview.md).</span></span>
* <span data-ttu-id="0e3ad-219">Lees de zelfstudie [Een .NET-toepassing implementeren in een container](service-fabric-host-app-in-a-container.md).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-219">Read the [Deploy a .NET application in a container](service-fabric-host-app-in-a-container.md) tutorial.</span></span>
* <span data-ttu-id="0e3ad-220">Meer informatie over de [levenscyclus](service-fabric-application-lifecycle.md) van de Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0e3ad-220">Learn about the Service Fabric [application life-cycle](service-fabric-application-lifecycle.md).</span></span>
* <span data-ttu-id="0e3ad-221">Bekijk [voorbeelden van Service Fabric-containercode op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers).</span><span class="sxs-lookup"><span data-stu-id="0e3ad-221">Checkout the [Service Fabric container code samples](https://github.com/Azure-Samples/service-fabric-dotnet-containers) on GitHub.</span></span>

[hello-world]: ./media/service-fabric-get-started-containers-linux/HelloWorld.png
[sf-yeoman]: ./media/service-fabric-get-started-containers-linux/YoSF.png
