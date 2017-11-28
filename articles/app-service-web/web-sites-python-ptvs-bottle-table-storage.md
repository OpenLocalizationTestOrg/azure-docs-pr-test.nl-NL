---
title: Bottle en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio
description: Informatie over het gebruik van de Python Tools for Visual Studio een Bottle-toepassing die gegevens in Azure Table Storage opslaat maken en implementeren van de web-app voor Azure App Service Web Apps.
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
ms.openlocfilehash: fb25f03607ac6e9af46b47f54e830e0283dd1b0a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="bottle-and-azure-table-storage-on-azure-with-python-tools-22-for-visual-studio"></a><span data-ttu-id="e3468-103">Bottle en Azure Table Storage in Azure met Python Tools 2.2 voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e3468-103">Bottle and Azure Table Storage on Azure with Python Tools 2.2 for Visual Studio</span></span>
<span data-ttu-id="e3468-104">In deze zelfstudie gebruiken we [Python-Tools voor Visual Studio] voor het maken van een eenvoudige polls web-app met een van de PTVS-voorbeeldsjablonen.</span><span class="sxs-lookup"><span data-stu-id="e3468-104">In this tutorial, we'll use [Python Tools for Visual Studio] to create a simple polls web app using one of the PTVS sample templates.</span></span> <span data-ttu-id="e3468-105">Deze zelfstudie is ook beschikbaar als een [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span><span class="sxs-lookup"><span data-stu-id="e3468-105">This tutorial is also available as a [video](https://www.youtube.com/watch?v=GJXDGaEPy94).</span></span>

<span data-ttu-id="e3468-106">De web-app polls definieert een abstractie voor de opslagplaats, zodat u gemakkelijk tussen verschillende soorten opslagplaatsen (In het geheugen, Azure Table Storage MongoDB schakelen kunt).</span><span class="sxs-lookup"><span data-stu-id="e3468-106">The polls web app defines an abstraction for its repository, so you can easily switch between different types of repositories (In-Memory, Azure Table Storage, MongoDB).</span></span>

<span data-ttu-id="e3468-107">We het maken van een Azure Storage-account, het configureren van de web-app voor het gebruik van Azure Table Storage en hoe u de web-app publiceert leert [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="e3468-107">We'll learn how to create an Azure Storage account, how to configure the web app to use Azure Table Storage, and how to publish the web app to [Azure App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span>

<span data-ttu-id="e3468-108">Zie de [Python Developer Center] voor meer artikelen over ontwikkeling met Azure App Service Web Apps met PTVS met behulp van Bottle Flask- en Django-webframeworks, met MongoDB, Azure Table Storage, MySQL en SQL Database-services.</span><span class="sxs-lookup"><span data-stu-id="e3468-108">See the [Python Developer Center] for more articles that cover development of Azure App Service Web Apps with PTVS using Bottle, Flask and Django web frameworks, with MongoDB, Azure Table Storage, MySQL and SQL Database services.</span></span> <span data-ttu-id="e3468-109">Dit artikel is gericht op App Service, maar voor het ontwikkelen van [Azure Cloud Services] volgt u soortgelijk stappen.</span><span class="sxs-lookup"><span data-stu-id="e3468-109">While this article focuses on App Service, the steps are similar when developing [Azure Cloud Services].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3468-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e3468-110">Prerequisites</span></span>
* <span data-ttu-id="e3468-111">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="e3468-111">Visual Studio 2015</span></span>
* <span data-ttu-id="e3468-112">[Python Tools 2.2 for Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e3468-112">[Python Tools 2.2 for Visual Studio]</span></span>
* <span data-ttu-id="e3468-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span><span class="sxs-lookup"><span data-stu-id="e3468-113">[Python Tools 2.2 for Visual Studio Samples VSIX]</span></span>
* <span data-ttu-id="e3468-114">[Azure SDK-tools voor VS 2015]</span><span class="sxs-lookup"><span data-stu-id="e3468-114">[Azure SDK Tools for VS 2015]</span></span>
* <span data-ttu-id="e3468-115">[Python 2.7 32-bits] of [Python 3.4 32-bits]</span><span class="sxs-lookup"><span data-stu-id="e3468-115">[Python 2.7 32-bit] or [Python 3.4 32-bit]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

> [!NOTE]
> <span data-ttu-id="e3468-116">Als u aan de slag wilt met Azure App Service voordat u zich aanmeldt voor een Azure-account, gaat u naar [App Service uitproberen](https://azure.microsoft.com/try/app-service/). Hier kunt u direct een tijdelijke web-app maken in App Service.</span><span class="sxs-lookup"><span data-stu-id="e3468-116">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="e3468-117">U hebt geen creditcard nodig en u doet geen toezeggingen.</span><span class="sxs-lookup"><span data-stu-id="e3468-117">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="create-the-project"></a><span data-ttu-id="e3468-118">Het project maken</span><span class="sxs-lookup"><span data-stu-id="e3468-118">Create the Project</span></span>
<span data-ttu-id="e3468-119">In deze sectie maakt we een Visual Studio-project met behulp van een voorbeeldsjabloon.</span><span class="sxs-lookup"><span data-stu-id="e3468-119">In this section, we'll create a Visual Studio project using a sample template.</span></span> <span data-ttu-id="e3468-120">We maken van een virtuele omgeving en installeert de vereiste pakketten.</span><span class="sxs-lookup"><span data-stu-id="e3468-120">We'll create a virtual environment and install required packages.</span></span> <span data-ttu-id="e3468-121">Vervolgens voert we de toepassing lokaal via de standaard in het geheugen-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e3468-121">Then we'll run the application locally using the default in-memory repository.</span></span>

1. <span data-ttu-id="e3468-122">Selecteer in Visual Studio **File**, **New Project**.</span><span class="sxs-lookup"><span data-stu-id="e3468-122">In Visual Studio, select **File**, **New Project**.</span></span>
2. <span data-ttu-id="e3468-123">De projectsjablonen uit de [Python Tools 2.2 for Visual Studio Samples VSIX] zijn beschikbaar onder **Python**, **Samples**.</span><span class="sxs-lookup"><span data-stu-id="e3468-123">The project templates from the [Python Tools 2.2 for Visual Studio Samples VSIX] are available under **Python**, **Samples**.</span></span> <span data-ttu-id="e3468-124">Selecteer **Polls Bottle-webproject** en klik op OK om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="e3468-124">Select **Polls Bottle Web Project** and click OK to create the project.</span></span>
   
     ![Het dialoogvenster Nieuw project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleNewProject.png)
3. <span data-ttu-id="e3468-126">U wordt gevraagd om externe pakketten te installeren.</span><span class="sxs-lookup"><span data-stu-id="e3468-126">You will be prompted to install external packages.</span></span> <span data-ttu-id="e3468-127">Selecteer **Install into a virtual environment**.</span><span class="sxs-lookup"><span data-stu-id="e3468-127">Select **Install into a virtual environment**.</span></span>
   
     ![Het dialoogvenster External Packages](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleExternalPackages.png)
4. <span data-ttu-id="e3468-129">Selecteer **Python 2.7** of **Python 3.4** als basisinterpreter.</span><span class="sxs-lookup"><span data-stu-id="e3468-129">Select **Python 2.7** or **Python 3.4** as the base interpreter.</span></span>
   
     ![Het dialoogvenster Add Virtual Environment](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAddVirtualEnv.png)
5. <span data-ttu-id="e3468-131">Controleer of de toepassing werkt, door te drukken op `F5`.</span><span class="sxs-lookup"><span data-stu-id="e3468-131">Confirm that the application works by pressing `F5`.</span></span> <span data-ttu-id="e3468-132">De toepassing gebruikt standaard een opslagplaats in het geheugen die geen configuratie vereist.</span><span class="sxs-lookup"><span data-stu-id="e3468-132">By default, the application uses an in-memory repository which doesn't require any configuration.</span></span> <span data-ttu-id="e3468-133">Alle gegevens gaat verloren wanneer de webserver is gestopt.</span><span class="sxs-lookup"><span data-stu-id="e3468-133">All data is lost when the web server is stopped.</span></span>
6. <span data-ttu-id="e3468-134">Klik op **Create Sample Polls**, klik op een poll en stem.</span><span class="sxs-lookup"><span data-stu-id="e3468-134">Click **Create Sample Polls**, then click on a poll and vote.</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleInMemoryBrowser.png)

## <a name="create-an-azure-storage-account"></a><span data-ttu-id="e3468-136">Een Azure Storage-Account maken</span><span class="sxs-lookup"><span data-stu-id="e3468-136">Create an Azure Storage Account</span></span>
<span data-ttu-id="e3468-137">Als u wilt gebruiken opslagbewerkingen, moet u een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="e3468-137">To use storage operations, you need an Azure storage account.</span></span> <span data-ttu-id="e3468-138">U kunt een opslagaccount maken met de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="e3468-138">You can create a storage account by following these steps.</span></span>

1. <span data-ttu-id="e3468-139">Meld u aan bij de [Azure-Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e3468-139">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e3468-140">Klik op de **nieuw** pictogram op de bovenkant van de Portal links, klikt u op **gegevens en opslag** > **Opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="e3468-140">Click the **New** icon on the top left of the Portal, then click **Data + Storage** > **Storage Account**.</span></span>  <span data-ttu-id="e3468-141">Klik op de **maken** knop en vervolgens het storage-account een unieke naam geven en maak een nieuwe [resourcegroep](../azure-resource-manager/resource-group-overview.md) voor.</span><span class="sxs-lookup"><span data-stu-id="e3468-141">Click the **Create** button, then give the storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Snelle invoer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageCreate.png)
   
    <span data-ttu-id="e3468-143">Wanneer het opslagaccount is gemaakt, de **meldingen** knop knippert een groene **geslaagd** en het opslagaccount blade geopend om weer te geven dat hoort bij de nieuwe resourcegroep die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3468-143">When the storage account has been created, the **Notifications** button will flash a green **SUCCESS** and the storage account's blade is open to show that it belongs to the new resource group you created.</span></span>
3. <span data-ttu-id="e3468-144">Klik op de **toegangssleutels** deel in het opslagaccount blade.</span><span class="sxs-lookup"><span data-stu-id="e3468-144">Click the **Access keys** part in the storage account's blade.</span></span> <span data-ttu-id="e3468-145">Let op de accountnaam en key1.</span><span class="sxs-lookup"><span data-stu-id="e3468-145">Take note of the account name and key1.</span></span>
   
      ![Sleutels](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonAzureStorageKeys.png)
   
    <span data-ttu-id="e3468-147">We nodig deze informatie voor het configureren van uw project in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="e3468-147">We will need this information to configure your project in the next section.</span></span>

## <a name="configure-the-project"></a><span data-ttu-id="e3468-148">Het project configureren</span><span class="sxs-lookup"><span data-stu-id="e3468-148">Configure the Project</span></span>
<span data-ttu-id="e3468-149">In deze sectie configureert onze toepassing voor het gebruik van het opslagaccount dat we zojuist hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e3468-149">In this section, we'll configure our application to use the storage account we just created.</span></span> <span data-ttu-id="e3468-150">Er moet vervolgens de toepassing lokaal uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e3468-150">Then we'll run the application locally.</span></span>

1. <span data-ttu-id="e3468-151">In Visual Studio met de rechtermuisknop op het projectknooppunt in Solution Explorer en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="e3468-151">In Visual Studio, right-click on your project node in Solution Explorer and select **Properties**.</span></span> <span data-ttu-id="e3468-152">Klik op de **Debug** tabblad.</span><span class="sxs-lookup"><span data-stu-id="e3468-152">Click on the **Debug** tab.</span></span>
   
     ![Instellingen voor foutopsporing van project](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageProjectDebugSettings.png)
2. <span data-ttu-id="e3468-154">Stel de waarden van omgevingsvariabelen die zijn vereist voor de toepassing in **serveropdracht Debug**, **omgeving**.</span><span class="sxs-lookup"><span data-stu-id="e3468-154">Set the values of environment variables required by the application in **Debug Server Command**, **Environment**.</span></span>
   
       REPOSITORY_NAME=azuretablestorage
       STORAGE_NAME=<storage account name>
       STORAGE_KEY=<primary access key>
   
   <span data-ttu-id="e3468-155">Hiermee wordt de omgevingsvariabelen ingesteld wanneer u **foutopsporing starten**.</span><span class="sxs-lookup"><span data-stu-id="e3468-155">This will set the environment variables when you **Start Debugging**.</span></span> <span data-ttu-id="e3468-156">Als u wilt dat de variabelen worden ingesteld wanneer u **zonder foutopsporing starten**, stelt u de dezelfde waarden onder **Server-opdracht uitvoeren** ook.</span><span class="sxs-lookup"><span data-stu-id="e3468-156">If you want the variables to be set when you **Start Without Debugging**, set the same values under **Run Server Command** as well.</span></span>
   
   <span data-ttu-id="e3468-157">U kunt ook met behulp van de Windows-Configuratiescherm omgevingsvariabelen definiëren.</span><span class="sxs-lookup"><span data-stu-id="e3468-157">Alternatively, you can define environment variables using the Windows Control Panel.</span></span> <span data-ttu-id="e3468-158">Dit is een betere optie als u wilt voorkomen dat opslaan van referenties in de broncode / project bestand.</span><span class="sxs-lookup"><span data-stu-id="e3468-158">This is a better option if you want to avoid storing credentials in source code / project file.</span></span> <span data-ttu-id="e3468-159">Houd er rekening mee dat u Start Visual Studio voor de nieuwe Omgevingswaarden wilt wel zijn beschikbaar voor de toepassing opnieuw.</span><span class="sxs-lookup"><span data-stu-id="e3468-159">Note that you will need to restart Visual Studio for the new environment values to be available to the application.</span></span>
3. <span data-ttu-id="e3468-160">De code die u de opslagplaats voor Azure Table Storage implementeert is in **models/azuretablestorage.py**.</span><span class="sxs-lookup"><span data-stu-id="e3468-160">The code that implements the Azure Table Storage repository is in **models/azuretablestorage.py**.</span></span> <span data-ttu-id="e3468-161">Zie de [documentatie] voor meer informatie over het gebruik van de Service van de tabel met Python.</span><span class="sxs-lookup"><span data-stu-id="e3468-161">See the [documentation] for more information on how to use Table Service from Python.</span></span>
4. <span data-ttu-id="e3468-162">Voer de toepassing uit met `F5`.</span><span class="sxs-lookup"><span data-stu-id="e3468-162">Run the application with `F5`.</span></span> <span data-ttu-id="e3468-163">Polls die zijn gemaakt met **Create Sample Polls** en de gegevens die zijn ingediend via stemmen, worden geserialiseerd in Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="e3468-163">Polls that are created with **Create Sample Polls** and the data submitted by voting will be serialized in Azure Table Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="e3468-164">De virtuele omgeving voor Python 2.7 kan ertoe leiden dat het einde van een uitzondering in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3468-164">The Python 2.7 Virtual Environment may cause an exception break in Visual Studio.</span></span>  <span data-ttu-id="e3468-165">Druk op `F5` om door te gaan met laden van het webproject.</span><span class="sxs-lookup"><span data-stu-id="e3468-165">Press `F5` to continue loading the web project.</span></span>
   > 
   > 
5. <span data-ttu-id="e3468-166">Blader naar de **over** pagina om te bevestigen dat de toepassing gebruikmaakt van de **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e3468-166">Browse to the **About** page to verify that the application is using the **Azure Table Storage** repository.</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureTableStorageAbout.png)

## <a name="explore-the-azure-table-storage"></a><span data-ttu-id="e3468-168">De Azure-tabelopslag verkennen</span><span class="sxs-lookup"><span data-stu-id="e3468-168">Explore the Azure Table Storage</span></span>
<span data-ttu-id="e3468-169">Het is gemakkelijk weergeven en bewerken van storage-tabellen met Cloud Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e3468-169">It's easy to view and edit storage tables using Cloud Explorer in Visual Studio.</span></span> <span data-ttu-id="e3468-170">In deze sectie we Server Explorer gebruiken om de inhoud van de toepassing polls tabellen weergeven.</span><span class="sxs-lookup"><span data-stu-id="e3468-170">In this section we'll use Server Explorer to view the contents of the polls application tables.</span></span>

> [!NOTE]
> <span data-ttu-id="e3468-171">Hiervoor moet Microsoft Azure-hulpprogramma's worden geïnstalleerd, die beschikbaar als zijn onderdeel van de [Azure SDK voor .NET].</span><span class="sxs-lookup"><span data-stu-id="e3468-171">This requires Microsoft Azure Tools to be installed, which are available as part of the [Azure SDK for .NET].</span></span>
> 
> 

1. <span data-ttu-id="e3468-172">Open **Cloud Explorer**.</span><span class="sxs-lookup"><span data-stu-id="e3468-172">Open **Cloud Explorer**.</span></span> <span data-ttu-id="e3468-173">Vouw **Opslagaccounts**, uw storage-account, klikt u vervolgens **tabellen**.</span><span class="sxs-lookup"><span data-stu-id="e3468-173">Expand **Storage Accounts**, your storage account, then **Tables**.</span></span>
   
     ![Cloud Explorer](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorer.png)
2. <span data-ttu-id="e3468-175">Dubbelklik op de **polls** of **keuzes** tabel om de inhoud van de tabel in het venster van een document, evenals toevoegen/verwijderen/bewerken entiteiten weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e3468-175">Double-click on the **polls** or **choices** table to view the contents of the table in a document window, as well as add/remove/edit entities.</span></span>
   
     ![De resultaten van de Query](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonServerExplorerTable.png)

## <a name="publish-the-web-app-to-azure-app-service"></a><span data-ttu-id="e3468-177">De web-app publiceren naar Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e3468-177">Publish the web app to Azure App Service</span></span>
<span data-ttu-id="e3468-178">De Azure SDK voor .NET biedt een eenvoudige manier om uw web-app in Azure App Service te implementeren.</span><span class="sxs-lookup"><span data-stu-id="e3468-178">The Azure .NET SDK provides an easy way to deploy your web app to Azure App Service.</span></span>

1. <span data-ttu-id="e3468-179">Klik in **Solution Explorer** met de rechtermuisknop op het projectknooppunt en selecteer **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="e3468-179">In **Solution Explorer**, right-click on the project node and select **Publish**.</span></span>
   
     ![Het dialoogvenster Publish Web](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonPublishWebSiteDialog.png)
2. <span data-ttu-id="e3468-181">Klik op **Microsoft Azure Web Apps**.</span><span class="sxs-lookup"><span data-stu-id="e3468-181">Click on **Microsoft Azure Web Apps**.</span></span>
3. <span data-ttu-id="e3468-182">Klik op **Nieuw** om een nieuwe web-app te maken.</span><span class="sxs-lookup"><span data-stu-id="e3468-182">Click on **New** to create a new web app.</span></span>
4. <span data-ttu-id="e3468-183">Vul de volgende velden in en klikt u op **maken**.</span><span class="sxs-lookup"><span data-stu-id="e3468-183">Fill in the following fields and click **Create**.</span></span>
   
   * <span data-ttu-id="e3468-184">**Web-appnaam**</span><span class="sxs-lookup"><span data-stu-id="e3468-184">**Web App name**</span></span>
   * <span data-ttu-id="e3468-185">**App Service-plan**</span><span class="sxs-lookup"><span data-stu-id="e3468-185">**App Service plan**</span></span>
   * <span data-ttu-id="e3468-186">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="e3468-186">**Resource group**</span></span>
   * <span data-ttu-id="e3468-187">**Regio**</span><span class="sxs-lookup"><span data-stu-id="e3468-187">**Region**</span></span>
   * <span data-ttu-id="e3468-188">Laat **Databaseserver** ingesteld op **Geen database**.</span><span class="sxs-lookup"><span data-stu-id="e3468-188">Leave **Database server** set to **No database**</span></span>
5. <span data-ttu-id="e3468-189">Accepteer alle overige standaardwaarden en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="e3468-189">Accept all other defaults and click **Publish**.</span></span>
6. <span data-ttu-id="e3468-190">De gepubliceerde web-app wordt automatisch geopend in uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="e3468-190">Your web browser will open automatically to the published web app.</span></span> <span data-ttu-id="e3468-191">Als u naar bladeren de pagina, ziet u dat deze gebruikmaakt van de **In-Memory** -opslagplaats, niet de **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e3468-191">If you browse to the about page, you'll see that it uses the **In-Memory** repository, not the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e3468-192">Dat komt doordat de omgevingsvariabelen zijn niet ingesteld op het exemplaar van de Web-Apps in Azure App Service, zodat deze gebruikmaakt van de standaardwaarden die is opgegeven in **settings.py**.</span><span class="sxs-lookup"><span data-stu-id="e3468-192">That's because the environment variables are not set on the Web Apps instance in Azure App Service, so it uses the default values specified in **settings.py**.</span></span>

## <a name="configure-the-web-apps-instance"></a><span data-ttu-id="e3468-193">Het exemplaar van de Web-Apps configureren</span><span class="sxs-lookup"><span data-stu-id="e3468-193">Configure the Web Apps instance</span></span>
<span data-ttu-id="e3468-194">In deze sectie configureert omgevingsvariabelen voor het exemplaar van de Web-Apps.</span><span class="sxs-lookup"><span data-stu-id="e3468-194">In this section, we'll configure environment variables for the Web Apps instance.</span></span>

1. <span data-ttu-id="e3468-195">In [Azure Portal], opent u de web-app-blade door te klikken op **Bladeren** > **App Services** > de naam van uw web-app.</span><span class="sxs-lookup"><span data-stu-id="e3468-195">In [Azure Portal], open the web app's blade by clicking **Browse** > **App Services** > your web app name.</span></span>
2. <span data-ttu-id="e3468-196">Klik op de blade van uw web-app **alle instellingen**, klikt u vervolgens op **toepassingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="e3468-196">In your web app's blade, click **All Settings**, then click **Application Settings**.</span></span>
3. <span data-ttu-id="e3468-197">Schuif omlaag naar de **appinstellingen** sectie en stel de waarden voor **OPSLAGPLAATS\_naam**, **opslag\_naam** en **opslag \_Sleutel** zoals beschreven in de **configureren van het project** sectie hierboven.</span><span class="sxs-lookup"><span data-stu-id="e3468-197">Scroll down to the **App settings** section and set the values for **REPOSITORY\_NAME**, **STORAGE\_NAME** and **STORAGE\_KEY** as described in the **Configure the project** section above.</span></span>
   
     ![App-instellingen](./media/web-sites-python-ptvs-bottle-table-storage/PollsCommonWebSiteConfigureSettingsTableStorage.png)
4. <span data-ttu-id="e3468-199">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="e3468-199">Click on **Save**.</span></span> <span data-ttu-id="e3468-200">Nadat u de meldingen dat de wijzigingen zijn toegepast hebt ontvangen, klikt u op **Bladeren** van de hoofdblade van Web-app.</span><span class="sxs-lookup"><span data-stu-id="e3468-200">After you've received the notifications that the changes were applied, click on **Browse** from the Web app main blade.</span></span>
5. <span data-ttu-id="e3468-201">U ziet de web-app werkt zoals verwacht, met behulp van de **Azure Table Storage** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="e3468-201">You should see the web app working as expected, using the **Azure Table Storage** repository.</span></span>
   
   <span data-ttu-id="e3468-202">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="e3468-202">Congratulations!</span></span>
   
     ![Webbrowser](./media/web-sites-python-ptvs-bottle-table-storage/PollsBottleAzureBrowser.png)

## <a name="next-steps"></a><span data-ttu-id="e3468-204">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3468-204">Next steps</span></span>
<span data-ttu-id="e3468-205">Volg deze koppelingen voor meer informatie over Python Tools for Visual Studio, Bottle en Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="e3468-205">Follow these links to learn more about Python Tools for Visual Studio, Bottle and Azure Table Storage.</span></span>

* <span data-ttu-id="e3468-206">[Documentatie Python Tools voor Visual Studio]</span><span class="sxs-lookup"><span data-stu-id="e3468-206">[Python Tools for Visual Studio Documentation]</span></span>
  * <span data-ttu-id="e3468-207">[Webprojecten]</span><span class="sxs-lookup"><span data-stu-id="e3468-207">[Web Projects]</span></span>
  * <span data-ttu-id="e3468-208">[Cloudserviceprojecten]</span><span class="sxs-lookup"><span data-stu-id="e3468-208">[Cloud Service Projects]</span></span>
  * <span data-ttu-id="e3468-209">[Foutopsporing op afstand in Microsoft Azure]</span><span class="sxs-lookup"><span data-stu-id="e3468-209">[Remote Debugging on Microsoft Azure]</span></span>
* <span data-ttu-id="e3468-210">[Bottle-documentatie]</span><span class="sxs-lookup"><span data-stu-id="e3468-210">[Bottle Documentation]</span></span>
* <span data-ttu-id="e3468-211">[Azure Storage]</span><span class="sxs-lookup"><span data-stu-id="e3468-211">[Azure Storage]</span></span>
* <span data-ttu-id="e3468-212">[Azure-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="e3468-212">[Azure SDK for Python]</span></span>
* <span data-ttu-id="e3468-213">[Het gebruik van de Storage-Service van de tabel met Python]</span><span class="sxs-lookup"><span data-stu-id="e3468-213">[How to Use the Table Storage Service from Python]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="e3468-214">Wat is er gewijzigd</span><span class="sxs-lookup"><span data-stu-id="e3468-214">What's changed</span></span>
* <span data-ttu-id="e3468-215">Als u van Websites wilt overstappen op App Service, raadpleegt u de volgende handleiding: [Azure App Service en de invloed ervan op bestaande Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="e3468-215">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!--Link references-->
[Python Developer Center]: /develop/python/
[Azure Cloud Services]: ../cloud-services/cloud-services-python-ptvs.md
[documentatie]:../cosmos-db/table-storage-how-to-use-python.md
[Het gebruik van de Storage-Service van de tabel met Python]:../cosmos-db/table-storage-how-to-use-python.md


<!--External Link references-->
[Azure Portal]: https://portal.azure.com
[Azure SDK voor .NET]: http://azure.microsoft.com/downloads/
[Python-Tools voor Visual Studio]: http://aka.ms/ptvs
[Python Tools 2.2 for Visual Studio]: http://go.microsoft.com/fwlink/?LinkId=624025
[Python Tools 2.2 for Visual Studio Samples VSIX]: http://go.microsoft.com/fwlink/?LinkId=624025
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
