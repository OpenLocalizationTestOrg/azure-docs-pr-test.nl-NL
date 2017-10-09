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
# <a name="deploy-a-linux-container-tooservice-fabric"></a><span data-ttu-id="36817-104">Implementeren van een Linux-container tooService Fabric</span><span class="sxs-lookup"><span data-stu-id="36817-104">Deploy a Linux container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="36817-105">Windows-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="36817-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="36817-106">Linux-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="36817-106">Deploy Linux Container</span></span>](service-fabric-deploy-container-linux.md)
>
>

<span data-ttu-id="36817-107">Dit artikel begeleidt u bij het ontwikkelen van beperkte services in Docker-containers op Linux.</span><span class="sxs-lookup"><span data-stu-id="36817-107">This article walks you through building containerized services in Docker containers on Linux.</span></span>

<span data-ttu-id="36817-108">Service Fabric heeft verschillende mogelijkheden voor de container die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices die beperkte zijn.</span><span class="sxs-lookup"><span data-stu-id="36817-108">Service Fabric has several container capabilities that help you with building applications that are composed of microservices that are containerized.</span></span> <span data-ttu-id="36817-109">Deze services worden beperkte services genoemd.</span><span class="sxs-lookup"><span data-stu-id="36817-109">These services are called containerized services.</span></span>

<span data-ttu-id="36817-110">Hallo-mogelijkheden zijn onder andere;</span><span class="sxs-lookup"><span data-stu-id="36817-110">hello capabilities include;</span></span>

* <span data-ttu-id="36817-111">Implementatie van de container en activeren</span><span class="sxs-lookup"><span data-stu-id="36817-111">Container image deployment and activation</span></span>
* <span data-ttu-id="36817-112">Resource governance</span><span class="sxs-lookup"><span data-stu-id="36817-112">Resource governance</span></span>
* <span data-ttu-id="36817-113">Verificatie van de opslagplaats</span><span class="sxs-lookup"><span data-stu-id="36817-113">Repository authentication</span></span>
* <span data-ttu-id="36817-114">Container toohost poort poorttoewijzing</span><span class="sxs-lookup"><span data-stu-id="36817-114">Container port toohost port mapping</span></span>
* <span data-ttu-id="36817-115">Container voor container detectie en communicatie</span><span class="sxs-lookup"><span data-stu-id="36817-115">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="36817-116">Mogelijkheid tooconfigure en omgevingsvariabelen worden ingesteld</span><span class="sxs-lookup"><span data-stu-id="36817-116">Ability tooconfigure and set environment variables</span></span>

## <a name="packaging-a-docker-container-with-yeoman"></a><span data-ttu-id="36817-117">Een docker-container verpakking met yeoman</span><span class="sxs-lookup"><span data-stu-id="36817-117">Packaging a docker container with yeoman</span></span>
<span data-ttu-id="36817-118">Als een container op Linux verpakking, kunt u beide toouse een sjabloon yeoman of [handmatig maken van het toepassingspakket Hallo](#manually).</span><span class="sxs-lookup"><span data-stu-id="36817-118">When packaging a container on Linux, you can choose either toouse a yeoman template or [create hello application package manually](#manually).</span></span>

<span data-ttu-id="36817-119">Een Service Fabric-toepassing kan een of meer containers, elk met een specifieke functie in het leveren van de functionaliteit van de toepassing hello bevatten.</span><span class="sxs-lookup"><span data-stu-id="36817-119">A Service Fabric application can contain one or more containers, each with a specific role in delivering hello application's functionality.</span></span> <span data-ttu-id="36817-120">Hallo Service Fabric SDK voor Linux bevat een [Yeoman](http://yeoman.io/) generator waardoor u eenvoudig toocreate uw toepassing en een installatiekopie van de container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="36817-120">hello Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy toocreate your application and add a container image.</span></span> <span data-ttu-id="36817-121">We gebruiken Yeoman toocreate aangeroepen voor een toepassing met een enkele Docker-container *SimpleContainerApp*.</span><span class="sxs-lookup"><span data-stu-id="36817-121">Let's use Yeoman toocreate an application with a single Docker container called *SimpleContainerApp*.</span></span> <span data-ttu-id="36817-122">U kunt later meer services toevoegen door Hallo gegenereerd manifest-bestanden te bewerken.</span><span class="sxs-lookup"><span data-stu-id="36817-122">You can add more services later by editing hello generated manifest files.</span></span>

## <a name="install-docker-on-your-development-box"></a><span data-ttu-id="36817-123">Docker installeren op de box ontwikkeling</span><span class="sxs-lookup"><span data-stu-id="36817-123">Install Docker on your development box</span></span>

<span data-ttu-id="36817-124">Voer Hallo deze opdrachten tooinstall docker op de box Linux-ontwikkeling (als u Hallo vagrant installatiekopie in OSX gebruikt, docker is al geïnstalleerd):</span><span class="sxs-lookup"><span data-stu-id="36817-124">Run hello following commands tooinstall docker on your Linux development box (if you are using hello vagrant image on OSX, docker is already installed):</span></span>

```bash
    sudo apt-get install wget
    wget -qO- https://get.docker.io/ | sh
```

## <a name="create-hello-application"></a><span data-ttu-id="36817-125">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="36817-125">Create hello application</span></span>
1. <span data-ttu-id="36817-126">Typ in een terminal `yo azuresfcontainer`.</span><span class="sxs-lookup"><span data-stu-id="36817-126">In a terminal, type `yo azuresfcontainer`.</span></span>
2. <span data-ttu-id="36817-127">Naam van uw toepassing - bijvoorbeeld mycontainerap</span><span class="sxs-lookup"><span data-stu-id="36817-127">Name your application - for example, mycontainerap</span></span>
3. <span data-ttu-id="36817-128">Hallo-URL opgeven voor Hallo container afbeelding uit een DockerHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="36817-128">Provide hello URL for hello container image from a DockerHub repo.</span></span> <span data-ttu-id="36817-129">Hallo installatiekopie parameter vergt Hallo formulier [opslagplaats] / [naam afbeelding]</span><span class="sxs-lookup"><span data-stu-id="36817-129">hello image parameter takes hello form [repo]/[image name]</span></span>
4. <span data-ttu-id="36817-130">Als Hallo installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u tooexplicitly invoer-opdrachten opgeven met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container die behoudt Hallo container uitgevoerd na het opstarten.</span><span class="sxs-lookup"><span data-stu-id="36817-130">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

![Service Fabric Yeoman-generator voor containers][sf-yeoman]

## <a name="deploy-hello-application"></a><span data-ttu-id="36817-132">Hallo-toepassing implementeren</span><span class="sxs-lookup"><span data-stu-id="36817-132">Deploy hello application</span></span>

### <a name="using-xplat-cli"></a><span data-ttu-id="36817-133">Met XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="36817-133">Using XPlat CLI</span></span>
<span data-ttu-id="36817-134">Als de toepassing hello is gebouwd, kunt u deze toohello lokale cluster met behulp van Azure CLI Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="36817-134">Once hello application is built, you can deploy it toohello local cluster using hello Azure CLI.</span></span>

1. <span data-ttu-id="36817-135">Verbinding maken met toohello lokale Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="36817-135">Connect toohello local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="36817-136">Gebruik Hallo installatiescript geleverd in Hallo sjabloon toocopy toepassing hello archief van de installatiekopie van het cluster toohello van het pakket, registratie van toepassingstype Hallo en op een exemplaar van de toepassing hello maken.</span><span class="sxs-lookup"><span data-stu-id="36817-136">Use hello install script provided in hello template toocopy hello application package toohello cluster's image store, register hello application type, and create an instance of hello application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="36817-137">Open een browser en ga tooService Fabric Explorer op http://localhost: 19080/Explorer (localhost vervangen met particuliere IP-Hallo Hallo VM als Vagrant op Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="36817-137">Open a browser and navigate tooService Fabric Explorer at http://localhost:19080/Explorer (replace localhost with hello private IP of hello VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="36817-138">Hallo toepassingen knooppunt uitvouwen en er is nu een vermelding voor het toepassingstype van uw en een andere voor Hallo eerste exemplaar van dat type.</span><span class="sxs-lookup"><span data-stu-id="36817-138">Expand hello Applications node and note that there is now an entry for your application type and another for hello first instance of that type.</span></span>
5. <span data-ttu-id="36817-139">Gebruik Hallo uninstall-script in Hallo toodelete Hallo toepassing sjabloonexemplaar en registratie van toepassingstype Hallo.</span><span class="sxs-lookup"><span data-stu-id="36817-139">Use hello uninstall script provided in hello template toodelete hello application instance and unregister hello application type.</span></span>

    ```bash
    ./uninstall.sh
    ```

### <a name="using-azure-cli-20"></a><span data-ttu-id="36817-140">Met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="36817-140">Using Azure CLI 2.0</span></span>

<span data-ttu-id="36817-141">Zie Hallo verwijzing document over het beheren van een [gebruik van de levenscyclus van de toepassing hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span><span class="sxs-lookup"><span data-stu-id="36817-141">See hello reference doc on managing an [application life cycle using hello Azure CLI 2.0](service-fabric-application-lifecycle-azure-cli-2-0.md).</span></span>

<span data-ttu-id="36817-142">Voor een voorbeeldtoepassing [afhandeling Hallo Service Fabric-containercode voorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="36817-142">For an example application, [checkout hello Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="adding-more-services-tooan-existing-application"></a><span data-ttu-id="36817-143">Meer services tooan bestaande toepassing toe te voegen</span><span class="sxs-lookup"><span data-stu-id="36817-143">Adding more services tooan existing application</span></span>

<span data-ttu-id="36817-144">tooadd een andere container servicetoepassing tooan al gemaakt met behulp van `yo`, Hallo volgende stappen uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="36817-144">tooadd another container service tooan application already created using `yo`, perform hello following steps:</span></span>

1. <span data-ttu-id="36817-145">Toohello hoofdmap van de bestaande toepassing hello wijzigen.</span><span class="sxs-lookup"><span data-stu-id="36817-145">Change directory toohello root of hello existing application.</span></span>  <span data-ttu-id="36817-146">Bijvoorbeeld: `cd ~/YeomanSamples/MyApplication`als `MyApplication` is gemaakt door Yeoman Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="36817-146">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is hello application created by Yeoman.</span></span>
2. <span data-ttu-id="36817-147">Voer `yo azuresfcontainer:AddService` uit.</span><span class="sxs-lookup"><span data-stu-id="36817-147">Run `yo azuresfcontainer:AddService`</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="36817-148">Handmatig van het pakket en een installatiekopie van een container implementeren</span><span class="sxs-lookup"><span data-stu-id="36817-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="36817-149">Hallo-proces handmatig een beperkte service verpakt is gebaseerd op Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="36817-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="36817-150">Hallo containers tooyour opslagplaats publiceren.</span><span class="sxs-lookup"><span data-stu-id="36817-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="36817-151">Mapstructuur Hallo-pakket maken.</span><span class="sxs-lookup"><span data-stu-id="36817-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="36817-152">Servicemanifest Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="36817-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="36817-153">Manifestbestand van de toepassing hello bewerken.</span><span class="sxs-lookup"><span data-stu-id="36817-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="36817-154">Implementeren en activeren van een installatiekopie van een container</span><span class="sxs-lookup"><span data-stu-id="36817-154">Deploy and activate a container image</span></span>
<span data-ttu-id="36817-155">In Service Fabric Hallo [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="36817-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="36817-156">toodeploy en activeren van een container, put Hallo-naam van Hallo container installatiekopie in een `ContainerHost` -element in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="36817-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="36817-157">Hallo servicemanifest, Voeg een `ContainerHost` voor Hallo toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="36817-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="36817-158">Vervolgens set Hallo `ImageName` toobe Hallo-naam van Hallo container opslagplaats en de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="36817-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="36817-159">Hallo volgende gedeeltelijke manifest toont een voorbeeld van hoe toodeploy Hallo container aangeroepen `myimage:v1` vanuit een opslagplaats aangeroepen `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="36817-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="36817-160">Kunt u opdrachten invoer bieden door te geven Hallo optionele `Commands` element met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="36817-160">You can provide input commands by specifying hello optional `Commands` element with a comma-delimited set of commands toorun inside hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="36817-161">Als Hallo installatiekopie beschikt niet over een werkbelasting-toegangspunt gedefinieerd, moet u tooexplicitly invoer-opdrachten binnen opgeven `Commands` element met een door komma's gescheiden reeks opdrachten toorun binnen Hallo-container die uitgevoerd behoudt na het Hallo-container opstarten.</span><span class="sxs-lookup"><span data-stu-id="36817-161">If hello image does not have a workload entry-point defined, then you need tooexplicitly specify input commands inside `Commands` element with a comma-delimited set of commands toorun inside hello container, which will keep hello container running after startup.</span></span>

## <a name="understand-resource-governance"></a><span data-ttu-id="36817-162">Resource governance begrijpen</span><span class="sxs-lookup"><span data-stu-id="36817-162">Understand resource governance</span></span>
<span data-ttu-id="36817-163">Resource governance is een functie van Hallo-container die beperkt Hallo-resources die container Hallo kunt gebruiken op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="36817-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="36817-164">Hallo `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest Hallo gebruikte toodeclare limieten voor een service-codepakket is.</span><span class="sxs-lookup"><span data-stu-id="36817-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="36817-165">Limieten kunnen worden ingesteld voor Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="36817-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="36817-166">Geheugen</span><span class="sxs-lookup"><span data-stu-id="36817-166">Memory</span></span>
* <span data-ttu-id="36817-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="36817-167">MemorySwap</span></span>
* <span data-ttu-id="36817-168">CpuShares (CPU relatieve gewicht)</span><span class="sxs-lookup"><span data-stu-id="36817-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="36817-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="36817-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="36817-170">BlkioWeight (BlockIO relatieve gewicht).</span><span class="sxs-lookup"><span data-stu-id="36817-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="36817-171">In een toekomstige release, ondersteuning voor het opgeven van specifieke blok i/o-limieten zoals IOP's, lezen/schrijven BPS en anderen worden opgenomen.</span><span class="sxs-lookup"><span data-stu-id="36817-171">In a future release, support for specifying specific block IO limits such as IOPs, read/write BPS, and others will be included.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="36817-172">Een opslagplaats verifiëren</span><span class="sxs-lookup"><span data-stu-id="36817-172">Authenticate a repository</span></span>
<span data-ttu-id="36817-173">toodownload een container, moet u wellicht tooprovide aanmeldingsreferenties toohello container opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="36817-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="36817-174">Hallo aanmeldingsreferenties, opgegeven in het toepassingsmanifest hello, zijn gebruikte toospecify Hallo aanmelden informatie of SSH-sleutel voor het downloaden van Hallo container installatiekopie van het Hallo-opslagplaats voor installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="36817-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="36817-175">Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker* samen met het wachtwoord in ongecodeerde tekst hello (*niet* aanbevolen):</span><span class="sxs-lookup"><span data-stu-id="36817-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="36817-176">Het is raadzaam dat u Hallo wachtwoord versleutelen met behulp van een certificaat dat is geïmplementeerd toohello machine.</span><span class="sxs-lookup"><span data-stu-id="36817-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="36817-177">Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker*, waarbij Hallo wachtwoord is versleuteld met behulp van een certificaat genaamd *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="36817-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="36817-178">U kunt Hallo `Invoke-ServiceFabricEncryptText` PowerShell-opdracht toocreate Hallo geheime gecodeerde tekst hello wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="36817-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="36817-179">Zie voor meer informatie artikel Hallo [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="36817-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="36817-180">Hallo persoonlijke sleutel van het Hallo-certificaat dat is gebruikt toodecrypt Hallo wachtwoord moet geïmplementeerde toohello lokale computer in een out-of-band-methode.</span><span class="sxs-lookup"><span data-stu-id="36817-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="36817-181">(In Azure is deze methode Azure Resource Manager.) Wanneer het Service Fabric Hallo service pakket toohello machine implementeert, kan het Hallo-geheim decoderen.</span><span class="sxs-lookup"><span data-stu-id="36817-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="36817-182">Met behulp van Hallo geheim samen met de accountnaam Hallo vervolgens verificatie met Hallo container opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="36817-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <a name="configure-container-port-to-host-port-mapping"></a><span data-ttu-id="36817-183">Poorttoewijzing container poort-naar-host configureren</span><span class="sxs-lookup"><span data-stu-id="36817-183">Configure container port-to-host port mapping</span></span>
<span data-ttu-id="36817-184">U kunt een host gebruikt poort toocommunicate configureren met Hallo-container door te geven een `PortBinding` Hallo-toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="36817-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="36817-185">Hallo poort binding maps Hallo poort toowhich Hallo service luistert binnen Hallo container tooa poort op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="36817-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="36817-186">Container voor container detectie en communicatie configureren</span><span class="sxs-lookup"><span data-stu-id="36817-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="36817-187">Met behulp van Hallo `PortBinding` beleid, kunt u een container poort tooan toewijzen `Endpoint` in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="36817-187">By using hello `PortBinding` policy, you can map a container port tooan `Endpoint` in hello service manifest.</span></span> <span data-ttu-id="36817-188">Hallo eindpunt `Endpoint1` een vaste poort (bijvoorbeeld poort 80) kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="36817-188">hello endpoint `Endpoint1` can specify a fixed port (for example, port 80).</span></span> <span data-ttu-id="36817-189">Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van toepassingspoortbereik Hallo-cluster wordt gekozen voor u.</span><span class="sxs-lookup"><span data-stu-id="36817-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>

<span data-ttu-id="36817-190">Als u een eindpunt opgeeft, met behulp van Hallo `Endpoint` tag op in Hallo servicemanifest van een gast-container, Service Fabric kan automatisch publiceren van dit eindpunt toohello Naming service.</span><span class="sxs-lookup"><span data-stu-id="36817-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="36817-191">Andere services die worden uitgevoerd in de cluster Hallo kunnen dus deze container Hallo REST-query's gebruiken voor het oplossen van detecteren.</span><span class="sxs-lookup"><span data-stu-id="36817-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

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

<span data-ttu-id="36817-192">Registreert Hello Naming service, hoeft u container-container-communicatie in Hallo code in de container met behulp van Hallo [omgekeerde proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="36817-192">By registering with hello Naming service, you can easily do container-to-container communication in hello code within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="36817-193">Communicatie wordt uitgevoerd door Hallo omgekeerde proxy http-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt.</span><span class="sxs-lookup"><span data-stu-id="36817-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="36817-194">Zie de volgende sectie Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="36817-194">For more information, see hello next section.</span></span>

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="36817-195">Omgevingsvariabelen configureren en instellen</span><span class="sxs-lookup"><span data-stu-id="36817-195">Configure and set environment variables</span></span>
<span data-ttu-id="36817-196">Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in servicemanifest hello, zowel voor services die worden geïmplementeerd in containers of voor services die worden geïmplementeerd als gast-processen uitvoerbare bestanden.</span><span class="sxs-lookup"><span data-stu-id="36817-196">Environment variables can be specified for each code package in hello service manifest, both for services that are deployed in containers or for services that are deployed as processes/guest executables.</span></span> <span data-ttu-id="36817-197">Deze variabele waarden voor omgevingsvariabelen worden genegeerd in het bijzonder in het toepassingsmanifest Hallo of opgegeven tijdens de implementatie als toepassingsparameters.</span><span class="sxs-lookup"><span data-stu-id="36817-197">These environment variable values can be overridden specifically in hello application manifest or specified during deployment as application parameters.</span></span>

<span data-ttu-id="36817-198">Hallo volgende service manifest XML-fragment toont een voorbeeld van hoe de omgevingsvariabelen toospecify voor een codepakket:</span><span class="sxs-lookup"><span data-stu-id="36817-198">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="36817-199">Deze omgevingsvariabelen kunnen worden genegeerd op toepassingsniveau voor Hallo-manifest:</span><span class="sxs-lookup"><span data-stu-id="36817-199">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="36817-200">In het vorige voorbeeld hello, we een expliciete waarde opgegeven voor Hallo `HttpGateway` omgevingsvariabele (19000), terwijl op Hallo-waarde voor `BackendServiceName` parameter via Hallo `[BackendSvc]` parameter van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="36817-200">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="36817-201">Deze instellingen kunt u toospecify Hallo waarde voor `BackendServiceName`wanneer u Hallo-toepassing implementeren en geen vaste waarde in het manifest Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="36817-201">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="36817-202">Voorbeelden voor de toepassing en servicemanifest voltooien</span><span class="sxs-lookup"><span data-stu-id="36817-202">Complete examples for application and service manifest</span></span>

<span data-ttu-id="36817-203">Hier volgt een voorbeeld-toepassingsmanifest:</span><span class="sxs-lookup"><span data-stu-id="36817-203">An example application manifest follows:</span></span>

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

<span data-ttu-id="36817-204">Hier volgt een voorbeeld van de servicemanifest (opgegeven in Hallo voorafgaand aan het toepassingsmanifest):</span><span class="sxs-lookup"><span data-stu-id="36817-204">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="36817-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="36817-205">Next steps</span></span>
<span data-ttu-id="36817-206">Nu u een beperkte service hebt geïmplementeerd, kunt u nagaan hoe toomanage levenscyclus door te lezen [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="36817-206">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="36817-207">Overzicht van Service Fabric en containers</span><span class="sxs-lookup"><span data-stu-id="36817-207">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* [<span data-ttu-id="36817-208">Interactie met Service Fabric-clusters met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="36817-208">Interacting with Service Fabric clusters using hello Azure CLI</span></span>](service-fabric-azure-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-deploy-container-linux/sf-container-yeoman1.png

## <a name="related-articles"></a><span data-ttu-id="36817-209">Verwante artikelen:</span><span class="sxs-lookup"><span data-stu-id="36817-209">Related articles</span></span>

* [<span data-ttu-id="36817-210">Aan de slag met Service Fabric en Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="36817-210">Getting started with Service Fabric and Azure CLI 2.0</span></span>](service-fabric-azure-cli-2-0.md)
* [<span data-ttu-id="36817-211">Aan de slag met Service Fabric XPlat CLI</span><span class="sxs-lookup"><span data-stu-id="36817-211">Getting started with Service Fabric XPlat CLI</span></span>](service-fabric-azure-cli.md)
