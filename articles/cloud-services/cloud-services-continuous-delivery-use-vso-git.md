---
title: Continue levering met Git en Visual Studio Team Services in Azure | Microsoft Docs
description: Informatie over het configureren van uw teamprojecten Visual Studio Team Services voor het gebruik van Git om automatisch te bouwen en implementeren voor de functie Web-App in Azure App Service- of cloud-services.
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
ms.openlocfilehash: f4f5f231536bc381d17898ff2c592be821168a65
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="continuous-delivery-to-azure-using-visual-studio-team-services-and-git"></a><span data-ttu-id="1f9aa-103">Onafgebroken levering naar Azure met Visual Studio Team Services en Git</span><span class="sxs-lookup"><span data-stu-id="1f9aa-103">Continuous delivery to Azure using Visual Studio Team Services and Git</span></span>
<span data-ttu-id="1f9aa-104">Teamprojecten Visual Studio Team Services kunt u een Git-opslagplaats host voor de broncode en om automatisch te bouwen en implementeren voor Azure-web-apps of cloudservices wanneer u een doorvoeren naar de opslagplaats forceren.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-104">You can use Visual Studio Team Services team projects to host a Git repository for your source code, and automatically build and deploy to Azure web apps or cloud services whenever you push a commit to the repository.</span></span>

<span data-ttu-id="1f9aa-105">U moet Visual Studio 2013 en de Azure-SDK geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-105">You'll need Visual Studio 2013 and the Azure SDK installed.</span></span> <span data-ttu-id="1f9aa-106">Als u nog geen Visual Studio 2013 hebt, downloadt u dit door het kiezen van de **gratis aan de slag** koppeling [www.visualstudio.com](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-106">If you don't already have Visual Studio 2013, download it by choosing the **Get started for free** link at [www.visualstudio.com](http://www.visualstudio.com).</span></span> <span data-ttu-id="1f9aa-107">Installeer de Azure-SDK van [hier](http://go.microsoft.com/fwlink/?LinkId=239540).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-107">Install the Azure SDK from [here](http://go.microsoft.com/fwlink/?LinkId=239540).</span></span>

> [!NOTE]
> <span data-ttu-id="1f9aa-108">U moet een Visual Studio Team Services-account om deze zelfstudie te voltooien: U kunt [gratis een Visual Studio Team Services-account openen](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-108">You need an Visual Studio Team Services account to complete this tutorial: You can [open a Visual Studio Team Services account for free](http://go.microsoft.com/fwlink/p/?LinkId=512979).</span></span>
> 
> 

<span data-ttu-id="1f9aa-109">Voer de volgende stappen uit voordat u een cloudservice om automatisch te bouwen en implementeren in Azure met behulp van Visual Studio Team Services kunt instellen.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-109">To set up a cloud service to automatically build and deploy to Azure by using Visual Studio Team Services, follow these steps.</span></span>

## <a name="1-create-a-git-repository"></a><span data-ttu-id="1f9aa-110">1: een Git-opslagplaats maken</span><span class="sxs-lookup"><span data-stu-id="1f9aa-110">1: Create a Git repository</span></span>
1. <span data-ttu-id="1f9aa-111">Als u nog een Visual Studio Team Services-account hebt, kunt u een [hier](http://go.microsoft.com/fwlink/?LinkId=397665).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-111">If you don’t already have a Visual Studio Team Services account, you can get one  [here](http://go.microsoft.com/fwlink/?LinkId=397665).</span></span> <span data-ttu-id="1f9aa-112">Wanneer u uw teamproject maakt, kiest u Git als uw bronbeheersysteem.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-112">When you create your team project, choose Git as your source control system.</span></span> <span data-ttu-id="1f9aa-113">Volg de instructies voor het verbinden van Visual Studio aan uw teamproject.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-113">Follow the instructions to connect Visual Studio to your team project.</span></span>
2. <span data-ttu-id="1f9aa-114">In **Team Explorer**, kies de **deze opslagplaats klonen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-114">In **Team Explorer**, choose the **Clone this repository** link.</span></span>
   
    ![][3]
3. <span data-ttu-id="1f9aa-115">Geef de locatie van de lokale kopie en kies vervolgens de **kloon** knop.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-115">Specify the location of the local copy and then choose the **Clone** button.</span></span>

## <a name="2-create-a-project-and-commit-it-to-the-repository"></a><span data-ttu-id="1f9aa-116">2: Maak een project en het doorvoeren naar de opslagplaats</span><span class="sxs-lookup"><span data-stu-id="1f9aa-116">2: Create a project and commit it to the repository</span></span>
1. <span data-ttu-id="1f9aa-117">In **Team Explorer**, in de **oplossingen** sectie, kiest u de **nieuw** koppeling naar een nieuw project maken in de lokale opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-117">In **Team Explorer**, in the **Solutions** section, choose the **New** link to create a new project in the local repository.</span></span>
   
    ![][4]
2. <span data-ttu-id="1f9aa-118">De stappen in dit scenario kunt u een web-app of een service in de cloud (Azure-toepassing) implementeren.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-118">You can deploy a web app or a cloud service (Azure Application) by following the steps in this walkthrough.</span></span> <span data-ttu-id="1f9aa-119">Maak een nieuw Azure Cloud Service-project of een nieuw ASP.NET MVC-project.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-119">Create a new Azure Cloud Service project, or a new ASP.NET MVC project.</span></span> <span data-ttu-id="1f9aa-120">Controleer of het project gericht op .NET Framework 4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-120">Make sure that the project targets the .NET Framework 4 or later.</span></span> <span data-ttu-id="1f9aa-121">Als u een cloudserviceproject maakt, een ASP.NET MVC-Webrol en een werkrol toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-121">If you are creating a cloud service project, add an ASP.NET MVC web role and a worker role.</span></span>
   <span data-ttu-id="1f9aa-122">Als u maken van een web-app wilt, kiest u de **ASP.NET-webtoepassing** sjabloon project en kies vervolgens **MVC**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-122">If you want to create a web app, choose the **ASP.NET Web Application** project template, and then choose **MVC**.</span></span> <span data-ttu-id="1f9aa-123">Zie [een ASP.NET-web-app maken in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-123">See [Create an ASP.NET web app in Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) for more information.</span></span>
3. <span data-ttu-id="1f9aa-124">Open het snelmenu voor de oplossing en kies **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-124">Open the shortcut menu for the solution, and choose **Commit**.</span></span>
   
    ![][7]
4. <span data-ttu-id="1f9aa-125">Als dit de eerste keer dat u Git in Visual Studio Team Services hebt gebruikt, moet u bepaalde informatie gegeven om u te identificeren in Git.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-125">If this is the first time you've used Git in Visual Studio Team Services, you'll need to provide some information to identify yourself in Git.</span></span> <span data-ttu-id="1f9aa-126">In de **wijzigingen in behandeling** gebied van **Team Explorer**, Voer uw gebruikersnaam en e-mailadres.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-126">In the **Pending Changes** area of **Team Explorer**, enter your username and email address.</span></span> <span data-ttu-id="1f9aa-127">Voer een opmerking in voor het doorvoeren en kies vervolgens de **doorvoeren** knop.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-127">Enter a comment for the commit and then choose the **Commit** button.</span></span>
   
    ![][8]
5. <span data-ttu-id="1f9aa-128">Noteer de opties die u wilt opnemen of uitsluiten van specifieke wijzigingen wanneer u incheckt.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-128">Note the options to include or exclude specific changes when you check in.</span></span> <span data-ttu-id="1f9aa-129">Als u de gewenste wijzigingen zijn uitgesloten, kiest u **omvatten alle**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-129">If the changes you want are excluded, choose **Include All**.</span></span>
6. <span data-ttu-id="1f9aa-130">U hebt nu de wijzigingen doorgevoerd in het lokale exemplaar van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-130">You've now committed the changes in your local copy of the repository.</span></span> <span data-ttu-id="1f9aa-131">Vervolgens deze wijzigingen met de server te synchroniseren door het kiezen van de **Sync** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-131">Next, sync those changes with the server by choosing the **Sync** link.</span></span>

## <a name="3-connect-the-project-to-azure"></a><span data-ttu-id="1f9aa-132">3: verbinding maken met het project naar Azure</span><span class="sxs-lookup"><span data-stu-id="1f9aa-132">3: Connect the project to Azure</span></span>
1. <span data-ttu-id="1f9aa-133">Nu dat u een Git-opslagplaats in Visual Studio Team Services met sommige broncode erin hebt, bent u klaar om de git-opslagplaats met in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-133">Now that you have a Git repository in Visual Studio Team Services with some source code in it, you are ready to connect your git repository to Azure.</span></span>  <span data-ttu-id="1f9aa-134">In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), selecteer uw cloud-service of web-app of een nieuwe maken door het kiezen van de + pictogram naar links en te kiezen onder **Cloudservice** of **Web-App** en vervolgens **snelle invoer**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-134">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), select your cloud service or web app, or create a new one by choosing the + icon at the bottom left and choosing **Cloud Service** or **Web App** and then **Quick Create**.</span></span>
   
    ![][9]
2. <span data-ttu-id="1f9aa-135">Kies voor cloudservices, de **publiceren met Visual Studio Team Services instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-135">For cloud services, choose the **Set up publishing with Visual Studio Team Services** link.</span></span> <span data-ttu-id="1f9aa-136">Kies voor web-apps, de **implementatie vanuit resourcebeheer instellen** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-136">For web apps, choose the **Set up deployment from source control** link.</span></span>
   
    ![][10]
3. <span data-ttu-id="1f9aa-137">Typ de naam van uw Visual Studio Team Services-account in het tekstvak in de wizard en kies de **autoriseren nu** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-137">In the wizard, type the name of your Visual Studio Team Services account in the textbox and choose the **Authorize Now** link.</span></span> <span data-ttu-id="1f9aa-138">U wordt mogelijk gevraagd aan te melden.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-138">You might be asked to sign in.</span></span>
   
    ![][11]
4. <span data-ttu-id="1f9aa-139">In de **verbindingsaanvraag** pop-upvenster kiezen **accepteren** voor het autoriseren van Azure voor het configureren van uw teamproject in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-139">In the **Connection Request** pop-up dialog, choose **Accept** to authorize Azure to configure your team project in Visual Studio Team Services.</span></span>
   
    ![][12]
5. <span data-ttu-id="1f9aa-140">Nadat de autorisatie is geslaagd, ziet u een vervolgkeuzelijst met uw teamprojecten Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-140">After authorization succeeds, you see a dropdown list that contains your Visual Studio Team Services team projects.</span></span>  <span data-ttu-id="1f9aa-141">Selecteer de naam van teamproject dat u in de vorige stappen hebt gemaakt en kies selectievakje-knop van de wizard.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-141">Select the name of team project that you created in the previous steps, and choose the wizard's checkmark button.</span></span>
   
    ![][13]
   
    <span data-ttu-id="1f9aa-142">De volgende keer dat u het doorvoeren van gegevens naar uw opslagplaats pushen Visual Studio Team Services bouwt en uw project implementeren in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-142">The next time you push a commit to your repository, Visual Studio Team Services will build and deploy your project to Azure.</span></span>

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a><span data-ttu-id="1f9aa-143">4: de tabel opnieuw activeren en implementeren van uw project</span><span class="sxs-lookup"><span data-stu-id="1f9aa-143">4: Trigger a rebuild and redeploy your project</span></span>
1. <span data-ttu-id="1f9aa-144">In Visual Studio, opent u een bestand en deze te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-144">In Visual Studio, open up a file and change it.</span></span> <span data-ttu-id="1f9aa-145">Wijzig bijvoorbeeld het bestand `_Layout.cshtml` onder de weergaven\\gedeelde map in een MVC-Webrol.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-145">For example, change the file `_Layout.cshtml` under the Views\\Shared folder in an MVC web role.</span></span>
   
    ![][17]
2. <span data-ttu-id="1f9aa-146">Bewerk de voettekst voor de site en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-146">Edit the footer text for the site and save the file.</span></span>
   
    ![][18]
3. <span data-ttu-id="1f9aa-147">In **Solution Explorer**, open het snelmenu voor het knooppunt oplossing, projectknooppunt of het bestand gewijzigd, en kies vervolgens **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-147">In **Solution Explorer**, open the shortcut menu for the solution node, project node, or the file you changed, and then choose **Commit**.</span></span>
4. <span data-ttu-id="1f9aa-148">Typ in een opmerking en kies **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-148">Type in a comment and choose **Commit**.</span></span>
   
    ![][20]
5. <span data-ttu-id="1f9aa-149">Kies de **Sync** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-149">Choose the **Sync** link.</span></span>
   
    ![][38]
6. <span data-ttu-id="1f9aa-150">Kies de **Push** koppeling naar uw commit push naar de opslagplaats in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-150">Choose the **Push** link to push your commit to the repository in Visual Studio Team Services.</span></span> <span data-ttu-id="1f9aa-151">(U kunt ook de **Sync** knop uw doorvoeracties kopiëren naar de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-151">(You can also use the **Sync** button to copy your commits to the repository.</span></span> <span data-ttu-id="1f9aa-152">Het verschil is dat **Sync** ook de meest recente wijzigingen ophaalt uit de opslagplaats.)</span><span class="sxs-lookup"><span data-stu-id="1f9aa-152">The difference is that **Sync** also pulls the latest changes from the repository.)</span></span>
   
    ![][39]
7. <span data-ttu-id="1f9aa-153">Kies de **thuis** terug te keren naar de **Team Explorer** startpagina.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-153">Choose the **Home** button to return to the **Team Explorer** home page.</span></span>
   
    ![][21]
8. <span data-ttu-id="1f9aa-154">Kies **Builds** om weer te geven van de opbouw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-154">Choose **Builds** to view the builds in progress.</span></span>
   
    ![][22]
   
    <span data-ttu-id="1f9aa-155">**In een team Explorer** ziet u dat een build voor uw inchecken is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-155">**Team Explorer** shows that a build has been triggered for your check-in.</span></span>
   
    ![][23]
9. <span data-ttu-id="1f9aa-156">Om weer te geven een gedetailleerd logboek in de loop van de build, dubbelklikt u op de naam van de build uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-156">To view a detailed log as the build progresses, double-click the name of the build in progress.</span></span>
10. <span data-ttu-id="1f9aa-157">Hoewel de build in voortgang, bekijk de build-definitie die is gemaakt toen u de wizard hebt gebruikt om te koppelen aan Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-157">While the build is in-progress, take a look at the build definition that was created when you used the wizard to link to Azure.</span></span>  <span data-ttu-id="1f9aa-158">Open het snelmenu voor de definitie van de build en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-158">Open the shortcut menu for the build definition and choose **Edit Build Definition**.</span></span>
    
    ![][25]
11. <span data-ttu-id="1f9aa-159">In de **Trigger** tabblad ziet u dat de definitie van de build is standaard ingesteld op voor elke inchecken bouwen.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-159">In the **Trigger** tab, you will see that the build definition is set to build on every check-in, by default.</span></span> <span data-ttu-id="1f9aa-160">(Voor een cloudservice, Visual Studio Team Services bouwt en worden de hoofdvertakking geïmplementeerd op de testomgeving.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-160">(For a cloud service, Visual Studio Team Services builds and deploys the master branch to the staging environment automatically.</span></span> <span data-ttu-id="1f9aa-161">U hebt nog wel een handmatige stap naar de live site implementeren.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-161">You still have to do a manual step to deploy to the live site.</span></span> <span data-ttu-id="1f9aa-162">Voor een web-app dat geen staging-omgeving, wordt de hoofdvertakking geïmplementeerd rechtstreeks naar de live site.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-162">For a web app that doesn't have staging environment, it deploys the master branch directly to the live site.</span></span>
    
    ![][26]
12. <span data-ttu-id="1f9aa-163">In de **proces** tabblad ziet u de implementatieomgeving is ingesteld op de naam van uw cloud-service of web-app.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-163">In the **Process** tab, you can see the deployment environment is set to the name of your cloud service or web app.</span></span>
    
     ![][27]
13. <span data-ttu-id="1f9aa-164">Geef waarden voor de eigenschappen als u wilt dat andere waarden dan de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-164">Specify values for the properties if you want different values than the defaults.</span></span> <span data-ttu-id="1f9aa-165">De eigenschappen voor Azure publicatie zijn de **implementatie** sectie en kunt u wellicht ook MSBuild-parameters instellen.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-165">The properties for Azure publishing are in the **Deployment** section, and you might also need to set MSBuild parameters.</span></span> <span data-ttu-id="1f9aa-166">Bijvoorbeeld in een cloud service-project op te geven van een serviceconfiguratie dan 'Cloud' ingesteld de MSbuild-parameters op `/p:TargetProfile=[YourProfile]` waar *[YourProfile]* overeenkomt met een configuratiebestand voor de service met een naam zoals serviceconfiguration zijn. *YourProfile*cscfg-bestand.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-166">For example, in a cloud service project, to specify a service configuration other than "Cloud", set the MSbuild parameters to `/p:TargetProfile=[YourProfile]` where *[YourProfile]* matches a service configuration file with a name like ServiceConfiguration.*YourProfile*.cscfg.</span></span>
    
     <span data-ttu-id="1f9aa-167">De volgende tabel bevat de beschikbare eigenschappen in de **implementatie** sectie:</span><span class="sxs-lookup"><span data-stu-id="1f9aa-167">The following table shows the available properties in the **Deployment** section:</span></span>
    
    | <span data-ttu-id="1f9aa-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1f9aa-168">Property</span></span> | <span data-ttu-id="1f9aa-169">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="1f9aa-169">Default Value</span></span> |
    | --- | --- |
    | <span data-ttu-id="1f9aa-170">Niet-vertrouwde certificaten toestaan</span><span class="sxs-lookup"><span data-stu-id="1f9aa-170">Allow Untrusted Certificates</span></span> |<span data-ttu-id="1f9aa-171">Als het ONWAAR is, moeten de SSL-certificaten zijn ondertekend door een basisinstantie.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-171">If false, SSL certificates must be signed by a root authority.</span></span> |
    | <span data-ttu-id="1f9aa-172">Upgrade toestaan</span><span class="sxs-lookup"><span data-stu-id="1f9aa-172">Allow Upgrade</span></span> |<span data-ttu-id="1f9aa-173">Hiermee kunt de implementatie bijwerken van een bestaande implementatie in plaats van een nieuwe maken.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-173">Allows the deployment to update an existing deployment instead of creating a new one.</span></span> <span data-ttu-id="1f9aa-174">Het IP-adres, blijft behouden.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-174">Preserves the IP address.</span></span> |
    | <span data-ttu-id="1f9aa-175">Niet verwijderen</span><span class="sxs-lookup"><span data-stu-id="1f9aa-175">Do Not Delete</span></span> |<span data-ttu-id="1f9aa-176">Indien waar, de implementatie van een bestaande niet-verwante niet overschrijven (upgrade is toegestaan).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-176">If true, do not overwrite an existing unrelated deployment (upgrade is allowed).</span></span> |
    | <span data-ttu-id="1f9aa-177">Pad naar de implementatie-instellingen</span><span class="sxs-lookup"><span data-stu-id="1f9aa-177">Path to Deployment Settings</span></span> |<span data-ttu-id="1f9aa-178">Het pad naar het bestand .pubxml voor een web-app, ten opzichte van de hoofdmap van de opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-178">The path to your .pubxml file for a web app, relative to the root folder of the repo.</span></span> <span data-ttu-id="1f9aa-179">Genegeerd voor cloud-services.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-179">Ignored for cloud services.</span></span> |
    | <span data-ttu-id="1f9aa-180">SharePoint-omgeving voor implementatie</span><span class="sxs-lookup"><span data-stu-id="1f9aa-180">Sharepoint Deployment Environment</span></span> |<span data-ttu-id="1f9aa-181">Hetzelfde als de naam van de service.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-181">The same as the service name.</span></span> |
    | <span data-ttu-id="1f9aa-182">Azure-implementatie-omgeving</span><span class="sxs-lookup"><span data-stu-id="1f9aa-182">Azure Deployment Environment</span></span> |<span data-ttu-id="1f9aa-183">De web-app of cloud servicenaam.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-183">The web app or cloud service name.</span></span> |
14. <span data-ttu-id="1f9aa-184">Op dit tijdstip moet uw build worden voltooid.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-184">By this time, your build should be completed successfully.</span></span>
    
     ![][28]
15. <span data-ttu-id="1f9aa-185">Als u dubbelklikt op de naam van de build, ziet u Visual Studio een **bouwen samenvatting**, met inbegrip van de testresultaten van eenheid Testprojecten die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-185">If you double-click the build name, Visual Studio shows a **Build Summary**, including any test results from associated unit test projects.</span></span>
    
     ![][29]
16. <span data-ttu-id="1f9aa-186">In de [klassieke Azure-portal](http://go.microsoft.com/fwlink/?LinkID=213885), kunt u de gekoppelde implementatie bekijken op de **implementaties** tabblad wanneer de faseringsomgeving is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-186">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885), you can view the associated deployment on the **Deployments** tab when the staging environment is selected.</span></span>
    
     ![][30]
17. <span data-ttu-id="1f9aa-187">Blader naar de URL van uw site.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-187">Browse to your site's URL.</span></span> <span data-ttu-id="1f9aa-188">Voor een web-app, kies de **Bladeren** knop in de portal.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-188">For a web app, just choose  the **Browse** button in the portal.</span></span> <span data-ttu-id="1f9aa-189">Voor een cloudservice, kiest u de URL in de **snel in één oogopslag** sectie van de **Dashboard** pagina waarin de Staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-189">For a cloud service, choose the URL in the **Quick Glance** section of the **Dashboard** page that shows the Staging environment.</span></span>
    
    <span data-ttu-id="1f9aa-190">Implementaties van continue integratie voor cloud-services worden gepubliceerd op de faseringsomgeving standaard.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-190">Deployments from continuous integration for cloud services are published to the Staging environment by default.</span></span> <span data-ttu-id="1f9aa-191">U kunt dit wijzigen door in te stellen de **alternatieve Cloudserviceomgeving** eigenschap **productie**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-191">You can change this by setting the **Alternate Cloud Service Environment** property to **Production**.</span></span> <span data-ttu-id="1f9aa-192">Hier is waarbij de URL van de site op de dashboardpagina van de cloudservice.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-192">Here's where the site URL is on the cloud service's dashboard page.</span></span>
    
    ![][31]
    
    <span data-ttu-id="1f9aa-193">Een nieuw browsertabblad geopend om uw actieve site weer te geven.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-193">A new browser tab will open to reveal your running site.</span></span>
    
    ![][32]
18. <span data-ttu-id="1f9aa-194">Als u andere wijzigingen aan uw project aanbrengt, u trigger meer maakt en u kunt meerdere implementaties wordt verzameld.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-194">If you make other changes to your project, you trigger more builds, and you will accumulate multiple deployments.</span></span> <span data-ttu-id="1f9aa-195">De meest recente versie is gemarkeerd als actief.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-195">The latest one is marked as Active.</span></span>
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a><span data-ttu-id="1f9aa-196">5: een eerdere build implementeren</span><span class="sxs-lookup"><span data-stu-id="1f9aa-196">5: Redeploy an earlier build</span></span>
<span data-ttu-id="1f9aa-197">Deze stap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-197">This step is optional.</span></span> <span data-ttu-id="1f9aa-198">In de klassieke Azure portal, kiest u een eerdere implementatie en kies **implementeren** terugspoelen van uw site een eerdere in te checken.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-198">In the Azure classic portal, choose an earlier deployment and choose **Redeploy** to rewind your site to an earlier check-in.</span></span> <span data-ttu-id="1f9aa-199">Houd er rekening mee dat dit een nieuwe build in TFS activeren en maken van een nieuwe vermelding in de geschiedenis van uw implementatie.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-199">Note that this will trigger a new build in TFS and create a new entry in your deployment history.</span></span>

![][34]

## <a name="6-change-the-production-deployment"></a><span data-ttu-id="1f9aa-200">6: de productie-implementatie wijzigen</span><span class="sxs-lookup"><span data-stu-id="1f9aa-200">6: Change the Production deployment</span></span>
<span data-ttu-id="1f9aa-201">Wanneer u klaar bent, kunt u de faseringsomgeving naar de productieomgeving promoveren kiezen **wisselen** in de klassieke Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-201">When you are ready, you can promote the Staging environment to the Production environment by choosing **Swap** in the Azure classic portal.</span></span> <span data-ttu-id="1f9aa-202">De zojuist geïmplementeerde faseringsomgeving wordt gepromoveerd voor productie en de vorige productie-omgeving, indien aanwezig, wordt een Staging-omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-202">The newly deployed Staging environment is promoted to Production, and the previous Production environment, if any, becomes a Staging environment.</span></span> <span data-ttu-id="1f9aa-203">De actieve implementatie mogelijk anders voor de productie- en Faseringsomgevingen, maar de geschiedenis van de implementatie van recente builds is hetzelfde, ongeacht de omgeving.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-203">The Active deployment may be different for the Production and Staging environments, but the deployment history of recent builds is the same regardless of environment.</span></span>

![][35]

## <a name="7-deploy-from-a-working-branch"></a><span data-ttu-id="1f9aa-204">7: implementeren vanuit een werkvertakking.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-204">7: Deploy from a working branch.</span></span>
<span data-ttu-id="1f9aa-205">Wanneer u met Git, meestal wijzigingen aanbrengt in een werkvertakking en integreren in de hoofdvertakking wanneer de ontwikkeling van een voltooide status bereikt.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-205">When you use Git, you usually make changes in a working branch and integrate into the master branch when your development reaches a finished state.</span></span> <span data-ttu-id="1f9aa-206">Tijdens de ontwikkelingsfase van een project, moet u het bouwen en implementeren van de werkvertakking in Azure.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-206">During the development phase of a project, you'll want to build and deploy the working branch to Azure.</span></span>

1. <span data-ttu-id="1f9aa-207">In **Team Explorer**, kies de **Start** knop en kies vervolgens de **vertakkingen** knop.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-207">In **Team Explorer**, choose the **Home** button and then choose the **Branches** button.</span></span>
   
    ![][40]
2. <span data-ttu-id="1f9aa-208">Kies de **nieuwe vertakking** koppeling.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-208">Choose the **New Branch** link.</span></span>
   
    ![][41]
3. <span data-ttu-id="1f9aa-209">Voer de naam van de vertakking, zoals 'werken', en kies **vertakking maken**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-209">Enter the name of the branch, such as "working," and choose **Create Branch**.</span></span> <span data-ttu-id="1f9aa-210">Hiermee maakt u een nieuwe lokale vertakking.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-210">This creates a new local branch.</span></span>
   
    ![][42]
4. <span data-ttu-id="1f9aa-211">Publiceer de vertakking.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-211">Publish the branch.</span></span> <span data-ttu-id="1f9aa-212">Kies de naam van de vertakking in **niet gepubliceerd vertakkingen**, en kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-212">Choose the branch name in **Unpublished branches**, and choose **Publish**.</span></span>
   
    ![][44]
5. <span data-ttu-id="1f9aa-213">Alleen de wijzigingen naar de hoofdvertakking activeren standaard een continue build.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-213">By default, only changes to the master branch trigger a continuous build.</span></span> <span data-ttu-id="1f9aa-214">Als u continue build voor een werkvertakking instelt, kies de **Builds** pagina in **Team Explorer**, en kies **bouwen definitie bewerken**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-214">To set up continuous build for a working branch, choose the **Builds** page in **Team Explorer**, and choose **Edit Build Definition**.</span></span>
6. <span data-ttu-id="1f9aa-215">Open de **broninstellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-215">Open the **Source Settings** tab.</span></span> <span data-ttu-id="1f9aa-216">Onder **bewaakt vertakkingen voor continue integratie en build**, kies **Klik hier om een nieuwe rij toegevoegd**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-216">Under **Monitored branches for continuous integration and build**, choose **Click here to add a new row**.</span></span>
   
    ![][47]
7. <span data-ttu-id="1f9aa-217">Geef de vertakking die u hebt gemaakt, zoals koppen refs werkende.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-217">Specify the branch you created, such as refs/heads/working.</span></span>
   
    ![][48]
8. <span data-ttu-id="1f9aa-218">Een wijziging aanbrengt in de code en kies vervolgens opent u het snelmenu voor het gewijzigde bestand **doorvoeren**.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-218">Make a change in the code, open the shortcut menu for the changed file, and then choose **Commit**.</span></span>
   
    ![][43]
9. <span data-ttu-id="1f9aa-219">Kies de **niet-gesynchroniseerde doorvoeracties** koppeling en kies de **Sync** knop of de **Push** koppeling kopiëren van de wijzigingen naar de kopie van de werkvertakking in Visual Studio Team Services.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-219">Choose the **Unsynced Commits** link, and choose  the **Sync** button or the **Push** link to copy the changes to the copy of the working branch in Visual Studio Team Services.</span></span>
   
   ![][45]
10. <span data-ttu-id="1f9aa-220">Navigeer naar de **Builds** bekijken en de build die zojuist is geactiveerd voor de werkvertakking niet vinden.</span><span class="sxs-lookup"><span data-stu-id="1f9aa-220">Navigate to the **Builds** view and find the build that just got triggered for the working branch.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1f9aa-221">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1f9aa-221">Next steps</span></span>
<span data-ttu-id="1f9aa-222">Zie voor meer tips over het gebruik van Git met Visual Studio Team Services meer [ontwikkelen en delen van uw code in Git met Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) en Zie voor meer informatie over het gebruik van een Git-opslagplaats die niet wordt beheerd door Visual Studio Team Services te publiceren naar Azure [continue implementatie naar Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-222">To learn more tips on using Git with Visual Studio Team Services, see [Develop and share your code in Git using Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) and for information about using a Git repository that's not managed by Visual Studio Team Services to publish to Azure, see [Continuous Deployment to Azure App Service](../app-service-web/app-service-continuous-deployment.md).</span></span> <span data-ttu-id="1f9aa-223">Zie voor meer informatie over Visual Studio Team Services [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span><span class="sxs-lookup"><span data-stu-id="1f9aa-223">For more information on Visual Studio Team Services, see [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).</span></span>

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
