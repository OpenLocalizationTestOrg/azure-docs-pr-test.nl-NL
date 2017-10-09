---
title: aaaCI/CD van Jenkins tooAzure virtuele machines in een Team Services | Microsoft Docs
description: Stel doorlopende integratie (CI) en continue implementatie (CD) van een Node.js-app met behulp van Jenkins tooAzure virtuele machines van Release Management in Visual Studio Team Services (VSTS) of Microsoft Team Foundation Server (TFS)
author: ahomer
manager: douge
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/15/2017
ms.author: ahomer
ms.custom: mvc
ms.openlocfilehash: 400ae34cbdf45da65351811c0ff6ff5d61ef862c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-app-toolinux-vms-using-jenkins-and-team-services"></a><span data-ttu-id="773db-103">Uw app tooLinux virtuele machines implementeren met behulp van Jenkins en Team Services</span><span class="sxs-lookup"><span data-stu-id="773db-103">Deploy your app tooLinux VMs using Jenkins and Team Services</span></span>

<span data-ttu-id="773db-104">Continue integratie (CI) en continue implementatie (CD) is een pijplijn waarmee u kunt bouwen, vrijgeven en implementeer uw code.</span><span class="sxs-lookup"><span data-stu-id="773db-104">Continuous integration (CI) and continuous deployment (CD) is a pipeline by which you can build, release, and deploy your code.</span></span> <span data-ttu-id="773db-105">Teamservices biedt een complete, volledig functionele aantal CI/CD automation-hulpprogramma's voor implementatie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="773db-105">Team Services provides a complete, fully featured set of CI/CD automation tools for deployment tooAzure.</span></span> <span data-ttu-id="773db-106">Jenkins is een populaire 3rd derden CI/CD servergebaseerde hulpprogramma dat ook CI/CD automation biedt.</span><span class="sxs-lookup"><span data-stu-id="773db-106">Jenkins is a popular 3rd-party CI/CD server-based tool that also provides CI/CD automation.</span></span> <span data-ttu-id="773db-107">U kunt beide samen toocustomize hoe u uw cloud-app of service leveren.</span><span class="sxs-lookup"><span data-stu-id="773db-107">You can use both together toocustomize how you deliver your cloud app or service.</span></span>

<span data-ttu-id="773db-108">In deze zelfstudie gebruikt u Jenkins toobuild een **Node.js-web-app**, en Visual Studio Team Services toodeploy het tooa [implementatiegroep](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) met virtuele Linux-machines.</span><span class="sxs-lookup"><span data-stu-id="773db-108">In this tutorial, you use Jenkins toobuild a **Node.js web app**, and Visual Studio Team Services toodeploy it tooa [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) containing Linux virtual machines.</span></span>

<span data-ttu-id="773db-109">U gaat het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="773db-109">You will:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="773db-110">Uw app in Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="773db-110">Build your app in Jenkins</span></span>
> * <span data-ttu-id="773db-111">Jenkins configureren voor integratie met Team Services</span><span class="sxs-lookup"><span data-stu-id="773db-111">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="773db-112">Een implementatiegroep voor hello Azure virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="773db-112">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="773db-113">De definitie van een versie die Hallo VMs configureert en implementeert Hallo-app maken</span><span class="sxs-lookup"><span data-stu-id="773db-113">Create a release definition that configures hello VMs and deploys hello app</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="773db-114">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="773db-114">Before you begin</span></span>

* <span data-ttu-id="773db-115">U hebt toegang tot tooa Jenkins account nodig.</span><span class="sxs-lookup"><span data-stu-id="773db-115">You need access tooa Jenkins account.</span></span> <span data-ttu-id="773db-116">Als u een server Jenkins nog geen hebt gemaakt, raadpleegt u [Jenkins documentatie](https://jenkins.io/doc/).</span><span class="sxs-lookup"><span data-stu-id="773db-116">If you have not yet created a Jenkins server, see [Jenkins Documentation](https://jenkins.io/doc/).</span></span> 

* <span data-ttu-id="773db-117">Meld u aan tooyour Team Services-account (`https://{youraccount}.visualstudio.com`).</span><span class="sxs-lookup"><span data-stu-id="773db-117">Sign in tooyour Team Services account (`https://{youraccount}.visualstudio.com`).</span></span> 
  <span data-ttu-id="773db-118">U krijgt een [gratis account Team Services](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span><span class="sxs-lookup"><span data-stu-id="773db-118">You can get a [free Team Services account](https://go.microsoft.com/fwlink/?LinkId=307137&clcid=0x409&wt.mc_id=o~msft~vscom~home-vsts-hero~27308&campaign=o~msft~vscom~home-vsts-hero~27308).</span></span>

  > [!NOTE]
  > <span data-ttu-id="773db-119">Zie voor meer informatie [tooTeam Services verbinding](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="773db-119">For more information, see [Connect tooTeam Services](https://www.visualstudio.com/docs/setup-admin/team-services/connect-to-visual-studio-team-services).</span></span>

* <span data-ttu-id="773db-120">Maak een persoonlijk toegangstoken (PAT) in uw Team Services-account als u er nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="773db-120">Create a personal access token (PAT) in your Team Services account if you don't already have one.</span></span> <span data-ttu-id="773db-121">Jenkins vereist deze informatie tooaccess uw Team Services-account.</span><span class="sxs-lookup"><span data-stu-id="773db-121">Jenkins requires this information tooaccess your Team Services account.</span></span>
  <span data-ttu-id="773db-122">Lees [hoe maak ik een persoonlijk toegangstoken voor Team Services en TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn hoe toogenerate een.</span><span class="sxs-lookup"><span data-stu-id="773db-122">Read [How do I create a personal access token for Team Services and TFS](https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) toolearn how toogenerate one.</span></span>

## <a name="get-hello-sample-app"></a><span data-ttu-id="773db-123">Hallo voorbeeld-app downloaden</span><span class="sxs-lookup"><span data-stu-id="773db-123">Get hello sample app</span></span>

<span data-ttu-id="773db-124">U moet een app toodeploy opgeslagen in een Git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="773db-124">You need an app toodeploy stored in a Git repository.</span></span>
<span data-ttu-id="773db-125">Voor deze zelfstudie wordt aangeraden u [deze voorbeeldapp beschikbaar is via GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span><span class="sxs-lookup"><span data-stu-id="773db-125">For this tutorial, we recommend you use [this sample app available from GitHub](https://github.com/azooinmyluggage/fabrikam-node).</span></span>

1. <span data-ttu-id="773db-126">Maak een fork van deze app en noteer Hallo locatie (URL) voor gebruik in latere stappen van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="773db-126">Create a fork of this app and take note of hello location (URL) for use in later steps of this tutorial.</span></span>

1. <span data-ttu-id="773db-127">Controleer Hallo fork **openbare** toosimplify tooGitHub later verbinding te maken.</span><span class="sxs-lookup"><span data-stu-id="773db-127">Make hello fork **public** toosimplify connecting tooGitHub later.</span></span>

> [!NOTE]
> <span data-ttu-id="773db-128">Zie voor meer informatie [een opslagplaats vertakken](https://help.github.com/articles/fork-a-repo/) en [een opslagplaats voor persoonlijke openbaar te maken](https://help.github.com/articles/making-a-private-repository-public/).</span><span class="sxs-lookup"><span data-stu-id="773db-128">For more information, see [Fork a repo](https://help.github.com/articles/fork-a-repo/) and [Making a private repository public](https://help.github.com/articles/making-a-private-repository-public/).</span></span>

> [!NOTE]
> <span data-ttu-id="773db-129">Hallo-app is gemaakt met [Yeoman](http://yeoman.io/learning/index.html); hierbij **Express**, **bower**, en **grunt**; en heeft een aantal **npm**pakketten als afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="773db-129">hello app was built using [Yeoman](http://yeoman.io/learning/index.html); it uses **Express**, **bower**, and **grunt**; and it has some **npm** packages as dependencies.</span></span>
> <span data-ttu-id="773db-130">Hallo voorbeeld-app bevat een set [Azure Resource Manager-sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) dat zijn gebruikte toodynamically Hallo virtuele machines maken voor implementatie op Azure.</span><span class="sxs-lookup"><span data-stu-id="773db-130">hello sample app contains a set of [Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) that are used toodynamically create hello virtual machines for deployment on Azure.</span></span> <span data-ttu-id="773db-131">Deze sjablonen worden gebruikt door de taken in Hallo [Team Services release definitie](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span><span class="sxs-lookup"><span data-stu-id="773db-131">These templates are used by tasks in hello [Team Services release definition](https://www.visualstudio.com/docs/build/actions/work-with-release-definitions).</span></span>
> <span data-ttu-id="773db-132">Hallo belangrijkste sjabloon maakt u een netwerkbeveiligingsgroep en een virtuele machine een virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="773db-132">hello main template creates a network security group, a virtual machine, and a virtual network.</span></span> <span data-ttu-id="773db-133">Het een openbare IP-adres toewijst en binnenkomende poort 80 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="773db-133">It assigns a public IP address and opens inbound port 80.</span></span> <span data-ttu-id="773db-134">Ook een code die wordt gebruikt door Hallo implementatie te selecteren Hallo machines tooreceive Hallo implementatie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="773db-134">It also adds a tag that is used by hello deployment group too select hello machines tooreceive hello deployment.</span></span>
>
> <span data-ttu-id="773db-135">Hallo-voorbeeld bevat ook een script dat Nginx ingesteld en het Hallo-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="773db-135">hello sample also contains a script that sets up Nginx and deploys hello app.</span></span> <span data-ttu-id="773db-136">Deze wordt uitgevoerd op elke Hallo virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="773db-136">It is executed on each of hello virtual machines.</span></span> <span data-ttu-id="773db-137">In het bijzonder installeert Hallo script knooppunt, Nginx en PM2; Hiermee configureert u Nginx en PM2; vervolgens wordt de Hallo knooppunt app gestart.</span><span class="sxs-lookup"><span data-stu-id="773db-137">Specifically, hello script installs Node, Nginx, and PM2; configures Nginx and PM2; then starts hello Node app.</span></span>

## <a name="configure-jenkins-plugins"></a><span data-ttu-id="773db-138">Jenkins plugins configureren</span><span class="sxs-lookup"><span data-stu-id="773db-138">Configure Jenkins plugins</span></span>

<span data-ttu-id="773db-139">Eerst moet u twee Jenkins invoegtoepassingen voor **NodeJS** en **integratie met Team Services**.</span><span class="sxs-lookup"><span data-stu-id="773db-139">First, you must configure two Jenkins plugins for **NodeJS** and **Integration with Team Services**.</span></span>

1. <span data-ttu-id="773db-140">Open uw Jenkins-account en kies **Jenkins beheren**.</span><span class="sxs-lookup"><span data-stu-id="773db-140">Open your Jenkins account and choose **Manage Jenkins**.</span></span>

1. <span data-ttu-id="773db-141">In Hallo **beheren Jenkins** pagina **invoegtoepassingen beheren**.</span><span class="sxs-lookup"><span data-stu-id="773db-141">In hello **Manage Jenkins** page, choose **Manage Plugins**.</span></span>

1. <span data-ttu-id="773db-142">Filter Hallo lijst toolocate hello **NodeJS** invoegtoepassing en zonder opnieuw te installeren.</span><span class="sxs-lookup"><span data-stu-id="773db-142">Filter hello list toolocate hello **NodeJS** plugin and install it without restart.</span></span>

   ![Hallo NodeJS invoegtoepassing tooJenkins toevoegen](media/tutorial-build-deploy-jenkins/jenkins-nodejs-plugin.png)

1. <span data-ttu-id="773db-144">Filter Hallo lijst toofind hello **Team Foundation Server** invoegtoepassing en te installeren.</span><span class="sxs-lookup"><span data-stu-id="773db-144">Filter hello list toofind hello **Team Foundation Server** plugin and install it.</span></span> <span data-ttu-id="773db-145">(Deze invoegtoepassing werkt voor zowel Team Services en Team Foundation Server.) Jenkins opnieuw te starten is niet nodig.</span><span class="sxs-lookup"><span data-stu-id="773db-145">(This plug-in works for both Team Services and Team Foundation Server.) Restarting Jenkins is not necessary.</span></span>

## <a name="configure-jenkins-build-for-nodejs"></a><span data-ttu-id="773db-146">Jenkins build configureren voor Node.js</span><span class="sxs-lookup"><span data-stu-id="773db-146">Configure Jenkins build for Node.js</span></span>

<span data-ttu-id="773db-147">Maak een nieuwe build-project in Jenkins, en als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="773db-147">In Jenkins, create a new build project and configure it as follows:</span></span>

1. <span data-ttu-id="773db-148">In Hallo **algemene** tabblad, voer een naam voor uw project bouwen.</span><span class="sxs-lookup"><span data-stu-id="773db-148">In hello **General** tab, enter a name for your build project.</span></span>

1. <span data-ttu-id="773db-149">In Hallo **Source Code Management** tabblad **Git** en Hallo details van Hallo opslagplaats en Hallo vertakking met uw app-code invoeren.</span><span class="sxs-lookup"><span data-stu-id="773db-149">In hello **Source Code Management** tab, select **Git** and enter hello details of hello repository and hello branch containing your app code.</span></span>

   ![Een opslagplaats tooyour build toevoegen](media/tutorial-build-deploy-jenkins/jenkins-git.png)

   > [!NOTE]
   > <span data-ttu-id="773db-151">Als uw opslagplaats niet openbaar is, kiest u **toevoegen** en referenties tooconnect tooit bieden.</span><span class="sxs-lookup"><span data-stu-id="773db-151">If your repository is not public, choose **Add** and provide credentials tooconnect tooit.</span></span>

1. <span data-ttu-id="773db-152">In Hallo **bouwen Triggers** tabblad **Poll SCM** en Voer Hallo planning `H/03 * * * *` toopoll Hallo Git-opslagplaats voor elke drie minuten wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="773db-152">In hello **Build Triggers** tab, select **Poll SCM** and enter hello schedule `H/03 * * * *` toopoll hello Git repository for changes every three minutes.</span></span> 

1. <span data-ttu-id="773db-153">In Hallo **bouwen omgeving** tabblad **bieden knooppunt &amp; npm bin / map pad** en voer `NodeJS` voor Hallo knooppunt JS installatie waarde.</span><span class="sxs-lookup"><span data-stu-id="773db-153">In hello **Build Environment** tab, select **Provide Node &amp; npm bin/ folder PATH** and enter `NodeJS` for hello Node JS Installation value.</span></span> <span data-ttu-id="773db-154">Laat **npmrc bestand** ingesteld op "systeemstandaard gebruiken".</span><span class="sxs-lookup"><span data-stu-id="773db-154">Leave **npmrc file** set to "use system default."</span></span>

1. <span data-ttu-id="773db-155">In Hallo **bouwen** tabblad, gebruikt u de opdracht Hallo `npm install` tooensure alle afhankelijkheden zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="773db-155">In hello **Build** tab, enter hello command `npm install` tooensure all dependencies are updated.</span></span>

## <a name="configure-jenkins-for-team-services-integration"></a><span data-ttu-id="773db-156">Jenkins configureren voor integratie met Team Services</span><span class="sxs-lookup"><span data-stu-id="773db-156">Configure Jenkins for Team Services integration</span></span>

1. <span data-ttu-id="773db-157">In Hallo **na build acties** tabblad voor **bestanden tooarchive**, voer `**/*` tooinclude alle bestanden.</span><span class="sxs-lookup"><span data-stu-id="773db-157">In hello **Post-build Actions** tab, for **Files tooarchive**, enter `**/*` tooinclude all files.</span></span>

1. <span data-ttu-id="773db-158">Voor **release in TFS/Team Services activeren**, Hallo volledige URL van uw account opgeven (zoals `https://your-account-name.visualstudio.com`), Hallo projectnaam, een naam voor de definitie van release hello (later gemaakt), en Hallo referenties tooconnect tooyour account.</span><span class="sxs-lookup"><span data-stu-id="773db-158">For **Trigger release in TFS/Team Services**, enter hello full URL of your account (such as `https://your-account-name.visualstudio.com`), hello project name, a name for hello release definition (created later), and hello credentials tooconnect tooyour account.</span></span>
   <span data-ttu-id="773db-159">U moet uw gebruikersnaam en het Hallo PAT die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="773db-159">You need your user name and hello PAT you created earlier.</span></span> 

   ![Jenkins na build acties configureren](media/tutorial-build-deploy-jenkins/trigger-release-from-jenkins.png)

1. <span data-ttu-id="773db-161">Hallo build project opslaan.</span><span class="sxs-lookup"><span data-stu-id="773db-161">Save hello build project.</span></span>

## <a name="create-a-jenkins-service-endpoint"></a><span data-ttu-id="773db-162">Een Jenkins service-eindpunt maken</span><span class="sxs-lookup"><span data-stu-id="773db-162">Create a Jenkins service endpoint</span></span>

<span data-ttu-id="773db-163">Een service-eindpunt kunt Team Services tooconnect tooJenkins.</span><span class="sxs-lookup"><span data-stu-id="773db-163">A service endpoint allows Team Services tooconnect tooJenkins.</span></span>

1. <span data-ttu-id="773db-164">Open Hallo **Services** pagina in een Team Services, open Hallo **nieuwe Service-eindpunt** lijst en kies **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="773db-164">Open hello **Services** page in Team Services, open hello **New Service Endpoint** list, and choose **Jenkins**.</span></span>

   ![Een eindpunt Jenkins toevoegen](media/tutorial-build-deploy-jenkins/add-jenkins-endpoint.png)

1. <span data-ttu-id="773db-166">Voer een naam die u toorefer toothis verbinding wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="773db-166">Enter a name you will use toorefer toothis connection.</span></span>

1. <span data-ttu-id="773db-167">Voer Hallo-URL van uw server Jenkins en maatstreepjes Hallo **accepteren van niet-vertrouwde certificaten voor SSL** optie.</span><span class="sxs-lookup"><span data-stu-id="773db-167">Enter hello URL of your Jenkins server, and tick hello **Accept untrusted SSL certificates** option.</span></span>

1. <span data-ttu-id="773db-168">Hallo-gebruikersnaam en wachtwoord invoeren voor uw account Jenkins.</span><span class="sxs-lookup"><span data-stu-id="773db-168">Enter hello user name and password for your Jenkins account.</span></span>

1. <span data-ttu-id="773db-169">Kies **verbinding controleren** toocheck die Hallo informatie juist is.</span><span class="sxs-lookup"><span data-stu-id="773db-169">Choose **Verify connection** toocheck that hello information is correct.</span></span>

1. <span data-ttu-id="773db-170">Kies **OK** toocreate Hallo service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="773db-170">Choose **OK** toocreate hello service endpoint.</span></span>

## <a name="create-a-deployment-group"></a><span data-ttu-id="773db-171">Een implementatiegroep maken</span><span class="sxs-lookup"><span data-stu-id="773db-171">Create a deployment group</span></span>

<span data-ttu-id="773db-172">U moet een [implementatiegroep](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) Hallo virtuele machines te bevatten.</span><span class="sxs-lookup"><span data-stu-id="773db-172">You need a [deployment group](https://www.visualstudio.com/docs/build/concepts/definitions/release/deployment-groups/) too contain hello virtual machines.</span></span>

1. <span data-ttu-id="773db-173">Open Hallo **Releases** tabblad Hallo **bouwen &amp; Release** hub en open Hallo **implementatiegroepen** tabblad en kies **+ nieuw**.</span><span class="sxs-lookup"><span data-stu-id="773db-173">Open hello **Releases** tab of hello **Build &amp; Release** hub, then open hello **Deployment groups** tab, and choose **+ New**.</span></span>

1. <span data-ttu-id="773db-174">Voer een naam voor de groep van Hallo-implementatie, en een optionele beschrijving.</span><span class="sxs-lookup"><span data-stu-id="773db-174">Enter a name for hello deployment group, and an optional description.</span></span>
   <span data-ttu-id="773db-175">Kies vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="773db-175">Then choose **Create**.</span></span>

<span data-ttu-id="773db-176">Hello Azure Resource Group Deployment taak maakt en registreert Hallo VM's wanneer deze wordt uitgevoerd met behulp van hello Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="773db-176">hello Azure Resource Group Deployment task creates and registers hello VMs when it runs using hello Azure Resource Manager template.</span></span>
<span data-ttu-id="773db-177">U geen toocreate nodig hebt en Hallo virtuele machines uzelf te registreren.</span><span class="sxs-lookup"><span data-stu-id="773db-177">You don't need toocreate and register hello virtual machines yourself.</span></span>

## <a name="create-a-release-definition"></a><span data-ttu-id="773db-178">Een release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="773db-178">Create a release definition</span></span>

<span data-ttu-id="773db-179">De definitie van een release geeft Hallo proces Team Services toodeploy Hallo app wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="773db-179">A release definition specifies hello process Team Services will execute toodeploy hello app.</span></span>
<span data-ttu-id="773db-180">toocreate hello release definitie in Team Services:</span><span class="sxs-lookup"><span data-stu-id="773db-180">toocreate hello release definition in Team Services:</span></span>

1. <span data-ttu-id="773db-181">Open Hallo **Releases** tabblad Hallo **bouwen &amp; Release** hub, open Hallo  **+**  omlaag in de lijst Hallo van release definities en kies Hallo **maken release definitie**.</span><span class="sxs-lookup"><span data-stu-id="773db-181">Open hello **Releases** tab of hello **Build &amp; Release** hub, open hello **+** drop-down in hello list of release definitions, and choose hello **Create release definition**.</span></span> 

1. <span data-ttu-id="773db-182">Selecteer Hallo **leeg** sjabloon en kies **volgende**.</span><span class="sxs-lookup"><span data-stu-id="773db-182">Select hello **Empty** template and choose **Next**.</span></span>

1. <span data-ttu-id="773db-183">In Hallo **artefacten** sectie, klikt u op **koppelen van een artefact** en kies **Jenkins**.</span><span class="sxs-lookup"><span data-stu-id="773db-183">In hello **Artifacts** section, click on **Link an Artifact** and choose **Jenkins**.</span></span> <span data-ttu-id="773db-184">Selecteer uw verbinding Jenkins service-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="773db-184">Select your Jenkins service endpoint connection.</span></span> <span data-ttu-id="773db-185">Vervolgens selecteert u Hallo Jenkins bron taak en kies **maken**.</span><span class="sxs-lookup"><span data-stu-id="773db-185">Then select hello Jenkins source job and choose **Create**.</span></span> 

1. <span data-ttu-id="773db-186">In de nieuwe Hallo definitie release, kies **+ taken toevoegen** en voeg een **Azure Resource Group Deployment** taak toohello standaardomgeving.</span><span class="sxs-lookup"><span data-stu-id="773db-186">In hello new release definition, choose **+ Add tasks** and add an **Azure Resource Group Deployment** task toohello default environment.</span></span>

1. <span data-ttu-id="773db-187">Kies Hallo vervolgkeuzelijst pijl volgende toohello **+ taken toevoegen** koppelen en het toevoegen van een implementatie fase toohello groepsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="773db-187">Choose hello drop down arrow next toohello **+ Add tasks** link and add a deployment group phase toohello definition.</span></span>

   ![Toevoegen van een groep implementatiefase](media/tutorial-build-deploy-jenkins/deployment-group-phase-in-release-definition.png) 

1. <span data-ttu-id="773db-189">Open in Hallo taak catalogus Hallo **hulpprogramma** sectie en het toevoegen van een exemplaar van Hallo **Shell-Script** taak.</span><span class="sxs-lookup"><span data-stu-id="773db-189">In hello Task catalog, open hello **Utility** section and add an instance of hello **Shell Script** task.</span></span>

1. <span data-ttu-id="773db-190">Hallo parameters sjabloon die wordt gebruikt in hello Azure Resource Group Deployment taak stelt Hallo beheerder serverwachtwoord tooconnect toohello virtuele machines.</span><span class="sxs-lookup"><span data-stu-id="773db-190">hello parameters template used in hello Azure Resource Group Deployment task sets hello admin password used tooconnect toohello VMs.</span></span>
   <span data-ttu-id="773db-191">U wachtwoord opgeven met de variabele Hallo **$(adminpassword)**:</span><span class="sxs-lookup"><span data-stu-id="773db-191">You provide this password with hello variable **$(adminpassword)**:</span></span>
   
   - <span data-ttu-id="773db-192">Open Hallo **variabelen** tabblad en, in Hallo **variabelen** sectie, voert u de naam van de Hallo `adminpassword`.</span><span class="sxs-lookup"><span data-stu-id="773db-192">Open hello **Variables** tab and, in hello **Variables** section, enter hello name `adminpassword`.</span></span>

   - <span data-ttu-id="773db-193">Hallo beheerderswachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="773db-193">Enter hello administrator password.</span></span>

   - <span data-ttu-id="773db-194">Hallo 'hangslot' pictogram volgende toohello waarde textbox tooprotect Hallo wachtwoord kiezen.</span><span class="sxs-lookup"><span data-stu-id="773db-194">Choose hello "padlock" icon next toohello value textbox tooprotect hello password.</span></span> 

## <a name="configure-hello-azure-resource-group-deployment-task"></a><span data-ttu-id="773db-195">Hello Azure Resource Group Deployment taak configureren</span><span class="sxs-lookup"><span data-stu-id="773db-195">Configure hello Azure Resource Group Deployment task</span></span>

<span data-ttu-id="773db-196">Hallo **Azure Resource Group Deployment** taak gebruikte toocreate hello implementatiegroep is.</span><span class="sxs-lookup"><span data-stu-id="773db-196">hello **Azure Resource Group Deployment** task is used toocreate hello deployment group.</span></span> <span data-ttu-id="773db-197">Als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="773db-197">Configure it as follows:</span></span>

* <span data-ttu-id="773db-198">**Azure-abonnement:** Selecteer een verbinding in de lijst onder Hallo **beschikbare Azure serviceverbindingen**.</span><span class="sxs-lookup"><span data-stu-id="773db-198">**Azure Subscription:** Select a connection from hello list under **Available Azure Service Connections**.</span></span> 
  <span data-ttu-id="773db-199">Als geen verbindingen worden weergegeven, kiest u **beheren**, selecteer **nieuwe Service-eindpunt** vervolgens **Azure Resource Manager**, en volg de aanwijzingen Hallo.</span><span class="sxs-lookup"><span data-stu-id="773db-199">If no connections appear, choose **Manage**, select **New Service Endpoint** then **Azure Resource Manager**, and follow hello prompts.</span></span>
  <span data-ttu-id="773db-200">Definitie van tooyour release, vernieuwen Hallo retourneren **AzureRM abonnement** lijst, en selecteer Hallo-verbinding die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="773db-200">Return tooyour release definition, refresh hello **AzureRM Subscription** list, and select hello connection you created.</span></span>

* <span data-ttu-id="773db-201">**Resourcegroep**: Voer een naam in van Hallo-resourcegroep die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="773db-201">**Resource group**: Enter a name of hello resource group you created earlier.</span></span>

* <span data-ttu-id="773db-202">**Locatie**: Selecteer een regio voor Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="773db-202">**Location**: Select a region for hello deployment.</span></span>

  ![Een nieuwe resourcegroep maken](media/tutorial-build-deploy-jenkins/provision-web-server.png)

* <span data-ttu-id="773db-204">**Sjabloonlocatie**:`URL of hello file`</span><span class="sxs-lookup"><span data-stu-id="773db-204">**Template location**: `URL of hello file`</span></span>

* <span data-ttu-id="773db-205">**Sjabloonkoppeling**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span><span class="sxs-lookup"><span data-stu-id="773db-205">**Template link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.json`</span></span>

* <span data-ttu-id="773db-206">**Koppeling van sjabloon parameters**:`{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span><span class="sxs-lookup"><span data-stu-id="773db-206">**Template parameters link**: `{your-git-repo}/ARM-Templates/UbuntuWeb1.parameters.json`</span></span>

* <span data-ttu-id="773db-207">**Sjabloonparameters overschrijven**: een lijst met Hallo onderdrukkingswaarden, bijvoorbeeld: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span><span class="sxs-lookup"><span data-stu-id="773db-207">**Override template parameters**: A list of hello override values, for example: `-location {location} -virtualMachineName {machine] -virtualMachineSize Standard_DS1_v2 -adminUsername {username} -virtualNetworkName fabrikam-node-rg-vnet -networkInterfaceName fabrikam-node-websvr1 -networkSecurityGroupName fabrikam-node-websvr1-nsg -adminPassword $(adminpassword) -diagnosticsStorageAccountName fabrikamnodewebsvr1 -diagnosticsStorageAccountId Microsoft.Storage/storageAccounts/fabrikamnodewebsvr1 -diagnosticsStorageAccountType Standard_LRS -addressPrefix 172.16.8.0/24 -subnetName default -subnetPrefix 172.16.8.0/24 -publicIpAddressName fabrikam-node-websvr1-ip -publicIpAddressType Dynamic`.</span></span><br /><span data-ttu-id="773db-208">Voeg in uw eigen specifieke waarden Hallo {tijdelijke aanduidingen}.</span><span class="sxs-lookup"><span data-stu-id="773db-208">Insert your own specific values for hello {placeholders}.</span></span> 

* <span data-ttu-id="773db-209">**Vereiste onderdelen inschakelt**:`Configure with Deployment Group agent`</span><span class="sxs-lookup"><span data-stu-id="773db-209">**Enable prerequisites**: `Configure with Deployment Group agent`</span></span>

* <span data-ttu-id="773db-210">**TFS/VSTS eindpunt**: kies **toevoegen** en selecteer in het dialoogvenster 'Nieuw Team Foundation Server-Team Services-verbinding toevoegen' hello **tokenverificatie op basis van**.</span><span class="sxs-lookup"><span data-stu-id="773db-210">**TFS/VSTS endpoint**: Choose **Add** and, in hello "Add new Team Foundation Server/Team Services Connection" dialog, select **Token Based Authentication**.</span></span> <span data-ttu-id="773db-211">Voer een naam van de verbinding Hallo en Hallo-URL van uw teamproject.</span><span class="sxs-lookup"><span data-stu-id="773db-211">Enter a name of hello connection and hello URL of your team project.</span></span> <span data-ttu-id="773db-212">Vervolgens genereren en voer een [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate Hallo verbinding tooyour-teamproject.</span><span class="sxs-lookup"><span data-stu-id="773db-212">Then generate and enter a [Personal Access Token (PAT)]( https://www.visualstudio.com/docs/setup-admin/team-services/use-personal-access-tokens-to-authenticate) tooauthenticate hello connection tooyour team project.</span></span>

  ![Maken van een persoonlijk toegangstoken](media/tutorial-build-deploy-jenkins/create-a-pat.png)

* <span data-ttu-id="773db-214">**Teamproject**: Selecteer het huidige project.</span><span class="sxs-lookup"><span data-stu-id="773db-214">**Team project**: Select your current project.</span></span>

* <span data-ttu-id="773db-215">**Implementatiegroep**: Voer dezelfde implementatie groepsnaam Hallo als u voor Hallo gebruikt **resourcegroep** parameter.</span><span class="sxs-lookup"><span data-stu-id="773db-215">**Deployment Group**: Enter hello same deployment group name as you used for hello **Resource group** parameter.</span></span>

<span data-ttu-id="773db-216">Hallo standaardinstellingen voor hello Azure Resource Group Deployment taak toocreate zijn of een resource en toodo dus stapsgewijs bijwerken.</span><span class="sxs-lookup"><span data-stu-id="773db-216">hello default settings for hello Azure Resource Group Deployment task are toocreate or update a resource, and toodo so incrementally.</span></span> <span data-ttu-id="773db-217">Hallo taak maakt Hallo VMs Hallo eerste keer wordt uitgevoerd en ze vervolgens net bijwerken.</span><span class="sxs-lookup"><span data-stu-id="773db-217">hello task creates hello VMs hello first time it runs, and subsequently just update them.</span></span>

## <a name="configure-hello-shell-script-task"></a><span data-ttu-id="773db-218">Hallo shellscript taak configureren</span><span class="sxs-lookup"><span data-stu-id="773db-218">Configure hello Shell Script task</span></span>

<span data-ttu-id="773db-219">Hallo **Shell-Script** taak gebruikte tooprovide Hallo configuratie voor een script toorun op elke server tooinstall Node.js en start Hallo app is.</span><span class="sxs-lookup"><span data-stu-id="773db-219">hello **Shell Script** task is used tooprovide hello configuration for a script toorun on each server tooinstall Node.js and start hello app.</span></span> <span data-ttu-id="773db-220">Als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="773db-220">Configure it as follows:</span></span>

* <span data-ttu-id="773db-221">**Pad naar een script**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span><span class="sxs-lookup"><span data-stu-id="773db-221">**Script Path**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node/deployscript.sh`</span></span>

* <span data-ttu-id="773db-222">**Geef werkende Directory**:`Checked`</span><span class="sxs-lookup"><span data-stu-id="773db-222">**Specify Working Directory**: `Checked`</span></span>

* <span data-ttu-id="773db-223">**Werkmap**:`$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span><span class="sxs-lookup"><span data-stu-id="773db-223">**Working Directory**: `$(System.DefaultWorkingDirectory)/Fabrikam-Node`</span></span>
   
## <a name="rename-and-save-hello-release-definition"></a><span data-ttu-id="773db-224">Wijzig de naam en Hallo release definitie op te slaan</span><span class="sxs-lookup"><span data-stu-id="773db-224">Rename and save hello release definition</span></span>

1. <span data-ttu-id="773db-225">Bewerken Hallo naam van Hallo release definitie toohello u hebt opgegeven in de **na build acties** tabblad van Hallo build in Jenkins.</span><span class="sxs-lookup"><span data-stu-id="773db-225">Edit hello name of hello release definition toohello name you specified in the **Post-build Actions** tab of hello build in Jenkins.</span></span> <span data-ttu-id="773db-226">Jenkins vereist deze naam toobe kunnen tootrigger een nieuwe release wanneer Hallo bron artefacten zijn bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="773db-226">Jenkins requires this name toobe able tootrigger a new release when hello source artifacts are updated.</span></span>

1. <span data-ttu-id="773db-227">Hallo-naam van Hallo omgeving desgewenst wijzigen door te klikken op Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="773db-227">Optionally, change hello name of hello environment by clicking on hello name.</span></span> 

1. <span data-ttu-id="773db-228">Kies **opslaan**, en kies **OK**.</span><span class="sxs-lookup"><span data-stu-id="773db-228">Choose **Save**, and choose **OK**.</span></span>

## <a name="start-a-manual-deployment"></a><span data-ttu-id="773db-229">Start een handmatige implementatie</span><span class="sxs-lookup"><span data-stu-id="773db-229">Start a manual deployment</span></span>

1. <span data-ttu-id="773db-230">Kies **+ Release** en selecteer **maken Release**.</span><span class="sxs-lookup"><span data-stu-id="773db-230">Choose **+ Release** and select **Create Release**.</span></span>

1. <span data-ttu-id="773db-231">Hallo-build u voltooid Hallo gemarkeerde vervolgkeuzelijst selecteert en kiest **maken**.</span><span class="sxs-lookup"><span data-stu-id="773db-231">Select hello build you completed in hello highlighted drop-down list and choose **Create**.</span></span>

1. <span data-ttu-id="773db-232">Kies Hallo release koppeling in het pop-upbericht Hallo.</span><span class="sxs-lookup"><span data-stu-id="773db-232">Choose hello release link in hello popup message.</span></span> <span data-ttu-id="773db-233">Bijvoorbeeld: ' Release **Release 1** is gemaakt. "</span><span class="sxs-lookup"><span data-stu-id="773db-233">For example: "Release **Release-1** has been created."</span></span>

1. <span data-ttu-id="773db-234">Open Hallo **logboeken** tabblad toowatch Hallo release console-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="773db-234">Open hello **Logs** tab toowatch hello release console output.</span></span>

1. <span data-ttu-id="773db-235">Open in uw browser Hallo-URL van een van de servers Hallo u tooyour implementatiegroep toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="773db-235">In your browser, open hello URL of one of hello servers you added tooyour deployment group.</span></span> <span data-ttu-id="773db-236">Voer bijvoorbeeld`http://{your-server-ip-address}`</span><span class="sxs-lookup"><span data-stu-id="773db-236">For example, enter `http://{your-server-ip-address}`</span></span>

## <a name="start-a-cicd-deployment"></a><span data-ttu-id="773db-237">Start een CI/CD-implementatie</span><span class="sxs-lookup"><span data-stu-id="773db-237">Start a CI/CD deployment</span></span>

1. <span data-ttu-id="773db-238">Release definitie in hello, schakelt u Hallo **ingeschakeld** checkbox in Hallo **beheeropties** sectie van het Hallo-instellingen voor hello Azure Resource Group Deployment taak.</span><span class="sxs-lookup"><span data-stu-id="773db-238">In hello release definition, uncheck hello **Enabled** checkbox in hello **Control Options** section of hello settings for hello Azure Resource Group Deployment task.</span></span>
   <span data-ttu-id="773db-239">Voor toekomstige implementaties toohello bestaande implementatiegroep, hoeft u niet toore-deze taak niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="773db-239">For future deployments toohello existing deployment group, you do not need toore-execute this task.</span></span>

1. <span data-ttu-id="773db-240">Ga toohello bron Git-opslagplaats en Hallo inhoud Hallo wijzigen **h1** in de kop van Hallo bestand [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span><span class="sxs-lookup"><span data-stu-id="773db-240">Go toohello source Git repository and modify hello contents of hello **h1** heading in hello file [app/views/index.jade](https://github.com/azooinmyluggage/fabrikam-node/blob/master/app/views/index.jade).</span></span>

1. <span data-ttu-id="773db-241">Uw wijzigingen worden doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="773db-241">Commit your change.</span></span>

1. <span data-ttu-id="773db-242">Na een paar minuten ziet u een nieuwe release gemaakt in Hallo **Releases** pagina van het Team Services of TFS.</span><span class="sxs-lookup"><span data-stu-id="773db-242">After a few minutes, you will see a new release created in hello **Releases** page of Team Services or TFS.</span></span> <span data-ttu-id="773db-243">Open Hallo release toosee Hallo implementatie plaatsvinden.</span><span class="sxs-lookup"><span data-stu-id="773db-243">Open hello release toosee hello deployment taking place.</span></span> <span data-ttu-id="773db-244">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="773db-244">Congratulations!</span></span>

## <a name="next-steps"></a><span data-ttu-id="773db-245">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="773db-245">Next Steps</span></span>

<span data-ttu-id="773db-246">In deze zelfstudie maakt geautomatiseerde u Hallo-implementatie van een app tooAzure met Jenkins build en Team Services voor release.</span><span class="sxs-lookup"><span data-stu-id="773db-246">In this tutorial, you automated hello deployment of an app tooAzure using Jenkins build and Team Services for release.</span></span> <span data-ttu-id="773db-247">U hebt geleerd hoe u:</span><span class="sxs-lookup"><span data-stu-id="773db-247">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="773db-248">Uw app in Jenkins maken</span><span class="sxs-lookup"><span data-stu-id="773db-248">Build your app in Jenkins</span></span>
> * <span data-ttu-id="773db-249">Jenkins configureren voor integratie met Team Services</span><span class="sxs-lookup"><span data-stu-id="773db-249">Configure Jenkins for Team Services integration</span></span>
> * <span data-ttu-id="773db-250">Een implementatiegroep voor hello Azure virtuele machines maken</span><span class="sxs-lookup"><span data-stu-id="773db-250">Create a deployment group for hello Azure virtual machines</span></span>
> * <span data-ttu-id="773db-251">De definitie van een versie die Hallo VMs configureert en implementeert Hallo-app maken</span><span class="sxs-lookup"><span data-stu-id="773db-251">Create a release definition that configures hello VMs and deploys hello app</span></span>

<span data-ttu-id="773db-252">De volgende zelfstudie toolearn toohello voor vooraf meer informatie over hoe stack is toodeploy een licht (Linux, Apache, MySQL en PHP).</span><span class="sxs-lookup"><span data-stu-id="773db-252">Advance toohello next tutorial toolearn more about how toodeploy a LAMP (Linux, Apache, MySQL, and PHP) stack.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="773db-253">LAMP-stack implementeren</span><span class="sxs-lookup"><span data-stu-id="773db-253">Deploy LAMP stack</span></span>](tutorial-lamp-stack.md)