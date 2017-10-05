---
title: Instructiehandleiding voor Node.js | Microsoft Docs
description: Informatie over het maken van een eenvoudige Node.js-webtoepassing en het implementeren van deze toepassing in een cloudservice van Azure.
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
ms.openlocfilehash: 980643f35c78bbae7b1b12336331ca15ad4fb89b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="build-and-deploy-a-nodejs-application-to-an-azure-cloud-service"></a><span data-ttu-id="63c9e-103">Een Node.js-toepassing maken en implementeren in een Azure Cloud Service</span><span class="sxs-lookup"><span data-stu-id="63c9e-103">Build and deploy a Node.js application to an Azure Cloud Service</span></span>

<span data-ttu-id="63c9e-104">In deze zelfstudie kunt u zien hoe u een eenvoudige Node.js-toepassing kunt maken die wordt uitgevoerd in een Azure Cloud Service.</span><span class="sxs-lookup"><span data-stu-id="63c9e-104">This tutorial shows how to create a simple Node.js application running in an Azure Cloud Service.</span></span> <span data-ttu-id="63c9e-105">Cloud Services vormen de bouwstenen van schaalbare cloudtoepassingen in Azure.</span><span class="sxs-lookup"><span data-stu-id="63c9e-105">Cloud Services are the building blocks of scalable cloud applications in Azure.</span></span> <span data-ttu-id="63c9e-106">Deze bieden de mogelijkheid om de front-end- en back-end-onderdelen van uw toepassing te scheiden en onafhankelijk van elkaar te beheren en uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="63c9e-106">They allow the separation and independent management and scale-out of front-end and back-end components of your application.</span></span>  <span data-ttu-id="63c9e-107">Cloud Services bieden een robuuste toegewezen virtuele machine voor het op betrouwbare wijze hosten van elke rol.</span><span class="sxs-lookup"><span data-stu-id="63c9e-107">Cloud Services provide a robust dedicated virtual machine for hosting each role reliably.</span></span>

<span data-ttu-id="63c9e-108">Zie [Vergelijking van Azure Websites, Cloud Services en Virtual Machines] voor meer informatie over Cloud Services en hoe deze zich verhouden tot Azure Websites en Virtual Machines.</span><span class="sxs-lookup"><span data-stu-id="63c9e-108">For more information on Cloud Services, and how they compare to Azure Websites and Virtual machines, see [Azure Websites, Cloud Services and Virtual Machines comparison].</span></span>

> [!TIP]
> <span data-ttu-id="63c9e-109">Wilt u een eenvoudige website bouwen?</span><span class="sxs-lookup"><span data-stu-id="63c9e-109">Looking to build a simple website?</span></span> <span data-ttu-id="63c9e-110">Als uw scenario alleen een ongecompliceerde website-front-end omvat, kunt u overwegen [een eenvoudige web-app-functie te gebruiken].</span><span class="sxs-lookup"><span data-stu-id="63c9e-110">If your scenario involves just a simple website front-end, consider [using a lightweight web app].</span></span> <span data-ttu-id="63c9e-111">U kunt vervolgens gemakkelijk upgraden naar een cloudservice naarmate uw web-app groeit en uw vereisten veranderen.</span><span class="sxs-lookup"><span data-stu-id="63c9e-111">You can easily upgrade to a Cloud Service as your web app grows and your requirements change.</span></span>

<span data-ttu-id="63c9e-112">In deze zelfstudie maakt u een eenvoudige webtoepassing gehost binnen een webrol.</span><span class="sxs-lookup"><span data-stu-id="63c9e-112">By following this tutorial, you will build a simple web application hosted inside a web role.</span></span> <span data-ttu-id="63c9e-113">U gebruikt de rekenemulator om uw toepassing lokaal te testen, en vervolgens implementeert u de toepassing met behulp van PowerShell- opdrachtregelprogramma's.</span><span class="sxs-lookup"><span data-stu-id="63c9e-113">You will use the compute emulator to test your application locally, then deploy it using PowerShell command-line tools.</span></span>

<span data-ttu-id="63c9e-114">De toepassing is een eenvoudige 'Hallo wereld'-toepassing:</span><span class="sxs-lookup"><span data-stu-id="63c9e-114">The application is a simple "hello world" application:</span></span>

![Een webbrowser waarin de webpagina 'Hallo wereld' wordt weergegeven][A web browser displaying the Hello World web page]

## <a name="prerequisites"></a><span data-ttu-id="63c9e-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="63c9e-116">Prerequisites</span></span>
> [!NOTE]
> <span data-ttu-id="63c9e-117">In deze zelfstudie wordt Azure PowerShell gebruikt waarvoor Windows is vereist.</span><span class="sxs-lookup"><span data-stu-id="63c9e-117">This tutorial uses Azure PowerShell, which requires Windows.</span></span>

* <span data-ttu-id="63c9e-118">Installeer en configureer [Azure Powershell].</span><span class="sxs-lookup"><span data-stu-id="63c9e-118">Install and configure [Azure Powershell].</span></span>
* <span data-ttu-id="63c9e-119">Download en installeer [Azure SDK voor .NET 2.7].</span><span class="sxs-lookup"><span data-stu-id="63c9e-119">Download and install the [Azure SDK for .NET 2.7].</span></span> <span data-ttu-id="63c9e-120">Selecteer in de installatie-instellingen:</span><span class="sxs-lookup"><span data-stu-id="63c9e-120">In the install setup, select:</span></span>
  * <span data-ttu-id="63c9e-121">MicrosoftAzureAuthoringTools</span><span class="sxs-lookup"><span data-stu-id="63c9e-121">MicrosoftAzureAuthoringTools</span></span>
  * <span data-ttu-id="63c9e-122">MicrosoftAzureComputeEmulator</span><span class="sxs-lookup"><span data-stu-id="63c9e-122">MicrosoftAzureComputeEmulator</span></span>

## <a name="create-an-azure-cloud-service-project"></a><span data-ttu-id="63c9e-123">Een Azure Cloud Service-project maken</span><span class="sxs-lookup"><span data-stu-id="63c9e-123">Create an Azure Cloud Service project</span></span>
<span data-ttu-id="63c9e-124">Voer de volgende taken uit om een nieuw Azure Cloud Services-project te maken, samen met een Node.js-basisstructuur:</span><span class="sxs-lookup"><span data-stu-id="63c9e-124">Perform the following tasks to create a new Azure Cloud Service project, along with basic Node.js scaffolding:</span></span>

1. <span data-ttu-id="63c9e-125">Voer **Windows PowerShell** als administrator uit. Zoek in het **Startmenu** of **Startscherm** naar **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="63c9e-125">Run **Windows PowerShell** as Administrator; from the **Start Menu** or **Start Screen**, search for **Windows PowerShell**.</span></span>
2. <span data-ttu-id="63c9e-126">[Koppel PowerShell] aan uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="63c9e-126">[Connect PowerShell] to your subscription.</span></span>
3. <span data-ttu-id="63c9e-127">Voer de volgende PowerShell-cmdlet in om het project te maken:</span><span class="sxs-lookup"><span data-stu-id="63c9e-127">Enter the following PowerShell cmdlet to create to create the project:</span></span>

        New-AzureServiceProject helloworld

    ![The result of the New-AzureService helloworld command][The result of the New-AzureService helloworld command]

    <span data-ttu-id="63c9e-129">De **New-AzureServiceProject**-cmdlet genereert een basisstructuur voor het publiceren van een Node.js-toepassing naar een cloudservice.</span><span class="sxs-lookup"><span data-stu-id="63c9e-129">The **New-AzureServiceProject** cmdlet generates a basic structure for publishing a Node.js application to a Cloud Service.</span></span> <span data-ttu-id="63c9e-130">Deze bevat configuratiebestanden die nodig zijn voor publicatie naar Azure.</span><span class="sxs-lookup"><span data-stu-id="63c9e-130">It contains configuration files necessary for publishing to Azure.</span></span> <span data-ttu-id="63c9e-131">De cmdlet wijzigt ook uw werkmap naar de map voor de service.</span><span class="sxs-lookup"><span data-stu-id="63c9e-131">The cmdlet also changes your working directory to the directory for the service.</span></span>

    <span data-ttu-id="63c9e-132">De cmdlet maakt de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="63c9e-132">The cmdlet creates the following files:</span></span>

   * <span data-ttu-id="63c9e-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** en **ServiceDefinition.csdef**: Azure-specifieke bestanden die nodig zijn voor het publiceren van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="63c9e-133">**ServiceConfiguration.Cloud.cscfg**, **ServiceConfiguration.Local.cscfg** and **ServiceDefinition.csdef**: Azure-specific files necessary for publishing your application.</span></span> <span data-ttu-id="63c9e-134">Zie [Overzicht van het maken van een gehoste service voor Azure].</span><span class="sxs-lookup"><span data-stu-id="63c9e-134">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
   * <span data-ttu-id="63c9e-135">**deploymentSettings.json**: lokale instellingen die worden gebruikt door de Azure PowerShell-cmdlets voor implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c9e-135">**deploymentSettings.json**: Stores local settings that are used by the Azure PowerShell deployment cmdlets.</span></span>
4. <span data-ttu-id="63c9e-136">Voer de volgende opdracht in om een nieuwe webrol toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="63c9e-136">Enter the following command to add a new web role:</span></span>

       Add-AzureNodeWebRole

   ![The output of the Add-AzureNodeWebRole command][The output of the Add-AzureNodeWebRole command]

   <span data-ttu-id="63c9e-138">De **Add-AzureNodeWebRole**-cmdlet maakt een eenvoudige Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="63c9e-138">The **Add-AzureNodeWebRole** cmdlet creates a basic Node.js application.</span></span> <span data-ttu-id="63c9e-139">Ook worden de **.csfg**- en **.csdef**-bestanden aangepast met configuratie-items voor de nieuwe rol.</span><span class="sxs-lookup"><span data-stu-id="63c9e-139">It also modifies the **.csfg** and **.csdef** files to add configuration entries for the new role.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63c9e-140">Als u geen rolnaam opgeeft, wordt een standaardnaam gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63c9e-140">If you do not specify a role name, a default name is used.</span></span> <span data-ttu-id="63c9e-141">U kunt een naam opgeven als de eerste parameter van de cmdlet: `Add-AzureNodeWebRole MyRole`</span><span class="sxs-lookup"><span data-stu-id="63c9e-141">You can provide a name as the first cmdlet parameter: `Add-AzureNodeWebRole MyRole`</span></span>

<span data-ttu-id="63c9e-142">De Node.js-app is gedefinieerd in het bestand **server.js**, dat zich bevindt in de map voor de webrol (standaard **WebRole1**).</span><span class="sxs-lookup"><span data-stu-id="63c9e-142">The Node.js app is defined in the file **server.js**, located in the directory for the web role (**WebRole1** by default).</span></span> <span data-ttu-id="63c9e-143">Dit is de code:</span><span class="sxs-lookup"><span data-stu-id="63c9e-143">Here is the code:</span></span>

    var http = require('http');
    var port = process.env.port || 1337;
    http.createServer(function (req, res) {
        res.writeHead(200, { 'Content-Type': 'text/plain' });
        res.end('Hello World\n');
    }).listen(port);

<span data-ttu-id="63c9e-144">Deze code is in wezen hetzelfde als het testitem 'Hallo wereld' op de [nodejs.org]-website, behalve dat het poortnummer wordt gebruikt dat is toegewezen door de cloudomgeving.</span><span class="sxs-lookup"><span data-stu-id="63c9e-144">This code is essentially the same as the "Hello World" sample on the [nodejs.org] website, except it uses the port number assigned by the cloud environment.</span></span>

## <a name="deploy-the-application-to-azure"></a><span data-ttu-id="63c9e-145">De toepassing implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="63c9e-145">Deploy the application to Azure</span></span>

> [!NOTE]
> <span data-ttu-id="63c9e-146">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="63c9e-146">To complete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="63c9e-147">U kunt [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) of [u aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span><span class="sxs-lookup"><span data-stu-id="63c9e-147">You can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A85619ABF) or [sign up for a free account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).</span></span>

### <a name="download-the-azure-publishing-settings"></a><span data-ttu-id="63c9e-148">De Azure-publicatie-instellingen downloaden</span><span class="sxs-lookup"><span data-stu-id="63c9e-148">Download the Azure publishing settings</span></span>
<span data-ttu-id="63c9e-149">Voor het implementeren van uw toepassing naar Azure moet u eerst de publicatie-instellingen voor uw Azure-abonnement downloaden.</span><span class="sxs-lookup"><span data-stu-id="63c9e-149">To deploy your application to Azure, you must first download the publishing settings for your Azure subscription.</span></span>

1. <span data-ttu-id="63c9e-150">Voer de volgende Azure PowerShell-cmdlet uit:</span><span class="sxs-lookup"><span data-stu-id="63c9e-150">Run the following Azure PowerShell cmdlet:</span></span>

       Get-AzurePublishSettingsFile

   <span data-ttu-id="63c9e-151">Hierbij wordt uw browser gebruikt om te navigeren naar de downloadpagina voor publicatie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="63c9e-151">This will use your browser to navigate to the publish settings download page.</span></span> <span data-ttu-id="63c9e-152">U wordt mogelijk gevraagd om aan te melden met een Microsoft-account.</span><span class="sxs-lookup"><span data-stu-id="63c9e-152">You may be prompted to log in with a Microsoft Account.</span></span> <span data-ttu-id="63c9e-153">Als dit het geval is, gebruikt u het account dat is gekoppeld aan uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="63c9e-153">If so, use the account associated with your Azure subscription.</span></span>

   <span data-ttu-id="63c9e-154">Sla het gedownloade profiel op naar een bestandslocatie waar u gemakkelijk bij kunt.</span><span class="sxs-lookup"><span data-stu-id="63c9e-154">Save the downloaded profile to a file location you can easily access.</span></span>
2. <span data-ttu-id="63c9e-155">Voer de volgende cmdlet uit om het publicatieprofiel te importeren dat u hebt gedownload:</span><span class="sxs-lookup"><span data-stu-id="63c9e-155">Run following cmdlet to import the publishing profile you downloaded:</span></span>

       Import-AzurePublishSettingsFile [path to file]

    > [!NOTE]
    > <span data-ttu-id="63c9e-156">Na het importeren van de publicatie-instellingen is het raadzaam het gedownloade .publishSettings-bestand te verwijderen, omdat dit informatie bevat die iemand toegang zou kunnen geven tot uw account.</span><span class="sxs-lookup"><span data-stu-id="63c9e-156">After importing the publish settings, consider deleting the downloaded .publishSettings file, because it contains information that could allow someone to access your account.</span></span>

### <a name="publish-the-application"></a><span data-ttu-id="63c9e-157">De toepassing publiceren</span><span class="sxs-lookup"><span data-stu-id="63c9e-157">Publish the application</span></span>
<span data-ttu-id="63c9e-158">Voer de volgende opdrachten uit om de toepassing te publiceren:</span><span class="sxs-lookup"><span data-stu-id="63c9e-158">To publish, run the following commands:</span></span>

      $ServiceName = "NodeHelloWorld" + $(Get-Date -Format ('ddhhmm'))
    Publish-AzureServiceProject -ServiceName $ServiceName  -Location "East US" -Launch

* <span data-ttu-id="63c9e-159">**-ServiceName** is de naam voor de implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c9e-159">**-ServiceName** specifies the name for the deployment.</span></span> <span data-ttu-id="63c9e-160">Dit moet een unieke naam zijn, anders mislukt het publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="63c9e-160">This must be a unique name, otherwise the publish process will fail.</span></span> <span data-ttu-id="63c9e-161">De **Get-Date**-opdracht voegt een datum/tijd-tekenreeks toe die de naam uniek zou moeten maken.</span><span class="sxs-lookup"><span data-stu-id="63c9e-161">The **Get-Date** command tacks on a date/time string that should make the name unique.</span></span>
* <span data-ttu-id="63c9e-162">Met **-Location** geeft u het datacenter op waarin de toepassing wordt gehost.</span><span class="sxs-lookup"><span data-stu-id="63c9e-162">**-Location** specifies the datacenter that the application will be hosted in.</span></span> <span data-ttu-id="63c9e-163">Gebruik de **Get-AzureLocation**- cmdlet als u een lijst van beschikbare datacenters wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="63c9e-163">To see a list of available datacenters, use the **Get-AzureLocation** cmdlet.</span></span>
* <span data-ttu-id="63c9e-164">Met **-Launch** opent u een browservenster en gaat u naar de gehoste service nadat de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="63c9e-164">**-Launch** opens a browser window and navigates to the hosted service after deployment has completed.</span></span>

<span data-ttu-id="63c9e-165">Nadat de publicatie is uitgevoerd, ziet u een reactie vergelijkbaar met de volgende:</span><span class="sxs-lookup"><span data-stu-id="63c9e-165">After publishing succeeds, you will see a response similar to the following:</span></span>

![The output of the Publish-AzureService command][The output of the Publish-AzureService command]

> [!NOTE]
> <span data-ttu-id="63c9e-167">Het kan enkele minuten duren voordat de toepassing is geïmplementeerd en beschikbaar is wanneer dit de eerste keer is dat de toepassing wordt gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="63c9e-167">It can take several minutes for the application to deploy and become available when first published.</span></span>

<span data-ttu-id="63c9e-168">Zodra de implementatie is voltooid, wordt een browservenster geopend waarin naar de cloudservice wordt genavigeerd.</span><span class="sxs-lookup"><span data-stu-id="63c9e-168">Once the deployment has completed, a browser window will open and navigate to the cloud service.</span></span>

![A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.][A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]

<span data-ttu-id="63c9e-170">Uw toepassing wordt nu uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="63c9e-170">Your application is now running on Azure.</span></span>

<span data-ttu-id="63c9e-171">De **Publish-AzureServiceProject**-cmdlet voert de volgende stappen uit:</span><span class="sxs-lookup"><span data-stu-id="63c9e-171">The **Publish-AzureServiceProject** cmdlet performs the following steps:</span></span>

1. <span data-ttu-id="63c9e-172">Er wordt een implementatiepakket gemaakt.</span><span class="sxs-lookup"><span data-stu-id="63c9e-172">Creates a package to deploy.</span></span> <span data-ttu-id="63c9e-173">Het pakket bevat alle bestanden in de toepassingsmap.</span><span class="sxs-lookup"><span data-stu-id="63c9e-173">The package contains all the files in your application folder.</span></span>
2. <span data-ttu-id="63c9e-174">Er wordt een nieuw **opslagaccount** gemaakt, als dit nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="63c9e-174">Creates a new **storage account** if one does not exist.</span></span> <span data-ttu-id="63c9e-175">Het Azure-opslagaccount wordt gebruikt voor het opslaan van het toepassingspakket tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="63c9e-175">The Azure storage account is used to store the application package during deployment.</span></span> <span data-ttu-id="63c9e-176">U kunt het opslagaccount gewoon verwijderen nadat de implementatie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="63c9e-176">You can safely delete the storage account after deployment is done.</span></span>
3. <span data-ttu-id="63c9e-177">Er wordt een nieuwe **cloudservice** gemaakt als deze nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="63c9e-177">Creates a new **cloud service** if one does not already exist.</span></span> <span data-ttu-id="63c9e-178">Een **cloudservice** is de container waarin uw toepassing wordt gehost wanneer deze naar Azure wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="63c9e-178">A **cloud service** is the container in which your application is hosted when it is deployed to Azure.</span></span> <span data-ttu-id="63c9e-179">Zie [Overzicht van het maken van een gehoste service voor Azure].</span><span class="sxs-lookup"><span data-stu-id="63c9e-179">For more information, see [Overview of Creating a Hosted Service for Azure].</span></span>
4. <span data-ttu-id="63c9e-180">Het implementatiepakket wordt gepubliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="63c9e-180">Publishes the deployment package to Azure.</span></span>

## <a name="stopping-and-deleting-your-application"></a><span data-ttu-id="63c9e-181">De toepassing stoppen en verwijderen</span><span class="sxs-lookup"><span data-stu-id="63c9e-181">Stopping and deleting your application</span></span>
<span data-ttu-id="63c9e-182">Nadat u uw toepassing hebt geïmplementeerd, wilt u deze mogelijk uitschakelen om extra kosten te vermijden.</span><span class="sxs-lookup"><span data-stu-id="63c9e-182">After deploying your application, you may want to disable it so you can avoid extra costs.</span></span> <span data-ttu-id="63c9e-183">Webrolexemplaren in Azure worden per uur van verbruikte servertijd in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="63c9e-183">Azure bills web role instances per hour of server time consumed.</span></span> <span data-ttu-id="63c9e-184">Er wordt servertijd verbruikt zodra de toepassing is geïmplementeerd, zelfs als de exemplaren niet worden uitgevoerd en de gestopte status hebben.</span><span class="sxs-lookup"><span data-stu-id="63c9e-184">Server time is consumed once your application is deployed, even if the instances are not running and are in the stopped state.</span></span>

1. <span data-ttu-id="63c9e-185">In het Windows PowerShell-venster stopt u de service-implementatie die u in de vorige sectie hebt gemaakt, met de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="63c9e-185">In the Windows PowerShell window, stop the service deployment created in the previous section with the following cmdlet:</span></span>

       Stop-AzureService

   <span data-ttu-id="63c9e-186">Het kan enkele minuten duren voordat de service is gestopt.</span><span class="sxs-lookup"><span data-stu-id="63c9e-186">Stopping the service may take several minutes.</span></span> <span data-ttu-id="63c9e-187">Als de service is gestopt, krijgt u een bericht waarin dit wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="63c9e-187">When the service is stopped, you receive a message indicating that it has stopped.</span></span>

   ![The status of the Stop-AzureService command][The status of the Stop-AzureService command]
2. <span data-ttu-id="63c9e-189">Als u de service wilt verwijderen, roept u de volgende cmdlet aan:</span><span class="sxs-lookup"><span data-stu-id="63c9e-189">To delete the service, call the following cmdlet:</span></span>

       Remove-AzureService

   <span data-ttu-id="63c9e-190">Wanneer dit wordt gevraagd, typt u **Y** om de service te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="63c9e-190">When prompted, enter **Y** to delete the service.</span></span>

   <span data-ttu-id="63c9e-191">Het kan enkele minuten duren voordat de service is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="63c9e-191">Deleting the service may take several minutes.</span></span> <span data-ttu-id="63c9e-192">Als de service is verwijderd, krijgt u een bericht waarin dit wordt aangegeven.</span><span class="sxs-lookup"><span data-stu-id="63c9e-192">After the service has been deleted you receive a message indicating that the service was deleted.</span></span>

   ![The status of the Remove-AzureService command][The status of the Remove-AzureService command]

   > [!NOTE]
   > <span data-ttu-id="63c9e-194">Als u de service verwijdert, wordt niet het opslagaccount verwijderd dat is gemaakt toen de service voor de eerste keer werd gepubliceerd, en de kosten voor gebruikte opslag worden nog wel in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="63c9e-194">Deleting the service does not delete the storage account that was created when the service was initially published, and you will continue to be billed for storage used.</span></span> <span data-ttu-id="63c9e-195">Als niets anders de opslag gebruikt, kunt u deze verwijderen.</span><span class="sxs-lookup"><span data-stu-id="63c9e-195">If nothing else is using the storage, you may want to delete it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63c9e-196">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63c9e-196">Next steps</span></span>
<span data-ttu-id="63c9e-197">Zie het [Node.js Developer Center] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="63c9e-197">For more information, see the [Node.js Developer Center].</span></span>

<!-- URL List -->

<span data-ttu-id="63c9e-198">[Vergelijking van Azure Websites, Cloud Services en Virtual Machines]: ../app-service-web/choose-web-site-cloud-service-vm.md</span><span class="sxs-lookup"><span data-stu-id="63c9e-198">[Azure Websites, Cloud Services and Virtual Machines comparison]: ../app-service-web/choose-web-site-cloud-service-vm.md</span></span>
<span data-ttu-id="63c9e-199">[een eenvoudige web-app-functie te gebruiken]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="63c9e-199">[using a lightweight web app]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="63c9e-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span><span class="sxs-lookup"><span data-stu-id="63c9e-200">[Azure Powershell]: /powershell/azureps-cmdlets-docs</span></span>
<span data-ttu-id="63c9e-201">[Azure SDK voor .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span><span class="sxs-lookup"><span data-stu-id="63c9e-201">[Azure SDK for .NET 2.7]: http://www.microsoft.com/en-us/download/details.aspx?id=48178</span></span>
<span data-ttu-id="63c9e-202">[Koppel PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span><span class="sxs-lookup"><span data-stu-id="63c9e-202">[Connect PowerShell]: /powershell/azureps-cmdlets-docs#step-3-connect</span></span>
<span data-ttu-id="63c9e-203">[nodejs.org]: http://nodejs.org/</span><span class="sxs-lookup"><span data-stu-id="63c9e-203">[nodejs.org]: http://nodejs.org/</span></span>
<span data-ttu-id="63c9e-204">[Overzicht van het maken van een gehoste service voor Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span><span class="sxs-lookup"><span data-stu-id="63c9e-204">[Overview of Creating a Hosted Service for Azure]: https://azure.microsoft.com/documentation/services/cloud-services/</span></span>
<span data-ttu-id="63c9e-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span><span class="sxs-lookup"><span data-stu-id="63c9e-205">[Node.js Developer Center]: https://azure.microsoft.com/develop/nodejs/</span></span>

<!-- IMG List -->

[The result of the New-AzureService helloworld command]: ./media/cloud-services-nodejs-develop-deploy-app/node9.png
[The output of the Add-AzureNodeWebRole command]: ./media/cloud-services-nodejs-develop-deploy-app/node11.png
[A web browser displaying the Hello World web page]: ./media/cloud-services-nodejs-develop-deploy-app/node14.png
[The output of the Publish-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node19.png
[A browser window displaying the hello world page; the URL indicates the page is hosted on Azure.]: ./media/cloud-services-nodejs-develop-deploy-app/node21.png
[The status of the Stop-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node48.png
[The status of the Remove-AzureService command]: ./media/cloud-services-nodejs-develop-deploy-app/node49.png
