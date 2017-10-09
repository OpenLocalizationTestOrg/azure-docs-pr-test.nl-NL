---
title: aaaCI/CD met Azure Container Service-Engine en Swarm-modus | Microsoft Docs
description: Azure Container Service-Engine gebruiken met Docker Swarm-modus, een Azure Container register- en Visual Studio Team Services toodeliver continu een toepassing met meerdere container .NET Core
services: container-service
documentationcenter: " "
author: diegomrtnzg
manager: esterdnb
tags: acs, azure-container-service, acs-engine
keywords: Docker, Containers Micro-services, Swarm, Azure, Visual Studio Team Services, DevOps, ACS-Engine
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/27/2017
ms.author: diegomrtnzg
ms.custom: mvc
ms.openlocfilehash: 040522c452f7ea0ce3c92f2fe57b1c141b97e380
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="14106-104">Volledige CI/CD pijplijn toodeploy een toepassing met meerdere container in Azure Container Service met de ACS-Engine en Docker Swarm-modus met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="14106-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="14106-105">*In dit artikel is gebaseerd op [volledige CI/CD pipeline toodeploy een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentatie*</span><span class="sxs-lookup"><span data-stu-id="14106-105">*This article is based on [Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="14106-106">Tegenwoordig een van de Hallo grootste uitdagingen wanneer kunnen toodeliver moderne toepassingen ontwikkelt voor Hallo cloud wordt deze toepassingen continu.</span><span class="sxs-lookup"><span data-stu-id="14106-106">Nowadays, One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="14106-107">In dit artikel leert u hoe tooimplement een volledige continue integratie en implementatie (CI/CD) pipeline gebruiken:</span><span class="sxs-lookup"><span data-stu-id="14106-107">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="14106-108">Azure Container Service-Engine met Docker Swarm-modus</span><span class="sxs-lookup"><span data-stu-id="14106-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="14106-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="14106-109">Azure Container Registry</span></span>
* <span data-ttu-id="14106-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="14106-110">Visual Studio Team Services</span></span>

<span data-ttu-id="14106-111">In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), ontwikkelde met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="14106-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="14106-112">Hallo-toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:</span><span class="sxs-lookup"><span data-stu-id="14106-112">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="14106-114">Hallo-doel is toodeliver deze toepassingen continu in een modus voor Docker Swarm-cluster met behulp van Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="14106-114">hello objective is toodeliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="14106-115">Hallo volgende afbeelding details van deze continue levering pijplijn:</span><span class="sxs-lookup"><span data-stu-id="14106-115">hello following figure details this continuous delivery pipeline:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="14106-117">Hier volgt een korte uitleg van Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="14106-117">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="14106-118">Codewijzigingen zijn doorgevoerd toohello source code opslagplaats (in dit geval GitHub)</span><span class="sxs-lookup"><span data-stu-id="14106-118">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="14106-119">GitHub activeert een bouwen in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="14106-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="14106-120">Visual Studio Team Services Hallo meest recente versie van Hallo bronnen opgehaald en maakt alle Hallo installatiekopieën waaruit Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="14106-120">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="14106-121">Visual Studio Team Services pushes elke installatiekopie tooa Docker register gemaakt met behulp van hello Azure Container Registry-service</span><span class="sxs-lookup"><span data-stu-id="14106-121">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="14106-122">Visual Studio Team Services activeert een nieuwe release</span><span class="sxs-lookup"><span data-stu-id="14106-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="14106-123">Hallo release bepaalde opdrachten via SSH op master clusterknooppunt van hello Azure container service uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="14106-123">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="14106-124">Docker Swarm modus op Hallo cluster haalt Hallo meest recente versie van Hallo installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="14106-124">Docker Swarm Mode on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="14106-125">nieuwe versie van de toepassing hello Hello wordt geïmplementeerd met behulp van Docker-Stack</span><span class="sxs-lookup"><span data-stu-id="14106-125">hello new version of hello application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="14106-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="14106-126">Prerequisites</span></span>

<span data-ttu-id="14106-127">Voordat u deze zelfstudie begint, moet u toocomplete Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="14106-127">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="14106-128">Een modus Swarm-cluster maken in Azure Container Service met de ACS-Engine</span><span class="sxs-lookup"><span data-stu-id="14106-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="14106-129">Verbinding maken met de Hallo Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="14106-129">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="14106-130">Een Azure container registry maken</span><span class="sxs-lookup"><span data-stu-id="14106-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="14106-131">Een Visual Studio Team Services-account en team project zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="14106-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="14106-132">Vertakken Hallo GitHub-opslagplaats tooyour GitHub-account</span><span class="sxs-lookup"><span data-stu-id="14106-132">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="14106-133">Hallo orchestrator Docker Swarm in Azure Container Service maakt gebruik van verouderde zelfstandige Swarm.</span><span class="sxs-lookup"><span data-stu-id="14106-133">hello Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="14106-134">Op dit moment Hallo geïntegreerd [Swarm modus](https://docs.docker.com/engine/swarm/) (in Docker 1.12 en hoger) is niet een ondersteunde orchestrator in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="14106-134">Currently, hello integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="14106-135">Daarom gebruiken we [ACS-Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), community-bijgedragen [snelstartsjabloon](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), of een Docker-oplossing in Hallo [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="14106-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in hello [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="14106-136">Stap 1: Uw Visual Studio Team Services-account configureren</span><span class="sxs-lookup"><span data-stu-id="14106-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="14106-137">In deze sectie configureert u uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="14106-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="14106-138">tooconfigure VSTS Services eindpunten in het project voor Visual Studio Team Services, klikt u op Hallo **instellingen** pictogram in het Hallo-werkbalk en selecteert u **Services**.</span><span class="sxs-lookup"><span data-stu-id="14106-138">tooconfigure VSTS Services Endpoints, in your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

![Open Services-eindpunt](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="14106-140">Verbinding maken met Visual Studio Team Services en Azure-account</span><span class="sxs-lookup"><span data-stu-id="14106-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="14106-141">Een verbinding tussen uw project VSTS en uw Azure-account instellen.</span><span class="sxs-lookup"><span data-stu-id="14106-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="14106-142">Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="14106-142">On hello left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="14106-143">tooauthorize VSTS toowork met uw Azure-account, selecteer uw **abonnement** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="14106-143">tooauthorize VSTS toowork with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio teamservices - autoriseren van Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="14106-145">Verbinding maken met Visual Studio teamservices en GitHub</span><span class="sxs-lookup"><span data-stu-id="14106-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="14106-146">Een verbinding tussen uw project VSTS en uw GitHub-account instellen.</span><span class="sxs-lookup"><span data-stu-id="14106-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="14106-147">Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="14106-147">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="14106-148">tooauthorize VSTS toowork met uw GitHub-account, klikt u op **autoriseren** en volg de procedure Hallo in Hallo-venster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="14106-148">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-tooyour-azure-container-service-cluster"></a><span data-ttu-id="14106-150">Verbinding maken met VSTS tooyour Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="14106-150">Connect VSTS tooyour Azure Container Service cluster</span></span>

<span data-ttu-id="14106-151">Hallo laatste stappen voordat u in Hallo CI/CD pipeline zijn tooconfigure externe verbindingen tooyour Docker Swarm-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="14106-151">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="14106-152">Voor Hallo Docker Swarm-cluster, voegt u een eindpunt van het type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="14106-152">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="14106-153">Voer vervolgens de gegevens van Hallo SSH-verbinding van uw Swarm-cluster (master knooppunt).</span><span class="sxs-lookup"><span data-stu-id="14106-153">Then enter hello SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="14106-155">Alle Hallo-configuratie wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="14106-155">All hello configuration is done now.</span></span> <span data-ttu-id="14106-156">In de volgende stappen hello maakt u Hallo CI/CD pijplijn die is gebaseerd en Docker Swarm-cluster van Hallo toepassing toohello implementeert.</span><span class="sxs-lookup"><span data-stu-id="14106-156">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="14106-157">Stap 2: Hallo build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="14106-157">Step 2: Create hello build definition</span></span>

<span data-ttu-id="14106-158">In deze stap maakt u een definitie van de build instellen voor uw project VSTS en Hallo build werkstroom definiëren voor de installatiekopieën van de container</span><span class="sxs-lookup"><span data-stu-id="14106-158">In this step, you set up a build definition for your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="14106-159">Initiële definitie setup</span><span class="sxs-lookup"><span data-stu-id="14106-159">Initial definition setup</span></span>

1. <span data-ttu-id="14106-160">de definitie van een build toocreate tooyour Visual Studio Team Services project en klik op verbinding **bouwen & Release**.</span><span class="sxs-lookup"><span data-stu-id="14106-160">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="14106-161">In Hallo **bouwen definities** sectie, klikt u op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="14106-161">In hello **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="14106-163">Selecteer Hallo **leeg proces**.</span><span class="sxs-lookup"><span data-stu-id="14106-163">Select hello **Empty process**.</span></span>

    ![Visual Studio teamservices - nieuwe, lege bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="14106-165">Klik vervolgens op Hallo **variabelen** tabblad en twee nieuwe variabelen maken: **RegistryURL** en **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="14106-165">Then, click hello **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="14106-166">Hallo-waarden van het register en het Cluster Agents DNS plakken.</span><span class="sxs-lookup"><span data-stu-id="14106-166">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio teamservices - variabelen Buildconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="14106-168">Op Hallo **bouwen definities** pagina, open Hallo **Triggers** tabblad en Hallo build toouse continue integratie met Hallo fork Hallo MyShop project dat u hebt gemaakt in Hallo vereisten configureren.</span><span class="sxs-lookup"><span data-stu-id="14106-168">On hello **Build Definitions** page, open hello **Triggers** tab and configure hello build toouse continuous integration with hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="14106-169">Selecteer **Batch wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="14106-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="14106-170">Zorg ervoor dat u selecteert *docker-linux* als Hallo **vertakking specificatie**.</span><span class="sxs-lookup"><span data-stu-id="14106-170">Make sure that you select *docker-linux* as hello **Branch specification**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="14106-172">Tot slot op Hallo **opties** tabblad en wachtrij Hallo-agent te configureren**gehost Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="14106-172">Finally, click hello **Options** tab and configure hello Default agent queue too**Hosted Linux Preview**.</span></span>

    ![Visual Studio teamservices - Agent de hostconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="14106-174">Hallo build werkstroom definiëren</span><span class="sxs-lookup"><span data-stu-id="14106-174">Define hello build workflow</span></span>
<span data-ttu-id="14106-175">de volgende stappen Hallo definiëren Hallo build werkstroom.</span><span class="sxs-lookup"><span data-stu-id="14106-175">hello next steps define hello build workflow.</span></span> <span data-ttu-id="14106-176">U moet eerst tooconfigure Hallo bron van Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="14106-176">First, you need tooconfigure hello source of hello code.</span></span> <span data-ttu-id="14106-177">toodo deze Selecteer **GitHub** en uw **opslagplaats** en **vertakking** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="14106-177">toodo it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio teamservices - configureren broncode](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="14106-179">Er zijn vijf container installatiekopieën toobuild voor Hallo *MyShop* toepassing.</span><span class="sxs-lookup"><span data-stu-id="14106-179">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="14106-180">Elke installatiekopie gebouwd met behulp van Hallo die dockerfile zich in Hallo projectmappen bevinden:</span><span class="sxs-lookup"><span data-stu-id="14106-180">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="14106-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="14106-181">ProductsApi</span></span>
* <span data-ttu-id="14106-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="14106-182">Proxy</span></span>
* <span data-ttu-id="14106-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="14106-183">RatingsApi</span></span>
* <span data-ttu-id="14106-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="14106-184">RecommandationsApi</span></span>
* <span data-ttu-id="14106-185">Winkelpagina</span><span class="sxs-lookup"><span data-stu-id="14106-185">ShopFront</span></span>

<span data-ttu-id="14106-186">U moet twee Docker-stappen voor elke installatiekopie, één toobuild Hallo afbeelding en één toopush Hallo image in hello Azure container register.</span><span class="sxs-lookup"><span data-stu-id="14106-186">You need two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="14106-187">tooadd een stap in Hallo build werkstroom, klikt u op **+ toevoegen build stap** en selecteer **Docker**.</span><span class="sxs-lookup"><span data-stu-id="14106-187">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="14106-189">Voor elke installatiekopie, configureert u één stap die gebruikmaakt van Hallo `docker build` opdracht.</span><span class="sxs-lookup"><span data-stu-id="14106-189">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="14106-191">Bouwen voor Hallo bewerking, selecteert u het register van de Container Azure hello **bouwen van een installatiekopie van een** actie en Hallo Dockerfile waarin elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="14106-191">For hello build operation, select your Azure Container Registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="14106-192">Set Hallo **werkmap** als hoofdmap Hallo Dockerfile, definieert u Hallo **Installatiekopienaam**, en selecteer **meest recente code bevatten**.</span><span class="sxs-lookup"><span data-stu-id="14106-192">Set hello **Working Directory** as hello Dockerfile root directory, define hello **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="14106-193">Hallo Installatiekopienaam toobe is in deze indeling: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="14106-193">hello Image Name has toobe in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="14106-194">Vervang **[NAME]** met de naam van de installatiekopie Hallo:</span><span class="sxs-lookup"><span data-stu-id="14106-194">Replace **[NAME]** with hello image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="14106-195">Voor elke installatiekopie, configureert u een tweede stap die gebruikmaakt van Hallo `docker push` opdracht.</span><span class="sxs-lookup"><span data-stu-id="14106-195">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="14106-197">Voor Hallo push-bewerking, selecteert u het register Azure container hello **een installatiekopie van een Push** actie, Voer Hallo **installatiekopie met de naam** die is ingebouwd in de vorige stap Hallo en selecteer **meest recente code opnemen** .</span><span class="sxs-lookup"><span data-stu-id="14106-197">For hello push operation, select your Azure container registry, hello **Push an image** action, enter hello **Image Name** that is built in hello previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="14106-198">Nadat u hebt configureren Hallo build en stappen voor elk van de vijf installatiekopieën Hallo push, drie meer stappen in Hallo bouwen werkstroom toevoegen.</span><span class="sxs-lookup"><span data-stu-id="14106-198">After you configure hello build and push steps for each of hello five images, add three more steps in hello build workflow.</span></span>

   ![Visual Studio teamservices - toevoegen opdrachtregelprogramma taak](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="14106-200">Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *RegistryURL* exemplaar in Hallo docker-compose.yml-bestand met Hallo RegistryURL variabele.</span><span class="sxs-lookup"><span data-stu-id="14106-200">A command-line task that uses a bash script tooreplace hello *RegistryURL* occurrence in hello docker-compose.yml file with hello RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio teamservices - Update opstellen-bestand met de Register-URL](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="14106-202">Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *AgentURL* exemplaar in Hallo docker-compose.yml-bestand met Hallo AgentURL variabele.</span><span class="sxs-lookup"><span data-stu-id="14106-202">A command-line task that uses a bash script tooreplace hello *AgentURL* occurrence in hello docker-compose.yml file with hello AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="14106-203">Een taak die wordt neergezet Hallo bijgewerkt opstellen bestand als een artefact build zodat deze kan worden gebruikt in Hallo-versie.</span><span class="sxs-lookup"><span data-stu-id="14106-203">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="14106-204">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14106-204">See hello following screen for details.</span></span>

         ![Visual Studio teamservices - publiceren artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="14106-207">Klik op **opslaan en wachtrij** tootest de definitie van de build.</span><span class="sxs-lookup"><span data-stu-id="14106-207">Click **Save & queue** tootest your build definition.</span></span>

   ![Visual Studio teamservices - opslaan en wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio teamservices - nieuwe wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="14106-210">Als hello **bouwen** juist is, hebt u toosee dit scherm:</span><span class="sxs-lookup"><span data-stu-id="14106-210">If hello **Build** is correct, you have toosee this screen:</span></span>

  ![Visual Studio teamservices - Build is voltooid](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="14106-212">Stap 3: Hallo release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="14106-212">Step 3: Create hello release definition</span></span>

<span data-ttu-id="14106-213">Visual Studio Team Services kunt u te[releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="14106-213">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="14106-214">U kunt continue implementatie toomake ervoor dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen.</span><span class="sxs-lookup"><span data-stu-id="14106-214">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="14106-215">U kunt een omgeving met uw Azure Container Service Docker Swarm modus cluster maken.</span><span class="sxs-lookup"><span data-stu-id="14106-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio teamservices - Release tooACS](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="14106-217">Installatie van de eerste release</span><span class="sxs-lookup"><span data-stu-id="14106-217">Initial release setup</span></span>

1. <span data-ttu-id="14106-218">toocreate de definitie van een release, klikt u op **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="14106-218">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="14106-219">tooconfigure hello artefact bron, klikt u op **artefacten** > **een artefact koppelingsbron**.</span><span class="sxs-lookup"><span data-stu-id="14106-219">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="14106-220">Deze nieuwe versie definitie toohello build die u hebt gedefinieerd in de vorige stap Hallo hier een koppeling.</span><span class="sxs-lookup"><span data-stu-id="14106-220">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="14106-221">Hallo docker-compose.yml-bestand is hierna is beschikbaar in Hallo release proces.</span><span class="sxs-lookup"><span data-stu-id="14106-221">After that, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="14106-223">tooconfigure hello release worden geactiveerd, klikt u op **Triggers** en selecteer **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="14106-223">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="14106-224">Set Hallo trigger op Hallo dezelfde artefact-bron.</span><span class="sxs-lookup"><span data-stu-id="14106-224">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="14106-225">Deze instelling zorgt ervoor dat er een nieuwe release wordt gestart wanneer Hallo build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="14106-225">This setting ensures that a new release starts when hello build completes successfully.</span></span>

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="14106-227">tooconfigure hello release variabelen, klikt u op **variabelen** en selecteer **+ variabele** toocreate drie nieuwe variabelen met Hallo-info van Hallo register: **docker.username**, **docker.password**, en **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="14106-227">tooconfigure hello release variables, click **Variables** and select **+Variable** toocreate three new variables with hello info of hello registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="14106-228">Hallo-waarden van het register en het Cluster Agents DNS plakken.</span><span class="sxs-lookup"><span data-stu-id="14106-228">Paste hello values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="14106-230">Zoals u in het vorige scherm hello, klikt u op Hallo **vergrendeling** checkbox in docker.password.</span><span class="sxs-lookup"><span data-stu-id="14106-230">As shown on hello previous screen, click hello **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="14106-231">Deze instelling is belangrijk toorestrict Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="14106-231">This setting is important toorestrict hello password.</span></span>
    >

### <a name="define-hello-release-workflow"></a><span data-ttu-id="14106-232">Hallo release werkstroom definiëren</span><span class="sxs-lookup"><span data-stu-id="14106-232">Define hello release workflow</span></span>

<span data-ttu-id="14106-233">Hallo release werkstroom bestaat uit twee taken die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="14106-233">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="14106-234">Configureren van een taak toosecurely kopie Hallo opstellen bestand tooa *implementeren* map op Hallo Docker Swarm-hoofdknooppunt, met behulp van Hallo SSH-verbinding u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="14106-234">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="14106-235">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14106-235">See hello following screen for details.</span></span>
    
    <span data-ttu-id="14106-236">Bronmap:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="14106-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="14106-238">Configureren van een tweede taak tooexecute een opdracht bash toorun `docker` en `docker stack deploy` opdrachten op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="14106-238">Configure a second task tooexecute a bash command toorun `docker` and `docker stack deploy` commands on hello master node.</span></span> <span data-ttu-id="14106-239">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="14106-239">See hello following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="14106-241">Hallo-opdracht uitgevoerd op Hallo master gebruikt Hallo Docker CLI en Hallo Docker Compose CLI toodo Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="14106-241">hello command executed on hello master uses hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="14106-242">Meld u bij toohello Azure container register (hierbij drie build-variabelen die zijn gedefinieerd in Hallo **variabelen** tabblad)</span><span class="sxs-lookup"><span data-stu-id="14106-242">Log in toohello Azure container registry (it uses three build variables that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="14106-243">Hallo definiëren **DOCKER_HOST** variabele toowork met Hallo Swarm-eindpunt (: 2375)</span><span class="sxs-lookup"><span data-stu-id="14106-243">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="14106-244">Navigeer toohello *implementeren* map die is gemaakt door Hallo voorafgaand aan beveiligde kopieertaak en die Hallo docker-compose.yml-bestand bevat</span><span class="sxs-lookup"><span data-stu-id="14106-244">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="14106-245">Uitvoeren van `docker stack deploy` opdrachten die pull-hallo nieuwe afbeeldingen en Hallo containers te maken.</span><span class="sxs-lookup"><span data-stu-id="14106-245">Execute `docker stack deploy` commands that pull hello new images and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="14106-246">Zoals u in het vorige scherm hello, laat u Hallo **mislukken op STDERR** selectievakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="14106-246">As shown on hello previous screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="14106-247">Deze instelling kunt ons toocomplete Hallo release proces vanwege te`docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op Hallo standaardfout uitvoer wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="14106-247">This setting allows us toocomplete hello release process due too`docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="14106-248">Als u het selectievakje Hallo inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens het Hallo-release, zelfs als alles goed gaat.</span><span class="sxs-lookup"><span data-stu-id="14106-248">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="14106-249">Sla deze definitie voor de nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="14106-249">Save this new release definition.</span></span>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="14106-250">Stap 4: Testen Hallo CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="14106-250">Step 4: Test hello CI/CD pipeline</span></span>

<span data-ttu-id="14106-251">Nu u klaar bent met Hallo configuratie, is het tijd tootest dit nieuwe CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="14106-251">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="14106-252">Hallo gemakkelijkste manier tootest tooupdate Hallo source code en doorvoeren Hallo is gewijzigd in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="14106-252">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="14106-253">Enkele seconden nadat u push-Hallo code, ziet u een nieuwe build uitgevoerd in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="14106-253">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="14106-254">Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en Hallo nieuwe versie van de toepassing hello op Hallo Azure Container Service-cluster wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="14106-254">Once completed successfully, a new release is triggered and deployed hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="14106-255">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="14106-255">Next steps</span></span>

* <span data-ttu-id="14106-256">Zie voor meer informatie over CI/CD met Visual Studio Team Services, Hallo [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="14106-256">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="14106-257">Zie voor meer informatie over de ACS-Engine Hallo [ACS-Engine GitHub-repo-](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="14106-257">For more information about ACS Engine, see hello [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="14106-258">Zie voor meer informatie over Docker Swarm modus Hallo [Docker Swarm modus overzicht](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="14106-258">For more information about Docker Swarm mode, see hello [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
