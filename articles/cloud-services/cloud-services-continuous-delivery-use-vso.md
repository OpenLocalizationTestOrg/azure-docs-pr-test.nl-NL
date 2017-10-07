---
title: aaaContinuous levering met Visual Studio Team Services in Azure | Microsoft Docs
description: Meer informatie over hoe tooconfigure uw Visual Studio Team Services team projecten tooautomatically bouwen en implementeren van de functie van de toohello Web-App in Azure App Service- of cloud-services.
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a><span data-ttu-id="01704-103">Continue levering tooAzure met behulp van Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="01704-103">Continuous delivery tooAzure using Visual Studio Team Services</span></span>
<span data-ttu-id="01704-104">U kunt uw Visual Studio Team Services team projecten tooautomatically build configureren en implementeren tooAzure web-apps of cloudservices.</span><span class="sxs-lookup"><span data-stu-id="01704-104">You can configure your Visual Studio Team Services team projects tooautomatically build and deploy tooAzure web apps or cloud services.</span></span>  <span data-ttu-id="01704-105">(Voor meer informatie over hoe tooset-up maken van een doorlopende build en implementeren met behulp van system een *lokale* Team Foundation Server Zie [continue leveringsmethode voor Cloud-Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="01704-105">(For information on how tooset up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="01704-106">Deze zelfstudie wordt ervan uitgegaan dat u hebt Visual Studio 2013 en hello Azure SDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="01704-106">This tutorial assumes you have Visual Studio 2013 and hello Azure SDK installed.</span></span> <span data-ttu-id="01704-107">Als u nog geen Visual Studio 2013 hebt, downloadt u dit door te kiezen Hallo **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com). Installeren Azure SDK Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="01704-107">If you don't already have Visual Studio 2013, download it by choosing hello **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com). Install hello Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="01704-108">U moet een toocomplete Visual Studio Team Services-account van deze zelfstudie: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="01704-108">You need an Visual Studio Team Services account toocomplete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="01704-109">tooset van een cloud service tooautomatically bouwen en tooAzure implementeren met behulp van Visual Studio Team Services, als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="01704-109">tooset up a cloud service tooautomatically build and deploy tooAzure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="01704-110">1: een teamproject maken</span><span class="sxs-lookup"><span data-stu-id="01704-110">1: Create a team project</span></span>
<span data-ttu-id="01704-111">Volg de instructies Hallo [hier](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate uw team project en een koppeling tooVisual Studio.</span><span class="sxs-lookup"><span data-stu-id="01704-111">Follow hello instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate your team project and link it tooVisual Studio.</span></span> <span data-ttu-id="01704-112">In dit scenario wordt ervan uitgegaan dat u Team Foundation versie besturingselement (TFVC) gebruikt als oplossing voor uw gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="01704-112">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="01704-113">Als u toouse Git voor versiebeheer wilt, Zie [Hallo Git-versie van deze rondleiding](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="01704-113">If you want toouse Git for version control, see [hello Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-toosource-control"></a><span data-ttu-id="01704-114">2: een project toosource besturingselement inchecken</span><span class="sxs-lookup"><span data-stu-id="01704-114">2: Check in a project toosource control</span></span>
1. <span data-ttu-id="01704-115">Open in Visual Studio Hallo-oplossing u wilt dat toodeploy of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="01704-115">In Visual Studio, open hello solution you want toodeploy, or create a new one.</span></span>
   <span data-ttu-id="01704-116">U kunt een web-app implementeren of een service in de cloud (Azure-toepassing) door de volgende Hallo stappen in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="01704-116">You can deploy a web app or a cloud service (Azure Application) by following hello steps in this walkthrough.</span></span>
   <span data-ttu-id="01704-117">Als u een nieuwe oplossing toocreate wilt, een nieuw Azure Cloud Service-project of een nieuwe ASP.NET MVC-project maken.</span><span class="sxs-lookup"><span data-stu-id="01704-117">If you want toocreate a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="01704-118">Zorg ervoor dat Hallo project doelen .NET Framework 4 of 4.5, en als u een cloudserviceproject maakt een ASP.NET MVC-Webrol en een werkrol toevoegen en kies Internet-toepassing voor de Webrol Hallo.</span><span class="sxs-lookup"><span data-stu-id="01704-118">Make sure that hello project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for hello web role.</span></span> <span data-ttu-id="01704-119">Als u wordt gevraagd, kiest u **internettoepassing**.</span><span class="sxs-lookup"><span data-stu-id="01704-119">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="01704-120">Als u toocreate een web-app wilt, kies Hallo ASP.NET-webtoepassing projectsjabloon en kies vervolgens MVC.</span><span class="sxs-lookup"><span data-stu-id="01704-120">If you want toocreate a web app, choose hello ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="01704-121">Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="01704-121">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="01704-122">Visual Studio Team Services ondersteunen alleen CI-implementaties van Visual Studio-webtoepassingen op dit moment.</span><span class="sxs-lookup"><span data-stu-id="01704-122">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="01704-123">Website-projecten vallen buiten het bereik.</span><span class="sxs-lookup"><span data-stu-id="01704-123">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="01704-124">Open Hallo contextmenu voor Hallo oplossing en kies **oplossing toevoegen tooSource besturingselement**.</span><span class="sxs-lookup"><span data-stu-id="01704-124">Open hello context menu for hello solution, and choose **Add Solution tooSource Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="01704-125">Accepteer of Hallo standaardinstellingen wijzigen en klik op Hallo **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="01704-125">Accept or change hello defaults and choose hello **OK** button.</span></span> <span data-ttu-id="01704-126">Zodra het Hallo-proces is voltooid, bron besturingselement pictogrammen worden weergegeven in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="01704-126">Once hello process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="01704-127">Open Hallo snelmenu voor Hallo oplossing en kies **inchecken**.</span><span class="sxs-lookup"><span data-stu-id="01704-127">Open hello shortcut menu for hello solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="01704-128">In Hallo **wijzigingen in behandeling** gebied van **Team Explorer**en typ een opmerking bij inchecken Hallo Hallo kiezen **inchecken** knop.</span><span class="sxs-lookup"><span data-stu-id="01704-128">In hello **Pending Changes** area of **Team Explorer**, type a comment for hello check-in and choose hello **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="01704-129">Houd er rekening mee Hallo opties tooinclude of specifieke wijzigingen uitsluiten wanneer u incheckt.</span><span class="sxs-lookup"><span data-stu-id="01704-129">Note hello options tooinclude or exclude specific changes when you check in.</span></span> <span data-ttu-id="01704-130">Indien gewenst wijzigingen zijn uitgesloten, kies Hallo **omvatten alle** koppeling.</span><span class="sxs-lookup"><span data-stu-id="01704-130">If desired changes are excluded, choose hello **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a><span data-ttu-id="01704-131">3: verbinding maken met de Hallo project tooAzure</span><span class="sxs-lookup"><span data-stu-id="01704-131">3: Connect hello project tooAzure</span></span>
1. <span data-ttu-id="01704-132">Nu dat u een teamproject tegenover Team Services met sommige broncode erin hebt, bent u klaar tooconnect uw team tooAzure project.</span><span class="sxs-lookup"><span data-stu-id="01704-132">Now that you have a VS Team Services team project with some source code in it, you are ready tooconnect your team project tooAzure.</span></span>  <span data-ttu-id="01704-133">In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door te kiezen Hallo  **+**  pictogram op Hallo linksonder en kiezen **Cloudservice** of **Web-App** en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="01704-133">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing hello **+** icon at hello bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="01704-134">Kies Hallo **publiceren met Visual Studio Team Services instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="01704-134">Choose hello **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="01704-135">In de wizard Hallo Typ Hallo-naam van uw Visual Studio Team Services-account Hallo tekstvak en klik op Hallo **autoriseren nu** koppeling.</span><span class="sxs-lookup"><span data-stu-id="01704-135">In hello wizard, type hello name of your Visual Studio Team Services account in hello textbox and click hello **Authorize Now** link.</span></span> <span data-ttu-id="01704-136">U wordt mogelijk gevraagd toosign in.</span><span class="sxs-lookup"><span data-stu-id="01704-136">You might be asked toosign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="01704-137">In Hallo **verbindingsaanvraag** pop-upvenster Hallo kiezen **accepteren** knop tooauthorize Azure tooconfigure uw team in VS-teamservices project.</span><span class="sxs-lookup"><span data-stu-id="01704-137">In hello **Connection Request** pop-up dialog, choose hello **Accept** button tooauthorize Azure tooconfigure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="01704-138">Als de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met een lijst met uw teamprojecten Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="01704-138">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="01704-139">Kies de naam Hallo van teamproject dat u hebt gemaakt in de vorige stappen Hallo en kies vervolgens van de wizard Hallo vinkje knop.</span><span class="sxs-lookup"><span data-stu-id="01704-139">Choose  hello name of team project that you created in hello previous steps, and then choose hello wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="01704-140">Nadat uw project is gekoppeld, ziet u enkele instructies voor het inchecken van wijzigingen tooyour Visual Studio Team Services teamproject.</span><span class="sxs-lookup"><span data-stu-id="01704-140">After your project is linked, you will see some instructions for checking in changes tooyour Visual Studio Team Services team project.</span></span>  <span data-ttu-id="01704-141">Bij de volgende controle, Visual Studio Team Services bouwt en implementeren van uw project tooAzure.</span><span class="sxs-lookup"><span data-stu-id="01704-141">On your next check-in, Visual Studio Team Services will build and deploy your project tooAzure.</span></span>  <span data-ttu-id="01704-142">Probeer deze nu door te klikken op Hallo **inchecken vanuit Visual Studio** koppelen en vervolgens Hallo **Visual Studio starten** koppeling (of gelijkwaardige Hallo **Visual Studio** knop Hallo onder aan portal welkomstscherm).</span><span class="sxs-lookup"><span data-stu-id="01704-142">Try this now by clicking hello **Check In from Visual Studio** link, and then hello **Launch Visual Studio** link (or hello equivalent **Visual Studio** button at hello bottom of hello portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="01704-143">4: de tabel opnieuw activeren en implementeren van uw project</span><span class="sxs-lookup"><span data-stu-id="01704-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="01704-144">In Visual Studio **Team Explorer**, kies Hallo **Source Control Explorer** koppeling.</span><span class="sxs-lookup"><span data-stu-id="01704-144">In Visual Studio's **Team Explorer**, choose hello **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="01704-145">Navigeer tooyour oplossingsbestand en open het.</span><span class="sxs-lookup"><span data-stu-id="01704-145">Navigate tooyour solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="01704-146">In **Solution Explorer**, opent u een bestand en deze te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="01704-146">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="01704-147">Wijzig bijvoorbeeld Hallo bestand `_Layout.cshtml` onder Hallo weergaven\\gedeelde map in een MVC-Webrol.</span><span class="sxs-lookup"><span data-stu-id="01704-147">For example, change hello file `_Layout.cshtml` under hello Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="01704-148">Hallo-logo voor Hallo site bewerken en kies **Ctrl + S** toosave Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="01704-148">Edit hello logo for hello site and choose **Ctrl+S** toosave hello file.</span></span>
   
    ![][18]
5. <span data-ttu-id="01704-149">In **Team Explorer**, kies Hallo **wijzigingen in behandeling** koppeling.</span><span class="sxs-lookup"><span data-stu-id="01704-149">In **Team Explorer**, choose hello **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="01704-150">Voer een opmerking en kies vervolgens Hallo **inchecken** knop.</span><span class="sxs-lookup"><span data-stu-id="01704-150">Enter a comment and then choose hello **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="01704-151">Kies Hallo **thuis** knop tooreturn toohello **Team Explorer** startpagina.</span><span class="sxs-lookup"><span data-stu-id="01704-151">Choose hello **Home** button tooreturn toohello **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="01704-152">Kies Hallo **Builds** koppeling tooview Hallo builds uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01704-152">Choose hello **Builds** link tooview hello builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="01704-153">**In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="01704-153">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="01704-154">Dubbelklik op Hallo van Hallo build in voortgang tooview een gedetailleerd logboek Hallo build loop.</span><span class="sxs-lookup"><span data-stu-id="01704-154">Double-click hello name of hello build in progress tooview a detailed log as hello build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="01704-155">Hallo build is uitgevoerd, bekijk Hallo build definitie die is gemaakt toen u TFS tooAzure gekoppeld met behulp van de wizard Hallo.</span><span class="sxs-lookup"><span data-stu-id="01704-155">While hello build is in-progress, take a look at hello build definition that was created when you linked TFS tooAzure by using hello wizard.</span></span>  <span data-ttu-id="01704-156">Hallo snelmenu voor Hallo build definitie openen en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="01704-156">Open hello shortcut menu for hello build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="01704-157">In Hallo **Trigger** tabblad ziet u dat Hallo build definitie is toobuild bij elke controle standaard ingesteld.</span><span class="sxs-lookup"><span data-stu-id="01704-157">In hello **Trigger** tab, you will see that hello build definition is set toobuild on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="01704-158">In Hallo **proces** tabblad ziet u de implementatieomgeving Hallo toohello naam van uw cloud-service of web-app is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="01704-158">In hello **Process** tab, you can see hello deployment environment is set toohello name of your cloud service or web app.</span></span> <span data-ttu-id="01704-159">Als u met web-apps werkt, is er Hallo-eigenschappen worden afwijken van die hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="01704-159">If you are working with web apps, hello properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="01704-160">Geef waarden voor Hallo eigenschappen als u wilt dat andere waarden dan Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="01704-160">Specify values for hello properties if you want different values than hello defaults.</span></span> <span data-ttu-id="01704-161">Hallo-eigenschappen voor Azure publicatie worden in Hallo **implementatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="01704-161">hello properties for Azure publishing are in hello **Deployment** section.</span></span>
    
     <span data-ttu-id="01704-162">Hallo volgende tabel bevat de beschikbare eigenschappen Hallo in Hallo **implementatie** sectie:</span><span class="sxs-lookup"><span data-stu-id="01704-162">hello following table shows hello available properties in hello **Deployment** section:</span></span>
    
    | <span data-ttu-id="01704-163">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="01704-163">Property</span></span> | <span data-ttu-id="01704-164">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="01704-164">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="01704-165">Niet-vertrouwde certificaten toestaan</span><span class="sxs-lookup"><span data-stu-id="01704-165">Allow Untrusted Certificates</span></span> |<span data-ttu-id="01704-166">Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie.</span><span class="sxs-lookup"><span data-stu-id="01704-166">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="01704-167">Upgrade toestaan</span><span class="sxs-lookup"><span data-stu-id="01704-167">Allow Upgrade</span></span> |<span data-ttu-id="01704-168">Hiermee kunt Hallo implementatie tooupdate een bestaande implementatie in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="01704-168">Allows hello deployment tooupdate an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="01704-169">Bewaart Hallo IP-adres.</span><span class="sxs-lookup"><span data-stu-id="01704-169">Preserves hello IP address.</span></span> |
    | <span data-ttu-id="01704-170">Niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="01704-170">Do Not Delete</span></span> |<span data-ttu-id="01704-171">Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan).</span><span class="sxs-lookup"><span data-stu-id="01704-171">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="01704-172">Pad tooDeployment instellingen</span><span class="sxs-lookup"><span data-stu-id="01704-172">Path tooDeployment Settings</span></span> |<span data-ttu-id="01704-173">Hallo pad tooyour .pubxml bestand voor een web-app relatieve toohello-hoofdmap van het Hallo-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="01704-173">hello path tooyour .pubxml file for a web app, relative toohello root folder of hello repo.</span></span> <span data-ttu-id="01704-174">Genegeerd voor cloud-services.</span><span class="sxs-lookup"><span data-stu-id="01704-174">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="01704-175">SharePoint-omgeving voor implementatie</span><span class="sxs-lookup"><span data-stu-id="01704-175">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="01704-176">dezelfde als de servicenaam Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="01704-176">hello same as hello service name.</span></span> |
    | <span data-ttu-id="01704-177">Azure-implementatie-omgeving</span><span class="sxs-lookup"><span data-stu-id="01704-177">Azure Deployment Environment</span></span> |<span data-ttu-id="01704-178">Hallo-app of cloud naam van de webservice.</span><span class="sxs-lookup"><span data-stu-id="01704-178">hello web app or cloud service name.</span></span> |
12. <span data-ttu-id="01704-179">Als u gebruikmaakt van serviceconfiguraties met meerdere (.cscfg-bestanden), kunt u de gewenste serviceconfiguratie Hallo opgeven in Hallo **bouwen, Geavanceerd MSBuild-argumenten** instelling.</span><span class="sxs-lookup"><span data-stu-id="01704-179">If you are using multiple service configurations (.cscfg files), you can specify hello desired service configuration in hello **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="01704-180">Bijvoorbeeld, toouse ServiceConfiguration.Test.cscfg, stelt MSBuild-argumenten regeloptie `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="01704-180">For example, toouse ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="01704-181">Op dit tijdstip moet uw build worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="01704-181">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="01704-182">Als u dubbelklikt op de naam van de build hello, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="01704-182">If you double-click hello build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="01704-183">In Hallo [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u Hallo gekoppeld implementatie bekijken op Hallo **implementaties** tabblad wanneer Hallo staging-omgeving is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="01704-183">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view hello associated deployment on hello **Deployments** tab when hello staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="01704-184">De URL van de site tooyour bladeren.</span><span class="sxs-lookup"><span data-stu-id="01704-184">Browse tooyour site's URL.</span></span> <span data-ttu-id="01704-185">Klik op Hallo voor een web-app **Bladeren** knop op de opdrachtbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="01704-185">For a web app, just click hello **Browse** button on hello command bar.</span></span> <span data-ttu-id="01704-186">Kies voor een cloudservice Hallo URL uit Hallo **snel in één oogopslag** sectie Hallo **Dashboard** pagina waarin de faseringsomgeving Hallo voor een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="01704-186">For a cloud service, choose hello URL in hello **Quick Glance** section of hello **Dashboard** page that shows hello Staging environment for a cloud service.</span></span> <span data-ttu-id="01704-187">Implementaties van continue integratie voor cloud-services worden gepubliceerde toohello faseringsomgeving standaard.</span><span class="sxs-lookup"><span data-stu-id="01704-187">Deployments from continuous integration for cloud services are published toohello Staging environment by default.</span></span> <span data-ttu-id="01704-188">U kunt dit wijzigen door de instelling Hallo **alternatieve Cloudserviceomgeving** eigenschap te**productie**.</span><span class="sxs-lookup"><span data-stu-id="01704-188">You can change this by setting hello **Alternate Cloud Service Environment** property too**Production**.</span></span> <span data-ttu-id="01704-189">Deze Schermafbeelding toont waar hello dat site-URL is op de dashboardpagina Hallo cloudservice.</span><span class="sxs-lookup"><span data-stu-id="01704-189">This screenshot shows where hello site URL is on hello cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="01704-190">Een nieuw browsertabblad geopend tooreveal uw site uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="01704-190">A new browser tab will open tooreveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="01704-191">Cloud-services, als u andere wijzigingen tooyour-project maakt, u trigger builds meer en wordt u meerdere implementaties verzamelt.</span><span class="sxs-lookup"><span data-stu-id="01704-191">For cloud services, if you make other changes tooyour project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="01704-192">Hallo recentste is gemarkeerd als actief.</span><span class="sxs-lookup"><span data-stu-id="01704-192">hello latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="01704-193">5: een eerdere build implementeren</span><span class="sxs-lookup"><span data-stu-id="01704-193">5: Redeploy an earlier build</span></span>
<span data-ttu-id="01704-194">Deze stap geldt toocloud services en is optioneel.</span><span class="sxs-lookup"><span data-stu-id="01704-194">This step applies toocloud services and is optional.</span></span> <span data-ttu-id="01704-195">In klassieke Azure-portal hello, kiest u een eerdere implementatie en kies vervolgens Hallo **implementeren** knop toorewind uw site tooan eerder incheckt.</span><span class="sxs-lookup"><span data-stu-id="01704-195">In hello Azure classic portal, choose an earlier deployment and then choose hello **Redeploy** button toorewind your site tooan earlier check-in.</span></span>  <span data-ttu-id="01704-196">Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="01704-196">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-hello-production-deployment"></a><span data-ttu-id="01704-197">6: Hallo productie-implementatie wijzigen</span><span class="sxs-lookup"><span data-stu-id="01704-197">6: Change hello Production deployment</span></span>
<span data-ttu-id="01704-198">Deze stap geldt alleen toocloud services, niet-web-apps.</span><span class="sxs-lookup"><span data-stu-id="01704-198">This step applies only toocloud services, not web apps.</span></span> <span data-ttu-id="01704-199">Wanneer u klaar bent, kunt u Hallo fasering toohello productieomgeving promoveren Hallo kiezen **wisselen** knop in Hallo klassieke Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="01704-199">When you are ready, you can promote hello Staging environment toohello production environment by choosing hello **Swap** button in hello Azure classic portal.</span></span> <span data-ttu-id="01704-200">faseringsomgeving Hallo zojuist geïmplementeerde is gepromoveerde tooProduction en Hallo vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="01704-200">hello newly deployed Staging environment is promoted tooProduction, and hello previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="01704-201">Hallo actieve implementatie mogelijk anders voor hello productie- en faseringsomgevingen, maar de implementatiegeschiedenis Hallo van recente builds is Hallo dezelfde omgeving ongeacht.</span><span class="sxs-lookup"><span data-stu-id="01704-201">hello Active deployment may be different for hello Production and Staging environments, but hello deployment history of recent builds is hello same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="01704-202">7: eenheidstests uitvoeren</span><span class="sxs-lookup"><span data-stu-id="01704-202">7: Run unit tests</span></span>
<span data-ttu-id="01704-203">Deze stap geldt alleen tooweb apps, niet-cloudservices.</span><span class="sxs-lookup"><span data-stu-id="01704-203">This step applies only tooweb apps, not cloud services.</span></span> <span data-ttu-id="01704-204">tooput een quality-gate voor uw implementatie, kunt u eenheidstests uitvoeren en als ze mislukken, kunt u Hallo implementatie stoppen.</span><span class="sxs-lookup"><span data-stu-id="01704-204">tooput a quality gate on your deployment, you can run unit tests and if they fail, you can stop hello deployment.</span></span>

1. <span data-ttu-id="01704-205">Voeg een eenheid test-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="01704-205">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="01704-206">Project verwijst naar toohello project u tootest wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="01704-206">Add project references toohello project you want tootest.</span></span>
   
   ![][40]
3. <span data-ttu-id="01704-207">Sommige eenheidstests toevoegen.</span><span class="sxs-lookup"><span data-stu-id="01704-207">Add some unit tests.</span></span> <span data-ttu-id="01704-208">tooget gestart, probeert u een dummy-test die altijd wordt doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="01704-208">tooget started, try a dummy test that will always pass.</span></span>
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. <span data-ttu-id="01704-209">De definitie van de build Hallo bewerken, kiest u Hallo **proces** tabblad uit en vouw Hallo **Test** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="01704-209">Edit hello build definition, choose hello **Process** tab, and expand hello **Test** node.</span></span>
5. <span data-ttu-id="01704-210">Set Hallo **mislukken build voor testfout** tooTrue.</span><span class="sxs-lookup"><span data-stu-id="01704-210">Set hello **Fail build on test failure** tooTrue.</span></span> <span data-ttu-id="01704-211">Dit betekent dat Hallo implementatie zich niet tenzij Hallo test zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="01704-211">This means that hello deployment won't occur unless hello tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="01704-212">Een nieuwe build wachtrij.</span><span class="sxs-lookup"><span data-stu-id="01704-212">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="01704-213">Tijdens het Hallo-build nadert, informatie over de voortgang bekijken.</span><span class="sxs-lookup"><span data-stu-id="01704-213">While hello build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="01704-214">Wanneer Hallo build is voltooid, controleert u de resultaten bekijkt hello.</span><span class="sxs-lookup"><span data-stu-id="01704-214">When hello build is done, check hello test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="01704-215">Maak een test die mislukt.</span><span class="sxs-lookup"><span data-stu-id="01704-215">Try creating a test that will fail.</span></span> <span data-ttu-id="01704-216">Toevoegen van een nieuwe test door te kopiëren Hallo eerste, wijzigt u de naam en uitcommentariëren Hallo coderegel dat notimplementedexception is een verwachte uitzondering gemeld.</span><span class="sxs-lookup"><span data-stu-id="01704-216">Add a new test by copying hello first one, rename it, and comment out hello line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="01704-217">Inchecken Hallo tooqueue een nieuwe build wijzigen.</span><span class="sxs-lookup"><span data-stu-id="01704-217">Check in hello change tooqueue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="01704-218">Hallo test resultaten toosee details weergeven over Hallo-fout.</span><span class="sxs-lookup"><span data-stu-id="01704-218">View hello test results toosee details about hello failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="01704-219">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="01704-219">Next steps</span></span>
<span data-ttu-id="01704-220">Zie voor meer informatie over eenheid testen in Visual Studio Team Services, [eenheidstests uitvoeren in uw build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="01704-220">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="01704-221">Als u Git, Zie [delen van uw code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) en [continue implementatie tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="01704-221">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment tooAzure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="01704-222">Zie voor meer informatie over Visual Studio Team Services, [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="01704-222">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
