---
title: CI/CD met Azure Containerservice- en Swarm | Microsoft Docs
description: Azure Container Service met Docker Swarm, een Azure Container register en Visual Studio Team Services gebruiken om te leveren continu een toepassing met meerdere .NET Core
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
ms.openlocfilehash: 99c27c37218a35d2a3416d6edd5e0a871cd5c011
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-docker-swarm-using-visual-studio-team-services"></a><span data-ttu-id="92231-104">Volledige CI/CD-pijplijn voor het implementeren van een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="92231-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services</span></span>

<span data-ttu-id="92231-105">Een van de grootste uitdagingen bij het ontwikkelen van moderne toepassingen voor de cloud wordt deze toepassingen continu leveren.</span><span class="sxs-lookup"><span data-stu-id="92231-105">One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="92231-106">In dit artikel leert u hoe u een volledige continue integratie en implementatie (CI/CD)-pijplijn met Azure Container Service met Docker Swarm, het register van Azure-Container en Visual Studio Team Services build te implementeren en releasebeheer.</span><span class="sxs-lookup"><span data-stu-id="92231-106">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using Azure Container Service with Docker Swarm, Azure Container Registry, and Visual Studio Team Services build and release management.</span></span>

<span data-ttu-id="92231-107">In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), ontwikkelde met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="92231-107">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/acs-docs), developed with ASP.NET Core.</span></span> <span data-ttu-id="92231-108">De toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:</span><span class="sxs-lookup"><span data-stu-id="92231-108">The application is composed of four different services: three web APIs and one web front end:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/myshop-application.png)

<span data-ttu-id="92231-110">Het doel is deze toepassing continu in een Docker Swarm-cluster met behulp van Visual Studio Team Services leveren.</span><span class="sxs-lookup"><span data-stu-id="92231-110">The objective is to deliver this application continuously in a Docker Swarm cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="92231-111">De volgende afbeelding om deze pipeline continue levering details:</span><span class="sxs-lookup"><span data-stu-id="92231-111">The following figure details this continuous delivery pipeline:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-setup-ci-cd/full-ci-cd-pipeline.png)

<span data-ttu-id="92231-113">Hier volgt een korte uitleg van de stappen uit:</span><span class="sxs-lookup"><span data-stu-id="92231-113">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="92231-114">Codewijzigingen zijn doorgevoerd in de opslagplaats van bron code (in dit geval GitHub)</span><span class="sxs-lookup"><span data-stu-id="92231-114">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="92231-115">GitHub activeert een bouwen in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="92231-115">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="92231-116">Visual Studio Team Services haalt de meest recente versie van de bronnen en maakt de installatiekopieën waaruit de toepassing</span><span class="sxs-lookup"><span data-stu-id="92231-116">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="92231-117">Visual Studio Team Services verstuurd elke installatiekopie naar een Docker-register gemaakt met behulp van de Azure-Container Registry-service</span><span class="sxs-lookup"><span data-stu-id="92231-117">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="92231-118">Visual Studio Team Services activeert een nieuwe release</span><span class="sxs-lookup"><span data-stu-id="92231-118">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="92231-119">De release van bepaalde opdrachten met SSH op het hoofdknooppunt van Azure container service-cluster wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="92231-119">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="92231-120">Docker Swarm op het cluster haalt de meest recente versie van de installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="92231-120">Docker Swarm on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="92231-121">De nieuwe versie van de toepassing wordt geïmplementeerd met behulp van Docker Compose</span><span class="sxs-lookup"><span data-stu-id="92231-121">The new version of the application is deployed using Docker Compose</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="92231-122">Vereisten</span><span class="sxs-lookup"><span data-stu-id="92231-122">Prerequisites</span></span>

<span data-ttu-id="92231-123">Voordat u deze zelfstudie begint, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="92231-123">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="92231-124">Een Swarm-cluster in Azure Container Service maken</span><span class="sxs-lookup"><span data-stu-id="92231-124">Create a Swarm cluster in Azure Container Service</span></span>](container-service-deployment.md)
- [<span data-ttu-id="92231-125">Verbinding maken met het Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="92231-125">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="92231-126">Een Azure container registry maken</span><span class="sxs-lookup"><span data-stu-id="92231-126">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="92231-127">Een Visual Studio Team Services-account en team project zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="92231-127">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="92231-128">Vertakken de GitHub-opslagplaats met uw GitHub-account</span><span class="sxs-lookup"><span data-stu-id="92231-128">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/)

[!INCLUDE [container-service-swarm-mode-note](../../../includes/container-service-swarm-mode-note.md)]

<span data-ttu-id="92231-129">U moet ook een machine Ubuntu (14.04 of 16.04) met Docker geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="92231-129">You also need an Ubuntu (14.04 or 16.04) machine with Docker installed.</span></span> <span data-ttu-id="92231-130">Deze computer wordt gebruikt door Visual Studio Team Services tijdens het bouwen en release.</span><span class="sxs-lookup"><span data-stu-id="92231-130">This machine is used by Visual Studio Team Services during the build and release processes.</span></span> <span data-ttu-id="92231-131">Een manier om deze machine te maken is het gebruik van de installatiekopie die beschikbaar zijn in de [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span><span class="sxs-lookup"><span data-stu-id="92231-131">One way to create this machine is to use the image available in the [Azure Marketplace](https://azure.microsoft.com/marketplace/partners/canonicalandmsopentech/dockeronubuntuserver1404lts/).</span></span> 

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="92231-132">Stap 1: Uw Visual Studio Team Services-account configureren</span><span class="sxs-lookup"><span data-stu-id="92231-132">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="92231-133">In deze sectie configureert u uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="92231-133">In this section, you configure your Visual Studio Team Services account.</span></span>

### <a name="configure-a-visual-studio-team-services-linux-build-agent"></a><span data-ttu-id="92231-134">Een Visual Studio Team Services Linux build-agent configureren</span><span class="sxs-lookup"><span data-stu-id="92231-134">Configure a Visual Studio Team Services Linux build agent</span></span>

<span data-ttu-id="92231-135">Als u wilt Docker-installatiekopieën maken en toepassen van deze installatiekopieën naar een Azure container register van de versie van een Visual Studio Team Services, moet u een Linux-agent registreren.</span><span class="sxs-lookup"><span data-stu-id="92231-135">To create Docker images and push these images into an Azure container registry from a Visual Studio Team Services build, you need to register a Linux agent.</span></span> <span data-ttu-id="92231-136">U hebt deze installatieopties:</span><span class="sxs-lookup"><span data-stu-id="92231-136">You have these installation options:</span></span>

* [<span data-ttu-id="92231-137">Een op Linux-agent implementeren</span><span class="sxs-lookup"><span data-stu-id="92231-137">Deploy an agent on Linux</span></span>](https://www.visualstudio.com/docs/build/admin/agents/v2-linux)

* [<span data-ttu-id="92231-138">Docker gebruiken voor het uitvoeren van de agent VSTS</span><span class="sxs-lookup"><span data-stu-id="92231-138">Use Docker to run the VSTS agent</span></span>](https://hub.docker.com/r/microsoft/vsts-agent)

### <a name="install-the-docker-integration-vsts-extension"></a><span data-ttu-id="92231-139">De uitbreiding voor de Docker-integratie VSTS installeren</span><span class="sxs-lookup"><span data-stu-id="92231-139">Install the Docker Integration VSTS extension</span></span>

<span data-ttu-id="92231-140">Microsoft biedt een uitbreiding VSTS om te werken met Docker gebouwd en release van processen.</span><span class="sxs-lookup"><span data-stu-id="92231-140">Microsoft provides a VSTS extension to work with Docker in build and release processes.</span></span> <span data-ttu-id="92231-141">Deze uitbreiding is beschikbaar in de [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span><span class="sxs-lookup"><span data-stu-id="92231-141">This extension is available in the [VSTS Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-vscs-rm.docker).</span></span> <span data-ttu-id="92231-142">Klik op **installeren** deze extensie toevoegen aan uw account VSTS:</span><span class="sxs-lookup"><span data-stu-id="92231-142">Click **Install** to add this extension to your VSTS account:</span></span>

![De Docker-integratie installeren](./media/container-service-docker-swarm-setup-ci-cd/install-docker-vsts.png)

<span data-ttu-id="92231-144">U wordt gevraagd of u verbinding maken met uw VSTS rekening met uw referenties.</span><span class="sxs-lookup"><span data-stu-id="92231-144">You are asked to connect to your VSTS account using your credentials.</span></span> 

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="92231-145">Verbinding maken met Visual Studio teamservices en GitHub</span><span class="sxs-lookup"><span data-stu-id="92231-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="92231-146">Een verbinding tussen uw project VSTS en uw GitHub-account instellen.</span><span class="sxs-lookup"><span data-stu-id="92231-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="92231-147">In het project voor Visual Studio Team Services, klikt u op de **instellingen** pictogram in de werkbalk en selecteert u **Services**.</span><span class="sxs-lookup"><span data-stu-id="92231-147">In your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

    ![Visual Studio teamservices - externe verbinding](./media/container-service-docker-swarm-setup-ci-cd/vsts-services-menu.png)

2. <span data-ttu-id="92231-149">Klik aan de linkerkant op **nieuwe Service-eindpunt** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="92231-149">On the left, click **New Service Endpoint** > **GitHub**.</span></span>

    ![Visual Studio teamservices - GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github.png)

3. <span data-ttu-id="92231-151">Als u wilt machtigen VSTS werken met uw GitHub-account, klikt u op **autoriseren** en volg de procedure in het venster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="92231-151">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-authorize.png)

### <a name="connect-vsts-to-your-azure-container-registry-and-azure-container-service-cluster"></a><span data-ttu-id="92231-153">VSTS verbinding met uw Azure-container register en Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="92231-153">Connect VSTS to your Azure container registry and Azure Container Service cluster</span></span>

<span data-ttu-id="92231-154">De laatste stappen voordat u in de pipeline CI/CD zijn voor het configureren van externe verbindingen met het register van de container en Docker Swarm-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="92231-154">The last steps before getting into the CI/CD pipeline are to configure external connections to your container registry and your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="92231-155">In de **Services** instellingen van uw project Visual Studio Team Services, Voeg een service-eindpunt van het type **Docker-register**.</span><span class="sxs-lookup"><span data-stu-id="92231-155">In the **Services** settings of your Visual Studio Team Services project, add a service endpoint of type **Docker Registry**.</span></span> 

2. <span data-ttu-id="92231-156">Voer de URL en de referenties van de registratie van uw Azure-container in de pop-up dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="92231-156">In the popup that opens, enter the URL and the credentials of your Azure container registry.</span></span>

    ![Visual Studio teamservices - Docker-register](./media/container-service-docker-swarm-setup-ci-cd/vsts-registry.png)

3. <span data-ttu-id="92231-158">Voeg een eindpunt van het type voor de Docker Swarm-cluster **SSH**.</span><span class="sxs-lookup"><span data-stu-id="92231-158">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="92231-159">Voer vervolgens de SSH-verbindingsgegevens van de Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="92231-159">Then enter the SSH connection information of your Swarm cluster.</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-setup-ci-cd/vsts-ssh.png)

<span data-ttu-id="92231-161">Alle van de configuratie wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="92231-161">All the configuration is done now.</span></span> <span data-ttu-id="92231-162">In de volgende stappen maakt u de CI/CD-pijplijn die u maakt en implementeert de toepassing op het Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="92231-162">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="92231-163">Stap 2: De definitie van de build maken</span><span class="sxs-lookup"><span data-stu-id="92231-163">Step 2: Create the build definition</span></span>

<span data-ttu-id="92231-164">In deze stap maakt u een build definitionfor instellen met uw project VSTS en definiëren van de build-werkstroom voor de installatiekopieën van de container</span><span class="sxs-lookup"><span data-stu-id="92231-164">In this step, you set up a build definitionfor your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="92231-165">Initiële definitie setup</span><span class="sxs-lookup"><span data-stu-id="92231-165">Initial definition setup</span></span>

1. <span data-ttu-id="92231-166">De definitie van een build maken, koppelen aan uw project voor Visual Studio Team Services en klik op **bouwen & Release**.</span><span class="sxs-lookup"><span data-stu-id="92231-166">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> 

2. <span data-ttu-id="92231-167">In de **bouwen definities** sectie, klikt u op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="92231-167">In the **Build definitions** section, click **+ New**.</span></span> <span data-ttu-id="92231-168">Selecteer de **leeg** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="92231-168">Select the **Empty** template.</span></span>

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-setup-ci-cd/create-build-vsts.png)

3. <span data-ttu-id="92231-170">De nieuwe build configureren met een GitHub-opslagplaats bron, selectievakje **continue integratie**, en selecteert u de agent wachtrij waar u uw Linux-agent is geregistreerd.</span><span class="sxs-lookup"><span data-stu-id="92231-170">Configure the new build with a GitHub repository source, check **Continuous integration**, and select the agent queue where you registered your Linux agent.</span></span> <span data-ttu-id="92231-171">Klik op **maken** de build-definitie maken.</span><span class="sxs-lookup"><span data-stu-id="92231-171">Click **Create** to create the build definition.</span></span>

    ![Visual Studio teamservices - maken Build-definitie](./media/container-service-docker-swarm-setup-ci-cd/vsts-create-build-github.png)

4. <span data-ttu-id="92231-173">Op de **bouwen definities** pagina, opent u eerst de **opslagplaats** tabblad en configureren van de build voor het gebruik van de fork van het MyShop-project dat u hebt gemaakt in de vereisten.</span><span class="sxs-lookup"><span data-stu-id="92231-173">On the **Build Definitions** page, first open the **Repository** tab and configure the build to use the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="92231-174">Zorg ervoor dat u selecteert *acs docs* als de **standaardvertakking**.</span><span class="sxs-lookup"><span data-stu-id="92231-174">Make sure that you select *acs-docs* as the **Default branch**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-repo-conf.png)

5. <span data-ttu-id="92231-176">Op de **Triggers** tabblad, het configureren van de build worden geactiveerd na elke doorvoer.</span><span class="sxs-lookup"><span data-stu-id="92231-176">On the **Triggers** tab, configure the build to be triggered after each commit.</span></span> <span data-ttu-id="92231-177">Selecteer **continue integratie** en **Batch wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="92231-177">Select **Continuous integration** and **Batch changes**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-Trigger](./media/container-service-docker-swarm-setup-ci-cd/vsts-github-trigger-conf.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="92231-179">Definieer de build-werkstroom</span><span class="sxs-lookup"><span data-stu-id="92231-179">Define the build workflow</span></span>
<span data-ttu-id="92231-180">De volgende stappen definiëren de build-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="92231-180">The next steps define the build workflow.</span></span> <span data-ttu-id="92231-181">Er zijn vijf container afbeeldingen maken voor de *MyShop* toepassing.</span><span class="sxs-lookup"><span data-stu-id="92231-181">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="92231-182">Elke installatiekopie gebouwd met behulp van de Dockerfile zich in de projectmappen:</span><span class="sxs-lookup"><span data-stu-id="92231-182">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="92231-183">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="92231-183">ProductsApi</span></span>
* <span data-ttu-id="92231-184">Proxy</span><span class="sxs-lookup"><span data-stu-id="92231-184">Proxy</span></span>
* <span data-ttu-id="92231-185">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="92231-185">RatingsApi</span></span>
* <span data-ttu-id="92231-186">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="92231-186">RecommandationsApi</span></span>
* <span data-ttu-id="92231-187">Winkelpagina</span><span class="sxs-lookup"><span data-stu-id="92231-187">ShopFront</span></span>

<span data-ttu-id="92231-188">U moet twee Docker-stappen voor elke installatiekopie, één voor het bouwen van de installatiekopie en één voor de push-installatiekopie van het in het register van de Azure-container toevoegen.</span><span class="sxs-lookup"><span data-stu-id="92231-188">You need to add two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="92231-189">Klik op als u een stap in de werkstroom build **+ toevoegen build stap** en selecteer **Docker**.</span><span class="sxs-lookup"><span data-stu-id="92231-189">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-add-task.png)

2. <span data-ttu-id="92231-191">Voor elke installatiekopie, configureert u één stap die gebruikmaakt van de `docker build` opdracht.</span><span class="sxs-lookup"><span data-stu-id="92231-191">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-build.png)

    <span data-ttu-id="92231-193">Voor de build-bewerking, selecteert u het register Azure container de **bouwen van een installatiekopie van een** actie en de Dockerfile waarin elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="92231-193">For the build operation, select your Azure container registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="92231-194">Stel de **Build context** als de Dockerfile hoofdmap en definieer de **installatiekopie met de naam**.</span><span class="sxs-lookup"><span data-stu-id="92231-194">Set the **Build context** as the Dockerfile root directory, and define the **Image Name**.</span></span> 
    
    <span data-ttu-id="92231-195">Zoals u in het vorige scherm, start u de naam van de installatiekopie met de URI van de registratie van uw Azure-container.</span><span class="sxs-lookup"><span data-stu-id="92231-195">As shown on the preceding screen, start the image name with the URI of your Azure container registry.</span></span> <span data-ttu-id="92231-196">(U kunt ook een build-variabele gebruiken om te voorzien van het label van de afbeelding, zoals de build-id in dit voorbeeld.)</span><span class="sxs-lookup"><span data-stu-id="92231-196">(You can also use a build variable to parameterize the tag of the image, such as the build identifier in this example.)</span></span>

3. <span data-ttu-id="92231-197">Voor elke installatiekopie configureert u een tweede stap die gebruikmaakt van de `docker push` opdracht.</span><span class="sxs-lookup"><span data-stu-id="92231-197">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-setup-ci-cd/vsts-docker-push.png)

    <span data-ttu-id="92231-199">Voor de push-bewerking, selecteert u het register Azure container de **een installatiekopie van een Push** actie en voer de **Installatiekopienaam** die is ingebouwd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="92231-199">For the push operation, select your Azure container registry, the **Push an image** action, and enter the **Image Name** that is built in the previous step.</span></span>

4. <span data-ttu-id="92231-200">Nadat u de stappen build en pushmeldingen voor elk van de vijf afbeeldingen hebt geconfigureerd, moet u twee meer stappen toevoegen in de build-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="92231-200">After you configure the build and push steps for each of the five images, add two more steps in the build workflow.</span></span>

    <span data-ttu-id="92231-201">a.</span><span class="sxs-lookup"><span data-stu-id="92231-201">a.</span></span> <span data-ttu-id="92231-202">Een opdrachtregeltaak die gebruikmaakt van een bash-scripts ter vervanging van de *BuildNumber* exemplaar in de docker-compose.yml-bestand met de huidige id maken Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92231-202">A command-line task that uses a bash script to replace the *BuildNumber* occurrence in the docker-compose.yml file with the current build Id. See the following screen for details.</span></span>

    ![Visual Studio teamservices - Update opstellen bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-build-replace-build-number.png)

    <span data-ttu-id="92231-204">b.</span><span class="sxs-lookup"><span data-stu-id="92231-204">b.</span></span> <span data-ttu-id="92231-205">Een taak die het bijgewerkte opstellen-bestand als een artefact build zakt zodat deze kan worden gebruikt in de release.</span><span class="sxs-lookup"><span data-stu-id="92231-205">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="92231-206">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92231-206">See the following screen for details.</span></span>

    ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-setup-ci-cd/vsts-publish-compose.png) 

5. <span data-ttu-id="92231-208">Klik op **opslaan** en de naam van de definitie van de build.</span><span class="sxs-lookup"><span data-stu-id="92231-208">Click **Save** and name your build definition.</span></span>

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="92231-209">Stap 3: De release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="92231-209">Step 3: Create the release definition</span></span>

<span data-ttu-id="92231-210">Visual Studio Team Services kunt u [releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="92231-210">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="92231-211">U kunt continue implementatie om ervoor te zorgen dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen.</span><span class="sxs-lookup"><span data-stu-id="92231-211">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="92231-212">U kunt een nieuwe omgeving met uw Azure Container Service Docker Swarm-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="92231-212">You can create a new environment that represents your Azure Container Service Docker Swarm cluster.</span></span>

![Visual Studio teamservices - ACS-versie](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="92231-214">Installatie van de eerste release</span><span class="sxs-lookup"><span data-stu-id="92231-214">Initial release setup</span></span>

1. <span data-ttu-id="92231-215">Klik op om de definitie van een release **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="92231-215">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="92231-216">Als u wilt de artefacten configureren, klikt u op **artefacten** > **een artefact koppelingsbron**.</span><span class="sxs-lookup"><span data-stu-id="92231-216">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="92231-217">Hier definitie voor dit nieuwe release koppeling naar de versie die u hebt gedefinieerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="92231-217">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="92231-218">Dit doet, is de docker-compose.yml-bestand beschikbaar in de release-proces.</span><span class="sxs-lookup"><span data-stu-id="92231-218">By doing this, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-artefacts.png) 

3. <span data-ttu-id="92231-220">Voor het configureren van de trigger release, klikt u op **Triggers** en selecteer **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="92231-220">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="92231-221">De trigger niet instellen op dezelfde bron artefacten.</span><span class="sxs-lookup"><span data-stu-id="92231-221">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="92231-222">Deze instelling zorgt ervoor dat er een nieuwe release begint zodra de build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="92231-222">This setting ensures that a new release starts as soon as the build completes successfully.</span></span>

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-trigger.png) 

### <a name="define-the-release-workflow"></a><span data-ttu-id="92231-224">Definieer de release-werkstroom</span><span class="sxs-lookup"><span data-stu-id="92231-224">Define the release workflow</span></span>

<span data-ttu-id="92231-225">De werkstroom release bestaat uit twee taken die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="92231-225">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="92231-226">Configureren van een taak voor het veilig de opstellen bestand kopiëren naar een *implementeren* map op het Docker Swarm hoofdknooppunt, met behulp van de SSH-verbinding die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="92231-226">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="92231-227">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92231-227">See the following screen for details.</span></span>

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-scp.png)

2. <span data-ttu-id="92231-229">Configureren van een tweede taak voor het uitvoeren van een bash-opdracht om uit te voeren `docker` en `docker-compose` opdrachten op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="92231-229">Configure a second task to execute a bash command to run `docker` and `docker-compose` commands on the master node.</span></span> <span data-ttu-id="92231-230">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="92231-230">See the following screen for details.</span></span>

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-setup-ci-cd/vsts-release-bash.png)

    <span data-ttu-id="92231-232">De opdracht wordt uitgevoerd op de master gebruikt de Docker CLI en Docker Compose CLI om de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="92231-232">The command executed on the master use the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="92231-233">Meld u aan bij het register van de Azure-container (hierbij drie build variab'les die zijn gedefinieerd in de **variabelen** tabblad)</span><span class="sxs-lookup"><span data-stu-id="92231-233">Login to the Azure container registry (it uses three build variab\`les that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="92231-234">Definieer de **DOCKER_HOST** variabele werken met het Swarm-eindpunt (: 2375)</span><span class="sxs-lookup"><span data-stu-id="92231-234">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="92231-235">Navigeer naar de *implementeren* map die door de voorgaande beveiligde kopie-taak is gemaakt en die de docker-compose.yml-bestand bevat</span><span class="sxs-lookup"><span data-stu-id="92231-235">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="92231-236">Uitvoeren van `docker-compose` opdrachten die de nieuwe afbeeldingen pull stop de services, verwijder de services en de containers te maken.</span><span class="sxs-lookup"><span data-stu-id="92231-236">Execute `docker-compose` commands that pull the new images, stop the services, remove the services, and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="92231-237">Zoals u in het vorige scherm, laat de **mislukken op STDERR** selectievakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="92231-237">As shown on the preceding screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="92231-238">Dit is een belangrijk instelling, omdat `docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op de uitvoer van de standaardfout wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="92231-238">This is an important setting, because `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="92231-239">Als u het selectievakje inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens de release, zelfs als alles goed gaat.</span><span class="sxs-lookup"><span data-stu-id="92231-239">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="92231-240">Sla deze definitie voor de nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="92231-240">Save this new release definition.</span></span>


>[!NOTE]
><span data-ttu-id="92231-241">Deze implementatie bevat enige uitvaltijd, omdat we stoppen van de oude services en waarop de nieuwe database wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="92231-241">This deployment includes some downtime because we are stopping the old services and running the new one.</span></span> <span data-ttu-id="92231-242">Het is mogelijk om te voorkomen dat dit als volgt een blauw-groen-implementatie.</span><span class="sxs-lookup"><span data-stu-id="92231-242">It is possible to avoid this by doing a blue-green deployment.</span></span>
>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="92231-243">Stap 4.</span><span class="sxs-lookup"><span data-stu-id="92231-243">Step 4.</span></span> <span data-ttu-id="92231-244">De pijplijn CI/CD testen</span><span class="sxs-lookup"><span data-stu-id="92231-244">Test the CI/CD pipeline</span></span>

<span data-ttu-id="92231-245">Nu u klaar bent met de configuratie, is het tijd voor het testen van dit nieuwe CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="92231-245">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="92231-246">De eenvoudigste manier om deze te testen, is voor het bijwerken van de broncode en voer de wijzigingen in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="92231-246">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="92231-247">Enkele seconden nadat u de code pushen ziet u een nieuwe build uitgevoerd in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="92231-247">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="92231-248">Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en de nieuwe versie van de toepassing op het Azure Container Service-cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="92231-248">Once completed successfully, a new release will be triggered and will deploy the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92231-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="92231-249">Next Steps</span></span>

* <span data-ttu-id="92231-250">Zie voor meer informatie over CI/CD met Visual Studio Team Services, de [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="92231-250">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
