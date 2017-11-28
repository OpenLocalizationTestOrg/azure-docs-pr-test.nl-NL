---
title: CI/CD met Azure Container Service-Engine en Swarm-modus | Microsoft Docs
description: Azure Container Service-Engine met Docker Swarm-modus, een Azure Container register en Visual Studio Team Services gebruiken om te leveren continu een toepassing met meerdere .NET Core
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
ms.openlocfilehash: 2c0e5fe4f60738fcc1aa67a78674e6f3c62e5628
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="full-cicd-pipeline-to-deploy-a-multi-container-application-on-azure-container-service-with-acs-engine-and-docker-swarm-mode-using-visual-studio-team-services"></a><span data-ttu-id="a5b31-104">Volledige CI/CD-pijplijn voor het implementeren van een toepassing met meerdere container in Azure Container Service met de ACS-Engine en Docker Swarm-modus met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a5b31-104">Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with ACS Engine and Docker Swarm Mode using Visual Studio Team Services</span></span>

<span data-ttu-id="a5b31-105">*In dit artikel is gebaseerd op [volledige CI/CD-pijplijn voor het implementeren van een toepassing met meerdere container in Azure Container Service met Docker Swarm met behulp van Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentatie*</span><span class="sxs-lookup"><span data-stu-id="a5b31-105">*This article is based on [Full CI/CD pipeline to deploy a multi-container application on Azure Container Service with Docker Swarm using Visual Studio Team Services](container-service-docker-swarm-setup-ci-cd.md) documentation*</span></span>

<span data-ttu-id="a5b31-106">Een van de grootste uitdagingen bij het ontwikkelen van moderne toepassingen voor de cloud wordt tegenwoordig deze toepassingen continu leveren.</span><span class="sxs-lookup"><span data-stu-id="a5b31-106">Nowadays, One of the biggest challenges when developing modern applications for the cloud is being able to deliver these applications continuously.</span></span> <span data-ttu-id="a5b31-107">In dit artikel leert u hoe voor het implementeren van een volledige continue integratie en implementatie (CI/CD) pijplijn:</span><span class="sxs-lookup"><span data-stu-id="a5b31-107">In this article, you learn how to implement a full continuous integration and deployment (CI/CD) pipeline using:</span></span> 
* <span data-ttu-id="a5b31-108">Azure Container Service-Engine met Docker Swarm-modus</span><span class="sxs-lookup"><span data-stu-id="a5b31-108">Azure Container Service Engine with Docker Swarm Mode</span></span>
* <span data-ttu-id="a5b31-109">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="a5b31-109">Azure Container Registry</span></span>
* <span data-ttu-id="a5b31-110">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a5b31-110">Visual Studio Team Services</span></span>

<span data-ttu-id="a5b31-111">In dit artikel is gebaseerd op een eenvoudige toepassing beschikbaar is op [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), ontwikkelde met ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="a5b31-111">This article is based on a simple application, available on [GitHub](https://github.com/jcorioland/MyShop/tree/docker-linux), developed with ASP.NET Core.</span></span> <span data-ttu-id="a5b31-112">De toepassing bestaat uit vier verschillende services: drie web-API's en een web-front-end:</span><span class="sxs-lookup"><span data-stu-id="a5b31-112">The application is composed of four different services: three web APIs and one web front end:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/myshop-application.png)

<span data-ttu-id="a5b31-114">Het doel is deze toepassing continu in een modus voor Docker Swarm-cluster met behulp van Visual Studio Team Services leveren.</span><span class="sxs-lookup"><span data-stu-id="a5b31-114">The objective is to deliver this application continuously in a Docker Swarm Mode cluster, using Visual Studio Team Services.</span></span> <span data-ttu-id="a5b31-115">De volgende afbeelding om deze pipeline continue levering details:</span><span class="sxs-lookup"><span data-stu-id="a5b31-115">The following figure details this continuous delivery pipeline:</span></span>

![De voorbeeldtoepassing MyShop](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/full-ci-cd-pipeline.png)

<span data-ttu-id="a5b31-117">Hier volgt een korte uitleg van de stappen uit:</span><span class="sxs-lookup"><span data-stu-id="a5b31-117">Here is a brief explanation of the steps:</span></span>

1. <span data-ttu-id="a5b31-118">Codewijzigingen zijn doorgevoerd in de opslagplaats van bron code (in dit geval GitHub)</span><span class="sxs-lookup"><span data-stu-id="a5b31-118">Code changes are committed to the source code repository (here, GitHub)</span></span> 
2. <span data-ttu-id="a5b31-119">GitHub activeert een bouwen in Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a5b31-119">GitHub triggers a build in Visual Studio Team Services</span></span> 
3. <span data-ttu-id="a5b31-120">Visual Studio Team Services haalt de meest recente versie van de bronnen en maakt de installatiekopieën waaruit de toepassing</span><span class="sxs-lookup"><span data-stu-id="a5b31-120">Visual Studio Team Services gets the latest version of the sources and builds all the images that compose the application</span></span> 
4. <span data-ttu-id="a5b31-121">Visual Studio Team Services verstuurd elke installatiekopie naar een Docker-register gemaakt met behulp van de Azure-Container Registry-service</span><span class="sxs-lookup"><span data-stu-id="a5b31-121">Visual Studio Team Services pushes each image to a Docker registry created using the Azure Container Registry service</span></span> 
5. <span data-ttu-id="a5b31-122">Visual Studio Team Services activeert een nieuwe release</span><span class="sxs-lookup"><span data-stu-id="a5b31-122">Visual Studio Team Services triggers a new release</span></span> 
6. <span data-ttu-id="a5b31-123">De release van bepaalde opdrachten met SSH op het hoofdknooppunt van Azure container service-cluster wordt uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="a5b31-123">The release runs some commands using SSH on the Azure container service cluster master node</span></span> 
7. <span data-ttu-id="a5b31-124">Docker Swarm modus op het cluster haalt de meest recente versie van de installatiekopieën</span><span class="sxs-lookup"><span data-stu-id="a5b31-124">Docker Swarm Mode on the cluster pulls the latest version of the images</span></span> 
8. <span data-ttu-id="a5b31-125">De nieuwe versie van de toepassing wordt geïmplementeerd met behulp van Docker-Stack</span><span class="sxs-lookup"><span data-stu-id="a5b31-125">The new version of the application is deployed using Docker Stack</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="a5b31-126">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a5b31-126">Prerequisites</span></span>

<span data-ttu-id="a5b31-127">Voordat u deze zelfstudie begint, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a5b31-127">Before starting this tutorial, you need to complete the following tasks:</span></span>

- [<span data-ttu-id="a5b31-128">Een modus Swarm-cluster maken in Azure Container Service met de ACS-Engine</span><span class="sxs-lookup"><span data-stu-id="a5b31-128">Create a Swarm Mode cluster in Azure Container Service with ACS Engine</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/101-acsengine-swarmmode)
- [<span data-ttu-id="a5b31-129">Verbinding maken met het Swarm-cluster in Azure Container Service</span><span class="sxs-lookup"><span data-stu-id="a5b31-129">Connect with the Swarm cluster in Azure Container Service</span></span>](../container-service-connect.md)
- [<span data-ttu-id="a5b31-130">Een Azure container registry maken</span><span class="sxs-lookup"><span data-stu-id="a5b31-130">Create an Azure container registry</span></span>](../../container-registry/container-registry-get-started-portal.md)
- [<span data-ttu-id="a5b31-131">Een Visual Studio Team Services-account en team project zijn gemaakt</span><span class="sxs-lookup"><span data-stu-id="a5b31-131">Have a Visual Studio Team Services account and team project created</span></span>](https://www.visualstudio.com/en-us/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
- [<span data-ttu-id="a5b31-132">Vertakken de GitHub-opslagplaats met uw GitHub-account</span><span class="sxs-lookup"><span data-stu-id="a5b31-132">Fork the GitHub repository to your GitHub account</span></span>](https://github.com/jcorioland/MyShop/tree/docker-linux)

>[!NOTE]
> <span data-ttu-id="a5b31-133">De Docker Swarm-orchestrator in Azure Container Service maakt gebruik van legacy standalone Swarm.</span><span class="sxs-lookup"><span data-stu-id="a5b31-133">The Docker Swarm orchestrator in Azure Container Service uses legacy standalone Swarm.</span></span> <span data-ttu-id="a5b31-134">Momenteel is de geïntegreerde [Swarm-modus](https://docs.docker.com/engine/swarm/) (in Docker 1.12 en hoger) geen ondersteunde orchestrator in Azure Container Service.</span><span class="sxs-lookup"><span data-stu-id="a5b31-134">Currently, the integrated [Swarm mode](https://docs.docker.com/engine/swarm/) (in Docker 1.12 and higher) is not a supported orchestrator in Azure Container Service.</span></span> <span data-ttu-id="a5b31-135">Daarom gebruiken we [ACS-Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), community-bijgedragen [snelstartsjabloon](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), of een Docker-oplossing in de [Azure Marketplace](https://azuremarketplace.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="a5b31-135">For this reason, we are using [ACS Engine](https://github.com/Azure/acs-engine/blob/master/docs/swarmmode.md), a community-contributed [quickstart template](https://azure.microsoft.com/resources/templates/101-acsengine-swarmmode/), or a Docker solution in the [Azure Marketplace](https://azuremarketplace.microsoft.com).</span></span>
>

## <a name="step-1-configure-your-visual-studio-team-services-account"></a><span data-ttu-id="a5b31-136">Stap 1: Uw Visual Studio Team Services-account configureren</span><span class="sxs-lookup"><span data-stu-id="a5b31-136">Step 1: Configure your Visual Studio Team Services account</span></span> 

<span data-ttu-id="a5b31-137">In deze sectie configureert u uw Visual Studio Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="a5b31-137">In this section, you configure your Visual Studio Team Services account.</span></span> <span data-ttu-id="a5b31-138">VSTS-Services-eindpunten configureren in uw project voor Visual Studio Team Services, klikt u op de **instellingen** pictogram in de werkbalk en selecteert u **Services**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-138">To configure VSTS Services Endpoints, in your Visual Studio Team Services project, click the **Settings** icon in the toolbar, and select **Services**.</span></span>

![Open Services-eindpunt](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/services-vsts.PNG)

### <a name="connect-visual-studio-team-services-and-azure-account"></a><span data-ttu-id="a5b31-140">Verbinding maken met Visual Studio Team Services en Azure-account</span><span class="sxs-lookup"><span data-stu-id="a5b31-140">Connect Visual Studio Team Services and Azure account</span></span>

<span data-ttu-id="a5b31-141">Een verbinding tussen uw project VSTS en uw Azure-account instellen.</span><span class="sxs-lookup"><span data-stu-id="a5b31-141">Set up a connection between your VSTS project and your Azure account.</span></span>

1. <span data-ttu-id="a5b31-142">Klik aan de linkerkant op **nieuwe Service-eindpunt** > **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-142">On the left, click **New Service Endpoint** > **Azure Resource Manager**.</span></span>
2. <span data-ttu-id="a5b31-143">Voor het autoriseren van VSTS werken met uw Azure-account, selecteer uw **abonnement** en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-143">To authorize VSTS to work with your Azure account, select your **Subscription** and click **OK**.</span></span>

    ![Visual Studio teamservices - autoriseren van Azure](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-azure.PNG)

### <a name="connect-visual-studio-team-services-and-github"></a><span data-ttu-id="a5b31-145">Verbinding maken met Visual Studio teamservices en GitHub</span><span class="sxs-lookup"><span data-stu-id="a5b31-145">Connect Visual Studio Team Services and GitHub</span></span>

<span data-ttu-id="a5b31-146">Een verbinding tussen uw project VSTS en uw GitHub-account instellen.</span><span class="sxs-lookup"><span data-stu-id="a5b31-146">Set up a connection between your VSTS project and your GitHub account.</span></span>

1. <span data-ttu-id="a5b31-147">Klik aan de linkerkant op **nieuwe Service-eindpunt** > **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-147">On the left, click **New Service Endpoint** > **GitHub**.</span></span>
2. <span data-ttu-id="a5b31-148">Als u wilt machtigen VSTS werken met uw GitHub-account, klikt u op **autoriseren** en volg de procedure in het venster dat wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="a5b31-148">To authorize VSTS to work with your GitHub account, click **Authorize** and follow the procedure in the window that opens.</span></span>

    ![Visual Studio teamservices - autoriseren GitHub](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github.png)

### <a name="connect-vsts-to-your-azure-container-service-cluster"></a><span data-ttu-id="a5b31-150">VSTS verbinding met uw Azure Container Service-cluster</span><span class="sxs-lookup"><span data-stu-id="a5b31-150">Connect VSTS to your Azure Container Service cluster</span></span>

<span data-ttu-id="a5b31-151">De laatste stappen voordat u in de pipeline CI/CD zijn voor het configureren van externe verbindingen met uw Docker Swarm-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="a5b31-151">The last steps before getting into the CI/CD pipeline are to configure external connections to your Docker Swarm cluster in Azure.</span></span> 

1. <span data-ttu-id="a5b31-152">Voeg een eindpunt van het type voor de Docker Swarm-cluster **SSH**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-152">For the Docker Swarm cluster, add an endpoint of type **SSH**.</span></span> <span data-ttu-id="a5b31-153">Voer vervolgens de SSH-verbindingsgegevens van de Swarm-cluster (master knooppunt).</span><span class="sxs-lookup"><span data-stu-id="a5b31-153">Then enter the SSH connection information of your Swarm cluster (master node).</span></span>

    ![Visual Studio Team Services - SSH](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-ssh.png)

<span data-ttu-id="a5b31-155">Alle van de configuratie wordt nu uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a5b31-155">All the configuration is done now.</span></span> <span data-ttu-id="a5b31-156">In de volgende stappen maakt u de CI/CD-pijplijn die u maakt en implementeert de toepassing op het Docker Swarm-cluster.</span><span class="sxs-lookup"><span data-stu-id="a5b31-156">In the next steps, you create the CI/CD pipeline that builds and deploys the application to the Docker Swarm cluster.</span></span> 

## <a name="step-2-create-the-build-definition"></a><span data-ttu-id="a5b31-157">Stap 2: De definitie van de build maken</span><span class="sxs-lookup"><span data-stu-id="a5b31-157">Step 2: Create the build definition</span></span>

<span data-ttu-id="a5b31-158">In deze stap maakt u een build-definitie voor uw project VSTS instellen en definiëren van de build-werkstroom voor de installatiekopieën van de container</span><span class="sxs-lookup"><span data-stu-id="a5b31-158">In this step, you set up a build definition for your VSTS project and define the build workflow for your container images</span></span>

### <a name="initial-definition-setup"></a><span data-ttu-id="a5b31-159">Initiële definitie setup</span><span class="sxs-lookup"><span data-stu-id="a5b31-159">Initial definition setup</span></span>

1. <span data-ttu-id="a5b31-160">De definitie van een build maken, koppelen aan uw project voor Visual Studio Team Services en klik op **bouwen & Release**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-160">To create a build definition, connect to your Visual Studio Team Services project and click **Build & Release**.</span></span> <span data-ttu-id="a5b31-161">In de **bouwen definities** sectie, klikt u op **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-161">In the **Build definitions** section, click **+ New**.</span></span> 

    ![Visual Studio teamservices - nieuwe bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-build-vsts.PNG)

2. <span data-ttu-id="a5b31-163">Selecteer de **leeg proces**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-163">Select the **Empty process**.</span></span>

    ![Visual Studio teamservices - nieuwe, lege bouwen definitie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/create-empty-build-vsts.PNG)

4. <span data-ttu-id="a5b31-165">Klik vervolgens op de **variabelen** tabblad en twee nieuwe variabelen maken: **RegistryURL** en **AgentURL**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-165">Then, click the **Variables** tab and create two new variables: **RegistryURL** and **AgentURL**.</span></span> <span data-ttu-id="a5b31-166">Plak de waarden van het register en DNS-Cluster-Agents.</span><span class="sxs-lookup"><span data-stu-id="a5b31-166">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio teamservices - variabelen Buildconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-variables.png)

5. <span data-ttu-id="a5b31-168">Op de **bouwen definities** pagina, open de **Triggers** tabblad en configureren van de build voor het gebruik van doorlopende integratie met de fork van het MyShop-project dat u hebt gemaakt in de vereisten.</span><span class="sxs-lookup"><span data-stu-id="a5b31-168">On the **Build Definitions** page, open the **Triggers** tab and configure the build to use continuous integration with the fork of the MyShop project that you created in the prerequisites.</span></span> <span data-ttu-id="a5b31-169">Selecteer **Batch wijzigingen**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-169">Then, select **Batch changes**.</span></span> <span data-ttu-id="a5b31-170">Zorg ervoor dat u selecteert *docker-linux* als de **vertakking specificatie**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-170">Make sure that you select *docker-linux* as the **Branch specification**.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-github-repo-conf.PNG)


6. <span data-ttu-id="a5b31-172">Ten slotte op de **opties** tabblad en configureren van de wachtrij agent naar **gehost Linux Preview**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-172">Finally, click the **Options** tab and configure the Default agent queue to **Hosted Linux Preview**.</span></span>

    ![Visual Studio teamservices - Agent de hostconfiguratie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-agent.png)

### <a name="define-the-build-workflow"></a><span data-ttu-id="a5b31-174">Definieer de build-werkstroom</span><span class="sxs-lookup"><span data-stu-id="a5b31-174">Define the build workflow</span></span>
<span data-ttu-id="a5b31-175">De volgende stappen definiëren de build-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="a5b31-175">The next steps define the build workflow.</span></span> <span data-ttu-id="a5b31-176">Eerst moet u de bron van de code te configureren.</span><span class="sxs-lookup"><span data-stu-id="a5b31-176">First, you need to configure the source of the code.</span></span> <span data-ttu-id="a5b31-177">Selecteer hiervoor **GitHub** en uw **opslagplaats** en **vertakking** (docker-linux).</span><span class="sxs-lookup"><span data-stu-id="a5b31-177">To do it, select **GitHub** and your **repository** and **branch** (docker-linux).</span></span>

![Visual Studio teamservices - configureren broncode](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-source-code.png)

<span data-ttu-id="a5b31-179">Er zijn vijf container afbeeldingen maken voor de *MyShop* toepassing.</span><span class="sxs-lookup"><span data-stu-id="a5b31-179">There are five container images to build for the *MyShop* application.</span></span> <span data-ttu-id="a5b31-180">Elke installatiekopie gebouwd met behulp van de Dockerfile zich in de projectmappen:</span><span class="sxs-lookup"><span data-stu-id="a5b31-180">Each image is built using the Dockerfile located in the project folders:</span></span>

* <span data-ttu-id="a5b31-181">ProductsApi</span><span class="sxs-lookup"><span data-stu-id="a5b31-181">ProductsApi</span></span>
* <span data-ttu-id="a5b31-182">Proxy</span><span class="sxs-lookup"><span data-stu-id="a5b31-182">Proxy</span></span>
* <span data-ttu-id="a5b31-183">RatingsApi</span><span class="sxs-lookup"><span data-stu-id="a5b31-183">RatingsApi</span></span>
* <span data-ttu-id="a5b31-184">RecommandationsApi</span><span class="sxs-lookup"><span data-stu-id="a5b31-184">RecommandationsApi</span></span>
* <span data-ttu-id="a5b31-185">Winkelpagina</span><span class="sxs-lookup"><span data-stu-id="a5b31-185">ShopFront</span></span>

<span data-ttu-id="a5b31-186">U moet twee Docker-stappen voor elke installatiekopie, één voor het bouwen van de installatiekopie en één voor de push-installatiekopie van het in het register van de Azure-container.</span><span class="sxs-lookup"><span data-stu-id="a5b31-186">You need two Docker steps for each image, one to build the image, and one to push the image in the Azure container registry.</span></span> 

1. <span data-ttu-id="a5b31-187">Klik op als u een stap in de werkstroom build **+ toevoegen build stap** en selecteer **Docker**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-187">To add a step in the build workflow, click **+ Add build step** and select **Docker**.</span></span>

    ![Visual Studio teamservices - toevoegen Build stappen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-add-task.png)

2. <span data-ttu-id="a5b31-189">Voor elke installatiekopie, configureert u één stap die gebruikmaakt van de `docker build` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a5b31-189">For each image, configure one step that uses the `docker build` command.</span></span>

    ![Visual Studio teamservices - Docker bouwen](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-build.png)

    <span data-ttu-id="a5b31-191">Voor de build-bewerking, selecteert u het register van de Container Azure de **bouwen van een installatiekopie van een** actie en de Dockerfile waarin elke installatiekopie.</span><span class="sxs-lookup"><span data-stu-id="a5b31-191">For the build operation, select your Azure Container Registry, the **Build an image** action, and the Dockerfile that defines each image.</span></span> <span data-ttu-id="a5b31-192">Instellen de **werkmap** als de hoofdmap Dockerfile definieert de **Installatiekopienaam**, en selecteer **meest recente code bevatten**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-192">Set the **Working Directory** as the Dockerfile root directory, define the **Image Name**, and select **Include Latest Tag**.</span></span>
    
    <span data-ttu-id="a5b31-193">Naam van de installatiekopie moet worden in deze indeling: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span><span class="sxs-lookup"><span data-stu-id="a5b31-193">The Image Name has to be in this format: ```$(RegistryURL)/[NAME]:$(Build.BuildId)```.</span></span> <span data-ttu-id="a5b31-194">Vervang **[NAME]** met de naam van de installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="a5b31-194">Replace **[NAME]** with the image name:</span></span>
    - ```proxy```
    - ```products-api```
    - ```ratings-api```
    - ```recommendations-api```
    - ```shopfront```

3. <span data-ttu-id="a5b31-195">Voor elke installatiekopie configureert u een tweede stap die gebruikmaakt van de `docker push` opdracht.</span><span class="sxs-lookup"><span data-stu-id="a5b31-195">For each image, configure a second step that uses the `docker push` command.</span></span>

    ![Visual Studio teamservices - Docker-Push](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-docker-push.png)

    <span data-ttu-id="a5b31-197">Voor de push-bewerking, selecteert u het register Azure container de **een installatiekopie van een Push** actie, voer de **installatiekopie met de naam** die is ingebouwd in de vorige stap en selecteer **meest recente code bevatten**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-197">For the push operation, select your Azure container registry, the **Push an image** action, enter the **Image Name** that is built in the previous step and select **Include Latest Tag**.</span></span>

4. <span data-ttu-id="a5b31-198">Nadat u de stappen build en pushmeldingen voor elk van de vijf afbeeldingen hebt geconfigureerd, moet u drie meer stappen toevoegen in de build-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="a5b31-198">After you configure the build and push steps for each of the five images, add three more steps in the build workflow.</span></span>

   ![Visual Studio teamservices - toevoegen opdrachtregelprogramma taak](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-command-task.png)

      1. <span data-ttu-id="a5b31-200">Een opdrachtregeltaak die gebruikmaakt van een bash-scripts ter vervanging van de *RegistryURL* exemplaar in de docker-compose.yml-bestand met de variabele RegistryURL.</span><span class="sxs-lookup"><span data-stu-id="a5b31-200">A command-line task that uses a bash script to replace the *RegistryURL* occurrence in the docker-compose.yml file with the RegistryURL variable.</span></span> 
    
          ```-c "sed -i 's/RegistryUrl/$(RegistryURL)/g' src/docker-compose-v3.yml"```

          ![Visual Studio teamservices - Update opstellen-bestand met de Register-URL](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-replace-registry.png)

      2. <span data-ttu-id="a5b31-202">Een opdrachtregeltaak die gebruikmaakt van een bash-scripts ter vervanging van de *AgentURL* exemplaar in de docker-compose.yml-bestand met de variabele AgentURL.</span><span class="sxs-lookup"><span data-stu-id="a5b31-202">A command-line task that uses a bash script to replace the *AgentURL* occurrence in the docker-compose.yml file with the AgentURL variable.</span></span>
  
          ```-c "sed -i 's/AgentUrl/$(AgentURL)/g' src/docker-compose-v3.yml"```

     3. <span data-ttu-id="a5b31-203">Een taak die het bijgewerkte opstellen-bestand als een artefact build zakt zodat deze kan worden gebruikt in de release.</span><span class="sxs-lookup"><span data-stu-id="a5b31-203">A task that drops the updated Compose file as a build artifact so it can be used in the release.</span></span> <span data-ttu-id="a5b31-204">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a5b31-204">See the following screen for details.</span></span>

         ![Visual Studio teamservices - publiceren artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish.png) 

         ![Visual Studio Team Services - opstellen publiceren bestand](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-publish-compose.png) 

5. <span data-ttu-id="a5b31-207">Klik op **opslaan en wachtrij** voor het testen van de definitie van de build.</span><span class="sxs-lookup"><span data-stu-id="a5b31-207">Click **Save & queue** to test your build definition.</span></span>

   ![Visual Studio teamservices - opslaan en wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-save.png) 

   ![Visual Studio teamservices - nieuwe wachtrij](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-queue.png) 

6. <span data-ttu-id="a5b31-210">Als de **bouwen** juist is, u moet dit scherm wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a5b31-210">If the **Build** is correct, you have to see this screen:</span></span>

  ![Visual Studio teamservices - Build is voltooid](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-build-succeeded.png) 

## <a name="step-3-create-the-release-definition"></a><span data-ttu-id="a5b31-212">Stap 3: De release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="a5b31-212">Step 3: Create the release definition</span></span>

<span data-ttu-id="a5b31-213">Visual Studio Team Services kunt u [releases beheren in omgevingen](https://www.visualstudio.com/team-services/release-management/).</span><span class="sxs-lookup"><span data-stu-id="a5b31-213">Visual Studio Team Services allows you to [manage releases across environments](https://www.visualstudio.com/team-services/release-management/).</span></span> <span data-ttu-id="a5b31-214">U kunt continue implementatie om ervoor te zorgen dat uw toepassing wordt geïmplementeerd op de verschillende omgevingen (zoals ontwikkelen, testen, preproductie en productie) in een goede manier inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a5b31-214">You can enable continuous deployment to make sure that your application is deployed on your different environments (such as dev, test, pre-production, and production) in a smooth way.</span></span> <span data-ttu-id="a5b31-215">U kunt een omgeving met uw Azure Container Service Docker Swarm modus cluster maken.</span><span class="sxs-lookup"><span data-stu-id="a5b31-215">You can create an environment that represents your Azure Container Service Docker Swarm Mode cluster.</span></span>

![Visual Studio teamservices - ACS-versie](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-acs.png) 

### <a name="initial-release-setup"></a><span data-ttu-id="a5b31-217">Installatie van de eerste release</span><span class="sxs-lookup"><span data-stu-id="a5b31-217">Initial release setup</span></span>

1. <span data-ttu-id="a5b31-218">Klik op om de definitie van een release **Releases** > **+ Release**</span><span class="sxs-lookup"><span data-stu-id="a5b31-218">To create a release definition, click **Releases** > **+ Release**</span></span>

2. <span data-ttu-id="a5b31-219">Als u wilt de artefacten configureren, klikt u op **artefacten** > **een artefact koppelingsbron**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-219">To configure the artifact source, Click **Artifacts** > **Link an artifact source**.</span></span> <span data-ttu-id="a5b31-220">Hier definitie voor dit nieuwe release koppeling naar de versie die u hebt gedefinieerd in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="a5b31-220">Here, link this new release definition to the build that you defined in the previous step.</span></span> <span data-ttu-id="a5b31-221">Hierna is vindt de docker-compose.yml-bestand u in de release-proces.</span><span class="sxs-lookup"><span data-stu-id="a5b31-221">After that, the docker-compose.yml file is available in the release process.</span></span>

    ![Visual Studio teamservices - Release artefacten](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-artefacts.png) 

3. <span data-ttu-id="a5b31-223">Voor het configureren van de trigger release, klikt u op **Triggers** en selecteer **continue implementatie**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-223">To configure the release trigger, click **Triggers** and select **Continuous Deployment**.</span></span> <span data-ttu-id="a5b31-224">De trigger niet instellen op dezelfde bron artefacten.</span><span class="sxs-lookup"><span data-stu-id="a5b31-224">Set the trigger on the same artifact source.</span></span> <span data-ttu-id="a5b31-225">Deze instelling zorgt ervoor dat er een nieuwe release wordt gestart wanneer de build voltooid is.</span><span class="sxs-lookup"><span data-stu-id="a5b31-225">This setting ensures that a new release starts when the build completes successfully.</span></span>

    ![Visual Studio teamservices - Release-Triggers](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-trigger.png) 

4. <span data-ttu-id="a5b31-227">Voor het configureren van de release-variabelen, klikt u op **variabelen** en selecteer **+ variabele** drie nieuwe variabelen maken met de gegevens van het register: **docker.username**, **docker.password**, en **docker.registry**.</span><span class="sxs-lookup"><span data-stu-id="a5b31-227">To configure the release variables, click **Variables** and select **+Variable** to create three new variables with the info of the registry: **docker.username**, **docker.password**, and **docker.registry**.</span></span> <span data-ttu-id="a5b31-228">Plak de waarden van het register en DNS-Cluster-Agents.</span><span class="sxs-lookup"><span data-stu-id="a5b31-228">Paste the values of your Registry and Cluster Agents DNS.</span></span>

    ![Visual Studio teamservices - configuratie van de Build-opslagplaats](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-variables.png)

    >[!IMPORTANT]
    > <span data-ttu-id="a5b31-230">Zoals u in het vorige scherm, klikt u op de **vergrendeling** checkbox in docker.password.</span><span class="sxs-lookup"><span data-stu-id="a5b31-230">As shown on the previous screen, click the **Lock** checkbox in docker.password.</span></span> <span data-ttu-id="a5b31-231">Deze instelling is belangrijk om te beperken van het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a5b31-231">This setting is important to restrict the password.</span></span>
    >

### <a name="define-the-release-workflow"></a><span data-ttu-id="a5b31-232">Definieer de release-werkstroom</span><span class="sxs-lookup"><span data-stu-id="a5b31-232">Define the release workflow</span></span>

<span data-ttu-id="a5b31-233">De werkstroom release bestaat uit twee taken die u toevoegt.</span><span class="sxs-lookup"><span data-stu-id="a5b31-233">The release workflow is composed of two tasks that you add.</span></span>

1. <span data-ttu-id="a5b31-234">Configureren van een taak voor het veilig de opstellen bestand kopiëren naar een *implementeren* map op het Docker Swarm hoofdknooppunt, met behulp van de SSH-verbinding die u eerder hebt geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="a5b31-234">Configure a task to securely copy the compose file to a *deploy* folder on the Docker Swarm master node, using the SSH connection you configured previously.</span></span> <span data-ttu-id="a5b31-235">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a5b31-235">See the following screen for details.</span></span>
    
    <span data-ttu-id="a5b31-236">Bronmap:```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span><span class="sxs-lookup"><span data-stu-id="a5b31-236">Source folder: ```$(System.DefaultWorkingDirectory)/MyShop-CI/drop```</span></span>

    ![Visual Studio teamservices - Release SCP](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-scp.png)

2. <span data-ttu-id="a5b31-238">Configureren van een tweede taak voor het uitvoeren van een bash-opdracht om uit te voeren `docker` en `docker stack deploy` opdrachten op het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="a5b31-238">Configure a second task to execute a bash command to run `docker` and `docker stack deploy` commands on the master node.</span></span> <span data-ttu-id="a5b31-239">Zie het volgende scherm voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a5b31-239">See the following screen for details.</span></span>

    ```docker login -u $(docker.username) -p $(docker.password) $(docker.registry) && export DOCKER_HOST=:2375 && cd deploy && docker stack deploy --compose-file docker-compose-v3.yml myshop --with-registry-auth```

    ![Visual Studio teamservices - Release Bash](./media/container-service-docker-swarm-mode-setup-ci-cd-acs-engine/vsts-release-bash.png)

    <span data-ttu-id="a5b31-241">De opdracht uitgevoerd op de hoofddoelserver gebruikt de Docker CLI en de CLI Docker Compose naar de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a5b31-241">The command executed on the master uses the Docker CLI and the Docker-Compose CLI to do the following tasks:</span></span>

    - <span data-ttu-id="a5b31-242">Aanmelden bij het register van de Azure-container (hierbij drie build-variabelen die zijn gedefinieerd in de **variabelen** tabblad)</span><span class="sxs-lookup"><span data-stu-id="a5b31-242">Log in to the Azure container registry (it uses three build variables that are defined in the **Variables** tab)</span></span>
    - <span data-ttu-id="a5b31-243">Definieer de **DOCKER_HOST** variabele werken met het Swarm-eindpunt (: 2375)</span><span class="sxs-lookup"><span data-stu-id="a5b31-243">Define the **DOCKER_HOST** variable to work with the Swarm endpoint (:2375)</span></span>
    - <span data-ttu-id="a5b31-244">Navigeer naar de *implementeren* map die door de voorgaande beveiligde kopie-taak is gemaakt en die de docker-compose.yml-bestand bevat</span><span class="sxs-lookup"><span data-stu-id="a5b31-244">Navigate to the *deploy* folder that was created by the preceding secure copy task and that contains the docker-compose.yml file</span></span> 
    - <span data-ttu-id="a5b31-245">Uitvoeren van `docker stack deploy` opdrachten die pull-de nieuwe afbeeldingen en de containers te maken.</span><span class="sxs-lookup"><span data-stu-id="a5b31-245">Execute `docker stack deploy` commands that pull the new images and create the containers.</span></span>

    >[!IMPORTANT]
    > <span data-ttu-id="a5b31-246">Zoals u in het vorige scherm, laat de **mislukken op STDERR** selectievakje uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a5b31-246">As shown on the previous screen, leave the **Fail on STDERR** checkbox unchecked.</span></span> <span data-ttu-id="a5b31-247">Deze instelling kunt u ons voltooien release vanwege `docker-compose` worden afgedrukt verschillende diagnostische berichten, zoals de containers zijn gestopt of op de uitvoer van de standaardfout wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="a5b31-247">This setting allows us to complete the release process due to `docker-compose` prints several diagnostic messages, such as containers are stopping or being deleted, on the standard error output.</span></span> <span data-ttu-id="a5b31-248">Als u het selectievakje inschakelt, rapporteert Visual Studio Team Services dat fouten zijn opgetreden tijdens de release, zelfs als alles goed gaat.</span><span class="sxs-lookup"><span data-stu-id="a5b31-248">If you check the checkbox, Visual Studio Team Services reports that errors occurred during the release, even if all goes well.</span></span>
    >
3. <span data-ttu-id="a5b31-249">Sla deze definitie voor de nieuwe versie.</span><span class="sxs-lookup"><span data-stu-id="a5b31-249">Save this new release definition.</span></span>

## <a name="step-4-test-the-cicd-pipeline"></a><span data-ttu-id="a5b31-250">Stap 4: De pijplijn CI/CD testen</span><span class="sxs-lookup"><span data-stu-id="a5b31-250">Step 4: Test the CI/CD pipeline</span></span>

<span data-ttu-id="a5b31-251">Nu u klaar bent met de configuratie, is het tijd voor het testen van dit nieuwe CI/CD-pijplijn.</span><span class="sxs-lookup"><span data-stu-id="a5b31-251">Now that you are done with the configuration, it's time to test this new CI/CD pipeline.</span></span> <span data-ttu-id="a5b31-252">De eenvoudigste manier om deze te testen, is voor het bijwerken van de broncode en voer de wijzigingen in uw GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="a5b31-252">The easiest way to test it is to update the source code and commit the changes into your GitHub repository.</span></span> <span data-ttu-id="a5b31-253">Enkele seconden nadat u de code pushen ziet u een nieuwe build uitgevoerd in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="a5b31-253">A few seconds after you push the code, you will see a new build running in Visual Studio Team Services.</span></span> <span data-ttu-id="a5b31-254">Zodra de installatie is voltooid, wordt een nieuwe release wordt geactiveerd en de nieuwe versie van de toepassing op het Azure Container Service-cluster wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a5b31-254">Once completed successfully, a new release is triggered and deployed the new version of the application on the Azure Container Service cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5b31-255">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a5b31-255">Next steps</span></span>

* <span data-ttu-id="a5b31-256">Zie voor meer informatie over CI/CD met Visual Studio Team Services, de [VSTS bouwen overzicht](https://www.visualstudio.com/docs/build/overview).</span><span class="sxs-lookup"><span data-stu-id="a5b31-256">For more information about CI/CD with Visual Studio Team Services, see the [VSTS Build overview](https://www.visualstudio.com/docs/build/overview).</span></span>
* <span data-ttu-id="a5b31-257">Zie voor meer informatie over de ACS-Engine de [ACS-Engine GitHub-repo-](https://github.com/Azure/acs-engine).</span><span class="sxs-lookup"><span data-stu-id="a5b31-257">For more information about ACS Engine, see the [ACS Engine GitHub repo](https://github.com/Azure/acs-engine).</span></span>
* <span data-ttu-id="a5b31-258">Zie voor meer informatie over Docker Swarm-modus, de [Docker Swarm modus overzicht](https://docs.docker.com/engine/swarm/).</span><span class="sxs-lookup"><span data-stu-id="a5b31-258">For more information about Docker Swarm mode, see the [Docker Swarm mode overview](https://docs.docker.com/engine/swarm/).</span></span>
