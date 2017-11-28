---
title: aaaContinuous levering met Git en Visual Studio Team Services in Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw Visual Studio Team Services team projecten toouse Git tooautomatically bouwen en implementeren van de functie van de toohello Web-App in Azure App Service- of cloud-services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="f2c26-103">Continue levering tooAzure met behulp van Visual Studio Team Services en Git</span><span class="sxs-lookup"><span data-stu-id="f2c26-103">Continuous delivery tooAzure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="f2c26-104">U kunt Visual Studio Team Services team projecten toohost een Git-opslagplaats gebruiken voor de broncode en automatisch bouwen en tooAzure web-apps implementeren of cloudservices wanneer u een commit toohello opslagplaats pushen.</span><span class="sxs-lookup"><span data-stu-id="f2c26-104">You can use Visual Studio Team Services team projects toohost a Git repository for your source code, and automatically build and deploy tooAzure web apps or cloud services whenever you push a commit toohello repository.</span></span>

<span data-ttu-id="f2c26-105">U moet Visual Studio 2013 en hello Azure SDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-105">You'll need Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="f2c26-106">Als u nog geen Visual Studio 2013 hebt, downloadt u dit door te kiezen Hallo **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeren Azure SDK Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="f2c26-106">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="f2c26-107">U moet een toocomplete Visual Studio Team Services-account van deze zelfstudie: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="f2c26-107">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="f2c26-108">tooset van een cloud service tooautomatically bouwen en tooAzure implementeren met behulp van Visual Studio Team Services, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="f2c26-108">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="f2c26-109">1: een Git-opslagplaats maken</span><span class="sxs-lookup"><span data-stu-id="f2c26-109">1: Create a Git repository</span></span>
1. <span data-ttu-id="f2c26-110">Als u nog een Visual Studio Team Services-account hebt, kunt u een [hier](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="f2c26-110">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="f2c26-111">Wanneer u uw teamproject maakt, kiest u Git als uw bronbeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="f2c26-111">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="f2c26-112">Ga als volgt Hallo instructies tooconnect Visual Studio tooyour teamproject.</span><span class="sxs-lookup"><span data-stu-id="f2c26-112">Follow hello instructions tooconnect Visual Studio tooyour team project.</span></span>
2. <span data-ttu-id="f2c26-113">In **Team Explorer**, kies Hallo **deze opslagplaats klonen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-113">In **Team Explorer**, choose hello **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="f2c26-114">Locatie van de lokale kopie Hallo Hallo opgeven en kies vervolgens Hallo **kloon** knop.</span><span class="sxs-lookup"><span data-stu-id="f2c26-114">Specify hello location of hello local copy and then choose hello **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a><span data-ttu-id="f2c26-115">2: een project maken en deze opslagplaats toohello doorvoeren</span><span class="sxs-lookup"><span data-stu-id="f2c26-115">2: Create a project and commit it toohello repository</span></span>
1. <span data-ttu-id="f2c26-116">In **Team Explorer**, in Hallo **oplossingen** sectie, kiest u Hallo **nieuw** toocreate een nieuw project in de lokale opslagplaats Hallo koppelen.</span><span class="sxs-lookup"><span data-stu-id="f2c26-116">In **Team Explorer**, in hello **Solutions** section, choose hello **New** link toocreate a new project in hello local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="f2c26-117">U kunt een web-app implementeren of een service in de cloud (Azure-toepassing) door de volgende Hallo stappen in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="f2c26-117">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span> <span data-ttu-id="f2c26-118">Maak een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project.</span><span class="sxs-lookup"><span data-stu-id="f2c26-118">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="f2c26-119">Controleer of dat Hallo project doelen Hallo .NET Framework 4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f2c26-119">Make sure that hello project targets hello .NET Framework 4 or later.</span></span> <span data-ttu-id="f2c26-120">Als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen.</span><span class="sxs-lookup"><span data-stu-id="f2c26-120">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="f2c26-121">Als u een web-app toocreate wilt, kunt u Hallo **ASP.NET-webtoepassing** sjabloon project en kies vervolgens **MVC**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-121">If you want toocreate a web app, choose hello **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="f2c26-122">Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f2c26-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="f2c26-123">Open Hallo snelmenu voor Hallo oplossing en kies **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-123">Open hello shortcut menu for hello solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="f2c26-124">Als dit Hallo eerst die u Git in Visual Studio Team Services hebt gebruikt, moet u tooprovide sommige tooidentify informatie zelf in Git.</span><span class="sxs-lookup"><span data-stu-id="f2c26-124">If this is hello first time you've used Git in Visual Studio Team Services, you'll need tooprovide some information tooidentify yourself in Git.</span></span> <span data-ttu-id="f2c26-125">In Hallo **wijzigingen in behandeling** gebied van **Team Explorer**, Voer uw gebruikersnaam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="f2c26-125">In hello **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="f2c26-126">Voer een opmerking voor Hallo doorvoeren en kies vervolgens Hallo **doorvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="f2c26-126">Enter a comment for hello commit and then choose hello **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="f2c26-127">Houd er rekening mee Hallo opties tooinclude of specifieke wijzigingen uitsluiten wanneer u incheckt.</span><span class="sxs-lookup"><span data-stu-id="f2c26-127">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="f2c26-128">Als Hallo wijzigingen u wilt worden uitgesloten, kiest u **omvatten alle**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-128">If hello changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="f2c26-129">U hebt nu doorgevoerd Hallo in de lokale kopie van het Hallo-opslagplaats wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="f2c26-129">You've now committed hello changes in your local copy of hello repository.</span></span> <span data-ttu-id="f2c26-130">Vervolgens deze wijzigingen met Hallo-server te synchroniseren door te kiezen Hallo **Sync** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-130">Next, sync those changes with hello server by choosing hello **Sync** link.</span></span>

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="f2c26-131">3: verbinding maken met de Hallo project tooAzure</span><span class="sxs-lookup"><span data-stu-id="f2c26-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="f2c26-132">Nu dat u een Git-opslagplaats in Visual Studio Team Services met sommige broncode erin hebt, bent u klaar tooconnect uw tooAzure git-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f2c26-132">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready tooconnect your git repository tooAzure.</span></span>  <span data-ttu-id="f2c26-133">In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door te kiezen Hallo + pictogram op Hallo linksonder en kiezen **Cloudservice** of **Web-App**en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello + icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="f2c26-134">Kies voor cloudservices, Hallo **publiceren met Visual Studio Team Services instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-134">For cloud services, choose hello **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="f2c26-135">Kies voor web-apps, Hallo **implementatie vanuit resourcebeheer instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-135">For web apps, choose hello **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="f2c26-136">In de wizard Hallo typenaam Hallo van uw Visual Studio Team Services-account in Hallo tekstvak en kies Hallo **autoriseren nu** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-136">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and choose hello **Authorize Now** link.</span></span> <span data-ttu-id="f2c26-137">U wordt mogelijk gevraagd toosign in.</span><span class="sxs-lookup"><span data-stu-id="f2c26-137">You might be asked toosign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="f2c26-138">In Hallo **verbindingsaanvraag** pop-upvenster kiezen **accepteren** tooauthorize Azure tooconfigure uw team in Visual Studio Team Services project.</span><span class="sxs-lookup"><span data-stu-id="f2c26-138">In hello **Connection Request** pop-up dialog, choose **Accept** tooauthorize Azure tooconfigure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="f2c26-139">Nadat de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met uw teamprojecten Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f2c26-139">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="f2c26-140">Selecteer de naam Hallo van teamproject dat u hebt gemaakt in de vorige stappen Hallo en kies van de wizard Hallo vinkje knop.</span><span class="sxs-lookup"><span data-stu-id="f2c26-140">Select hello name of team project that you created in hello previous steps, and choose hello wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="f2c26-141">Hallo volgende keer dat u Visual Studio Team Services van een commit tooyour opslagplaats pushen bouwt en implementeren van uw project tooAzure.</span><span class="sxs-lookup"><span data-stu-id="f2c26-141">hello next time you push a commit tooyour repository, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="f2c26-142">4: de tabel opnieuw activeren en implementeren van uw project</span><span class="sxs-lookup"><span data-stu-id="f2c26-142">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="f2c26-143">In Visual Studio, opent u een bestand en deze te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="f2c26-143">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="f2c26-144">Wijzig bijvoorbeeld Hallo bestand `_Layout.cshtml` onder Hallo weergaven\\gedeelde map in een MVC-Webrol.</span><span class="sxs-lookup"><span data-stu-id="f2c26-144">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="f2c26-145">Hallo voettekst voor Hallo site bewerken en sla Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="f2c26-145">Edit hello footer text for hello site and save hello file.</span></span>
   
    ![][18]
3. <span data-ttu-id="f2c26-146">In **Solution Explorer**, open de Hallo snelmenu voor hello oplossing knooppunt, projectknooppunt of Hallo bestand dat u gewijzigd en kies vervolgens **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-146">In **Solution Explorer**, open hello shortcut menu for hello solution node, project node, or hello file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="f2c26-147">Typ in een opmerking en kies **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-147">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="f2c26-148">Kies Hallo **Sync** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-148">Choose hello **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="f2c26-149">Kies Hallo **Push** koppelen toopush uw opslagplaats doorvoeren toohello in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="f2c26-149">Choose hello **Push** link toopush your commit toohello repository in Visual Studio Team Services.</span></span> <span data-ttu-id="f2c26-150">(U kunt ook Hallo **Sync** knop toocopy uw doorvoeracties toohello-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f2c26-150">(You can also use hello **Sync** button toocopy your commits toohello repository.</span></span> <span data-ttu-id="f2c26-151">Hallo verschil is dat **Sync** ook worden de meest recente wijzigingen in de opslagplaats voor Hallo Hallo.)</span><span class="sxs-lookup"><span data-stu-id="f2c26-151">hello difference is that **Sync** also pulls hello latest changes from hello repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="f2c26-152">Kies Hallo **thuis** knop tooreturn toohello **Team Explorer** startpagina.</span><span class="sxs-lookup"><span data-stu-id="f2c26-152">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="f2c26-153">Kies **Builds** tooview hello-bouwt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-153">Choose **Builds** tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="f2c26-154">**In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="f2c26-155">tooview een gedetailleerd logboek terwijl Hallo maakt de voortgang van Dubbelklik op Hallo van Hallo build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-155">tooview a detailed log as hello build progresses, double-click hello name of hello build in progress.</span></span>
10. <span data-ttu-id="f2c26-156">Hallo build is uitgevoerd, bekijk Hallo build definitie die is gemaakt toen u Hallo wizard toolink tooAzure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f2c26-156">While hello build is in-progress, take a look at hello build definition that was created when you used hello wizard toolink tooAzure.</span></span>  <span data-ttu-id="f2c26-157">Hallo snelmenu voor Hallo build definitie openen en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-157">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="f2c26-158">In Hallo **Trigger** tabblad ziet u dat Hallo build definitie toobuild is ingesteld op elke inchecken standaard.</span><span class="sxs-lookup"><span data-stu-id="f2c26-158">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in, by default.</span></span> <span data-ttu-id="f2c26-159">(Voor een cloudservice Visual Studio Team Services maakt en implementeert Hallo hoofdvertakking toohello automatisch staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2c26-159">(For a cloud service, Visual Studio Team Services builds and deploys hello master branch toohello staging environment automatically.</span></span> <span data-ttu-id="f2c26-160">U hebt nog toodo een handmatige stap toodeploy toohello live site.</span><span class="sxs-lookup"><span data-stu-id="f2c26-160">You still have toodo a manual step toodeploy toohello live site.</span></span> <span data-ttu-id="f2c26-161">Voor een web-app dat geen staging-omgeving, wordt het Hallo hoofdvertakking direct toohello live site geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-161">For a web app that doesn't have staging environment, it deploys hello master branch directly toohello live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="f2c26-162">In Hallo **proces** tabblad ziet u de implementatieomgeving Hallo toohello naam van uw cloud-service of web-app is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f2c26-162">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="f2c26-163">Geef waarden voor Hallo eigenschappen als u wilt dat andere waarden dan Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="f2c26-163">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="f2c26-164">Hallo-eigenschappen voor Azure publicatie worden in Hallo **implementatie** sectie en kunt u wellicht ook tooset MSBuild-parameters.</span><span class="sxs-lookup"><span data-stu-id="f2c26-164">hello properties for Azure publishing are in hello **Deployment** section, and you might also need tooset MSBuild parameters.</span></span> <span data-ttu-id="f2c26-165">Bijvoorbeeld in een cloud service-project toospecify een serviceconfiguratie dan 'Cloud' hello MSbuild parameters instellen te`/p:TargetProfile=[YourProfile]` waar *[YourProfile]* overeenkomt met een configuratiebestand voor de service met een naam zoals Serviceconfiguration zijn. *YourProfile*cscfg-bestand.</span><span class="sxs-lookup"><span data-stu-id="f2c26-165">For example, in a cloud service project, toospecify a service configuration other than "Cloud", set hello MSbuild parameters too`/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="f2c26-166">Hallo volgende tabel bevat de beschikbare eigenschappen Hallo in Hallo **implementatie** sectie:</span><span class="sxs-lookup"><span data-stu-id="f2c26-166">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="f2c26-167">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f2c26-167">Property</span></span> | <span data-ttu-id="f2c26-168">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="f2c26-168">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="f2c26-169">Niet-vertrouwde certificaten toestaan</span><span class="sxs-lookup"><span data-stu-id="f2c26-169">Allow Untrusted Certificates</span></span> |<span data-ttu-id="f2c26-170">Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie.</span><span class="sxs-lookup"><span data-stu-id="f2c26-170">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="f2c26-171">Upgrade toestaan</span><span class="sxs-lookup"><span data-stu-id="f2c26-171">Allow Upgrade</span></span> |<span data-ttu-id="f2c26-172">Hiermee kunt Hallo implementatie tooupdate een bestaande implementatie in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="f2c26-172">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="f2c26-173">Bewaart Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="f2c26-173">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="f2c26-174">Niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="f2c26-174">Do Not Delete</span></span> |<span data-ttu-id="f2c26-175">Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan).</span><span class="sxs-lookup"><span data-stu-id="f2c26-175">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="f2c26-176">Pad tooDeployment instellingen</span><span class="sxs-lookup"><span data-stu-id="f2c26-176">Path tooDeployment Settings</span></span> |<span data-ttu-id="f2c26-177">Hallo pad tooyour .pubxml bestand voor een web-app relatieve toohello-hoofdmap van het Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="f2c26-177">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="f2c26-178">Genegeerd voor cloud-services.</span><span class="sxs-lookup"><span data-stu-id="f2c26-178">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="f2c26-179">SharePoint-omgeving voor implementatie</span><span class="sxs-lookup"><span data-stu-id="f2c26-179">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="f2c26-180">dezelfde als de servicenaam Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2c26-180">hello same as hello service name.</span></span> |
    | <span data-ttu-id="f2c26-181">Azure-implementatie-omgeving</span><span class="sxs-lookup"><span data-stu-id="f2c26-181">Azure Deployment Environment</span></span> |<span data-ttu-id="f2c26-182">Hallo-app of cloud naam van de webservice.</span><span class="sxs-lookup"><span data-stu-id="f2c26-182">hello web app or cloud service name.</span></span> |
14. <span data-ttu-id="f2c26-183">Op dit tijdstip moet uw build worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="f2c26-183">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="f2c26-184">Als u dubbelklikt op de naam van de build hello, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f2c26-184">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="f2c26-185">In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u Hallo gekoppeld implementatie bekijken op Hallo **implementaties** tabblad wanneer Hallo staging-omgeving is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-185">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="f2c26-186">De URL van de site tooyour bladeren.</span><span class="sxs-lookup"><span data-stu-id="f2c26-186">Browse tooyour site's URL.</span></span> <span data-ttu-id="f2c26-187">Kies voor een web-app Hallo **Bladeren** knop in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="f2c26-187">For a web app, just choose  hello **Browse** button in hello portal.</span></span> <span data-ttu-id="f2c26-188">Kies voor een cloudservice Hallo URL uit Hallo **snel in één oogopslag** sectie Hallo **Dashboard** pagina waarin de faseringsomgeving Hallo.</span><span class="sxs-lookup"><span data-stu-id="f2c26-188">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment.</span></span>
    
    <span data-ttu-id="f2c26-189">Implementaties van continue integratie voor cloud-services worden gepubliceerde toohello faseringsomgeving standaard.</span><span class="sxs-lookup"><span data-stu-id="f2c26-189">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="f2c26-190">U kunt dit wijzigen door de instelling Hallo **alternatieve Cloudserviceomgeving** eigenschap te**productie**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-190">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="f2c26-191">Hier is waarbij Hallo site-URL op de dashboardpagina Hallo cloudservice.</span><span class="sxs-lookup"><span data-stu-id="f2c26-191">Here's where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="f2c26-192">Een nieuw browsertabblad geopend tooreveal uw site uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f2c26-192">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="f2c26-193">Als u andere wijzigingen tooyour project, u trigger builds meer en wordt u meerdere implementaties verzamelt.</span><span class="sxs-lookup"><span data-stu-id="f2c26-193">If you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="f2c26-194">Hallo laatste één is gemarkeerd als actief.</span><span class="sxs-lookup"><span data-stu-id="f2c26-194">hello latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="f2c26-195">5: een eerdere build implementeren</span><span class="sxs-lookup"><span data-stu-id="f2c26-195">5: Redeploy an earlier build</span></span>
<span data-ttu-id="f2c26-196">Deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="f2c26-196">This step is optional.</span></span> <span data-ttu-id="f2c26-197">In klassieke Azure-portal hello, kies een eerdere implementatie en **implementeren** toorewind uw site tooan eerder incheckt.</span><span class="sxs-lookup"><span data-stu-id="f2c26-197">In hello Azure classic portal, choose an earlier deployment and choose **Redeploy** toorewind your site tooan earlier check-in.</span></span> <span data-ttu-id="f2c26-198">Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="f2c26-198">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="f2c26-199">6: Hallo productie-implementatie wijzigen</span><span class="sxs-lookup"><span data-stu-id="f2c26-199">6: Change hello Production deployment</span></span>
<span data-ttu-id="f2c26-200">Wanneer u klaar bent, kunt u Hallo fasering toohello productieomgeving promoveren kiezen **wisselen** in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="f2c26-200">When you are ready, you can promote hello Staging environment toohello Production environment by choosing **Swap** in hello Azure classic portal.</span></span> <span data-ttu-id="f2c26-201">faseringsomgeving Hallo zojuist geïmplementeerde is gepromoveerde tooProduction en Hallo vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="f2c26-201">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="f2c26-202">Hallo actieve implementatie mogelijk anders voor hello productie- en faseringsomgevingen, maar de implementatiegeschiedenis Hallo van recente builds is Hallo dezelfde omgeving ongeacht.</span><span class="sxs-lookup"><span data-stu-id="f2c26-202">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="f2c26-203">7: implementeren vanuit een werkvertakking.</span><span class="sxs-lookup"><span data-stu-id="f2c26-203">7: Deploy from a working branch.</span></span>
<span data-ttu-id="f2c26-204">Wanneer u met Git, meestal wijzigingen aanbrengt in een werkvertakking en integreren in de hoofdvertakking Hallo wanneer de ontwikkeling van een voltooide status bereikt.</span><span class="sxs-lookup"><span data-stu-id="f2c26-204">When you use Git, you usually make changes in a working branch and integrate into hello master branch when your development reaches a finished state.</span></span> <span data-ttu-id="f2c26-205">Tijdens de ontwikkelingsfase Hallo van een project, u wilt toobuild en Hallo werkende vertakking tooAzure implementeren.</span><span class="sxs-lookup"><span data-stu-id="f2c26-205">During hello development phase of a project, you'll want toobuild and deploy hello working branch tooAzure.</span></span>

1. <span data-ttu-id="f2c26-206">In **Team Explorer**, kies Hallo **Start** knop en kies vervolgens Hallo **vertakkingen** knop.</span><span class="sxs-lookup"><span data-stu-id="f2c26-206">In **Team Explorer**, choose hello **Home** button and then choose hello **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="f2c26-207">Kies Hallo **nieuwe vertakking** koppeling.</span><span class="sxs-lookup"><span data-stu-id="f2c26-207">Choose hello **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="f2c26-208">Geef de naam Hallo van Hallo vertakking, zoals 'werken', en kies **vertakking maken**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-208">Enter hello name of hello branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="f2c26-209">Hiermee maakt u een nieuwe lokale vertakking.</span><span class="sxs-lookup"><span data-stu-id="f2c26-209">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="f2c26-210">Hallo vertakking publiceren.</span><span class="sxs-lookup"><span data-stu-id="f2c26-210">Publish hello branch.</span></span> <span data-ttu-id="f2c26-211">Kies Hallo vertakking naam in **niet gepubliceerd vertakkingen**, en kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-211">Choose hello branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="f2c26-212">Standaard verandert alleen toohello hoofdvertakking trigger een continue build.</span><span class="sxs-lookup"><span data-stu-id="f2c26-212">By default, only changes toohello master branch trigger a continuous build.</span></span> <span data-ttu-id="f2c26-213">tooset up continue build voor een werkvertakking, kies Hallo **Builds** pagina in **Team Explorer**, en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-213">tooset up continuous build for a working branch, choose hello **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="f2c26-214">Open Hallo **broninstellingen** tabblad. Onder **bewaakt vertakkingen voor continue integratie en build**, kies **Klik hier tooadd een nieuwe rij**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-214">Open hello **Source Settings** tab. Under **Monitored branches for continuous integration and build**, choose **Click here tooadd a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="f2c26-215">Hallo vertakking die u hebt gemaakt, zoals koppen refs werkende opgeven.</span><span class="sxs-lookup"><span data-stu-id="f2c26-215">Specify hello branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="f2c26-216">Een wijziging aanbrengt in Hallo code, open Hallo snelmenu voor het bestand Hallo gewijzigd, en kies vervolgens **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="f2c26-216">Make a change in hello code, open hello shortcut menu for hello changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="f2c26-217">Kies Hallo **niet-gesynchroniseerde doorvoeracties** koppeling en kies Hallo **synchronisatie** knop of Hallo **Push** koppeling toocopy Hallo wijzigingen toohello kopie van de werkvertakking Hallo in Visual Studio Teamservices.</span><span class="sxs-lookup"><span data-stu-id="f2c26-217">Choose hello **Unsynced Commits** link, and choose  hello **Sync** button or hello **Push** link toocopy hello changes toohello copy of hello working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="f2c26-218">Navigeer toohello **Builds** weergeven en Hallo-build die zojuist is geactiveerd voor Hallo werkvertakking niet vinden.</span><span class="sxs-lookup"><span data-stu-id="f2c26-218">Navigate toohello **Builds** view and find hello build that just got triggered for hello working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2c26-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f2c26-219">Next steps</span></span>
<span data-ttu-id="f2c26-220">toolearn meer tips over het gebruik van Git met Visual Studio Team Services, Zie [ontwikkelen en delen van uw code in Git met Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) en voor informatie over het gebruik van een Git-opslagplaats die niet wordt beheerd door Visual Studio Team Services toopublish tooAzure, Zie [continue implementatie tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="f2c26-220">toolearn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services toopublish tooAzure, see [Continuous Deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="f2c26-221">Zie voor meer informatie over Visual Studio Team Services [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="f2c26-221">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
