---
title: aaaNode.js Getting Started Guide | Microsoft Docs
description: Ontdek hoe toocreate een eenvoudige Node.js-webtoepassing en tooan Azure cloudservice implementeren.
services: cloud-services
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 50951a87-fed4-48e0-bcfa-453b9e50452e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 08/17/2017
ms.author: tarcher
ms.openlocfilehash: 22945bfcc1b0e5da2a2d37dc5cc86be013cc0b5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-a-nodejs-application-tooan-azure-cloud-service"></a><span data-ttu-id="9dbce-103">Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="9dbce-103">Build and deploy a Node.js application tooan Azure Cloud Service</span></span>

<span data-ttu-id="9dbce-104">Deze zelfstudie laat zien hoe een eenvoudige Node.js toocreate toepassing die in een Azure Cloud Service wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9dbce-104">This tutorial shows how toocreate a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="9dbce-105">Cloudservices zijn Hallo bouwstenen van schaalbare cloudtoepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbce-105">Cloud Services are hello building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="9dbce-106">Ze staan Hallo scheiding en onafhankelijke management en scale-out van de front-end en back-end-onderdelen van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9dbce-106">They allow hello separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="9dbce-107">Cloud Services bieden een robuuste toegewezen virtuele machine voor het op betrouwbare wijze hosten van elke rol.</span><span class="sxs-lookup"><span data-stu-id="9dbce-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="9dbce-108">Zie voor meer informatie over Cloudservices en hoe ze zich verhouden tooAzure Websites en virtuele machines [vergelijking van Azure Websites, Cloudservices en virtuele Machines].</span><span class="sxs-lookup"><span data-stu-id="9dbce-108">For more information on Cloud Services, and how they compare tooAzure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="9dbce-109">Zoek toobuild een ongecompliceerde website?</span><span class="sxs-lookup"><span data-stu-id="9dbce-109">Looking toobuild a simple website?</span></span> <span data-ttu-id="9dbce-110">Als uw scenario alleen een ongecompliceerde website-front-end omvat, kunt u overwegen [een eenvoudige web-app-functie te gebruiken].</span><span class="sxs-lookup"><span data-stu-id="9dbce-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="9dbce-111">U kunt eenvoudig tooa Cloudservice bijwerken naarmate uw web-app groeit en uw vereisten veranderen.</span><span class="sxs-lookup"><span data-stu-id="9dbce-111">You can easily upgrade tooa Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="9dbce-112">In deze zelfstudie maakt u een eenvoudige webtoepassing gehost binnen een webrol.</span><span class="sxs-lookup"><span data-stu-id="9dbce-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="9dbce-113">U wordt Hallo compute-emulator tootest lokaal uw toepassing gebruiken, en vervolgens implementeren met behulp van PowerShell-opdrachtregelprogramma's.</span><span class="sxs-lookup"><span data-stu-id="9dbce-113">You will use hello compute emulator tootest your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="9dbce-114">Hallo-toepassing is een eenvoudige 'Hallo wereld'-toepassing:</span><span class="sxs-lookup"><span data-stu-id="9dbce-114">hello application is a simple "hello world" application:</span></span>

![Een webbrowser waarin Hallo Hallo wereld-webpagina][A web browser displaying hello Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="9dbce-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9dbce-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="9dbce-117">In deze zelfstudie wordt Azure PowerShell gebruikt waarvoor Windows is vereist.</span><span class="sxs-lookup"><span data-stu-id="9dbce-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="9dbce-118">Installeer en configureer [Azure Powershell].</span><span class="sxs-lookup"><span data-stu-id="9dbce-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="9dbce-119">Download en installeer Hallo [Azure SDK voor .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="9dbce-119">Download and install hello [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="9dbce-120">Installeer in Hallo setup, selecteren:</span><span class="sxs-lookup"><span data-stu-id="9dbce-120">In hello install setup, select:</span></span>
  * <span data-ttu-id="9dbce-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="9dbce-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="9dbce-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="9dbce-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="9dbce-123">Een Azure Cloud Service-project maken</span><span class="sxs-lookup"><span data-stu-id="9dbce-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="9dbce-124">Voer Hallo taken toocreate een nieuw Azure Cloud Service-project, samen met Node.js-basisstructuur volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbce-124">Perform hello following tasks toocreate a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="9dbce-125">Uitvoeren **Windows PowerShell** als Administrator; van Hallo **startmenu** of **startscherm**, zoeken naar **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9dbce-125">Run **Windows PowerShell** as Administrator; from hello **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="9dbce-126">[Koppel PowerShell] tooyour abonnement.</span><span class="sxs-lookup"><span data-stu-id="9dbce-126">[Connect PowerShell] tooyour subscription.</span></span>
3. <span data-ttu-id="9dbce-127">Voer Hallo PowerShell cmdlet toocreate toocreate Hallo project te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbce-127">Enter hello following PowerShell cmdlet toocreate toocreate hello project:</span></span>

        New-AzureServiceProject helloworld

    ![Hallo resultaat van de helloworld-opdracht Hallo New-AzureService][hello result of hello New-AzureService helloworld command]

    <span data-ttu-id="9dbce-129">Hallo **New-AzureServiceProject** cmdlet genereert een basisstructuur voor het publiceren van een Node.js-toepassing tooa Service in de Cloud.</span><span class="sxs-lookup"><span data-stu-id="9dbce-129">hello **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application tooa Cloud Service.</span></span> <span data-ttu-id="9dbce-130">Deze bevat configuratiebestanden die nodig zijn voor publicatie tooAzure.</span><span class="sxs-lookup"><span data-stu-id="9dbce-130">It contains configuration files necessary for publishing tooAzure.</span></span> <span data-ttu-id="9dbce-131">Hallo cmdlet wijzigt ook uw werkmap voor het toohello van directory voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="9dbce-131">hello cmdlet also changes your working directory toohello directory for hello service.</span></span>

    <span data-ttu-id="9dbce-132">Hallo-cmdlet maakt Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="9dbce-132">hello cmdlet creates hello following files:</span></span>

   * <span data-ttu-id="9dbce-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** en **ServiceDefinition.csdef**: Azure-specifieke bestanden die nodig zijn voor het publiceren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="9dbce-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="9dbce-134">Zie [Overzicht van het maken van een gehoste service voor Azure].</span><span class="sxs-lookup"><span data-stu-id="9dbce-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="9dbce-135">**deploymentSettings.json**: lokale instellingen die worden gebruikt door hello Azure PowerShell-cmdlets voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="9dbce-135">**deploymentSettings.json**: Stores local settings that are used by hello Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="9dbce-136">Voer Hallo opdracht tooadd een nieuwe Webrol te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbce-136">Enter hello following command tooadd a new web role:</span></span>

       Add-AzureNodeWebRole

   ![Hallo-uitvoer van de opdracht Add-AzureNodeWebRole Hallo][hello output of hello Add-AzureNodeWebRole command]

   <span data-ttu-id="9dbce-138">Hallo **Add-AzureNodeWebRole** cmdlet maakt een eenvoudige Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="9dbce-138">hello **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="9dbce-139">Hallo ook gewijzigd **.csfg** en **csdef** tooadd configuratie-items voor de nieuwe rol Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="9dbce-139">It also modifies hello **.csfg** and **.csdef** files tooadd configuration entries for hello new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="9dbce-140">Als u geen rolnaam opgeeft, wordt een standaardnaam gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9dbce-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="9dbce-141">U kunt een naam opgeven als eerste Hallo-cmdlet-parameter:`Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="9dbce-141">You can provide a name as hello first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="9dbce-142">Hallo Node.js-app is gedefinieerd in Hallo bestand **server.js**, dat zich bevindt in de directory voor de Webrol Hallo Hallo (**WebRole1** standaard).</span><span class="sxs-lookup"><span data-stu-id="9dbce-142">hello Node.js app is defined in hello file **server.js**, located in hello directory for hello web role (**WebRole1** by default).</span></span> <span data-ttu-id="9dbce-143">Dit is Hallo code:</span><span class="sxs-lookup"><span data-stu-id="9dbce-143">Here is hello code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="9dbce-144">Deze code is in wezen Hallo hetzelfde als 'Hallo wereld' Hallo steekproef op Hallo [nodejs.org] website, behalve het Hallo-poortnummer dat is toegewezen door de cloudomgeving Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9dbce-144">This code is essentially hello same as hello "Hello World" sample on hello [nodejs.org] website, except it uses hello port number assigned by hello cloud environment.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="9dbce-145">Hallo toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="9dbce-145">Deploy hello application tooAzure</span></span>

> [!NOTE]
> <span data-ttu-id="9dbce-146">toocomplete in deze zelfstudie, moet u een Azure-account.</span><span class="sxs-lookup"><span data-stu-id="9dbce-146">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="9dbce-147">U kunt [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) of [u aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="9dbce-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-hello-azure-publishing-settings"></a><span data-ttu-id="9dbce-148">Hello Azure downloaden instellingen publiceren</span><span class="sxs-lookup"><span data-stu-id="9dbce-148">Download hello Azure publishing settings</span></span>
<span data-ttu-id="9dbce-149">toodeploy uw tooAzure toepassing moet u eerst Hallo publicatie-instellingen voor uw Azure-abonnement downloaden.</span><span class="sxs-lookup"><span data-stu-id="9dbce-149">toodeploy your application tooAzure, you must first download hello publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="9dbce-150">Voer hello Azure PowerShell-cmdlet te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbce-150">Run hello following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="9dbce-151">Hiermee worden gebruikt. uw browser toonavigate toohello publiceren downloadpagina van instellingen.</span><span class="sxs-lookup"><span data-stu-id="9dbce-151">This will use your browser toonavigate toohello publish settings download page.</span></span> <span data-ttu-id="9dbce-152">Hebt u mogelijk na vragen aan gebruiker toolog met een Microsoft-Account.</span><span class="sxs-lookup"><span data-stu-id="9dbce-152">You may be prompted toolog in with a Microsoft Account.</span></span> <span data-ttu-id="9dbce-153">Als dit het geval is, moet u Hallo-account die is gekoppeld aan uw Azure-abonnement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9dbce-153">If so, use hello account associated with your Azure subscription.</span></span>

   <span data-ttu-id="9dbce-154">Hallo gedownload profiel tooa bestandslocatie u gemakkelijk bij kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="9dbce-154">Save hello downloaded profile tooa file location you can easily access.</span></span>
2. <span data-ttu-id="9dbce-155">Voer de volgende cmdlet tooimport Hallo publiceren profiel dat u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="9dbce-155">Run following cmdlet tooimport hello publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path toofile]

    > [!NOTE]
    > <span data-ttu-id="9dbce-156">Na het importeren van Hallo publicatie-instellingen, overweeg dan verwijderen Hallo gedownloade .publishSettings-bestand, omdat dit informatie bevat die iemand zou kunnen tooaccess uw account.</span><span class="sxs-lookup"><span data-stu-id="9dbce-156">After importing hello publish settings, consider deleting hello downloaded .publishSettings file, because it contains information that could allow someone tooaccess your account.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="9dbce-157">Hallo toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="9dbce-157">Publish hello application</span></span>
<span data-ttu-id="9dbce-158">toopublish hello volgende opdrachten uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9dbce-158">toopublish, run hello following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="9dbce-159">**-ServiceName** Hallo-naam voor het Hallo-implementatie.</span><span class="sxs-lookup"><span data-stu-id="9dbce-159">**-ServiceName** specifies hello name for hello deployment.</span></span> <span data-ttu-id="9dbce-160">Dit moet een unieke naam, anders Hallo publicatieproces zal mislukken.</span><span class="sxs-lookup"><span data-stu-id="9dbce-160">This must be a unique name, otherwise hello publish process will fail.</span></span> <span data-ttu-id="9dbce-161">Hallo **Get-Date** opdracht voegt een datum/tijd-tekenreeks die Hallo naam uniek te maken.</span><span class="sxs-lookup"><span data-stu-id="9dbce-161">hello **Get-Date** command tacks on a date/time string that should make hello name unique.</span></span>
* <span data-ttu-id="9dbce-162">**-Locatie** geeft Hallo datacenter waarin de toepassing hello zal worden gehost in.</span><span class="sxs-lookup"><span data-stu-id="9dbce-162">**-Location** specifies hello datacenter that hello application will be hosted in.</span></span> <span data-ttu-id="9dbce-163">een lijst van beschikbare datacenters, gebruik Hallo toosee **Get-AzureLocation** cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9dbce-163">toosee a list of available datacenters, use hello **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="9dbce-164">**-Launch** opent een browservenster en gaat u toohello gehoste service nadat de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9dbce-164">**-Launch** opens a browser window and navigates toohello hosted service after deployment has completed.</span></span>

<span data-ttu-id="9dbce-165">Nadat de publicatie is uitgevoerd, ziet u een reactie vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="9dbce-165">After publishing succeeds, you will see a response similar toohello following:</span></span>

![Hallo-uitvoer van Hallo opdracht Publish-AzureService][hello output of hello Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="9dbce-167">Het kan enkele minuten duren voordat Hallo toepassing toodeploy en beschikbaar is wanneer de eerste keer wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="9dbce-167">It can take several minutes for hello application toodeploy and become available when first published.</span></span>

<span data-ttu-id="9dbce-168">Zodra het Hallo-implementatie is voltooid, wordt een browservenster open en navigeer toohello-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="9dbce-168">Once hello deployment has completed, a browser window will open and navigate toohello cloud service.</span></span>

![Een browservenster met Hallo Hallo wereld-pagina. Hallo URL geeft Hallo pagina wordt gehost in Azure.][A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]

<span data-ttu-id="9dbce-170">Uw toepassing wordt nu uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="9dbce-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="9dbce-171">Hallo **Publish-AzureServiceProject** cmdlet voert Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dbce-171">hello **Publish-AzureServiceProject** cmdlet performs hello following steps:</span></span>

1. <span data-ttu-id="9dbce-172">Hiermee maakt u een pakket toodeploy.</span><span class="sxs-lookup"><span data-stu-id="9dbce-172">Creates a package toodeploy.</span></span> <span data-ttu-id="9dbce-173">Hallo-pakket bevat alle Hallo-bestanden in de toepassingsmap.</span><span class="sxs-lookup"><span data-stu-id="9dbce-173">hello package contains all hello files in your application folder.</span></span>
2. <span data-ttu-id="9dbce-174">Er wordt een nieuw **opslagaccount** gemaakt, als dit nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="9dbce-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="9dbce-175">gebruikte toostore Hallo toepassingspakket is Hello Azure storage-account tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="9dbce-175">hello Azure storage account is used toostore hello application package during deployment.</span></span> <span data-ttu-id="9dbce-176">Nadat de implementatie is voltooid, kunt u veilig Hallo storage-account verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9dbce-176">You can safely delete hello storage account after deployment is done.</span></span>
3. <span data-ttu-id="9dbce-177">Er wordt een nieuwe **cloudservice** gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="9dbce-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="9dbce-178">Een **cloudservice** Hallo container waarin uw toepassing wordt gehost wanneer deze geïmplementeerde tooAzure is.</span><span class="sxs-lookup"><span data-stu-id="9dbce-178">A **cloud service** is hello container in which your application is hosted when it is deployed tooAzure.</span></span> <span data-ttu-id="9dbce-179">Zie [Overzicht van het maken van een gehoste service voor Azure].</span><span class="sxs-lookup"><span data-stu-id="9dbce-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="9dbce-180">Hallo implementatie pakket tooAzure publiceert.</span><span class="sxs-lookup"><span data-stu-id="9dbce-180">Publishes hello deployment package tooAzure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="9dbce-181">De toepassing stoppen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="9dbce-181">Stopping and deleting your application</span></span>
<span data-ttu-id="9dbce-182">Na implementatie van uw toepassing, kunt u toodisable zodat u extra kosten kunt voorkomen.</span><span class="sxs-lookup"><span data-stu-id="9dbce-182">After deploying your application, you may want toodisable it so you can avoid extra costs.</span></span> <span data-ttu-id="9dbce-183">Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="9dbce-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="9dbce-184">Er wordt servertijd verbruikt zodra uw toepassing is geïmplementeerd, zelfs als Hallo exemplaren niet worden uitgevoerd en met de status Hallo gestopt.</span><span class="sxs-lookup"><span data-stu-id="9dbce-184">Server time is consumed once your application is deployed, even if hello instances are not running and are in hello stopped state.</span></span>

1. <span data-ttu-id="9dbce-185">In Hallo Windows PowerShell-venster stopt Hallo service-implementatie gemaakt in de vorige sectie Hallo Hello volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dbce-185">In hello Windows PowerShell window, stop hello service deployment created in hello previous section with hello following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="9dbce-186">Hallo-service wordt gestopt, kan dit enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="9dbce-186">Stopping hello service may take several minutes.</span></span> <span data-ttu-id="9dbce-187">Wanneer het Hallo-service wordt gestopt, krijgt u een bericht weergegeven dat aangeeft dat deze is gestopt.</span><span class="sxs-lookup"><span data-stu-id="9dbce-187">When hello service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![Hallo-status van de opdracht Hallo Stop-AzureService][hello status of hello Stop-AzureService command]
2. <span data-ttu-id="9dbce-189">toodelete hello service aanroep Hallo volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9dbce-189">toodelete hello service, call hello following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="9dbce-190">Wanneer u wordt gevraagd, typt u **Y** toodelete Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="9dbce-190">When prompted, enter **Y** toodelete hello service.</span></span>

   <span data-ttu-id="9dbce-191">Verwijderen van Hallo-service kan enkele minuten duren.</span><span class="sxs-lookup"><span data-stu-id="9dbce-191">Deleting hello service may take several minutes.</span></span> <span data-ttu-id="9dbce-192">U ontvangt een bericht weergegeven dat aangeeft dat het Hallo-service is verwijderd nadat het Hallo-service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9dbce-192">After hello service has been deleted you receive a message indicating that hello service was deleted.</span></span>

   ![Hallo-status van de opdracht Hallo Remove-AzureService][hello status of hello Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="9dbce-194">Hallo-service verwijderen Hallo storage-account dat is gemaakt tijdens het Hallo-service is in eerste instantie gepubliceerd niet verwijderd en u blijft toobe kosten in rekening gebracht voor opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9dbce-194">Deleting hello service does not delete hello storage account that was created when hello service was initially published, and you will continue toobe billed for storage used.</span></span> <span data-ttu-id="9dbce-195">Als niets anders Hallo opslag wordt gebruikt, kunt u toodelete deze.</span><span class="sxs-lookup"><span data-stu-id="9dbce-195">If nothing else is using hello storage, you may want toodelete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9dbce-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9dbce-196">Next steps</span></span>
<span data-ttu-id="9dbce-197">Zie voor meer informatie, Hallo [Node.js Developer Center].</span><span class="sxs-lookup"><span data-stu-id="9dbce-197">For more information, see hello [Node.js Developer Center].</span></span>

<!-- URL List -->

[vergelijking van Azure Websites, Cloudservices en virtuele Machines]: ../app-service-web/choose-web-site-cloud-service-vm.md
[een eenvoudige web-app-functie te gebruiken]: ../app-service-web/app-service-web-get-started-nodejs.md
[Azure Powershell]: /powershell/azureps-cmdlets-docs
[Azure SDK voor .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178
[Koppel PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect
[nodejs.org]: http://nodejs.org/
[Overzicht van het maken van een gehoste service voor Azure]: https://azure.microsoft.com/documentation/services/cloud-services/
[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/

<!-- IMG List -->

[hello result of hello New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[hello output of hello Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying hello Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[hello output of hello Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying hello hello world page; hello URL indicates hello page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[hello status of hello Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[hello status of hello Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
