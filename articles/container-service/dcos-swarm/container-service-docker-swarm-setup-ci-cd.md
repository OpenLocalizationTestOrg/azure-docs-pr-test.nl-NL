---
title: aaaCI/CD met Azure Container Service- en Swarm | Microsoft Docs
description: Gebruik Azure Container Service met Docker Swarm, een Azure Container register- en Visual Studio Team Services toodeliver continu een toepassing met meerdere container .NET Core
services: container-service
documentationcenter: " "
author: jcorioland
manager: pierlag
tags: acs, azure-container-service
keywords: Docker, Containers Micro-services, Swarm, Azure, Visual Studio teamservices, DevOps
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/08/2016
ms.author: jucoriol
ms.custom: mvc
ms.openlocfilehash: 35348800aa620469fb62ab3e5a02b33834359446
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="full-cicd-pipeline-toodeploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="3dc65-104">Volledige CI/CD pijplijn toodeploy een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3dc65-104">Full CI/CD pipeline toodeploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="3dc65-105">Een van de Hallo grootste uitdagingen wanneer kunnen toodeliver moderne toepassingen ontwikkelt voor Hallo cloud wordt deze toepassingen continu.</span><span class="sxs-lookup"><span data-stu-id="3dc65-105">One of hello biggest challenges when developing modern applications for hello cloud is being able toodeliver these applications continuously.</span></span> <span data-ttu-id="3dc65-106">In dit artikel leert u meer informatie over het tooimplement een volledige continue integratie en implementatie (CI/CD)-pijplijn met Azure Container Service met Docker Swarm, het register van Azure-Container en Visual Studio Team Services bouwen en releasebeheer.</span><span class="sxs-lookup"><span data-stu-id="3dc65-106">In this article, you learn how tooimplement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="3dc65-107">In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ontwikkelde met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="3dc65-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="3dc65-108">Hallo-toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:</span><span class="sxs-lookup"><span data-stu-id="3dc65-108">hello application is composed of four different services: three web APIs and one web front end:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="3dc65-110">Hallo-doel is toodeliver deze toepassingen continu in een Docker Swarm-cluster met behulp van Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3dc65-110">hello objective is toodeliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="3dc65-111">Hallo volgende afbeelding details van deze continue levering pijplijn:</span><span class="sxs-lookup"><span data-stu-id="3dc65-111">hello following figure details this continuous delivery pipeline:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="3dc65-113">Hier volgt een korte uitleg van Hallo stappen:</span><span class="sxs-lookup"><span data-stu-id="3dc65-113">Here is a brief explanation of hello steps:</span></span>

1. <span data-ttu-id="3dc65-114">Codewijzigingen zijn doorgevoerd toohello source code opslagplaats (in dit geval GitHub)</span><span class="sxs-lookup"><span data-stu-id="3dc65-114">Code changes are committed toohello source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="3dc65-115">GitHub activeert een bouwen in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="3dc65-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="3dc65-116">Visual Studio Team Services Hallo meest recente versie van Hallo bronnen opgehaald en maakt alle Hallo installatiekopieën waaruit Hallo-toepassing</span><span class="sxs-lookup"><span data-stu-id="3dc65-116">Visual Studio Team Services gets hello latest version of hello sources and builds all hello images that compose hello application</span></span> 
4. <span data-ttu-id="3dc65-117">Visual Studio Team Services pushes elke installatiekopie tooa Docker register gemaakt met behulp van hello Azure Container Registry-service</span><span class="sxs-lookup"><span data-stu-id="3dc65-117">Visual Studio Team Services pushes each image tooa Docker registry created using hello Azure Container Registry service</span></span> 
5. <span data-ttu-id="3dc65-118">Visual Studio Team Services activeert een nieuwe release</span><span class="sxs-lookup"><span data-stu-id="3dc65-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="3dc65-119">Hallo release bepaalde opdrachten via SSH op master clusterknooppunt van hello Azure container service uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="3dc65-119">hello release runs some commands using SSH on hello Azure container service cluster master node</span></span> 
7. <span data-ttu-id="3dc65-120">Docker Swarm op Hallo cluster worden Hallo meest recente versie van het Hallo-installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="3dc65-120">Docker Swarm on hello cluster pulls hello latest version of hello images</span></span> 
8. <span data-ttu-id="3dc65-121">nieuwe versie van de toepassing hello Hallo wordt geïmplementeerd met behulp van Docker Compose</span><span class="sxs-lookup"><span data-stu-id="3dc65-121">hello new version of hello application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3dc65-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3dc65-122">Prerequisites</span></span>

<span data-ttu-id="3dc65-123">Voordat u deze zelfstudie begint, moet u toocomplete Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="3dc65-123">Before starting this tutorial, you need toocomplete hello following tasks:</span></span>

- [<span data-ttu-id="3dc65-124">Een Swarm-cluster in Azure Container Service maken</span><span class="sxs-lookup"><span data-stu-id="3dc65-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="3dc65-125">Verbinding maken met de Hallo Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="3dc65-125">Connect with hello Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="3dc65-126">Een Azure container registry maken</span><span class="sxs-lookup"><span data-stu-id="3dc65-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="3dc65-127">Een Visual Studio Team Services-account en team project zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="3dc65-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="3dc65-128">Vertakken Hallo GitHub-opslagplaats tooyour GitHub-account</span><span class="sxs-lookup"><span data-stu-id="3dc65-128">Fork hello GitHub repository tooyour GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="3dc65-129">U moet ook een machine Ubuntu (14.04 of 16.04) met Docker geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="3dc65-130">Deze computer wordt gebruikt door Visual Studio Team Services tijdens Hallo bouwen en de vrijgave van processen.</span><span class="sxs-lookup"><span data-stu-id="3dc65-130">This machine is used by Visual Studio Team Services during hello build and release processes.</span></span> <span data-ttu-id="3dc65-131">Eenzijdige toocreate deze machine is beschikbaar in Hallo toouse Hallo-installatiekopie [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="3dc65-131">One way toocreate this machine is toouse hello image available in hello [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="3dc65-132">Stap 1: Uw Visual Studio Team Services-account configureren</span><span class="sxs-lookup"><span data-stu-id="3dc65-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="3dc65-133">In deze sectie configureert u uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="3dc65-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="3dc65-134">Een Visual Studio Team Services Linux build-agent configureren</span><span class="sxs-lookup"><span data-stu-id="3dc65-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="3dc65-135">toocreate Docker-installatiekopieën en push die deze installatiekopieën naar een Azure container register van een Visual Studio Team Services bouwen, moet u tooregister een Linux-agent.</span><span class="sxs-lookup"><span data-stu-id="3dc65-135">toocreate Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need tooregister a Linux agent.</span></span> <span data-ttu-id="3dc65-136">U hebt deze installatieopties:</span><span class="sxs-lookup"><span data-stu-id="3dc65-136">You have these installation options:</span></span>

* [<span data-ttu-id="3dc65-137">Een op Linux-agent implementeren</span><span class="sxs-lookup"><span data-stu-id="3dc65-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="3dc65-138">Docker toorun Hallo VSTS agent gebruiken</span><span class="sxs-lookup"><span data-stu-id="3dc65-138">Use Docker toorun hello VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-hello-docker-integration-vsts-extension"></a><span data-ttu-id="3dc65-139">Hallo Docker-integratie VSTS uitbreiding installeren</span><span class="sxs-lookup"><span data-stu-id="3dc65-139">Install hello Docker Integration VSTS extension</span></span>

<span data-ttu-id="3dc65-140">Microsoft biedt een uitbreiding toowork VSTS gebouwd met Docker en de vrijgave van processen.</span><span class="sxs-lookup"><span data-stu-id="3dc65-140">Microsoft provides a VSTS extension toowork with Docker in build and release processes.</span></span> <span data-ttu-id="3dc65-141">Deze uitbreiding is beschikbaar in Hallo [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="3dc65-141">This extension is available in hello [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="3dc65-142">Klik op **installeren** tooadd deze extensie tooyour VSTS account:</span><span class="sxs-lookup"><span data-stu-id="3dc65-142">Click **Install** tooadd this extension tooyour VSTS account:</span></span>

![Hallo Docker-integratie installeren](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="3dc65-144">U kunt tooconnect tooyour VSTS rekening met uw referenties wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-144">You are asked tooconnect tooyour VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="3dc65-145">Verbinding maken met Visual Studio teamservices en GitHub</span><span class="sxs-lookup"><span data-stu-id="3dc65-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="3dc65-146">Een verbinding tussen uw project VSTS en uw GitHub-account instellen.</span><span class="sxs-lookup"><span data-stu-id="3dc65-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="3dc65-147">Klik in het project voor Visual Studio Team Services, op Hallo **instellingen** pictogram in het Hallo-werkbalk en selecteert u **Services**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-147">In your Visual Studio Team Services project, click hello **Settings** icon in hello toolbar, and select **Services**.</span></span>

    ![Visual Studio teamservices - externe verbinding](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="3dc65-149">Klik aan de linkerkant Hallo op **nieuwe Service-eindpunt** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-149">On hello left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio teamservices - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="3dc65-151">tooauthorize VSTS toowork met uw GitHub-account, klikt u op **autoriseren** en volg de procedure Hallo in Hallo-venster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="3dc65-151">tooauthorize VSTS toowork with your GitHub account, click **Authorize** and follow hello procedure in hello window that opens.</span></span>

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-tooyour-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="3dc65-153">Verbinding maken met VSTS tooyour Azure container register en Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="3dc65-153">Connect VSTS tooyour Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="3dc65-154">Hallo laatste stappen voordat u in Hallo CI/CD pipeline zijn tooconfigure externe verbindingen tooyour container register en uw Docker Swarm-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="3dc65-154">hello last steps before getting into hello CI/CD pipeline are tooconfigure external connections tooyour container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="3dc65-155">In Hallo **Services** instellingen van uw project Visual Studio Team Services, Voeg een service-eindpunt van het type **Docker-register**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-155">In hello **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="3dc65-156">Voer in Hallo pop-upvenster dat wordt geopend, Hallo-URL en referenties op Hallo van uw Azure-container-register.</span><span class="sxs-lookup"><span data-stu-id="3dc65-156">In hello popup that opens, enter hello URL and hello credentials of your Azure container registry.</span></span>

    ![Visual Studio teamservices - Docker-register](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="3dc65-158">Voor Hallo Docker Swarm-cluster, voegt u een eindpunt van het type **SSH**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-158">For hello Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="3dc65-159">Voer vervolgens de gegevens van Hallo SSH-verbinding van uw Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="3dc65-159">Then enter hello SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="3dc65-161">Alle Hallo-configuratie wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-161">All hello configuration is done now.</span></span> <span data-ttu-id="3dc65-162">In de volgende stappen hello maakt u Hallo CI/CD pijplijn die is gebaseerd en Docker Swarm-cluster van Hallo toepassing toohello implementeert.</span><span class="sxs-lookup"><span data-stu-id="3dc65-162">In hello next steps, you create hello CI/CD pipeline that builds and deploys hello application toohello Docker Swarm cluster.</span></span> 

## <a name="step-2-create-hello-build-definition"></a><span data-ttu-id="3dc65-163">Stap 2: Hallo build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="3dc65-163">Step 2: Create hello build definition</span></span>

<span data-ttu-id="3dc65-164">In deze stap maakt u een build definitionfor instellen met uw project VSTS en Hallo build werkstroom definiëren voor de installatiekopieën van de container</span><span class="sxs-lookup"><span data-stu-id="3dc65-164">In this step, you set up a build definitionfor your VSTS project and define hello build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="3dc65-165">Initiële definitie setup</span><span class="sxs-lookup"><span data-stu-id="3dc65-165">Initial definition setup</span></span>

1. <span data-ttu-id="3dc65-166">de definitie van een build toocreate tooyour Visual Studio Team Services project en klik op verbinding **bouwen & Release**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-166">toocreate a build definition, connect tooyour Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="3dc65-167">In Hallo **bouwen definities** sectie, klikt u op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-167">In hello **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="3dc65-168">Selecteer Hallo **leeg** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3dc65-168">Select hello **Empty** template.</span></span>

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="3dc65-170">Nieuwe build Hallo configureren met een GitHub-opslagplaats bron, selectievakje **continue integratie**, en selecteer Hallo agent wachtrij waar u uw Linux-agent is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-170">Configure hello new build with a GitHub repository source, check **Continuous integration**, and select hello agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="3dc65-171">Klik op **maken** toocreate Hallo bouwen definitie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-171">Click **Create** toocreate hello build definition.</span></span>

    ![Visual Studio teamservices - maken Build-definitie](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="3dc65-173">Op Hallo **bouwen definities** pagina, opent u eerst Hallo **opslagplaats** tabblad en Hallo build toouse Hallo fork Hallo MyShop project dat u hebt gemaakt in Hallo vereisten configureren.</span><span class="sxs-lookup"><span data-stu-id="3dc65-173">On hello **Build Definitions** page, first open hello **Repository** tab and configure hello build toouse hello fork of hello MyShop project that you created in hello prerequisites.</span></span> <span data-ttu-id="3dc65-174">Zorg ervoor dat u selecteert *acs docs* als Hallo **standaardvertakking**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-174">Make sure that you select *acs-docs* as hello **Default branch**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="3dc65-176">Op Hallo **Triggers** tabblad, Hallo build toobe geactiveerd na elke doorvoer configureren.</span><span class="sxs-lookup"><span data-stu-id="3dc65-176">On hello **Triggers** tab, configure hello build toobe triggered after each commit.</span></span> <span data-ttu-id="3dc65-177">Selecteer **continue integratie** en **Batch wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-Trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-hello-build-workflow"></a><span data-ttu-id="3dc65-179">Hallo build werkstroom definiëren</span><span class="sxs-lookup"><span data-stu-id="3dc65-179">Define hello build workflow</span></span>
<span data-ttu-id="3dc65-180">de volgende stappen Hallo definiëren Hallo build werkstroom.</span><span class="sxs-lookup"><span data-stu-id="3dc65-180">hello next steps define hello build workflow.</span></span> <span data-ttu-id="3dc65-181">Er zijn vijf container installatiekopieën toobuild voor Hallo *MyShop* toepassing.</span><span class="sxs-lookup"><span data-stu-id="3dc65-181">There are five container images toobuild for hello *MyShop* application.</span></span> <span data-ttu-id="3dc65-182">Elke installatiekopie gebouwd met behulp van Hallo die dockerfile zich in Hallo projectmappen bevinden:</span><span class="sxs-lookup"><span data-stu-id="3dc65-182">Each image is built using hello Dockerfile located in hello project folders:</span></span>

* <span data-ttu-id="3dc65-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="3dc65-183">ProductsApi</span></span>
* <span data-ttu-id="3dc65-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="3dc65-184">Proxy</span></span>
* <span data-ttu-id="3dc65-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="3dc65-185">RatingsApi</span></span>
* <span data-ttu-id="3dc65-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="3dc65-186">RecommandationsApi</span></span>
* <span data-ttu-id="3dc65-187">Winkelpagina</span><span class="sxs-lookup"><span data-stu-id="3dc65-187">ShopFront</span></span>

<span data-ttu-id="3dc65-188">U moet tooadd twee Docker stappen voor elke installatiekopie, één toobuild Hallo afbeelding en één toopush Hallo image in hello Azure container register.</span><span class="sxs-lookup"><span data-stu-id="3dc65-188">You need tooadd two Docker steps for each image, one toobuild hello image, and one toopush hello image in hello Azure container registry.</span></span> 

1. <span data-ttu-id="3dc65-189">tooadd een stap in Hallo build werkstroom, klikt u op **+ toevoegen build stap** en selecteer **Docker**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-189">tooadd a step in hello build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="3dc65-191">Voor elke installatiekopie, configureert u één stap die gebruikmaakt van Hallo `docker build` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3dc65-191">For each image, configure one step that uses hello `docker build` command.</span></span>

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="3dc65-193">Bouwen voor Hallo bewerking, selecteert u het register Azure container hello **bouwen van een installatiekopie van een** actie en Hallo Dockerfile waarin elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-193">For hello build operation, select your Azure container registry, hello **Build an image** action, and hello Dockerfile that defines each image.</span></span> <span data-ttu-id="3dc65-194">Set Hallo **Build context** als Hallo Dockerfile hoofdmap en definiëren Hallo **Installatiekopienaam**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-194">Set hello **Build context** as hello Dockerfile root directory, and define hello **Image Name**.</span></span> 
    
    <span data-ttu-id="3dc65-195">Zoals wordt weergegeven op de voorgaande scherm hello, start u Hallo installatiekopie met de naam met Hallo URI van de registratie van uw Azure-container.</span><span class="sxs-lookup"><span data-stu-id="3dc65-195">As shown on hello preceding screen, start hello image name with hello URI of your Azure container registry.</span></span> <span data-ttu-id="3dc65-196">(U kunt ook een code build variabele tooparameterize Hallo van Hallo-installatiekopie, zoals Hallo build-id in dit voorbeeld gebruiken.)</span><span class="sxs-lookup"><span data-stu-id="3dc65-196">(You can also use a build variable tooparameterize hello tag of hello image, such as hello build identifier in this example.)</span></span>

3. <span data-ttu-id="3dc65-197">Voor elke installatiekopie, configureert u een tweede stap die gebruikmaakt van Hallo `docker push` opdracht.</span><span class="sxs-lookup"><span data-stu-id="3dc65-197">For each image, configure a second step that uses hello `docker push` command.</span></span>

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="3dc65-199">Voor Hallo push-bewerking, selecteert u het register Azure container hello **een installatiekopie van een Push** actie, en Voer Hallo **Installatiekopienaam** die is ingebouwd in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="3dc65-199">For hello push operation, select your Azure container registry, hello **Push an image** action, and enter hello **Image Name** that is built in hello previous step.</span></span>

4. <span data-ttu-id="3dc65-200">Nadat u hebt configureren Hallo build en stappen voor elk van de vijf installatiekopieën Hallo push, voeg dat meer uit twee stappen in Hallo bouwen werkstroom.</span><span class="sxs-lookup"><span data-stu-id="3dc65-200">After you configure hello build and push steps for each of hello five images, add two more steps in hello build workflow.</span></span>

    <span data-ttu-id="3dc65-201">a.</span><span class="sxs-lookup"><span data-stu-id="3dc65-201">a.</span></span> <span data-ttu-id="3dc65-202">Een opdrachtregeltaak die gebruikmaakt van een bash script tooreplace hello *BuildNumber* exemplaar in Hallo docker-compose.yml-bestand met de huidige Hallo bouwen id. Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-202">A command-line task that uses a bash script tooreplace hello *BuildNumber* occurrence in hello docker-compose.yml file with hello current build Id. See hello following screen for details.</span></span>

    ![Visual Studio teamservices - Update opstellen bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="3dc65-204">b.</span><span class="sxs-lookup"><span data-stu-id="3dc65-204">b.</span></span> <span data-ttu-id="3dc65-205">Een taak die wordt neergezet Hallo bijgewerkt opstellen bestand als een artefact build zodat deze kan worden gebruikt in Hallo-versie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-205">A task that drops hello updated Compose file as a build artifact so it can be used in hello release.</span></span> <span data-ttu-id="3dc65-206">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-206">See hello following screen for details.</span></span>

    ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="3dc65-208">Klik op **opslaan** en de naam van de definitie van de build.</span><span class="sxs-lookup"><span data-stu-id="3dc65-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-hello-release-definition"></a><span data-ttu-id="3dc65-209">Stap 3: Hallo release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="3dc65-209">Step 3: Create hello release definition</span></span>

<span data-ttu-id="3dc65-210">Visual Studio Team Services kunt u te[releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="3dc65-210">Visual Studio Team Services allows you too[manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="3dc65-211">U kunt continue implementatie toomake ervoor dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen.</span><span class="sxs-lookup"><span data-stu-id="3dc65-211">You can enable continuous deployment toomake sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="3dc65-212">U kunt een nieuwe omgeving met uw Azure Container Service Docker Swarm-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="3dc65-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio teamservices - Release tooACS](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="3dc65-214">Installatie van de eerste release</span><span class="sxs-lookup"><span data-stu-id="3dc65-214">Initial release setup</span></span>

1. <span data-ttu-id="3dc65-215">toocreate de definitie van een release, klikt u op **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="3dc65-215">toocreate a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="3dc65-216">tooconfigure hello artefact bron, klikt u op **artefacten** > **een artefact koppelingsbron**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-216">tooconfigure hello artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="3dc65-217">Deze nieuwe versie definitie toohello build die u hebt gedefinieerd in de vorige stap Hallo hier een koppeling.</span><span class="sxs-lookup"><span data-stu-id="3dc65-217">Here, link this new release definition toohello build that you defined in hello previous step.</span></span> <span data-ttu-id="3dc65-218">Op deze manier is beschikbaar in Hallo release proces Hallo docker-compose.yml-bestand.</span><span class="sxs-lookup"><span data-stu-id="3dc65-218">By doing this, hello docker-compose.yml file is available in hello release process.</span></span>

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="3dc65-220">tooconfigure hello release worden geactiveerd, klikt u op **Triggers** en selecteer **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="3dc65-220">tooconfigure hello release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="3dc65-221">Set Hallo trigger op Hallo dezelfde artefact-bron.</span><span class="sxs-lookup"><span data-stu-id="3dc65-221">Set hello trigger on hello same artifact source.</span></span> <span data-ttu-id="3dc65-222">Deze instelling zorgt ervoor dat er een nieuwe release begint zodra Hallo build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="3dc65-222">This setting ensures that a new release starts as soon as hello build completes successfully.</span></span>

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-hello-release-workflow"></a><span data-ttu-id="3dc65-224">Hallo release werkstroom definiëren</span><span class="sxs-lookup"><span data-stu-id="3dc65-224">Define hello release workflow</span></span>

<span data-ttu-id="3dc65-225">Hallo release werkstroom bestaat uit twee taken die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="3dc65-225">hello release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="3dc65-226">Configureren van een taak toosecurely kopie Hallo opstellen bestand tooa *implementeren* map op Hallo Docker Swarm-hoofdknooppunt, met behulp van Hallo SSH-verbinding u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-226">Configure a task toosecurely copy hello compose file tooa *deploy* folder on hello Docker Swarm master node, using hello SSH connection you configured previously.</span></span> <span data-ttu-id="3dc65-227">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-227">See hello following screen for details.</span></span>

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="3dc65-229">Configureren van een tweede taak tooexecute een opdracht bash toorun `docker` en `docker-compose` opdrachten op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="3dc65-229">Configure a second task tooexecute a bash command toorun `docker` and `docker-compose` commands on hello master node.</span></span> <span data-ttu-id="3dc65-230">Zie Hallo na scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-230">See hello following screen for details.</span></span>

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="3dc65-232">Hallo-opdracht is uitgevoerd op Hallo master gebruik Hallo Docker CLI en Hallo Docker Compose CLI toodo Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="3dc65-232">hello command executed on hello master use hello Docker CLI and hello Docker-Compose CLI toodo hello following tasks:</span></span>

    - <span data-ttu-id="3dc65-233">Aanmelding toohello Azure container register (hierbij drie build variab'les die zijn gedefinieerd in Hallo **variabelen** tabblad)</span><span class="sxs-lookup"><span data-stu-id="3dc65-233">Login toohello Azure container registry (it uses three build variab\`les that are defined in hello **Variables** tab)</span></span>
    - <span data-ttu-id="3dc65-234">Hallo definiëren **DOCKER_HOST** variabele toowork met Hallo Swarm-eindpunt (: 2375)</span><span class="sxs-lookup"><span data-stu-id="3dc65-234">Define hello **DOCKER_HOST** variable toowork with hello Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="3dc65-235">Navigeer toohello *implementeren* map die is gemaakt door Hallo voorafgaand aan beveiligde kopieertaak en die Hallo docker-compose.yml-bestand bevat</span><span class="sxs-lookup"><span data-stu-id="3dc65-235">Navigate toohello *deploy* folder that was created by hello preceding secure copy task and that contains hello docker-compose.yml file</span></span> 
    - <span data-ttu-id="3dc65-236">Uitvoeren van `docker-compose` opdrachten die pull-hallo nieuwe afbeeldingen, Hallo-services stoppen, verwijdert u Hallo services en Hallo containers te maken.</span><span class="sxs-lookup"><span data-stu-id="3dc65-236">Execute `docker-compose` commands that pull hello new images, stop hello services, remove hello services, and create hello containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="3dc65-237">Zoals wordt weergegeven op de voorgaande scherm hello, laat u Hallo **mislukken op STDERR** selectievakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="3dc65-237">As shown on hello preceding screen, leave hello **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="3dc65-238">Dit is een belangrijk instelling, omdat `docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op Hallo standaardfout uitvoer wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on hello standard error output.</span></span> <span data-ttu-id="3dc65-239">Als u het selectievakje Hallo inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens het Hallo-release, zelfs als alles goed gaat.</span><span class="sxs-lookup"><span data-stu-id="3dc65-239">If you check hello checkbox, Visual Studio Team Services reports that errors occurred during hello release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="3dc65-240">Sla deze definitie voor de nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="3dc65-241">Deze implementatie bevat enige uitvaltijd, omdat we Hallo oude services worden gestopt en Hallo nieuwe uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3dc65-241">This deployment includes some downtime because we are stopping hello old services and running hello new one.</span></span> <span data-ttu-id="3dc65-242">Het is mogelijk tooavoid dit als volgt een blauw-groen-implementatie.</span><span class="sxs-lookup"><span data-stu-id="3dc65-242">It is possible tooavoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-hello-cicd-pipeline"></a><span data-ttu-id="3dc65-243">Stap 4.</span><span class="sxs-lookup"><span data-stu-id="3dc65-243">Step 4.</span></span> <span data-ttu-id="3dc65-244">Test Hallo CI/CD-pipeline</span><span class="sxs-lookup"><span data-stu-id="3dc65-244">Test hello CI/CD pipeline</span></span>

<span data-ttu-id="3dc65-245">Nu u klaar bent met Hallo configuratie, is het tijd tootest dit nieuwe CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="3dc65-245">Now that you are done with hello configuration, it's time tootest this new CI/CD pipeline.</span></span> <span data-ttu-id="3dc65-246">Hallo gemakkelijkste manier tootest tooupdate Hallo source code en doorvoeren Hallo is gewijzigd in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="3dc65-246">hello easiest way tootest it is tooupdate hello source code and commit hello changes into your GitHub repository.</span></span> <span data-ttu-id="3dc65-247">Enkele seconden nadat u push-Hallo code, ziet u een nieuwe build uitgevoerd in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="3dc65-247">A few seconds after you push hello code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="3dc65-248">Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en Hallo nieuwe versie van de toepassing hello op Hallo Azure Container Service-cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="3dc65-248">Once completed successfully, a new release will be triggered and will deploy hello new version of hello application on hello Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dc65-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3dc65-249">Next Steps</span></span>

* <span data-ttu-id="3dc65-250">Zie voor meer informatie over CI/CD met Visual Studio Team Services, Hallo [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="3dc65-250">For more information about CI/CD with Visual Studio Team Services, see hello [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
