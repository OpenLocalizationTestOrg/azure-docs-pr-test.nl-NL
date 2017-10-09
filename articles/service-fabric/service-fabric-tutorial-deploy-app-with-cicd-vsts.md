---
title: aaaDeploy een Azure Service Fabric-toepassing met continue integratie (Team Services) | Microsoft Docs
description: Meer informatie over hoe tooset up continue integratie en implementatie voor een Service Fabric-toepassing met behulp van Visual Studio Team Services.  Een toepassing tooa Service Fabric-cluster in Azure implementeren.
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a><span data-ttu-id="2b97b-104">Implementeer een toepassing met CI/CD tooa Service Fabric-cluster</span><span class="sxs-lookup"><span data-stu-id="2b97b-104">Deploy an application with CI/CD tooa Service Fabric cluster</span></span>
<span data-ttu-id="2b97b-105">Deze zelfstudie maakt deel uit drie van een reeks en wordt beschreven hoe tooset up continue integratie en implementatie voor een Azure Service Fabric-toepassing met behulp van Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="2b97b-105">This tutorial is part three of a series and describes how tooset up continuous integration and deployment for an Azure Service Fabric application using Visual Studio Team Services.</span></span>  <span data-ttu-id="2b97b-106">Een bestaande Service Fabric-toepassing nodig is, de toepassing hello gemaakt in [een .NET-toepassing bouwen](service-fabric-tutorial-create-dotnet-app.md) wordt gebruikt als een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="2b97b-106">An existing Service Fabric application is needed, hello application created in [Build a .NET application](service-fabric-tutorial-create-dotnet-app.md) is used as an example.</span></span>

<span data-ttu-id="2b97b-107">In het onderdeel drie van Hallo-serie, leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="2b97b-107">In part three of hello series, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b97b-108">Source control tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b97b-108">Add source control tooyour project</span></span>
> * <span data-ttu-id="2b97b-109">Een build-definitie maken in een Team Services</span><span class="sxs-lookup"><span data-stu-id="2b97b-109">Create a build definition in Team Services</span></span>
> * <span data-ttu-id="2b97b-110">De definitie van een release in Team Services maken</span><span class="sxs-lookup"><span data-stu-id="2b97b-110">Create a release definition in Team Services</span></span>
> * <span data-ttu-id="2b97b-111">Automatisch implementeren en bijwerken van een toepassing</span><span class="sxs-lookup"><span data-stu-id="2b97b-111">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="2b97b-112">In deze zelfstudie reeks leert u hoe:</span><span class="sxs-lookup"><span data-stu-id="2b97b-112">In this tutorial series you learn how to:</span></span>
> [!div class="checklist"]
> * [<span data-ttu-id="2b97b-113">Een .NET-Service Fabric-toepassing bouwen</span><span class="sxs-lookup"><span data-stu-id="2b97b-113">Build a .NET Service Fabric application</span></span>](service-fabric-tutorial-create-dotnet-app.md)
> * [<span data-ttu-id="2b97b-114">Hallo toepassing tooa RAS-cluster implementeren</span><span class="sxs-lookup"><span data-stu-id="2b97b-114">Deploy hello application tooa remote cluster</span></span>](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * <span data-ttu-id="2b97b-115">CI/CD met behulp van Visual Studio Team Services configureren</span><span class="sxs-lookup"><span data-stu-id="2b97b-115">Configure CI/CD using Visual Studio Team Services</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b97b-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2b97b-116">Prerequisites</span></span>
<span data-ttu-id="2b97b-117">Voordat u deze zelfstudie begint:</span><span class="sxs-lookup"><span data-stu-id="2b97b-117">Before you begin this tutorial:</span></span>
- <span data-ttu-id="2b97b-118">Als u geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="2b97b-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)</span></span>
- <span data-ttu-id="2b97b-119">[Installeer Visual Studio 2017](https://www.visualstudio.com/) en installeer Hallo **ontwikkelen van Azure** en **ASP.NET en web ontwikkeling** werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="2b97b-119">[Install Visual Studio 2017](https://www.visualstudio.com/) and install hello **Azure development** and **ASP.NET and web development** workloads.</span></span>
- [<span data-ttu-id="2b97b-120">Hallo Service Fabric SDK installeren</span><span class="sxs-lookup"><span data-stu-id="2b97b-120">Install hello Service Fabric SDK</span></span>](service-fabric-get-started.md)
- <span data-ttu-id="2b97b-121">Maak een Service Fabric-toepassing, bijvoorbeeld door [deze zelfstudie](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b97b-121">Create a Service Fabric application, for example by [following this tutorial](service-fabric-tutorial-create-dotnet-app.md).</span></span> 
- <span data-ttu-id="2b97b-122">Maak een Windows-Service Fabric-cluster in Azure, bijvoorbeeld door [deze zelfstudie](service-fabric-tutorial-create-cluster-azure-ps.md)</span><span class="sxs-lookup"><span data-stu-id="2b97b-122">Create a Windows Service Fabric cluster on Azure, for example by [following this tutorial](service-fabric-tutorial-create-cluster-azure-ps.md)</span></span>
- <span data-ttu-id="2b97b-123">Maak een [Team Services-account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span><span class="sxs-lookup"><span data-stu-id="2b97b-123">Create a [Team Services account](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).</span></span>

## <a name="download-hello-voting-sample-application"></a><span data-ttu-id="2b97b-124">Hallo Voting voorbeeldtoepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="2b97b-124">Download hello Voting sample application</span></span>
<span data-ttu-id="2b97b-125">Als u geen Hallo Voting voorbeeldtoepassing heeft bouwen [deel uitmaken van een van deze zelfstudie reeks](service-fabric-tutorial-create-dotnet-app.md), u kunt dit downloaden.</span><span class="sxs-lookup"><span data-stu-id="2b97b-125">If you did not build hello Voting sample application in [part one of this tutorial series](service-fabric-tutorial-create-dotnet-app.md), you can download it.</span></span> <span data-ttu-id="2b97b-126">In een opdrachtvenster Hallo na de opdracht tooclone Hallo voorbeeld-app-opslagplaats tooyour lokale computer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2b97b-126">In a command window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a><span data-ttu-id="2b97b-127">Een publicatieprofiel voorbereiden</span><span class="sxs-lookup"><span data-stu-id="2b97b-127">Prepare a publish profile</span></span>
<span data-ttu-id="2b97b-128">Nu dat u hebt [gemaakt van een toepassing](service-fabric-tutorial-create-dotnet-app.md) en [geïmplementeerd Hallo toepassing tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), bent u klaar tooset van continue integratie.</span><span class="sxs-lookup"><span data-stu-id="2b97b-128">Now that you've [created an application](service-fabric-tutorial-create-dotnet-app.md) and have [deployed hello application tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), you're ready tooset up continuous integration.</span></span>  <span data-ttu-id="2b97b-129">Bereid eerst een publicatieprofiel in uw toepassing voor gebruik door Hallo-implementatieproces die wordt uitgevoerd binnen Team Services.</span><span class="sxs-lookup"><span data-stu-id="2b97b-129">First, prepare a publish profile within your application for use by hello deployment process that executes within Team Services.</span></span>  <span data-ttu-id="2b97b-130">Hallo publicatieprofiel moet geconfigureerde tootarget Hallo cluster dat u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b97b-130">hello publish profile should be configured tootarget hello cluster that you've previously created.</span></span>  <span data-ttu-id="2b97b-131">Visual Studio starten en opent u een bestaand project van de Service Fabric-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2b97b-131">Start Visual Studio and open an existing Service Fabric application project.</span></span>  <span data-ttu-id="2b97b-132">In **Solution Explorer**, met de rechtermuisknop op het Hallo-toepassing en selecteer **publiceren...** .</span><span class="sxs-lookup"><span data-stu-id="2b97b-132">In **Solution Explorer**, right-click hello application and select **Publish...**.</span></span>

<span data-ttu-id="2b97b-133">Een profiel van de doelcomputer in uw toepassing project toouse voor uw werkstroom continue integratie kiezen, bijvoorbeeld Cloud.</span><span class="sxs-lookup"><span data-stu-id="2b97b-133">Choose a target profile within your application project toouse for your continuous integration workflow, for example Cloud.</span></span>  <span data-ttu-id="2b97b-134">Geef verbindingseindpunt Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-134">Specify hello cluster connection endpoint.</span></span>  <span data-ttu-id="2b97b-135">Controleer Hallo **Upgrade Hallo toepassing** selectievakje in zodat uw toepassing upgrades voor elke implementatie in een Team Services.</span><span class="sxs-lookup"><span data-stu-id="2b97b-135">Check hello **Upgrade hello Application** checkbox so that your application upgrades for each deployment in Team Services.</span></span>  <span data-ttu-id="2b97b-136">Klik op Hallo **opslaan** hyperlink toosave Hallo instellingen toohello publicatieprofiel en klik vervolgens op **annuleren** tooclose Hallo dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-136">Click hello **Save** hyperlink toosave hello settings toohello publish profile and then click **Cancel** tooclose hello dialog box.</span></span>  

![Push-profiel][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a><span data-ttu-id="2b97b-138">Delen van uw Visual Studio-oplossing tooa nieuw Team Services Git-opslagplaats</span><span class="sxs-lookup"><span data-stu-id="2b97b-138">Share your Visual Studio solution tooa new Team Services Git repo</span></span>
<span data-ttu-id="2b97b-139">De bronbestanden van uw toepassing tooa teamproject in Team Services zodat u kunt genereren builds delen.</span><span class="sxs-lookup"><span data-stu-id="2b97b-139">Share your application source files tooa team project in Team Services so you can generate builds.</span></span>  

<span data-ttu-id="2b97b-140">Een nieuwe lokale Git-opslagplaats voor uw project maken door te selecteren **tooSource besturingselement toevoegen** -> **Git** op de statusbalk Hallo in Hallo rechterbenedenhoek van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b97b-140">Create a new local Git repo for your project by selecting **Add tooSource Control** -> **Git** on hello status bar in hello lower right-hand corner of Visual Studio.</span></span> 

<span data-ttu-id="2b97b-141">In Hallo **Push** weergeven in **Team Explorer**, selecteer Hallo **Git-opslagplaats publiceren** knop onder **tooVisual Studio Team Services Push**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-141">In hello **Push** view in **Team Explorer**, select hello **Publish Git Repo** button under **Push tooVisual Studio Team Services**.</span></span>

![Push Git-opslagplaats][push-git-repo]

<span data-ttu-id="2b97b-143">Controleer of uw e-mailadres in en selecteer uw account Hallo **Team Services domein** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="2b97b-143">Verify your email and select your account in hello **Team Services Domain** drop-down.</span></span> <span data-ttu-id="2b97b-144">Voer de naam van uw opslagplaats en selecteer **publiceren opslagplaats**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-144">Enter your repository name and select **Publish repository**.</span></span>

![Push Git-opslagplaats][publish-code]

<span data-ttu-id="2b97b-146">Hallo opslagplaats publiceren, maakt een nieuw teamproject in uw account met dezelfde naam als lokale opslagplaats Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="2b97b-146">Publishing hello repo creates a new team project in your account with hello same name as hello local repo.</span></span> <span data-ttu-id="2b97b-147">toocreate Hallo-opslagplaats in een bestaande teamproject, klikt u op **Geavanceerd** volgende te**opslagplaats** naam en selecteer een teamproject.</span><span class="sxs-lookup"><span data-stu-id="2b97b-147">toocreate hello repo in an existing team project, click **Advanced** next too**Repository** name and select a team project.</span></span> <span data-ttu-id="2b97b-148">U kunt uw code op Hallo web weergeven door **zien op Hallo web**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-148">You can view your code on hello web by selecting **See it on hello web**.</span></span>

## <a name="configure-continuous-delivery-with-vsts"></a><span data-ttu-id="2b97b-149">Continue levering met VSTS configureren</span><span class="sxs-lookup"><span data-stu-id="2b97b-149">Configure Continuous Delivery with VSTS</span></span>
<span data-ttu-id="2b97b-150">De definitie van een Team Services build beschrijft een werkstroom die bestaat uit een reeks build stappen die sequentieel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2b97b-150">A Team Services build definition describes a workflow that is composed of a set of build steps that are executed sequentially.</span></span> <span data-ttu-id="2b97b-151">Een build-definitie maken die die een Service Fabric-toepassingspakket en andere artefacten, toodeploy tooa Service Fabric-cluster produceert.</span><span class="sxs-lookup"><span data-stu-id="2b97b-151">Create a build definition that that produces a Service Fabric application package, and other artifacts, toodeploy tooa Service Fabric cluster.</span></span> <span data-ttu-id="2b97b-152">Meer informatie over [Team Services bouwen definities](https://www.visualstudio.com/docs/build/define/create).</span><span class="sxs-lookup"><span data-stu-id="2b97b-152">Learn more about [Team Services build definitions](https://www.visualstudio.com/docs/build/define/create).</span></span> 

<span data-ttu-id="2b97b-153">De definitie van een Team Services release beschrijft een werkstroom die een toepassing pakket tooa cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="2b97b-153">A Team Services release definition describes a workflow that deploys an application package tooa cluster.</span></span> <span data-ttu-id="2b97b-154">Wanneer samen worden gebruikt, Hallo definitie bouwen en release definitie uitvoeren Hallo van de volledige werkstroom beginnen met bron bestanden tooending met een actieve toepassing in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-154">When used together, hello build definition and release definition execute hello entire workflow starting with source files tooending with a running application in your cluster.</span></span> <span data-ttu-id="2b97b-155">Meer informatie over Services Team [definities release](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span><span class="sxs-lookup"><span data-stu-id="2b97b-155">Learn more about Team Services [release definitions](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition).</span></span>

### <a name="create-a-build-definition"></a><span data-ttu-id="2b97b-156">Een build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2b97b-156">Create a build definition</span></span>
<span data-ttu-id="2b97b-157">Open een webbrowser en navigeer tooyour nieuw teamproject op: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting.</span><span class="sxs-lookup"><span data-stu-id="2b97b-157">Open a web browser and navigate tooyour new team project at: https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting .</span></span> 

<span data-ttu-id="2b97b-158">Selecteer Hallo **bouwen & Release** tabblad vervolgens **Builds**, klikt u vervolgens **+ nieuwe definitie**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-158">Select hello **Build & Release** tab, then **Builds**, then **+ New definition**.</span></span>  <span data-ttu-id="2b97b-159">In **Selecteer een sjabloon**, selecteer Hallo **Azure Service Fabric-toepassing** sjabloon en klikt u op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-159">In **Select a template**, select hello **Azure Service Fabric Application** template and click **Apply**.</span></span> 

![Kies build-sjabloon][select-build-template] 

<span data-ttu-id="2b97b-161">Hallo stemmen toepassing bevat een project .NET Core, dus een taak die wordt hersteld Hallo afhankelijkheden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="2b97b-161">hello voting application contains a .NET Core project, so add a task that restores hello dependencies.</span></span> <span data-ttu-id="2b97b-162">In Hallo **taken** weergave, selecteer **+ taak toevoegen** in Hallo linksonder.</span><span class="sxs-lookup"><span data-stu-id="2b97b-162">In hello **Tasks** view, select **+ Add Task** in hello bottom left.</span></span> <span data-ttu-id="2b97b-163">Zoeken op 'Opdrachtregel' toofind hello opdrachtregeltaak en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-163">Search on "Command Line" toofind hello command-line task, then click **Add**.</span></span> 

![Taak toevoegen][add-task] 

<span data-ttu-id="2b97b-165">Voer in de nieuwe taak Hallo 'Dotnet.exe uitvoeren' in **weergavenaam**, 'dotnet.exe' in **hulpprogramma**, en "herstellen" in **argumenten**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-165">In hello new task, enter "Run dotnet.exe" in **Display name**, "dotnet.exe" in **Tool**, and "restore" in **Arguments**.</span></span> 

![Nieuwe taak][new-task] 

<span data-ttu-id="2b97b-167">In Hallo **Triggers** weergeven, klikt u op Hallo **inschakelen van deze trigger** overschakelen onder **continue integratie**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-167">In hello **Triggers** view, click hello **Enable this trigger** switch under **Continuous Integration**.</span></span> 

<span data-ttu-id="2b97b-168">Selecteer **opslaan en wachtrij** en voer 'VS2017 gehost' als Hallo **Agent wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-168">Select **Save & queue** and enter "Hosted VS2017" as hello **Agent queue**.</span></span> <span data-ttu-id="2b97b-169">Selecteer **wachtrij** toomanually start een build.</span><span class="sxs-lookup"><span data-stu-id="2b97b-169">Select **Queue** toomanually start a build.</span></span>  <span data-ttu-id="2b97b-170">Voortbouwt ook triggers op push of inchecken.</span><span class="sxs-lookup"><span data-stu-id="2b97b-170">Builds also triggers upon push or check-in.</span></span>

<span data-ttu-id="2b97b-171">toocheck uw voortgang build, switch toohello **Builds** tabblad.  Zodra u hebt gecontroleerd dat Hallo build met succes wordt uitgevoerd, definieert u de definitie van een versie die uw toepassing tooa cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="2b97b-171">toocheck your build progress, switch toohello **Builds** tab.  Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span> 

### <a name="create-a-release-definition"></a><span data-ttu-id="2b97b-172">Een release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2b97b-172">Create a release definition</span></span>  

<span data-ttu-id="2b97b-173">Selecteer Hallo **bouwen & Release** tabblad vervolgens **Releases**, klikt u vervolgens **+ nieuwe definitie**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-173">Select hello **Build & Release** tab, then **Releases**, then **+ New definition**.</span></span>  <span data-ttu-id="2b97b-174">In **maken release definitie**, selecteer Hallo **Azure Service Fabric-implementatie** sjabloon van Hallo lijst en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-174">In **Create release definition**, select hello **Azure Service Fabric Deployment** template from hello list and click **Next**.</span></span>  <span data-ttu-id="2b97b-175">Selecteer Hallo **bouwen** bron, controleert u Hallo **continue implementatie** vak en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-175">Select hello **Build** source, check hello **Continuous deployment** box, and click **Create**.</span></span> 

<span data-ttu-id="2b97b-176">In Hallo **omgevingen** weergeven, klikt u op **toevoegen** toohello rechts van **Cluster verbinding**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-176">In hello **Environments** view, click **Add** toohello right of **Cluster Connection**.</span></span>  <span data-ttu-id="2b97b-177">Geef de verbindingsnaam van een van 'mysftestcluster', een clustereindpunt van 'tcp://mysftestcluster.westus.cloudapp.azure.com:19000' en hello Azure Active Directory of referenties van het computercertificaat voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-177">Specify a connection name of "mysftestcluster", a cluster endpoint of "tcp://mysftestcluster.westus.cloudapp.azure.com:19000", and hello Azure Active Directory or certificate credentials for hello cluster.</span></span> <span data-ttu-id="2b97b-178">Voor Azure Active Directory-referenties, definiëren Hallo referenties gewenste toouse tooconnect toohello cluster in Hallo **gebruikersnaam** en **wachtwoord** velden.</span><span class="sxs-lookup"><span data-stu-id="2b97b-178">For Azure Active Directory credentials, define hello credentials you want toouse tooconnect toohello cluster in hello **Username** and **Password** fields.</span></span> <span data-ttu-id="2b97b-179">Voor verificatie op basis van certificaten definiëren Hallo Base64-codering Hallo certificaatbestand in Hallo **clientcertificaat** veld.</span><span class="sxs-lookup"><span data-stu-id="2b97b-179">For certificate-based authentication, define hello Base64 encoding of hello client certificate file in hello **Client Certificate** field.</span></span>  <span data-ttu-id="2b97b-180">Hallo help pop-up bekijken op het veld voor informatie over het tooget die waarde.</span><span class="sxs-lookup"><span data-stu-id="2b97b-180">See hello help pop-up on that field for info on how tooget that value.</span></span>  <span data-ttu-id="2b97b-181">Als uw certificaat beveiligd met een wachtwoord is, hello wachtwoord definiëren in Hallo **wachtwoord** veld.</span><span class="sxs-lookup"><span data-stu-id="2b97b-181">If your certificate is password-protected, define hello password in hello **Password** field.</span></span>  <span data-ttu-id="2b97b-182">Klik op **opslaan** toosave Hallo release definitie.</span><span class="sxs-lookup"><span data-stu-id="2b97b-182">Click **Save** toosave hello release definition.</span></span>

![Cluster-verbinding toevoegen][add-cluster-connection] 

<span data-ttu-id="2b97b-184">Klik op **uitvoeren op de agent**, selecteer daarna **VS2017 gehost** voor **implementatie wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="2b97b-184">Click **Run on agent**, then select **Hosted VS2017** for **Deployment queue**.</span></span> <span data-ttu-id="2b97b-185">Klik op **opslaan** toosave Hallo release definitie.</span><span class="sxs-lookup"><span data-stu-id="2b97b-185">Click **Save** toosave hello release definition.</span></span>

![Voer op de agent][run-on-agent]

<span data-ttu-id="2b97b-187">Selecteer **+ Release** -> **maken Release** -> **maken** toomanually een release gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2b97b-187">Select **+Release** -> **Create Release** -> **Create** toomanually create a release.</span></span>  <span data-ttu-id="2b97b-188">Controleer of Hallo-implementatie is voltooid en Hallo toepassing wordt uitgevoerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-188">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="2b97b-189">Open een webbrowser en navigeer te[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="2b97b-189">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="2b97b-190">Houd er rekening mee Hallo toepassingsversie, in dit voorbeeld is '1.0.0.20170616.3'.</span><span class="sxs-lookup"><span data-stu-id="2b97b-190">Note hello application version, in this example it is "1.0.0.20170616.3".</span></span> 

## <a name="commit-and-push-changes-trigger-a-release"></a><span data-ttu-id="2b97b-191">Doorvoeren en wijzigingen forceren, een release activeren</span><span class="sxs-lookup"><span data-stu-id="2b97b-191">Commit and push changes, trigger a release</span></span>
<span data-ttu-id="2b97b-192">tooverify die continue integratie pijplijn Hallo werkt door te controleren in een aantal codewijzigingen tooTeam Services.</span><span class="sxs-lookup"><span data-stu-id="2b97b-192">tooverify that hello continuous integration pipeline is functioning by checking in some code changes tooTeam Services.</span></span>    

<span data-ttu-id="2b97b-193">Als u uw code schrijft, worden uw wijzigingen automatisch bijgehouden door Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b97b-193">As you write your code, your changes are automatically tracked by Visual Studio.</span></span> <span data-ttu-id="2b97b-194">Het doorvoeren van wijzigingen tooyour lokale Git-opslagplaats door Hallo in behandeling zijnde wijzigingen pictogram (selecteren</span><span class="sxs-lookup"><span data-stu-id="2b97b-194">Commit changes tooyour local Git repository by selecting hello pending changes icon (</span></span>![In behandeling][pending]<span data-ttu-id="2b97b-196">) van de statusbalk Hallo in Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="2b97b-196">) from hello status bar in hello bottom right.</span></span>

<span data-ttu-id="2b97b-197">Op Hallo **wijzigingen** weergeven in Verkenner-Team, een bericht met een beschrijving van de update toevoegen en uw wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="2b97b-197">On hello **Changes** view in Team Explorer, add a message describing your update and commit your changes.</span></span>

![Alle doorvoeren][changes]

<span data-ttu-id="2b97b-199">Selecteer Hallo niet-gepubliceerde wijzigingen statuspictogram balk (![niet-gepubliceerde wijzigingen][unpublished-changes]) of Hallo Sync weergave in de Explorer-Team.</span><span class="sxs-lookup"><span data-stu-id="2b97b-199">Select hello unpublished changes status bar icon (![Unpublished changes][unpublished-changes]) or hello Sync view in Team Explorer.</span></span> <span data-ttu-id="2b97b-200">Selecteer **Push** tooupdate uw code in Services/TFS Team.</span><span class="sxs-lookup"><span data-stu-id="2b97b-200">Select **Push** tooupdate your code in Team Services/TFS.</span></span>

![Wijzigingen][push]

<span data-ttu-id="2b97b-202">Hallo wijzigingen tooTeam pushen Services automatisch triggers een build.</span><span class="sxs-lookup"><span data-stu-id="2b97b-202">Pushing hello changes tooTeam Services automatically triggers a build.</span></span>  <span data-ttu-id="2b97b-203">Wanneer Hallo build definitie is voltooid, wordt een versie wordt automatisch gemaakt en begint met het upgraden van de toepassing hello op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-203">When hello build definition successfully completes, a release is automatically created and starts upgrading hello application on hello cluster.</span></span>

<span data-ttu-id="2b97b-204">toocheck uw voortgang build, switch toohello **Builds** tabblad **Team Explorer** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2b97b-204">toocheck your build progress, switch toohello **Builds** tab in **Team Explorer** in Visual Studio.</span></span>  <span data-ttu-id="2b97b-205">Zodra u hebt gecontroleerd dat Hallo build met succes wordt uitgevoerd, definieert u de definitie van een versie die uw toepassing tooa cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="2b97b-205">Once you verify that hello build executes successfully, define a release definition that deploys your application tooa cluster.</span></span>

<span data-ttu-id="2b97b-206">Controleer of Hallo-implementatie is voltooid en Hallo toepassing wordt uitgevoerd in Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2b97b-206">Verify that hello deployment succeeded and hello application is running in hello cluster.</span></span>  <span data-ttu-id="2b97b-207">Open een webbrowser en navigeer te[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span><span class="sxs-lookup"><span data-stu-id="2b97b-207">Open a web browser and navigate too[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).</span></span>  <span data-ttu-id="2b97b-208">Houd er rekening mee Hallo toepassingsversie, in dit voorbeeld is '1.0.0.20170815.3'.</span><span class="sxs-lookup"><span data-stu-id="2b97b-208">Note hello application version, in this example it is "1.0.0.20170815.3".</span></span>

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a><span data-ttu-id="2b97b-210">Hallo toepassing bijwerken</span><span class="sxs-lookup"><span data-stu-id="2b97b-210">Update hello application</span></span>
<span data-ttu-id="2b97b-211">Codewijzigingen aanbrengen in de toepassing hello.</span><span class="sxs-lookup"><span data-stu-id="2b97b-211">Make code changes in hello application.</span></span>  <span data-ttu-id="2b97b-212">Opslaan en wijzigingen hello, Hallo vorige stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="2b97b-212">Save and commit hello changes, following hello previous steps.</span></span>

<span data-ttu-id="2b97b-213">Zodra het Hallo-upgrade van Hallo toepassing wordt gestart, kunt u de voortgang van Hallo upgrade in Service Fabric Explorer bekijken:</span><span class="sxs-lookup"><span data-stu-id="2b97b-213">Once hello upgrade of hello application begins, you can watch hello upgrade progress in Service Fabric Explorer:</span></span>

![Service Fabric Explorer][sfx2]

<span data-ttu-id="2b97b-215">upgrade van de toepassing Hello kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="2b97b-215">hello application upgrade may take several minutes.</span></span> <span data-ttu-id="2b97b-216">Wanneer het Hallo-upgrade is voltooid, wordt Hallo toepassing hello volgende versie worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2b97b-216">When hello upgrade is complete, hello application will be running hello next version.</span></span>  <span data-ttu-id="2b97b-217">In dit voorbeeld '1.0.0.20170815.4'.</span><span class="sxs-lookup"><span data-stu-id="2b97b-217">In this example "1.0.0.20170815.4".</span></span>

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a><span data-ttu-id="2b97b-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2b97b-219">Next steps</span></span>
<span data-ttu-id="2b97b-220">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="2b97b-220">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2b97b-221">Source control tooyour project toevoegen</span><span class="sxs-lookup"><span data-stu-id="2b97b-221">Add source control tooyour project</span></span>
> * <span data-ttu-id="2b97b-222">Een build-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2b97b-222">Create a build definition</span></span>
> * <span data-ttu-id="2b97b-223">Een release-definitie maken</span><span class="sxs-lookup"><span data-stu-id="2b97b-223">Create a release definition</span></span>
> * <span data-ttu-id="2b97b-224">Automatisch implementeren en bijwerken van een toepassing</span><span class="sxs-lookup"><span data-stu-id="2b97b-224">Automatically deploy and upgrade an application</span></span>

<span data-ttu-id="2b97b-225">Nu dat u hebt een toepassing is geïmplementeerd en geconfigureerd continue integratie, voer een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="2b97b-225">Now that you have deployed an application and configured continuous integration, try hello following:</span></span>
- [<span data-ttu-id="2b97b-226">Een app bijwerken</span><span class="sxs-lookup"><span data-stu-id="2b97b-226">Upgrade an app</span></span>](service-fabric-application-upgrade.md)
- [<span data-ttu-id="2b97b-227">Een app testen</span><span class="sxs-lookup"><span data-stu-id="2b97b-227">Test an app</span></span>](service-fabric-testability-overview.md) 
- [<span data-ttu-id="2b97b-228">Controle en diagnose</span><span class="sxs-lookup"><span data-stu-id="2b97b-228">Monitor and diagnose</span></span>](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png