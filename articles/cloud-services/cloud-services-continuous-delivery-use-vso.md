---
title: Continue levering met Visual Studio Team Services in Azure | Microsoft Docs
description: Informatie over het configureren van uw Visual Studio Team Services teamprojecten om automatisch te bouwen en implementeren voor de functie Web-App in Azure App Service- of cloud-services.
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
ms.openlocfilehash: d80ce63eb7ddfd7c45726be887a772f9a7594b28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services"></a><span data-ttu-id="ae85a-103">Onafgebroken levering naar Azure met Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="ae85a-103">Continuous delivery to Azure using Visual Studio Team Services</span></span>
<span data-ttu-id="ae85a-104">U kunt uw teamprojecten Visual Studio Team Services om automatisch te bouwen en implementeren voor Azure-web-apps of cloudservices configureren.</span><span class="sxs-lookup"><span data-stu-id="ae85a-104">You can configure your Visual Studio Team Services team projects to automatically build and deploy to Azure web apps or cloud services.</span></span>  <span data-ttu-id="ae85a-105">(Voor meer informatie over het instellen van een doorlopende build en implementeren met behulp van system een *lokale* Team Foundation Server Zie [continue leveringsmethode voor Cloud-Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span><span class="sxs-lookup"><span data-stu-id="ae85a-105">(For information on how to set up a continuous build and deploy system using an *on-premises* Team Foundation Server, see [Continuous Delivery for Cloud Services in Azure](cloud-services-dotnet-continuous-delivery.md).)</span></span>

<span data-ttu-id="ae85a-106">Deze zelfstudie wordt ervan uitgegaan dat u hebt Visual Studio 2013 en de Azure-SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ae85a-106">This tutorial assumes you have Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="ae85a-107">Als u nog geen Visual Studio 2013 hebt, downloadt u dit door het kiezen van de **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="ae85a-107">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="ae85a-108">Installeer de Azure-SDK van [hier](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="ae85a-108">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="ae85a-109">U moet een Visual Studio Team Services-account om deze zelfstudie te voltooien: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="ae85a-109">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="ae85a-110">Voer de volgende stappen uit voordat u een cloudservice om automatisch te bouwen en implementeren in Azure met behulp van Visual Studio Team Services kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-110">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-team-project"></a><span data-ttu-id="ae85a-111">1: een teamproject maken</span><span class="sxs-lookup"><span data-stu-id="ae85a-111">1: Create a team project</span></span>
<span data-ttu-id="ae85a-112">Volg de instructies [hier](http://go.microsoft.com/fwlink/?LinkId=512980) uw teamproject maken en koppelen aan Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae85a-112">Follow the instructions [here](http://go.microsoft.com/fwlink/?LinkId=512980) to create your team project and link it to Visual Studio.</span></span> <span data-ttu-id="ae85a-113">In dit scenario wordt ervan uitgegaan dat u Team Foundation versie besturingselement (TFVC) gebruikt als oplossing voor uw gegevensbron.</span><span class="sxs-lookup"><span data-stu-id="ae85a-113">This walkthrough assumes you are using Team Foundation Version Control (TFVC) as your source control solution.</span></span> <span data-ttu-id="ae85a-114">Als u wilt met Git voor versiebeheer, Zie [de Git-versie van deze rondleiding](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span><span class="sxs-lookup"><span data-stu-id="ae85a-114">If you want to use Git for version control, see [the Git version of this walkthrough](http://go.microsoft.com/fwlink/p/?LinkId=397358).</span></span>

## <a name="2-check-in-a-project-to-source-control"></a><span data-ttu-id="ae85a-115">2: een project met resourcebeheer inchecken</span><span class="sxs-lookup"><span data-stu-id="ae85a-115">2: Check in a project to source control</span></span>
1. <span data-ttu-id="ae85a-116">In Visual Studio, opent u de oplossing die u wilt implementeren of een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="ae85a-116">In Visual Studio, open the solution you want to deploy, or create a new one.</span></span>
   <span data-ttu-id="ae85a-117">De stappen in dit scenario kunt u een web-app of een service in de cloud (Azure-toepassing) implementeren.</span><span class="sxs-lookup"><span data-stu-id="ae85a-117">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span>
   <span data-ttu-id="ae85a-118">Als u maken van een nieuwe oplossing wilt, maakt u een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project.</span><span class="sxs-lookup"><span data-stu-id="ae85a-118">If you want to create a new solution, create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="ae85a-119">Zorg ervoor dat het project gericht is op .NET Framework 4 of 4.5, en als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen en kiest u Internet-toepassing voor de Webrol.</span><span class="sxs-lookup"><span data-stu-id="ae85a-119">Make sure that the project targets .NET Framework 4 or 4.5, and if you are creating a cloud service project, add an ASP.NET MVC web role and a worker role, and choose Internet application for the web role.</span></span> <span data-ttu-id="ae85a-120">Als u wordt gevraagd, kiest u **internettoepassing**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-120">When prompted, choose **Internet Application**.</span></span>
   <span data-ttu-id="ae85a-121">Als u maken van een web-app wilt, kiest de ASP.NET-webtoepassing projectsjabloon, maken en kies vervolgens MVC.</span><span class="sxs-lookup"><span data-stu-id="ae85a-121">If you want to create a web app, choose the ASP.NET Web Application project template, and then choose MVC.</span></span> <span data-ttu-id="ae85a-122">Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="ae85a-122">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ae85a-123">Visual Studio Team Services ondersteunen alleen CI-implementaties van Visual Studio-webtoepassingen op dit moment.</span><span class="sxs-lookup"><span data-stu-id="ae85a-123">Visual Studio Team Services only support CI deployments of Visual Studio Web Applications at this time.</span></span> <span data-ttu-id="ae85a-124">Website-projecten vallen buiten het bereik.</span><span class="sxs-lookup"><span data-stu-id="ae85a-124">Web Site projects are out of scope.</span></span>
   > 
   > 
2. <span data-ttu-id="ae85a-125">Open het snelmenu voor de oplossing en kies **oplossing toevoegen aan bronbeheer**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-125">Open the context menu for the solution, and choose **Add Solution to Source Control**.</span></span>
   
    ![][5]
3. <span data-ttu-id="ae85a-126">Accepteer of wijzig de standaardinstellingen en klik op de **OK** knop.</span><span class="sxs-lookup"><span data-stu-id="ae85a-126">Accept or change the defaults and choose the **OK** button.</span></span> <span data-ttu-id="ae85a-127">Zodra het proces is voltooid, bron besturingselement pictogrammen worden weergegeven in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-127">Once the process completes, source control icons appear in **Solution Explorer**.</span></span>
   
    ![][6]
4. <span data-ttu-id="ae85a-128">Open het snelmenu voor de oplossing en kies **inchecken**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-128">Open the shortcut menu for the solution, and choose **Check In**.</span></span>
   
    ![][7]
5. <span data-ttu-id="ae85a-129">In de **wijzigingen in behandeling** gebied van **Team Explorer**, typ een opmerking voor het inchecken en kiest u de **inchecken** knop.</span><span class="sxs-lookup"><span data-stu-id="ae85a-129">In the **Pending Changes** area of **Team Explorer**, type a comment for the check-in and choose the **Check In** button.</span></span>
   
    ![][8]
   
    <span data-ttu-id="ae85a-130">Noteer de opties die u wilt opnemen of uitsluiten van specifieke wijzigingen wanneer u incheckt.</span><span class="sxs-lookup"><span data-stu-id="ae85a-130">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="ae85a-131">Indien gewenst wijzigingen zijn uitgesloten, kies de **omvatten alle** koppeling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-131">If desired changes are excluded, choose the **Include All** link.</span></span>
   
    ![][9]

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="ae85a-132">3: verbinding maken met het project naar Azure</span><span class="sxs-lookup"><span data-stu-id="ae85a-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="ae85a-133">Nu dat u een teamproject tegenover Team Services met sommige broncode erin hebt, bent u klaar uw teamproject verbinding te maken met Azure.</span><span class="sxs-lookup"><span data-stu-id="ae85a-133">Now that you have a VS Team Services team project with some source code in it, you are ready to connect your team project to Azure.</span></span>  <span data-ttu-id="ae85a-134">In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door het kiezen van de  **+**  pictogram naar links en te kiezen onder **Cloudservice**of **Web-App** en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the **+** icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span> <span data-ttu-id="ae85a-135">Kies de **publiceren met Visual Studio Team Services instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-135">Choose the **Set up publishing with Visual Studio Team Services** link.</span></span>
   
    ![][10]
2. <span data-ttu-id="ae85a-136">In de wizard, typ de naam van uw Visual Studio Team Services-account in het tekstvak en klik op de **autoriseren nu** koppeling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-136">In the wizard, type the name of your Visual Studio Team Services account in the textbox and click the **Authorize Now** link.</span></span> <span data-ttu-id="ae85a-137">U wordt mogelijk gevraagd aan te melden.</span><span class="sxs-lookup"><span data-stu-id="ae85a-137">You might be asked to sign in.</span></span>
   
    ![][11]
3. <span data-ttu-id="ae85a-138">In de **verbindingsaanvraag** pop-upvenster, kies de **accepteren** knop voor het autoriseren van Azure uw teamproject in VS-Team Services configureren.</span><span class="sxs-lookup"><span data-stu-id="ae85a-138">In the **Connection Request** pop-up dialog, choose the **Accept** button to authorize Azure to configure your team project in VS Team Services.</span></span>
   
    ![][12]
4. <span data-ttu-id="ae85a-139">Als de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met een lijst met uw teamprojecten Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="ae85a-139">When authorization succeeds, you see a dropdown containing a list of your Visual Studio Team Services team projects.</span></span> <span data-ttu-id="ae85a-140">Kies de naam van teamproject dat u in de vorige stappen hebt gemaakt en kies vervolgens de wizard vinkje knop.</span><span class="sxs-lookup"><span data-stu-id="ae85a-140">Choose  the name of team project that you created in the previous steps, and then choose the wizard's checkmark button.</span></span>
   
    ![][13]
5. <span data-ttu-id="ae85a-141">Nadat uw project is gekoppeld, ziet u enkele instructies voor het controleren van wijzigingen aan uw project Visual Studio Team Services-team.</span><span class="sxs-lookup"><span data-stu-id="ae85a-141">After your project is linked, you will see some instructions for checking in changes to your Visual Studio Team Services team project.</span></span>  <span data-ttu-id="ae85a-142">Bij de volgende controle, Visual Studio Team Services bouwt en uw project implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="ae85a-142">On your next check-in, Visual Studio Team Services will build and deploy your project to Azure.</span></span>  <span data-ttu-id="ae85a-143">Probeer deze nu door te klikken op de **inchecken vanuit Visual Studio** koppeling, en vervolgens de **Visual Studio starten** koppeling (of een vergelijkbare **Visual Studio** knop aan de onderkant van de Portal scherm).</span><span class="sxs-lookup"><span data-stu-id="ae85a-143">Try this now by clicking the **Check In from Visual Studio** link, and then the **Launch Visual Studio** link (or the equivalent **Visual Studio** button at the bottom of the portal screen).</span></span>
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="ae85a-144">4: de tabel opnieuw activeren en implementeren van uw project</span><span class="sxs-lookup"><span data-stu-id="ae85a-144">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="ae85a-145">In Visual Studio **Team Explorer**, kies de **Source Control Explorer** koppeling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-145">In Visual Studio's **Team Explorer**, choose the **Source Control Explorer** link.</span></span>
   
    ![][15]
2. <span data-ttu-id="ae85a-146">Ga naar uw oplossingsbestand en open het.</span><span class="sxs-lookup"><span data-stu-id="ae85a-146">Navigate to your solution file and open it.</span></span>
   
    ![][16]
3. <span data-ttu-id="ae85a-147">In **Solution Explorer**, opent u een bestand en deze te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-147">In **Solution Explorer**, open up a file and change it.</span></span> <span data-ttu-id="ae85a-148">Wijzig bijvoorbeeld het bestand `_Layout.cshtml` onder de weergaven\\gedeelde map in een MVC-Webrol.</span><span class="sxs-lookup"><span data-stu-id="ae85a-148">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
4. <span data-ttu-id="ae85a-149">Het logo voor de site bewerken en kies **Ctrl + S** het bestand wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="ae85a-149">Edit the logo for the site and choose **Ctrl+S** to save the file.</span></span>
   
    ![][18]
5. <span data-ttu-id="ae85a-150">In **Team Explorer**, kies de **wijzigingen in behandeling** koppeling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-150">In **Team Explorer**, choose the **Pending Changes** link.</span></span>
   
    ![][19]
6. <span data-ttu-id="ae85a-151">Voer een opmerking en kies vervolgens de **inchecken** knop.</span><span class="sxs-lookup"><span data-stu-id="ae85a-151">Enter a comment and then choose the **Check In** button.</span></span>
   
    ![][20]
7. <span data-ttu-id="ae85a-152">Kies de **thuis** terug te keren naar de **Team Explorer** startpagina.</span><span class="sxs-lookup"><span data-stu-id="ae85a-152">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="ae85a-153">Kies de **Builds** koppeling om de opbouw in voortgang weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ae85a-153">Choose the **Builds** link to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="ae85a-154">**In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="ae85a-154">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="ae85a-155">Dubbelklik op de naam van de build uitgevoerd om een gedetailleerde logboekbestanden tijdens de voortgang van de build weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ae85a-155">Double-click the name of the build in progress to view a detailed log as the build progresses.</span></span>
   
    ![][24]
10. <span data-ttu-id="ae85a-156">Hoewel de build in voortgang, bekijk de build-definitie die is gemaakt toen u TFS gekoppeld aan Azure met behulp van de wizard.</span><span class="sxs-lookup"><span data-stu-id="ae85a-156">While the build is in-progress, take a look at the build definition that was created when you linked TFS to Azure by using the wizard.</span></span>  <span data-ttu-id="ae85a-157">Open het snelmenu voor de definitie van de build en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-157">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
     ![][25]
    
     <span data-ttu-id="ae85a-158">In de **Trigger** tabblad ziet u dat de build-definitie is standaard ingesteld op voor elke inchecken bouwen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-158">In the **Trigger** tab, you will see that the build definition is set to build on every check-in by default.</span></span>
    
     ![][26]
    
     <span data-ttu-id="ae85a-159">In de **proces** tabblad ziet u de implementatieomgeving is ingesteld op de naam van uw cloud-service of web-app.</span><span class="sxs-lookup"><span data-stu-id="ae85a-159">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span> <span data-ttu-id="ae85a-160">Als u met web-apps werkt, niet de eigenschappen die u ziet verschillen van die hier wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ae85a-160">If you are working with web apps, the properties you see will be different from those shown here.</span></span>
    
     ![][27]
11. <span data-ttu-id="ae85a-161">Geef waarden voor de eigenschappen als u wilt dat andere waarden dan de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="ae85a-161">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="ae85a-162">De eigenschappen voor Azure publicatie zijn de **implementatie** sectie.</span><span class="sxs-lookup"><span data-stu-id="ae85a-162">The properties for Azure publishing are in the **Deployment** section.</span></span>
    
     <span data-ttu-id="ae85a-163">De volgende tabel bevat de beschikbare eigenschappen in de **implementatie** sectie:</span><span class="sxs-lookup"><span data-stu-id="ae85a-163">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="ae85a-164">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ae85a-164">Property</span></span> | <span data-ttu-id="ae85a-165">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="ae85a-165">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="ae85a-166">Niet-vertrouwde certificaten toestaan</span><span class="sxs-lookup"><span data-stu-id="ae85a-166">Allow Untrusted Certificates</span></span> |<span data-ttu-id="ae85a-167">Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie.</span><span class="sxs-lookup"><span data-stu-id="ae85a-167">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="ae85a-168">Upgrade toestaan</span><span class="sxs-lookup"><span data-stu-id="ae85a-168">Allow Upgrade</span></span> |<span data-ttu-id="ae85a-169">Hiermee kunt de implementatie bijwerken van een bestaande implementatie in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="ae85a-169">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="ae85a-170">Het IP-adres, blijft behouden.</span><span class="sxs-lookup"><span data-stu-id="ae85a-170">Preserves the IP address.</span></span> |
    | <span data-ttu-id="ae85a-171">Niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="ae85a-171">Do Not Delete</span></span> |<span data-ttu-id="ae85a-172">Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan).</span><span class="sxs-lookup"><span data-stu-id="ae85a-172">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="ae85a-173">Pad naar de implementatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="ae85a-173">Path to Deployment Settings</span></span> |<span data-ttu-id="ae85a-174">Het pad naar het bestand .pubxml voor een web-app, ten opzichte van de hoofdmap van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ae85a-174">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="ae85a-175">Genegeerd voor cloud-services.</span><span class="sxs-lookup"><span data-stu-id="ae85a-175">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="ae85a-176">SharePoint-omgeving voor implementatie</span><span class="sxs-lookup"><span data-stu-id="ae85a-176">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="ae85a-177">Hetzelfde als de naam van de service.</span><span class="sxs-lookup"><span data-stu-id="ae85a-177">The same as the service name.</span></span> |
    | <span data-ttu-id="ae85a-178">Azure-implementatie-omgeving</span><span class="sxs-lookup"><span data-stu-id="ae85a-178">Azure Deployment Environment</span></span> |<span data-ttu-id="ae85a-179">De web-app of cloud servicenaam.</span><span class="sxs-lookup"><span data-stu-id="ae85a-179">The web app or cloud service name.</span></span> |
12. <span data-ttu-id="ae85a-180">Als u meerdere-configuraties (.cscfg-bestanden) gebruikt, kunt u de configuratie van de gewenste service in de **bouwen, Geavanceerd MSBuild-argumenten** instelling.</span><span class="sxs-lookup"><span data-stu-id="ae85a-180">If you are using multiple service configurations (.cscfg files), you can specify the desired service configuration in the **Build, Advanced, MSBuild arguments** setting.</span></span> <span data-ttu-id="ae85a-181">Bijvoorbeeld, voor het gebruik van ServiceConfiguration.Test.cscfg ingesteld MSBuild-argumenten regeloptie `/p:TargetProfile=Test`.</span><span class="sxs-lookup"><span data-stu-id="ae85a-181">For example, to use ServiceConfiguration.Test.cscfg, set MSBuild arguments line option `/p:TargetProfile=Test`.</span></span>
    
     ![][38]
    
     <span data-ttu-id="ae85a-182">Op dit tijdstip moet uw build worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="ae85a-182">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
13. <span data-ttu-id="ae85a-183">Als u dubbelklikt op de naam van de build, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ae85a-183">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
14. <span data-ttu-id="ae85a-184">In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u de gekoppelde implementatie bekijken op de **implementaties** tabblad wanneer de faseringsomgeving is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ae85a-184">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
15. <span data-ttu-id="ae85a-185">Blader naar de URL van uw site.</span><span class="sxs-lookup"><span data-stu-id="ae85a-185">Browse to your site's URL.</span></span> <span data-ttu-id="ae85a-186">Voor een web-app, klik op de **Bladeren** knop op de opdrachtbalk.</span><span class="sxs-lookup"><span data-stu-id="ae85a-186">For a web app, just click the **Browse** button on the command bar.</span></span> <span data-ttu-id="ae85a-187">Voor een cloudservice, kiest u de URL in de **snel in één oogopslag** sectie van de **Dashboard** pagina waarin de faseringsomgeving voor een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ae85a-187">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment for a cloud service.</span></span> <span data-ttu-id="ae85a-188">Implementaties van continue integratie voor cloud-services worden gepubliceerd op de faseringsomgeving standaard.</span><span class="sxs-lookup"><span data-stu-id="ae85a-188">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="ae85a-189">U kunt dit wijzigen door in te stellen de **alternatieve Cloudserviceomgeving** eigenschap **productie**.</span><span class="sxs-lookup"><span data-stu-id="ae85a-189">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="ae85a-190">Deze schermafbeelding ziet waar de URL van de site is op de dashboardpagina van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="ae85a-190">This screenshot shows where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="ae85a-191">Een nieuw browsertabblad geopend om uw actieve site weer te geven.</span><span class="sxs-lookup"><span data-stu-id="ae85a-191">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
    
    <span data-ttu-id="ae85a-192">Cloud-services, als u andere wijzigingen aan uw project aanbrengt, u trigger builds meer en wordt u meerdere implementaties verzamelt.</span><span class="sxs-lookup"><span data-stu-id="ae85a-192">For cloud services, if you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="ae85a-193">Het recentste is gemarkeerd als actief.</span><span class="sxs-lookup"><span data-stu-id="ae85a-193">The latest one marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="ae85a-194">5: een eerdere build implementeren</span><span class="sxs-lookup"><span data-stu-id="ae85a-194">5: Redeploy an earlier build</span></span>
<span data-ttu-id="ae85a-195">Deze stap geldt voor cloudservices en is optioneel.</span><span class="sxs-lookup"><span data-stu-id="ae85a-195">This step applies to cloud services and is optional.</span></span> <span data-ttu-id="ae85a-196">In de klassieke Azure portal, kiest u een eerdere implementatie en kies vervolgens de **implementeren** knop terugspoelen van uw site een eerdere in te checken.</span><span class="sxs-lookup"><span data-stu-id="ae85a-196">In the Azure classic portal, choose an earlier deployment and then choose the **Redeploy** button to rewind your site to an earlier check-in.</span></span>  <span data-ttu-id="ae85a-197">Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="ae85a-197">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="ae85a-198">6: de productie-implementatie wijzigen</span><span class="sxs-lookup"><span data-stu-id="ae85a-198">6: Change the Production deployment</span></span>
<span data-ttu-id="ae85a-199">Deze stap geldt alleen voor cloud-services, niet-web-apps.</span><span class="sxs-lookup"><span data-stu-id="ae85a-199">This step applies only to cloud services, not web apps.</span></span> <span data-ttu-id="ae85a-200">Wanneer u klaar bent, kunt u de faseringsomgeving naar de productieomgeving promoveren kiezen de **wisselen** knop in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ae85a-200">When you are ready, you can promote the Staging environment to the production environment by choosing the **Swap** button in the Azure classic portal.</span></span> <span data-ttu-id="ae85a-201">De zojuist geïmplementeerde faseringsomgeving wordt gepromoveerd voor productie en de vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="ae85a-201">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="ae85a-202">De actieve implementatie mogelijk anders voor de productie- en Faseringsomgevingen, maar de geschiedenis van de implementatie van recente builds is hetzelfde, ongeacht de omgeving.</span><span class="sxs-lookup"><span data-stu-id="ae85a-202">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-run-unit-tests"></a><span data-ttu-id="ae85a-203">7: eenheidstests uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ae85a-203">7: Run unit tests</span></span>
<span data-ttu-id="ae85a-204">Deze stap geldt alleen voor web-apps, niet cloudservices.</span><span class="sxs-lookup"><span data-stu-id="ae85a-204">This step applies only to web apps, not cloud services.</span></span> <span data-ttu-id="ae85a-205">Als u een quality-gate voor uw implementatie, kunt u eenheidstests uitvoeren en als ze mislukken, kunt u de implementatie stoppen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-205">To put a quality gate on your deployment, you can run unit tests and if they fail, you can stop the deployment.</span></span>

1. <span data-ttu-id="ae85a-206">Voeg een eenheid test-project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae85a-206">In Visual Studio, add a unit test project.</span></span>
   
   ![][39]
2. <span data-ttu-id="ae85a-207">Projectverwijzingen toevoegen aan het project dat u wilt testen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-207">Add project references to the project you want to test.</span></span>
   
   ![][40]
3. <span data-ttu-id="ae85a-208">Sommige eenheidstests toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ae85a-208">Add some unit tests.</span></span> <span data-ttu-id="ae85a-209">Probeer een dummy-test die altijd wordt doorgegeven aan de slag.</span><span class="sxs-lookup"><span data-stu-id="ae85a-209">To get started, try a dummy test that will always pass.</span></span>
   
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
4. <span data-ttu-id="ae85a-210">Bewerk de build-definitie, kiest u de **proces** tabblad uit en vouw de **Test** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ae85a-210">Edit the build definition, choose the **Process** tab, and expand the **Test** node.</span></span>
5. <span data-ttu-id="ae85a-211">Stel de **mislukken build voor testfout** op True.</span><span class="sxs-lookup"><span data-stu-id="ae85a-211">Set the **Fail build on test failure** to True.</span></span> <span data-ttu-id="ae85a-212">Dit betekent dat de implementatie zich niet tenzij de tests zijn geslaagd.</span><span class="sxs-lookup"><span data-stu-id="ae85a-212">This means that the deployment won't occur unless the tests pass.</span></span>
   
   ![][41]
6. <span data-ttu-id="ae85a-213">Een nieuwe build wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ae85a-213">Queue a new build.</span></span>
   
   ![][42]
   
   ![][43]
7. <span data-ttu-id="ae85a-214">Terwijl de build nadert, informatie over de voortgang bekijken.</span><span class="sxs-lookup"><span data-stu-id="ae85a-214">While the build is proceeding, check on its progress.</span></span>
   
    ![][44]
   
    ![][45]
8. <span data-ttu-id="ae85a-215">Wanneer de build is voltooid, controleert u de testresultaten.</span><span class="sxs-lookup"><span data-stu-id="ae85a-215">When the build is done, check the test results.</span></span>
   
    ![][46]
   
    ![][47]
9. <span data-ttu-id="ae85a-216">Maak een test die mislukt.</span><span class="sxs-lookup"><span data-stu-id="ae85a-216">Try creating a test that will fail.</span></span> <span data-ttu-id="ae85a-217">Een nieuwe test toevoegen door te kopiëren van het eerste beheerpunt, wijzigt u de naam en de coderegel waarin wordt vermeld dat notimplementedexception is een verwachte uitzondering uitcommentariëren.</span><span class="sxs-lookup"><span data-stu-id="ae85a-217">Add a new test by copying the first one, rename it, and comment out the line of code that states NotImplementedException is an expected exception.</span></span>
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. <span data-ttu-id="ae85a-218">Controleer in de wijziging in de wachtrij een nieuwe build.</span><span class="sxs-lookup"><span data-stu-id="ae85a-218">Check in the change to queue a new build.</span></span>
    
     ![][48]
11. <span data-ttu-id="ae85a-219">Bekijk de testresultaten voor details over de fout.</span><span class="sxs-lookup"><span data-stu-id="ae85a-219">View the test results to see details about the failure.</span></span>
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a><span data-ttu-id="ae85a-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae85a-220">Next steps</span></span>
<span data-ttu-id="ae85a-221">Zie voor meer informatie over eenheid testen in Visual Studio Team Services, [eenheidstests uitvoeren in uw build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span><span class="sxs-lookup"><span data-stu-id="ae85a-221">For more about unit testing in Visual Studio Team Services, see [Run unit tests in your build](http://go.microsoft.com/fwlink/p/?LinkId=510474).</span></span> <span data-ttu-id="ae85a-222">Als u Git, Zie [delen van uw code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) en [continue implementatie naar Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="ae85a-222">If you're using Git, see [Share your code in Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) and [Continuous deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span>  <span data-ttu-id="ae85a-223">Zie voor meer informatie over Visual Studio Team Services, [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="ae85a-223">For more information about Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
