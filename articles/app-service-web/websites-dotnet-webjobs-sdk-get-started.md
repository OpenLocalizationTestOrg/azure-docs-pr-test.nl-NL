---
title: Maken van een webtaak .NET in Azure App Service | Microsoft Docs
description: Maak een app met meerdere lagen met ASP.NET MVC en Azure. De front-end wordt in een web-app in Azure App Service en de vorige einde wordt uitgevoerd als een webtaak wordt uitgevoerd. De app gebruikmaakt van Entity Framework, SQL-Database en Azure storage-wachtrijen en blobs.
services: app-service
documentationcenter: .net
author: tdykstra
manager: erikre
editor: mollybos
ms.assetid: 99cb9917-483a-45f8-a98d-07d19c68c753
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 6/14/2017
ms.author: glenga
ms.openlocfilehash: a20b13058caecff75af14957468f20e63a3325c9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="4c999-105">Een .NET-webtaak maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4c999-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="4c999-106">Deze zelfstudie laat zien hoe u code schrijven voor een eenvoudige ASP.NET MVC 5 toepassing met meerdere lagen die gebruikmaakt van de [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="4c999-106">This tutorial shows how to write code for a simple multi-tier ASP.NET MVC 5 application that uses the [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="4c999-107">Het doel van de [WebJobs SDK](websites-webjobs-resources.md) te vereenvoudigen, de code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="4c999-107">The purpose of the [WebJobs SDK](websites-webjobs-resources.md) is to simplify the code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="4c999-108">De WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's.</span><span class="sxs-lookup"><span data-stu-id="4c999-108">The WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="4c999-109">Bovendien kan worden uitgebreid ontworpen en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="4c999-109">In addition, it's designed to be extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="4c999-110">De voorbeeldtoepassing is een bulletinboard voor advertenties.</span><span class="sxs-lookup"><span data-stu-id="4c999-110">The sample application is an advertising bulletin board.</span></span> <span data-ttu-id="4c999-111">Gebruikers kunnen uploaden afbeeldingen voor advertenties en een back-end-proces de afbeeldingen worden geconverteerd naar miniatuurweergaven.</span><span class="sxs-lookup"><span data-stu-id="4c999-111">Users can upload images for ads, and a backend process converts the images to thumbnails.</span></span> <span data-ttu-id="4c999-112">De pagina van de lijst met ad toont de miniaturen en de detailpagina ad ziet u de afbeelding.</span><span class="sxs-lookup"><span data-stu-id="4c999-112">The ad list page shows the thumbnails, and the ad details page shows the full-size image.</span></span> <span data-ttu-id="4c999-113">Hier volgt een schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="4c999-113">Here's a screenshot:</span></span>

![Advertentielijst](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="4c999-115">Deze voorbeeldtoepassing werkt met [Azure wachtrijen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) en [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="4c999-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="4c999-116">De zelfstudie laat zien hoe de toepassing implementeren naar [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="4c999-116">The tutorial shows how to deploy the application to [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="4c999-117"><a id="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="4c999-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="4c999-118">De zelfstudie wordt ervan uitgegaan dat u hoe weet werken met [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projecten in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c999-118">The tutorial assumes that you know how to work with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="4c999-119">De zelfstudie oorspronkelijk is geschreven voor Visual Studio 2013, maar kan worden gebruikt met latere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c999-119">The tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="4c999-120">Als u van Visual Studio 2015 of 2017 gebruikmaakt, noteert u dat voordat u de toepassing lokaal uitvoeren, moet u de `Data Source` deel uit van de SQL Server LocalDB-verbindingsreeks in de Web.config en App.config bestanden van `Data Source=(localdb)\v11.0` naar `Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="4c999-120">If you are using Visual Studio 2015 or 2017, make note that before you run the application locally, you must change the `Data Source` part of the SQL Server LocalDB connection string in the Web.config and App.config files from `Data Source=(localdb)\v11.0` to `Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="4c999-121"><a name="note"></a>U hebt een Azure-account om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="4c999-121"><a name="note"></a>You must have an Azure account to complete this tutorial:</span></span>
>
> * <span data-ttu-id="4c999-122">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): U ontvangt tegoed dat u gebruiken kunt om betaalde Azure-services te proberen en zelfs nadat ze zijn gebruikt, kunt u het account houden en gratis Azure-services, zoals Websites gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4c999-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use to try out paid Azure services, and even after they're used up, you can keep the account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="4c999-123">Er wordt nooit iets op uw creditcard in rekening gebracht, tenzij u expliciet de instellingen wijzigt en vraagt of de kosten op uw creditcard in rekening kunnen worden gebracht.</span><span class="sxs-lookup"><span data-stu-id="4c999-123">Your credit card will never be charged, unless you explicitly change your settings and ask to be charged.</span></span>
> * <span data-ttu-id="4c999-124">U kunt [maandelijkse Azure-krediet voor Visual Studio-abonnees activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): uw abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4c999-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="4c999-125">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="4c999-125">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="4c999-126">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="4c999-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="4c999-127"><a id="learn"></a>Wat u leert</span><span class="sxs-lookup"><span data-stu-id="4c999-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="4c999-128">De zelfstudie laat zien hoe de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4c999-128">The tutorial shows how to do the following tasks:</span></span>

* <span data-ttu-id="4c999-129">Computer klaarmaken voor het ontwikkelen van Azure inschakelen door het installeren van de Azure-SDK (alleen voor Visual Studio 2013 en 2015 gebruikers).</span><span class="sxs-lookup"><span data-stu-id="4c999-129">Enable your machine for Azure development by installing the Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="4c999-130">Maak een project-consoletoepassing die automatisch wordt geïmplementeerd als een webtaak Azure wanneer u het bijbehorende webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="4c999-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy the associated web project.</span></span>
* <span data-ttu-id="4c999-131">Test een WebJobs SDK back-end lokaal op de ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="4c999-131">Test a WebJobs SDK backend locally on the development computer.</span></span>
* <span data-ttu-id="4c999-132">Publiceer een toepassing met een back-end voor API in een WebApp in App Service.</span><span class="sxs-lookup"><span data-stu-id="4c999-132">Publish an application with a WebJobs backend to a web app in App Service.</span></span>
* <span data-ttu-id="4c999-133">Bestanden uploaden en op te slaan in de Azure Blob-service.</span><span class="sxs-lookup"><span data-stu-id="4c999-133">Upload files and store them in the Azure Blob service.</span></span>
* <span data-ttu-id="4c999-134">Gebruik de Azure WebJobs SDK werken met Azure Storage-wachtrijen en blobs.</span><span class="sxs-lookup"><span data-stu-id="4c999-134">Use the Azure WebJobs SDK to work with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="4c999-135"><a id="contosoads"></a>Toepassingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="4c999-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="4c999-136">De voorbeeldtoepassing gebruikt de [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) naar tijdens stillegging het CPU-intensief werk van het maken van miniatuurweergaven voor een back-end-proces.</span><span class="sxs-lookup"><span data-stu-id="4c999-136">The sample application uses the [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) to off-load the CPU-intensive work of creating thumbnails to a backend process.</span></span>

<span data-ttu-id="4c999-137">De app slaat de advertenties met behulp van Entity Framework Code First op in een SQL-database om de tabellen te maken en toegang te krijgen tot de gegevens.</span><span class="sxs-lookup"><span data-stu-id="4c999-137">The app stores ads in a SQL database, using Entity Framework Code First to create the tables and access the data.</span></span> <span data-ttu-id="4c999-138">Voor elke advertentie slaat de database twee URL's: één voor de afbeelding op volledige grootte en één voor de miniatuur.</span><span class="sxs-lookup"><span data-stu-id="4c999-138">For each ad, the database stores two URLs: one for the full-size image and one for the thumbnail.</span></span>

![Advertentietabel](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="4c999-140">Wanneer een gebruiker een afbeelding uploadt de web-app slaat de afbeelding in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), slaat de Advertentiegegevens worden opgeslagen in de database met een URL die naar de blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="4c999-140">When a user uploads an image, the web app stores the image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores the ad information in the database with a URL that points to the blob.</span></span> <span data-ttu-id="4c999-141">Tegelijkertijd schrijft de front-end een bericht naar een Azure-wachtrij.</span><span class="sxs-lookup"><span data-stu-id="4c999-141">At the same time, it writes a message to an Azure queue.</span></span> <span data-ttu-id="4c999-142">In een back-end-proces als een Azure-webtaak wordt uitgevoerd, controleert de WebJobs SDK of de wachtrij voor nieuwe berichten.</span><span class="sxs-lookup"><span data-stu-id="4c999-142">In a backend process running as an Azure WebJob, the WebJobs SDK polls the queue for new messages.</span></span> <span data-ttu-id="4c999-143">Wanneer een nieuw bericht wordt weergegeven, wordt de webtaak wordt gemaakt van een miniatuur voor de betreffende afbeelding en de miniatuur databaseveld URL voor de advertentie-updates.</span><span class="sxs-lookup"><span data-stu-id="4c999-143">When a new message appears, the WebJob creates a thumbnail for that image and updates the thumbnail URL database field for that ad.</span></span> <span data-ttu-id="4c999-144">Hier volgt een diagram toont de wisselwerking tussen de onderdelen van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="4c999-144">Here's a diagram that shows how the parts of the application interact:</span></span>

![Architectuur van Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="4c999-146">De zelfstudie instructies gelden voor de Azure SDK voor .NET 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4c999-146">The tutorial instructions apply to Azure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="4c999-147"><a id="storage"></a>Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="4c999-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="4c999-148">Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij- en blobgegevens in de cloud.</span><span class="sxs-lookup"><span data-stu-id="4c999-148">An Azure storage account provides resources for storing queue and blob data in the cloud.</span></span> <span data-ttu-id="4c999-149">Dit wordt ook gebruikt door de WebJobs SDK voor het opslaan van gegevens van de logboekregistratie voor het dashboard.</span><span class="sxs-lookup"><span data-stu-id="4c999-149">It's also used by the WebJobs SDK to store logging data for the dashboard.</span></span>

<span data-ttu-id="4c999-150">In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens en afzonderlijke accounts voor testgegevens versus productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="4c999-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="4c999-151">Voor deze zelfstudie gebruikt u slechts één account.</span><span class="sxs-lookup"><span data-stu-id="4c999-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="4c999-152">Open de **Server Explorer** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c999-152">Open the **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="4c999-153">Met de rechtermuisknop op de **Azure** knooppunt en klik vervolgens op **verbinding maken met Microsoft Azure-abonnement...** .</span><span class="sxs-lookup"><span data-stu-id="4c999-153">Right-click the **Azure** node, and then click **Connect to Microsoft Azure Subscription...**.</span></span>
   
   ![Verbinding maken met Azure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="4c999-155">Meld u aan met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="4c999-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="4c999-156">Met de rechtermuisknop op **opslag** onder de Azure-knooppunt en klik vervolgens op **Storage-Account maken**.</span><span class="sxs-lookup"><span data-stu-id="4c999-156">Right-click **Storage** under the Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Storage-Account maken](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="4c999-158">In de **Storage-Account maken** dialoogvenster, voer een naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4c999-158">In the **Create Storage Account** dialog, enter a name for the storage account.</span></span>

    <span data-ttu-id="4c999-159">De naam moet uniek zijn (geen Azure storage-account kan dezelfde naam hebben).</span><span class="sxs-lookup"><span data-stu-id="4c999-159">The name must be must be unique (no other Azure storage account can have the same name).</span></span> <span data-ttu-id="4c999-160">Als de naam die u invoert, al gebruikt wordt, krijgt u een kans om dit te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4c999-160">If the name you enter is already in use, you'll get a chance to change it.</span></span>

    <span data-ttu-id="4c999-161">De URL voor toegang tot uw storage-account *{name}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="4c999-161">The URL to access your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="4c999-162">Stel de **regio of Affiniteitsgroep** vervolgkeuzelijst voor de regio die het dichtst bij u.</span><span class="sxs-lookup"><span data-stu-id="4c999-162">Set the **Region or Affinity Group** drop-down list to the region closest to you.</span></span>

    <span data-ttu-id="4c999-163">Deze instelling bepaalt u welke Azure-datacenter fungeert als host voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4c999-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="4c999-164">Voor deze zelfstudie won't uw keuze maakt geen merkbaar verschil.</span><span class="sxs-lookup"><span data-stu-id="4c999-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="4c999-165">Voor een productie-web-app wilt u echter uw storage-account zich in dezelfde regio kosten voor uitgaande gegevens en de latentie te minimaliseren en de webserver.</span><span class="sxs-lookup"><span data-stu-id="4c999-165">However, for a production web app, you want your web server and your storage account to be in the same region to minimize latency and data egress charges.</span></span> <span data-ttu-id="4c999-166">De web-app (die u later maken) datacenter moet zo dicht mogelijk bij de toegang tot de web-app om te minimaliseren latentie browsers.</span><span class="sxs-lookup"><span data-stu-id="4c999-166">The web app (which you'll create later) datacenter should be as close as possible to the browsers accessing the web app in order to minimize latency.</span></span>
7. <span data-ttu-id="4c999-167">Stel de vervolgkeuzelijst **Replicatie** in op **Lokaal redundant**.</span><span class="sxs-lookup"><span data-stu-id="4c999-167">Set the **Replication** drop-down list to **Locally redundant**.</span></span>

    <span data-ttu-id="4c999-168">Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, wordt de opgeslagen inhoud gerepliceerd naar een secundair datacenter om failover naar die locatie mogelijk te maken in het geval van een noodgeval op de primaire locatie.</span><span class="sxs-lookup"><span data-stu-id="4c999-168">When geo-replication is enabled for a storage account, the stored content is replicated to a secondary datacenter to enable failover to that location in case of a major disaster in the primary location.</span></span> <span data-ttu-id="4c999-169">Geo-replicatie kan extra kosten met zich meebrengen.</span><span class="sxs-lookup"><span data-stu-id="4c999-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="4c999-170">Voor test- en ontwikkelingsaccounts wilt u in het algemeen niet betalen voor geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="4c999-170">For test and development accounts, you generally don't want to pay for geo-replication.</span></span> <span data-ttu-id="4c999-171">Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4c999-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="4c999-172">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="4c999-172">Click **Create**.</span></span>

    ![Nieuw opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="4c999-174"><a id="download"></a>De toepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="4c999-174"><a id="download"></a>Download the application</span></span>
1. <span data-ttu-id="4c999-175">Download de [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb) en pak deze uit.</span><span class="sxs-lookup"><span data-stu-id="4c999-175">Download and unzip the [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="4c999-176">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4c999-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="4c999-177">Van de **bestand** in het menu **openen > Project/oplossing**, gaat u naar waar u de oplossing gedownload en open het oplossingsbestand.</span><span class="sxs-lookup"><span data-stu-id="4c999-177">From the **File** menu choose **Open > Project/Solution**, navigate to where you downloaded the solution, and then open the solution file.</span></span>
4. <span data-ttu-id="4c999-178">Druk op CTRL + SHIFT + B om de oplossing te bouwen.</span><span class="sxs-lookup"><span data-stu-id="4c999-178">Press CTRL+SHIFT+B to build the solution.</span></span>

    <span data-ttu-id="4c999-179">Standaard herstelt Visual Studio automatisch de inhoud van het NuGet-pakket, dat niet is opgenomen in het *.zip*-bestand.</span><span class="sxs-lookup"><span data-stu-id="4c999-179">By default, Visual Studio automatically restores the NuGet package content, which was not included in the *.zip* file.</span></span> <span data-ttu-id="4c999-180">Als de pakketten niet worden hersteld, deze handmatig installeren door te gaan naar de **NuGet-pakketten beheren voor oplossing** dialoogvenster en te klikken op de **herstellen** knop in de rechterbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="4c999-180">If the packages don't restore, install them manually by going to the **Manage NuGet Packages for Solution** dialog and clicking the **Restore** button at the top right.</span></span>
5. <span data-ttu-id="4c999-181">In **Solution Explorer**, zorg ervoor dat **ContosoAdsWeb** is geselecteerd als opstartproject.</span><span class="sxs-lookup"><span data-stu-id="4c999-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as the startup project.</span></span>

## <span data-ttu-id="4c999-182"><a id="configurestorage"></a>De toepassing configureren voor uw storage-account gebruiken</span><span class="sxs-lookup"><span data-stu-id="4c999-182"><a id="configurestorage"></a>Configure the application to use your storage account</span></span>
1. <span data-ttu-id="4c999-183">Open de toepassing *Web.config* bestand in het project ContosoAdsWeb.</span><span class="sxs-lookup"><span data-stu-id="4c999-183">Open the application *Web.config* file in the ContosoAdsWeb project.</span></span>

    <span data-ttu-id="4c999-184">Het bestand bevat een SQL-verbindingsreeks en de verbindingsreeks van een Azure-opslag voor het werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="4c999-184">The file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="4c999-185">De SQL-verbindingsreeks verwijst naar een [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span><span class="sxs-lookup"><span data-stu-id="4c999-185">The SQL connection string points to a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="4c999-186">De verbindingsreeks voor opslag is een voorbeeld van tijdelijke aanduidingen voor de storage-account naam en toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="4c999-186">The storage connection string is an example that has placeholders for the storage account name and access key.</span></span> <span data-ttu-id="4c999-187">U hebt deze vervangen met een verbindingsreeks met de naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="4c999-187">You'll replace this with a connection string that has the name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="4c999-188">De verbindingsreeks voor opslag is standaard de naam AzureWebJobsStorage omdat dat de naam van die de WebJobs SDK wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4c999-188">The storage connection string is named AzureWebJobsStorage because that's the name the WebJobs SDK uses by default.</span></span> <span data-ttu-id="4c999-189">Dezelfde naam wordt hier gebruikt, hoeft u slechts één gegevensbronwaarde in de Azure-omgeving instellen.</span><span class="sxs-lookup"><span data-stu-id="4c999-189">The same name is used here so you have to set only one connection string value in the Azure environment.</span></span>
2. <span data-ttu-id="4c999-190">In **Server Explorer**, met de rechtermuisknop op uw opslagaccount onder de **opslag** knooppunt en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-190">In **Server Explorer**, right-click your storage account under the **Storage** node, and then click **Properties**.</span></span>

    ![Klik op Eigenschappen van het Opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="4c999-192">In de **eigenschappen** venster, klikt u op **Opslagaccountsleutels**, en klik vervolgens op het weglatingsteken.</span><span class="sxs-lookup"><span data-stu-id="4c999-192">In the **Properties** window, click **Storage Account Keys**, and then click the ellipsis.</span></span>

    ![Toegangscodes voor opslag](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="4c999-194">Kopieer de **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="4c999-194">Copy the **Connection String**.</span></span>

    ![Opslag toegangscodes dialoogvenster](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="4c999-196">Vervang de verbindingsreeks voor opslag in de *Web.config* bestand met de verbindingsreeks die u zojuist hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-196">Replace the storage connection string in the *Web.config* file with the connection string you just copied.</span></span> <span data-ttu-id="4c999-197">Zorg ervoor dat u Alles selecteren binnen de aanhalingstekens, maar niet inclusief de aanhalingstekens voordat u gaat plakken.</span><span class="sxs-lookup"><span data-stu-id="4c999-197">Make sure you select everything inside the quotation marks but not including the quotation marks before pasting.</span></span>
6. <span data-ttu-id="4c999-198">Open de *App.config* bestand in het project ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="4c999-198">Open the *App.config* file in the ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="4c999-199">Dit bestand heeft twee storage-verbindingsreeksen, één voor toepassingsgegevens en één voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="4c999-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="4c999-200">U kunt afzonderlijke storage-accounts voor toepassingsgegevens en logboekregistratie en kunt u [meerdere opslagaccounts voor gegevens](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="4c999-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="4c999-201">Voor deze zelfstudie maakt u een één opslagaccount gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4c999-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="4c999-202">De verbindingsreeksen hebben tijdelijke aanduidingen voor de opslagaccountsleutels.</span><span class="sxs-lookup"><span data-stu-id="4c999-202">The connection strings have placeholders for the storage account keys.</span></span>

    ```
    <configuration>
        <connectionStrings>
            <add name="AzureWebJobsDashboard" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
            <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;"/>
    </connectionStrings>
        <startup>
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    </configuration>

    ```

    <span data-ttu-id="4c999-203">Standaard zoekt de WebJobs SDK met de naam AzureWebJobsStorage en AzureWebJobsDashboard verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="4c999-203">By default, the WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="4c999-204">Als alternatief kunt u [store de verbinding string, maar u wilt en geef dit in expliciet aan de `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="4c999-204">As an alternative, you can [store the connection string however you want and pass it in explicitly to the `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="4c999-205">Beide storage-verbindingsreeksen vervangen door de verbindingsreeks die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-205">Replace both storage connection strings with the connection string you copied earlier.</span></span>
8. <span data-ttu-id="4c999-206">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="4c999-206">Save your changes.</span></span>

## <span data-ttu-id="4c999-207"><a id="run"></a>De toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4c999-207"><a id="run"></a>Run the application locally</span></span>
1. <span data-ttu-id="4c999-208">Druk op CTRL + F5 voor het starten van de front-end webserver van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c999-208">To start the web frontend of the application, press CTRL+F5.</span></span>

    <span data-ttu-id="4c999-209">De standaardbrowser geopend met de startpagina.</span><span class="sxs-lookup"><span data-stu-id="4c999-209">The default browser opens to the home page.</span></span> <span data-ttu-id="4c999-210">(Het webproject wordt uitgevoerd omdat u opstartproject hebt aangebracht.)</span><span class="sxs-lookup"><span data-stu-id="4c999-210">(The web project runs because you've made it the startup project.)</span></span>

    ![Contoso Ads-startpagina](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="4c999-212">Voor het starten van de webtaak back-end van de toepassing met de rechtermuisknop op het project ContosoAdsWebJob in **Solution Explorer**, en klik vervolgens op **Debug** > **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="4c999-212">To start the WebJob backend of the application, right-click the ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="4c999-213">Een toepassing consolevenster opent en toont logboekregistratie-berichten die aangeven dat het object WebJobs SDK JobHost is gestart om uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4c999-213">A console application window opens and displays logging messages indicating the WebJobs SDK JobHost object has started to run.</span></span>

    ![Toepassing consolevenster weergegeven dat de back-end wordt uitgevoerd](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="4c999-215">Klik in uw browser **maken een advertentie**.</span><span class="sxs-lookup"><span data-stu-id="4c999-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="4c999-216">Voer enkele testgegevens, selecteert u een installatiekopie uploaden en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4c999-216">Enter some test data, select an image to upload, and then click **Create**.</span></span>

    ![De pagina Create](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="4c999-218">De app gaat naar de indexpagina, maar geeft voor de nieuwe advertentie geen miniatuur weer omdat de betreffende bewerking nog niet heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="4c999-218">The app goes to the Index page, but it doesn't show a thumbnail for the new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="4c999-219">Ondertussen na een korte wachten logboekregistratie in een bericht in het consolevenster van de toepassing aangegeven dat een wachtrijbericht is ontvangen en is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4c999-219">Meanwhile, after a short wait a logging message in the console application window shows that a queue message was received and has been processed.</span></span>

    ![Toepassing consolevenster weergegeven dat er een wachtrijbericht is verwerkt](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="4c999-221">Nadat u de logboekregistratie van berichten in het consolevenster van de toepassing ziet, vernieuwt u de indexpagina om te zien van de miniatuur.</span><span class="sxs-lookup"><span data-stu-id="4c999-221">After you see the logging messages in the console application window, refresh the Index page to see the thumbnail.</span></span>

    ![De indexpagina](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="4c999-223">Klik op **Details** voor uw advertentie om de afbeelding op volledige grootte te bekijken.</span><span class="sxs-lookup"><span data-stu-id="4c999-223">Click **Details** for your ad to see the full-size image.</span></span>

    ![De pagina Details](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="4c999-225">U hebt uitvoert, de toepassing op uw lokale computer, en deze gebruik maakt van een SQL Server-database op de computer, maar werkt met wachtrijen en blobs in de cloud.</span><span class="sxs-lookup"><span data-stu-id="4c999-225">You've been running the application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in the cloud.</span></span> <span data-ttu-id="4c999-226">In de volgende sectie voert u de toepassing in de cloud, met behulp van een cloud-database, evenals cloud blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="4c999-226">In the following section you'll run the application in the cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="4c999-227"><a id="runincloud"></a>De toepassing uitvoert in de cloud</span><span class="sxs-lookup"><span data-stu-id="4c999-227"><a id="runincloud"></a>Run the application in the cloud</span></span>
<span data-ttu-id="4c999-228">U voert de volgende stappen uit voor het uitvoeren van de toepassing in de cloud:</span><span class="sxs-lookup"><span data-stu-id="4c999-228">You'll do the following steps to run the application in the cloud:</span></span>

* <span data-ttu-id="4c999-229">Implementeer op Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="4c999-229">Deploy to Web Apps.</span></span> <span data-ttu-id="4c999-230">Visual Studio maakt automatisch een nieuwe web-app in App Service en een exemplaar van SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="4c999-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="4c999-231">De web-app voor het gebruik van uw Azure SQL database- en storage-account configureren.</span><span class="sxs-lookup"><span data-stu-id="4c999-231">Configure the web app to use your Azure SQL database and storage account.</span></span>

<span data-ttu-id="4c999-232">Nadat u advertenties hebt gemaakt tijdens het uitvoeren van de cloud, bekijkt u het WebJobs SDK dashboard overzicht van de uitgebreide bewakingsfuncties niet optimaal.</span><span class="sxs-lookup"><span data-stu-id="4c999-232">After you've created some ads while running in the cloud, you'll view the WebJobs SDK dashboard to see the rich monitoring features it has to offer.</span></span>

### <a name="deploy-to-web-apps"></a><span data-ttu-id="4c999-233">Implementeren voor Web-Apps</span><span class="sxs-lookup"><span data-stu-id="4c999-233">Deploy to Web Apps</span></span>

1. <span data-ttu-id="4c999-234">Sluit de browser en het consolevenster van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="4c999-234">Close the browser and the console application window.</span></span>
2. <span data-ttu-id="4c999-235">Volg de stappen in de [publiceren naar Azure met SQL-Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sectie.</span><span class="sxs-lookup"><span data-stu-id="4c999-235">Follow the steps in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="4c999-236">Nadat u de stappen voor de implementatie hebt voltooid, kunt u doorgaan met de resterende taken in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4c999-236">After you complete the steps for deploying, continue with the remaining tasks in this article.</span></span>

### <a name="configure-the-web-app-to-use-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="4c999-237">De web-app voor het gebruik van uw Azure SQL database- en storage-account configureren</span><span class="sxs-lookup"><span data-stu-id="4c999-237">Configure the web app to use your Azure SQL database and storage account</span></span>
<span data-ttu-id="4c999-238">Het is een best practice bij beveiliging naar [te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="4c999-238">It's a security best practice to [avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="4c999-239">Azure biedt een manier om u te doen: u kunt de verbindingstekenreeks en andere instellingswaarden instellen in de Azure-omgeving en ASP.NET-configuratie API's automatisch kunnen worden opgepikt deze waarden als de app wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="4c999-239">Azure provides a way to do that: you can set connection string and other setting values in the Azure environment, and ASP.NET configuration APIs automatically pick up these values when the app runs in Azure.</span></span> <span data-ttu-id="4c999-240">U kunt deze waarden instellen in Azure met behulp van **Server Explorer**, de Azure Portal, Windows PowerShell of de platformoverschrijdende opdrachtregelinterface.</span><span class="sxs-lookup"><span data-stu-id="4c999-240">You can set these values in Azure by using **Server Explorer**, the Azure Portal, Windows PowerShell, or the cross-platform command-line interface.</span></span> <span data-ttu-id="4c999-241">Zie voor meer informatie [tekenreeksen van toepassingen en verbindingsreeksen](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="4c999-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="4c999-242">In deze sectie gebruikt u **Server Explorer** verbinding tekenreekswaarden instellen in Azure.</span><span class="sxs-lookup"><span data-stu-id="4c999-242">In this section, you use **Server Explorer** to set connection string values in Azure.</span></span>

1. <span data-ttu-id="4c999-243">In **Server Explorer**, met de rechtermuisknop op uw web-app onder **Azure > App Service > {uw resourcegroep}**, en klik vervolgens op **weergave-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="4c999-244">De **Azure-Web-App** venster wordt geopend op de **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4c999-244">The **Azure Web App** window opens on the **Configuration** tab.</span></span>
2. <span data-ttu-id="4c999-245">Wijzig de naam van de verbindingsreeks DefaultConnection in de naam die u hebt gekozen bij het instellen van de SQL-database in de [publiceren naar Azure met SQL-Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artikel.</span><span class="sxs-lookup"><span data-stu-id="4c999-245">Change the name of the DefaultConnection connection string to the name you chose when you configured the SQL database in the [Publish to Azure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="4c999-246">Deze verbindingsreeks Azure automatisch gemaakt wanneer u de web-app met een bijbehorende database gemaakt, zodat deze de waarde voor de juiste verbinding al heeft.</span><span class="sxs-lookup"><span data-stu-id="4c999-246">Azure automatically created this connection string when you created the web app with an associated database, so it already has the right connection string value.</span></span> <span data-ttu-id="4c999-247">Alleen de naam wijzigt u op wat uw code zoekt.</span><span class="sxs-lookup"><span data-stu-id="4c999-247">You're changing just the name to what your code is looking for.</span></span>
3. <span data-ttu-id="4c999-248">Twee nieuwe verbindingsreeksen, met de naam AzureWebJobsStorage en AzureWebJobsDashboard toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c999-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="4c999-249">Het databasetype instellen op **aangepaste**, en stel de waarde voor de verbinding op dezelfde waarde die u eerder hebt gebruikt voor de *Web.config* en *App.config* bestanden.</span><span class="sxs-lookup"><span data-stu-id="4c999-249">Set the database type to **Custom**, and set the connection string value to the same value that you used earlier for the *Web.config* and *App.config* files.</span></span> <span data-ttu-id="4c999-250">(Zorg ervoor dat u de volledige verbindingsreeks, niet alleen de toegangssleutel opneemt en de aanhalingstekens zijn niet opgenomen.)</span><span class="sxs-lookup"><span data-stu-id="4c999-250">(Be sure you include the entire connection string, not just the access key, and don't include the quotation marks.)</span></span>

    <span data-ttu-id="4c999-251">Deze verbindingsreeksen worden gebruikt door de WebJobs SDK, één voor toepassingsgegevens en één voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="4c999-251">These connection strings are used by the WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="4c999-252">Als u eerder hebt gezien, wordt voor toepassingsgegevens wordt ook gebruikt door de web-front-code.</span><span class="sxs-lookup"><span data-stu-id="4c999-252">As you saw earlier, the one for application data is also used by the web front-end code.</span></span>
4. <span data-ttu-id="4c999-253">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4c999-253">Click **Save**.</span></span>

    ![Verbindingsreeksen in Azure Portal](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="4c999-255">In **Server Explorer**, met de rechtermuisknop op de web-app en klik vervolgens op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-255">In **Server Explorer**, right-click the web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="4c999-256">Nadat de web-app stopt, opnieuw met de rechtermuisknop op de web-app en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="4c999-256">After the web app stops, right-click the web app again, and then click **Start**.</span></span>

   <span data-ttu-id="4c999-257">De webtaak wordt automatisch gestart wanneer u publiceren, maar stopt wanneer u een configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="4c999-257">The WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="4c999-258">Om deze opnieuw starten, kunt u de web-app starten of opnieuw opstarten van de webtaak in de [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="4c999-258">To restart it, you can either restart the web app or restart the WebJob in the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="4c999-259">Het is doorgaans aanbevolen na een wijziging in de configuratie opnieuw opstarten van de web-app.</span><span class="sxs-lookup"><span data-stu-id="4c999-259">It's generally recommended to restart the web app after a configuration change.</span></span>
7. <span data-ttu-id="4c999-260">Vernieuw het browservenster met de web-app-URL in de adresbalk.</span><span class="sxs-lookup"><span data-stu-id="4c999-260">Refresh the browser window that has the web app URL in its address bar.</span></span>

    <span data-ttu-id="4c999-261">De startpagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-261">The home page appears.</span></span>
8. <span data-ttu-id="4c999-262">Maken van een advertentie, net als wanneer u [de toepassing lokaal uitgevoerd](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="4c999-262">Create an ad, as you did when you [ran the application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="4c999-263">De indexpagina toont zonder een miniatuur in eerste instantie.</span><span class="sxs-lookup"><span data-stu-id="4c999-263">The Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="4c999-264">Vernieuw de pagina na enkele seconden en de miniatuur weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-264">Refresh the page after a few seconds and the thumbnail appears.</span></span>

   <span data-ttu-id="4c999-265">Als de miniatuur niet wordt weergegeven, moet u wellicht wachten totdat een minuut of doet voor de webtaak op te starten.</span><span class="sxs-lookup"><span data-stu-id="4c999-265">If the thumbnail doesn't appear, you might have to wait a minute or so for the WebJob to restart.</span></span> <span data-ttu-id="4c999-266">Als u na een tijdje nog steeds niet wordt weergegeven de miniatuur wanneer u de pagina vernieuwt, kan de webtaak niet automatisch hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="4c999-266">If after a while, you still don't see the thumbnail when you refresh the page, the WebJob might not have started automatically.</span></span> <span data-ttu-id="4c999-267">In dat geval gaat u naar de **App Services** blade in de [Azure-portal](https://portal.azure.com/), zoek uw web-app en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="4c999-267">In that case, go to the **App Services** blade in the [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-the-webjobs-sdk-dashboard"></a><span data-ttu-id="4c999-268">De WebJobs SDK-dashboard weergeven</span><span class="sxs-lookup"><span data-stu-id="4c999-268">View the WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="4c999-269">In de [Azure-portal](https://portal.azure.com/), selecteer de **blade App Services**, Ga naar uw web-app en selecteer **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="4c999-269">In the [Azure portal](https://portal.azure.com/), select the **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="4c999-270">Selecteer de **logboeken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="4c999-270">Select the **Logs** tab.</span></span>

    ![Tabblad Logboeken](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="4c999-272">Een nieuw browsertabblad geopend met de WebJobs SDK-dashboard.</span><span class="sxs-lookup"><span data-stu-id="4c999-272">A new browser tab opens to the WebJobs SDK dashboard.</span></span> <span data-ttu-id="4c999-273">Het dashboard ziet u dat de webtaak wordt uitgevoerd en wordt een lijst met functies in uw code waarmee de WebJobs SDK is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-273">The dashboard shows that the WebJob is running and shows a list of functions in your code that the WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="4c999-274">Klik op een van de functies voor informatie over de uitvoering ervan.</span><span class="sxs-lookup"><span data-stu-id="4c999-274">Click one of the functions to see details about its execution.</span></span>

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="4c999-277">De **Replay-functie** knop op deze pagina zorgt ervoor dat de WebJobs SDK framework Roep de functie opnieuw, en geeft u een kans om de gegevens doorgegeven aan de functie eerst te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4c999-277">The **Replay Function** button on this page causes the WebJobs SDK framework to call the function again, and it gives you a chance to change the data passed to the function first.</span></span>

> [!NOTE]
> <span data-ttu-id="4c999-278">Wanneer u klaar bent met testen, kunt u eventueel de web-app, storage-account en uw exemplaar van SQL-Database verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4c999-278">When you're finished testing, consider deleting the web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="4c999-279">De web-app is gratis, maar het SQL-storage-account en de database-exemplaar doorlopen kosten (zij, minimale vanwege de grootte klein).</span><span class="sxs-lookup"><span data-stu-id="4c999-279">The web app is free, but the SQL storage account and database instance accrue charges (albeit, minimal due to the small size).</span></span> <span data-ttu-id="4c999-280">Ook als u de web-app actief laat, kunt iedereen die uw URL vindt advertenties maken en weergeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-280">Also, if you leave the web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="4c999-281">Uw web-app verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c999-281">Delete your web app</span></span>
<span data-ttu-id="4c999-282">In de portal, gaat u naar de **App Services** blade Zoek en selecteer uw web-app en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-282">In the portal, go to the **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="4c999-283">Als u alleen tijdelijk voorkomen dat anderen toegang hebben tot de web-app, klikt u op wilt **stoppen** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="4c999-283">If you just want to temporarily prevent others from accessing the web app, click **Stop** instead.</span></span> <span data-ttu-id="4c999-284">In dat geval blijven de kosten doorlopen voor het SQL-Database en Storage-account.</span><span class="sxs-lookup"><span data-stu-id="4c999-284">In that case, charges will continue to accrue for the SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="4c999-285">Uw storage-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c999-285">Delete your storage account</span></span>
<span data-ttu-id="4c999-286">Zie het verwijderen van uw opslagaccount [een opslagaccount verwijderen](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="4c999-286">To delete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="4c999-287">Uw database verwijderen</span><span class="sxs-lookup"><span data-stu-id="4c999-287">Delete your database</span></span>
<span data-ttu-id="4c999-288">Zie het verwijderen van de SQL-database de [REST-API van Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="4c999-288">To delete your SQL database, see the [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="4c999-289"><a id="create"></a>De toepassing vanaf het begin maken</span><span class="sxs-lookup"><span data-stu-id="4c999-289"><a id="create"></a>Create the application from scratch</span></span>
<span data-ttu-id="4c999-290">In deze sectie, doet u de volgende taken:</span><span class="sxs-lookup"><span data-stu-id="4c999-290">In this section you'll do the following tasks:</span></span>

* <span data-ttu-id="4c999-291">Een Visual Studio-oplossing maken met een webproject.</span><span class="sxs-lookup"><span data-stu-id="4c999-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="4c999-292">Voeg een klasse bibliotheek-project voor de data access-laag die wordt gedeeld tussen de front-end en back-end.</span><span class="sxs-lookup"><span data-stu-id="4c999-292">Add a class library project for the data access layer that is shared between the front end and back end.</span></span>
* <span data-ttu-id="4c999-293">Voeg een consoletoepassing-project voor de back-end met WebJobs-implementatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="4c999-293">Add a Console Application project for the backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="4c999-294">NuGet-pakketten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4c999-294">Add NuGet packages.</span></span>
* <span data-ttu-id="4c999-295">Projectverwijzingen instellen.</span><span class="sxs-lookup"><span data-stu-id="4c999-295">Set project references.</span></span>
* <span data-ttu-id="4c999-296">Kopieer toepassingsbestanden code en configuratie van de gedownloade toepassing die u in de vorige sectie van de zelfstudie hebt gewerkt.</span><span class="sxs-lookup"><span data-stu-id="4c999-296">Copy application code and configuration files from the downloaded application that you worked with in the previous section of the tutorial.</span></span>
* <span data-ttu-id="4c999-297">Bekijk de onderdelen van de code die met Azure blobs en wachtrijen en de WebJobs SDK werken.</span><span class="sxs-lookup"><span data-stu-id="4c999-297">Review the parts of the code that work with Azure blobs and queues and the WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="4c999-298">Een Visual Studio-oplossing maken met een webproject en class library-project</span><span class="sxs-lookup"><span data-stu-id="4c999-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="4c999-299">Kies in Visual Studio **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="4c999-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="4c999-300">In de **nieuw Project** dialoogvenster kiezen **Visual C#** > **Web** > **ASP.NET-webtoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="4c999-300">In the **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="4c999-301">Noem het project ContosoAdsWeb, de naam van de oplossing ContosoAdsWebJobsSDK (wijzigen de oplossing als u deze wilt opslaan in dezelfde map als de gedownloade oplossing naam) en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-301">Name the project ContosoAdsWeb, name the solution ContosoAdsWebJobsSDK (change the solution name if you're putting it in the same folder as the downloaded solution), and then click **OK**.</span></span>

    ![Nieuw project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="4c999-303">In de **nieuwe ASP.NET-webtoepassing** dialoogvenster, kies de MVC-sjabloon en selecteer **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-303">In the **New ASP.NET Web Application** dialog, choose the MVC template, and select **Change Authentication**.</span></span>

    ![Verificatie wijzigen](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="4c999-305">In de **verificatie wijzigen** dialoogvenster kiezen **geen verificatie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-305">In the **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Geen verificatie](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="4c999-307">In de **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-307">In the **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="4c999-308">Visual Studio maakt de oplossing en het webproject.</span><span class="sxs-lookup"><span data-stu-id="4c999-308">Visual Studio creates the solution and the web project.</span></span>
7. <span data-ttu-id="4c999-309">In **Solution Explorer**, met de rechtermuisknop op de oplossing (niet op het project) en kies **toevoegen** > **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="4c999-309">In **Solution Explorer**, right-click the solution (not the project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="4c999-310">In de **Add New Project** dialoogvenster kiezen **Visual C#** > **Classic Windows Desktop** > **Class Library (.NET Framework)** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4c999-310">In the **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="4c999-311">Geef het project de naam *ContosoAdsCommon* en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-311">Name the project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="4c999-312">Dit project bevat de Entity Framework-context en het bijbehorende gegevensmodel die door de front-end- en back-end worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4c999-312">This project will contain the Entity Framework context and the data model which both the front end and back end will use.</span></span> <span data-ttu-id="4c999-313">Als alternatief kan u de EF-gerelateerde klassen definiëren in het webproject en uit het project webtaak naar verwijzen.</span><span class="sxs-lookup"><span data-stu-id="4c999-313">As an alternative, you could define the EF-related classes in the web project and reference that project from the WebJob project.</span></span> <span data-ttu-id="4c999-314">Maar vervolgens uw webtaak project een verwijzing naar webassembly's, die niet noodzakelijk zou hebben.</span><span class="sxs-lookup"><span data-stu-id="4c999-314">But, then your WebJob project would have a reference to web assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="4c999-315">Voeg een consoletoepassing-project met webtaken implementatie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="4c999-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="4c999-316">Met de rechtermuisknop op het webproject (niet de oplossing of de klasse library-project) en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.</span><span class="sxs-lookup"><span data-stu-id="4c999-316">Right-click the web project (not the solution or the class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Nieuwe Azure webtaak Project menuselectie](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="4c999-318">In de **toevoegen Azure webtaak** dialoogvenster ContosoAdsWebJob invoeren als zowel de **projectnaam** en de **naam van een webtaak**.</span><span class="sxs-lookup"><span data-stu-id="4c999-318">In the **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both the **Project name** and the **WebJob name**.</span></span> <span data-ttu-id="4c999-319">Laat **webtaak uitvoeren modus** ingesteld op **continu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="4c999-319">Leave **WebJob run mode** set to **Run Continuously**.</span></span>
3. <span data-ttu-id="4c999-320">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-320">Click **OK**.</span></span>

   <span data-ttu-id="4c999-321">Visual Studio maakt een consoletoepassing die is geconfigureerd om te implementeren als een webtaak wanneer u het webproject implementeren.</span><span class="sxs-lookup"><span data-stu-id="4c999-321">Visual Studio creates a Console application that is configured to deploy as a WebJob whenever you deploy the web project.</span></span> <span data-ttu-id="4c999-322">Als u wilt dat deze de volgende taken uitgevoerd na het maken van het project:</span><span class="sxs-lookup"><span data-stu-id="4c999-322">To do that, it performed the following tasks after creating the project:</span></span>

   * <span data-ttu-id="4c999-323">Toegevoegd een *webtaak-publiceren settings.json* bestand in de eigenschappen van webtaak projectmap.</span><span class="sxs-lookup"><span data-stu-id="4c999-323">Added a *webjob-publish-settings.json* file in the WebJob project Properties folder.</span></span>
   * <span data-ttu-id="4c999-324">Toegevoegd een *webjobs list.json* bestand in de map web project eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4c999-324">Added a *webjobs-list.json* file in the web project Properties folder.</span></span>
   * <span data-ttu-id="4c999-325">Het Microsoft.Web.WebJobs.Publish NuGet-pakket in het project webtaak geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-325">Installed the Microsoft.Web.WebJobs.Publish NuGet package in the WebJob project.</span></span>

   <span data-ttu-id="4c999-326">Zie voor meer informatie over deze wijzigingen [WebJobs implementeren met behulp van Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="4c999-326">For more information about these changes, see [How to deploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="4c999-327">NuGet-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="4c999-327">Add NuGet packages</span></span>
<span data-ttu-id="4c999-328">De sjabloon nieuw project voor een webtaak project installeert automatisch de WebJobs SDK NuGet-pakket [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="4c999-328">The new-project template for a WebJob project automatically installs the WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="4c999-329">Een van de WebJobs SDK-afhankelijkheden die automatisch wordt geïnstalleerd in het project webtaak is de Azure Storage Client-bibliotheek (SCL).</span><span class="sxs-lookup"><span data-stu-id="4c999-329">One of the WebJobs SDK dependencies that is installed automatically in the WebJob project is the Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="4c999-330">U moet echter toe te voegen aan het webproject werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="4c999-330">However, you need to add it to the web project to work with blobs and queues.</span></span>

1. <span data-ttu-id="4c999-331">Open de **NuGet-pakketten beheren** dialoogvenster voor de oplossing.</span><span class="sxs-lookup"><span data-stu-id="4c999-331">Open the **Manage NuGet Packages** dialog for the solution.</span></span>
2. <span data-ttu-id="4c999-332">Selecteer in het linkerdeelvenster **geïnstalleerde pakketten**.</span><span class="sxs-lookup"><span data-stu-id="4c999-332">In the left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="4c999-333">Zoek de *Azure Storage* van het pakket en klik vervolgens op **beheren**.</span><span class="sxs-lookup"><span data-stu-id="4c999-333">Find the *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="4c999-334">In de **projecten selecteren** Selecteer de **ContosoAdsWeb** selectievakje en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="4c999-334">In the **Select Projects** box, select the **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="4c999-335">Alle drie de projecten gebruiken de Entity Framework werkt met gegevens in SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="4c999-335">All three projects use the Entity Framework to work with data in SQL Database.</span></span>
5. <span data-ttu-id="4c999-336">Selecteer in het linkerdeelvenster **Online**.</span><span class="sxs-lookup"><span data-stu-id="4c999-336">In the left pane, select **Online**.</span></span>
6. <span data-ttu-id="4c999-337">Zoek het NuGet pakket *EntityFramework* op en installeer het in alle drie de projecten.</span><span class="sxs-lookup"><span data-stu-id="4c999-337">Find the *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="4c999-338">Projectverwijzingen instellen</span><span class="sxs-lookup"><span data-stu-id="4c999-338">Set project references</span></span>
<span data-ttu-id="4c999-339">Web- en webtaak projecten werken met de SQL-database, zodat beide een verwijzing naar het project ContosoAdsCommon moeten.</span><span class="sxs-lookup"><span data-stu-id="4c999-339">Both web and WebJob projects work with the SQL database, so both need a reference to the ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="4c999-340">Stel in het project ContosoAdsWeb een verwijzing in naar het project ContosoAdsCommon.</span><span class="sxs-lookup"><span data-stu-id="4c999-340">In the ContosoAdsWeb project, set a reference to the ContosoAdsCommon project.</span></span> <span data-ttu-id="4c999-341">(Met de rechtermuisknop op het project ContosoAdsWeb en klik vervolgens op **toevoegen** > **verwijzing**.</span><span class="sxs-lookup"><span data-stu-id="4c999-341">(Right-click the ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="4c999-342">In de **Reference Manager** dialoogvenster, **projecten** > **oplossing** > **ContosoAdsCommon**, en klik vervolgens op **OK**.)</span><span class="sxs-lookup"><span data-stu-id="4c999-342">In the **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="4c999-343">Het project webtaak moet verwijzingen voor het werken met installatiekopieën en voor het openen van verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="4c999-343">The WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="4c999-344">In het project ContosoAdsWebJob, stelt u een verwijzing naar `System.Drawing` en `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="4c999-344">In the ContosoAdsWebJob project, set a reference to `System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="4c999-345">Code-en configuratiebestanden toevoegen</span><span class="sxs-lookup"><span data-stu-id="4c999-345">Add code and configuration files</span></span>
<span data-ttu-id="4c999-346">Deze zelfstudie wordt niet weergegeven hoe [maken van MVC-controllers en weergaven met steigers](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), hoe naar [schrijven van code voor Entity Framework die geschikt is voor SQL Server-databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), of [de basisbeginselen van asynchrone programmering in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="4c999-346">This tutorial does not show how to [create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how to [write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [the basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="4c999-347">Dus alles wat blijft te doen is de code en configuratie bestanden kopiëren vanuit de gedownloade oplossing naar de nieuwe oplossing.</span><span class="sxs-lookup"><span data-stu-id="4c999-347">So, all that remains to do is copy code and configuration files from the downloaded solution into the new solution.</span></span> <span data-ttu-id="4c999-348">Nadat u dat doet, wordt de volgende secties weergeven en uitgelegd van de belangrijkste onderdelen van de code.</span><span class="sxs-lookup"><span data-stu-id="4c999-348">After you do that, the following sections show and explain key parts of the code.</span></span>

<span data-ttu-id="4c999-349">Als u bestanden wilt toevoegen aan een project of map, klikt u met de rechtermuisknop op het project of de map en klikt u vervolgens op **Add** > **Existing Item**.</span><span class="sxs-lookup"><span data-stu-id="4c999-349">To add files to a project or a folder, right-click the project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="4c999-350">Selecteer de bestanden die u wilt en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4c999-350">Select the files you want and click **Add**.</span></span> <span data-ttu-id="4c999-351">Als u wordt gevraagd of u de bestaande bestanden wilt vervangen, klikt u op **Yes**.</span><span class="sxs-lookup"><span data-stu-id="4c999-351">If asked whether you want to replace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="4c999-352">Verwijder in het project ContosoAdsCommon het *Class1.cs* bestands- en toevoegen in plaats daarvan de volgende bestanden uit het gedownloade project.</span><span class="sxs-lookup"><span data-stu-id="4c999-352">In the ContosoAdsCommon project, delete the *Class1.cs* file and add in its place the following files from the downloaded project.</span></span>

   * <span data-ttu-id="4c999-353">*AD.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-353">*Ad.cs*</span></span>
   * <span data-ttu-id="4c999-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="4c999-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="4c999-356">Voeg in het project ContosoAdsWeb de volgende bestanden uit het gedownloade project toe.</span><span class="sxs-lookup"><span data-stu-id="4c999-356">In the ContosoAdsWeb project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="4c999-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="4c999-357">*Web.config*</span></span>
   * <span data-ttu-id="4c999-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="4c999-359">In de *domeincontrollers* map: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-359">In the *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="4c999-360">In de *Views\Shared* map: *_Layout.cshtml* bestand</span><span class="sxs-lookup"><span data-stu-id="4c999-360">In the *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="4c999-361">In de *Views\Home* map: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="4c999-361">In the *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="4c999-362">In de *Views\Ad* map (Maak eerst de map): vijf *.cshtml* bestanden</span><span class="sxs-lookup"><span data-stu-id="4c999-362">In the *Views\Ad* folder (create the folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="4c999-363">Voeg de volgende bestanden uit het gedownloade project in het project ContosoAdsWebJob.</span><span class="sxs-lookup"><span data-stu-id="4c999-363">In the ContosoAdsWebJob project, add the following files from the downloaded project.</span></span>

   * <span data-ttu-id="4c999-364">*App.config* (wijzigen van het type bestandsfilter **alle bestanden**)</span><span class="sxs-lookup"><span data-stu-id="4c999-364">*App.config* (change the file type filter to **All Files**)</span></span>
   * <span data-ttu-id="4c999-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-365">*Program.cs*</span></span>
   * <span data-ttu-id="4c999-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="4c999-366">*Functions.cs*</span></span>

<span data-ttu-id="4c999-367">U kunt nu samenstellen, uitvoeren en de toepassing implementeren volgens de instructies eerder in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="4c999-367">You can now build, run, and deploy the application as instructed earlier in the tutorial.</span></span> <span data-ttu-id="4c999-368">Voordat u dat doet, moet u echter de webtaak die nog steeds worden uitgevoerd in de eerste web-app die u hebt geïmplementeerd om te stoppen.</span><span class="sxs-lookup"><span data-stu-id="4c999-368">Before you do that, however, stop the WebJob that is still running in the first web app you deployed to.</span></span> <span data-ttu-id="4c999-369">Anders verwerkt die webtaak Wachtrijberichten lokaal of door de app in een nieuwe web-app wordt uitgevoerd, omdat alles met behulp van hetzelfde opslagaccount is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c999-369">Otherwise, that WebJob will process queue messages created locally or by the app running in a new web app, since all are using the same storage account.</span></span>

## <span data-ttu-id="4c999-370"><a id="code"></a>De toepassingscode bekijken</span><span class="sxs-lookup"><span data-stu-id="4c999-370"><a id="code"></a>Review the application code</span></span>
<span data-ttu-id="4c999-371">De volgende secties worden de code voor het werken met de WebJobs SDK en Azure Storage-blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="4c999-371">The following sections explain the code related to working with the WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="4c999-372">Voor de code die specifiek zijn voor de WebJobs SDK, gaat u naar de [Program.cs en Functions.cs](#programcs) secties.</span><span class="sxs-lookup"><span data-stu-id="4c999-372">For the code specific to the WebJobs SDK, go to the [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="4c999-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="4c999-374">Het bestand Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="4c999-374">The Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

        public enum Category
        {
            Cars,
            [Display(Name="Real Estate")]
            RealEstate,
            [Display(Name = "Free Stuff")]
            FreeStuff
        }

        public class Ad
        {
            public int AdId { get; set; }

            [StringLength(100)]
            public string Title { get; set; }

            public int Price { get; set; }

            [StringLength(1000)]
            [DataType(DataType.MultilineText)]
            public string Description { get; set; }

            [StringLength(1000)]
            [DisplayName("Full-size Image")]
            public string ImageURL { get; set; }

            [StringLength(1000)]
            [DisplayName("Thumbnail")]
            public string ThumbnailURL { get; set; }

            [DataType(DataType.Date)]
            [DisplayFormat(DataFormatString = "{0:yyyy-MM-dd}", ApplyFormatInEditMode = true)]
            public DateTime PostedDate { get; set; }

            public Category? Category { get; set; }
            [StringLength(12)]
            public string Phone { get; set; }
        }

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="4c999-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="4c999-376">De klasse contosoadscontext geeft aan dat de Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4c999-376">The ContosoAdsContext class specifies that the Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

        public class ContosoAdsContext : DbContext
        {
            public ContosoAdsContext() : base("name=ContosoAdsContext")
            {
            }
            public ContosoAdsContext(string connString)
                : base(connString)
            {
            }
            public System.Data.Entity.DbSet<Ad> Ads { get; set; }
        }

<span data-ttu-id="4c999-377">De klasse heeft twee constructors.</span><span class="sxs-lookup"><span data-stu-id="4c999-377">The class has two constructors.</span></span> <span data-ttu-id="4c999-378">De eerste wordt gebruikt door het webproject en specificeert de naam van een verbindingsreeks die is opgeslagen in het Web.config-bestand of de Azure-runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="4c999-378">The first is used by the web project, and specifies the name of a connection string that is stored in the Web.config file or the Azure runtime environment.</span></span> <span data-ttu-id="4c999-379">Met de tweede constructor kunt u de werkelijke verbindingsreeks doorgeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-379">The second constructor enables you to pass in the actual connection string.</span></span> <span data-ttu-id="4c999-380">Deze is nodig voor het project webtaak omdat het geen een Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="4c999-380">That is needed by the WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="4c999-381">U weet al waar deze verbindingsreeks is opgeslagen. Later ziet u hoe de code de verbindingsreeks ophaalt bij het instantiëren van de DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="4c999-381">You saw earlier where this connection string was stored, and you'll see later how the code retrieves the connection string when it instantiates the DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="4c999-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="4c999-383">De `BlobInformation` klasse wordt gebruikt voor het opslaan van informatie over een blob installatiekopie in een wachtrijbericht.</span><span class="sxs-lookup"><span data-stu-id="4c999-383">The `BlobInformation` class is used to store information about an image blob in a queue message.</span></span>

        public class BlobInformation
        {
            public Uri BlobUri { get; set; }

            public string BlobName
            {
                get
                {
                    return BlobUri.Segments[BlobUri.Segments.Length - 1];
                }
            }
            public string BlobNameWithoutExtension
            {
                get
                {
                    return Path.GetFileNameWithoutExtension(BlobName);
                }
            }
            public int AdId { get; set; }
        }


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="4c999-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="4c999-385">Code die wordt aangeroepen vanuit de `Application_Start`-methode maakt een blobcontainer met *afbeeldingen* en een wachtrij met *afbeeldingen* als deze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="4c999-385">Code that is called from the `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="4c999-386">Dit zorgt ervoor dat wanneer u met behulp van een nieuw opslagaccount begint, de vereiste blobcontainer en wachtrij automatisch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c999-386">This ensures that whenever you start using a new storage account, the required blob container and queue are created automatically.</span></span>

<span data-ttu-id="4c999-387">De code krijgt toegang tot het opslagaccount met behulp van de verbindingsreeks voor opslag van de *Web.config* bestands- of Azure runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="4c999-387">The code gets access to the storage account by using the storage connection string from the *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="4c999-388">Vervolgens wordt het een verwijzing naar de *installatiekopieën* blob-container, maakt u de container als deze niet al bestaat en stelt deze voor de nieuwe container toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="4c999-388">Then, it gets a reference to the *images* blob container, creates the container if it doesn't already exist, and sets access permissions on the new container.</span></span> <span data-ttu-id="4c999-389">Standaard staan nieuwe containers alleen clients met opslagaccountreferenties voor toegang tot blobs.</span><span class="sxs-lookup"><span data-stu-id="4c999-389">By default, new containers allow only clients with storage account credentials to access blobs.</span></span> <span data-ttu-id="4c999-390">De web-app moet de blobs openbaar zodat deze afbeeldingen met URL's die naar de afbeeldingsblobs wijzen verwijzen kan weergeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-390">The web app needs the blobs to be public so that it can display images using URLs that point to the image blobs.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        var imagesBlobContainer = blobClient.GetContainerReference("images");
        if (imagesBlobContainer.CreateIfNotExists())
        {
            imagesBlobContainer.SetPermissions(
                new BlobContainerPermissions
                {
                    PublicAccess = BlobContainerPublicAccessType.Blob
                });
        }

<span data-ttu-id="4c999-391">Vergelijkbare code wordt een verwijzing naar de *thumbnailrequest* wachtrij en een nieuwe wachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c999-391">Similar code gets a reference to the *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="4c999-392">In dit geval is er geen machtigingswijziging nodig.</span><span class="sxs-lookup"><span data-stu-id="4c999-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="4c999-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c999-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="4c999-394">Het bestand *_Layout.cshtml* stelt de naam van de app in de kop- en voettekst in en maakt een menu-item 'Ads'.</span><span class="sxs-lookup"><span data-stu-id="4c999-394">The *_Layout.cshtml* file sets the app name in the header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="4c999-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c999-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="4c999-396">Het bestand *Views\Home\Index.cshtml* geeft categoriekoppelingen weer op de startpagina.</span><span class="sxs-lookup"><span data-stu-id="4c999-396">The *Views\Home\Index.cshtml* file displays category links on the home page.</span></span> <span data-ttu-id="4c999-397">De koppelingen geven de integerwaarde van de `Category`-enum door in een queryreeksvariabele naar de pagina Ads Index.</span><span class="sxs-lookup"><span data-stu-id="4c999-397">The links pass the integer value of the `Category` enum in a querystring variable to the Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="4c999-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="4c999-399">In het bestand *AdController.cs* roept de constructor de `InitializeStorage`-methode aan voor het maken van Azure Storage Client-bibliotheekobjecten die een API leveren voor het werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="4c999-399">In the *AdController.cs* file, the constructor calls the `InitializeStorage` method to create Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="4c999-400">Vervolgens haalt de code een verwijzing naar de *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="4c999-400">Then, the code gets a reference to the *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="4c999-401">Tijdens het uitvoeren, wordt standaard ingesteld [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) geschikt is voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="4c999-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="4c999-402">Toepassing van het standaardbeleid voor opnieuw proberen met exponentieel uitstel kan ertoe leiden dat de web-app bij een tijdelijke fout langer dan een minuut blijft hangen vanwege herhaalde pogingen om het opnieuw te proberen.</span><span class="sxs-lookup"><span data-stu-id="4c999-402">The default exponential backoff retry policy could hang the web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="4c999-403">Het beleid dat hier is opgegeven, schrijft voor dat er na elke poging drie seconden wordt gewacht en dat het aantal pogingen maximaal drie bedraagt.</span><span class="sxs-lookup"><span data-stu-id="4c999-403">The retry policy specified here waits three seconds after each try for up to three tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="4c999-404">Door vergelijkbare code wordt een verwijzing naar de *afbeeldingen* wachtrij opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4c999-404">Similar code gets a reference to the *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="4c999-405">Het grootste deel van de controllercode is typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="4c999-405">Most of the controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="4c999-406">Een uitzondering is de HttpPost `Create`-methode, waarmee een bestand wordt geüpload en opgeslagen in blobopslag.</span><span class="sxs-lookup"><span data-stu-id="4c999-406">An exception is the HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="4c999-407">De modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx)-object aan de methode.</span><span class="sxs-lookup"><span data-stu-id="4c999-407">The model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object to the method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="4c999-408">Als de gebruiker een bestand heeft geselecteerd om te uploaden, wordt het door de code geüpload en opgeslagen in een blob. Tegelijkertijd wordt het Ad-databaserecord bijgewerkt met een URL die naar de blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="4c999-408">If the user selected a file to upload, the code uploads the file, saves it in a blob, and updates the Ad database record with a URL that points to the blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="4c999-409">De code die het uploaden uitvoert, bevindt zich in de `UploadAndSaveBlobAsync`-methode.</span><span class="sxs-lookup"><span data-stu-id="4c999-409">The code that does the upload is in the `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="4c999-410">Deze maakt een GUID-naam voor de blob, uploadt het bestand en slaat dit op, en retourneert een verwijzing naar de opgeslagen blob.</span><span class="sxs-lookup"><span data-stu-id="4c999-410">It creates a GUID name for the blob, uploads and saves the file, and returns a reference to the saved blob.</span></span>

        private async Task<CloudBlockBlob> UploadAndSaveBlobAsync(HttpPostedFileBase imageFile)
        {
            string blobName = Guid.NewGuid().ToString() + Path.GetExtension(imageFile.FileName);
            CloudBlockBlob imageBlob = imagesBlobContainer.GetBlockBlobReference(blobName);
            using (var fileStream = imageFile.InputStream)
            {
                await imageBlob.UploadFromStreamAsync(fileStream);
            }
            return imageBlob;
        }

<span data-ttu-id="4c999-411">Nadat de HttpPost `Create` methode een blob uploadt en de database bijwerkt, maakt deze een wachtrijbericht om te informeren over de back-endproces dat een afbeelding gereed voor conversie naar een miniatuur is.</span><span class="sxs-lookup"><span data-stu-id="4c999-411">After the HttpPost `Create` method uploads a blob and updates the database, it creates a queue message to inform the back-end process that an image is ready for conversion to a thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="4c999-412">De code voor de HttpPost `Edit` methode is vergelijkbaar, behalve dat als de gebruiker selecteert een nieuw afbeeldingsbestand, alle blobs die al bestaan voor deze advertentie moeten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4c999-412">The code for the HttpPost `Edit` method is similar, except that if the user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="4c999-413">Hier volgt de code die verwijderen van blobs wanneer u een advertentie verwijdert:</span><span class="sxs-lookup"><span data-stu-id="4c999-413">Here is the code that deletes blobs when you delete an ad:</span></span>

        private async Task DeleteAdBlobsAsync(Ad ad)
        {
            if (!string.IsNullOrWhiteSpace(ad.ImageURL))
            {
                Uri blobUri = new Uri(ad.ImageURL);
                await DeleteAdBlobAsync(blobUri);
            }
            if (!string.IsNullOrWhiteSpace(ad.ThumbnailURL))
            {
                Uri blobUri = new Uri(ad.ThumbnailURL);
                await DeleteAdBlobAsync(blobUri);
            }
        }
        private static async Task DeleteAdBlobAsync(Uri blobUri)
        {
            string blobName = blobUri.Segments[blobUri.Segments.Length - 1];
            CloudBlockBlob blobToDelete = imagesBlobContainer.GetBlockBlobReference(blobName);
            await blobToDelete.DeleteAsync();
        }

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="4c999-414">ContosoAdsWeb - Views\Ad\Index.cshtml en Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c999-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="4c999-415">De *Index.cshtml* bestand miniaturen met de ad-gegevens worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4c999-415">The *Index.cshtml* file displays thumbnails with the other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="4c999-416">De *Details.cshtml* bestand de afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4c999-416">The *Details.cshtml* file displays the full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="4c999-417">ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="4c999-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="4c999-418">De bestanden *Create.cshtml* en *Edit.cshtml* specificeren formuliercodering waarmee de controller het `HttpPostedFileBase`-object kan ophalen.</span><span class="sxs-lookup"><span data-stu-id="4c999-418">The *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables the controller to get the `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="4c999-419">Een `<input>`-element vertelt de browser dat deze een dialoogvenster voor bestandsselectie moet aanleveren.</span><span class="sxs-lookup"><span data-stu-id="4c999-419">An `<input>` element tells the browser to provide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="4c999-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="4c999-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="4c999-421">Wanneer de webtaak wordt gestart, wordt de `Main` methode roept de WebJobs SDK `JobHost.RunAndBlock` methode om te beginnen met het uitvoeren van functies in de huidige thread geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-421">When the WebJob starts, the `Main` method calls the WebJobs SDK `JobHost.RunAndBlock` method to begin execution of triggered functions on the current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="4c999-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail methode</span><span class="sxs-lookup"><span data-stu-id="4c999-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="4c999-423">De WebJobs SDK roept deze methode wanneer er een wachtrijbericht wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="4c999-423">The WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="4c999-424">De methode een miniatuur gemaakt en plaatst de miniatuur-URL in de database.</span><span class="sxs-lookup"><span data-stu-id="4c999-424">The method creates a thumbnail and puts the thumbnail URL in the database.</span></span>

        public static void GenerateThumbnail(
        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,
        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)
        {
            using (Stream output = outputBlob.OpenWrite())
            {
                ConvertImageToThumbnailJPG(input, output);
                outputBlob.Properties.ContentType = "image/jpeg";
            }

            // Entity Framework context class is not thread-safe, so it must
            // be instantiated and disposed within the function.
            using (ContosoAdsContext db = new ContosoAdsContext())
            {
                var id = blobInfo.AdId;
                Ad ad = db.Ads.Find(id);
                if (ad == null)
                {
                    throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", id.ToString()));
                }
                ad.ThumbnailURL = outputBlob.Uri.ToString();
                db.SaveChanges();
            }
        }

* <span data-ttu-id="4c999-425">De `QueueTrigger` kenmerk de WebJobs SDK deze methode niet aanroepen wanneer een nieuw bericht wordt ontvangen op de thumbnailrequest wachtrij stuurt.</span><span class="sxs-lookup"><span data-stu-id="4c999-425">The `QueueTrigger` attribute directs the WebJobs SDK to call this method when a new message is received on the thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="4c999-426">De `BlobInformation` -object in bericht in de wachtrij is automatisch gedeserialiseerde in de `blobInfo` parameter.</span><span class="sxs-lookup"><span data-stu-id="4c999-426">The `BlobInformation` object in the queue message is automatically deserialized into the `blobInfo` parameter.</span></span> <span data-ttu-id="4c999-427">Wanneer de methode is voltooid, wordt het bericht van de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="4c999-427">When the method completes, the queue message is deleted.</span></span> <span data-ttu-id="4c999-428">Als de methode is mislukt voordat wordt voltooid, wordt het bericht van de wachtrij niet verwijderd. Nadat een lease 10 minuten is verstreken, wordt het bericht beschikbaar voor het opnieuw worden opgepikt en verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4c999-428">If the method fails before completing, the queue message is not deleted; after a 10-minute lease expires, the message is released to be picked up again and processed.</span></span> <span data-ttu-id="4c999-429">Deze reeks won't voor onbepaalde tijd worden herhaald als een bericht altijd een uitzondering veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="4c999-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="4c999-430">Na 5 mislukte pogingen een bericht te verwerken, het bericht is verplaatst naar een wachtrij met de naam {wachtrijnaam}-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="4c999-430">After 5 unsuccessful attempts to process a message, the message is moved to a queue named {queuename}-poison.</span></span> <span data-ttu-id="4c999-431">Het maximum aantal pogingen kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-431">The maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="4c999-432">De twee `Blob` kenmerken Geef objecten die zijn gekoppeld aan BLOB's: een voor de bestaande installatiekopie blob en één met een nieuwe miniatuur blob die de methode wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4c999-432">The two `Blob` attributes provide objects that are bound to blobs: one to the existing image blob and one to a new thumbnail blob that the method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="4c999-433">BLOB-namen afkomstig zijn van de eigenschappen van de `BlobInformation` object in bericht in de wachtrij ontvangen (`BlobName` en `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="4c999-433">Blob names come from properties of the `BlobInformation` object received in the queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="4c999-434">Als u de volledige functionaliteit van de Storage-clientbibliotheek, kunt u de `CloudBlockBlob` klasse werken met blobs.</span><span class="sxs-lookup"><span data-stu-id="4c999-434">To get the full functionality of the Storage Client Library, you can use the `CloudBlockBlob` class to work with blobs.</span></span> <span data-ttu-id="4c999-435">Als u gebruiken als code die is geschreven wilt naar het werken met `Stream` objecten, kunt u de `Stream` klasse.</span><span class="sxs-lookup"><span data-stu-id="4c999-435">If you want to reuse code that was written to work with `Stream` objects, you can use the `Stream` class.</span></span>

<span data-ttu-id="4c999-436">Zie de volgende bronnen voor meer informatie over het schrijven van functies die WebJobs SDK kenmerken gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4c999-436">For more information about how to write functions that use  WebJobs SDK attributes, see the following resources:</span></span>

* [<span data-ttu-id="4c999-437">Azure Queue Storage gebruiken met de WebJobs-SDK</span><span class="sxs-lookup"><span data-stu-id="4c999-437">How to use Azure queue storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="4c999-438">Het gebruik van Azure Blob Storage met de WebJobs-SDK</span><span class="sxs-lookup"><span data-stu-id="4c999-438">How to use Azure blob storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="4c999-439">Azure Table Storage gebruiken met de WebJobs-SDK</span><span class="sxs-lookup"><span data-stu-id="4c999-439">How to use Azure table storage with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="4c999-440">Azure Service Bus gebruiken met de WebJobs-SDK</span><span class="sxs-lookup"><span data-stu-id="4c999-440">How to use Azure Service Bus with the WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="4c999-441">Als uw web-app wordt uitgevoerd op meerdere virtuele machines, meerdere WebJobs wordt tegelijkertijd worden uitgevoerd en in sommige scenario's die dit kan leiden tot dezelfde gegevens meerdere keren wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4c999-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in the same data getting processed multiple times.</span></span> <span data-ttu-id="4c999-442">Dit is niet een probleem als u de ingebouwde wachtrij, blobs en Service Bus-triggers.</span><span class="sxs-lookup"><span data-stu-id="4c999-442">This is not a problem if you use the built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="4c999-443">De SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.</span><span class="sxs-lookup"><span data-stu-id="4c999-443">The SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="4c999-444">Zie voor meer informatie over het correct afsluiten implementeren [correct afsluiten](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="4c999-444">For information about how to implement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="4c999-445">De code in de `ConvertImageToThumbnailJPG` methode (niet weergegeven) maakt gebruik van klassen in de `System.Drawing` naamruimte voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="4c999-445">The code in the `ConvertImageToThumbnailJPG` method (not shown) uses classes in the `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="4c999-446">De klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="4c999-446">However, the classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="4c999-447">Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service.</span><span class="sxs-lookup"><span data-stu-id="4c999-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="4c999-448">Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="4c999-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="4c999-449">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c999-449">Next steps</span></span>
<span data-ttu-id="4c999-450">In deze zelfstudie hebt u een eenvoudige toepassing met meerdere lagen die gebruikmaakt van de WebJobs SDK voor de verwerking van de back-end gezien.</span><span class="sxs-lookup"><span data-stu-id="4c999-450">In this tutorial, you've seen a simple multi-tier application that uses the WebJobs SDK for backend processing.</span></span> <span data-ttu-id="4c999-451">Deze sectie vindt u enkele suggesties voor meer informatie over toepassingen met meerdere lagen ASP.NET en WebJobs.</span><span class="sxs-lookup"><span data-stu-id="4c999-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="4c999-452">Ontbrekende functies</span><span class="sxs-lookup"><span data-stu-id="4c999-452">Missing features</span></span>
<span data-ttu-id="4c999-453">De toepassing heeft gehouden eenvoudige voor een zelfstudie aan de slag.</span><span class="sxs-lookup"><span data-stu-id="4c999-453">The application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="4c999-454">In een echte toepassing die u wilt implementeren [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) en de [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), gebruik [een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), gebruik [EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) voor het beheren van wijzigingen in het gegevensmodel en gebruik [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) voor het beheren van tijdelijke netwerkfouten.</span><span class="sxs-lookup"><span data-stu-id="4c999-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and the [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) to manage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) to manage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="4c999-455">Schalen WebJobs</span><span class="sxs-lookup"><span data-stu-id="4c999-455">Scaling WebJobs</span></span>
<span data-ttu-id="4c999-456">WebJobs uitgevoerd in de context van een web-app en zijn niet afzonderlijk worden schaalbaar.</span><span class="sxs-lookup"><span data-stu-id="4c999-456">WebJobs run in the context of a web app and are not scalable separately.</span></span> <span data-ttu-id="4c999-457">Als u een standaard web-app-exemplaar hebt, hebt u slechts één exemplaar van de achtergrondproces wordt uitgevoerd en het gebruik van een aantal van de server-resources (CPU, geheugen, enzovoort) die anders beschikbaar zijn zou voor het leveren van webinhoud.</span><span class="sxs-lookup"><span data-stu-id="4c999-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of the server resources (CPU, memory, etc.) that otherwise would be available to serve web content.</span></span>

<span data-ttu-id="4c999-458">Als het verkeer door de tijd van de dag of week varieert, en als de back-end-verwerking die u wilt kunt wachten, kunt u uw WebJobs om uit te voeren op tijdstippen met weinig verkeer kan plannen.</span><span class="sxs-lookup"><span data-stu-id="4c999-458">If traffic varies by time of day or day of week, and if the backend processing you need to do can wait, you could schedule your WebJobs to run at low-traffic times.</span></span> <span data-ttu-id="4c999-459">Als de belasting nog steeds te hoog is voor deze oplossing wordt, kunt u de back-end uitvoeren als een webtaak in een speciale afzonderlijke web-app voor dat doel.</span><span class="sxs-lookup"><span data-stu-id="4c999-459">If the load is still too high for that solution, you can run the backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="4c999-460">U kunt uw back-end-web-app vervolgens onafhankelijk van elkaar schalen van uw frontend-web-app.</span><span class="sxs-lookup"><span data-stu-id="4c999-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="4c999-461">Zie voor meer informatie [WebJobs schalen](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="4c999-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="4c999-462">Web-app time-out afsluiten-keuzelijsten voorkomen</span><span class="sxs-lookup"><span data-stu-id="4c999-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="4c999-463">Om te controleren of uw WebJobs altijd worden uitgevoerd en u hebt uitgevoerd op alle exemplaren van uw web-app, zodat de [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) functie.</span><span class="sxs-lookup"><span data-stu-id="4c999-463">To make sure your WebJobs are always running, and running on all instances of your web app, you have to enable the [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-the-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="4c999-464">Met behulp van de WebJobs SDK buiten WebJobs</span><span class="sxs-lookup"><span data-stu-id="4c999-464">Using the WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="4c999-465">Een programma dat gebruikmaakt van de WebJobs SDK beschikt niet over in Azure in een webtaak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4c999-465">A program that uses the WebJobs SDK doesn't have to run in Azure in a WebJob.</span></span> <span data-ttu-id="4c999-466">Lokaal kunt uitvoeren, en ook in andere omgevingen zoals een werkrol Cloudservice of een Windows-service kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4c999-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="4c999-467">Echter, u kunt alleen toegang tot het dashboard WebJobs SDK via een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="4c999-467">However, you can only access the WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="4c999-468">Gebruik het dashboard dat u hebt verbinding maken met de web-app van het opslagaccount dat u de verbindingsreeks AzureWebJobsDashboard door in te stellen de **configureren** tabblad van de klassieke portal.</span><span class="sxs-lookup"><span data-stu-id="4c999-468">To use the dashboard you have to connect the web app to the storage account you're using by setting the AzureWebJobsDashboard connection string on the **Configure** tab of the classic portal.</span></span> <span data-ttu-id="4c999-469">U kunt vervolgens naar het Dashboard krijgen met behulp van de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="4c999-469">Then, you can get to the Dashboard by using the following URL:</span></span>

<span data-ttu-id="4c999-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="4c999-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="4c999-471">Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling met de WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat er een oude naam van verbindingsreeks wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4c999-471">For more information, see [Getting a dashboard for local development with the WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="4c999-472">Documentatie voor meer WebJobs</span><span class="sxs-lookup"><span data-stu-id="4c999-472">More WebJobs documentation</span></span>
<span data-ttu-id="4c999-473">Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="4c999-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
