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
# <a name="deploy-a-linux-container-to-service-fabric"></a><span data-ttu-id="a7e76-104">Implementeren van een Linux-container voor Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a7e76-104">Deploy a Linux container to Service Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a7e76-105">Windows-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="a7e76-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="a7e76-106">Linux-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="a7e76-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="a7e76-107">Dit artikel begeleidt u bij het ontwikkelen van beperkte services in Docker-containers op Linux.</span><span class="sxs-lookup"><span data-stu-id="a7e76-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="a7e76-108">Service Fabric heeft verschillende mogelijkheden voor de container die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices die beperkte zijn.</span><span class="sxs-lookup"><span data-stu-id="a7e76-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="a7e76-109">Deze services worden beperkte services genoemd.</span><span class="sxs-lookup"><span data-stu-id="a7e76-109">These services are called containerized services.</span></span>

<span data-ttu-id="a7e76-110">De mogelijkheden omvatten;</span><span class="sxs-lookup"><span data-stu-id="a7e76-110">The capabilities include;</span></span>

* <span data-ttu-id="a7e76-111">Implementatie van de container en activeren</span><span class="sxs-lookup"><span data-stu-id="a7e76-111">Container image deployment and activation</span></span>
* <span data-ttu-id="a7e76-112">Resource governance</span><span class="sxs-lookup"><span data-stu-id="a7e76-112">Resource governance</span></span>
* <span data-ttu-id="a7e76-113">Verificatie van de opslagplaats</span><span class="sxs-lookup"><span data-stu-id="a7e76-113">Repository authentication</span></span>
* <span data-ttu-id="a7e76-114">Poort van de container voor poorttoewijzing host</span><span class="sxs-lookup"><span data-stu-id="a7e76-114">Container port to host port mapping</span></span>
* <span data-ttu-id="a7e76-115">Container voor container detectie en communicatie</span><span class="sxs-lookup"><span data-stu-id="a7e76-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="a7e76-116">Mogelijkheid om te configureren en de omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="a7e76-116">Ability to configure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="a7e76-117">Een docker-container verpakking met yeoman</span><span class="sxs-lookup"><span data-stu-id="a7e76-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="a7e76-118">Als een container op Linux verpakking, kunt u ofwel een sjabloon yeoman gebruiken of [handmatig maken van het toepassingspakket](#manually).</span><span class="sxs-lookup"><span data-stu-id="a7e76-118">When packaging a container on Linux, you can choose either to use a yeoman template or [create the application package manually](#manually).</span></span>

<span data-ttu-id="a7e76-119">Een Service Fabric-toepassing kan een of meer containers, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing bevatten.</span><span class="sxs-lookup"><span data-stu-id="a7e76-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="a7e76-120">De Service Fabric-SDK voor Linux bevat een [Yeoman](http://yeoman.io/)-generator waarmee u gemakkelijk uw eerste toepassing kunt maken en een containerinstallatiekopie kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a7e76-120">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your application and add a container image.</span></span> <span data-ttu-id="a7e76-121">We gebruiken Yeoman om een toepassing te maken met een enkele Docker-container genaamd *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="a7e76-121">Let's use Yeoman to create an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="a7e76-122">U kunt toevoegen om dat meer services die zich later door te bewerken van de gegenereerde manifest bestanden.</span><span class="sxs-lookup"><span data-stu-id="a7e76-122">You can add more services later by editing the generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="a7e76-123">Docker installeren op de box ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="a7e76-123">Install Docker on your development box</span></span>

<span data-ttu-id="a7e76-124">Voer de volgende opdrachten voor het installeren van docker op de box Linux-ontwikkeling (als u de installatiekopie van het vagrant in OSX gebruikt, docker is al geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="a7e76-124">Run the following commands to install docker on your Linux development box (if you are using the vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-the-application"></a><span data-ttu-id="a7e76-125">De toepassing maken</span><span class="sxs-lookup"><span data-stu-id="a7e76-125">Create the application</span></span>
1. <span data-ttu-id="a7e76-126">Typ in een terminal `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="a7e76-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="a7e76-127">Naam van uw toepassing - bijvoorbeeld mycontainerap</span><span class="sxs-lookup"><span data-stu-id="a7e76-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="a7e76-128">Geef de URL voor de container-installatiekopie uit een DockerHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a7e76-128">Provide the URL for the container image from a DockerHub repo.</span></span> <span data-ttu-id="a7e76-129">De parameter van de installatiekopie heeft de vorm [opslagplaats] / [naam afbeelding]</span><span class="sxs-lookup"><span data-stu-id="a7e76-129">The image parameter takes the form [repo]/[image name]</span></span>
4. <span data-ttu-id="a7e76-130">Als de installatiekopie geen een werkbelasting-toegangspunt gedefinieerd, heeft moet u opdrachten invoer expliciet opgeven met een door komma's gescheiden reeks opdrachten in de container, zodat de container uitgevoerd na het opstarten wordt behouden.</span><span class="sxs-lookup"><span data-stu-id="a7e76-130">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="deploy-the-application"></a><span data-ttu-id="a7e76-132">De toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="a7e76-132">Deploy the application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="a7e76-133">Met XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="a7e76-133">Using XPlat CLI</span></span>
<span data-ttu-id="a7e76-134">Als de toepassing is gemaakt, kunt u deze kunt implementeren in het lokale cluster met behulp van de Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="a7e76-134">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="a7e76-135">Maak verbinding met het lokale cluster van Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="a7e76-135">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="a7e76-136">Gebruik het installatiescript dat is opgegeven in de sjabloon om het toepassingspakket te kopiëren naar de installatiekopieopslag van het cluster, het toepassingstype te registreren en een exemplaar van de toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="a7e76-136">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="a7e76-137">Open een browser en navigeer naar de Service Fabric Explorer op http://localhost:19080/Explorer (vervang localhost door het privé IP-adres van de virtuele machine als u Vagrant in Mac OS X gebruikt).</span><span class="sxs-lookup"><span data-stu-id="a7e76-137">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="a7e76-138">Vouw het knooppunt Toepassingen uit. U ziet dat er nu een vermelding is voor uw toepassingstype en nog een voor het eerste exemplaar van dat type.</span><span class="sxs-lookup"><span data-stu-id="a7e76-138">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>
5. <span data-ttu-id="a7e76-139">Het uninstall-script dat is opgegeven in de sjabloon gebruiken om te verwijderen van exemplaar van de toepassing en registratie van het toepassingstype.</span><span class="sxs-lookup"><span data-stu-id="a7e76-139">Use the uninstall script provided in the template to delete the application instance and unregister the application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="a7e76-140">Met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a7e76-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="a7e76-141">Zie het document naslaginformatie over het beheren van een [levenscyclus van de toepassing met de Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="a7e76-141">See the reference doc on managing an [application life cycle using the Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="a7e76-142">Voor een voorbeeldtoepassing [afhandeling van de code van de container Service Fabric-voorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="a7e76-142">For an example application, [checkout the Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="a7e76-143">Meer services toevoegen aan een bestaande toepassing</span><span class="sxs-lookup"><span data-stu-id="a7e76-143">Adding more services to an existing application</span></span>

<span data-ttu-id="a7e76-144">Een andere containerservice toevoegen aan een toepassing die al is gemaakt met behulp van `yo`, voer de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a7e76-144">To add another container service to an application already created using `yo`, perform the following steps:</span></span>

1. <span data-ttu-id="a7e76-145">Stel de directory in op de hoofdmap van de bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7e76-145">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="a7e76-146">Bijvoorbeeld `cd ~/YeomanSamples/MyApplication` als `MyApplication` de toepassing is die is gemaakt door Yeoman.</span><span class="sxs-lookup"><span data-stu-id="a7e76-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="a7e76-147">Voer `yo azuresfcontainer:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="a7e76-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="a7e76-148">Handmatig van het pakket en een installatiekopie van een container implementeren</span><span class="sxs-lookup"><span data-stu-id="a7e76-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="a7e76-149">Het proces van het verpakken van handmatig een beperkte service is gebaseerd op de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a7e76-149">The process of manually packaging a containerized service is based on the following steps:</span></span>

1. <span data-ttu-id="a7e76-150">Publiceer de containers naar uw opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a7e76-150">Publish the containers to your repository.</span></span>
2. <span data-ttu-id="a7e76-151">De mapstructuur pakket maken.</span><span class="sxs-lookup"><span data-stu-id="a7e76-151">Create the package directory structure.</span></span>
3. <span data-ttu-id="a7e76-152">Bewerk het manifestbestand van de service.</span><span class="sxs-lookup"><span data-stu-id="a7e76-152">Edit the service manifest file.</span></span>
4. <span data-ttu-id="a7e76-153">Bewerk het manifestbestand van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7e76-153">Edit the application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="a7e76-154">Implementeren en activeren van een installatiekopie van een container</span><span class="sxs-lookup"><span data-stu-id="a7e76-154">Deploy and activate a container image</span></span>
<span data-ttu-id="a7e76-155">In de Service Fabric [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a7e76-155">In the Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="a7e76-156">Als u wilt implementeren en activeren van een container, plaatst u de naam van de container-installatiekopie in een `ContainerHost` element in het servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="a7e76-156">To deploy and activate a container, put the name of the container image into a `ContainerHost` element in the service manifest.</span></span>

<span data-ttu-id="a7e76-157">Voeg in het servicemanifest een `ContainerHost` voor het toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="a7e76-157">In the service manifest, add a `ContainerHost` for the entry point.</span></span> <span data-ttu-id="a7e76-158">Stel de `ImageName` moet de naam van de container-opslagplaats en de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a7e76-158">Then set the `ImageName` to be the name of the container repository and image.</span></span> <span data-ttu-id="a7e76-159">Het volgende gedeeltelijke manifest toont een voorbeeld van het implementeren van de container aangeroepen `myimage:v1` vanuit een opslagplaats aangeroepen `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="a7e76-159">The following partial manifest shows an example of how to deploy the container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="a7e76-160">U kunt de opdrachten invoer opgeven door te geven de optionele `Commands` element met een door komma's gescheiden reeks opdrachten uitvoeren in de container.</span><span class="sxs-lookup"><span data-stu-id="a7e76-160">You can provide input commands by specifying the optional `Commands` element with a comma-delimited set of commands to run inside the container.</span></span>

> [!NOTE]
> <span data-ttu-id="a7e76-161">Als de installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u expliciet opgeven van de opdrachten binnen invoer `Commands` element met een door komma's gescheiden reeks opdrachten uitvoeren in de container, zodat de container uitgevoerd na het opstarten wordt behouden.</span><span class="sxs-lookup"><span data-stu-id="a7e76-161">If the image does not have a workload entry-point defined, then you need to explicitly specify input commands inside `Commands` element with a comma-delimited set of commands to run inside the container, which will keep the container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="a7e76-162">Resource governance begrijpen</span><span class="sxs-lookup"><span data-stu-id="a7e76-162">Understand resource governance</span></span>
<span data-ttu-id="a7e76-163">Resource governance is een functie van de container die beperkt de resources die de container op de host gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="a7e76-163">Resource governance is a capability of the container that restricts the resources that the container can use on the host.</span></span> <span data-ttu-id="a7e76-164">De `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest wordt gebruikt om te declareren limieten voor een service code-pakket.</span><span class="sxs-lookup"><span data-stu-id="a7e76-164">The `ResourceGovernancePolicy`, which is specified in the application manifest is used to declare resource limits for a service code package.</span></span> <span data-ttu-id="a7e76-165">Limieten kunnen worden ingesteld voor de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="a7e76-165">Resource limits can be set for the following resources:</span></span>

* <span data-ttu-id="a7e76-166">Geheugen</span><span class="sxs-lookup"><span data-stu-id="a7e76-166">Memory</span></span>
* <span data-ttu-id="a7e76-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="a7e76-167">MemorySwap</span></span>
* <span data-ttu-id="a7e76-168">CpuShares (CPU relatieve gewicht)</span><span class="sxs-lookup"><span data-stu-id="a7e76-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="a7e76-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="a7e76-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="a7e76-170">BlkioWeight (BlockIO relatieve gewicht).</span><span class="sxs-lookup"><span data-stu-id="a7e76-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="a7e76-171">In een toekomstige release, ondersteuning voor het opgeven van specifieke blok i/o-limieten zoals IOP's, lezen/schrijven BPS en anderen worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="a7e76-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="a7e76-172">Een opslagplaats verifiëren</span><span class="sxs-lookup"><span data-stu-id="a7e76-172">Authenticate a repository</span></span>
<span data-ttu-id="a7e76-173">Voor het downloaden van een container, kunt u wellicht aanmelden referenties aan de container-opslagplaats op te geven.</span><span class="sxs-lookup"><span data-stu-id="a7e76-173">To download a container, you might have to provide sign-in credentials to the container repository.</span></span> <span data-ttu-id="a7e76-174">De aanmeldingsreferenties, opgegeven in het toepassingsmanifest worden gebruikt om op te geven van de aanmeldingsgegevens of SSH-sleutel voor het downloaden van de container-installatiekopie uit de opslagplaats voor installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="a7e76-174">The sign-in credentials, specified in the application manifest, are used to specify the sign-in information, or SSH key, for downloading the container image from the image repository.</span></span> <span data-ttu-id="a7e76-175">Het volgende voorbeeld ziet u een account met de naam *testgebruiker* samen met het wachtwoord in ongecodeerde tekst (*niet* aanbevolen):</span><span class="sxs-lookup"><span data-stu-id="a7e76-175">The following example shows an account called *TestUser* along with the password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="a7e76-176">Het is raadzaam dat u het wachtwoord versleutelen met behulp van een certificaat dat geïmplementeerd op de machine.</span><span class="sxs-lookup"><span data-stu-id="a7e76-176">We recommend that you encrypt the password by using a certificate that's deployed to the machine.</span></span>

<span data-ttu-id="a7e76-177">Het volgende voorbeeld ziet u een account met de naam *testgebruiker*, waar het wachtwoord is versleuteld met behulp van een certificaat genaamd *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="a7e76-177">The following example shows an account called *TestUser*, where the password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="a7e76-178">U kunt de `Invoke-ServiceFabricEncryptText` PowerShell-opdracht voor het maken van de geheime gecodeerde tekst voor het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a7e76-178">You can use the `Invoke-ServiceFabricEncryptText` PowerShell command to create the secret cipher text for the password.</span></span> <span data-ttu-id="a7e76-179">Zie voor meer informatie het artikel [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="a7e76-179">For more information, see the article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="a7e76-180">De persoonlijke sleutel van het certificaat dat wordt gebruikt voor het ontsleutelen van het wachtwoord moet worden geïmplementeerd op de lokale computer in een out-of-band-methode.</span><span class="sxs-lookup"><span data-stu-id="a7e76-180">The private key of the certificate that's used to decrypt the password must be deployed to the local machine in an out-of-band method.</span></span> <span data-ttu-id="a7e76-181">(In Azure is deze methode Azure Resource Manager.) Wanneer het Service Fabric pakket met de service op de machine implementeert, kan deze het geheim decoderen.</span><span class="sxs-lookup"><span data-stu-id="a7e76-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys the service package to the machine, it can decrypt the secret.</span></span> <span data-ttu-id="a7e76-182">Met behulp van het geheim samen met de accountnaam vervolgens verificatie met de container-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a7e76-182">By using the secret along with the account name, it can then authenticate with the container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="a7e76-183">Poorttoewijzing container poort-naar-host configureren</span><span class="sxs-lookup"><span data-stu-id="a7e76-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="a7e76-184">U kunt een hostpoort gebruikt voor communicatie met de container door te geven een `PortBinding` in het toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="a7e76-184">You can configure a host port used to communicate with the container by specifying a `PortBinding` in the application manifest.</span></span> <span data-ttu-id="a7e76-185">De poortbinding wijst de poort waarnaar de service binnen de container voor een poort op de host luistert.</span><span class="sxs-lookup"><span data-stu-id="a7e76-185">The port binding maps the port to which the service is listening inside the container to a port on the host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="a7e76-186">Container voor container detectie en communicatie configureren</span><span class="sxs-lookup"><span data-stu-id="a7e76-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="a7e76-187">Met behulp van de `PortBinding` beleid, kunt u een poort van de container voor toewijzen een `Endpoint` in het servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="a7e76-187">By using the `PortBinding` policy, you can map a container port to an `Endpoint` in the service manifest.</span></span> <span data-ttu-id="a7e76-188">Het eindpunt `Endpoint1` een vaste poort (bijvoorbeeld poort 80) kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="a7e76-188">The endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="a7e76-189">Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van het cluster toepassingspoortbereik voor u is gekozen.</span><span class="sxs-lookup"><span data-stu-id="a7e76-189">It can also specify no port at all, in which case a random port from the cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="a7e76-190">Als u een eindpunt opgeven, gebruikt de `Endpoint` -tag in het servicemanifest van een gast-container, Service Fabric automatisch dit eindpunt kunt publiceren naar de Naming service.</span><span class="sxs-lookup"><span data-stu-id="a7e76-190">If you specify an endpoint, using the `Endpoint` tag in the service manifest of a guest container, Service Fabric can automatically publish this endpoint to the Naming service.</span></span> <span data-ttu-id="a7e76-191">Deze container met de REST-query's voor het oplossen van kunnen dus detecteren door andere services die worden uitgevoerd in het cluster.</span><span class="sxs-lookup"><span data-stu-id="a7e76-191">Other services that are running in the cluster can thus discover this container using the REST queries for resolving.</span></span>

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

<span data-ttu-id="a7e76-192">Registreert met de service Naming, hoeft u container-container-communicatie in de code in de container met behulp van de [omgekeerde proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="a7e76-192">By registering with the Naming service, you can easily do container-to-container communication in the code within your container by using the [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="a7e76-193">Communicatie wordt uitgevoerd door de http-luisterpoort omgekeerde proxy en de naam van de services die u communiceren wilt met als omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="a7e76-193">Communication is performed by providing the reverse proxy http listening port and the name of the services that you want to communicate with as environment variables.</span></span> <span data-ttu-id="a7e76-194">Zie de volgende sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a7e76-194">For more information, see the next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="a7e76-195">Omgevingsvariabelen configureren en instellen</span><span class="sxs-lookup"><span data-stu-id="a7e76-195">Configure and set environment variables</span></span>
<span data-ttu-id="a7e76-196">Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in het servicemanifest van de, zowel voor services die worden geïmplementeerd in containers of voor services die worden geïmplementeerd als gast-processen uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="a7e76-196">Environment variables can be specified for each code package in the service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="a7e76-197">Deze variabele waarden voor omgevingsvariabelen worden genegeerd in het bijzonder in het toepassingsmanifest of opgegeven tijdens de implementatie als toepassingsparameters.</span><span class="sxs-lookup"><span data-stu-id="a7e76-197">These environment variable values can be overridden specifically in the application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="a7e76-198">Het volgende XML-fragment voor het servicemanifest toont een voorbeeld van het opgeven van omgevingsvariabelen voor een codepakket:</span><span class="sxs-lookup"><span data-stu-id="a7e76-198">The following service manifest XML snippet shows an example of how to specify environment variables for a code package:</span></span>

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

<span data-ttu-id="a7e76-199">Deze omgevingsvariabelen kunnen worden genegeerd op het niveau van manifest:</span><span class="sxs-lookup"><span data-stu-id="a7e76-199">These environment variables can be overridden at the application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="a7e76-200">In het vorige voorbeeld wordt een expliciete waarde opgegeven voor de `HttpGateway` omgevingsvariabele (19000), terwijl op de waarde voor `BackendServiceName` parameter via de `[BackendSvc]` parameter van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="a7e76-200">In the previous example, we specified an explicit value for the `HttpGateway` environment variable (19000), while we set the value for `BackendServiceName` parameter via the `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="a7e76-201">Deze instellingen kunt u de waarde voor `BackendServiceName`waarde wanneer u de toepassing implementeren en geen vaste waarde in het manifest.</span><span class="sxs-lookup"><span data-stu-id="a7e76-201">These settings enable you to specify the value for `BackendServiceName`value when you deploy the application and not have a fixed value in the manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="a7e76-202">Voorbeelden voor de toepassing en servicemanifest voltooien</span><span class="sxs-lookup"><span data-stu-id="a7e76-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="a7e76-203">Hier volgt een voorbeeld-toepassingsmanifest:</span><span class="sxs-lookup"><span data-stu-id="a7e76-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="a7e76-204">Hier volgt een voorbeeld van de servicemanifest (opgegeven in het voorgaande toepassingsmanifest):</span><span class="sxs-lookup"><span data-stu-id="a7e76-204">An example service manifest (specified in the preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="a7e76-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7e76-205">Next steps</span></span>
<span data-ttu-id="a7e76-206">Nu dat u een beperkte service hebt geïmplementeerd, informatie over het beheren van de levenscyclus door te lezen [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="a7e76-206">Now that you have deployed a containerized service, learn how to manage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="a7e76-207">Overzicht van Service Fabric en containers</span><span class="sxs-lookup"><span data-stu-id="a7e76-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="a7e76-208">Interactie aangaan met Service Fabric-clusters met de Azure-CLI</span><span class="sxs-lookup"><span data-stu-id="a7e76-208">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="a7e76-209">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="a7e76-209">Related articles</span></span>

* [<span data-ttu-id="a7e76-210">Aan de slag met Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a7e76-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="a7e76-211">Aan de slag met Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="a7e76-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
