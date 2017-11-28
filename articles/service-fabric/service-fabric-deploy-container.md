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
# <a name="deploy-a-windows-container-tooservice-fabric"></a><span data-ttu-id="f8fa6-104">Een Windows-container tooService Fabric implementeren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-104">Deploy a Windows container tooService Fabric</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f8fa6-105">Windows-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-105">Deploy Windows Container</span></span>](service-fabric-deploy-container.md)
> * [<span data-ttu-id="f8fa6-106">Docker-Container implementeren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-106">Deploy Docker Container</span></span>](service-fabric-deploy-container-linux.md)
> 
> 

<span data-ttu-id="f8fa6-107">In dit artikel begeleidt u bij Hallo proces van het bouwen van beperkte services in Windows-containers.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-107">This article walks you through hello process of building containerized services in Windows containers.</span></span>

<span data-ttu-id="f8fa6-108">Service Fabric heeft verschillende mogelijkheden die u helpen bij het bouwen van toepassingen die zijn samengesteld van microservices in containers wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-108">Service Fabric has several capabilities that help you with building applications that are composed of microservices running inside containers.</span></span> 

<span data-ttu-id="f8fa6-109">Hallo-mogelijkheden zijn:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-109">hello capabilities include:</span></span>

* <span data-ttu-id="f8fa6-110">Implementatie van de container en activeren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-110">Container image deployment and activation</span></span>
* <span data-ttu-id="f8fa6-111">Resource governance</span><span class="sxs-lookup"><span data-stu-id="f8fa6-111">Resource governance</span></span>
* <span data-ttu-id="f8fa6-112">Verificatie van de opslagplaats</span><span class="sxs-lookup"><span data-stu-id="f8fa6-112">Repository authentication</span></span>
* <span data-ttu-id="f8fa6-113">Poorttoewijzing container poort-naar-host</span><span class="sxs-lookup"><span data-stu-id="f8fa6-113">Container port-to-host port mapping</span></span>
* <span data-ttu-id="f8fa6-114">Container voor container detectie en communicatie</span><span class="sxs-lookup"><span data-stu-id="f8fa6-114">Container-to-container discovery and communication</span></span>
* <span data-ttu-id="f8fa6-115">Mogelijkheid tooconfigure en omgevingsvariabelen worden ingesteld</span><span class="sxs-lookup"><span data-stu-id="f8fa6-115">Ability tooconfigure and set environment variables</span></span>

<span data-ttu-id="f8fa6-116">Bekijk hoe elk van de mogelijkheden werkt wanneer u een beperkte service toobe opgenomen in uw toepassing inpakt.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-116">Let's look at how each of capabilities works when you're packaging a containerized service toobe included in your application.</span></span>

## <a name="package-a-windows-container"></a><span data-ttu-id="f8fa6-117">Pakket met een Windows-container</span><span class="sxs-lookup"><span data-stu-id="f8fa6-117">Package a Windows container</span></span>
<span data-ttu-id="f8fa6-118">Wanneer u een container van het pakket, kunt u kiezen toouse ofwel een Visual Studio-projectsjabloon of [handmatig maken van het toepassingspakket Hallo](#manually).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-118">When you package a container, you can choose toouse either a Visual Studio project template or [create hello application package manually](#manually).</span></span>  <span data-ttu-id="f8fa6-119">Wanneer u Visual Studio, Hallo toepassing pakketstructuur en manifest-bestanden voor u gemaakt door Hallo nieuw Project-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-119">When you use Visual Studio, hello application package structure and manifest files are created by hello New Project template for you.</span></span>

> [!TIP]
> <span data-ttu-id="f8fa6-120">Hallo gemakkelijkste manier toopackage een installatiekopie van een bestaande container in een service is toouse Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-120">hello easiest way toopackage an existing container image into a service is toouse Visual Studio.</span></span>

## <a name="use-visual-studio-toopackage-an-existing-container-image"></a><span data-ttu-id="f8fa6-121">Visual Studio toopackage een installatiekopie van een bestaande container gebruiken</span><span class="sxs-lookup"><span data-stu-id="f8fa6-121">Use Visual Studio toopackage an existing container image</span></span>
<span data-ttu-id="f8fa6-122">Visual Studio biedt een Service Fabric service sjabloon toohelp implementeren van een container tooa Service Fabric-cluster.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-122">Visual Studio provides a Service Fabric service template toohelp you deploy a container tooa Service Fabric cluster.</span></span>

1. <span data-ttu-id="f8fa6-123">Kies **bestand** > **nieuw Project**, en maak een Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-123">Choose **File** > **New Project**, and create a Service Fabric application.</span></span>
2. <span data-ttu-id="f8fa6-124">Kies **Gast Container** als Hallo-servicesjabloon.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-124">Choose **Guest Container** as hello service template.</span></span>
3. <span data-ttu-id="f8fa6-125">Kies **Installatiekopienaam** en mogelijk Hallo pad toohello installatiekopie in de container-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-125">Choose **Image Name** and provide hello path toohello image in your container repository.</span></span> <span data-ttu-id="f8fa6-126">Bijvoorbeeld: `myrepo/myimage:v1` in https://hub.docker.com</span><span class="sxs-lookup"><span data-stu-id="f8fa6-126">For example, `myrepo/myimage:v1` in https://hub.docker.com</span></span>
4. <span data-ttu-id="f8fa6-127">Geef de service een naam en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-127">Give your service a name, and click **OK**.</span></span>
5. <span data-ttu-id="f8fa6-128">Als uw beperkte service een eindpunt voor communicatie moet, kunt u nu Hallo-protocol en poort type toohello ServiceManifest.xml bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-128">If your containerized service needs an endpoint for communication, you can now add hello protocol, port, and type toohello ServiceManifest.xml file.</span></span> <span data-ttu-id="f8fa6-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-129">For example:</span></span> 
     
    `<Endpoint Name="MyContainerServiceEndpoint" Protocol="http" Port="80" UriScheme="http" PathSuffix="myapp/" Type="Input" />`
    
    <span data-ttu-id="f8fa6-130">Dankzij de Hallo `UriScheme`, Service Fabric Hallo container eindpunt wordt automatisch wordt geregistreerd bij Hallo Naming service voor detectie.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-130">By providing hello `UriScheme`, Service Fabric automatically registers hello container endpoint with hello Naming service for discoverability.</span></span> <span data-ttu-id="f8fa6-131">Hallo-poort kan worden opgelost (zoals weergegeven in het voorgaande voorbeeld Hallo) of dynamisch toegewezen.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-131">hello port can either be fixed (as shown in hello preceding example) or dynamically allocated.</span></span> <span data-ttu-id="f8fa6-132">Als u een poort niet opgeeft, wordt het dynamisch toegewezen van Hallo toepassingspoortbereik (zoals met een service gebeuren zou).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-132">If you don't specify a port, it is dynamically allocated from hello application port range (as would happen with any service).</span></span>
    <span data-ttu-id="f8fa6-133">U moet ook tooconfigure Hallo container toohost-poorttoewijzing door te geven een `PortBinding` beleid in het toepassingsmanifest Hallo.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-133">You also need tooconfigure hello container toohost port mapping by specifying a `PortBinding` policy in hello application manifest.</span></span> <span data-ttu-id="f8fa6-134">Zie voor meer informatie [container toohost poorttoewijzing configureren](#Portsection).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-134">For more information, see [Configure container toohost port mapping](#Portsection).</span></span>
6. <span data-ttu-id="f8fa6-135">Als uw container moet resource governance en vervolgens voegt u een `ResourceGovernancePolicy`.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-135">If your container needs resource governance then add a `ResourceGovernancePolicy`.</span></span>
8. <span data-ttu-id="f8fa6-136">Als uw container tooauthenticate met een persoonlijke opslagplaats moet, voegt u `RepositoryCredentials`.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-136">If your container needs tooauthenticate with a private repository, then add `RepositoryCredentials`.</span></span>
7. <span data-ttu-id="f8fa6-137">Als u op een Windows Server 2016-machine met de ondersteuning van de container is ingeschakeld uitvoert, kunt u Hallo pakket gebruiken en publiceren actie toodeploy tooyour lokale cluster.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-137">If you are running on a Windows Server 2016 machine with container support enabled, you can use hello package and publish action toodeploy tooyour local cluster.</span></span> 
8. <span data-ttu-id="f8fa6-138">Wanneer u klaar bent, kunt u Hallo toepassing tooa extern clusterbeheer publiceren of inchecken Hallo oplossing toosource besturingselement.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-138">When ready, you can publish hello application tooa remote cluster or check in hello solution toosource control.</span></span> 

<span data-ttu-id="f8fa6-139">Voor een voorbeeld: Bekijk Hallo [Service Fabric-container codevoorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="f8fa6-139">For an example, checkout hello [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>

## <a name="creating-a-windows-server-2016-cluster"></a><span data-ttu-id="f8fa6-140">Maken van een cluster met Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="f8fa6-140">Creating a Windows Server 2016 cluster</span></span>
<span data-ttu-id="f8fa6-141">toodeploy uw beperkte toepassing, moet u een cluster met Windows Server 2016 met ondersteuning voor de container ingeschakeld toocreate.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-141">toodeploy your containerized application, you need toocreate a cluster running Windows Server 2016 with container support enabled.</span></span> <span data-ttu-id="f8fa6-142">Uw cluster lokaal worden uitgevoerd of geïmplementeerd via Azure Resource Manager in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-142">Your cluster may be running locally, or deployed via Azure Resource Manager in Azure.</span></span> 

<span data-ttu-id="f8fa6-143">een cluster met Azure Resource Manager toodeploy kiezen Hallo **Windows Server 2016 met Containers** installatiekopie optie in Azure.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-143">toodeploy a cluster using Azure Resource Manager, choose hello **Windows Server 2016 with Containers** image option in Azure.</span></span> <span data-ttu-id="f8fa6-144">Zie het artikel Hallo [Service Fabric-cluster maken met behulp van Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-144">See hello article [Create a Service Fabric cluster by using Azure Resource Manager](service-fabric-cluster-creation-via-arm.md).</span></span> <span data-ttu-id="f8fa6-145">Zorg ervoor dat u hello Azure Resource Manager-instellingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-145">Ensure that you use hello following Azure Resource Manager settings:</span></span>

```xml
"vmImageOffer": { "type": "string","defaultValue": "WindowsServer"     },
"vmImageSku": { "defaultValue": "2016-Datacenter-with-Containers","type": "string"     },
"vmImageVersion": { "defaultValue": "latest","type": "string"     },  
```
<span data-ttu-id="f8fa6-146">U kunt ook Hallo [vijf knooppunt Azure Resource Manager-sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate een cluster.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-146">You can also use hello [Five Node Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/service-fabric-secure-cluster-5-node-1-nodetype) toocreate a cluster.</span></span> <span data-ttu-id="f8fa6-147">U kunt ook een community lezen [blogbericht](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) over het gebruik van Service Fabric- en Windows-containers.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-147">Alternatively read a community [blog post](https://loekd.blogspot.com/2017/01/running-windows-containers-on-azure.html) on using Service Fabric and Windows containers.</span></span>

<a id="manually"></a>

## <a name="manually-package-and-deploy-a-container-image"></a><span data-ttu-id="f8fa6-148">Handmatig van het pakket en een installatiekopie van een container implementeren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-148">Manually package and deploy a container image</span></span>
<span data-ttu-id="f8fa6-149">Hallo-proces handmatig een beperkte service verpakt is gebaseerd op Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-149">hello process of manually packaging a containerized service is based on hello following steps:</span></span>

1. <span data-ttu-id="f8fa6-150">Hallo containers tooyour opslagplaats publiceren.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-150">Publish hello containers tooyour repository.</span></span>
2. <span data-ttu-id="f8fa6-151">Mapstructuur Hallo-pakket maken.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-151">Create hello package directory structure.</span></span>
3. <span data-ttu-id="f8fa6-152">Servicemanifest Hallo bewerken.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-152">Edit hello service manifest file.</span></span>
4. <span data-ttu-id="f8fa6-153">Manifestbestand van de toepassing hello bewerken.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-153">Edit hello application manifest file.</span></span>

## <a name="deploy-and-activate-a-container-image"></a><span data-ttu-id="f8fa6-154">Implementeren en activeren van een installatiekopie van een container</span><span class="sxs-lookup"><span data-stu-id="f8fa6-154">Deploy and activate a container image</span></span>
<span data-ttu-id="f8fa6-155">In Service Fabric Hallo [toepassingsmodel](service-fabric-application-model.md), een container vertegenwoordigt een toepassingshost welke service meerdere replica's worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-155">In hello Service Fabric [application model](service-fabric-application-model.md), a container represents an application host in which multiple service replicas are placed.</span></span> <span data-ttu-id="f8fa6-156">toodeploy en activeren van een container, put Hallo-naam van Hallo container installatiekopie in een `ContainerHost` -element in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-156">toodeploy and activate a container, put hello name of hello container image into a `ContainerHost` element in hello service manifest.</span></span>

<span data-ttu-id="f8fa6-157">Hallo servicemanifest, Voeg een `ContainerHost` voor Hallo toegangspunt.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-157">In hello service manifest, add a `ContainerHost` for hello entry point.</span></span> <span data-ttu-id="f8fa6-158">Vervolgens set Hallo `ImageName` toobe Hallo-naam van Hallo container opslagplaats en de installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-158">Then set hello `ImageName` toobe hello name of hello container repository and image.</span></span> <span data-ttu-id="f8fa6-159">Hallo volgende gedeeltelijke manifest toont een voorbeeld van hoe toodeploy Hallo container aangeroepen `myimage:v1` vanuit een opslagplaats aangeroepen `myrepo`:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-159">hello following partial manifest shows an example of how toodeploy hello container called `myimage:v1` from a repository called `myrepo`:</span></span>

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

<span data-ttu-id="f8fa6-160">Kunt u optionele opdrachten toorun bij het starten van de container onder Hallo Hallo `Commands` element.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-160">You can specify optional commands toorun upon starting hello container under hello `Commands` element.</span></span> <span data-ttu-id="f8fa6-161">Voor meerdere opdrachten komma-beperken ze.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-161">For multiple commands, comma-delimit them.</span></span> 

## <a name="understand-resource-governance"></a><span data-ttu-id="f8fa6-162">Resource governance begrijpen</span><span class="sxs-lookup"><span data-stu-id="f8fa6-162">Understand resource governance</span></span>
<span data-ttu-id="f8fa6-163">Resource governance is een functie van Hallo-container die beperkt Hallo-resources die container Hallo kunt gebruiken op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-163">Resource governance is a capability of hello container that restricts hello resources that hello container can use on hello host.</span></span> <span data-ttu-id="f8fa6-164">Hallo `ResourceGovernancePolicy`, die is opgegeven in het toepassingsmanifest Hallo gebruikte toodeclare limieten voor een service-codepakket is.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-164">hello `ResourceGovernancePolicy`, which is specified in hello application manifest is used toodeclare resource limits for a service code package.</span></span> <span data-ttu-id="f8fa6-165">Limieten kunnen worden ingesteld voor Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-165">Resource limits can be set for hello following resources:</span></span>

* <span data-ttu-id="f8fa6-166">Geheugen</span><span class="sxs-lookup"><span data-stu-id="f8fa6-166">Memory</span></span>
* <span data-ttu-id="f8fa6-167">MemorySwap</span><span class="sxs-lookup"><span data-stu-id="f8fa6-167">MemorySwap</span></span>
* <span data-ttu-id="f8fa6-168">CpuShares (CPU relatieve gewicht)</span><span class="sxs-lookup"><span data-stu-id="f8fa6-168">CpuShares (CPU relative weight)</span></span>
* <span data-ttu-id="f8fa6-169">MemoryReservationInMB</span><span class="sxs-lookup"><span data-stu-id="f8fa6-169">MemoryReservationInMB</span></span>  
* <span data-ttu-id="f8fa6-170">BlkioWeight (BlockIO relatieve gewicht).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-170">BlkioWeight (BlockIO relative weight).</span></span>

> [!NOTE]
> <span data-ttu-id="f8fa6-171">Ondersteuning voor het opgeven van specifieke blokkeren i/o-limieten, zoals IOP's, lezen/schrijven BPS en andere zijn gepland voor een toekomstige release.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-171">Support for specifying specific block IO limits such as IOPs, read/write BPS, and others are planned for a future release.</span></span>
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

## <a name="authenticate-a-repository"></a><span data-ttu-id="f8fa6-172">Een opslagplaats verifiëren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-172">Authenticate a repository</span></span>
<span data-ttu-id="f8fa6-173">toodownload een container, moet u wellicht tooprovide aanmeldingsreferenties toohello container opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-173">toodownload a container, you might have tooprovide sign-in credentials toohello container repository.</span></span> <span data-ttu-id="f8fa6-174">Hallo aanmeldingsreferenties, opgegeven in het toepassingsmanifest hello, zijn gebruikte toospecify Hallo aanmelden informatie of SSH-sleutel voor het downloaden van Hallo container installatiekopie van het Hallo-opslagplaats voor installatiekopieën.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-174">hello sign-in credentials, specified in hello application manifest, are used toospecify hello sign-in information, or SSH key, for downloading hello container image from hello image repository.</span></span> <span data-ttu-id="f8fa6-175">Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker* samen met het wachtwoord in ongecodeerde tekst hello (*niet* aanbevolen):</span><span class="sxs-lookup"><span data-stu-id="f8fa6-175">hello following example shows an account called *TestUser* along with hello password in clear text (*not* recommended):</span></span>

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

<span data-ttu-id="f8fa6-176">Het is raadzaam dat u Hallo wachtwoord versleutelen met behulp van een certificaat dat is geïmplementeerd toohello machine.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-176">We recommend that you encrypt hello password by using a certificate that's deployed toohello machine.</span></span>

<span data-ttu-id="f8fa6-177">Hallo volgende voorbeeld ziet u een account met de naam *testgebruiker*, waarbij Hallo wachtwoord is versleuteld met behulp van een certificaat genaamd *MyCert*.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-177">hello following example shows an account called *TestUser*, where hello password was encrypted by using a certificate called *MyCert*.</span></span> <span data-ttu-id="f8fa6-178">U kunt Hallo `Invoke-ServiceFabricEncryptText` PowerShell-opdracht toocreate Hallo geheime gecodeerde tekst hello wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-178">You can use hello `Invoke-ServiceFabricEncryptText` PowerShell command toocreate hello secret cipher text for hello password.</span></span> <span data-ttu-id="f8fa6-179">Zie voor meer informatie artikel Hallo [geheimen in Service Fabric-toepassingen beheren](service-fabric-application-secret-management.md).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-179">For more information, see hello article [Managing secrets in Service Fabric applications](service-fabric-application-secret-management.md).</span></span>

<span data-ttu-id="f8fa6-180">Hallo persoonlijke sleutel van het Hallo-certificaat dat is gebruikt toodecrypt Hallo wachtwoord moet geïmplementeerde toohello lokale computer in een out-of-band-methode.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-180">hello private key of hello certificate that's used toodecrypt hello password must be deployed toohello local machine in an out-of-band method.</span></span> <span data-ttu-id="f8fa6-181">(In Azure is deze methode Azure Resource Manager.) Wanneer het Service Fabric Hallo service pakket toohello machine implementeert, kan het Hallo-geheim decoderen.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-181">(In Azure, this method is Azure Resource Manager.) Then, when Service Fabric deploys hello service package toohello machine, it can decrypt hello secret.</span></span> <span data-ttu-id="f8fa6-182">Met behulp van Hallo geheim samen met de accountnaam Hallo vervolgens verificatie met Hallo container opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-182">By using hello secret along with hello account name, it can then authenticate with hello container repository.</span></span>

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

## <span data-ttu-id="f8fa6-183"><a name ="Portsection"></a>Container toohost poorttoewijzing configureren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-183"><a name ="Portsection"></a> Configure container toohost port mapping</span></span>
<span data-ttu-id="f8fa6-184">U kunt een host gebruikt poort toocommunicate configureren met Hallo-container door te geven een `PortBinding` Hallo-toepassingsmanifest.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-184">You can configure a host port used toocommunicate with hello container by specifying a `PortBinding` in hello application manifest.</span></span> <span data-ttu-id="f8fa6-185">Hallo poort binding maps Hallo poort toowhich Hallo service luistert binnen Hallo container tooa poort op Hallo host.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-185">hello port binding maps hello port toowhich hello service is listening inside hello container tooa port on hello host.</span></span>

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

## <a name="configure-container-to-container-discovery-and-communication"></a><span data-ttu-id="f8fa6-186">Container voor container detectie en communicatie configureren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-186">Configure container-to-container discovery and communication</span></span>
<span data-ttu-id="f8fa6-187">U kunt Hallo `PortBinding` element toomap een eindpunt van de container poort tooan in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-187">You can use hello `PortBinding` element toomap a container port tooan endpoint in hello service manifest.</span></span> <span data-ttu-id="f8fa6-188">Hallo in Hallo voorbeeld te volgen, eindpunt `Endpoint1` geeft een vaste poort, 8905.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-188">In hello following example, hello endpoint `Endpoint1` specifies a fixed port, 8905.</span></span> <span data-ttu-id="f8fa6-189">Ook u kunt opgeven geen poort op alle in dat geval een willekeurige poort van toepassingspoortbereik Hallo-cluster wordt gekozen voor u.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-189">It can also specify no port at all, in which case a random port from hello cluster's application port range is chosen for you.</span></span>


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
<span data-ttu-id="f8fa6-190">Als u een eindpunt opgeeft, met behulp van Hallo `Endpoint` tag op in Hallo servicemanifest van een gast-container, Service Fabric kan automatisch publiceren van dit eindpunt toohello Naming service.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-190">If you specify an endpoint, using hello `Endpoint` tag in hello service manifest of a guest container, Service Fabric can automatically publish this endpoint toohello Naming service.</span></span> <span data-ttu-id="f8fa6-191">Andere services die worden uitgevoerd in de cluster Hallo kunnen dus deze container Hallo REST-query's gebruiken voor het oplossen van detecteren.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-191">Other services that are running in hello cluster can thus discover this container using hello REST queries for resolving.</span></span>

<span data-ttu-id="f8fa6-192">Registreert Hello Naming service, kunt u container-container-communicatie uitvoeren binnen uw container via Hallo [omgekeerde proxy](service-fabric-reverseproxy.md).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-192">By registering with hello Naming service, you can perform container-to-container communication within your container by using hello [reverse proxy](service-fabric-reverseproxy.md).</span></span> <span data-ttu-id="f8fa6-193">Communicatie wordt uitgevoerd door Hallo omgekeerde proxy http-luisterpoort en Hallo-naam van het Hallo-services die u toocommunicate met als omgevingsvariabelen wilt.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-193">Communication is performed by providing hello reverse proxy http listening port and hello name of hello services that you want toocommunicate with as environment variables.</span></span> <span data-ttu-id="f8fa6-194">Zie de volgende sectie Hallo voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-194">For more information, see hello next section.</span></span> 

## <a name="configure-and-set-environment-variables"></a><span data-ttu-id="f8fa6-195">Omgevingsvariabelen configureren en instellen</span><span class="sxs-lookup"><span data-stu-id="f8fa6-195">Configure and set environment variables</span></span>
<span data-ttu-id="f8fa6-196">Omgevingsvariabelen kunnen worden opgegeven voor elk codepakket in Hallo servicemanifest.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-196">Environment variables can be specified for each code package in hello service manifest.</span></span> <span data-ttu-id="f8fa6-197">Deze functie is beschikbaar voor alle services, ongeacht of ze zijn geïmplementeerd als containers, processen of uitvoerbare gastbestanden.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-197">This feature is available for all services irrespective of whether they are deployed as containers or processes or guest executables.</span></span> <span data-ttu-id="f8fa6-198">U kunt de omgevingsvariabele waarden in de toepassing hello manifest of geef ze tijdens de implementatie als toepassingsparameters overschrijven.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-198">You can override environment variable values in hello application manifest or specify them during deployment as application parameters.</span></span>

<span data-ttu-id="f8fa6-199">Hallo volgende service manifest XML-fragment toont een voorbeeld van hoe de omgevingsvariabelen toospecify voor een codepakket:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-199">hello following service manifest XML snippet shows an example of how toospecify environment variables for a code package:</span></span>

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

<span data-ttu-id="f8fa6-200">Deze omgevingsvariabelen kunnen worden genegeerd op toepassingsniveau voor Hallo-manifest:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-200">These environment variables can be overridden at hello application manifest level:</span></span>

```xml
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="FrontendServicePackage" ServiceManifestVersion="1.0"/>
        <EnvironmentOverrides CodePackageRef="FrontendService.Code">
            <EnvironmentVariable Name="BackendServiceName" Value="[BackendSvc]"/>
            <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
        </EnvironmentOverrides>
    </ServiceManifestImport>
```

<span data-ttu-id="f8fa6-201">In het vorige voorbeeld hello, we een expliciete waarde opgegeven voor Hallo `HttpGateway` omgevingsvariabele (19000), terwijl op Hallo-waarde voor `BackendServiceName` parameter via Hallo `[BackendSvc]` parameter van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-201">In hello previous example, we specified an explicit value for hello `HttpGateway` environment variable (19000), while we set hello value for `BackendServiceName` parameter via hello `[BackendSvc]` application parameter.</span></span> <span data-ttu-id="f8fa6-202">Deze instellingen kunt u toospecify Hallo waarde voor `BackendServiceName`wanneer u Hallo-toepassing implementeren en geen vaste waarde in het manifest Hallo waarde.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-202">These settings enable you toospecify hello value for `BackendServiceName`value when you deploy hello application and not have a fixed value in hello manifest.</span></span>

## <a name="configure-isolation-mode"></a><span data-ttu-id="f8fa6-203">Isolatiemodus configureren</span><span class="sxs-lookup"><span data-stu-id="f8fa6-203">Configure isolation mode</span></span>

<span data-ttu-id="f8fa6-204">Windows ondersteunt twee isolatiemodi voor containers - proces en Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-204">Windows supports two isolation modes for containers - process and Hyper-V.</span></span>  <span data-ttu-id="f8fa6-205">Met isolatiemodus voor Hallo Hallo alle Hallo containers die worden uitgevoerd op dezelfde host machine share Hallo kernel met Hallo host.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-205">With hello process isolation mode, all hello containers running on hello same host machine share hello kernel with hello host.</span></span> <span data-ttu-id="f8fa6-206">Hallo kernels zijn met de isolatiemodus Hallo Hyper-V, tussen elke Hyper-V-container en Hallo containerhost geïsoleerd.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-206">With hello Hyper-V isolation mode, hello kernels are isolated between each Hyper-V container and hello container host.</span></span> <span data-ttu-id="f8fa6-207">Hallo isolatiemodus is opgegeven in Hallo `ContainerHostPolicies` -tag in het manifestbestand van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-207">hello isolation mode is specified in hello `ContainerHostPolicies` tag in hello application manifest file.</span></span>  <span data-ttu-id="f8fa6-208">Hallo isolatie modi die kunnen worden opgegeven `process`, `hyperv`, en `default`.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-208">hello isolation modes that can be specified are `process`, `hyperv`, and `default`.</span></span> <span data-ttu-id="f8fa6-209">Hallo `default` isolatiemodus standaardwaarden te`process` op Windows-Server fungeert als host en de standaardinstellingen te`hyperv` op hosts met Windows 10.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-209">hello `default` isolation mode defaults too`process` on Windows Server hosts, and defaults too`hyperv` on Windows 10 hosts.</span></span>  <span data-ttu-id="f8fa6-210">Hallo volgende fragment toont hoe Hallo isolatiemodus is opgegeven in het manifestbestand van de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="f8fa6-210">hello following snippet shows how hello isolation mode is specified in hello application manifest file.</span></span>

```xml
   <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv">
```


## <a name="complete-examples-for-application-and-service-manifest"></a><span data-ttu-id="f8fa6-211">Voorbeelden voor de toepassing en servicemanifest voltooien</span><span class="sxs-lookup"><span data-stu-id="f8fa6-211">Complete examples for application and service manifest</span></span>

<span data-ttu-id="f8fa6-212">Hier volgt een voorbeeld-toepassingsmanifest:</span><span class="sxs-lookup"><span data-stu-id="f8fa6-212">An example application manifest follows:</span></span>

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

<span data-ttu-id="f8fa6-213">Hier volgt een voorbeeld van de servicemanifest (opgegeven in Hallo voorafgaand aan het toepassingsmanifest):</span><span class="sxs-lookup"><span data-stu-id="f8fa6-213">An example service manifest (specified in hello preceding application manifest) follows:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="f8fa6-214">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8fa6-214">Next steps</span></span>
<span data-ttu-id="f8fa6-215">Nu u een beperkte service hebt geïmplementeerd, kunt u nagaan hoe toomanage levenscyclus door te lezen [Service Fabric-toepassing lifecycle](service-fabric-application-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="f8fa6-215">Now that you have deployed a containerized service, learn how toomanage its lifecycle by reading [Service Fabric application lifecycle](service-fabric-application-lifecycle.md).</span></span>

* [<span data-ttu-id="f8fa6-216">Overzicht van Service Fabric en containers</span><span class="sxs-lookup"><span data-stu-id="f8fa6-216">Overview of Service Fabric and containers</span></span>](service-fabric-containers-overview.md)
* <span data-ttu-id="f8fa6-217">Voor een voorbeeld afhandeling [Service Fabric-container codevoorbeelden op GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span><span class="sxs-lookup"><span data-stu-id="f8fa6-217">For an example, checkout [Service Fabric container code samples on GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-containers)</span></span>
