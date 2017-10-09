---
title: aaaBottle en Azure Table Storage in Azure met Python-Tools 2.2 voor Visual Studio
description: Informatie over hoe toouse hello Python-Tools voor Visual Studio toocreate een Bottle-toepassing die gegevens opslaat in Azure Table Storage en Hallo web app tooAzure App Service Web Apps te implementeren.
services: app-service\web
documentationcenter: python
author: huguesv
manager: erikre
editor: 
ms.assetid: f075124b-db79-4e51-b394-09187dd6c634
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/07/2016
ms.author: huvalo
ms.openlocfilehash: 25b9eb002b8748483d5b9458b7b5860a958b4bb3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="5b1df-103">Bottle en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b1df-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="5b1df-104">In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] toocreate een eenvoudige web-app met een van de PTVS-voorbeeldsjablonen Hallo worden opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="5b1df-104">In this tutorial, we'll use [Python Tools for Visual Studio] toocreate a simple polls web app using one of hello PTVS sample templates.</span></span> <span data-ttu-id="5b1df-105">Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="5b1df-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="5b1df-106">Hallo polls web-app definieert een abstractie voor de opslagplaats, zodat u gemakkelijk tussen verschillende soorten opslagplaatsen (In het geheugen, Azure Table Storage MongoDB schakelen kunt).</span><span class="sxs-lookup"><span data-stu-id="5b1df-106">hello polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="5b1df-107">We leert hoe toocreate een Azure Storage-account, hoe tooconfigure Hallo web app toouse Azure Table Storage en hoe toopublish Hallo web-app te[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="5b1df-107">We'll learn how toocreate an Azure Storage account, how tooconfigure hello web app toouse Azure Table Storage, and how toopublish hello web app too[Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="5b1df-108">Zie Hallo [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met MongoDB, Azure Table Storage, MySQL en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="5b1df-108">See hello [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="5b1df-109">Dit artikel is gericht op App Service, Hallo stappen zijn vergelijkbaar bij het ontwikkelen van [Azure Cloud Services].</span><span class="sxs-lookup"><span data-stu-id="5b1df-109">While this article focuses on App Service, hello steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b1df-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5b1df-110">Prerequisites</span></span>
* <span data-ttu-id="5b1df-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5b1df-111">Visual Studio 2015</span></span>
* <span data-ttu-id="5b1df-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="5b1df-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="5b1df-113">[Python-Tools 2.2 voor Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="5b1df-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="5b1df-114">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="5b1df-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="5b1df-115">[Python 2.7 32-bits] of [Python 3.4 32-bits]</span><span class="sxs-lookup"><span data-stu-id="5b1df-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="5b1df-116">Als u wilt dat tooget de slag met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u verder te[App Service uitproberen](https://azure.microsoft.com/try/app-service/), waar u direct een tijdelijke en eenvoudige web-app kunt maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="5b1df-116">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="5b1df-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="5b1df-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-hello-project"></a><span data-ttu-id="5b1df-118">Hallo-Project maken</span><span class="sxs-lookup"><span data-stu-id="5b1df-118">Create hello Project</span></span>
<span data-ttu-id="5b1df-119">In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="5b1df-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="5b1df-120">We maken van een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="5b1df-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="5b1df-121">Vervolgens voert we Hallo-toepassing lokaal via Hallo standaard in het geheugen opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5b1df-121">Then we'll run hello application locally using hello default in-memory repository.</span></span>

1. <span data-ttu-id="5b1df-122">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="5b1df-123">Hallo projectsjablonen uit Hallo [Python-Tools 2.2 voor Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **voorbeelden**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-123">hello project templates from hello [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="5b1df-124">Selecteer **Polls Bottle-webproject** en klik op OK toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="5b1df-124">Select **Polls Bottle Web Project** and click OK toocreate hello project.</span></span>
   
     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="5b1df-126">U zult na vragen aan gebruiker tooinstall externe pakketten.</span><span class="sxs-lookup"><span data-stu-id="5b1df-126">You will be prompted tooinstall external packages.</span></span> <span data-ttu-id="5b1df-127">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-127">Select **Install into a virtual environment**.</span></span>
   
     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="5b1df-129">Selecteer **Python 2.7** of **Python 3.4** als Hallo basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="5b1df-129">Select **Python 2.7** or **Python 3.4** as hello base interpreter.</span></span>
   
     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="5b1df-131">Controleer of de toepassing hello door te drukken werkt `F5`.</span><span class="sxs-lookup"><span data-stu-id="5b1df-131">Confirm that hello application works by pressing `F5`.</span></span> <span data-ttu-id="5b1df-132">Hallo-toepassing gebruikt standaard een opslagplaats in het geheugen die geen configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="5b1df-132">By default, hello application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="5b1df-133">Alle gegevens gaat verloren wanneer Hallo webserver is gestopt.</span><span class="sxs-lookup"><span data-stu-id="5b1df-133">All data is lost when hello web server is stopped.</span></span>
6. <span data-ttu-id="5b1df-134">Klik op **Create Sample Polls**, klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="5b1df-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="5b1df-136">Een Azure Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="5b1df-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="5b1df-137">toouse-opslagbewerkingen, moet u een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="5b1df-137">toouse storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="5b1df-138">U kunt een opslagaccount maken met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="5b1df-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="5b1df-139">Meld u aan bij Hallo [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5b1df-139">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="5b1df-140">Klik op Hallo **nieuw** pictogram op de voorgrond Hallo Hallo Portal links, klikt u op **gegevens en opslag** > **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-140">Click hello **New** icon on hello top left of hello Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="5b1df-141">Klik op Hallo **maken** knop vervolgens Hallo storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.</span><span class="sxs-lookup"><span data-stu-id="5b1df-141">Click hello **Create** button, then give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Snelle invoer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="5b1df-143">Wanneer Hallo storage-account is gemaakt, Hallo **meldingen** knop knippert een groene **geslaagd** en blade Hallo van het opslagaccount is geopend dat deze deel uitmaakt van de nieuwe resource toohello tooshow groep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b1df-143">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="5b1df-144">Klik op Hallo **toegangssleutels** deel in de blade Hallo van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b1df-144">Click hello **Access keys** part in hello storage account's blade.</span></span> <span data-ttu-id="5b1df-145">Let op het Hallo-accountnaam en key1.</span><span class="sxs-lookup"><span data-stu-id="5b1df-145">Take note of hello account name and key1.</span></span>
   
      ![Sleutels](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="5b1df-147">We moet deze informatie tooconfigure uw project in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b1df-147">We will need this information tooconfigure your project in hello next section.</span></span>

## <a name="configure-hello-project"></a><span data-ttu-id="5b1df-148">Hallo Project configureren</span><span class="sxs-lookup"><span data-stu-id="5b1df-148">Configure hello Project</span></span>
<span data-ttu-id="5b1df-149">In deze sectie configureert we onze toepassing toouse hello opslagaccount die we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5b1df-149">In this section, we'll configure our application toouse hello storage account we just created.</span></span> <span data-ttu-id="5b1df-150">Vervolgens voert we lokaal Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5b1df-150">Then we'll run hello application locally.</span></span>

1. <span data-ttu-id="5b1df-151">In Visual Studio met de rechtermuisknop op het projectknooppunt in Solution Explorer en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="5b1df-152">Klik op Hallo **Debug** tabblad.</span><span class="sxs-lookup"><span data-stu-id="5b1df-152">Click on hello **Debug** tab.</span></span>
   
     ![Instellingen voor foutopsporing van project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="5b1df-154">Stel Hallo waarden van omgevingsvariabelen die worden vereist door de toepassing hello in **serveropdracht Debug**, **omgeving**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-154">Set hello values of environment variables required by hello application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="5b1df-155">Deze omgevingsvariabelen hello wordt ingesteld wanneer u **foutopsporing starten**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-155">This will set hello environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="5b1df-156">Als u wilt dat Hallo variabelen toobe ingesteld wanneer u **zonder foutopsporing starten**, set Hallo dezelfde waarden onder **Server-opdracht uitvoeren** ook.</span><span class="sxs-lookup"><span data-stu-id="5b1df-156">If you want hello variables toobe set when you **Start Without Debugging**, set hello same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="5b1df-157">U kunt ook met behulp van het Configuratiescherm van Windows hello omgevingsvariabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="5b1df-157">Alternatively, you can define environment variables using hello Windows Control Panel.</span></span> <span data-ttu-id="5b1df-158">Dit is een betere optie als u wilt opslaan van referenties in de broncode tooavoid / projectbestand.</span><span class="sxs-lookup"><span data-stu-id="5b1df-158">This is a better option if you want tooavoid storing credentials in source code / project file.</span></span> <span data-ttu-id="5b1df-159">Houd er rekening mee dat u Visual Studio toorestart voor Hallo nieuwe omgeving waarden toobe beschikbaar toohello toepassing nodig.</span><span class="sxs-lookup"><span data-stu-id="5b1df-159">Note that you will need toorestart Visual Studio for hello new environment values toobe available toohello application.</span></span>
3. <span data-ttu-id="5b1df-160">Hallo-code die wordt geïmplementeerd hello Azure Table Storage opslagplaats **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-160">hello code that implements hello Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="5b1df-161">Zie Hallo [documentatie] voor meer informatie over het toouse Tabelservice van Python.</span><span class="sxs-lookup"><span data-stu-id="5b1df-161">See hello [documentation] for more information on how toouse Table Service from Python.</span></span>
4. <span data-ttu-id="5b1df-162">Voer de toepassing hello met `F5`.</span><span class="sxs-lookup"><span data-stu-id="5b1df-162">Run hello application with `F5`.</span></span> <span data-ttu-id="5b1df-163">Polls die zijn gemaakt met **Create Sample Polls** en het Hallo-gegevens die zijn ingediend via stemmen, worden geserialiseerd in Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="5b1df-163">Polls that are created with **Create Sample Polls** and hello data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="5b1df-164">Hallo virtuele omgeving voor Python 2.7 kan ertoe leiden dat het einde van een uitzondering in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b1df-164">hello Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="5b1df-165">Druk op `F5` toocontinue Hallo webproject wordt geladen.</span><span class="sxs-lookup"><span data-stu-id="5b1df-165">Press `F5` toocontinue loading hello web project.</span></span>
   > 
   > 
5. <span data-ttu-id="5b1df-166">Blader toohello **over** pagina tooverify die toepassing hello maakt gebruik van Hallo **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5b1df-166">Browse toohello **About** page tooverify that hello application is using hello **Azure Table Storage** repository.</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-hello-azure-table-storage"></a><span data-ttu-id="5b1df-168">Hello Azure Table Storage verkennen</span><span class="sxs-lookup"><span data-stu-id="5b1df-168">Explore hello Azure Table Storage</span></span>
<span data-ttu-id="5b1df-169">Het is gemakkelijk tooview en storage-tabellen met Cloud Explorer in Visual Studio bewerken.</span><span class="sxs-lookup"><span data-stu-id="5b1df-169">It's easy tooview and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="5b1df-170">We gebruiken Server Explorer tooview Hallo inhoud van Hallo polls toepassingstabellen in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="5b1df-170">In this section we'll use Server Explorer tooview hello contents of hello polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="5b1df-171">Hiervoor moeten toobe van Microsoft Azure-hulpprogramma's geïnstalleerd, die beschikbaar zijn als onderdeel van Hallo [Azure SDK voor .NET].</span><span class="sxs-lookup"><span data-stu-id="5b1df-171">This requires Microsoft Azure Tools toobe installed, which are available as part of hello [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="5b1df-172">Open **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="5b1df-173">Vouw **Opslagaccounts**, uw storage-account, klikt u vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="5b1df-175">Dubbelklik op Hallo **polls** of **keuzes** tabel tooview Hallo inhoud van Hallo-tabel in het venster van een document, alsmede entiteiten toevoegen/verwijderen/bewerken.</span><span class="sxs-lookup"><span data-stu-id="5b1df-175">Double-click on hello **polls** or **choices** table tooview hello contents of hello table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![De resultaten van de Query](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-hello-web-app-tooazure-app-service"></a><span data-ttu-id="5b1df-177">Hallo web app tooAzure App Service publiceren</span><span class="sxs-lookup"><span data-stu-id="5b1df-177">Publish hello web app tooAzure App Service</span></span>
<span data-ttu-id="5b1df-178">Hello Azure .NET SDK biedt een eenvoudige manier toodeploy uw web-app tooAzure App Service.</span><span class="sxs-lookup"><span data-stu-id="5b1df-178">hello Azure .NET SDK provides an easy way toodeploy your web app tooAzure App Service.</span></span>

1. <span data-ttu-id="5b1df-179">In **Solution Explorer**, met de rechtermuisknop op Hallo projectknooppunt en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-179">In **Solution Explorer**, right-click on hello project node and select **Publish**.</span></span>
   
     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="5b1df-181">Klik op **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="5b1df-182">Klik op **nieuw** toocreate een nieuwe web-app.</span><span class="sxs-lookup"><span data-stu-id="5b1df-182">Click on **New** toocreate a new web app.</span></span>
4. <span data-ttu-id="5b1df-183">Vul Hallo velden te volgen en klik op **maken**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-183">Fill in hello following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="5b1df-184">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="5b1df-184">**Web App name**</span></span>
   * <span data-ttu-id="5b1df-185">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="5b1df-185">**App Service plan**</span></span>
   * <span data-ttu-id="5b1df-186">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="5b1df-186">**Resource group**</span></span>
   * <span data-ttu-id="5b1df-187">**Regio**</span><span class="sxs-lookup"><span data-stu-id="5b1df-187">**Region**</span></span>
   * <span data-ttu-id="5b1df-188">Laat **databaseserver** instellen te**geen database**</span><span class="sxs-lookup"><span data-stu-id="5b1df-188">Leave **Database server** set too**No database**</span></span>
5. <span data-ttu-id="5b1df-189">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="5b1df-190">De webbrowser wordt automatisch geopend toohello gepubliceerde web-app.</span><span class="sxs-lookup"><span data-stu-id="5b1df-190">Your web browser will open automatically toohello published web app.</span></span> <span data-ttu-id="5b1df-191">Als u toohello over pagina bladert, ziet u dat deze gebruikmaakt van Hallo **In-Memory** opslagplaats, niet Hallo **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5b1df-191">If you browse toohello about page, you'll see that it uses hello **In-Memory** repository, not hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="5b1df-192">Dat komt doordat Hallo omgevingsvariabelen zijn niet ingesteld op Hallo Web-Apps-exemplaar in Azure App Service, zodat het Hallo-standaardwaarden die is opgegeven in beslag **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-192">That's because hello environment variables are not set on hello Web Apps instance in Azure App Service, so it uses hello default values specified in **settings.py**.</span></span>

## <a name="configure-hello-web-apps-instance"></a><span data-ttu-id="5b1df-193">Hallo-Web-Apps exemplaar configureren</span><span class="sxs-lookup"><span data-stu-id="5b1df-193">Configure hello Web Apps instance</span></span>
<span data-ttu-id="5b1df-194">In deze sectie configureert omgevingsvariabelen voor Hallo Web-Apps-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="5b1df-194">In this section, we'll configure environment variables for hello Web Apps instance.</span></span>

1. <span data-ttu-id="5b1df-195">In [Azure Portal], Hallo van web-app-blade geopend door te klikken op **Bladeren** > **App Services** > de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="5b1df-195">In [Azure Portal], open hello web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="5b1df-196">Klik op de blade van uw web-app **alle instellingen**, klikt u vervolgens op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="5b1df-197">Schuif omlaag toohello **appinstellingen** en stel de waarden voor Hallo **OPSLAGPLAATS\_naam**, **opslag\_naam** en  **OPSLAG\_sleutel** zoals beschreven in Hallo **configureren Hallo project** sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="5b1df-197">Scroll down toohello **App settings** section and set hello values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in hello **Configure hello project** section above.</span></span>
   
     ![App-instellingen](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="5b1df-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5b1df-199">Click on **Save**.</span></span> <span data-ttu-id="5b1df-200">Nadat u hebt ontvangen Hallo meldingen dat Hallo wijzigingen zijn toegepast, klikt u op **Bladeren** van Web-app hoofdblade Hallo.</span><span class="sxs-lookup"><span data-stu-id="5b1df-200">After you've received hello notifications that hello changes were applied, click on **Browse** from hello Web app main blade.</span></span>
5. <span data-ttu-id="5b1df-201">U ziet Hallo web-app werkt zoals verwacht, met behulp van Hallo **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="5b1df-201">You should see hello web app working as expected, using hello **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="5b1df-202">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="5b1df-202">Congratulations!</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="5b1df-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b1df-204">Next steps</span></span>
<span data-ttu-id="5b1df-205">Volg deze koppelingen toolearn meer over Python-Tools voor Visual Studio, Bottle en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="5b1df-205">Follow these links toolearn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="5b1df-206">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="5b1df-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="5b1df-207">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="5b1df-207">[Web Projects]</span></span>
  * <span data-ttu-id="5b1df-208">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="5b1df-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="5b1df-209">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="5b1df-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="5b1df-210">[Bottle-documentatie]</span><span class="sxs-lookup"><span data-stu-id="5b1df-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="5b1df-211">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="5b1df-211">[Azure Storage]</span></span>
* <span data-ttu-id="5b1df-212">[Azure-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="5b1df-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="5b1df-213">[Hoe tooUse Hallo Table Storage-Service met Python]</span><span class="sxs-lookup"><span data-stu-id="5b1df-213">[How tooUse hello Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="5b1df-214">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="5b1df-214">What's changed</span></span>
* <span data-ttu-id="5b1df-215">Zie voor een handleiding toohello wijzigingen van de Websites tooApp Service: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="5b1df-215">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentatie]:../cosmos-db/table-storage-how-to-use-python.md
[Hoe tooUse Hallo Table Storage-Service met Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK voor .NET]: http://azure.microsoft.com/downloads/
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python-Tools 2.2 voor Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
[Azure SDK-tools voor VS 2015]: http://go.microsoft.com/fwlink/?LinkId=518003
[Python 2.7 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517190
[Python 3.4 32-bits]: http://go.microsoft.com/fwlink/?LinkId=517191
[Documentatie Python Tools voor Visual Studio]: http://aka.ms/ptvsdocs
[Bottle-documentatie]: http://bottlepy.org/docs/dev/index.html
[Foutopsporing op afstand in Microsoft Azure]: http://go.microsoft.com/fwlink/?LinkId=624026
[Webprojecten]: http://go.microsoft.com/fwlink/?LinkId=624027
[Cloudserviceprojecten]: http://go.microsoft.com/fwlink/?LinkId=624028
[Azure Storage]: http://azure.microsoft.com/documentation/services/storage/
[Azure-SDK voor Python]: https://github.com/Azure/azure-sdk-for-python
