---
title: aaaCreate een webtaak .NET in Azure App Service | Microsoft Docs
description: Maak een app met meerdere lagen met ASP.NET MVC en Azure. Hallo front end wordt uitgevoerd in een web-app in Azure App Service en Hallo back-end wordt uitgevoerd als een webtaak. Hallo app gebruikmaakt van Entity Framework, SQL-Database en Azure storage-wachtrijen en blobs.
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
ms.openlocfilehash: d92fc4b81cc0d58f8e900f257e747af56d32b911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-net-webjob-in-azure-app-service"></a><span data-ttu-id="926ee-105">Een .NET-webtaak maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="926ee-105">Create a .NET WebJob in Azure App Service</span></span>
<span data-ttu-id="926ee-106">Deze zelfstudie laat zien hoe toowrite code voor een eenvoudige ASP.NET MVC 5 toepassing met meerdere lagen die gebruikmaakt van Hallo [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="926ee-106">This tutorial shows how toowrite code for a simple multi-tier ASP.NET MVC 5 application that uses hello [WebJobs SDK](websites-dotnet-webjobs-sdk.md).</span></span>

[!INCLUDE [app-service-web-webjobs-corenote](../../includes/app-service-web-webjobs-corenote.md)]

<span data-ttu-id="926ee-107">doel van Hallo Hallo [WebJobs SDK](websites-webjobs-resources.md) is toosimplify Hallo code voor algemene taken die een webtaak schrijven, zoals beeldverwerking, wachtrijbewerkingen, RSS aggregatie, onderhouden van bestanden uitvoeren kunt en e-mailberichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="926ee-107">hello purpose of hello [WebJobs SDK](websites-webjobs-resources.md) is toosimplify hello code you write for common tasks that a WebJob can perform, such as image processing, queue processing, RSS aggregation, file maintenance, and sending emails.</span></span> <span data-ttu-id="926ee-108">Hallo WebJobs SDK bevat ingebouwde functies voor het werken met Azure Storage en Service Bus, voor het plannen van taken en het afhandelen van fouten en voor veel andere veelvoorkomende scenario's.</span><span class="sxs-lookup"><span data-stu-id="926ee-108">hello WebJobs SDK has built-in features for working with Azure Storage and Service Bus, for scheduling tasks and handling errors, and for many other common scenarios.</span></span> <span data-ttu-id="926ee-109">Bovendien heeft toobe extensible ontworpen en er is een [open-source-opslagplaats voor uitbreidingen](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span><span class="sxs-lookup"><span data-stu-id="926ee-109">In addition, it's designed toobe extensible, and there's an [open source repository for extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/wiki/Binding-Extensions-Overview).</span></span>

<span data-ttu-id="926ee-110">Hallo-voorbeeldtoepassing is een bulletinboard voor advertenties.</span><span class="sxs-lookup"><span data-stu-id="926ee-110">hello sample application is an advertising bulletin board.</span></span> <span data-ttu-id="926ee-111">Gebruikers kunnen uploaden afbeeldingen voor advertenties en een back-end-proces Hallo installatiekopieën toothumbnails geconverteerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-111">Users can upload images for ads, and a backend process converts hello images toothumbnails.</span></span> <span data-ttu-id="926ee-112">pagina ad Hallo toont Hallo miniaturen en Hallo ad detailpagina toont Hallo-afbeelding.</span><span class="sxs-lookup"><span data-stu-id="926ee-112">hello ad list page shows hello thumbnails, and hello ad details page shows hello full-size image.</span></span> <span data-ttu-id="926ee-113">Hier volgt een schermafbeelding:</span><span class="sxs-lookup"><span data-stu-id="926ee-113">Here's a screenshot:</span></span>

![Advertentielijst](./media/websites-dotnet-webjobs-sdk-get-started/list.png)

<span data-ttu-id="926ee-115">Deze voorbeeldtoepassing werkt met [Azure wachtrijen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) en [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span><span class="sxs-lookup"><span data-stu-id="926ee-115">This sample application works with [Azure queues](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) and [Azure blobs](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage).</span></span> <span data-ttu-id="926ee-116">Hallo zelfstudie laat zien hoe Hallo toodeploy toepassing te[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) en [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span><span class="sxs-lookup"><span data-stu-id="926ee-116">hello tutorial shows how toodeploy hello application too[Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) and [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279).</span></span>

## <span data-ttu-id="926ee-117"><a id="prerequisites"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="926ee-117"><a id="prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="926ee-118">Hallo zelfstudie wordt ervan uitgegaan dat u weet hoe toowork met [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projecten in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="926ee-118">hello tutorial assumes that you know how toowork with [ASP.NET MVC 5](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) projects in Visual Studio.</span></span>

<span data-ttu-id="926ee-119">Hallo-zelfstudie oorspronkelijk is geschreven voor Visual Studio 2013, maar kan worden gebruikt met latere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="926ee-119">hello tutorial was originally written for Visual Studio 2013, but can be used with later versions of Visual Studio.</span></span> <span data-ttu-id="926ee-120">Als u van Visual Studio 2015 of 2017 gebruikmaakt, noteert u voordat u de toepassing hello lokaal uitvoeren, moet u de Hallo wijzigen `Data Source` deel van het SQL Server LocalDB-verbindingsreeks Hallo in Hallo Web.config en App.config-bestanden van `Data Source=(localdb)\v11.0` te`Data Source=(LocalDb)\MSSQLLocalDB`.</span><span class="sxs-lookup"><span data-stu-id="926ee-120">If you are using Visual Studio 2015 or 2017, make note that before you run hello application locally, you must change hello `Data Source` part of hello SQL Server LocalDB connection string in hello Web.config and App.config files from `Data Source=(localdb)\v11.0` too`Data Source=(LocalDb)\MSSQLLocalDB`.</span></span>

> [!NOTE]
> <span data-ttu-id="926ee-121"><a name="note"></a>Deze zelfstudie, moet u een Azure-account toocomplete hebben:</span><span class="sxs-lookup"><span data-stu-id="926ee-121"><a name="note"></a>You must have an Azure account toocomplete this tutorial:</span></span>
>
> * <span data-ttu-id="926ee-122">U kunt [gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): U ontvangt tegoed dat u tootry uit betaalde Azure-services kunt en zelfs nadat ze zijn gebruikt, kunt u Hallo account houden en gratis Azure-services, zoals Websites gebruiken.</span><span class="sxs-lookup"><span data-stu-id="926ee-122">You can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F): You get credits that you can use tootry out paid Azure services, and even after they're used up, you can keep hello account and use free Azure services, such as Websites.</span></span> <span data-ttu-id="926ee-123">Uw creditcard wordt nooit worden in rekening gebracht, tenzij u expliciet de instellingen wijzigen en vraag toobe in rekening gebracht.</span><span class="sxs-lookup"><span data-stu-id="926ee-123">Your credit card will never be charged, unless you explicitly change your settings and ask toobe charged.</span></span>
> * <span data-ttu-id="926ee-124">U kunt [maandelijkse Azure-krediet voor Visual Studio-abonnees activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): uw abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="926ee-124">You can [activate Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): Your subscription gives you credits every month that you can use for paid Azure services.</span></span>
>
> <span data-ttu-id="926ee-125">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="926ee-125">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="926ee-126">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="926ee-126">No credit cards required; no commitments.</span></span>
>
>

## <span data-ttu-id="926ee-127"><a id="learn"></a>Wat u leert</span><span class="sxs-lookup"><span data-stu-id="926ee-127"><a id="learn"></a>What you'll learn</span></span>
<span data-ttu-id="926ee-128">Hallo-zelfstudie laat zien hoe toodo Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="926ee-128">hello tutorial shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="926ee-129">Computer klaarmaken voor het ontwikkelen van Azure inschakelen door het hello Azure SDK installeren (alleen voor Visual Studio 2013 en 2015 gebruikers).</span><span class="sxs-lookup"><span data-stu-id="926ee-129">Enable your machine for Azure development by installing hello Azure SDK (only for Visual Studio 2013 and 2015 users).</span></span>
* <span data-ttu-id="926ee-130">Maak een project-consoletoepassing die automatisch wordt geïmplementeerd als een webtaak Azure wanneer u de bijbehorende Hallo-webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="926ee-130">Create a Console Application project that automatically deploys as an Azure WebJob when you deploy hello associated web project.</span></span>
* <span data-ttu-id="926ee-131">Een WebJobs SDK back-end lokaal op de ontwikkelcomputer Hallo testen.</span><span class="sxs-lookup"><span data-stu-id="926ee-131">Test a WebJobs SDK backend locally on hello development computer.</span></span>
* <span data-ttu-id="926ee-132">Publiceer een toepassing met een API-back-end tooa web-app in App Service.</span><span class="sxs-lookup"><span data-stu-id="926ee-132">Publish an application with a WebJobs backend tooa web app in App Service.</span></span>
* <span data-ttu-id="926ee-133">Bestanden uploaden en op te slaan in hello Azure Blob-service.</span><span class="sxs-lookup"><span data-stu-id="926ee-133">Upload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="926ee-134">Hello Azure WebJobs SDK toowork gebruiken met Azure Storage-wachtrijen en blobs.</span><span class="sxs-lookup"><span data-stu-id="926ee-134">Use hello Azure WebJobs SDK toowork with Azure Storage queues and blobs.</span></span>

## <span data-ttu-id="926ee-135"><a id="contosoads"></a>Toepassingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="926ee-135"><a id="contosoads"></a>Application architecture</span></span>
<span data-ttu-id="926ee-136">Hallo-voorbeeldtoepassing gebruikt Hallo [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff load Hallo CPU-intensief werk van het maken van miniatuurweergaven tooa back-end-proces.</span><span class="sxs-lookup"><span data-stu-id="926ee-136">hello sample application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa backend process.</span></span>

<span data-ttu-id="926ee-137">Hallo app slaat de advertenties in een SQL-database, met behulp van Entity Framework Code First toocreate Hallo tabellen en toegang tot Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="926ee-137">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="926ee-138">Voor elke advertentie slaat Hallo database twee URL's: één voor de afbeelding Hallo en één voor Hallo miniatuur.</span><span class="sxs-lookup"><span data-stu-id="926ee-138">For each ad, hello database stores two URLs: one for hello full-size image and one for hello thumbnail.</span></span>

![Advertentietabel](./media/websites-dotnet-webjobs-sdk-get-started/adtable.png)

<span data-ttu-id="926ee-140">Wanneer een gebruiker een installatiekopie, het Hallo-web-app uploadt, slaat Hallo-installatiekopie in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo ad informatie opslaat in de database Hallo met een URL die toohello blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="926ee-140">When a user uploads an image, hello web app stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="926ee-141">AT Hallo dezelfde tijd, wordt een bericht tooan Azure-wachtrij geschreven.</span><span class="sxs-lookup"><span data-stu-id="926ee-141">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="926ee-142">Hallo in een back-end-proces uitgevoerd als een webtaak Azure WebJobs SDK polls Hallo wachtrij voor nieuwe berichten.</span><span class="sxs-lookup"><span data-stu-id="926ee-142">In a backend process running as an Azure WebJob, hello WebJobs SDK polls hello queue for new messages.</span></span> <span data-ttu-id="926ee-143">Wanneer een nieuw bericht wordt weergegeven, Hallo webtaak maakt een miniatuur voor de betreffende afbeelding en updates Hallo miniaturen URL databaseveld voor de advertentie.</span><span class="sxs-lookup"><span data-stu-id="926ee-143">When a new message appears, hello WebJob creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="926ee-144">Hier volgt een diagram toont de wisselwerking tussen onderdelen van de toepassing hello Hallo:</span><span class="sxs-lookup"><span data-stu-id="926ee-144">Here's a diagram that shows how hello parts of hello application interact:</span></span>

![Architectuur van Contoso Ads](./media/websites-dotnet-webjobs-sdk-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]  
<span data-ttu-id="926ee-146">Hallo zelfstudie instructies gelden tooAzure SDK voor .NET 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="926ee-146">hello tutorial instructions apply tooAzure SDK for .NET 2.7.1 or later.</span></span>

## <span data-ttu-id="926ee-147"><a id="storage"></a>Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="926ee-147"><a id="storage"></a>Create an Azure Storage account</span></span>
<span data-ttu-id="926ee-148">Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij en de blob-gegevens in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-148">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span> <span data-ttu-id="926ee-149">Dit wordt ook gebruikt door Hallo WebJobs SDK toostore-logboekgegevens voor Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="926ee-149">It's also used by hello WebJobs SDK toostore logging data for hello dashboard.</span></span>

<span data-ttu-id="926ee-150">In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens en afzonderlijke accounts voor testgegevens versus productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="926ee-150">In a real-world application, you typically create separate accounts for application data versus logging data and separate accounts for test data versus production data.</span></span> <span data-ttu-id="926ee-151">Voor deze zelfstudie gebruikt u slechts één account.</span><span class="sxs-lookup"><span data-stu-id="926ee-151">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="926ee-152">Open Hallo **Server Explorer** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="926ee-152">Open hello **Server Explorer** window in Visual Studio.</span></span>
2. <span data-ttu-id="926ee-153">Klik met de rechtermuisknop Hallo **Azure** knooppunt en klik vervolgens op **tooMicrosoft Azure-abonnement verbinden...** .</span><span class="sxs-lookup"><span data-stu-id="926ee-153">Right-click hello **Azure** node, and then click **Connect tooMicrosoft Azure Subscription...**.</span></span>
   
   ![Verbinding maken met tooAzure](./media/websites-dotnet-webjobs-sdk-get-started/connaz.png)

3. <span data-ttu-id="926ee-155">Meld u aan met uw Azure-referenties.</span><span class="sxs-lookup"><span data-stu-id="926ee-155">Sign in using your Azure credentials.</span></span>
4. <span data-ttu-id="926ee-156">Met de rechtermuisknop op **opslag** onder hello Azure knooppunt en klik vervolgens op **Storage-Account maken**.</span><span class="sxs-lookup"><span data-stu-id="926ee-156">Right-click **Storage** under hello Azure node, and then click **Create Storage Account**.</span></span>
   
   ![Storage-Account maken](./media/websites-dotnet-webjobs-sdk-get-started/createstor.png)
   
5. <span data-ttu-id="926ee-158">In Hallo **Storage-Account maken** dialoogvenster, voer een naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="926ee-158">In hello **Create Storage Account** dialog, enter a name for hello storage account.</span></span>

    <span data-ttu-id="926ee-159">Hallo-naam moet uniek zijn (geen Azure storage-account kan Hallo hebben dezelfde naam).</span><span class="sxs-lookup"><span data-stu-id="926ee-159">hello name must be must be unique (no other Azure storage account can have hello same name).</span></span> <span data-ttu-id="926ee-160">Als het Hallo-naam die u invoert, wordt al gebruikt, krijgt u een kans toochange deze.</span><span class="sxs-lookup"><span data-stu-id="926ee-160">If hello name you enter is already in use, you'll get a chance toochange it.</span></span>

    <span data-ttu-id="926ee-161">Hallo URL tooaccess uw storage-account worden *{name}*. core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="926ee-161">hello URL tooaccess your storage account will be *{name}*.core.windows.net.</span></span>
6. <span data-ttu-id="926ee-162">Set Hallo **regio of Affiniteitsgroep** vervolgkeuzelijst toohello regio dichtstbijzijnde tooyou.</span><span class="sxs-lookup"><span data-stu-id="926ee-162">Set hello **Region or Affinity Group** drop-down list toohello region closest tooyou.</span></span>

    <span data-ttu-id="926ee-163">Deze instelling bepaalt u welke Azure-datacenter fungeert als host voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="926ee-163">This setting specifies which Azure datacenter will host your storage account.</span></span> <span data-ttu-id="926ee-164">Voor deze zelfstudie won't uw keuze maakt geen merkbaar verschil.</span><span class="sxs-lookup"><span data-stu-id="926ee-164">For this tutorial, your choice won't make a noticeable difference.</span></span> <span data-ttu-id="926ee-165">Voor een productie-web-app, wilt u echter uw webserver en uw storage-account toobe in Hallo dezelfde regio toominimize latentie en gegevens uitgaande kosten.</span><span class="sxs-lookup"><span data-stu-id="926ee-165">However, for a production web app, you want your web server and your storage account toobe in hello same region toominimize latency and data egress charges.</span></span> <span data-ttu-id="926ee-166">Hallo-web-app (die u later maken) datacenter moet zo dicht mogelijk toohello browsers Hallo web-app openen in volgorde toominimize latentie.</span><span class="sxs-lookup"><span data-stu-id="926ee-166">hello web app (which you'll create later) datacenter should be as close as possible toohello browsers accessing hello web app in order toominimize latency.</span></span>
7. <span data-ttu-id="926ee-167">Set Hallo **replicatie** vervolgkeuzelijst te**lokaal redundante**.</span><span class="sxs-lookup"><span data-stu-id="926ee-167">Set hello **Replication** drop-down list too**Locally redundant**.</span></span>

    <span data-ttu-id="926ee-168">Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, is Hallo opgeslagen inhoud gerepliceerde tooa secundair datacenter tooenable failover toothat locatie in het geval van een noodgeval op Hallo primaire locatie.</span><span class="sxs-lookup"><span data-stu-id="926ee-168">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover toothat location in case of a major disaster in hello primary location.</span></span> <span data-ttu-id="926ee-169">Geo-replicatie kan extra kosten met zich meebrengen.</span><span class="sxs-lookup"><span data-stu-id="926ee-169">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="926ee-170">Voor test- en -accounts in het algemeen niet de bedoeling toopay voor geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="926ee-170">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="926ee-171">Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="926ee-171">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>
8. <span data-ttu-id="926ee-172">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="926ee-172">Click **Create**.</span></span>

    ![Nieuw opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/newstorage.png)

## <span data-ttu-id="926ee-174"><a id="download"></a>Hallo-toepassing downloaden</span><span class="sxs-lookup"><span data-stu-id="926ee-174"><a id="download"></a>Download hello application</span></span>
1. <span data-ttu-id="926ee-175">Downloaden en uitpakken Hallo [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span><span class="sxs-lookup"><span data-stu-id="926ee-175">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Website-with-b4391eeb).</span></span>
2. <span data-ttu-id="926ee-176">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="926ee-176">Start Visual Studio.</span></span>
3. <span data-ttu-id="926ee-177">Van Hallo **bestand** in het menu **openen > Project/oplossing**, gaat u toowhere u Hallo oplossing gedownload en open het oplossingsbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-177">From hello **File** menu choose **Open > Project/Solution**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="926ee-178">Druk op CTRL + SHIFT + B toobuild Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="926ee-178">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="926ee-179">Standaard herstelt Visual Studio automatisch Hallo NuGet-pakketinhoud die niet is opgenomen in Hallo *.zip* bestand.</span><span class="sxs-lookup"><span data-stu-id="926ee-179">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="926ee-180">Als hello-pakketten niet worden hersteld, deze handmatig installeren door te gaan toohello **NuGet-pakketten beheren voor oplossing** dialoogvenster en te klikken op Hallo **herstellen** knop Hallo rechts bovenaan.</span><span class="sxs-lookup"><span data-stu-id="926ee-180">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="926ee-181">In **Solution Explorer**, zorg ervoor dat **ContosoAdsWeb** is geselecteerd als opstartproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-181">In **Solution Explorer**, make sure that **ContosoAdsWeb** is selected as hello startup project.</span></span>

## <span data-ttu-id="926ee-182"><a id="configurestorage"></a>Hallo toepassing toouse uw storage-account configureren</span><span class="sxs-lookup"><span data-stu-id="926ee-182"><a id="configurestorage"></a>Configure hello application toouse your storage account</span></span>
1. <span data-ttu-id="926ee-183">Open de toepassing hello *Web.config* bestand in Hallo ContosoAdsWeb-project.</span><span class="sxs-lookup"><span data-stu-id="926ee-183">Open hello application *Web.config* file in hello ContosoAdsWeb project.</span></span>

    <span data-ttu-id="926ee-184">Hallo-bestand bevat een SQL-verbindingsreeks en een Azure-opslag-verbindingsreeks voor het werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="926ee-184">hello file contains a SQL connection string and an Azure storage connection string for working with blobs and queues.</span></span>

    <span data-ttu-id="926ee-185">Hallo SQL-verbindingsreeks verwijst tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span><span class="sxs-lookup"><span data-stu-id="926ee-185">hello SQL connection string points tooa [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database.</span></span>

    <span data-ttu-id="926ee-186">Hallo-verbindingsreeks voor opslag is een voorbeeld van tijdelijke aanduidingen voor Hallo storage account naam en toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="926ee-186">hello storage connection string is an example that has placeholders for hello storage account name and access key.</span></span> <span data-ttu-id="926ee-187">U hebt deze vervangen met een verbindingsreeks met Hallo naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="926ee-187">You'll replace this with a connection string that has hello name and key of your storage account.</span></span>  

    ```
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
        <add name="AzureWebJobsStorage" connectionString="DefaultEndpointsProtocol=https;AccountName=[accountname];AccountKey=[accesskey]"/>
    </connectionStrings>
    ```
    <span data-ttu-id="926ee-188">Hallo-verbindingsreeks voor opslag is standaard de naam AzureWebJobsStorage omdat dat Hallo naam Hallo die webjobs SDK wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="926ee-188">hello storage connection string is named AzureWebJobsStorage because that's hello name hello WebJobs SDK uses by default.</span></span> <span data-ttu-id="926ee-189">Hallo dezelfde naam hier gebruikt wordt zodat u tooset slechts één gegevensbronwaarde in hello Azure-omgeving hebt.</span><span class="sxs-lookup"><span data-stu-id="926ee-189">hello same name is used here so you have tooset only one connection string value in hello Azure environment.</span></span>
2. <span data-ttu-id="926ee-190">In **Server Explorer**, met de rechtermuisknop op uw opslagaccount onder Hallo **opslag** knooppunt en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-190">In **Server Explorer**, right-click your storage account under hello **Storage** node, and then click **Properties**.</span></span>

    ![Klik op Eigenschappen van het Opslagaccount](./media/websites-dotnet-webjobs-sdk-get-started/storppty.png)
3. <span data-ttu-id="926ee-192">In Hallo **eigenschappen** venster, klikt u op **Opslagaccountsleutels**, en klik vervolgens op Hallo weglatingsteken.</span><span class="sxs-lookup"><span data-stu-id="926ee-192">In hello **Properties** window, click **Storage Account Keys**, and then click hello ellipsis.</span></span>

    ![Toegangscodes voor opslag](./media/websites-dotnet-webjobs-sdk-get-started/stor-account-keys.png)
4. <span data-ttu-id="926ee-194">Kopiëren Hallo **verbindingsreeks**.</span><span class="sxs-lookup"><span data-stu-id="926ee-194">Copy hello **Connection String**.</span></span>

    ![Opslag toegangscodes dialoogvenster](./media/websites-dotnet-webjobs-sdk-get-started/cpak.png)
5. <span data-ttu-id="926ee-196">Vervang Hallo verbindingsreeks voor opslag in Hallo *Web.config* bestand met de Hallo-verbindingsreeks die u zojuist hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-196">Replace hello storage connection string in hello *Web.config* file with hello connection string you just copied.</span></span> <span data-ttu-id="926ee-197">Zorg ervoor dat u Alles selecteren binnen de aanhalingstekens Hallo maar niet inclusief de aanhalingstekens Hallo voordat u gaat plakken.</span><span class="sxs-lookup"><span data-stu-id="926ee-197">Make sure you select everything inside hello quotation marks but not including hello quotation marks before pasting.</span></span>
6. <span data-ttu-id="926ee-198">Open Hallo *App.config* bestand in Hallo ContosoAdsWebJob project.</span><span class="sxs-lookup"><span data-stu-id="926ee-198">Open hello *App.config* file in hello ContosoAdsWebJob project.</span></span>

    <span data-ttu-id="926ee-199">Dit bestand heeft twee storage-verbindingsreeksen, één voor toepassingsgegevens en één voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="926ee-199">This file has two storage connection strings, one for application data and one for logging.</span></span> <span data-ttu-id="926ee-200">U kunt afzonderlijke storage-accounts voor toepassingsgegevens en logboekregistratie en kunt u [meerdere opslagaccounts voor gegevens](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span><span class="sxs-lookup"><span data-stu-id="926ee-200">You can use separate storage accounts for application data and logging, and you can use [multiple storage accounts for data](https://github.com/Azure/azure-webjobs-sdk/blob/master/test/Microsoft.Azure.WebJobs.Host.EndToEndTests/MultipleStorageAccountsEndToEndTests.cs).</span></span> <span data-ttu-id="926ee-201">Voor deze zelfstudie maakt u een één opslagaccount gebruikt.</span><span class="sxs-lookup"><span data-stu-id="926ee-201">For this tutorial, you'll use a single storage account.</span></span> <span data-ttu-id="926ee-202">Hallo-verbindingsreeksen hebben tijdelijke aanduidingen voor Hallo opslagaccountsleutels.</span><span class="sxs-lookup"><span data-stu-id="926ee-202">hello connection strings have placeholders for hello storage account keys.</span></span>

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

    <span data-ttu-id="926ee-203">Standaard zoekt Hallo WebJobs SDK met de naam AzureWebJobsStorage en AzureWebJobsDashboard verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="926ee-203">By default, hello WebJobs SDK looks for connection strings named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="926ee-204">Als alternatief kunt u [Hallo verbindingsreeks opslaan, maar u wilt en geef dit door in expliciet toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span><span class="sxs-lookup"><span data-stu-id="926ee-204">As an alternative, you can [store hello connection string however you want and pass it in explicitly toohello `JobHost` object](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#config).</span></span>
7. <span data-ttu-id="926ee-205">Beide storage-verbindingsreeksen vervangen door Hallo-verbindingsreeks die u eerder hebt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-205">Replace both storage connection strings with hello connection string you copied earlier.</span></span>
8. <span data-ttu-id="926ee-206">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="926ee-206">Save your changes.</span></span>

## <span data-ttu-id="926ee-207"><a id="run"></a>Hallo-toepassing lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="926ee-207"><a id="run"></a>Run hello application locally</span></span>
1. <span data-ttu-id="926ee-208">toostart hello web frontend toepassing hello, druk op CTRL + F5.</span><span class="sxs-lookup"><span data-stu-id="926ee-208">toostart hello web frontend of hello application, press CTRL+F5.</span></span>

    <span data-ttu-id="926ee-209">Hallo standaardbrowser geopend toohello startpagina.</span><span class="sxs-lookup"><span data-stu-id="926ee-209">hello default browser opens toohello home page.</span></span> <span data-ttu-id="926ee-210">(Hallo-webproject wordt uitgevoerd, omdat u deze hebt aangebracht Hallo opstartproject.)</span><span class="sxs-lookup"><span data-stu-id="926ee-210">(hello web project runs because you've made it hello startup project.)</span></span>

    ![Contoso Ads-startpagina](./media/websites-dotnet-webjobs-sdk-get-started/home.png)
2. <span data-ttu-id="926ee-212">toostart hello webtaak-back-end van de toepassing hello, met de rechtermuisknop op Hallo ContosoAdsWebJob project in **Solution Explorer**, en klik vervolgens op **Debug** > **nieuw exemplaar gestart** .</span><span class="sxs-lookup"><span data-stu-id="926ee-212">toostart hello WebJob backend of hello application, right-click hello ContosoAdsWebJob project in **Solution Explorer**, and then click **Debug** > **Start new instance**.</span></span>

    <span data-ttu-id="926ee-213">Een toepassing consolevenster opent en toont berichtregistratie die aangeeft Hallo WebJobs SDK JobHost object toorun is begonnen.</span><span class="sxs-lookup"><span data-stu-id="926ee-213">A console application window opens and displays logging messages indicating hello WebJobs SDK JobHost object has started toorun.</span></span>

    ![Toepassing consolevenster weergegeven die backend hello wordt uitgevoerd](./media/websites-dotnet-webjobs-sdk-get-started/backendrunning.png)
3. <span data-ttu-id="926ee-215">Klik in uw browser **maken een advertentie**.</span><span class="sxs-lookup"><span data-stu-id="926ee-215">In your browser, click  **Create an Ad**.</span></span>
4. <span data-ttu-id="926ee-216">Voer enkele testgegevens, selecteert u een installatiekopie tooupload en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="926ee-216">Enter some test data, select an image tooupload, and then click **Create**.</span></span>

    ![De pagina Create](./media/websites-dotnet-webjobs-sdk-get-started/create.png)

    <span data-ttu-id="926ee-218">Hallo app gaat toohello indexpagina, maar niet wordt weergegeven een miniatuur voor de nieuwe ad Hallo omdat die verwerking nog niet heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="926ee-218">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>

    <span data-ttu-id="926ee-219">Ondertussen na een korte wachten logboekregistratie in een bericht in de toepassing consolevenster Hallo aangegeven dat een wachtrijbericht is ontvangen en is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="926ee-219">Meanwhile, after a short wait a logging message in hello console application window shows that a queue message was received and has been processed.</span></span>

    ![Toepassing consolevenster weergegeven dat er een wachtrijbericht is verwerkt](./media/websites-dotnet-webjobs-sdk-get-started/backendlogs.png)
5. <span data-ttu-id="926ee-221">Nadat u logboekregistratie van berichten in de toepassing consolevenster Hallo Hallo ziet, Hallo Index pagina toosee Hallo miniatuur vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="926ee-221">After you see hello logging messages in hello console application window, refresh hello Index page toosee hello thumbnail.</span></span>

    ![De indexpagina](./media/websites-dotnet-webjobs-sdk-get-started/list.png)
6. <span data-ttu-id="926ee-223">Klik op **Details** voor uw afbeelding van ad toosee Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-223">Click **Details** for your ad toosee hello full-size image.</span></span>

    ![De pagina Details](./media/websites-dotnet-webjobs-sdk-get-started/details.png)

<span data-ttu-id="926ee-225">U hebt is Hallo toepassing uitvoeren op uw lokale computer en deze gebruik maakt van een SQL Server-database op de computer, maar werkt met wachtrijen en blobs in Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="926ee-225">You've been running hello application on your local computer, and it's using a SQL Server database located on your computer, but it's working with queues and blobs in hello cloud.</span></span> <span data-ttu-id="926ee-226">In de volgende sectie Hallo voert u de toepassing hello in de cloud Hallo, met behulp van een cloud-database, evenals cloud blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="926ee-226">In hello following section you'll run hello application in hello cloud, using a cloud database as well as cloud blobs and queues.</span></span>  

## <span data-ttu-id="926ee-227"><a id="runincloud"></a>Hallo-toepassing uitvoeren in de cloud Hallo</span><span class="sxs-lookup"><span data-stu-id="926ee-227"><a id="runincloud"></a>Run hello application in hello cloud</span></span>
<span data-ttu-id="926ee-228">U voert de volgende stappen toorun Hallo toepassing in de cloud Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="926ee-228">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="926ee-229">TooWeb Apps implementeren.</span><span class="sxs-lookup"><span data-stu-id="926ee-229">Deploy tooWeb Apps.</span></span> <span data-ttu-id="926ee-230">Visual Studio maakt automatisch een nieuwe web-app in App Service en een exemplaar van SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="926ee-230">Visual Studio automatically creates a new web app in App Service and a SQL Database instance.</span></span>
* <span data-ttu-id="926ee-231">Hallo web app toouse uw Azure SQL database- en storage-account configureren.</span><span class="sxs-lookup"><span data-stu-id="926ee-231">Configure hello web app toouse your Azure SQL database and storage account.</span></span>

<span data-ttu-id="926ee-232">Nadat u advertenties hebt gemaakt tijdens het uitvoeren van de cloud hello, bekijkt u Hallo WebJobs SDK dashboard toosee Hallo uitgebreide bewakingsfuncties toooffer heeft.</span><span class="sxs-lookup"><span data-stu-id="926ee-232">After you've created some ads while running in hello cloud, you'll view hello WebJobs SDK dashboard toosee hello rich monitoring features it has toooffer.</span></span>

### <a name="deploy-tooweb-apps"></a><span data-ttu-id="926ee-233">TooWeb Apps implementeren</span><span class="sxs-lookup"><span data-stu-id="926ee-233">Deploy tooWeb Apps</span></span>

1. <span data-ttu-id="926ee-234">Hallo-browser en Hallo-consolevenster toepassing sluiten.</span><span class="sxs-lookup"><span data-stu-id="926ee-234">Close hello browser and hello console application window.</span></span>
2. <span data-ttu-id="926ee-235">Volg de stappen Hallo in Hallo [tooAzure met SQL Database publiceren](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) sectie.</span><span class="sxs-lookup"><span data-stu-id="926ee-235">Follow hello steps in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) section.</span></span>
3. <span data-ttu-id="926ee-236">Nadat u de stappen voor het implementeren van Hallo hebt voltooid, kunt u doorgaan met de Hallo resterende taken in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="926ee-236">After you complete hello steps for deploying, continue with hello remaining tasks in this article.</span></span>

### <a name="configure-hello-web-app-toouse-your-azure-sql-database-and-storage-account"></a><span data-ttu-id="926ee-237">Hallo web app toouse uw Azure SQL database- en storage-account configureren</span><span class="sxs-lookup"><span data-stu-id="926ee-237">Configure hello web app toouse your Azure SQL database and storage account</span></span>
<span data-ttu-id="926ee-238">Er is een best practice bij beveiliging te[te voorkomen dat gevoelige informatie zoals verbindingsreeksen in bestanden die zijn opgeslagen in broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="926ee-238">It's a security best practice too[avoid putting sensitive information such as connection strings in files that are stored in source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span> <span data-ttu-id="926ee-239">Azure biedt een manier toodo: u kunt de verbindingstekenreeks en andere instellingswaarden in hello Azure-omgeving instellen en ASP.NET-configuratie API's automatisch kunnen worden opgepikt deze waarden als Hallo-app wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="926ee-239">Azure provides a way toodo that: you can set connection string and other setting values in hello Azure environment, and ASP.NET configuration APIs automatically pick up these values when hello app runs in Azure.</span></span> <span data-ttu-id="926ee-240">U kunt deze waarden instellen in Azure met behulp van **Server Explorer**, hello Azure-Portal Windows PowerShell of Hallo platformoverschrijdende opdrachtregelinterface.</span><span class="sxs-lookup"><span data-stu-id="926ee-240">You can set these values in Azure by using **Server Explorer**, hello Azure Portal, Windows PowerShell, or hello cross-platform command-line interface.</span></span> <span data-ttu-id="926ee-241">Zie voor meer informatie [tekenreeksen van toepassingen en verbindingsreeksen](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="926ee-241">For more information, see [How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span>

<span data-ttu-id="926ee-242">In deze sectie gebruikt u **Server Explorer** tooset de waarden van verbindingsreeksen in Azure.</span><span class="sxs-lookup"><span data-stu-id="926ee-242">In this section, you use **Server Explorer** tooset connection string values in Azure.</span></span>

1. <span data-ttu-id="926ee-243">In **Server Explorer**, met de rechtermuisknop op uw web-app onder **Azure > App Service > {uw resourcegroep}**, en klik vervolgens op **weergave-instellingen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-243">In **Server Explorer**, right-click your web app under **Azure > App Service > {your resource group}**, and then click **View Settings**.</span></span>

    <span data-ttu-id="926ee-244">Hallo **Azure-Web-App** venster wordt geopend op Hallo **configuratie** tabblad.</span><span class="sxs-lookup"><span data-stu-id="926ee-244">hello **Azure Web App** window opens on hello **Configuration** tab.</span></span>
2. <span data-ttu-id="926ee-245">Hallo naam wijzigen van Hallo DefaultConnection toohello verbindingsreeksnaam u hebt gekozen als u Hallo SQL-database geconfigureerd in Hallo [tooAzure met SQL Database publiceren](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) artikel.</span><span class="sxs-lookup"><span data-stu-id="926ee-245">Change hello name of hello DefaultConnection connection string toohello name you chose when you configured hello SQL database in hello [Publish tooAzure with SQL Database](https://docs.microsoft.com/azure/app-service-web/app-service-web-tutorial-dotnet-sqldatabase#publish-to-azure-with-sql-database) article.</span></span>

    <span data-ttu-id="926ee-246">Deze verbindingsreeks Azure automatisch gemaakt wanneer u Hallo web-app met een bijbehorende database gemaakt, zodat het Hallo rechts gegevensbronwaarde al heeft.</span><span class="sxs-lookup"><span data-stu-id="926ee-246">Azure automatically created this connection string when you created hello web app with an associated database, so it already has hello right connection string value.</span></span> <span data-ttu-id="926ee-247">U kunt alleen Hallo naam-toowhat naar uw code zoekt wilt wijzigen.</span><span class="sxs-lookup"><span data-stu-id="926ee-247">You're changing just hello name toowhat your code is looking for.</span></span>
3. <span data-ttu-id="926ee-248">Twee nieuwe verbindingsreeksen, met de naam AzureWebJobsStorage en AzureWebJobsDashboard toevoegen.</span><span class="sxs-lookup"><span data-stu-id="926ee-248">Add two new connection strings, named AzureWebJobsStorage and AzureWebJobsDashboard.</span></span> <span data-ttu-id="926ee-249">Hallo databasetype te ingesteld**aangepaste**, en set Hallo verbinding tekenreeks waarde toohello dezelfde waarde die u hebt eerder voor Hallo gebruikt *Web.config* en *App.config* bestanden.</span><span class="sxs-lookup"><span data-stu-id="926ee-249">Set hello database type too**Custom**, and set hello connection string value toohello same value that you used earlier for hello *Web.config* and *App.config* files.</span></span> <span data-ttu-id="926ee-250">(Zorg ervoor u Hallo hele verbindingsreeks, niet alleen Hallo-toegangssleutel, opneemt en Hallo aanhalingstekens zijn niet opgenomen.)</span><span class="sxs-lookup"><span data-stu-id="926ee-250">(Be sure you include hello entire connection string, not just hello access key, and don't include hello quotation marks.)</span></span>

    <span data-ttu-id="926ee-251">Deze verbindingsreeksen worden gebruikt door Hallo WebJobs SDK, één voor toepassingsgegevens en één voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="926ee-251">These connection strings are used by hello WebJobs SDK, one for application data and one for logging.</span></span> <span data-ttu-id="926ee-252">Als u eerder hebt gezien, wordt Hallo voor toepassingsgegevens worden ook gebruikt door Hallo web-front-code.</span><span class="sxs-lookup"><span data-stu-id="926ee-252">As you saw earlier, hello one for application data is also used by hello web front-end code.</span></span>
4. <span data-ttu-id="926ee-253">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="926ee-253">Click **Save**.</span></span>

    ![Verbindingsreeksen in Azure Portal](./media/websites-dotnet-webjobs-sdk-get-started/azconnstr.png)
5. <span data-ttu-id="926ee-255">In **Server Explorer**, met de rechtermuisknop op het Hallo-web-app en klik vervolgens op **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-255">In **Server Explorer**, right-click hello web app, and then click **Stop**.</span></span>
6. <span data-ttu-id="926ee-256">Nadat het Hallo-web-app stopt, opnieuw met de rechtermuisknop op Hallo web-app en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="926ee-256">After hello web app stops, right-click hello web app again, and then click **Start**.</span></span>

   <span data-ttu-id="926ee-257">Hallo webtaak wordt automatisch gestart wanneer u publiceren, maar stopt wanneer u een configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="926ee-257">hello WebJob automatically starts when you publish, but it stops when you make a configuration change.</span></span> <span data-ttu-id="926ee-258">toorestart, kunt u Hallo web-app te starten of opnieuw opstarten Hallo webtaak in Hallo [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span><span class="sxs-lookup"><span data-stu-id="926ee-258">toorestart it, you can either restart hello web app or restart hello WebJob in hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715).</span></span> <span data-ttu-id="926ee-259">Het is doorgaans aanbevolen toorestart Hallo web-app na een configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="926ee-259">It's generally recommended toorestart hello web app after a configuration change.</span></span>
7. <span data-ttu-id="926ee-260">Hallo-browservenster met Hallo web-app-URL in de adresbalk vernieuwen.</span><span class="sxs-lookup"><span data-stu-id="926ee-260">Refresh hello browser window that has hello web app URL in its address bar.</span></span>

    <span data-ttu-id="926ee-261">Hallo-startpagina wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="926ee-261">hello home page appears.</span></span>
8. <span data-ttu-id="926ee-262">Maken van een advertentie, net als wanneer u [Hallo toepassing lokaal uitgevoerd](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span><span class="sxs-lookup"><span data-stu-id="926ee-262">Create an ad, as you did when you [ran hello application locally](https://docs.microsoft.com/azure/app-service-web/websites-dotnet-webjobs-sdk-get-started#a-idrunarun-the-application-locally).</span></span>

   <span data-ttu-id="926ee-263">Hallo indexpagina wordt weergegeven zonder een miniatuur in eerste instantie.</span><span class="sxs-lookup"><span data-stu-id="926ee-263">hello Index page shows without a thumbnail at first.</span></span>
9. <span data-ttu-id="926ee-264">Vernieuw Hallo pagina na enkele seconden en hello miniatuur weergegeven.</span><span class="sxs-lookup"><span data-stu-id="926ee-264">Refresh hello page after a few seconds and hello thumbnail appears.</span></span>

   <span data-ttu-id="926ee-265">Als de miniatuur Hallo niet wordt weergegeven, wellicht u toowait een minuut voor Hallo webtaak toorestart.</span><span class="sxs-lookup"><span data-stu-id="926ee-265">If hello thumbnail doesn't appear, you might have toowait a minute or so for hello WebJob toorestart.</span></span> <span data-ttu-id="926ee-266">Als u na een tijdje u nog steeds ziet niet Hallo miniatuur bij het vernieuwen van Hallo pagina Hallo webtaak niet automatisch hebt gestart.</span><span class="sxs-lookup"><span data-stu-id="926ee-266">If after a while, you still don't see hello thumbnail when you refresh hello page, hello WebJob might not have started automatically.</span></span> <span data-ttu-id="926ee-267">In dat geval gaan toohello **App Services** blade in Hallo [Azure-portal](https://portal.azure.com/), zoek uw web-app en klik vervolgens op **Start**.</span><span class="sxs-lookup"><span data-stu-id="926ee-267">In that case, go toohello **App Services** blade in hello [Azure portal](https://portal.azure.com/), locate your web app, and then click **Start**.</span></span>

### <a name="view-hello-webjobs-sdk-dashboard"></a><span data-ttu-id="926ee-268">Weergave Hallo WebJobs SDK-dashboard</span><span class="sxs-lookup"><span data-stu-id="926ee-268">View hello WebJobs SDK dashboard</span></span>
1. <span data-ttu-id="926ee-269">In Hallo [Azure-portal](https://portal.azure.com/), selecteer Hallo **blade App Services**, Ga naar uw web-app en selecteer **WebJobs**.</span><span class="sxs-lookup"><span data-stu-id="926ee-269">In hello [Azure portal](https://portal.azure.com/), select hello **App Services blade**, locate your web app, and select **WebJobs**.</span></span>
3. <span data-ttu-id="926ee-270">Selecteer Hallo **logboeken** tabblad.</span><span class="sxs-lookup"><span data-stu-id="926ee-270">Select hello **Logs** tab.</span></span>

    ![Tabblad Logboeken](./media/websites-dotnet-webjobs-sdk-get-started/log-tab.png)

    <span data-ttu-id="926ee-272">Een nieuw browsertabblad geopend toohello WebJobs SDK-dashboard.</span><span class="sxs-lookup"><span data-stu-id="926ee-272">A new browser tab opens toohello WebJobs SDK dashboard.</span></span> <span data-ttu-id="926ee-273">Hallo-dashboard ziet u dat Hallo webtaak wordt uitgevoerd en wordt een lijst met functies in uw code die Hallo die webjobs SDK wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-273">hello dashboard shows that hello WebJob is running and shows a list of functions in your code that hello WebJobs SDK triggered.</span></span>
4. <span data-ttu-id="926ee-274">Klik op een Hallo functies toosee details over de uitvoering ervan.</span><span class="sxs-lookup"><span data-stu-id="926ee-274">Click one of hello functions toosee details about its execution.</span></span>

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjdashboardhome.png)

    ![WebJobs SDK-dashboard](./media/websites-dotnet-webjobs-sdk-get-started/wjfunctiondetails.png)

    <span data-ttu-id="926ee-277">Hallo **Replay-functie** op deze pagina wordt knop Hallo WebJobs SDK framework toocall Hallo functie opnieuw, en geeft u een kans toochange Hallo doorgegeven toohello functie eerst.</span><span class="sxs-lookup"><span data-stu-id="926ee-277">hello **Replay Function** button on this page causes hello WebJobs SDK framework toocall hello function again, and it gives you a chance toochange hello data passed toohello function first.</span></span>

> [!NOTE]
> <span data-ttu-id="926ee-278">Wanneer u klaar bent met testen, kunt u eventueel de Hallo web-app, storage-account en uw exemplaar van SQL-Database verwijderen.</span><span class="sxs-lookup"><span data-stu-id="926ee-278">When you're finished testing, consider deleting hello web app, storage account, and your SQL Database instance.</span></span> <span data-ttu-id="926ee-279">Hallo-web-app is gratis, maar Hallo storage-account voor SQL en database-exemplaar doorlopen kosten (zij, minimale vanwege toohello klein).</span><span class="sxs-lookup"><span data-stu-id="926ee-279">hello web app is free, but hello SQL storage account and database instance accrue charges (albeit, minimal due toohello small size).</span></span> <span data-ttu-id="926ee-280">Ook als u niets Hallo web-app die wordt uitgevoerd, kunt iedereen die uw URL vindt advertenties maken en weergeven.</span><span class="sxs-lookup"><span data-stu-id="926ee-280">Also, if you leave hello web app running, anyone who finds your URL can create and view ads.</span></span> 
>
>

### <a name="delete-your-web-app"></a><span data-ttu-id="926ee-281">Uw web-app verwijderen</span><span class="sxs-lookup"><span data-stu-id="926ee-281">Delete your web app</span></span>
<span data-ttu-id="926ee-282">Ga in de portal voor Hallo toohello **App Services** blade Zoek en selecteer uw web-app en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-282">In hello portal, go toohello **App Services** blade, locate and select your web app, and then click **Delete**.</span></span> <span data-ttu-id="926ee-283">Als u alleen wilt tootemporarily voorkomen dat anderen toegang hebben tot de web-app hello, klikt u op **stoppen** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="926ee-283">If you just want tootemporarily prevent others from accessing hello web app, click **Stop** instead.</span></span> <span data-ttu-id="926ee-284">In dat geval blijven de kosten tooaccrue voor Hallo SQL-Database en het Opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="926ee-284">In that case, charges will continue tooaccrue for hello SQL Database and Storage account.</span></span>

### <a name="delete-your-storage-account"></a><span data-ttu-id="926ee-285">Uw storage-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="926ee-285">Delete your storage account</span></span>
<span data-ttu-id="926ee-286">toodelete uw storage-account, Zie [een opslagaccount verwijderen](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="926ee-286">toodelete your storage account, see [Delete a storage account](https://docs.microsoft.com/azure/storage/storage-create-storage-account#delete-a-storage-account).</span></span> 

### <a name="delete-your-database"></a><span data-ttu-id="926ee-287">Uw database verwijderen</span><span class="sxs-lookup"><span data-stu-id="926ee-287">Delete your database</span></span>
<span data-ttu-id="926ee-288">toodelete uw SQL database, Zie Hallo [REST-API van Azure SQL Database](https://docs.microsoft.com/rest/api/sql/) documentatie.</span><span class="sxs-lookup"><span data-stu-id="926ee-288">toodelete your SQL database, see hello [Azure SQL Database REST API](https://docs.microsoft.com/rest/api/sql/) documentation.</span></span>

## <span data-ttu-id="926ee-289"><a id="create"></a>Hallo toepassing vanaf het begin maken</span><span class="sxs-lookup"><span data-stu-id="926ee-289"><a id="create"></a>Create hello application from scratch</span></span>
<span data-ttu-id="926ee-290">In deze sectie, doet u Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="926ee-290">In this section you'll do hello following tasks:</span></span>

* <span data-ttu-id="926ee-291">Een Visual Studio-oplossing maken met een webproject.</span><span class="sxs-lookup"><span data-stu-id="926ee-291">Create a Visual Studio solution with a web project.</span></span>
* <span data-ttu-id="926ee-292">Voeg een klasse bibliotheek-project voor Hallo gegevens toegang laag die wordt gedeeld tussen Hallo front-end en back-end.</span><span class="sxs-lookup"><span data-stu-id="926ee-292">Add a class library project for hello data access layer that is shared between hello front end and back end.</span></span>
* <span data-ttu-id="926ee-293">Voeg een project-consoletoepassing voor back-end van Hallo met WebJobs-implementatie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="926ee-293">Add a Console Application project for hello backend, with WebJobs deployment enabled.</span></span>
* <span data-ttu-id="926ee-294">NuGet-pakketten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="926ee-294">Add NuGet packages.</span></span>
* <span data-ttu-id="926ee-295">Projectverwijzingen instellen.</span><span class="sxs-lookup"><span data-stu-id="926ee-295">Set project references.</span></span>
* <span data-ttu-id="926ee-296">Kopieer toepassingsbestanden code en configuratie uit gedownload Hallo-toepassing die u in de vorige sectie Hallo Hallo-zelfstudie hebt gewerkt.</span><span class="sxs-lookup"><span data-stu-id="926ee-296">Copy application code and configuration files from hello downloaded application that you worked with in hello previous section of hello tutorial.</span></span>
* <span data-ttu-id="926ee-297">Bekijk Hallo delen Hallo-code die werken met Azure blobs en wachtrijen en Hallo WebJobs SDK.</span><span class="sxs-lookup"><span data-stu-id="926ee-297">Review hello parts of hello code that work with Azure blobs and queues and hello WebJobs SDK.</span></span>

### <a name="create-a-visual-studio-solution-with-a-web-project-and-class-library-project"></a><span data-ttu-id="926ee-298">Een Visual Studio-oplossing maken met een webproject en class library-project</span><span class="sxs-lookup"><span data-stu-id="926ee-298">Create a Visual Studio solution with a web project and class library project</span></span>
1. <span data-ttu-id="926ee-299">Kies in Visual Studio **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="926ee-299">In Visual Studio, choose **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="926ee-300">In Hallo **nieuw Project** dialoogvenster kiezen **Visual C#** > **Web** > **ASP.NET-webtoepassing (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="926ee-300">In hello **New Project** dialog, choose **Visual C#** > **Web** > **ASP.NET Web Application (.NET Framework)**.</span></span>
3. <span data-ttu-id="926ee-301">Noem Hallo project ContosoAdsWeb en geef de naam Hallo oplossing ContosoAdsWebJobsSDK (Hallo oplossingsnaam wijzigen als u deze wilt opslaan in Hallo dezelfde map als Hallo gedownload oplossing), en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-301">Name hello project ContosoAdsWeb, name hello solution ContosoAdsWebJobsSDK (change hello solution name if you're putting it in hello same folder as hello downloaded solution), and then click **OK**.</span></span>

    ![Nieuw project](./media/websites-dotnet-webjobs-sdk-get-started/newproject.png)
4. <span data-ttu-id="926ee-303">In Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster Hallo MVC-sjabloon kiest en selecteert u **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-303">In hello **New ASP.NET Web Application** dialog, choose hello MVC template, and select **Change Authentication**.</span></span>

    ![Verificatie wijzigen](./media/websites-dotnet-webjobs-sdk-get-started/chgauth.png)
5. <span data-ttu-id="926ee-305">In Hallo **verificatie wijzigen** dialoogvenster kiezen **geen verificatie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-305">In hello **Change Authentication** dialog, choose **No Authentication**, and then click **OK**.</span></span>

    ![Geen verificatie](./media/websites-dotnet-webjobs-sdk-get-started/noauth.png)
6. <span data-ttu-id="926ee-307">In Hallo **nieuwe ASP.NET-webtoepassing** dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-307">In hello **New ASP.NET Web Application** dialog, click **OK**.</span></span>

    <span data-ttu-id="926ee-308">Visual Studio maakt het Hallo-oplossing en Hallo-webproject.</span><span class="sxs-lookup"><span data-stu-id="926ee-308">Visual Studio creates hello solution and hello web project.</span></span>
7. <span data-ttu-id="926ee-309">In **Solution Explorer**, met de rechtermuisknop op het Hallo-oplossing (niet Hallo project) en kies **toevoegen** > **nieuw Project**.</span><span class="sxs-lookup"><span data-stu-id="926ee-309">In **Solution Explorer**, right-click hello solution (not hello project), and choose **Add** > **New Project**.</span></span>
8. <span data-ttu-id="926ee-310">In Hallo **Add New Project** dialoogvenster kiezen **Visual C#** > **Classic Windows Desktop** > **Class Library (.NET Framework)** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="926ee-310">In hello **Add New Project** dialog, choose **Visual C#** > **Windows Classic Desktop** > **Class Library (.NET Framework)** template.</span></span>  
9. <span data-ttu-id="926ee-311">Naam Hallo project *ContosoAdsCommon*, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-311">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="926ee-312">Dit project bevat Hallo Entity Framework-context en Hallo-gegevensmodel die beide Hallo front-end en back-end gebruikt.</span><span class="sxs-lookup"><span data-stu-id="926ee-312">This project will contain hello Entity Framework context and hello data model which both hello front end and back end will use.</span></span> <span data-ttu-id="926ee-313">Als alternatief kan u Hallo EF-gerelateerde klassen definiëren in Hallo-webproject en uit Hallo webtaak project naar verwijzen.</span><span class="sxs-lookup"><span data-stu-id="926ee-313">As an alternative, you could define hello EF-related classes in hello web project and reference that project from hello WebJob project.</span></span> <span data-ttu-id="926ee-314">Maar vervolgens uw webtaak project een verwijzing tooweb assembly's, waarbij het niet nodig zou hebben.</span><span class="sxs-lookup"><span data-stu-id="926ee-314">But, then your WebJob project would have a reference tooweb assemblies, which it doesn't need.</span></span>

### <a name="add-a-console-application-project-that-has-webjobs-deployment-enabled"></a><span data-ttu-id="926ee-315">Voeg een consoletoepassing-project met webtaken implementatie is ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="926ee-315">Add a Console Application project that has WebJobs deployment enabled</span></span>
1. <span data-ttu-id="926ee-316">Met de rechtermuisknop op het Hallo-webproject (geen Hallo oplossing of Hallo class library-project) en klik vervolgens op **toevoegen** > **nieuwe Azure webtaak Project**.</span><span class="sxs-lookup"><span data-stu-id="926ee-316">Right-click hello web project (not hello solution or hello class library project), and then click **Add** > **New Azure WebJob Project**.</span></span>

    ![Nieuwe Azure webtaak Project menuselectie](./media/websites-dotnet-webjobs-sdk-get-started/newawjp.png)
2. <span data-ttu-id="926ee-318">In Hallo **toevoegen Azure webtaak** dialoogvenster ContosoAdsWebJob invoeren als beide Hallo **projectnaam** en Hallo **naam van een webtaak**.</span><span class="sxs-lookup"><span data-stu-id="926ee-318">In hello **Add Azure WebJob** dialog, enter ContosoAdsWebJob as both hello **Project name** and hello **WebJob name**.</span></span> <span data-ttu-id="926ee-319">Laat **webtaak uitvoeren modus** instellen te**continu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="926ee-319">Leave **WebJob run mode** set too**Run Continuously**.</span></span>
3. <span data-ttu-id="926ee-320">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-320">Click **OK**.</span></span>

   <span data-ttu-id="926ee-321">Visual Studio maakt een consoletoepassing die is geconfigureerd toodeploy als een webtaak wanneer u Hallo-webproject implementeert.</span><span class="sxs-lookup"><span data-stu-id="926ee-321">Visual Studio creates a Console application that is configured toodeploy as a WebJob whenever you deploy hello web project.</span></span> <span data-ttu-id="926ee-322">toodo dat het uitvoeren van Hallo taken te volgen nadat het Hallo-project maken:</span><span class="sxs-lookup"><span data-stu-id="926ee-322">toodo that, it performed hello following tasks after creating hello project:</span></span>

   * <span data-ttu-id="926ee-323">Toegevoegd een *webtaak-publiceren settings.json* bestand in map Hallo webtaak project-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="926ee-323">Added a *webjob-publish-settings.json* file in hello WebJob project Properties folder.</span></span>
   * <span data-ttu-id="926ee-324">Toegevoegd een *webjobs list.json* bestand in map Hallo web project-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="926ee-324">Added a *webjobs-list.json* file in hello web project Properties folder.</span></span>
   * <span data-ttu-id="926ee-325">Hallo Microsoft.Web.WebJobs.Publish NuGet-pakket in Hallo webtaak project geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-325">Installed hello Microsoft.Web.WebJobs.Publish NuGet package in hello WebJob project.</span></span>

   <span data-ttu-id="926ee-326">Zie voor meer informatie over deze wijzigingen [hoe toodeploy WebJobs met behulp van Visual Studio](websites-dotnet-deploy-webjobs.md).</span><span class="sxs-lookup"><span data-stu-id="926ee-326">For more information about these changes, see [How toodeploy WebJobs by using Visual Studio](websites-dotnet-deploy-webjobs.md).</span></span>

### <a name="add-nuget-packages"></a><span data-ttu-id="926ee-327">NuGet-pakketten toevoegen</span><span class="sxs-lookup"><span data-stu-id="926ee-327">Add NuGet packages</span></span>
<span data-ttu-id="926ee-328">Hallo nieuw project-sjabloon voor een webtaak project installeert automatisch Hallo WebJobs SDK NuGet-pakket [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="926ee-328">hello new-project template for a WebJob project automatically installs hello WebJobs SDK NuGet package [Microsoft.Azure.WebJobs](http://www.nuget.org/packages/Microsoft.Azure.WebJobs) and its dependencies.</span></span>

<span data-ttu-id="926ee-329">Een van de WebJobs SDK-afhankelijkheden die automatisch wordt geïnstalleerd in Hallo webtaak project is Hallo hello Azure Storage Client-bibliotheek (SCL).</span><span class="sxs-lookup"><span data-stu-id="926ee-329">One of hello WebJobs SDK dependencies that is installed automatically in hello WebJob project is hello Azure Storage Client Library (SCL).</span></span> <span data-ttu-id="926ee-330">U moet echter tooadd het toohello web project toowork met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="926ee-330">However, you need tooadd it toohello web project toowork with blobs and queues.</span></span>

1. <span data-ttu-id="926ee-331">Open Hallo **NuGet-pakketten beheren** dialoogvenster voor Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="926ee-331">Open hello **Manage NuGet Packages** dialog for hello solution.</span></span>
2. <span data-ttu-id="926ee-332">Selecteer in het linkerdeelvenster Hallo **geïnstalleerde pakketten**.</span><span class="sxs-lookup"><span data-stu-id="926ee-332">In hello left pane, select **Installed packages**.</span></span>
3. <span data-ttu-id="926ee-333">Hallo zoeken *Azure Storage* van het pakket en klik vervolgens op **beheren**.</span><span class="sxs-lookup"><span data-stu-id="926ee-333">Find hello *Azure Storage* package, and then click **Manage**.</span></span>
4. <span data-ttu-id="926ee-334">In Hallo **projecten selecteren** in, selecteer Hallo **ContosoAdsWeb** selectievakje en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="926ee-334">In hello **Select Projects** box, select hello **ContosoAdsWeb** check box, and then click **OK**.</span></span>

    <span data-ttu-id="926ee-335">Alle drie de projecten Hallo Entity Framework toowork met gegevens in SQL-Database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="926ee-335">All three projects use hello Entity Framework toowork with data in SQL Database.</span></span>
5. <span data-ttu-id="926ee-336">Selecteer in het linkerdeelvenster Hallo **Online**.</span><span class="sxs-lookup"><span data-stu-id="926ee-336">In hello left pane, select **Online**.</span></span>
6. <span data-ttu-id="926ee-337">Hallo zoeken *EntityFramework* NuGet-pakket en installeer het in alle drie de projecten.</span><span class="sxs-lookup"><span data-stu-id="926ee-337">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="926ee-338">Projectverwijzingen instellen</span><span class="sxs-lookup"><span data-stu-id="926ee-338">Set project references</span></span>
<span data-ttu-id="926ee-339">Web- en webtaak projecten werken met Hallo SQL-database, zodat beide een verwijzing toohello ContosoAdsCommon project moeten.</span><span class="sxs-lookup"><span data-stu-id="926ee-339">Both web and WebJob projects work with hello SQL database, so both need a reference toohello ContosoAdsCommon project.</span></span>

1. <span data-ttu-id="926ee-340">In Hallo ingesteld project ContosoAdsWeb een verwijzing toohello ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="926ee-340">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="926ee-341">(Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **toevoegen** > **verwijzing**.</span><span class="sxs-lookup"><span data-stu-id="926ee-341">(Right-click hello ContosoAdsWeb project, and then click **Add** > **Reference**.</span></span> 
2. <span data-ttu-id="926ee-342">In Hallo **Reference Manager** dialoogvenster, **projecten** > **oplossing** > **ContosoAdsCommon**, en klik vervolgens op **OK**.)</span><span class="sxs-lookup"><span data-stu-id="926ee-342">In hello **Reference Manager** dialog box, select **Projects** > **Solution** > **ContosoAdsCommon**, and then click **OK**.)</span></span>
   
    <span data-ttu-id="926ee-343">Hallo webtaak project moet verwijzingen voor het werken met installatiekopieën en voor het openen van verbindingsreeksen.</span><span class="sxs-lookup"><span data-stu-id="926ee-343">hello WebJob project needs references for working with images and for accessing connection strings.</span></span>

4. <span data-ttu-id="926ee-344">Stel in Hallo ContosoAdsWebJob project een verwijzing te`System.Drawing` en `System.Configuration`.</span><span class="sxs-lookup"><span data-stu-id="926ee-344">In hello ContosoAdsWebJob project, set a reference too`System.Drawing` and `System.Configuration`.</span></span>

### <a name="add-code-and-configuration-files"></a><span data-ttu-id="926ee-345">Code-en configuratiebestanden toevoegen</span><span class="sxs-lookup"><span data-stu-id="926ee-345">Add code and configuration files</span></span>
<span data-ttu-id="926ee-346">Deze zelfstudie toont niet hoe te[maken van MVC-controllers en weergaven met steigers](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), hoe te[schrijven van code voor Entity Framework die geschikt is voor SQL Server-databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), of [Hallo basisprincipes van asynchrone programmering in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="926ee-346">This tutorial does not show how too[create MVC controllers and views using scaffolding](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started), how too[write Entity Framework code that works with SQL Server databases](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc), or [hello basics of asynchronous programming in ASP.NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span> <span data-ttu-id="926ee-347">Zo, dat alle is blijft toodo code en configuratie bestanden kopiëren van de oplossing in de nieuwe oplossing Hallo Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="926ee-347">So, all that remains toodo is copy code and configuration files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="926ee-348">Nadat u dat doet, hello volgende secties weergeven en toegelicht belangrijke onderdelen van Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="926ee-348">After you do that, hello following sections show and explain key parts of hello code.</span></span>

<span data-ttu-id="926ee-349">tooadd bestanden tooa project of een map, klik met de rechtermuisknop Hallo project of map en klikt u op **toevoegen** > **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="926ee-349">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** > **Existing Item**.</span></span> <span data-ttu-id="926ee-350">Selecteer Hallo bestanden wilt en klikt u op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="926ee-350">Select hello files you want and click **Add**.</span></span> <span data-ttu-id="926ee-351">Als u wordt gevraagd of u wilt dat de bestaande bestanden tooreplace, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="926ee-351">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="926ee-352">Verwijder in project ContosoAdsCommon Hallo Hallo *Class1.cs* -bestand en in de plaats Hallo volgende bestanden uit Hallo gedownload project toevoegen.</span><span class="sxs-lookup"><span data-stu-id="926ee-352">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="926ee-353">*AD.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-353">*Ad.cs*</span></span>
   * <span data-ttu-id="926ee-354">*ContosoAdscontext.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-354">*ContosoAdscontext.cs*</span></span>
   * <span data-ttu-id="926ee-355">*BlobInformation.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-355">*BlobInformation.cs*</span></span>
2. <span data-ttu-id="926ee-356">In het project ContosoAdsWeb Hallo toevoegen Hallo volgende bestanden uit Hallo gedownload project.</span><span class="sxs-lookup"><span data-stu-id="926ee-356">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="926ee-357">*Web.config*</span><span class="sxs-lookup"><span data-stu-id="926ee-357">*Web.config*</span></span>
   * <span data-ttu-id="926ee-358">*Global.asax.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-358">*Global.asax.cs*</span></span>  
   * <span data-ttu-id="926ee-359">In Hallo *domeincontrollers* map: *AdController.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-359">In hello *Controllers* folder: *AdController.cs*</span></span>
   * <span data-ttu-id="926ee-360">In Hallo *Views\Shared* map: *_Layout.cshtml* bestand</span><span class="sxs-lookup"><span data-stu-id="926ee-360">In hello *Views\Shared* folder: *_Layout.cshtml* file</span></span>
   * <span data-ttu-id="926ee-361">In Hallo *Views\Home* map: *Index.cshtml*</span><span class="sxs-lookup"><span data-stu-id="926ee-361">In hello *Views\Home* folder: *Index.cshtml*</span></span>
   * <span data-ttu-id="926ee-362">In Hallo *Views\Ad* map (Maak eerst Hallo map): vijf *.cshtml* bestanden</span><span class="sxs-lookup"><span data-stu-id="926ee-362">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files</span></span>
3. <span data-ttu-id="926ee-363">Voeg in Hallo ContosoAdsWebJob project Hallo volgende bestanden uit project Hallo gedownload.</span><span class="sxs-lookup"><span data-stu-id="926ee-363">In hello ContosoAdsWebJob project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="926ee-364">*App.config* (Hallo type bestandsfilter ook wijzigen**alle bestanden**)</span><span class="sxs-lookup"><span data-stu-id="926ee-364">*App.config* (change hello file type filter too**All Files**)</span></span>
   * <span data-ttu-id="926ee-365">*Program.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-365">*Program.cs*</span></span>
   * <span data-ttu-id="926ee-366">*Functions.cs*</span><span class="sxs-lookup"><span data-stu-id="926ee-366">*Functions.cs*</span></span>

<span data-ttu-id="926ee-367">Nu kunt u samenstellen, uitvoeren en implementeren van de toepassing hello volgens de instructies eerder in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-367">You can now build, run, and deploy hello application as instructed earlier in hello tutorial.</span></span> <span data-ttu-id="926ee-368">Voordat u dat doet, moet u echter Hallo webtaak die nog steeds worden uitgevoerd in Hallo eerste web-app geïmplementeerd stoppen.</span><span class="sxs-lookup"><span data-stu-id="926ee-368">Before you do that, however, stop hello WebJob that is still running in hello first web app you deployed to.</span></span> <span data-ttu-id="926ee-369">Anders die webtaak wordt verwerkt berichten in wachtrij plaatsen lokaal gemaakt of door Hallo-app in een nieuwe web-app wordt uitgevoerd, omdat alle gebruikt dezelfde Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="926ee-369">Otherwise, that WebJob will process queue messages created locally or by hello app running in a new web app, since all are using hello same storage account.</span></span>

## <span data-ttu-id="926ee-370"><a id="code"></a>Hallo toepassingscode bekijken</span><span class="sxs-lookup"><span data-stu-id="926ee-370"><a id="code"></a>Review hello application code</span></span>
<span data-ttu-id="926ee-371">Hallo volgende secties wordt uitgelegd Hallo code verband tooworking Hello WebJobs SDK en Azure Storage-blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="926ee-371">hello following sections explain hello code related tooworking with hello WebJobs SDK and Azure Storage blobs and queues.</span></span>

> [!NOTE]
> <span data-ttu-id="926ee-372">Ga voor Hallo code specifieke toohello WebJobs SDK toohello [Program.cs en Functions.cs](#programcs) secties.</span><span class="sxs-lookup"><span data-stu-id="926ee-372">For hello code specific toohello WebJobs SDK, go toohello [Program.cs and Functions.cs](#programcs) sections.</span></span>
>
>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="926ee-373">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-373">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="926ee-374">bestand van Hallo Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="926ee-374">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

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

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="926ee-375">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-375">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="926ee-376">Hallo klasse contosoadscontext geeft aan dat Hallo Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="926ee-376">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework stores in a SQL database.</span></span>

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

<span data-ttu-id="926ee-377">Hallo-klasse heeft twee constructors.</span><span class="sxs-lookup"><span data-stu-id="926ee-377">hello class has two constructors.</span></span> <span data-ttu-id="926ee-378">Hallo eerst wordt gebruikt door Hallo-webproject en specificeert Hallo-naam van een verbindingsreeks die is opgeslagen in Web.config Hallo of hello Azure runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="926ee-378">hello first is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file or hello Azure runtime environment.</span></span> <span data-ttu-id="926ee-379">Hallo tweede constructor kunt u toopass in Hallo werkelijke verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="926ee-379">hello second constructor enables you toopass in hello actual connection string.</span></span> <span data-ttu-id="926ee-380">Deze is nodig voor Hallo webtaak project omdat het geen een Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="926ee-380">That is needed by hello WebJob project since it doesn't have a Web.config file.</span></span> <span data-ttu-id="926ee-381">U eerder hebt gezien waar deze verbindingsreeks is opgeslagen en ziet u hoe Hallo-code Hallo verbindingsreeks ophaalt bij het instantiëren van Hallo DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="926ee-381">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadscommon---blobinformationcs"></a><span data-ttu-id="926ee-382">ContosoAdsCommon - BlobInformation.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-382">ContosoAdsCommon - BlobInformation.cs</span></span>
<span data-ttu-id="926ee-383">Hallo `BlobInformation` klasse gebruikte toostore informatie over een blob installatiekopie in een wachtrijbericht is.</span><span class="sxs-lookup"><span data-stu-id="926ee-383">hello `BlobInformation` class is used toostore information about an image blob in a queue message.</span></span>

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


### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="926ee-384">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-384">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="926ee-385">Code die wordt aangeroepen vanuit Hallo `Application_Start` methode maakt u een *installatiekopieën* blob-container en een *installatiekopieën* als ze nog niet bestaan in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="926ee-385">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="926ee-386">Dit zorgt ervoor dat wanneer u met behulp van een nieuw opslagaccount begint, Hallo vereiste blobcontainer en wachtrij automatisch worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="926ee-386">This ensures that whenever you start using a new storage account, hello required blob container and queue are created automatically.</span></span>

<span data-ttu-id="926ee-387">code haalt toegang toohello storage-account met behulp van de opslagverbindingsreeks uit Hallo HALLO hallo *Web.config* bestands- of Azure runtime-omgeving.</span><span class="sxs-lookup"><span data-stu-id="926ee-387">hello code gets access toohello storage account by using hello storage connection string from hello *Web.config* file or Azure runtime environment.</span></span>

        var storageAccount = CloudStorageAccount.Parse
            (ConfigurationManager.ConnectionStrings["AzureWebJobsStorage"].ToString());

<span data-ttu-id="926ee-388">Vervolgens wordt een verwijzing toohello *installatiekopieën* blob-container, Hallo container maakt als deze niet al bestaat en stelt deze voor de nieuwe container Hallo toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="926ee-388">Then, it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="926ee-389">Standaard staan nieuwe containers alleen clients met storage-account referenties tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="926ee-389">By default, new containers allow only clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="926ee-390">Hallo-web-app moet blobs toobe openbare Hallo zodat deze afbeeldingen met URL's die punt toohello afbeeldingsblobs wijzen kan weergeven.</span><span class="sxs-lookup"><span data-stu-id="926ee-390">hello web app needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

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

<span data-ttu-id="926ee-391">Vergelijkbare code wordt een verwijzing toohello *thumbnailrequest* wachtrij en een nieuwe wachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="926ee-391">Similar code gets a reference toohello *thumbnailrequest* queue and creates a new queue.</span></span> <span data-ttu-id="926ee-392">In dit geval is er geen machtigingswijziging nodig.</span><span class="sxs-lookup"><span data-stu-id="926ee-392">In this case no permissions change is needed.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        var imagesQueue = queueClient.GetQueueReference("thumbnailrequest");
        imagesQueue.CreateIfNotExists();

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="926ee-393">ContosoAdsWeb - _Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="926ee-393">ContosoAdsWeb - _Layout.cshtml</span></span>
<span data-ttu-id="926ee-394">Hallo *_Layout.cshtml* bestand Hallo app-naam stelt in Hallo koptekst en voettekst en maakt een menu-item 'Ads'.</span><span class="sxs-lookup"><span data-stu-id="926ee-394">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="926ee-395">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="926ee-395">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="926ee-396">Hallo *Views\Home\Index.cshtml* bestand geeft categoriekoppelingen weer op Hallo-startpagina.</span><span class="sxs-lookup"><span data-stu-id="926ee-396">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="926ee-397">Hallo-koppelingen geven de integerwaarde Hallo Hallo `Category` enum in een pagina querystring variabele toohello Ads Index.</span><span class="sxs-lookup"><span data-stu-id="926ee-397">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

        <li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
        <li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
        <li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
        <li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="926ee-398">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-398">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="926ee-399">In Hallo *AdController.cs* bestand, Hallo constructor aanroepen Hallo `InitializeStorage` methode toocreate Azure Storage-clientbibliotheek objecten die een API leveren voor het werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="926ee-399">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="926ee-400">Vervolgens Hallo code een verwijzing toohello opgehaald *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="926ee-400">Then, hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="926ee-401">Tijdens het uitvoeren, wordt standaard ingesteld [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) geschikt is voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="926ee-401">While doing that, it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="926ee-402">Hallo standaard exponentieel uitstel-beleid voor opnieuw proberen kan vastlopen Hallo web-app langer dan een minuut herhaalde pogingen voor een tijdelijke fout.</span><span class="sxs-lookup"><span data-stu-id="926ee-402">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="926ee-403">beleid voor opnieuw proberen Hallo hier opgegeven wacht drie seconden na elke poging up toothree pogingen.</span><span class="sxs-lookup"><span data-stu-id="926ee-403">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

        var blobClient = storageAccount.CreateCloudBlobClient();
        blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesBlobContainer = blobClient.GetContainerReference("images");

<span data-ttu-id="926ee-404">Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij.</span><span class="sxs-lookup"><span data-stu-id="926ee-404">Similar code gets a reference toohello *images* queue.</span></span>

        CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
        queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
        imagesQueue = queueClient.GetQueueReference("blobnamerequest");

<span data-ttu-id="926ee-405">De meeste Hallo controllercode is Typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="926ee-405">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="926ee-406">Een uitzondering is Hallo HttpPost `Create` methode, waarmee een bestand wordt geüpload en opgeslagen in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="926ee-406">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="926ee-407">Hallo modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello methode-object.</span><span class="sxs-lookup"><span data-stu-id="926ee-407">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

        [HttpPost]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> Create(
            [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
            HttpPostedFileBase imageFile)

<span data-ttu-id="926ee-408">Hallo gebruiker geselecteerd een bestand tooupload, Hallo code Hallo-bestand wordt geüpload, opgeslagen in een blob als Hallo Ad-databaserecord bijgewerkt met een URL die toohello blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="926ee-408">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            blob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = blob.Uri.ToString();
        }

<span data-ttu-id="926ee-409">Hallo-code die uploaden Hallo heeft Hallo `UploadAndSaveBlobAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="926ee-409">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="926ee-410">Deze maakt een GUID-naam voor Hallo blob, uploads en slaat Hallo-bestand en retourneert een verwijzing toohello opgeslagen blob.</span><span class="sxs-lookup"><span data-stu-id="926ee-410">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

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

<span data-ttu-id="926ee-411">Na het Hallo HttpPost `Create` methode een blob uploadt en updates Hallo database, het maken van een wachtrij bericht tooinform Hallo back-endproces dat een afbeelding gereed voor conversie tooa miniatuur is.</span><span class="sxs-lookup"><span data-stu-id="926ee-411">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform hello back-end process that an image is ready for conversion tooa thumbnail.</span></span>

        BlobInformation blobInfo = new BlobInformation() { AdId = ad.AdId, BlobUri = new Uri(ad.ImageURL) };
        var queueMessage = new CloudQueueMessage(JsonConvert.SerializeObject(blobInfo));
        await thumbnailRequestQueue.AddMessageAsync(queueMessage);

<span data-ttu-id="926ee-412">code voor Hallo HttpPost Hallo `Edit` methode is vergelijkbaar, behalve dat als Hallo gebruiker selecteert een nieuw afbeeldingsbestand, alle blobs die al bestaan voor deze advertentie moeten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="926ee-412">hello code for hello HttpPost `Edit` method is similar, except that if hello user selects a new image file, any blobs that already exist for this ad must be deleted.</span></span>

        if (imageFile != null && imageFile.ContentLength != 0)
        {
            await DeleteAdBlobsAsync(ad);
            imageBlob = await UploadAndSaveBlobAsync(imageFile);
            ad.ImageURL = imageBlob.Uri.ToString();
        }

<span data-ttu-id="926ee-413">Dit is Hallo code verwijderen van blobs wanneer u een advertentie verwijdert:</span><span class="sxs-lookup"><span data-stu-id="926ee-413">Here is hello code that deletes blobs when you delete an ad:</span></span>

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

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="926ee-414">ContosoAdsWeb - Views\Ad\Index.cshtml en Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="926ee-414">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="926ee-415">Hallo *Index.cshtml* bestand bevat miniaturen Hello andere ad-gegevens:</span><span class="sxs-lookup"><span data-stu-id="926ee-415">hello *Index.cshtml* file displays thumbnails with hello other ad data:</span></span>

        <img  src="@Html.Raw(item.ThumbnailURL)" />

<span data-ttu-id="926ee-416">Hallo *Details.cshtml* bestand Hallo-afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="926ee-416">hello *Details.cshtml* file displays hello full-size image:</span></span>

        <img src="@Html.Raw(Model.ImageURL)" />

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="926ee-417">ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="926ee-417">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="926ee-418">Hallo *Create.cshtml* en *Edit.cshtml* bestanden formulier dat Hiermee controller tooget Hallo Hallo codering opgeven `HttpPostedFileBase` object.</span><span class="sxs-lookup"><span data-stu-id="926ee-418">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

        @using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))

<span data-ttu-id="926ee-419">Een `<input>` element vertelt Hallo browser tooprovide een dialoogvenster voor bestandsselectie.</span><span class="sxs-lookup"><span data-stu-id="926ee-419">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

        <input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />

### <span data-ttu-id="926ee-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span><span class="sxs-lookup"><span data-stu-id="926ee-420"><a id="programcs"></a>ContosoAdsWebJob - Program.cs</span></span>
<span data-ttu-id="926ee-421">Wanneer Hallo webtaak wordt gestart, hello `Main` methodeaanroepen Hallo WebJobs SDK `JobHost.RunAndBlock` methode toobegin uitvoering van de geactiveerde functies in de huidige thread Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-421">When hello WebJob starts, hello `Main` method calls hello WebJobs SDK `JobHost.RunAndBlock` method toobegin execution of triggered functions on hello current thread.</span></span>

        static void Main(string[] args)
        {
            JobHost host = new JobHost();
            host.RunAndBlock();
        }

### <span data-ttu-id="926ee-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail methode</span><span class="sxs-lookup"><span data-stu-id="926ee-422"><a id="generatethumbnail"></a>ContosoAdsWebJob - Functions.cs - GenerateThumbnail method</span></span>
<span data-ttu-id="926ee-423">Hallo WebJobs SDK roept deze methode wanneer er een wachtrijbericht wordt ontvangen.</span><span class="sxs-lookup"><span data-stu-id="926ee-423">hello WebJobs SDK calls this method when a queue message is received.</span></span> <span data-ttu-id="926ee-424">Hallo-methode maakt u een miniatuur en puts Hallo miniatuur-URL in het Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="926ee-424">hello method creates a thumbnail and puts hello thumbnail URL in hello database.</span></span>

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
            // be instantiated and disposed within hello function.
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

* <span data-ttu-id="926ee-425">Hallo `QueueTrigger` kenmerk stuurt Hallo WebJobs SDK toocall deze methode wanneer een nieuw bericht wordt ontvangen op Hallo thumbnailrequest wachtrij.</span><span class="sxs-lookup"><span data-stu-id="926ee-425">hello `QueueTrigger` attribute directs hello WebJobs SDK toocall this method when a new message is received on hello thumbnailrequest queue.</span></span>

        [QueueTrigger("thumbnailrequest")] BlobInformation blobInfo,

    <span data-ttu-id="926ee-426">Hallo `BlobInformation` -object in de wachtrij het Hallo-bericht is automatisch gedeserialiseerde in Hallo `blobInfo` parameter.</span><span class="sxs-lookup"><span data-stu-id="926ee-426">hello `BlobInformation` object in hello queue message is automatically deserialized into hello `blobInfo` parameter.</span></span> <span data-ttu-id="926ee-427">Wanneer Hallo-methode is voltooid, wordt de wachtrij het Hallo-bericht verwijderd.</span><span class="sxs-lookup"><span data-stu-id="926ee-427">When hello method completes, hello queue message is deleted.</span></span> <span data-ttu-id="926ee-428">Als Hallo methode mislukt voordat wordt voltooid, wordt wachtrij het Hallo-bericht niet verwijderd. Nadat een 10 minuten lease is verlopen, is het Hallo-bericht uitgebrachte toobe opnieuw opgehaald en verwerkt.</span><span class="sxs-lookup"><span data-stu-id="926ee-428">If hello method fails before completing, hello queue message is not deleted; after a 10-minute lease expires, hello message is released toobe picked up again and processed.</span></span> <span data-ttu-id="926ee-429">Deze reeks won't voor onbepaalde tijd worden herhaald als een bericht altijd een uitzondering veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="926ee-429">This sequence won't be repeated indefinitely if a message always causes an exception.</span></span> <span data-ttu-id="926ee-430">Na 5 mislukte tooprocess een bericht pogingen, het Hallo-bericht is verplaatst tooa wachtrij met de naam {wachtrijnaam}-verontreinigd.</span><span class="sxs-lookup"><span data-stu-id="926ee-430">After 5 unsuccessful attempts tooprocess a message, hello message is moved tooa queue named {queuename}-poison.</span></span> <span data-ttu-id="926ee-431">maximum aantal pogingen Hallo kan worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-431">hello maximum number of attempts is configurable.</span></span>
* <span data-ttu-id="926ee-432">Hallo twee `Blob` kenmerken Geef objecten die gebonden tooblobs zijn: één toohello bestaande installatiekopie blob en één tooa nieuwe miniaturen blob die Hallo-methode maakt.</span><span class="sxs-lookup"><span data-stu-id="926ee-432">hello two `Blob` attributes provide objects that are bound tooblobs: one toohello existing image blob and one tooa new thumbnail blob that hello method creates.</span></span>

        [Blob("images/{BlobName}", FileAccess.Read)] Stream input,
        [Blob("images/{BlobNameWithoutExtension}_thumbnail.jpg")] CloudBlockBlob outputBlob)

    <span data-ttu-id="926ee-433">BLOB-namen afkomstig zijn van de eigenschappen van Hallo `BlobInformation` object in de wachtrij het Hallo-bericht ontvangen (`BlobName` en `BlobNameWithoutExtension`).</span><span class="sxs-lookup"><span data-stu-id="926ee-433">Blob names come from properties of hello `BlobInformation` object received in hello queue message (`BlobName` and `BlobNameWithoutExtension`).</span></span> <span data-ttu-id="926ee-434">tooget hello volledige functionaliteit van Hallo Storage-clientbibliotheek, kunt u Hallo `CloudBlockBlob` klasse toowork met blobs.</span><span class="sxs-lookup"><span data-stu-id="926ee-434">tooget hello full functionality of hello Storage Client Library, you can use hello `CloudBlockBlob` class toowork with blobs.</span></span> <span data-ttu-id="926ee-435">Als u wilt dat tooreuse-code die is geschreven toowork met `Stream` objecten, kunt u Hallo `Stream` klasse.</span><span class="sxs-lookup"><span data-stu-id="926ee-435">If you want tooreuse code that was written toowork with `Stream` objects, you can use hello `Stream` class.</span></span>

<span data-ttu-id="926ee-436">Voor meer informatie over hoe toowrite functioneert die kenmerken van de WebJobs SDK gebruiken, raadpleegt u Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="926ee-436">For more information about how toowrite functions that use  WebJobs SDK attributes, see hello following resources:</span></span>

* [<span data-ttu-id="926ee-437">Hoe toouse Azure queue storage Hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="926ee-437">How toouse Azure queue storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-queues-how-to.md)
* [<span data-ttu-id="926ee-438">Hoe toouse Azure blob-opslag met Hallo WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="926ee-438">How toouse Azure blob storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
* [<span data-ttu-id="926ee-439">Hoe toouse Azure table storage Hello WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="926ee-439">How toouse Azure table storage with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-storage-tables-how-to.md)
* [<span data-ttu-id="926ee-440">Hoe toouse Azure Service Bus met Hallo WebJobs SDK</span><span class="sxs-lookup"><span data-stu-id="926ee-440">How toouse Azure Service Bus with hello WebJobs SDK</span></span>](websites-dotnet-webjobs-sdk-service-bus.md)

> [!NOTE]
> * <span data-ttu-id="926ee-441">Als uw web-app wordt uitgevoerd op meerdere virtuele machines, meerdere WebJobs wordt tegelijkertijd worden uitgevoerd en in sommige gevallen kan dit resulteren in Hallo dezelfde gegevens meerdere keren wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="926ee-441">If your web app runs on multiple VMs, multiple WebJobs will be running simultaneously, and in some scenarios this can result in hello same data getting processed multiple times.</span></span> <span data-ttu-id="926ee-442">Dit is niet een probleem als u ingebouwde wachtrij hello, blob en Service Bus-triggers.</span><span class="sxs-lookup"><span data-stu-id="926ee-442">This is not a problem if you use hello built-in queue, blob, and Service Bus triggers.</span></span> <span data-ttu-id="926ee-443">Hallo SDK zorgt ervoor dat uw functies slechts één keer worden verwerkt voor elk bericht of blob.</span><span class="sxs-lookup"><span data-stu-id="926ee-443">hello SDK ensures that your functions will be processed only once for each message or blob.</span></span>
> * <span data-ttu-id="926ee-444">Voor informatie over het correct afsluiten tooimplement, Zie [correct afsluiten](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span><span class="sxs-lookup"><span data-stu-id="926ee-444">For information about how tooimplement graceful shutdown, see [Graceful Shutdown](websites-dotnet-webjobs-sdk-storage-queues-how-to.md#graceful).</span></span>
> * <span data-ttu-id="926ee-445">Hallo-code in Hallo `ConvertImageToThumbnailJPG` methode (niet weergegeven) maakt gebruik van klassen in Hallo `System.Drawing` naamruimte voor eenvoud.</span><span class="sxs-lookup"><span data-stu-id="926ee-445">hello code in hello `ConvertImageToThumbnailJPG` method (not shown) uses classes in hello `System.Drawing` namespace for simplicity.</span></span> <span data-ttu-id="926ee-446">Hallo-klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="926ee-446">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="926ee-447">Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service.</span><span class="sxs-lookup"><span data-stu-id="926ee-447">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="926ee-448">Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="926ee-448">For more information about image processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="926ee-449">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="926ee-449">Next steps</span></span>
<span data-ttu-id="926ee-450">In deze zelfstudie hebt u een eenvoudige toepassing met meerdere lagen die Hallo WebJobs SDK voor de verwerking van de back-end gebruikt gezien.</span><span class="sxs-lookup"><span data-stu-id="926ee-450">In this tutorial, you've seen a simple multi-tier application that uses hello WebJobs SDK for backend processing.</span></span> <span data-ttu-id="926ee-451">Deze sectie vindt u enkele suggesties voor meer informatie over toepassingen met meerdere lagen ASP.NET en WebJobs.</span><span class="sxs-lookup"><span data-stu-id="926ee-451">This section offers some suggestions for learning more about ASP.NET multi-tier applications and WebJobs.</span></span>

### <a name="missing-features"></a><span data-ttu-id="926ee-452">Ontbrekende functies</span><span class="sxs-lookup"><span data-stu-id="926ee-452">Missing features</span></span>
<span data-ttu-id="926ee-453">de toepassing Hello gehouden eenvoudige voor een zelfstudie aan de slag.</span><span class="sxs-lookup"><span data-stu-id="926ee-453">hello application has been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="926ee-454">In een echte toepassing die u wilt implementeren [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) en Hallo [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), gebruik [een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), gebruiken[ EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model wijzigingen en gebruik [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage tijdelijke netwerkfouten.</span><span class="sxs-lookup"><span data-stu-id="926ee-454">In a real-world application you would implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) and hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), use [an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes, and use [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors.</span></span>

### <a name="scaling-webjobs"></a><span data-ttu-id="926ee-455">Schalen WebJobs</span><span class="sxs-lookup"><span data-stu-id="926ee-455">Scaling WebJobs</span></span>
<span data-ttu-id="926ee-456">WebJobs in Hallo context van een web-app uitgevoerd en zijn niet afzonderlijk worden schaalbaar.</span><span class="sxs-lookup"><span data-stu-id="926ee-456">WebJobs run in hello context of a web app and are not scalable separately.</span></span> <span data-ttu-id="926ee-457">Als u een standaard web-app-exemplaar hebt, hebt u slechts één exemplaar van de achtergrondproces wordt uitgevoerd en sommige Hallo serverbronnen (CPU, geheugen, enzovoort) die anders beschikbaar tooserve webinhoud zijn zou wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="926ee-457">For example, if you have one Standard web app instance, you have only one instance of your background process running, and it is using some of hello server resources (CPU, memory, etc.) that otherwise would be available tooserve web content.</span></span>

<span data-ttu-id="926ee-458">Als verkeer hangt af van de tijd van de dag of week, en als back-end Hallo verwerken u moet toodo kunt wachten, uw toorun WebJobs kan worden gepland op tijden weinig verkeer.</span><span class="sxs-lookup"><span data-stu-id="926ee-458">If traffic varies by time of day or day of week, and if hello backend processing you need toodo can wait, you could schedule your WebJobs toorun at low-traffic times.</span></span> <span data-ttu-id="926ee-459">Als Hallo belasting nog steeds te hoog is voor deze oplossing wordt, kunt u back-end voor Hallo als een webtaak in een speciale afzonderlijke web-app uitvoeren daarvoor.</span><span class="sxs-lookup"><span data-stu-id="926ee-459">If hello load is still too high for that solution, you can run hello backend as a WebJob in a separate web app dedicated for that purpose.</span></span> <span data-ttu-id="926ee-460">U kunt uw back-end-web-app vervolgens onafhankelijk van elkaar schalen van uw frontend-web-app.</span><span class="sxs-lookup"><span data-stu-id="926ee-460">You can then scale your backend web app independently from your frontend web app.</span></span>

<span data-ttu-id="926ee-461">Zie voor meer informatie [WebJobs schalen](websites-webjobs-resources.md#scale).</span><span class="sxs-lookup"><span data-stu-id="926ee-461">For more information, see [Scaling WebJobs](websites-webjobs-resources.md#scale).</span></span>

### <a name="avoiding-web-app-timeout-shut-downs"></a><span data-ttu-id="926ee-462">Web-app time-out afsluiten-keuzelijsten voorkomen</span><span class="sxs-lookup"><span data-stu-id="926ee-462">Avoiding web app timeout shut-downs</span></span>
<span data-ttu-id="926ee-463">toomake ervoor dat uw WebJobs worden altijd uitgevoerd en wordt uitgevoerd op alle exemplaren van uw web-app, hebt u tooenable Hallo [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) functie.</span><span class="sxs-lookup"><span data-stu-id="926ee-463">toomake sure your WebJobs are always running, and running on all instances of your web app, you have tooenable hello [AlwaysOn](http://weblogs.asp.net/scottgu/archive/2014/01/16/windows-azure-staging-publishing-support-for-web-sites-monitoring-improvements-hyper-v-recovery-manager-ga-and-pci-compliance.aspx) feature.</span></span>

### <a name="using-hello-webjobs-sdk-outside-of-webjobs"></a><span data-ttu-id="926ee-464">Met behulp van Hallo WebJobs SDK buiten WebJobs</span><span class="sxs-lookup"><span data-stu-id="926ee-464">Using hello WebJobs SDK outside of WebJobs</span></span>
<span data-ttu-id="926ee-465">Een programma dat gebruikmaakt van Hallo WebJobs SDK biedt geen toorun in Azure in een webtaak.</span><span class="sxs-lookup"><span data-stu-id="926ee-465">A program that uses hello WebJobs SDK doesn't have toorun in Azure in a WebJob.</span></span> <span data-ttu-id="926ee-466">Lokaal kunt uitvoeren, en ook in andere omgevingen zoals een werkrol Cloudservice of een Windows-service kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="926ee-466">It can run locally, and it can also run in other environments such as a Cloud Service worker role or a Windows service.</span></span> <span data-ttu-id="926ee-467">U kunt echter alleen Hallo WebJobs SDK dashboard openen via een Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="926ee-467">However, you can only access hello WebJobs SDK dashboard through an Azure web app.</span></span> <span data-ttu-id="926ee-468">toouse Hallo-dashboard tooconnect Hallo web app toohello opslagaccount u hebt door het Hallo AzureWebJobsDashboard verbindingsreeks instellen op Hallo **configureren** tabblad van de klassieke portal Hallo.</span><span class="sxs-lookup"><span data-stu-id="926ee-468">toouse hello dashboard you have tooconnect hello web app toohello storage account you're using by setting hello AzureWebJobsDashboard connection string on hello **Configure** tab of hello classic portal.</span></span> <span data-ttu-id="926ee-469">U kunt vervolgens toohello Dashboard krijgen met behulp van Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="926ee-469">Then, you can get toohello Dashboard by using hello following URL:</span></span>

<span data-ttu-id="926ee-470">https://{webappname}.SCM.azurewebsites.NET/azurejobs/#/Functions</span><span class="sxs-lookup"><span data-stu-id="926ee-470">https://{webappname}.scm.azurewebsites.net/azurejobs/#/functions</span></span>

<span data-ttu-id="926ee-471">Zie voor meer informatie [ophalen van een dashboard voor lokale ontwikkeling Hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), maar houd er rekening mee dat er een oude naam van verbindingsreeks wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="926ee-471">For more information, see [Getting a dashboard for local development with hello WebJobs SDK](http://blogs.msdn.com/b/jmstall/archive/2014/01/27/getting-a-dashboard-for-local-development-with-the-webjobs-sdk.aspx), but note that it shows an old connection string name.</span></span>

### <a name="more-webjobs-documentation"></a><span data-ttu-id="926ee-472">Documentatie voor meer WebJobs</span><span class="sxs-lookup"><span data-stu-id="926ee-472">More WebJobs documentation</span></span>
<span data-ttu-id="926ee-473">Zie voor meer informatie [documentatiebronnen Azure WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226).</span><span class="sxs-lookup"><span data-stu-id="926ee-473">For more information, see [Azure WebJobs documentation resources](http://go.microsoft.com/fwlink/?LinkId=390226).</span></span>
