---
title: aaaGet slag met Azure Cloud Services en ASP.NET | Microsoft Docs
description: Meer informatie over hoe toocreate een app met meerdere lagen met ASP.NET MVC en Azure. Hallo-app wordt uitgevoerd in een cloudservice met de Webrol en een werkrol. De app maakt gebruik van Entity Framework, SQL Database, en wachtrijen en blobs van Azure Storage.
services: cloud-services, storage
documentationcenter: .net
author: Thraka
manager: timlt
editor: 
ms.assetid: d7aa440d-af4a-4f80-b804-cc46178df4f9
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/15/2017
ms.author: adegeo
ms.openlocfilehash: 86271c29b79fad3f01f8ea0e88fd00c7aefc970c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cloud-services-and-aspnet"></a><span data-ttu-id="7b06e-105">Aan de slag met Azure Cloud Services en ASP.NET</span><span class="sxs-lookup"><span data-stu-id="7b06e-105">Get started with Azure Cloud Services and ASP.NET</span></span>

## <a name="overview"></a><span data-ttu-id="7b06e-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7b06e-106">Overview</span></span>
<span data-ttu-id="7b06e-107">Deze zelfstudie laat zien hoe toocreate een meerlaagse .NET-toepassing met een ASP.NET MVC-front-, en implementeert tooan [Azure-cloudservice](cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="7b06e-107">This tutorial shows how toocreate a multi-tier .NET application with an ASP.NET MVC front-end, and deploy it tooan [Azure cloud service](cloud-services-choose-me.md).</span></span> <span data-ttu-id="7b06e-108">toepassing gebruikt Hallo [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), Hallo [Azure Blob-service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo [Azure Queue-service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span><span class="sxs-lookup"><span data-stu-id="7b06e-108">hello application uses [Azure SQL Database](http://msdn.microsoft.com/library/azure/ee336279), hello [Azure Blob service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and hello [Azure Queue service](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern).</span></span> <span data-ttu-id="7b06e-109">U kunt [Hallo Visual Studio-project downloaden](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) van Hallo MSDN-Codegalerie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-109">You can [download hello Visual Studio project](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4) from hello MSDN Code Gallery.</span></span>

<span data-ttu-id="7b06e-110">Hallo-zelfstudie ziet u hoe toobuild en Voer Hallo toepassing lokaal door hoe toodeploy het tooAzure en uitvoeren in Hallo cloud, en hoe toobuild deze vanaf het begin.</span><span class="sxs-lookup"><span data-stu-id="7b06e-110">hello tutorial shows you how toobuild and run hello application locally, how toodeploy it tooAzure and run in hello cloud, and how toobuild it from scratch.</span></span> <span data-ttu-id="7b06e-111">U kunt starten door gebouw vanaf het begin en vervolgens Hallo test en stappen daarna implementeren als u liever.</span><span class="sxs-lookup"><span data-stu-id="7b06e-111">You can start by building from scratch and then do hello test and deploy steps afterward if you prefer.</span></span>

## <a name="contoso-ads-application"></a><span data-ttu-id="7b06e-112">Toepassing Contoso Ads</span><span class="sxs-lookup"><span data-stu-id="7b06e-112">Contoso Ads application</span></span>
<span data-ttu-id="7b06e-113">Hallo-toepassing is een bulletinboard voor advertenties.</span><span class="sxs-lookup"><span data-stu-id="7b06e-113">hello application is an advertising bulletin board.</span></span> <span data-ttu-id="7b06e-114">Gebruikers maken een advertentie door de tekst in te voeren en een afbeelding te uploaden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-114">Users create an ad by entering text and uploading an image.</span></span> <span data-ttu-id="7b06e-115">Zien ze een lijst met advertenties met miniatuurafbeeldingen en ze Hallo afbeelding kunnen zien wanneer ze een ad toosee Hallo details selecteren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-115">They can see a list of ads with thumbnail images, and they can see hello full-size image when they select an ad toosee hello details.</span></span>

![Advertentielijst](./media/cloud-services-dotnet-get-started/list.png)

<span data-ttu-id="7b06e-117">Hallo-toepassing hello gebruikt [wachtrijgerichte werkpatroon](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff load Hallo CPU-intensief werk van het maken van miniatuurweergaven tooa back-end-proces.</span><span class="sxs-lookup"><span data-stu-id="7b06e-117">hello application uses hello [queue-centric work pattern](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern) toooff-load hello CPU-intensive work of creating thumbnails tooa back-end process.</span></span>

## <a name="alternative-architecture-websites-and-webjobs"></a><span data-ttu-id="7b06e-118">Alternatieve architectuur: Websites en WebJobs</span><span class="sxs-lookup"><span data-stu-id="7b06e-118">Alternative architecture: Websites and WebJobs</span></span>
<span data-ttu-id="7b06e-119">Deze zelfstudie laat zien hoe toorun front-end- en back-end in een Azure cloud service.</span><span class="sxs-lookup"><span data-stu-id="7b06e-119">This tutorial shows how toorun both front-end and back-end in an Azure cloud service.</span></span> <span data-ttu-id="7b06e-120">Een alternatief is toorun Hallo front-end in een [Azure-website](/services/web-sites/) en gebruik Hallo [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) functie (momenteel in preview) voor Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="7b06e-120">An alternative is toorun hello front-end in an [Azure website](/services/web-sites/) and use hello [WebJobs](http://go.microsoft.com/fwlink/?LinkId=390226) feature (currently in preview) for hello back-end.</span></span> <span data-ttu-id="7b06e-121">Zie voor een zelfstudie die gebruikmaakt van WebJobs [aan de slag met Azure WebJobs SDK Hallo](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7b06e-121">For a tutorial that uses WebJobs, see [Get Started with hello Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md).</span></span> <span data-ttu-id="7b06e-122">Zie voor meer informatie over hoe toochoose Hallo services waar beste uw scenario past, [vergelijking van Azure Websites, Cloudservices en virtuele machines](../app-service-web/choose-web-site-cloud-service-vm.md).</span><span class="sxs-lookup"><span data-stu-id="7b06e-122">For information about how toochoose hello services that best fit your scenario, see [Azure Websites, Cloud Services, and virtual machines comparison](../app-service-web/choose-web-site-cloud-service-vm.md).</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7b06e-123">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="7b06e-123">What you'll learn</span></span>
* <span data-ttu-id="7b06e-124">Hoe tooenable computer klaarmaken voor het ontwikkelen van Azure door het installeren van hello Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="7b06e-124">How tooenable your machine for Azure development by installing hello Azure SDK.</span></span>
* <span data-ttu-id="7b06e-125">Hoe een Visual Studio toocreate cloud service-project met een ASP.NET MVC-Webrol en een werkrol.</span><span class="sxs-lookup"><span data-stu-id="7b06e-125">How toocreate a Visual Studio cloud service project with an ASP.NET MVC web role and a worker role.</span></span>
* <span data-ttu-id="7b06e-126">Hoe Hallo tootest cloudserviceproject lokaal hello Azure-opslagemulator gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-126">How tootest hello cloud service project locally, using hello Azure storage emulator.</span></span>
* <span data-ttu-id="7b06e-127">Hoe toopublish Hallo cloud project tooan Azure-cloudservice en testen met behulp van een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b06e-127">How toopublish hello cloud project tooan Azure cloud service and test using an Azure storage account.</span></span>
* <span data-ttu-id="7b06e-128">Hoe tooupload bestanden en deze opslaan op Hallo Azure Blob-service.</span><span class="sxs-lookup"><span data-stu-id="7b06e-128">How tooupload files and store them in hello Azure Blob service.</span></span>
* <span data-ttu-id="7b06e-129">Hoe toouse hello Azure Queue-service voor communicatie tussen lagen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-129">How toouse hello Azure Queue service for communication between tiers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b06e-130">Vereisten</span><span class="sxs-lookup"><span data-stu-id="7b06e-130">Prerequisites</span></span>
<span data-ttu-id="7b06e-131">Hallo zelfstudie wordt ervan uitgegaan dat u begrijpt [basisconcepten van Azure-cloudservices](cloud-services-choose-me.md) zoals *Webrol* en *werkrol* terminologie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-131">hello tutorial assumes that you understand [basic concepts about Azure cloud services](cloud-services-choose-me.md) such as *web role* and *worker role* terminology.</span></span>  <span data-ttu-id="7b06e-132">Ook wordt ervan uitgegaan dat u weet hoe toowork met [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) of [webformulieren](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projecten in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b06e-132">It also assumes that you know how toowork with [ASP.NET MVC](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started) or [Web Forms](http://www.asp.net/web-forms/tutorials/aspnet-45/getting-started-with-aspnet-45-web-forms/introduction-and-overview) projects in Visual Studio.</span></span> <span data-ttu-id="7b06e-133">Hallo-voorbeeldtoepassing gebruikt MVC, maar de meeste Hallo zelfstudie geldt ook tooWeb formulieren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-133">hello sample application uses MVC, but most of hello tutorial also applies tooWeb Forms.</span></span>

<span data-ttu-id="7b06e-134">U kunt Hallo app lokaal zonder een Azure-abonnement uitvoeren, maar moet u één toodeploy Hallo toepassing toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="7b06e-134">You can run hello app locally without an Azure subscription, but you'll need one toodeploy hello application toohello cloud.</span></span> <span data-ttu-id="7b06e-135">Als u geen account hebt, kunt u [uw voordelen als MSDN-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) of [zich aanmelden voor een gratis proefversie](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span><span class="sxs-lookup"><span data-stu-id="7b06e-135">If you don't have an account, you can [activate your MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A55E3C668) or [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A55E3C668).</span></span>

<span data-ttu-id="7b06e-136">Hallo zelfstudie instructies werken met een van de volgende producten Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b06e-136">hello tutorial instructions work with either of hello following products:</span></span>

* <span data-ttu-id="7b06e-137">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="7b06e-137">Visual Studio 2013</span></span>
* <span data-ttu-id="7b06e-138">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="7b06e-138">Visual Studio 2015</span></span>
* <span data-ttu-id="7b06e-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="7b06e-139">Visual Studio 2017</span></span>

<span data-ttu-id="7b06e-140">Als u een van deze geen hebt, wordt Visual Studio kan worden automatisch geïnstalleerd wanneer u hello Azure SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-140">If you don't have one of these, Visual Studio may be installed automatically when you install hello Azure SDK.</span></span>

## <a name="application-architecture"></a><span data-ttu-id="7b06e-141">Toepassingsarchitectuur</span><span class="sxs-lookup"><span data-stu-id="7b06e-141">Application architecture</span></span>
<span data-ttu-id="7b06e-142">Hallo app slaat de advertenties in een SQL-database, met behulp van Entity Framework Code First toocreate Hallo tabellen en toegang tot Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="7b06e-142">hello app stores ads in a SQL database, using Entity Framework Code First toocreate hello tables and access hello data.</span></span> <span data-ttu-id="7b06e-143">Voor elke advertentie Hallo Hallo database winkels twee URL's, één voor afbeelding op volledige grootte en één voor Hallo miniatuur.</span><span class="sxs-lookup"><span data-stu-id="7b06e-143">For each ad, hello database stores two URLs, one for hello full-size image and one for hello thumbnail.</span></span>

![Advertentietabel](./media/cloud-services-dotnet-get-started/adtable.png)

<span data-ttu-id="7b06e-145">Wanneer een gebruiker een afbeelding uploadt, front-uitgevoerd van Hallo in een Webrol slaat Hallo-installatiekopie in een [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), en Hallo ad informatie opslaat in de database Hallo met een URL die toohello blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="7b06e-145">When a user uploads an image, hello front-end running in a web role stores hello image in an [Azure blob](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage), and it stores hello ad information in hello database with a URL that points toohello blob.</span></span> <span data-ttu-id="7b06e-146">AT Hallo dezelfde tijd, wordt een bericht tooan Azure-wachtrij geschreven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-146">At hello same time, it writes a message tooan Azure queue.</span></span> <span data-ttu-id="7b06e-147">Een back-end-proces dat periodiek wordt uitgevoerd in een werkrol Hallo wachtrij voor nieuwe berichten worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-147">A back-end process running in a worker role periodically polls hello queue for new messages.</span></span> <span data-ttu-id="7b06e-148">Wanneer een nieuw bericht wordt weergegeven, Hallo werkrol een miniatuur voor de betreffende afbeelding gemaakt en updates Hallo miniaturen URL databaseveld voor de advertentie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-148">When a new message appears, hello worker role creates a thumbnail for that image and updates hello thumbnail URL database field for that ad.</span></span> <span data-ttu-id="7b06e-149">Hallo volgende diagram toont de wisselwerking tussen onderdelen van de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-149">hello following diagram shows how hello parts of hello application interact.</span></span>

![Architectuur van Contoso Ads](./media/cloud-services-dotnet-get-started/apparchitecture.png)

[!INCLUDE [install-sdk](../../includes/install-sdk-2017-2015-2013.md)]

## <a name="download-and-run-hello-completed-solution"></a><span data-ttu-id="7b06e-151">Hallo voltooid oplossing downloaden en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7b06e-151">Download and run hello completed solution</span></span>
1. <span data-ttu-id="7b06e-152">Downloaden en uitpakken Hallo [voltooide oplossing](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span><span class="sxs-lookup"><span data-stu-id="7b06e-152">Download and unzip hello [completed solution](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4).</span></span>
2. <span data-ttu-id="7b06e-153">Start Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b06e-153">Start Visual Studio.</span></span>
3. <span data-ttu-id="7b06e-154">Van Hallo **bestand** in het menu **Open Project**, gaat u toowhere u Hallo oplossing gedownload en open het oplossingsbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-154">From hello **File** menu choose **Open Project**, navigate toowhere you downloaded hello solution, and then open hello solution file.</span></span>
4. <span data-ttu-id="7b06e-155">Druk op CTRL + SHIFT + B toobuild Hallo oplossing.</span><span class="sxs-lookup"><span data-stu-id="7b06e-155">Press CTRL+SHIFT+B toobuild hello solution.</span></span>

    <span data-ttu-id="7b06e-156">Standaard herstelt Visual Studio automatisch Hallo NuGet-pakketinhoud die niet is opgenomen in Hallo *.zip* bestand.</span><span class="sxs-lookup"><span data-stu-id="7b06e-156">By default, Visual Studio automatically restores hello NuGet package content, which was not included in hello *.zip* file.</span></span> <span data-ttu-id="7b06e-157">Als hello-pakketten niet worden hersteld, deze handmatig installeren door te gaan toohello **NuGet-pakketten beheren voor oplossing** in het dialoogvenster en te klikken op Hallo **herstellen** knop Hallo rechts bovenaan.</span><span class="sxs-lookup"><span data-stu-id="7b06e-157">If hello packages don't restore, install them manually by going toohello **Manage NuGet Packages for Solution** dialog box and clicking hello **Restore** button at hello top right.</span></span>
5. <span data-ttu-id="7b06e-158">In **Solution Explorer**, zorg ervoor dat **ContosoAdsCloudService** is geselecteerd als opstartproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-158">In **Solution Explorer**, make sure that **ContosoAdsCloudService** is selected as hello startup project.</span></span>
6. <span data-ttu-id="7b06e-159">Als u Visual Studio 2015 gebruikt of hoger, Hallo SQL Server-verbindingsreeks in de toepassing hello wijzigt *Web.config* bestand van het ContosoAdsWeb-project hello en in Hallo *ServiceConfiguration.Local.cscfg* -bestand van Hallo ContosoAdsCloudService-project.</span><span class="sxs-lookup"><span data-stu-id="7b06e-159">If you're using Visual Studio 2015 or higher, change hello SQL Server connection string in hello application *Web.config* file of hello ContosoAdsWeb project and in hello *ServiceConfiguration.Local.cscfg* file of hello ContosoAdsCloudService project.</span></span> <span data-ttu-id="7b06e-160">In elk geval kan ook '(localdb) \v11.0' wijzigen '(localdb) \MSSQLLocalDB'.</span><span class="sxs-lookup"><span data-stu-id="7b06e-160">In each case, change "(localdb)\v11.0" too"(localdb)\MSSQLLocalDB".</span></span>
7. <span data-ttu-id="7b06e-161">Druk op CTRL + F5 toorun Hallo toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b06e-161">Press CTRL+F5 toorun hello application.</span></span>

    <span data-ttu-id="7b06e-162">Wanneer u een cloudserviceproject lokaal uitvoert, roept Visual Studio automatisch hello Azure *rekenemulator* en Azure *opslagemulator*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-162">When you run a cloud service project locally, Visual Studio automatically invokes hello Azure *compute emulator* and Azure *storage emulator*.</span></span> <span data-ttu-id="7b06e-163">Hallo compute emulator maakt gebruik van uw computer resources toosimulate Hallo-Webrol en omgevingen voor worker-rol.</span><span class="sxs-lookup"><span data-stu-id="7b06e-163">hello compute emulator uses your computer's resources toosimulate hello web role and worker role environments.</span></span> <span data-ttu-id="7b06e-164">Hallo-opslagemulator maakt gebruik van een [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) toosimulate Azure cloud-opslag van de database.</span><span class="sxs-lookup"><span data-stu-id="7b06e-164">hello storage emulator uses a [SQL Server Express LocalDB](http://msdn.microsoft.com/library/hh510202.aspx) database toosimulate Azure cloud storage.</span></span>

    <span data-ttu-id="7b06e-165">Hallo waarna eerste keer dat u een cloudserviceproject uitvoert een minuut Hallo emulators toostart up.</span><span class="sxs-lookup"><span data-stu-id="7b06e-165">hello first time you run a cloud service project, it takes a minute or so for hello emulators toostart up.</span></span> <span data-ttu-id="7b06e-166">Wanneer de emulator is opgestart, opent de standaardbrowser Hallo toohello toepassing-startpagina.</span><span class="sxs-lookup"><span data-stu-id="7b06e-166">When emulator startup is finished, hello default browser opens toohello application home page.</span></span>

    ![Architectuur van Contoso Ads](./media/cloud-services-dotnet-get-started/home.png)
8. <span data-ttu-id="7b06e-168">Klik op **Create an Ad**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-168">Click  **Create an Ad**.</span></span>
9. <span data-ttu-id="7b06e-169">Voer enkele testgegevens in en selecteer een *.jpg* tooupload installatiekopie en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-169">Enter some test data and select a *.jpg* image tooupload, and then click **Create**.</span></span>

    ![De pagina Create](./media/cloud-services-dotnet-get-started/create.png)

    <span data-ttu-id="7b06e-171">Hallo app gaat toohello indexpagina, maar niet wordt weergegeven een miniatuur voor de nieuwe ad Hallo omdat die verwerking nog niet heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-171">hello app goes toohello Index page, but it doesn't show a thumbnail for hello new ad because that processing hasn't happened yet.</span></span>
10. <span data-ttu-id="7b06e-172">Wacht even en vernieuw vervolgens Hallo Index pagina toosee Hallo miniatuur.</span><span class="sxs-lookup"><span data-stu-id="7b06e-172">Wait a moment and then refresh hello Index page toosee hello thumbnail.</span></span>

     ![De indexpagina](./media/cloud-services-dotnet-get-started/list.png)
11. <span data-ttu-id="7b06e-174">Klik op **Details** voor uw afbeelding van ad toosee Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-174">Click **Details** for your ad toosee hello full-size image.</span></span>

     ![De pagina Details](./media/cloud-services-dotnet-get-started/details.png)

<span data-ttu-id="7b06e-176">U hebt de toepassing hello uitgevoerd volledig op uw lokale computer, zonder verbinding toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="7b06e-176">You've been running hello application entirely on your local computer, with no connection toohello cloud.</span></span> <span data-ttu-id="7b06e-177">Hallo-opslagemulator slaat Hallo wachtrij en blobgegevens in een SQL Server Express LocalDB-database en de toepassing hello Hallo ad-gegevens opslaat in een andere LocalDB-database.</span><span class="sxs-lookup"><span data-stu-id="7b06e-177">hello storage emulator stores hello queue and blob data in a SQL Server Express LocalDB database, and hello application stores hello ad data in another LocalDB database.</span></span> <span data-ttu-id="7b06e-178">Entity Framework Code First automatisch gemaakte Hallo ad-database Hallo Hallo web-app heeft geprobeerd tooaccess eerst het.</span><span class="sxs-lookup"><span data-stu-id="7b06e-178">Entity Framework Code First automatically created hello ad database hello first time hello web app tried tooaccess it.</span></span>

<span data-ttu-id="7b06e-179">In de volgende sectie Hallo configureert u Hallo oplossing toouse Azure-cloudbronnen voor wachtrijen, blobs en Hallo toepassingsdatabase wanneer deze wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-179">In hello following section you'll configure hello solution toouse Azure cloud resources for queues, blobs, and hello application database when it runs in hello cloud.</span></span> <span data-ttu-id="7b06e-180">Als u lokaal toocontinue toorun wilden maar gebruik van cloud- en databasebronnen, kunt u dat doen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-180">If you wanted toocontinue toorun locally but use cloud storage and database resources, you could do that.</span></span> <span data-ttu-id="7b06e-181">Het is alleen een kwestie van het instellen van verbindingsreeksen, u ziet hoe toodo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-181">It's just a matter of setting connection strings, which you'll see how toodo.</span></span>

## <a name="deploy-hello-application-tooazure"></a><span data-ttu-id="7b06e-182">Hallo toepassing tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="7b06e-182">Deploy hello application tooAzure</span></span>
<span data-ttu-id="7b06e-183">U voert de volgende stappen toorun Hallo toepassing in de cloud Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b06e-183">You'll do hello following steps toorun hello application in hello cloud:</span></span>

* <span data-ttu-id="7b06e-184">Een Azure-cloudservice maken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-184">Create an Azure cloud service.</span></span>
* <span data-ttu-id="7b06e-185">Een Azure SQL-database maken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-185">Create an Azure SQL database.</span></span>
* <span data-ttu-id="7b06e-186">Een Azure-opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-186">Create an Azure storage account.</span></span>
* <span data-ttu-id="7b06e-187">Configureer Hallo oplossing toouse uw Azure SQL database als deze wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b06e-187">Configure hello solution toouse your Azure SQL database when it runs in Azure.</span></span>
* <span data-ttu-id="7b06e-188">Configureer Hallo oplossing toouse uw Azure storage-account wanneer deze wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b06e-188">Configure hello solution toouse your Azure storage account when it runs in Azure.</span></span>
* <span data-ttu-id="7b06e-189">Hallo project tooyour Azure cloudservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-189">Deploy hello project tooyour Azure cloud service.</span></span>

### <a name="create-an-azure-cloud-service"></a><span data-ttu-id="7b06e-190">Een Azure-cloudservice maken</span><span class="sxs-lookup"><span data-stu-id="7b06e-190">Create an Azure cloud service</span></span>
<span data-ttu-id="7b06e-191">Een Azure-cloudservice is Hallo omgeving Hallo toepassing wordt uitgevoerd in.</span><span class="sxs-lookup"><span data-stu-id="7b06e-191">An Azure cloud service is hello environment hello application will run in.</span></span>

1. <span data-ttu-id="7b06e-192">Open in uw browser Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7b06e-192">In your browser, open hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="7b06e-193">Klik op **Nieuw > Berekenen > Cloudservice**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-193">Click **New > Compute > Cloud Service**.</span></span>

3. <span data-ttu-id="7b06e-194">Voer in Hallo DNS-naam-invoervak een URL-voorvoegsel voor Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-194">In hello DNS name input box, enter a URL prefix for hello cloud service.</span></span>

    <span data-ttu-id="7b06e-195">Deze URL heeft toobe uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="7b06e-195">This URL has toobe unique.</span></span>  <span data-ttu-id="7b06e-196">U krijgt een foutmelding als Hallo voorvoegsel dat u kiest al in gebruik is.</span><span class="sxs-lookup"><span data-stu-id="7b06e-196">You'll get an error message if hello prefix you choose is already in use.</span></span>
4. <span data-ttu-id="7b06e-197">Geef een nieuwe resourcegroep voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7b06e-197">Specify a new Resource group for hello  service.</span></span> <span data-ttu-id="7b06e-198">Klik op **nieuw** en typ een naam in Hallo Resource groep invoervak, zoals CS_contososadsRG.</span><span class="sxs-lookup"><span data-stu-id="7b06e-198">Click **Create new** and then type a name in hello Resource group input box, such as CS_contososadsRG.</span></span>

5. <span data-ttu-id="7b06e-199">Hallo-regio waar u toodeploy Hallo toepassing kiezen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-199">Choose hello region where you want toodeploy hello application.</span></span>

    <span data-ttu-id="7b06e-200">Dit veld geeft aan in welk datacenter uw cloudservice zal worden gehost.</span><span class="sxs-lookup"><span data-stu-id="7b06e-200">This field specifies which datacenter your cloud service will be hosted in.</span></span> <span data-ttu-id="7b06e-201">Voor een productietoepassing kiest u Hallo regio dichtstbijzijnde tooyour klanten.</span><span class="sxs-lookup"><span data-stu-id="7b06e-201">For a production application, you'd choose hello region closest tooyour customers.</span></span> <span data-ttu-id="7b06e-202">Voor deze zelfstudie kiest Hallo regio dichtstbijzijnde tooyou.</span><span class="sxs-lookup"><span data-stu-id="7b06e-202">For this tutorial, choose hello region closest tooyou.</span></span>
5. <span data-ttu-id="7b06e-203">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-203">Click **Create**.</span></span>

    <span data-ttu-id="7b06e-204">In Hallo volgende afbeelding, een cloudservice met Hallo URL CSvccontosoads.cloudapp.net gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-204">In hello following image, a cloud service is created with hello URL CSvccontosoads.cloudapp.net.</span></span>

    ![Nieuwe cloudservice](./media/cloud-services-dotnet-get-started/newcs.png)

### <a name="create-an-azure-sql-database"></a><span data-ttu-id="7b06e-206">Een Azure SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="7b06e-206">Create an Azure SQL database</span></span>
<span data-ttu-id="7b06e-207">Wanneer Hallo-app wordt uitgevoerd in de cloud hello, wordt een cloud-gebaseerde database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-207">When hello app runs in hello cloud, it will use a cloud-based database.</span></span>

1. <span data-ttu-id="7b06e-208">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Nieuw > Databases > SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-208">In hello [Azure portal](https://portal.azure.com), click **New > Databases > SQL Database**.</span></span>
2. <span data-ttu-id="7b06e-209">In Hallo **databasenaam** Voer *contosoads*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-209">In hello **Database Name** box, enter *contosoads*.</span></span>
3. <span data-ttu-id="7b06e-210">In Hallo **resourcegroep**, klikt u op **gebruik bestaande** en selecteer Hallo resourcegroep gebruikt voor het Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-210">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
4. <span data-ttu-id="7b06e-211">Klik in het Hallo-installatiekopie, volgt op **Server - vereiste instellingen configureren** en **Maak een nieuwe server**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-211">In hello following image, click **Server - Configure required settings** and **Create a new server**.</span></span>

    ![Tunnel toodatabase server](./media/cloud-services-dotnet-get-started/newdb.png)

    <span data-ttu-id="7b06e-213">Als uw abonnement beschikt al over een server, kunt u ook die server selecteren uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-213">Alternatively, if your subscription already has a server, you can select that server from hello drop-down list.</span></span>
5. <span data-ttu-id="7b06e-214">In Hallo **servernaam** Voer *csvccontosodbserver*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-214">In hello **Server name** box, enter *csvccontosodbserver*.</span></span>

6. <span data-ttu-id="7b06e-215">Geef een **Aanmeldingsnaam** en een **Wachtwoord** op voor de beheerder.</span><span class="sxs-lookup"><span data-stu-id="7b06e-215">Enter an administrator **Login Name** and **Password**.</span></span>

    <span data-ttu-id="7b06e-216">Als u **Een nieuwe server maken** hebt geselecteerd, voert u hier geen bestaande naam en bestaand wachtwoord in.</span><span class="sxs-lookup"><span data-stu-id="7b06e-216">If you selected **Create a new server**, you aren't entering an existing name and password here.</span></span> <span data-ttu-id="7b06e-217">U invoert een nieuwe naam en het wachtwoord dat u nu toouse later definieert wanneer u Hallo database.</span><span class="sxs-lookup"><span data-stu-id="7b06e-217">You're entering a new name and password that you're defining now toouse later when you access hello database.</span></span> <span data-ttu-id="7b06e-218">Als u een server die u eerder hebt gemaakt, hebt geselecteerd, wordt u gevraagd voor Hallo wachtwoord toohello gebruiker met beheerdersrechten account die u al hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-218">If you selected a server that you created previously, you'll be prompted for hello password toohello administrative user account you already created.</span></span>
7. <span data-ttu-id="7b06e-219">Kies dezelfde Hallo **locatie** die u hebt gekozen voor Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-219">Choose hello same **Location** that you chose for hello cloud service.</span></span>

    <span data-ttu-id="7b06e-220">Wanneer Hallo-cloudservice en de database zich in verschillende datacenters (verschillende regio's), de latentie toe en wordt u gefactureerd voor de bandbreedte buiten het datacenter Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-220">When hello cloud service and database are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="7b06e-221">Bandbreedte binnen een datacenter is gratis.</span><span class="sxs-lookup"><span data-stu-id="7b06e-221">Bandwidth within a data center is free.</span></span>
8. <span data-ttu-id="7b06e-222">Controleer **toestaan azure-services tooaccess server**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-222">Check **Allow azure services tooaccess server**.</span></span>
9. <span data-ttu-id="7b06e-223">Klik op **Selecteer** voor Hallo nieuwe server.</span><span class="sxs-lookup"><span data-stu-id="7b06e-223">Click **Select** for hello new server.</span></span>

    ![Nieuwe SQL-databaseserver](./media/cloud-services-dotnet-get-started/newdbserver.png)
10. <span data-ttu-id="7b06e-225">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-225">Click **Create**.</span></span>

### <a name="create-an-azure-storage-account"></a><span data-ttu-id="7b06e-226">Een Azure-opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="7b06e-226">Create an Azure storage account</span></span>
<span data-ttu-id="7b06e-227">Een Azure-opslagaccount biedt resources voor het opslaan van wachtrij en de blob-gegevens in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-227">An Azure storage account provides resources for storing queue and blob data in hello cloud.</span></span>

<span data-ttu-id="7b06e-228">In een echte toepassing maakt u meestal afzonderlijke accounts voor toepassingsgegevens versus logboekgegevens, en afzonderlijke accounts voor testgegevens versus productiegegevens.</span><span class="sxs-lookup"><span data-stu-id="7b06e-228">In a real-world application, you would typically create separate accounts for application data versus logging data, and separate accounts for test data versus production data.</span></span> <span data-ttu-id="7b06e-229">Voor deze zelfstudie gebruikt u slechts één account.</span><span class="sxs-lookup"><span data-stu-id="7b06e-229">For this tutorial, you'll use just one account.</span></span>

1. <span data-ttu-id="7b06e-230">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **Nieuw > opslag > opslagaccount - blob, bestand, tabel, wachtrij**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-230">In hello [Azure portal](https://portal.azure.com), click **New > Storage > Storage account - blob, file, table, queue**.</span></span>
2. <span data-ttu-id="7b06e-231">In Hallo **naam** Voer een URL-voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="7b06e-231">In hello **Name** box, enter a URL prefix.</span></span>

    <span data-ttu-id="7b06e-232">Dit voorvoegsel wordt samen met Hallo tekst onder Hallo vak worden Hallo unieke URL tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="7b06e-232">This prefix plus hello text you see under hello box will be hello unique URL tooyour storage account.</span></span> <span data-ttu-id="7b06e-233">Als het voorvoegsel dat u invoert Hallo is al door iemand anders gebruikt, hebt u toochoose een ander voorvoegsel.</span><span class="sxs-lookup"><span data-stu-id="7b06e-233">If hello prefix you enter has already been used by someone else, you'll have toochoose a different prefix.</span></span>
3. <span data-ttu-id="7b06e-234">Set Hallo **implementatiemodel** te*klassieke*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-234">Set hello **Deployment model** too*Classic*.</span></span>

4. <span data-ttu-id="7b06e-235">Set Hallo **replicatie** vervolgkeuzelijst te**lokaal redundante opslag**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-235">Set hello **Replication** drop-down list too**Locally redundant storage**.</span></span>

    <span data-ttu-id="7b06e-236">Wanneer geo-replicatie is ingeschakeld voor een opslagaccount, is Hallo opgeslagen inhoud gerepliceerde tooa secundair datacenter tooenable failover als er een noodgeval op de primaire locatie Hallo optreedt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-236">When geo-replication is enabled for a storage account, hello stored content is replicated tooa secondary datacenter tooenable failover if a major disaster occurs in hello primary location.</span></span> <span data-ttu-id="7b06e-237">Geo-replicatie kan extra kosten met zich meebrengen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-237">Geo-replication can incur additional costs.</span></span> <span data-ttu-id="7b06e-238">Voor test- en -accounts in het algemeen niet de bedoeling toopay voor geo-replicatie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-238">For test and development accounts, you generally don't want toopay for geo-replication.</span></span> <span data-ttu-id="7b06e-239">Zie [Een opslagaccount maken, beheren of verwijderen](../storage/common/storage-create-storage-account.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-239">For more information, see [Create, manage, or delete a storage account](../storage/common/storage-create-storage-account.md).</span></span>

5. <span data-ttu-id="7b06e-240">In Hallo **resourcegroep**, klikt u op **gebruik bestaande** en selecteer Hallo resourcegroep gebruikt voor het Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-240">In hello **Resource group**, click **Use existing** and select hello resource group used for hello cloud service.</span></span>
6. <span data-ttu-id="7b06e-241">Set Hallo **locatie** vervolgkeuzelijst toohello dezelfde regio die u hebt gekozen voor Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-241">Set hello **Location** drop-down list toohello same region you chose for hello cloud service.</span></span>

    <span data-ttu-id="7b06e-242">Wanneer Hallo cloud service- en storage-account zich in verschillende datacenters (verschillende regio's), de latentie toe en wordt u gefactureerd voor de bandbreedte buiten het datacenter Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-242">When hello cloud service and storage account are in different datacenters (different regions), latency will increase and you will be charged for bandwidth outside hello data center.</span></span> <span data-ttu-id="7b06e-243">Bandbreedte binnen een datacenter is gratis.</span><span class="sxs-lookup"><span data-stu-id="7b06e-243">Bandwidth within a data center is free.</span></span>

    <span data-ttu-id="7b06e-244">Azure-affiniteitsgroepen bieden een mechanisme toominimize Hallo afstand tussen resources in een datacenter, waardoor latentie kan verminderen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-244">Azure affinity groups provide a mechanism toominimize hello distance between resources in a data center, which can reduce latency.</span></span> <span data-ttu-id="7b06e-245">In deze zelfstudie worden geen affiniteitsgroepen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-245">This tutorial does not use affinity groups.</span></span> <span data-ttu-id="7b06e-246">Zie voor meer informatie [hoe tooCreate een affiniteit groepeert in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b06e-246">For more information, see [How tooCreate an Affinity Group in Azure](http://msdn.microsoft.com/library/jj156209.aspx).</span></span>
7. <span data-ttu-id="7b06e-247">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-247">Click **Create**.</span></span>

    ![Nieuw opslagaccount](./media/cloud-services-dotnet-get-started/newstorage.png)

    <span data-ttu-id="7b06e-249">In afbeelding hello, een opslagaccount is gemaakt met Hallo URL `csvccontosoads.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="7b06e-249">In hello image, a storage account is created with hello URL `csvccontosoads.core.windows.net`.</span></span>

### <a name="configure-hello-solution-toouse-your-azure-sql-database-when-it-runs-in-azure"></a><span data-ttu-id="7b06e-250">Hallo oplossing toouse configureren uw Azure SQL database als deze wordt uitgevoerd in Azure</span><span class="sxs-lookup"><span data-stu-id="7b06e-250">Configure hello solution toouse your Azure SQL database when it runs in Azure</span></span>
<span data-ttu-id="7b06e-251">Hallo-webproject hello werkrolproject elke heeft een eigen databaseverbindingsreeks en elk toopoint toohello Azure SQL-database moet bij het Hallo-app wordt uitgevoerd in Azure.</span><span class="sxs-lookup"><span data-stu-id="7b06e-251">hello web project and hello worker role project each has its own database connection string, and each needs toopoint toohello Azure SQL database when hello app runs in Azure.</span></span>

<span data-ttu-id="7b06e-252">U gebruikt een [Web.config-transformatie](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) voor Hallo-Webrol en een cloud service-omgeving-instelling voor Hallo-werkrol.</span><span class="sxs-lookup"><span data-stu-id="7b06e-252">You'll use a [Web.config transform](http://www.asp.net/mvc/tutorials/deployment/visual-studio-web-deployment/web-config-transformations) for hello web role and a cloud service environment setting for hello worker role.</span></span>

> [!NOTE]
> <span data-ttu-id="7b06e-253">In deze sectie en de volgende sectie hello slaat u referenties op in projectbestanden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-253">In this section and hello next section, you store credentials in project files.</span></span> <span data-ttu-id="7b06e-254">[Sla gevoelige gegevens niet op in openbare broncodeopslagplaatsen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span><span class="sxs-lookup"><span data-stu-id="7b06e-254">[Don't store sensitive data in public source code repositories](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control#secrets).</span></span>
>
>

1. <span data-ttu-id="7b06e-255">Open in het project ContosoAdsWeb Hallo Hallo *Web.Release.config* transformatiebestand voor de toepassing hello *Web.config* , verwijder Hallo Opmerkingenblok met een `<connectionStrings>` -element en plak Hallo code in plaats daarvan te volgen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-255">In hello ContosoAdsWeb project, open hello *Web.Release.config* transform file for hello application *Web.config* file, delete hello comment block that contains a `<connectionStrings>` element, and paste hello following code in its place.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="{connectionstring}"
        providerName="System.Data.SqlClient" xdt:Transform="SetAttributes" xdt:Locator="Match(name)"/>
    </connectionStrings>
    ```

    <span data-ttu-id="7b06e-256">Laat Hallo bestand geopend voor bewerken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-256">Leave hello file open for editing.</span></span>
2. <span data-ttu-id="7b06e-257">In Hallo [Azure-portal](https://portal.azure.com), klikt u op **SQL-Databases** in het linkerdeelvenster hello, klikt u op Hallo-database die u voor deze zelfstudie hebt gemaakt en klik vervolgens op **verbindingsreeksen weergeven**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-257">In hello [Azure portal](https://portal.azure.com), click **SQL Databases** in hello left pane, click hello database you created for this tutorial, and then click **Show connection strings**.</span></span>

    ![Verbindingsreeksen weergeven](./media/cloud-services-dotnet-get-started/showcs.png)

    <span data-ttu-id="7b06e-259">Hallo portal worden verbindingsreeksen met een tijdelijke aanduiding voor Hallo wachtwoord weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-259">hello portal displays connection strings, with a placeholder for hello password.</span></span>

    ![Verbindingsreeksen](./media/cloud-services-dotnet-get-started/connstrings.png)
3. <span data-ttu-id="7b06e-261">In Hallo *Web.Release.config* transformatiebestand `{connectionstring}` en plak in de plaats Hallo ADO.NET-verbindingsreeks uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="7b06e-261">In hello *Web.Release.config* transform file, delete `{connectionstring}` and paste in its place hello ADO.NET connection string from hello Azure portal.</span></span>
4. <span data-ttu-id="7b06e-262">In de verbindingsreeks Hallo die u in Hallo geplakt *Web.Release.config* transformatiebestand, vervangen door `{your_password_here}` met Hallo wachtwoord die u hebt gemaakt voor Hallo nieuwe SQL-database.</span><span class="sxs-lookup"><span data-stu-id="7b06e-262">In hello connection string that you pasted into hello *Web.Release.config* transform file, replace `{your_password_here}` with hello password you created for hello new SQL database.</span></span>
5. <span data-ttu-id="7b06e-263">Hallo-bestand opslaan.</span><span class="sxs-lookup"><span data-stu-id="7b06e-263">Save hello file.</span></span>  
6. <span data-ttu-id="7b06e-264">Selecteer en kopieer de verbindingsreeks Hallo (zonder Hallo aanhalingstekens rond) voor gebruik in de volgende stappen uit voor het configureren van het werkrolproject Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-264">Select and copy hello connection string (without hello surrounding quotation marks) for use in hello following steps for configuring hello worker role project.</span></span>
7. <span data-ttu-id="7b06e-265">In **Solution Explorer**onder **rollen** hello cloudserviceproject met de rechtermuisknop op **ContosoAdsWorker** en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-265">In **Solution Explorer**, under **Roles** in hello cloud service project, right-click **ContosoAdsWorker** and then click **Properties**.</span></span>

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/rolepropertiesworker.png)
8. <span data-ttu-id="7b06e-267">Klik op Hallo **instellingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="7b06e-267">Click hello **Settings** tab.</span></span>
9. <span data-ttu-id="7b06e-268">Wijziging **serviceconfiguratie** te**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-268">Change **Service Configuration** too**Cloud**.</span></span>
10. <span data-ttu-id="7b06e-269">Selecteer Hallo **waarde** veld voor Hallo `ContosoAdsDbConnectionString` instelling en plak Hallo verbindingsreeks die u hebt gekopieerd uit de vorige sectie Hallo Hallo zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-269">Select hello **Value** field for hello `ContosoAdsDbConnectionString` setting, and then paste hello connection string that you copied from hello previous section of hello tutorial.</span></span>

     ![Databaseverbindingsreeks voor werkrol](./media/cloud-services-dotnet-get-started/workerdbcs.png)
11. <span data-ttu-id="7b06e-271">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="7b06e-271">Save your changes.</span></span>  

### <a name="configure-hello-solution-toouse-your-azure-storage-account-when-it-runs-in-azure"></a><span data-ttu-id="7b06e-272">Hallo oplossing toouse configureren uw Azure-opslagaccount als deze wordt uitgevoerd in Azure</span><span class="sxs-lookup"><span data-stu-id="7b06e-272">Configure hello solution toouse your Azure storage account when it runs in Azure</span></span>
<span data-ttu-id="7b06e-273">Azure storage-account-verbindingsreeksen voor zowel het webrolproject Hallo als Hallo werkrolproject worden opgeslagen in de omgevingsinstellingen in het cloudserviceproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-273">Azure storage account connection strings for both hello web role project and hello worker role project are stored in environment settings in hello cloud service project.</span></span> <span data-ttu-id="7b06e-274">Er is een afzonderlijke reeks instellingen toobe gebruikt bij het Hallo-toepassing lokaal wordt uitgevoerd en wanneer deze wordt uitgevoerd in de cloud Hallo voor elk project.</span><span class="sxs-lookup"><span data-stu-id="7b06e-274">For each project, there is a separate set of settings toobe used when hello application runs locally and when it runs in hello cloud.</span></span> <span data-ttu-id="7b06e-275">U zult Hallo cloudomgevingsinstellingen voor zowel web als het werkrolproject bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-275">You'll update hello cloud environment settings for both web and worker role projects.</span></span>

1. <span data-ttu-id="7b06e-276">In **Solution Explorer**, met de rechtermuisknop op **ContosoAdsWeb** onder **rollen** in Hallo **ContosoAdsCloudService** project en klik vervolgens op **Eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-276">In **Solution Explorer**, right-click **ContosoAdsWeb** under **Roles** in hello **ContosoAdsCloudService** project, and then click **Properties**.</span></span>

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/roleproperties.png)
2. <span data-ttu-id="7b06e-278">Klik op Hallo **instellingen** tabblad. In Hallo **serviceconfiguratie** vervolgkeuzelijst Kies **Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-278">Click hello **Settings** tab. In hello **Service Configuration** drop-down box, choose **Cloud**.</span></span>

    ![Cloudconfiguratie](./media/cloud-services-dotnet-get-started/sccloud.png)
3. <span data-ttu-id="7b06e-280">Selecteer Hallo **StorageConnectionString** invoer en u ziet een weglatingsteken (**...** ) knop Hallo rechts Hallo-regel op.</span><span class="sxs-lookup"><span data-stu-id="7b06e-280">Select hello **StorageConnectionString** entry, and you'll see an ellipsis (**...**) button at hello right end of hello line.</span></span> <span data-ttu-id="7b06e-281">Klik op Hallo weglatingsteken knop tooopen hello **Create Storage Account Connection String** in het dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="7b06e-281">Click hello ellipsis button tooopen hello **Create Storage Account Connection String** dialog box.</span></span>

    ![Het dialoogvenster Create Storage Connection String](./media/cloud-services-dotnet-get-started/opencscreate.png)
4. <span data-ttu-id="7b06e-283">In Hallo **Create Storage Connection String** in het dialoogvenster, klikt u op **uw abonnement**, kies Hallo storage-account dat u eerder hebt gemaakt en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-283">In hello **Create Storage Connection String** dialog box, click **Your subscription**, choose hello storage account that you created earlier, and then click **OK**.</span></span> <span data-ttu-id="7b06e-284">Als u nog niet bent aangemeld, wordt u gevraagd om uw referenties voor uw Azure-account op te geven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-284">If you're not already logged in, you'll be prompted for your Azure account credentials.</span></span>

    ![Verbindingsreeks voor opslag maken](./media/cloud-services-dotnet-get-started/createstoragecs.png)
5. <span data-ttu-id="7b06e-286">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="7b06e-286">Save your changes.</span></span>
6. <span data-ttu-id="7b06e-287">Volg Hallo dezelfde procedure die u voor Hallo gebruikt `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="7b06e-287">Follow hello same procedure that you used for hello `StorageConnectionString` connection string tooset hello `Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString` connection string.</span></span>

    <span data-ttu-id="7b06e-288">Deze verbindingsreeks wordt gebruikt voor logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-288">This connection string is used for logging.</span></span>
7. <span data-ttu-id="7b06e-289">Volg Hallo dezelfde procedure die u voor Hallo gebruikt **ContosoAdsWeb** rol tooset beide verbindingsreeksen voor Hallo **ContosoAdsWorker** rol.</span><span class="sxs-lookup"><span data-stu-id="7b06e-289">Follow hello same procedure that you used for hello **ContosoAdsWeb** role tooset both connection strings for hello **ContosoAdsWorker** role.</span></span> <span data-ttu-id="7b06e-290">Vergeet niet tooset **serviceconfiguratie** te**Cloud**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-290">Don't forget tooset **Service Configuration** too**Cloud**.</span></span>

<span data-ttu-id="7b06e-291">Hallo rolomgevingsinstellingen dat u hebt geconfigureerd met behulp van Visual Studio-gebruikersinterface Hallo worden opgeslagen in de volgende bestanden in de project ContosoAdsCloudService Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="7b06e-291">hello role environment settings that you have configured using hello Visual Studio UI are stored in hello following files in hello ContosoAdsCloudService project:</span></span>

* <span data-ttu-id="7b06e-292">*ServiceDefinition.csdef* -namen Hallo definieert.</span><span class="sxs-lookup"><span data-stu-id="7b06e-292">*ServiceDefinition.csdef* - Defines hello setting names.</span></span>
* <span data-ttu-id="7b06e-293">*ServiceConfiguration.Cloud.cscfg* -levert waarden voor wanneer Hallo-app wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-293">*ServiceConfiguration.Cloud.cscfg* - Provides values for when hello app runs in hello cloud.</span></span>
* <span data-ttu-id="7b06e-294">*ServiceConfiguration.Local.cscfg* -levert waarden voor wanneer Hallo app lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-294">*ServiceConfiguration.Local.cscfg* - Provides values for when hello app runs locally.</span></span>

<span data-ttu-id="7b06e-295">Hallo ServiceDefinition.csdef omvat bijvoorbeeld Hallo definities te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b06e-295">For example, hello ServiceDefinition.csdef includes hello following definitions:</span></span>

```xml
<ConfigurationSettings>
    <Setting name="StorageConnectionString" />
    <Setting name="ContosoAdsDbConnectionString" />
</ConfigurationSettings>
```

<span data-ttu-id="7b06e-296">En Hallo *ServiceConfiguration.Cloud.cscfg* bestand bevat Hallo-waarden die u hebt ingevoerd voor deze instellingen in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b06e-296">And hello *ServiceConfiguration.Cloud.cscfg* file includes hello values you entered for those settings in Visual Studio.</span></span>

```xml
<Role name="ContosoAdsWorker">
    <Instances count="1" />
    <ConfigurationSettings>
        <Setting name="StorageConnectionString" value="{yourconnectionstring}" />
        <Setting name="ContosoAdsDbConnectionString" value="{yourconnectionstring}" />
        <!-- other settings not shown -->

    </ConfigurationSettings>
    <!-- other settings not shown -->

</Role>
```

<span data-ttu-id="7b06e-297">Hallo `<Instances>` instelling bepaalt u het aantal virtuele machines die door Azure wordt uitgevoerd Hallo worker-rol op Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-297">hello `<Instances>` setting specifies hello number of virtual machines that Azure will run hello worker role code on.</span></span> <span data-ttu-id="7b06e-298">Hallo [Vervolgstappen](#next-steps) sectie bevat koppelingen toomore informatie over het uitbreiden van een cloudservice</span><span class="sxs-lookup"><span data-stu-id="7b06e-298">hello [Next steps](#next-steps) section includes links toomore information about scaling out a cloud service,</span></span>

### <a name="deploy-hello-project-tooazure"></a><span data-ttu-id="7b06e-299">Hallo project tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="7b06e-299">Deploy hello project tooAzure</span></span>
1. <span data-ttu-id="7b06e-300">In **Solution Explorer**, klik met de rechtermuisknop Hallo **ContosoAdsCloudService** cloudproject en selecteer vervolgens **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-300">In **Solution Explorer**, right-click hello **ContosoAdsCloudService** cloud project and then select **Publish**.</span></span>

   ![Het menu Publish](./media/cloud-services-dotnet-get-started/pubmenu.png)
2. <span data-ttu-id="7b06e-302">In Hallo **aanmelden** stap Hallo **Publish Azure Application** wizard, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-302">In hello **Sign in** step of hello **Publish Azure Application** wizard, click **Next**.</span></span>

    ![Aanmeldingsstap](./media/cloud-services-dotnet-get-started/pubsignin.png)
3. <span data-ttu-id="7b06e-304">In Hallo **instellingen** stap van de wizard hello, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-304">In hello **Settings** step of hello wizard, click **Next**.</span></span>

    ![De stap Settings](./media/cloud-services-dotnet-get-started/pubsettings.png)

    <span data-ttu-id="7b06e-306">Standaard-instellingen in Hallo Hallo **Geavanceerd** tabblad zijn afdoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-306">hello default settings in hello **Advanced** tab are fine for this tutorial.</span></span> <span data-ttu-id="7b06e-307">Zie voor meer informatie over geavanceerde tabblad Hallo [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span><span class="sxs-lookup"><span data-stu-id="7b06e-307">For information about hello advanced tab, see [Publish Azure Application Wizard](http://msdn.microsoft.com/library/hh535756.aspx).</span></span>
4. <span data-ttu-id="7b06e-308">In Hallo **samenvatting** stap, klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-308">In hello **Summary** step, click **Publish**.</span></span>

    ![De stap Summary](./media/cloud-services-dotnet-get-started/pubsummary.png)

   <span data-ttu-id="7b06e-310">Hallo **Azure Activity Log** venster wordt geopend in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7b06e-310">hello **Azure Activity Log** window opens in Visual Studio.</span></span>
5. <span data-ttu-id="7b06e-311">Klik op Hallo pijl naar rechts pictogram tooexpand Hallo details van de implementatie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-311">Click hello right arrow icon tooexpand hello deployment details.</span></span>

    <span data-ttu-id="7b06e-312">Hallo-implementatie kan too5 minuten of meer toocomplete duren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-312">hello deployment can take up too5 minutes or more toocomplete.</span></span>

    ![Het venster Azure Activity Log](./media/cloud-services-dotnet-get-started/waal.png)
6. <span data-ttu-id="7b06e-314">Als de implementatiestatus Hallo voltooid is, klikt u op Hallo **Web-app-URL** toostart Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="7b06e-314">When hello deployment status is complete, click hello **Web app URL** toostart hello application.</span></span>
7. <span data-ttu-id="7b06e-315">U kunt nu Hallo app testen door maken, weergeven en bewerken van advertenties, net als bij u Hallo toepassing lokaal uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-315">You can now test hello app by creating, viewing, and editing some ads, as you did when you ran hello application locally.</span></span>

> [!NOTE]
> <span data-ttu-id="7b06e-316">Wanneer u bent klaar met testen, verwijderen of stoppen Hallo-cloudservice.</span><span class="sxs-lookup"><span data-stu-id="7b06e-316">When you're finished testing, delete or stop hello cloud service.</span></span> <span data-ttu-id="7b06e-317">Zelfs als u geen Hallo cloudservice gebruikt, lopen de kosten omdat bronnen voor virtuele machines worden gereserveerd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-317">Even if you're not using hello cloud service, it's accruing charges because virtual machine resources are reserved for it.</span></span> <span data-ttu-id="7b06e-318">Als u de cloudservice actief laat, kan bovendien iedereen die uw URL vindt, advertenties maken en weergeven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-318">And if you leave it running, anyone who finds your URL can create and view ads.</span></span> <span data-ttu-id="7b06e-319">In Hallo [Azure-portal](https://portal.azure.com), gaat u toohello **overzicht** tabblad voor de cloudservice en klik vervolgens op Hallo **verwijderen** knop bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="7b06e-319">In hello [Azure portal](https://portal.azure.com), go toohello **Overview** tab for your cloud service, and then click hello **Delete** button at hello top of hello page.</span></span> <span data-ttu-id="7b06e-320">Als u alleen wilt tootemporarily voorkomen dat anderen toegang hebben tot Hallo-site, klikt u op **stoppen** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="7b06e-320">If you just want tootemporarily prevent others from accessing hello site, click **Stop** instead.</span></span> <span data-ttu-id="7b06e-321">In dat geval blijven de kosten tooaccrue.</span><span class="sxs-lookup"><span data-stu-id="7b06e-321">In that case, charges will continue tooaccrue.</span></span> <span data-ttu-id="7b06e-322">Wanneer u ze niet meer nodig hebt, kunt u een vergelijkbare procedure toodelete Hallo account voor SQL database- en opslaggroepen volgen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-322">You can follow a similar procedure toodelete hello SQL database and storage account when you no longer need them.</span></span>
>
>

## <a name="create-hello-application-from-scratch"></a><span data-ttu-id="7b06e-323">Hallo toepassing vanaf het begin maken</span><span class="sxs-lookup"><span data-stu-id="7b06e-323">Create hello application from scratch</span></span>
<span data-ttu-id="7b06e-324">Als u nog niet hebt gedownload [toepassing hello voltooid](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), doet u dat nu.</span><span class="sxs-lookup"><span data-stu-id="7b06e-324">If you haven't already downloaded [hello completed application](http://code.msdn.microsoft.com/Simple-Azure-Cloud-Service-e01df2e4), do that now.</span></span> <span data-ttu-id="7b06e-325">U kopieert de bestanden uit project Hallo gedownload naar het nieuwe project Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-325">You'll copy files from hello downloaded project into hello new project.</span></span>

<span data-ttu-id="7b06e-326">Hallo Contoso Ads-toepassing maken omvat Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b06e-326">Creating hello Contoso Ads application involves hello following steps:</span></span>

* <span data-ttu-id="7b06e-327">Met Visual Studio een cloudserviceoplossing maken.</span><span class="sxs-lookup"><span data-stu-id="7b06e-327">Create a cloud service Visual Studio solution.</span></span>
* <span data-ttu-id="7b06e-328">NuGet-pakketten bijwerken en toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-328">Update and add NuGet packages.</span></span>
* <span data-ttu-id="7b06e-329">Projectverwijzingen instellen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-329">Set project references.</span></span>
* <span data-ttu-id="7b06e-330">Verbindingsreeksen configureren.</span><span class="sxs-lookup"><span data-stu-id="7b06e-330">Configure connection strings.</span></span>
* <span data-ttu-id="7b06e-331">Codebestanden toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-331">Add code files.</span></span>

<span data-ttu-id="7b06e-332">Nadat het Hallo-oplossing is gemaakt, bekijkt u Hallo-code die uniek toocloud serviceprojecten en Azure blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-332">After hello solution is created, you'll review hello code that is unique toocloud service projects and Azure blobs and queues.</span></span>

### <a name="create-a-cloud-service-visual-studio-solution"></a><span data-ttu-id="7b06e-333">Met Visual Studio een cloudserviceoplossing maken</span><span class="sxs-lookup"><span data-stu-id="7b06e-333">Create a cloud service Visual Studio solution</span></span>
1. <span data-ttu-id="7b06e-334">Kies in Visual Studio **nieuw Project** van Hallo **bestand** menu.</span><span class="sxs-lookup"><span data-stu-id="7b06e-334">In Visual Studio, choose **New Project** from hello **File** menu.</span></span>
2. <span data-ttu-id="7b06e-335">In het linkerdeelvenster van Hallo Hallo **nieuw Project** dialoogvenster Vouw **Visual C#** en kies **Cloud** sjablonen, en kies vervolgens Hallo **Azure Cloud Service** sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7b06e-335">In hello left pane of hello **New Project** dialog box, expand **Visual C#** and choose **Cloud** templates, and then choose hello **Azure Cloud Service** template.</span></span>
3. <span data-ttu-id="7b06e-336">Naam Hallo-project en de oplossing ContosoAdsCloudService en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-336">Name hello project and solution ContosoAdsCloudService, and then click **OK**.</span></span>

    ![Nieuw project](./media/cloud-services-dotnet-get-started/newproject.png)
4. <span data-ttu-id="7b06e-338">In Hallo **New Azure Cloud Service** dialoogvenster Voeg een Webrol en een werkrol toe.</span><span class="sxs-lookup"><span data-stu-id="7b06e-338">In hello **New Azure Cloud Service** dialog box, add a web role and a worker role.</span></span> <span data-ttu-id="7b06e-339">Hallo-Webrol ContosoAdsWeb een naam en de naam Hallo werkrol ContosoAdsWorker.</span><span class="sxs-lookup"><span data-stu-id="7b06e-339">Name hello web role ContosoAdsWeb, and name hello worker role ContosoAdsWorker.</span></span> <span data-ttu-id="7b06e-340">(Hallo potloodpictogram in Hallo rechterdeelvenster toochange Hallo standaardnamen van Hallo-functies gebruiken.)</span><span class="sxs-lookup"><span data-stu-id="7b06e-340">(Use hello pencil icon in hello right-hand pane toochange hello default names of hello roles.)</span></span>

    ![Nieuw cloudserviceproject](./media/cloud-services-dotnet-get-started/newcsproj.png)
5. <span data-ttu-id="7b06e-342">Wanneer er Hallo **nieuw ASP.NET-Project** in het dialoogvenster voor de Webrol hello, kies Hallo MVC-sjabloon en klik vervolgens op **verificatie wijzigen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-342">When you see hello **New ASP.NET Project** dialog box for hello web role, choose hello MVC template, and then click **Change Authentication**.</span></span>

    ![Verificatie wijzigen](./media/cloud-services-dotnet-get-started/chgauth.png)
6. <span data-ttu-id="7b06e-344">In Hallo **verificatie wijzigen** dialoogvenster Kies **geen verificatie**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-344">In hello **Change Authentication** dialog box, choose **No Authentication**, and then click **OK**.</span></span>

    ![Geen verificatie](./media/cloud-services-dotnet-get-started/noauth.png)
7. <span data-ttu-id="7b06e-346">In Hallo **nieuw ASP.NET-Project** dialoogvenster, klikt u op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-346">In hello **New ASP.NET Project** dialog, click **OK**.</span></span>
8. <span data-ttu-id="7b06e-347">In **Solution Explorer**, met de rechtermuisknop op het Hallo-oplossing (niet een van de Hallo projecten) en kies **Add - New Project**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-347">In **Solution Explorer**, right-click hello solution (not one of hello projects), and choose **Add - New Project**.</span></span>
9. <span data-ttu-id="7b06e-348">In Hallo **Add New Project** dialoogvenster Kies **Windows** onder **Visual C#** in linkerdeelvenster hello, en klik vervolgens op Hallo **Class Library** de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="7b06e-348">In hello **Add New Project** dialog box, choose **Windows** under **Visual C#** in hello left pane, and then click hello **Class Library** template.</span></span>  
10. <span data-ttu-id="7b06e-349">Naam Hallo project *ContosoAdsCommon*, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-349">Name hello project *ContosoAdsCommon*, and then click **OK**.</span></span>

    <span data-ttu-id="7b06e-350">U moet tooreference Hallo Entity Framework context en Hallo-gegevensmodel van web- en werkrollen rol projecten.</span><span class="sxs-lookup"><span data-stu-id="7b06e-350">You need tooreference hello Entity Framework context and hello data model from both web and worker role projects.</span></span> <span data-ttu-id="7b06e-351">Als alternatief kan u Hallo EF-gerelateerde klassen definiëren in het webrolproject hello en van Hallo werkrolproject naar verwijzen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-351">As an alternative, you could define hello EF-related classes in hello web role project and reference that project from hello worker role project.</span></span> <span data-ttu-id="7b06e-352">Maar in de alternatieve methode hello, uw werkrolproject een assembly-verwijzingen tooweb die niet meer nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-352">But in hello alternative approach, your worker role project would have a reference tooweb assemblies that it doesn't need.</span></span>

### <a name="update-and-add-nuget-packages"></a><span data-ttu-id="7b06e-353">NuGet-pakketten bijwerken en toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b06e-353">Update and add NuGet packages</span></span>
1. <span data-ttu-id="7b06e-354">Open Hallo **NuGet-pakketten beheren** in het dialoogvenster voor het Hallo-oplossing.</span><span class="sxs-lookup"><span data-stu-id="7b06e-354">Open hello **Manage NuGet Packages** dialog box for hello solution.</span></span>
2. <span data-ttu-id="7b06e-355">Selecteer bovenaan Hallo Hallo-venster, **Updates**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-355">At hello top of hello window, select **Updates**.</span></span>
3. <span data-ttu-id="7b06e-356">Zoek naar Hallo *WindowsAzure.Storage* van het pakket en als het in de lijst hello, selecteert u deze en selecteer Hallo web- en werkrollen projecten tooupdate in en klik vervolgens op **Update**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-356">Look for hello *WindowsAzure.Storage* package, and if it's in hello list, select it and select hello web and worker projects tooupdate it in, and then click **Update**.</span></span>

    <span data-ttu-id="7b06e-357">Hallo opslagclientbibliotheek wordt vaker bijgewerkt dan Visual Studio-projectsjablonen, zodat u vaak die Hallo-versie in een nieuw gemaakt project moet toobe bijgewerkt zult.</span><span class="sxs-lookup"><span data-stu-id="7b06e-357">hello storage client library is updated more frequently than Visual Studio project templates, so you'll often find that hello version in a newly-created project needs toobe updated.</span></span>
4. <span data-ttu-id="7b06e-358">Selecteer bovenaan Hallo Hallo-venster, **Bladeren**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-358">At hello top of hello window, select **Browse**.</span></span>
5. <span data-ttu-id="7b06e-359">Hallo zoeken *EntityFramework* NuGet-pakket en installeer het in alle drie de projecten.</span><span class="sxs-lookup"><span data-stu-id="7b06e-359">Find hello *EntityFramework* NuGet package, and install it in all three projects.</span></span>
6. <span data-ttu-id="7b06e-360">Hallo zoeken *Microsoft.WindowsAzure.ConfigurationManager* NuGet-pakket en installeer het in het werkrolproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-360">Find hello *Microsoft.WindowsAzure.ConfigurationManager* NuGet package, and install it in hello worker role project.</span></span>

### <a name="set-project-references"></a><span data-ttu-id="7b06e-361">Projectverwijzingen instellen</span><span class="sxs-lookup"><span data-stu-id="7b06e-361">Set project references</span></span>
1. <span data-ttu-id="7b06e-362">In Hallo ingesteld project ContosoAdsWeb een verwijzing toohello ContosoAdsCommon project.</span><span class="sxs-lookup"><span data-stu-id="7b06e-362">In hello ContosoAdsWeb project, set a reference toohello ContosoAdsCommon project.</span></span> <span data-ttu-id="7b06e-363">Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **verwijzingen** - **Add References**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-363">Right-click hello ContosoAdsWeb project, and then click **References** - **Add References**.</span></span> <span data-ttu-id="7b06e-364">In Hallo **Reference Manager** dialoogvenster, **Solution – Projects** selecteren in het linkerdeelvenster Hallo **ContosoAdsCommon**, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-364">In hello **Reference Manager** dialog box, select **Solution – Projects** in hello left pane, select **ContosoAdsCommon**, and then click **OK**.</span></span>
2. <span data-ttu-id="7b06e-365">In Hallo ingesteld project ContosoAdsWorker een verwijzing toohello Contosoadscommon project.</span><span class="sxs-lookup"><span data-stu-id="7b06e-365">In hello ContosoAdsWorker project, set a reference toohello ContosAdsCommon project.</span></span>

    <span data-ttu-id="7b06e-366">ContosoAdsCommon bevat Hallo Entity Framework data model en in het contextmenu klasse, die wordt gebruikt door beide Hallo front-end en back-end.</span><span class="sxs-lookup"><span data-stu-id="7b06e-366">ContosoAdsCommon will contain hello Entity Framework data model and context class, which will be used by both hello front-end and back-end.</span></span>
3. <span data-ttu-id="7b06e-367">Stel in Hallo project ContosoAdsWorker een verwijzing te`System.Drawing`.</span><span class="sxs-lookup"><span data-stu-id="7b06e-367">In hello ContosoAdsWorker project, set a reference too`System.Drawing`.</span></span>

    <span data-ttu-id="7b06e-368">Deze assembly wordt gebruikt door Hallo back-end tooconvert installatiekopieën toothumbnails.</span><span class="sxs-lookup"><span data-stu-id="7b06e-368">This assembly is used by hello back-end tooconvert images toothumbnails.</span></span>

### <a name="configure-connection-strings"></a><span data-ttu-id="7b06e-369">Verbindingsreeksen configureren</span><span class="sxs-lookup"><span data-stu-id="7b06e-369">Configure connection strings</span></span>
<span data-ttu-id="7b06e-370">In deze sectie configureert u Azure Storage- en SQL-verbindingsreeksen om lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-370">In this section, you configure Azure Storage and SQL connection strings for testing locally.</span></span> <span data-ttu-id="7b06e-371">Hallo implementatie-instructies eerder in Hallo zelfstudie wordt uitgelegd hoe tooset Hallo verbinding tekenreeksen voor wanneer hello app wordt uitgevoerd in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-371">hello deployment instructions earlier in hello tutorial explain how tooset up hello connection strings for when hello app runs in hello cloud.</span></span>

1. <span data-ttu-id="7b06e-372">In Hallo ContosoAdsWeb-project, open Hallo toepassing Web.config-bestand en insert Hallo volgende `connectionStrings` element na Hallo `configSections` element.</span><span class="sxs-lookup"><span data-stu-id="7b06e-372">In hello ContosoAdsWeb project, open hello application Web.config file, and insert hello following `connectionStrings` element after hello `configSections` element.</span></span>

    ```xml
    <connectionStrings>
        <add name="ContosoAdsContext" connectionString="Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;" providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="7b06e-373">Als u Visual Studio 2015 of hoger gebruikt, vervangt u 'v11.0' door 'MSSQLLocalDB'.</span><span class="sxs-lookup"><span data-stu-id="7b06e-373">If you're using Visual Studio 2015 or higher, replace "v11.0" with "MSSQLLocalDB".</span></span>
2. <span data-ttu-id="7b06e-374">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="7b06e-374">Save your changes.</span></span>
3. <span data-ttu-id="7b06e-375">Hallo ContosoAdsCloudService-project met de rechtermuisknop op ContosoAdsWeb onder **rollen**, en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-375">In hello ContosoAdsCloudService project, right-click ContosoAdsWeb under **Roles**, and then click **Properties**.</span></span>

    ![Roleigenschappen](./media/cloud-services-dotnet-get-started/roleproperties.png)
4. <span data-ttu-id="7b06e-377">In Hallo **ContosAdsWeb [rol]** eigenschappenvenster, klikt u op Hallo **instellingen** tabblad en klik vervolgens op **instelling toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-377">In hello **ContosAdsWeb [Role]** properties window, click hello **Settings** tab, and then click **Add Setting**.</span></span>

    <span data-ttu-id="7b06e-378">Laat **serviceconfiguratie** instellen te**alle configuraties**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-378">Leave **Service Configuration** set too**All Configurations**.</span></span>
5. <span data-ttu-id="7b06e-379">Voeg een instelling toe met de naam *StorageConnectionString*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-379">Add a setting named *StorageConnectionString*.</span></span> <span data-ttu-id="7b06e-380">Stel **Type** te*ConnectionString*, en stel **waarde** te*UseDevelopmentStorage = true*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-380">Set **Type** too*ConnectionString*, and set **Value** too*UseDevelopmentStorage=true*.</span></span>

    ![Nieuwe verbindingsreeks](./media/cloud-services-dotnet-get-started/scall.png)
6. <span data-ttu-id="7b06e-382">Sla uw wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="7b06e-382">Save your changes.</span></span>
7. <span data-ttu-id="7b06e-383">Volg Hallo dezelfde procedure tooadd een verbindingsreeks voor opslag in de eigenschappen van Hallo ContosoAdsWorker-rol.</span><span class="sxs-lookup"><span data-stu-id="7b06e-383">Follow hello same procedure tooadd a storage connection string in hello ContosoAdsWorker role properties.</span></span>
8. <span data-ttu-id="7b06e-384">Nog steeds in Hallo **ContosoAdsWorker [rol]** eigenschappenvenster van een andere verbindingsreeks toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7b06e-384">Still in hello **ContosoAdsWorker [Role]** properties window, add another connection string:</span></span>

   * <span data-ttu-id="7b06e-385">Name: ContosoAdsDbConnectionString</span><span class="sxs-lookup"><span data-stu-id="7b06e-385">Name: ContosoAdsDbConnectionString</span></span>
   * <span data-ttu-id="7b06e-386">Type: String</span><span class="sxs-lookup"><span data-stu-id="7b06e-386">Type: String</span></span>
   * <span data-ttu-id="7b06e-387">Waarde: Plakken Hallo dezelfde verbindingsreeks die u voor het webrolproject Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-387">Value: Paste hello same connection string you used for hello web role project.</span></span> <span data-ttu-id="7b06e-388">(Hallo volgende voorbeeld is voor Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="7b06e-388">(hello following example is for Visual Studio 2013.</span></span> <span data-ttu-id="7b06e-389">Vergeet niet toochange Hallo gegevensbron als u dit voorbeeld kopieert en u Visual Studio 2015 of hoger.)</span><span class="sxs-lookup"><span data-stu-id="7b06e-389">Don't forget toochange hello Data Source if you copy this example and you're using Visual Studio 2015 or higher.)</span></span>

       ```
       Data Source=(localdb)\v11.0; Initial Catalog=ContosoAds; Integrated Security=True; MultipleActiveResultSets=True;
       ```

### <a name="add-code-files"></a><span data-ttu-id="7b06e-390">Codebestanden toevoegen</span><span class="sxs-lookup"><span data-stu-id="7b06e-390">Add code files</span></span>
<span data-ttu-id="7b06e-391">In deze sectie kopieert u codebestanden vanuit Hallo gedownloade oplossing naar de nieuwe oplossing Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-391">In this section, you copy code files from hello downloaded solution into hello new solution.</span></span> <span data-ttu-id="7b06e-392">Hallo volgende secties wordt weergeven en belangrijke onderdelen van deze code wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-392">hello following sections will show and explain key parts of this code.</span></span>

<span data-ttu-id="7b06e-393">tooadd bestanden tooa project of een map, klik met de rechtermuisknop Hallo project of map en klikt u op **toevoegen** - **bestaand Item**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-393">tooadd files tooa project or a folder, right-click hello project or folder and click **Add** - **Existing Item**.</span></span> <span data-ttu-id="7b06e-394">Selecteer Hallo bestanden die u wilt en klik vervolgens op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-394">Select hello files you want and then click **Add**.</span></span> <span data-ttu-id="7b06e-395">Als u wordt gevraagd of u wilt dat de bestaande bestanden tooreplace, klikt u op **Ja**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-395">If asked whether you want tooreplace existing files, click **Yes**.</span></span>

1. <span data-ttu-id="7b06e-396">Verwijder in project ContosoAdsCommon Hallo Hallo *Class1.cs* bestand en voeg in de plaats Hallo *Ad.cs* en *ContosoAdscontext.cs* bestanden van Hallo project gedownload.</span><span class="sxs-lookup"><span data-stu-id="7b06e-396">In hello ContosoAdsCommon project, delete hello *Class1.cs* file and add in its place hello *Ad.cs* and *ContosoAdscontext.cs* files from hello downloaded project.</span></span>
2. <span data-ttu-id="7b06e-397">In het project ContosoAdsWeb Hallo toevoegen Hallo volgende bestanden uit Hallo gedownload project.</span><span class="sxs-lookup"><span data-stu-id="7b06e-397">In hello ContosoAdsWeb project, add hello following files from hello downloaded project.</span></span>

   * <span data-ttu-id="7b06e-398">*Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-398">*Global.asax.cs*.</span></span>  
   * <span data-ttu-id="7b06e-399">In Hallo *Views\Shared* map:  *\_Layout.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-399">In hello *Views\Shared* folder: *\_Layout.cshtml*.</span></span>
   * <span data-ttu-id="7b06e-400">In Hallo *Views\Home* map: *Index.cshtml*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-400">In hello *Views\Home* folder: *Index.cshtml*.</span></span>
   * <span data-ttu-id="7b06e-401">In Hallo *domeincontrollers* map: *AdController.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-401">In hello *Controllers* folder: *AdController.cs*.</span></span>
   * <span data-ttu-id="7b06e-402">In Hallo *Views\Ad* map (Maak eerst Hallo map): vijf *.cshtml* bestanden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-402">In hello *Views\Ad* folder (create hello folder first): five *.cshtml* files.</span></span>
3. <span data-ttu-id="7b06e-403">Voeg in het project ContosoAdsWorker hello *WorkerRole.cs* Hallo project gedownload.</span><span class="sxs-lookup"><span data-stu-id="7b06e-403">In hello ContosoAdsWorker project, add *WorkerRole.cs* from hello downloaded project.</span></span>

<span data-ttu-id="7b06e-404">U kunt nu toepassing bouwen en uitvoeren Hallo volgens de instructies eerder in de zelfstudie Hallo en Hallo app gebruikt lokale database- en opslagemulatorresources.</span><span class="sxs-lookup"><span data-stu-id="7b06e-404">You can now build and run hello application as instructed earlier in hello tutorial, and hello app will use local database and storage emulator resources.</span></span>

<span data-ttu-id="7b06e-405">Hallo volgende secties wordt uitgelegd Hallo code gerelateerde tooworking met hello Azure-omgeving, blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-405">hello following sections explain hello code related tooworking with hello Azure environment, blobs, and queues.</span></span> <span data-ttu-id="7b06e-406">Deze zelfstudie wordt niet uitgelegd hoe toocreate MVC-controllers en weergaven met behulp van steigers, hoe toowrite code voor Entity Framework die werkt met SQL Server-databases of Hallo basisbeginselen van asynchrone programmering in ASP.NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="7b06e-406">This tutorial does not explain how toocreate MVC controllers and views using scaffolding, how toowrite Entity Framework code that works with SQL Server databases, or hello basics of asynchronous programming in ASP.NET 4.5.</span></span> <span data-ttu-id="7b06e-407">Zie voor informatie over deze onderwerpen Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b06e-407">For information about these topics, see hello following resources:</span></span>

* [<span data-ttu-id="7b06e-408">Aan de slag met MVC 5</span><span class="sxs-lookup"><span data-stu-id="7b06e-408">Get started with MVC 5</span></span>](http://www.asp.net/mvc/tutorials/mvc-5/introduction/getting-started)
* [<span data-ttu-id="7b06e-409">Aan de slag met EF 6 en MVC 5</span><span class="sxs-lookup"><span data-stu-id="7b06e-409">Get started with EF 6 and MVC 5</span></span>](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc)
* <span data-ttu-id="7b06e-410">[Inleiding tooasynchronous programmering in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span><span class="sxs-lookup"><span data-stu-id="7b06e-410">[Introduction tooasynchronous programming in .NET 4.5](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices#async).</span></span>

### <a name="contosoadscommon---adcs"></a><span data-ttu-id="7b06e-411">ContosoAdsCommon - Ad.cs</span><span class="sxs-lookup"><span data-stu-id="7b06e-411">ContosoAdsCommon - Ad.cs</span></span>
<span data-ttu-id="7b06e-412">bestand van Hallo Ad.cs definieert een enum voor advertentiecategorieën en een POCO-entiteitsklasse voor advertentie-informatie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-412">hello Ad.cs file defines an enum for ad categories and a POCO entity class for ad information.</span></span>

```csharp
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
```

### <a name="contosoadscommon---contosoadscontextcs"></a><span data-ttu-id="7b06e-413">ContosoAdsCommon - ContosoAdsContext.cs</span><span class="sxs-lookup"><span data-stu-id="7b06e-413">ContosoAdsCommon - ContosoAdsContext.cs</span></span>
<span data-ttu-id="7b06e-414">Hallo klasse contosoadscontext geeft aan dat Hallo Ad-klasse wordt gebruikt in een DbSet-verzameling Entity Framework wordt opgeslagen in een SQL-database.</span><span class="sxs-lookup"><span data-stu-id="7b06e-414">hello ContosoAdsContext class specifies that hello Ad class is used in a DbSet collection, which Entity Framework will store in a SQL database.</span></span>

```csharp
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
```

<span data-ttu-id="7b06e-415">Hallo-klasse heeft twee constructors.</span><span class="sxs-lookup"><span data-stu-id="7b06e-415">hello class has two constructors.</span></span> <span data-ttu-id="7b06e-416">Hallo eerst hiervan wordt gebruikt door het webproject Hallo en geeft Hallo-naam van een verbindingsreeks die is opgeslagen in Hallo Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="7b06e-416">hello first of them is used by hello web project, and specifies hello name of a connection string that is stored in hello Web.config file.</span></span> <span data-ttu-id="7b06e-417">Hallo tweede constructor kunt u toopass in Hallo werkelijke verbindingsreeks die wordt gebruikt door Hallo werkrolproject, omdat het geen een Web.config-bestand.</span><span class="sxs-lookup"><span data-stu-id="7b06e-417">hello second constructor enables you toopass in hello actual connection string used by hello worker role project, since it doesn't have a Web.config file.</span></span> <span data-ttu-id="7b06e-418">U eerder hebt gezien waar deze verbindingsreeks is opgeslagen en ziet u hoe Hallo-code Hallo verbindingsreeks ophaalt bij het instantiëren van Hallo DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="7b06e-418">You saw earlier where this connection string was stored, and you'll see later how hello code retrieves hello connection string when it instantiates hello DbContext class.</span></span>

### <a name="contosoadsweb---globalasaxcs"></a><span data-ttu-id="7b06e-419">ContosoAdsWeb - Global.asax.cs</span><span class="sxs-lookup"><span data-stu-id="7b06e-419">ContosoAdsWeb - Global.asax.cs</span></span>
<span data-ttu-id="7b06e-420">Code die wordt aangeroepen vanuit Hallo `Application_Start` methode maakt u een *installatiekopieën* blob-container en een *installatiekopieën* als ze nog niet bestaan in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7b06e-420">Code that is called from hello `Application_Start` method creates an *images* blob container and an *images* queue if they don't already exist.</span></span> <span data-ttu-id="7b06e-421">Dit zorgt ervoor dat wanneer u begint met behulp van een nieuw opslagaccount, of met behulp van de opslagemulator Hallo op een nieuwe computer, Hallo vereiste blobcontainer en wachtrij wordt automatisch gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-421">This ensures that whenever you start using a new storage account, or start using hello storage emulator on a new computer, hello required blob container and queue will be created automatically.</span></span>

<span data-ttu-id="7b06e-422">code haalt toegang toohello storage-account met behulp van de opslagverbindingsreeks uit Hallo HALLO hallo *.cscfg* bestand.</span><span class="sxs-lookup"><span data-stu-id="7b06e-422">hello code gets access toohello storage account by using hello storage connection string from hello *.cscfg* file.</span></span>

```csharp
var storageAccount = CloudStorageAccount.Parse
    (RoleEnvironment.GetConfigurationSettingValue("StorageConnectionString"));
```

<span data-ttu-id="7b06e-423">Vervolgens haalt de code een verwijzing toohello *installatiekopieën* blob-container, Hallo container maakt als deze niet al bestaat en stelt deze voor de nieuwe container Hallo toegangsrechten.</span><span class="sxs-lookup"><span data-stu-id="7b06e-423">Then it gets a reference toohello *images* blob container, creates hello container if it doesn't already exist, and sets access permissions on hello new container.</span></span> <span data-ttu-id="7b06e-424">Standaard staan nieuwe containers alleen clients met storage-account referenties tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="7b06e-424">By default, new containers only allow clients with storage account credentials tooaccess blobs.</span></span> <span data-ttu-id="7b06e-425">Hallo-website moet blobs toobe openbare Hallo zodat deze afbeeldingen met URL's die punt toohello afbeeldingsblobs wijzen kan weergeven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-425">hello website needs hello blobs toobe public so that it can display images using URLs that point toohello image blobs.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
var imagesBlobContainer = blobClient.GetContainerReference("images");
if (imagesBlobContainer.CreateIfNotExists())
{
    imagesBlobContainer.SetPermissions(
        new BlobContainerPermissions
        {
            PublicAccess =BlobContainerPublicAccessType.Blob
        });
}
```

<span data-ttu-id="7b06e-426">Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij en een nieuwe wachtrij gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7b06e-426">Similar code gets a reference toohello *images* queue and creates a new queue.</span></span> <span data-ttu-id="7b06e-427">In dit geval is er geen machtigingswijziging nodig.</span><span class="sxs-lookup"><span data-stu-id="7b06e-427">In this case, no permissions change is needed.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
var imagesQueue = queueClient.GetQueueReference("images");
imagesQueue.CreateIfNotExists();
```

### <a name="contosoadsweb---layoutcshtml"></a><span data-ttu-id="7b06e-428">ContosoAdsWeb - \_Layout.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b06e-428">ContosoAdsWeb - \_Layout.cshtml</span></span>
<span data-ttu-id="7b06e-429">Hallo *_Layout.cshtml* bestand Hallo app-naam stelt in Hallo koptekst en voettekst en maakt een menu-item 'Ads'.</span><span class="sxs-lookup"><span data-stu-id="7b06e-429">hello *_Layout.cshtml* file sets hello app name in hello header and footer, and creates an "Ads" menu entry.</span></span>

### <a name="contosoadsweb---viewshomeindexcshtml"></a><span data-ttu-id="7b06e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b06e-430">ContosoAdsWeb - Views\Home\Index.cshtml</span></span>
<span data-ttu-id="7b06e-431">Hallo *Views\Home\Index.cshtml* bestand geeft categoriekoppelingen weer op Hallo-startpagina.</span><span class="sxs-lookup"><span data-stu-id="7b06e-431">hello *Views\Home\Index.cshtml* file displays category links on hello home page.</span></span> <span data-ttu-id="7b06e-432">Hallo-koppelingen geven de integerwaarde Hallo Hallo `Category` enum in een pagina querystring variabele toohello Ads Index.</span><span class="sxs-lookup"><span data-stu-id="7b06e-432">hello links pass hello integer value of hello `Category` enum in a querystring variable toohello Ads Index page.</span></span>

```razor
<li>@Html.ActionLink("Cars", "Index", "Ad", new { category = (int)Category.Cars }, null)</li>
<li>@Html.ActionLink("Real estate", "Index", "Ad", new { category = (int)Category.RealEstate }, null)</li>
<li>@Html.ActionLink("Free stuff", "Index", "Ad", new { category = (int)Category.FreeStuff }, null)</li>
<li>@Html.ActionLink("All", "Index", "Ad", null, null)</li>
```

### <a name="contosoadsweb---adcontrollercs"></a><span data-ttu-id="7b06e-433">ContosoAdsWeb - AdController.cs</span><span class="sxs-lookup"><span data-stu-id="7b06e-433">ContosoAdsWeb - AdController.cs</span></span>
<span data-ttu-id="7b06e-434">In Hallo *AdController.cs* bestand, Hallo constructor aanroepen Hallo `InitializeStorage` methode toocreate Azure Storage-clientbibliotheek objecten die een API leveren voor het werken met blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-434">In hello *AdController.cs* file, hello constructor calls hello `InitializeStorage` method toocreate Azure Storage Client Library objects that provide an API for working with blobs and queues.</span></span>

<span data-ttu-id="7b06e-435">Vervolgens Hallo code een verwijzing toohello wordt *installatiekopieën* blobcontainer, zoals u eerder in gezien *Global.asax.cs*.</span><span class="sxs-lookup"><span data-stu-id="7b06e-435">Then hello code gets a reference toohello *images* blob container as you saw earlier in *Global.asax.cs*.</span></span> <span data-ttu-id="7b06e-436">Tijdens het uitvoeren hiervan wordt standaard [beleid voor opnieuw proberen](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) ingesteld dat geschikt is voor een web-app.</span><span class="sxs-lookup"><span data-stu-id="7b06e-436">While doing that it sets a default [retry policy](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/transient-fault-handling) appropriate for a web app.</span></span> <span data-ttu-id="7b06e-437">Hallo standaard exponentieel uitstel-beleid voor opnieuw proberen kan vastlopen Hallo web-app langer dan een minuut herhaalde pogingen voor een tijdelijke fout.</span><span class="sxs-lookup"><span data-stu-id="7b06e-437">hello default exponential backoff retry policy could hang hello web app for longer than a minute on repeated retries for a transient fault.</span></span> <span data-ttu-id="7b06e-438">beleid voor opnieuw proberen Hallo hier opgegeven wacht drie seconden na elke poging up toothree pogingen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-438">hello retry policy specified here waits three seconds after each try for up toothree tries.</span></span>

```csharp
var blobClient = storageAccount.CreateCloudBlobClient();
blobClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesBlobContainer = blobClient.GetContainerReference("images");
```

<span data-ttu-id="7b06e-439">Vergelijkbare code wordt een verwijzing toohello *installatiekopieën* wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7b06e-439">Similar code gets a reference toohello *images* queue.</span></span>

```csharp
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();
queueClient.DefaultRequestOptions.RetryPolicy = new LinearRetry(TimeSpan.FromSeconds(3), 3);
imagesQueue = queueClient.GetQueueReference("images");
```

<span data-ttu-id="7b06e-440">De meeste Hallo controllercode is Typerend voor het werken met een Entity Framework-gegevensmodel met behulp van een DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="7b06e-440">Most of hello controller code is typical for working with an Entity Framework data model using a DbContext class.</span></span> <span data-ttu-id="7b06e-441">Een uitzondering is Hallo HttpPost `Create` methode, waarmee een bestand wordt geüpload en opgeslagen in blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="7b06e-441">An exception is hello HttpPost `Create` method, which uploads a file and saves it in blob storage.</span></span> <span data-ttu-id="7b06e-442">Hallo modelbinder levert een [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) toohello methode-object.</span><span class="sxs-lookup"><span data-stu-id="7b06e-442">hello model binder provides an [HttpPostedFileBase](http://msdn.microsoft.com/library/system.web.httppostedfilebase.aspx) object toohello method.</span></span>

```csharp
[HttpPost]
[ValidateAntiForgeryToken]
public async Task<ActionResult> Create(
    [Bind(Include = "Title,Price,Description,Category,Phone")] Ad ad,
    HttpPostedFileBase imageFile)
```

<span data-ttu-id="7b06e-443">Hallo gebruiker geselecteerd een bestand tooupload, Hallo code Hallo-bestand wordt geüpload, opgeslagen in een blob als Hallo Ad-databaserecord bijgewerkt met een URL die toohello blob verwijst.</span><span class="sxs-lookup"><span data-stu-id="7b06e-443">If hello user selected a file tooupload, hello code uploads hello file, saves it in a blob, and updates hello Ad database record with a URL that points toohello blob.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    blob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = blob.Uri.ToString();
}
```

<span data-ttu-id="7b06e-444">Hallo-code die uploaden Hallo heeft Hallo `UploadAndSaveBlobAsync` methode.</span><span class="sxs-lookup"><span data-stu-id="7b06e-444">hello code that does hello upload is in hello `UploadAndSaveBlobAsync` method.</span></span> <span data-ttu-id="7b06e-445">Deze maakt een GUID-naam voor Hallo blob, uploads en slaat Hallo-bestand en retourneert een verwijzing toohello opgeslagen blob.</span><span class="sxs-lookup"><span data-stu-id="7b06e-445">It creates a GUID name for hello blob, uploads and saves hello file, and returns a reference toohello saved blob.</span></span>

```csharp
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
```

<span data-ttu-id="7b06e-446">Na het Hallo HttpPost `Create` methode een blob uploadt en updates Hallo database, het maken van een wachtrij bericht tooinform dat back-end-proces dat een afbeelding gereed voor conversie tooa miniatuur is.</span><span class="sxs-lookup"><span data-stu-id="7b06e-446">After hello HttpPost `Create` method uploads a blob and updates hello database, it creates a queue message tooinform that back-end process that an image is ready for conversion tooa thumbnail.</span></span>

```csharp
string queueMessageString = ad.AdId.ToString();
var queueMessage = new CloudQueueMessage(queueMessageString);
await queue.AddMessageAsync(queueMessage);
```

<span data-ttu-id="7b06e-447">code voor Hallo HttpPost Hallo `Edit` methode is vergelijkbaar met dit verschil dat als Hallo gebruiker een nieuw afbeeldingsbestand selecteert alle blobs die al bestaan moeten worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-447">hello code for hello HttpPost `Edit` method is similar except that if hello user selects a new image file any blobs that already exist must be deleted.</span></span>

```csharp
if (imageFile != null && imageFile.ContentLength != 0)
{
    await DeleteAdBlobsAsync(ad);
    imageBlob = await UploadAndSaveBlobAsync(imageFile);
    ad.ImageURL = imageBlob.Uri.ToString();
}
```

<span data-ttu-id="7b06e-448">Hallo volgende voorbeeld ziet u Hallo-code die verwijderen van blobs wanneer u een advertentie verwijdert.</span><span class="sxs-lookup"><span data-stu-id="7b06e-448">hello next example shows hello code that deletes blobs when you delete an ad.</span></span>

```csharp
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
```

### <a name="contosoadsweb---viewsadindexcshtml-and-detailscshtml"></a><span data-ttu-id="7b06e-449">ContosoAdsWeb - Views\Ad\Index.cshtml en Details.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b06e-449">ContosoAdsWeb - Views\Ad\Index.cshtml and Details.cshtml</span></span>
<span data-ttu-id="7b06e-450">Hallo *Index.cshtml* bestand bevat miniaturen Hello andere ad-gegevens.</span><span class="sxs-lookup"><span data-stu-id="7b06e-450">hello *Index.cshtml* file displays thumbnails with hello other ad data.</span></span>

```razor
<img src="@Html.Raw(item.ThumbnailURL)" />
```

<span data-ttu-id="7b06e-451">Hallo *Details.cshtml* bestand Hallo-afbeelding wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-451">hello *Details.cshtml* file displays hello full-size image.</span></span>

```razor
<img src="@Html.Raw(Model.ImageURL)" />
```

### <a name="contosoadsweb---viewsadcreatecshtml-and-editcshtml"></a><span data-ttu-id="7b06e-452">ContosoAdsWeb - Views\Ad\Create.cshtml en Edit.cshtml</span><span class="sxs-lookup"><span data-stu-id="7b06e-452">ContosoAdsWeb - Views\Ad\Create.cshtml and Edit.cshtml</span></span>
<span data-ttu-id="7b06e-453">Hallo *Create.cshtml* en *Edit.cshtml* bestanden formulier dat Hiermee controller tooget Hallo Hallo codering opgeven `HttpPostedFileBase` object.</span><span class="sxs-lookup"><span data-stu-id="7b06e-453">hello *Create.cshtml* and *Edit.cshtml* files specify form encoding that enables hello controller tooget hello `HttpPostedFileBase` object.</span></span>

```razor
@using (Html.BeginForm("Create", "Ad", FormMethod.Post, new { enctype = "multipart/form-data" }))
```

<span data-ttu-id="7b06e-454">Een `<input>` element vertelt Hallo browser tooprovide een dialoogvenster voor bestandsselectie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-454">An `<input>` element tells hello browser tooprovide a file selection dialog.</span></span>

```razor
<input type="file" name="imageFile" accept="image/*" class="form-control fileupload" />
```

### <a name="contosoadsworker---workerrolecs---onstart-method"></a><span data-ttu-id="7b06e-455">ContosoAdsWorker - WorkerRole.cs - OnStart-methode</span><span class="sxs-lookup"><span data-stu-id="7b06e-455">ContosoAdsWorker - WorkerRole.cs - OnStart method</span></span>
<span data-ttu-id="7b06e-456">Hello Azure worker-rol omgeving roept Hallo `OnStart` methode in Hallo `WorkerRole` klasse wanneer Hallo werkrol begint en Hallo roept `Run` methode wanneer hello `OnStart` methode is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7b06e-456">hello Azure worker role environment calls hello `OnStart` method in hello `WorkerRole` class when hello worker role is getting started, and it calls hello `Run` method when hello `OnStart` method finishes.</span></span>

<span data-ttu-id="7b06e-457">Hallo `OnStart` methode haalt de databaseverbindingsreeks Hallo uit Hallo *.cscfg* bestands- en geeft deze door toohello Entity Framework DbContext-klasse.</span><span class="sxs-lookup"><span data-stu-id="7b06e-457">hello `OnStart` method gets hello database connection string from hello *.cscfg* file and passes it toohello Entity Framework DbContext class.</span></span> <span data-ttu-id="7b06e-458">Hallo SQLClient-provider wordt standaard gebruikt, zodat het Hallo-provider heeft geen toobe opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-458">hello SQLClient provider is used by default, so hello provider does not have toobe specified.</span></span>

```csharp
var dbConnString = CloudConfigurationManager.GetSetting("ContosoAdsDbConnectionString");
db = new ContosoAdsContext(dbConnString);
```

<span data-ttu-id="7b06e-459">Hierna is Hallo-methode een verwijzing toohello storage-account opgehaald en Hallo blobcontainer en wachtrij wordt gemaakt als deze nog niet bestaan.</span><span class="sxs-lookup"><span data-stu-id="7b06e-459">After that, hello method gets a reference toohello storage account and creates hello blob container and queue if they don't exist.</span></span> <span data-ttu-id="7b06e-460">Hallo code hiervoor is vergelijkbaar toowhat u al hebt gezien in de Webrol Hallo `Application_Start` methode.</span><span class="sxs-lookup"><span data-stu-id="7b06e-460">hello code for that is similar toowhat you already saw in hello web role `Application_Start` method.</span></span>

### <a name="contosoadsworker---workerrolecs---run-method"></a><span data-ttu-id="7b06e-461">ContosoAdsWorker - WorkerRole.cs - Run-methode</span><span class="sxs-lookup"><span data-stu-id="7b06e-461">ContosoAdsWorker - WorkerRole.cs - Run method</span></span>
<span data-ttu-id="7b06e-462">Hallo `Run` methode wordt aangeroepen wanneer hello `OnStart` methode een initialisatiewerk.</span><span class="sxs-lookup"><span data-stu-id="7b06e-462">hello `Run` method is called when hello `OnStart` method finishes its initialization work.</span></span> <span data-ttu-id="7b06e-463">Hallo-methode voert een oneindige lus die controleert op nieuwe Wachtrijberichten en verwerkt deze wanneer ze binnenkomen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-463">hello method executes an infinite loop that watches for new queue messages and processes them when they arrive.</span></span>

```csharp
public override void Run()
{
    CloudQueueMessage msg = null;

    while (true)
    {
        try
        {
            msg = this.imagesQueue.GetMessage();
            if (msg != null)
            {
                ProcessQueueMessage(msg);
            }
            else
            {
                System.Threading.Thread.Sleep(1000);
            }
        }
        catch (StorageException e)
        {
            if (msg != null && msg.DequeueCount > 5)
            {
                this.imagesQueue.DeleteMessage(msg);
            }
            System.Threading.Thread.Sleep(5000);
        }
    }
}
```

<span data-ttu-id="7b06e-464">Na elke herhaling van de lus hello, als er geen wachtrijbericht is gevonden, Hallo inactieve modus ingeschakeld gedurende een seconde.</span><span class="sxs-lookup"><span data-stu-id="7b06e-464">After each iteration of hello loop, if no queue message was found, hello program sleeps for a second.</span></span> <span data-ttu-id="7b06e-465">Dit voorkomt dat Hallo werkrol buitensporig CPU tijd en opslag transactiekosten aangaan.</span><span class="sxs-lookup"><span data-stu-id="7b06e-465">This prevents hello worker role from incurring excessive CPU time and storage transaction costs.</span></span> <span data-ttu-id="7b06e-466">Hallo Microsoft Customer Advisory Team kent het verhaal van een ontwikkelaar die tooinclude dit vergeten tooproduction geïmplementeerd en op vakantie ging.</span><span class="sxs-lookup"><span data-stu-id="7b06e-466">hello Microsoft Customer Advisory Team tells a story about a  developer who forgot tooinclude this, deployed tooproduction, and left for vacation.</span></span> <span data-ttu-id="7b06e-467">Wanneer hij zich ook, duurder zijn toezicht dan Hallo vakantie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-467">When he got back, his oversight cost more than hello vacation.</span></span>

<span data-ttu-id="7b06e-468">Soms veroorzaakt Hallo inhoud van een wachtrijbericht een fout bij de verwerking.</span><span class="sxs-lookup"><span data-stu-id="7b06e-468">Sometimes hello content of a queue message causes an error in processing.</span></span> <span data-ttu-id="7b06e-469">Dit wordt genoemd, een *verontreinigd bericht*, en als u alleen een fout opgetreden in het logboek geregistreerd en Hallo lus opnieuw opgestart, kan dit leiden tot eindeloze probeert tooprocess bericht.</span><span class="sxs-lookup"><span data-stu-id="7b06e-469">This is called a *poison message*, and if you just logged an error and restarted hello loop, you could endlessly try tooprocess that message.</span></span>  <span data-ttu-id="7b06e-470">Daarom Hallo catch-blok een if bevat instructie waarmee wordt gecontroleerd toosee hoe vaak Hallo app heeft geprobeerd tooprocess Hallo huidige bericht, en als het al meer dan 5 maal, het Hallo-bericht is verwijderd uit Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7b06e-470">Therefore hello catch block includes an if statement that checks toosee how many times hello app has tried tooprocess hello current message, and if it has been more than 5 times, hello message is deleted from hello queue.</span></span>

<span data-ttu-id="7b06e-471">`ProcessQueueMessage` wordt aangeroepen wanneer er een wachtrijbericht is gevonden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-471">`ProcessQueueMessage` is called when a queue message is found.</span></span>

```csharp
private void ProcessQueueMessage(CloudQueueMessage msg)
{
    var adId = int.Parse(msg.AsString);
    Ad ad = db.Ads.Find(adId);
    if (ad == null)
    {
        throw new Exception(String.Format("AdId {0} not found, can't create thumbnail", adId.ToString()));
    }

    CloudBlockBlob inputBlob = this.imagesBlobContainer.GetBlockBlobReference(ad.ImageURL);

    string thumbnailName = Path.GetFileNameWithoutExtension(inputBlob.Name) + "thumb.jpg";
    CloudBlockBlob outputBlob = this.imagesBlobContainer.GetBlockBlobReference(thumbnailName);

    using (Stream input = inputBlob.OpenRead())
    using (Stream output = outputBlob.OpenWrite())
    {
        ConvertImageToThumbnailJPG(input, output);
        outputBlob.Properties.ContentType = "image/jpeg";
    }

    ad.ThumbnailURL = outputBlob.Uri.ToString();
    db.SaveChanges();

    this.imagesQueue.DeleteMessage(msg);
}
```

<span data-ttu-id="7b06e-472">Deze code leest Hallo database tooget Hallo afbeeldings-URL, converteert de miniatuur tooa Hallo Hallo miniatuur opgeslagen in een blob, werkt Hallo-database met Hallo miniaturen blob-URL en Hallo-bericht van wachtrij worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7b06e-472">This code reads hello database tooget hello image URL, converts hello image tooa thumbnail, saves hello thumbnail in a blob, updates hello database with hello thumbnail blob URL, and deletes hello queue message.</span></span>

> [!NOTE]
> <span data-ttu-id="7b06e-473">Hallo-code in Hallo `ConvertImageToThumbnailJPG` methode gebruik van klassen in Hallo System.Drawing-naamruimte voor de eenvoud.</span><span class="sxs-lookup"><span data-stu-id="7b06e-473">hello code in hello `ConvertImageToThumbnailJPG` method uses classes in hello System.Drawing namespace for simplicity.</span></span> <span data-ttu-id="7b06e-474">Hallo-klassen in deze naamruimte zijn echter bedoeld voor gebruik met Windows Forms.</span><span class="sxs-lookup"><span data-stu-id="7b06e-474">However, hello classes in this namespace were designed for use with Windows Forms.</span></span> <span data-ttu-id="7b06e-475">Ze worden niet ondersteund voor gebruik in een Windows- of ASP.NET-service.</span><span class="sxs-lookup"><span data-stu-id="7b06e-475">They are not supported for use in a Windows or ASP.NET service.</span></span> <span data-ttu-id="7b06e-476">Zie [Afbeeldingen dynamisch genereren](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) en [Alles over het wijzigen van het formaat van afbeeldingen](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na) voor meer informatie over opties voor de verwerking van afbeeldingen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-476">For more information about image-processing options, see [Dynamic Image Generation](http://www.hanselman.com/blog/BackToBasicsDynamicImageGenerationASPNETControllersRoutingIHttpHandlersAndRunAllManagedModulesForAllRequests.aspx) and [Deep Inside Image Resizing](http://www.hanselminutes.com/313/deep-inside-image-resizing-and-scaling-with-aspnet-and-iis-with-imageresizingnet-author-na).</span></span>
>
>

## <a name="troubleshooting"></a><span data-ttu-id="7b06e-477">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7b06e-477">Troubleshooting</span></span>
<span data-ttu-id="7b06e-478">Als er iets niet werkt terwijl u Hallo-instructies in deze zelfstudie, Hier volgen een aantal veelvoorkomende fouten en hoe tooresolve ze.</span><span class="sxs-lookup"><span data-stu-id="7b06e-478">In case something doesn't work while you're following hello instructions in this tutorial, here are some common errors and how tooresolve them.</span></span>

### <a name="serviceruntimeroleenvironmentexception"></a><span data-ttu-id="7b06e-479">ServiceRuntime.RoleEnvironmentException</span><span class="sxs-lookup"><span data-stu-id="7b06e-479">ServiceRuntime.RoleEnvironmentException</span></span>
<span data-ttu-id="7b06e-480">Hallo `RoleEnvironment` object wordt verstrekt door Azure wanneer u een toepassing in Azure uitvoert of bij het uitvoeren van een lokaal via hello Azure-rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="7b06e-480">hello `RoleEnvironment` object is provided by Azure when you run an application in Azure or when you run locally using hello Azure compute emulator.</span></span>  <span data-ttu-id="7b06e-481">Als u deze fout krijgt wanneer u lokaal uitvoert, zorg ervoor dat u Hallo ContosoAdsCloudService-project als opstartproject Hallo hebt ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7b06e-481">If you get this error when you're running locally, make sure that you have set hello ContosoAdsCloudService project as hello startup project.</span></span> <span data-ttu-id="7b06e-482">Hiermee stelt u Hallo project toorun met hello Azure-rekenemulator.</span><span class="sxs-lookup"><span data-stu-id="7b06e-482">This sets up hello project toorun using hello Azure compute emulator.</span></span>

<span data-ttu-id="7b06e-483">Hallo-bewerkingen Hallo toepassing gebruikt hello Azure RoleEnvironment voor tooget Hallo waarden van verbindingsreeksen die zijn opgeslagen in Hallo is *.cscfg* bestanden, zodat een andere oorzaak van deze uitzondering een ontbrekende verbindingsreeks is.</span><span class="sxs-lookup"><span data-stu-id="7b06e-483">One of hello things hello application uses hello Azure RoleEnvironment for is tooget hello connection string values that are stored in hello *.cscfg* files, so another cause of this exception is a missing connection string.</span></span> <span data-ttu-id="7b06e-484">Zorg ervoor dat u Hallo StorageConnectionString instelling voor zowel Cloud- en lokale configuraties in Hallo ContosoAdsWeb-project gemaakt en dat u beide verbindingsreeksen voor beide configuraties hebt gemaakt in de project ContosoAdsWorker Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-484">Make sure that you created hello StorageConnectionString setting for both Cloud and Local configurations in hello ContosoAdsWeb project, and that you created both connection strings for both configurations in hello ContosoAdsWorker project.</span></span> <span data-ttu-id="7b06e-485">Als u een **Alles zoeken** zoeken voor StorageConnectionString in de hele oplossing hello, ziet u het 9 maal in 6 bestanden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-485">If you do a **Find All** search for StorageConnectionString in hello entire solution, you should see it 9 times in 6 files.</span></span>

### <a name="cannot-override-tooport-xxx-new-port-below-minimum-allowed-value-8080-for-protocol-http"></a><span data-ttu-id="7b06e-486">Kan de tooport xxx niet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="7b06e-486">Cannot override tooport xxx.</span></span> <span data-ttu-id="7b06e-487">Nieuwe poort onder minimaal toegestane waarde 8080 voor http-protocol</span><span class="sxs-lookup"><span data-stu-id="7b06e-487">New port below minimum allowed value 8080 for protocol http</span></span>
<span data-ttu-id="7b06e-488">Wijzig Hallo poortnummer dat wordt gebruikt door het webproject Hallo.</span><span class="sxs-lookup"><span data-stu-id="7b06e-488">Try changing hello port number used by hello web project.</span></span> <span data-ttu-id="7b06e-489">Met de rechtermuisknop op Hallo ContosoAdsWeb-project en klik vervolgens op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-489">Right-click hello ContosoAdsWeb project, and then click **Properties**.</span></span> <span data-ttu-id="7b06e-490">Klik op Hallo **Web** tabblad en wijzig vervolgens de Hallo poortnummer in Hallo **Project Url** instelling.</span><span class="sxs-lookup"><span data-stu-id="7b06e-490">Click hello **Web** tab, and then change hello port number in hello **Project Url** setting.</span></span>

<span data-ttu-id="7b06e-491">Zie voor een alternatieve Hallo probleem kan mogelijk worden opgelost, Hallo volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="7b06e-491">For another alternative that might resolve hello problem, see hello following  section.</span></span>

### <a name="other-errors-when-running-locally"></a><span data-ttu-id="7b06e-492">Andere fouten bij lokale uitvoering</span><span class="sxs-lookup"><span data-stu-id="7b06e-492">Other errors when running locally</span></span>
<span data-ttu-id="7b06e-493">Cloudserviceprojecten gebruik door nieuwe cloud standaard hello Azure compute-emulator snelle toosimulate hello Azure-omgeving.</span><span class="sxs-lookup"><span data-stu-id="7b06e-493">By default new cloud service projects use hello Azure compute emulator express toosimulate hello Azure environment.</span></span> <span data-ttu-id="7b06e-494">Dit is een lichtgewicht versie van de volledige rekenemulator hello en onder bepaalde omstandigheden Hallo volledige emulator werkt wanneer Hallo express-versie niet.</span><span class="sxs-lookup"><span data-stu-id="7b06e-494">This is a lightweight version of hello full compute emulator, and under some conditions hello full emulator will work when hello express version does not.</span></span>  

<span data-ttu-id="7b06e-495">toochange Hallo project toouse Hallo volledige emulator, met de rechtermuisknop op Hallo ContosoAdsCloudService-project en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7b06e-495">toochange hello project toouse hello full emulator, right-click hello ContosoAdsCloudService project, and then click **Properties**.</span></span> <span data-ttu-id="7b06e-496">In Hallo **eigenschappen** venster klikt u op Hallo **Web** tabblad en klik vervolgens op Hallo **Use Full Emulator** keuzerondje.</span><span class="sxs-lookup"><span data-stu-id="7b06e-496">In hello **Properties** window click hello **Web** tab, and then click hello **Use Full Emulator** radio button.</span></span>

<span data-ttu-id="7b06e-497">In de volgorde toorun Hallo toepassing met de volledige emulator hello hebt u tooopen Visual Studio met administratorbevoegdheden.</span><span class="sxs-lookup"><span data-stu-id="7b06e-497">In order toorun hello application with hello full emulator, you have tooopen Visual Studio with administrator privileges.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b06e-498">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7b06e-498">Next steps</span></span>
<span data-ttu-id="7b06e-499">Hallo Contoso Ads-toepassing is opzettelijk is eenvoudig gehouden voor een zelfstudie aan de slag.</span><span class="sxs-lookup"><span data-stu-id="7b06e-499">hello Contoso Ads application has intentionally been kept simple for a getting-started tutorial.</span></span> <span data-ttu-id="7b06e-500">Bijvoorbeeld, implementeert niet [afhankelijkheidsinjectie](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) of Hallo [opslagplaatsen en werkeenheden](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), dat niet het geval [gebruik van een interface voor logboekregistratie](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), nietwordtgebruikt[ EF Code First-migraties](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage gegevensmodel wijzigingen of [EF-Verbindingstolerantie](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage tijdelijke netwerkfouten, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="7b06e-500">For example, it doesn't implement [dependency injection](http://www.asp.net/mvc/tutorials/hands-on-labs/aspnet-mvc-4-dependency-injection) or hello [repository and unit of work patterns](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application#repo), it doesn't [use an interface for logging](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry#log), it doesn't use [EF Code First Migrations](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage data model changes or [EF Connection Resiliency](http://www.asp.net/mvc/tutorials/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application) toomanage transient network errors, and so forth.</span></span>

<span data-ttu-id="7b06e-501">Hier volgen enkele cloud service-voorbeeldtoepassingen waarin meer echte code te bevorderen, van cloudservicetoepassingen toomore complexe vermeld:</span><span class="sxs-lookup"><span data-stu-id="7b06e-501">Here are some cloud service sample applications that demonstrate more real-world coding practices, listed from less complex toomore complex:</span></span>

* <span data-ttu-id="7b06e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span><span class="sxs-lookup"><span data-stu-id="7b06e-502">[PhluffyFotos](http://code.msdn.microsoft.com/PhluffyFotos-Sample-7ecffd31).</span></span> <span data-ttu-id="7b06e-503">Qua concept tooContoso advertenties maar implementeert meer functies en meer echte code te bevorderen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-503">Similar in concept tooContoso Ads but implements more features and more real-world coding practices.</span></span>
* <span data-ttu-id="7b06e-504">[Azure Cloud Service-toepassing met meerdere lagen die opslagtabellen, wachtrijen en blobs bevat](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span><span class="sxs-lookup"><span data-stu-id="7b06e-504">[Azure Cloud Service Multi-Tier Application with Tables, Queues, and Blobs](http://code.msdn.microsoft.com/windowsazure/Windows-Azure-Multi-Tier-eadceb36).</span></span> <span data-ttu-id="7b06e-505">Introduceert Azure Storage-tabellen, evenals blobs en wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="7b06e-505">Introduces Azure Storage tables as well as blobs and queues.</span></span> <span data-ttu-id="7b06e-506">Op basis van een oudere versie van hello Azure SDK voor .NET, is enkele wijzigingen toowork met de huidige versie Hallo vereist.</span><span class="sxs-lookup"><span data-stu-id="7b06e-506">Based on an older version of hello Azure SDK for .NET, will require some modifications toowork with hello current version.</span></span>
* <span data-ttu-id="7b06e-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span><span class="sxs-lookup"><span data-stu-id="7b06e-507">[Cloud Service Fundamentals in Microsoft Azure](http://code.msdn.microsoft.com/Cloud-Service-Fundamentals-4ca72649).</span></span> <span data-ttu-id="7b06e-508">Een uitgebreid voorbeeld met van een breed scala aan aanbevolen procedures, opgezet door Hallo Microsoft Patterns and Practice-groep.</span><span class="sxs-lookup"><span data-stu-id="7b06e-508">A comprehensive sample demonstrating a wide range of best practices, produced by hello Microsoft Patterns and Practices group.</span></span>

<span data-ttu-id="7b06e-509">Raadpleeg voor algemene informatie over het ontwikkelen voor Hallo cloud [gebouw echte Cloud-Apps met Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span><span class="sxs-lookup"><span data-stu-id="7b06e-509">For general information about developing for hello cloud, see [Building Real-World Cloud Apps with Azure](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction).</span></span>

<span data-ttu-id="7b06e-510">Aanbevolen procedures en patronen voor een video-inleiding tooAzure opslag, Zie [Microsoft Azure Storage-wat is er nieuw, aanbevolen procedures en patronen](http://channel9.msdn.com/Events/Build/2014/3-628).</span><span class="sxs-lookup"><span data-stu-id="7b06e-510">For a video introduction tooAzure Storage best practices and patterns, see [Microsoft Azure Storage – What's New, Best Practices and Patterns](http://channel9.msdn.com/Events/Build/2014/3-628).</span></span>

<span data-ttu-id="7b06e-511">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="7b06e-511">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="7b06e-512">Deel 1 Azure Cloud Services: Inleiding</span><span class="sxs-lookup"><span data-stu-id="7b06e-512">Azure Cloud Services Part 1: Introduction</span></span>](http://justazure.com/microsoft-azure-cloud-services-part-1-introduction/)
* [<span data-ttu-id="7b06e-513">Hoe toomanage Cloud-Services</span><span class="sxs-lookup"><span data-stu-id="7b06e-513">How toomanage Cloud Services</span></span>](cloud-services-how-to-manage.md)
* [<span data-ttu-id="7b06e-514">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="7b06e-514">Azure Storage</span></span>](/documentation/services/storage/)
* [<span data-ttu-id="7b06e-515">Hoe toochoose een cloud-serviceprovider</span><span class="sxs-lookup"><span data-stu-id="7b06e-515">How toochoose a cloud service provider</span></span>](https://azure.microsoft.com/overview/choosing-a-cloud-service-provider/)
