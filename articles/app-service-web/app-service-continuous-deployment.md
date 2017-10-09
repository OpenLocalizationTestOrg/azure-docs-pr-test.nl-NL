---
title: aaaContinuous implementatie tooAzure App Service | Microsoft Docs
description: Meer informatie over hoe tooenable continue implementatie tooAzure App Service.
services: app-service
documentationcenter: 
author: dariagrigoriu
manager: erikre
editor: mollybos
ms.assetid: 6adb5c84-6cf3-424e-a336-c554f23b4000
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: dariagrigoriu
ms.openlocfilehash: 62a22cbda354fd5b0a1b9729c8c375408e75049f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-deployment-tooazure-app-service"></a><span data-ttu-id="0265e-103">Doorlopende implementatie tooAzure App Service</span><span class="sxs-lookup"><span data-stu-id="0265e-103">Continuous Deployment tooAzure App Service</span></span>
<span data-ttu-id="0265e-104">Deze zelfstudie leert u hoe tooconfigure een werkstroom continue implementatie voor uw [Azure App Service] app.</span><span class="sxs-lookup"><span data-stu-id="0265e-104">This tutorial shows you how tooconfigure a continuous deployment workflow for your [Azure App Service] app.</span></span> <span data-ttu-id="0265e-105">App Service-integratie met BitBucket, GitHub en [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) kunnen een continue implementatiewerkstroom waarbij Azure in de meest recente updates Hallo van uw project ophaalt gepubliceerd tooone van deze services.</span><span class="sxs-lookup"><span data-stu-id="0265e-105">App Service integration with BitBucket, GitHub, and [Visual Studio Team Services (VSTS)](https://www.visualstudio.com/team-services/) enables a continuous deployment workflow where Azure pulls in hello most recent updates from your project published tooone of these services.</span></span> <span data-ttu-id="0265e-106">Continue implementatie is een goede optie voor projecten waar meerdere en regelmatige bijdragen worden geïntegreerd.</span><span class="sxs-lookup"><span data-stu-id="0265e-106">Continuous deployment is a great option for projects where multiple and frequent contributions are being integrated.</span></span>

<span data-ttu-id="0265e-107">toofind uit hoe tooconfigure continue implementatie handmatig van een cloud-opslagplaats niet vermeld in Azure Portal Hallo (zoals [GitLab](https://gitlab.com/)), Zie [instellen van continue implementatie met handmatige stappen](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span><span class="sxs-lookup"><span data-stu-id="0265e-107">toofind out how tooconfigure continuous deployment manually from a cloud repository not listed by hello Azure Portal (such as [GitLab](https://gitlab.com/)), see [Setting up continuous deployment using manual steps](https://github.com/projectkudu/kudu/wiki/Continuous-deployment#setting-up-continuous-deployment-using-manual-steps).</span></span>

## <span data-ttu-id="0265e-108"><a name="overview"></a>Continue implementatie inschakelen</span><span class="sxs-lookup"><span data-stu-id="0265e-108"><a name="overview"></a>Enable continuous deployment</span></span>
<span data-ttu-id="0265e-109">doorlopende implementatie tooenable,</span><span class="sxs-lookup"><span data-stu-id="0265e-109">tooenable continuous deployment,</span></span>

1. <span data-ttu-id="0265e-110">Publiceer de app inhoud toohello opslagplaats die wordt gebruikt voor continue implementatie.</span><span class="sxs-lookup"><span data-stu-id="0265e-110">Publish your app content toohello repository that will be used for continuous deployment.</span></span>  
    <span data-ttu-id="0265e-111">Zie voor meer informatie over het publiceren van uw project toothese services [maken van een opslagplaats (GitHub)], [maken van een opslagplaats (BitBucket)], en [aan de slag met VSTS].</span><span class="sxs-lookup"><span data-stu-id="0265e-111">For more information on publishing your project toothese services, see [Create a repo (GitHub)], [Create a repo (BitBucket)], and [Get started with VSTS].</span></span>
2. <span data-ttu-id="0265e-112">In de blade van uw app-menu in Hallo [Azure-portal], klikt u op **APP-implementatie > implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="0265e-112">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="0265e-113">Klik op **bron kiezen**, selecteer vervolgens de implementatiebron Hallo.</span><span class="sxs-lookup"><span data-stu-id="0265e-113">Click **Choose Source**, then select hello deployment source.</span></span>  
   
    ![](./media/app-service-continuous-deployment/cd_options.png)
   
   > [!NOTE]
   > <span data-ttu-id="0265e-114">een account VSTS voor App Service-implementatie tooconfigure raadpleegt u dit [zelfstudie](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span><span class="sxs-lookup"><span data-stu-id="0265e-114">tooconfigure a VSTS account for App Service deployment please see this [tutorial](https://github.com/projectkudu/kudu/wiki/Setting-up-a-VSTS-account-so-it-can-deploy-to-a-Web-App).</span></span>
   > 
   > 
3. <span data-ttu-id="0265e-115">Hallo autorisatie werkstroom voltooien.</span><span class="sxs-lookup"><span data-stu-id="0265e-115">Complete hello authorization workflow.</span></span>
4. <span data-ttu-id="0265e-116">In Hallo **implementatiebron** blade Hallo project kiezen en vertakken toodeploy uit.</span><span class="sxs-lookup"><span data-stu-id="0265e-116">In hello **Deployment source** blade, choose hello project and branch toodeploy from.</span></span> <span data-ttu-id="0265e-117">Wanneer u klaar bent, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0265e-117">When you're done, click **OK**.</span></span>
   
    ![](./media/app-service-continuous-deployment/github_option.png)
   
   > [!NOTE]
   > <span data-ttu-id="0265e-118">Wanneer u continue implementatie met GitHub of BitBucket inschakelt, worden openbare en particuliere projecten weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0265e-118">When enabling continuous deployment with GitHub or BitBucket, both public and private projects will be displayed.</span></span>
   > 
   > 
   
    <span data-ttu-id="0265e-119">App Service een koppeling met de geselecteerde opslagplaats Hallo maakt, worden opgehaald in het Hallo-bestanden van de opgegeven vertakking Hallo en onderhoudt een kloon van de opslagplaats voor uw App Service-app.</span><span class="sxs-lookup"><span data-stu-id="0265e-119">App Service creates an association with hello selected repository, pulls in hello files from hello specified branch, and maintains a clone of your repository for your App Service app.</span></span> <span data-ttu-id="0265e-120">Bij het configureren van VSTS continue implementatie van Azure-portal Hallo Hallo integratie Hallo App Service gebruikt [implementatie-engine Kudu](https://github.com/projectkudu/kudu/wiki), die al automatiseert het build- en taken met elke `git push`.</span><span class="sxs-lookup"><span data-stu-id="0265e-120">When you configure VSTS continuous deployment from hello Azure portal, hello integration uses hello App Service [Kudu deployment engine](https://github.com/projectkudu/kudu/wiki), which already automates build and deployment tasks with every `git push`.</span></span> <span data-ttu-id="0265e-121">U hoeft geen tooseparately doorlopende implementatie in VSTS ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0265e-121">You do not need tooseparately set up continuous deployment in VSTS.</span></span> <span data-ttu-id="0265e-122">Nadat dit proces is voltooid, hello **implementatieopties** blade app wordt weergegeven met een actieve implementatie waarmee implementatie is geslaagd.</span><span class="sxs-lookup"><span data-stu-id="0265e-122">After this process completes, hello **Deployment options** app blade will show an active deployment that indicates deployment has succeeded.</span></span>
5. <span data-ttu-id="0265e-123">tooverify hello app is geïmplementeerd, klikt u op Hallo **URL** Hallo boven aan de blade Hallo-app in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="0265e-123">tooverify hello app is successfully deployed, click hello **URL** at hello top of hello app's blade in hello Azure portal.</span></span>
6. <span data-ttu-id="0265e-124">tooverify continue implementatie plaatsvindt uit Hallo opslagplaats van uw keuze, een wijziging toohello opslagplaats pushen.</span><span class="sxs-lookup"><span data-stu-id="0265e-124">tooverify that continuous deployment is occurring from hello repository of your choice, push a change toohello repository.</span></span> <span data-ttu-id="0265e-125">Uw app moet tooreflect Hallo wijzigingen bijwerken kort nadat Hallo push toohello opslagplaats is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0265e-125">Your app should update tooreflect hello changes shortly after hello push toohello repository completes.</span></span> <span data-ttu-id="0265e-126">U kunt controleren of in de update in Hallo Hallo heeft getrokken **implementatieopties** blade van uw app.</span><span class="sxs-lookup"><span data-stu-id="0265e-126">You can verify that it has pulled in hello update in hello **Deployment options** blade of your app.</span></span>

## <span data-ttu-id="0265e-127"><a name="VSsolution"></a>Continue implementatie van een Visual Studio-oplossing</span><span class="sxs-lookup"><span data-stu-id="0265e-127"><a name="VSsolution"></a>Continuous deployment of a Visual Studio solution</span></span>
<span data-ttu-id="0265e-128">Een Visual Studio-oplossing tooAzure App Service pushen is net zo gemakkelijk een eenvoudige index.html bestand pushen.</span><span class="sxs-lookup"><span data-stu-id="0265e-128">Pushing a Visual Studio solution tooAzure App Service is just as easy as pushing a simple index.html file.</span></span> <span data-ttu-id="0265e-129">Hallo-App Service-implementatieproces stroomlijnt alle Hallo-informatie, zoals NuGet afhankelijkheden herstellen en het bouwen van de binaire bestanden Hallo van toepassingen.</span><span class="sxs-lookup"><span data-stu-id="0265e-129">hello App Service deployment process streamlines all hello details, including restoring NuGet dependencies and building hello application binaries.</span></span> <span data-ttu-id="0265e-130">U kunt Volg Hallo bron besturingselement aanbevolen procedures van het onderhouden van de code alleen in de Git-opslagplaats en kunt App Service-implementatie zorgt voor Hallo rest.</span><span class="sxs-lookup"><span data-stu-id="0265e-130">You can follow hello source control best practices of maintaining code only in your Git repository, and let App Service deployment take care of hello rest.</span></span>

<span data-ttu-id="0265e-131">Hallo stappen voor het pushen van uw Visual Studio-oplossing tooApp Service zijn Hallo hetzelfde als in Hallo [vorige sectie](#overview), mits u de oplossing en de opslagplaats als volgt configureren:</span><span class="sxs-lookup"><span data-stu-id="0265e-131">hello steps for pushing your Visual Studio solution tooApp Service are hello same as in hello [previous section](#overview), provided that you configure your solution and repository as follows:</span></span>

* <span data-ttu-id="0265e-132">Hallo Visual Studio bron besturingselement optie toogenerate gebruiken een `.gitignore` bestand zoals Hallo installatiekopie hieronder of Voeg handmatig een `.gitignore` bestand in de hoofdmap van uw opslagplaats met inhoud vergelijkbare toothis [.gitignore voorbeeld](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span><span class="sxs-lookup"><span data-stu-id="0265e-132">Use hello Visual Studio source control option toogenerate a `.gitignore` file such as hello image below or manually add a `.gitignore` file in your repository root with content similar toothis [.gitignore sample](https://github.com/github/gitignore/blob/master/VisualStudio.gitignore).</span></span>
  
  ![](./media/app-service-continuous-deployment/VS_source_control.png)
* <span data-ttu-id="0265e-133">Hallo hele oplossing directory structuur tooyour opslagplaats met Hallo .sln-bestand in de hoofdmap van de opslagplaats Hallo toevoegen.</span><span class="sxs-lookup"><span data-stu-id="0265e-133">Add hello entire solution's directory tree tooyour repository, with hello .sln file in hello repository root.</span></span>

<span data-ttu-id="0265e-134">Zodra u hebt uw opslagplaats zoals is beschreven instellen en uw app in Azure geconfigureerd voor continue publicatie van een van de online Git-opslagplaatsen hello, kunt u uw ASP.NET-toepassing lokaal in Visual Studio ontwikkelen en continu uw code gewoon door implementeren uw wijzigingen tooyour online Git-opslagplaats pushen.</span><span class="sxs-lookup"><span data-stu-id="0265e-134">Once you have set up your repository as described, and configured your app in Azure for continuous publishing from one of hello online Git repositories, you can develop your ASP.NET application locally in Visual Studio and continuously deploy your code simply by pushing your changes tooyour online Git repository.</span></span>

## <span data-ttu-id="0265e-135"><a name="disableCD"></a>Continue implementatie uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0265e-135"><a name="disableCD"></a>Disable continuous deployment</span></span>
<span data-ttu-id="0265e-136">doorlopende implementatie toodisable,</span><span class="sxs-lookup"><span data-stu-id="0265e-136">toodisable continuous deployment,</span></span>

1. <span data-ttu-id="0265e-137">In de blade van uw app-menu in Hallo [Azure-portal], klikt u op **APP-implementatie > implementatieopties**.</span><span class="sxs-lookup"><span data-stu-id="0265e-137">In your app's menu blade in hello [Azure portal], click **APP DEPLOYMENT > Deployment options**.</span></span> <span data-ttu-id="0265e-138">Klik vervolgens op **Disconnect** in Hallo **implementatieopties** blade.</span><span class="sxs-lookup"><span data-stu-id="0265e-138">Then click **Disconnect** in hello **Deployment options** blade.</span></span>
   
    ![](./media/app-service-continuous-deployment/cd_disconnect.png)
2. <span data-ttu-id="0265e-139">Na het beantwoorden van **Ja** toohello bevestigingsbericht die u kunt retourneren blade tooyour-app en klik op **APP-implementatie > implementatieopties** indien tooset van publicatie van een andere bron gewenst.</span><span class="sxs-lookup"><span data-stu-id="0265e-139">After answering **Yes** toohello confirmation message, you can return tooyour app's blade and click **APP DEPLOYMENT > Deployment options** if you would like tooset up publishing from another source.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="0265e-140">Aanvullende resources</span><span class="sxs-lookup"><span data-stu-id="0265e-140">Additional Resources</span></span>
* [<span data-ttu-id="0265e-141">Hoe tooinvestigate algemene problemen met een continue implementatie</span><span class="sxs-lookup"><span data-stu-id="0265e-141">How tooinvestigate common issues with continuous deployment</span></span>](https://github.com/projectkudu/kudu/wiki/Investigating-continuous-deployment)
* <span data-ttu-id="0265e-142">[Hoe toouse PowerShell voor Azure]</span><span class="sxs-lookup"><span data-stu-id="0265e-142">[How toouse PowerShell for Azure]</span></span>
* <span data-ttu-id="0265e-143">[Hoe toouse Azure opdrachtregelprogramma's Hallo voor Mac en Linux]</span><span class="sxs-lookup"><span data-stu-id="0265e-143">[How toouse hello Azure Command-Line Tools for Mac and Linux]</span></span>
* <span data-ttu-id="0265e-144">[Git-documentatie]</span><span class="sxs-lookup"><span data-stu-id="0265e-144">[Git documentation]</span></span>
* [<span data-ttu-id="0265e-145">Project Kudu</span><span class="sxs-lookup"><span data-stu-id="0265e-145">Project Kudu</span></span>](https://github.com/projectkudu/kudu/wiki)
* [<span data-ttu-id="0265e-146">Gebruik Azure tooautomatically genereren een CI/CD pijplijn toodeploy een ASP.NET-4-app</span><span class="sxs-lookup"><span data-stu-id="0265e-146">Use Azure tooautomatically generate a CI/CD pipeline toodeploy an ASP.NET 4 app</span></span>](https://www.visualstudio.com/docs/build/get-started/aspnet-4-ci-cd-azure-automatic)

> [!NOTE]
> <span data-ttu-id="0265e-147">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="0265e-147">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="0265e-148">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="0265e-148">No credit cards required; no commitments.</span></span>
> 
> 

[Azure App Service]: https://azure.microsoft.com/en-us/documentation/articles/app-service-changes-existing-services/
[Azure-portal]: https://portal.azure.com
[VSTS Portal]: https://www.visualstudio.com/en-us/products/visual-studio-team-services-vs.aspx
[Installing Git]: http://git-scm.com/book/en/Getting-Started-Installing-Git
[Hoe toouse PowerShell voor Azure]: /powershell/azureps-cmdlets-docs
[Hoe toouse Azure opdrachtregelprogramma's Hallo voor Mac en Linux]:../cli-install-nodejs.md
[Git-documentatie]: http://git-scm.com/documentation

[maken van een opslagplaats (GitHub)]: https://help.github.com/articles/create-a-repo
[maken van een opslagplaats (BitBucket)]: https://confluence.atlassian.com/display/BITBUCKET/Create+an+Account+and+a+Git+Repo
[aan de slag met VSTS]: https://www.visualstudio.com/docs/vsts-tfs-overview
