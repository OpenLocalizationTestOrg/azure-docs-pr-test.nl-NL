---
title: Een ASP.NET-app in Azure met SQL-Database bouwen | Microsoft Docs
description: Informatie over het ophalen van een ASP.NET-app in Azure, werkt met verbinding met een SQL-Database.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 03c584f1-a93c-4e3d-ac1b-c82b50c75d3e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: csharp
ms.topic: tutorial
ms.date: 06/09/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: c22b8ef4866fe2f1ae32c7cb9158fc7866788b26
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="068c3-103">Een ASP.NET-app in Azure met SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="068c3-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="068c3-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="068c3-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="068c3-105">Deze zelfstudie leert u hoe u een gegevensgestuurd ASP.NET web-app implementeren in Azure en verbindt deze met [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="068c3-105">This tutorial shows you how to deploy a data-driven ASP.NET web app in Azure and connect it to [Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="068c3-106">Wanneer u klaar bent, hebt u een ASP.NET-app uitgevoerd in de [Azure App Service](../app-service/app-service-value-prop-what-is.md) en verbonden met SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="068c3-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected to SQL Database.</span></span>

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="068c3-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="068c3-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="068c3-109">Maken van een SQL-Database in Azure</span><span class="sxs-lookup"><span data-stu-id="068c3-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="068c3-110">Een ASP.NET-app verbinden met SQL Database</span><span class="sxs-lookup"><span data-stu-id="068c3-110">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="068c3-111">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="068c3-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="068c3-112">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="068c3-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="068c3-113">Logboeken van de stroom van Azure naar uw terminal</span><span class="sxs-lookup"><span data-stu-id="068c3-113">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="068c3-114">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="068c3-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="068c3-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="068c3-115">Prerequisites</span></span>

<span data-ttu-id="068c3-116">Vereisten voor het voltooien van deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="068c3-116">To complete this tutorial:</span></span>

* <span data-ttu-id="068c3-117">Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) met de volgende workloads:</span><span class="sxs-lookup"><span data-stu-id="068c3-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with the following workloads:</span></span>
  - <span data-ttu-id="068c3-118">**ASP.NET- en web-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="068c3-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="068c3-119">**Azure-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="068c3-119">**Azure development**</span></span>

  ![ASP.NET- en web-ontwikkeling en Azure-ontwikkeling (onder Web en cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample"></a><span data-ttu-id="068c3-121">Het voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="068c3-121">Download the sample</span></span>

<span data-ttu-id="068c3-122">[Download het voorbeeldproject](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="068c3-122">[Download the sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="068c3-123">Pak (uitpakken van) de *dotnet-sqldb-zelfstudie-master.zip* bestand.</span><span class="sxs-lookup"><span data-stu-id="068c3-123">Extract (unzip) the  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="068c3-124">Het voorbeeldproject bevat een eenvoudige [ASP.NET MVC](https://www.asp.net/mvc) CRUD (maken-lezen-update-verwijderen) met behulp van app [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="068c3-124">The sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-the-app"></a><span data-ttu-id="068c3-125">De app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="068c3-125">Run the app</span></span>

<span data-ttu-id="068c3-126">Open de *dotnet-sqldb-zelfstudie-master/DotNetAppSqlDb.sln* bestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="068c3-126">Open the *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="068c3-127">Type `Ctrl+F5` voor het uitvoeren van de app zonder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="068c3-127">Type `Ctrl+F5` to run the app without debugging.</span></span> <span data-ttu-id="068c3-128">De app wordt weergegeven in de browser.</span><span class="sxs-lookup"><span data-stu-id="068c3-128">The app is displayed in your default browser.</span></span> <span data-ttu-id="068c3-129">Selecteer de **nieuw** koppelen en maken van een paar *taak* items.</span><span class="sxs-lookup"><span data-stu-id="068c3-129">Select the **Create New** link and create a couple *to-do* items.</span></span> 

![Het dialoogvenster Nieuw ASP.NET-project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="068c3-131">Test de **bewerken**, **Details**, en **verwijderen** koppelingen.</span><span class="sxs-lookup"><span data-stu-id="068c3-131">Test the **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="068c3-132">De app gebruikmaakt van een databasecontext om te verbinden met de database.</span><span class="sxs-lookup"><span data-stu-id="068c3-132">The app uses a database context to connect with the database.</span></span> <span data-ttu-id="068c3-133">In dit voorbeeld gebruikt de databasecontext een verbindingsreeks met de naam `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="068c3-133">In this sample, the database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="068c3-134">De verbindingsreeks is ingesteld in de *Web.config* bestands- en waarnaar wordt verwezen in de *Models/MyDatabaseContext.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="068c3-134">The connection string is set in the *Web.config* file and referenced in the *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="068c3-135">De naam van de tekenreeks wordt verderop in de zelfstudie gebruikt voor de Azure-web-app verbinden met een Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="068c3-135">The connection string name is used later in the tutorial to connect the Azure web app to an Azure SQL Database.</span></span> 

## <a name="publish-to-azure-with-sql-database"></a><span data-ttu-id="068c3-136">Publiceren naar Azure met SQL Database</span><span class="sxs-lookup"><span data-stu-id="068c3-136">Publish to Azure with SQL Database</span></span>

<span data-ttu-id="068c3-137">In de **Solution Explorer**, met de rechtermuisknop op uw **DotNetAppSqlDb** project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="068c3-137">In the **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publiceren vanuit Solution Explorer](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="068c3-139">Zorg ervoor dat **Microsoft Azure App Service** is geselecteerd en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="068c3-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publiceren vanaf de projectoverzichtspagina](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="068c3-141">Publiceren wordt geopend de **Create App Service** dialoogvenster dat helpt u bij het maken van alle Azure moet u uw ASP.NET-web-app uitvoeren in Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="068c3-141">Publishing opens the **Create App Service** dialog, which helps you create all the Azure resources you need to run your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-to-azure"></a><span data-ttu-id="068c3-142">Aanmelden bij Azure</span><span class="sxs-lookup"><span data-stu-id="068c3-142">Sign in to Azure</span></span>

<span data-ttu-id="068c3-143">Klik in het dialoogvenster **App Service maken** op **Een account toevoegen** en meld u vervolgens aan bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="068c3-143">In the **Create App Service** dialog, click **Add an account**, and then sign in to your Azure subscription.</span></span> <span data-ttu-id="068c3-144">Als u al bent aangemeld bij een Microsoft-account, moet u ervoor zorgen dat dit account uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="068c3-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="068c3-145">Als het aangemelde Microsoft-account niet uw Azure-abonnement bevat, klikt u erop om het juiste account toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="068c3-145">If the signed-in Microsoft account doesn't have your Azure subscription, click it to add the correct account.</span></span>
   
![Aanmelden bij Azure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="068c3-147">Als u bent aangemeld, kunt u in dit dialoogvenster alle resources gaan maken die u nodig hebt voor uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-147">Once signed in, you're ready to create all the resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-the-web-app-name"></a><span data-ttu-id="068c3-148">De naam van de web-app configureren</span><span class="sxs-lookup"><span data-stu-id="068c3-148">Configure the web app name</span></span>

<span data-ttu-id="068c3-149">De naam van de gegenereerde web-app te houden of wijzig dit in een andere unieke naam (geldige tekens zijn `a-z`, `0-9`, en `-`).</span><span class="sxs-lookup"><span data-stu-id="068c3-149">You can keep the generated web app name, or change it to another unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="068c3-150">De naam van de web-app wordt gebruikt als onderdeel van de standaard-URL voor uw app (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de naam van uw web-app).</span><span class="sxs-lookup"><span data-stu-id="068c3-150">The web app name is used as part of the default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="068c3-151">De naam van de web-app moet uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-151">The web app name needs to be unique across all apps in Azure.</span></span> 

![Het dialoogvenster app service maken](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="068c3-153">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="068c3-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="068c3-154">Klik naast **Resourcegroep** op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="068c3-154">Next to **Resource Group**, click **New**.</span></span>

![Naast de resourcegroep, klik op Nieuw.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="068c3-156">De resourcegroep een naam **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="068c3-156">Name the resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="068c3-157">Klik niet op **maken**.</span><span class="sxs-lookup"><span data-stu-id="068c3-157">Do not click **Create**.</span></span> <span data-ttu-id="068c3-158">U moet eerst een SQL-Database in een later stadium instellen.</span><span class="sxs-lookup"><span data-stu-id="068c3-158">You first need to set up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="068c3-159">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="068c3-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="068c3-160">Klik naast **App Service-plan** op **Nieuw**.</span><span class="sxs-lookup"><span data-stu-id="068c3-160">Next to **App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="068c3-161">Configureer in het dialoogvenster **App Service-plan configureren** het nieuwe App Service-plan met de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="068c3-161">In the **Configure App Service Plan** dialog, configure the new App Service plan with the following settings:</span></span>

![Een App Service-plan maken](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="068c3-163">Instelling</span><span class="sxs-lookup"><span data-stu-id="068c3-163">Setting</span></span>  | <span data-ttu-id="068c3-164">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="068c3-164">Suggested value</span></span> | <span data-ttu-id="068c3-165">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="068c3-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="068c3-166">**App Service-abonnement**</span><span class="sxs-lookup"><span data-stu-id="068c3-166">**App Service Plan**</span></span>| <span data-ttu-id="068c3-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="068c3-167">myAppServicePlan</span></span> | [<span data-ttu-id="068c3-168">App Service-abonnementen</span><span class="sxs-lookup"><span data-stu-id="068c3-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="068c3-169">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="068c3-169">**Location**</span></span>| <span data-ttu-id="068c3-170">West-Europa</span><span class="sxs-lookup"><span data-stu-id="068c3-170">West Europe</span></span> | [<span data-ttu-id="068c3-171">Azure-regio's</span><span class="sxs-lookup"><span data-stu-id="068c3-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="068c3-172">**Grootte**</span><span class="sxs-lookup"><span data-stu-id="068c3-172">**Size**</span></span>| <span data-ttu-id="068c3-173">Gratis</span><span class="sxs-lookup"><span data-stu-id="068c3-173">Free</span></span> | [<span data-ttu-id="068c3-174">Prijscategorieën</span><span class="sxs-lookup"><span data-stu-id="068c3-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="068c3-175">Maak een SQL Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="068c3-175">Create a SQL Server instance</span></span>

<span data-ttu-id="068c3-176">Voordat u een database maakt, moet u een [logische Azure SQL Database-server](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="068c3-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="068c3-177">Een logische server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="068c3-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="068c3-178">Selecteer **verkennen extra Azure-services**.</span><span class="sxs-lookup"><span data-stu-id="068c3-178">Select **Explore additional Azure services**.</span></span>

![Naam van web-app configureren](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="068c3-180">In de **Services** en klik op de  **+**  pictogram naast **SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="068c3-180">In the **Services** tab, click the **+** icon next to **SQL Database**.</span></span> 

![Klik op het tabblad Services op het pictogram naast SQL Database +.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="068c3-182">In de **SQL-Database configureren** dialoogvenster, klikt u op **nieuw** naast **SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="068c3-182">In the **Configure SQL Database** dialog, click **New** next to **SQL Server**.</span></span> 

<span data-ttu-id="068c3-183">Er wordt een unieke naam gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="068c3-183">A unique server name is generated.</span></span> <span data-ttu-id="068c3-184">Deze naam wordt gebruikt als onderdeel van de standaard-URL voor de logische server `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="068c3-184">This name is used as part of the default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="068c3-185">Het moet uniek zijn in alle exemplaren van logische server in Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="068c3-186">U kunt de servernaam van de wijzigen, maar de gegenereerde waarde voor deze zelfstudie te behouden.</span><span class="sxs-lookup"><span data-stu-id="068c3-186">You can change the server name, but for this tutorial, keep the generated value.</span></span>

<span data-ttu-id="068c3-187">Toevoegen van een gebruikersnaam voor de beheerder en het wachtwoord en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="068c3-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="068c3-188">Zie voor de vereisten voor wachtwoordcomplexiteit, [wachtwoordbeleid](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="068c3-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="068c3-189">Deze gebruikersnaam en wachtwoord onthouden.</span><span class="sxs-lookup"><span data-stu-id="068c3-189">Remember this username and password.</span></span> <span data-ttu-id="068c3-190">U moet ze voor het beheren van de logische server-exemplaar later.</span><span class="sxs-lookup"><span data-stu-id="068c3-190">You need them to manage the logical server instance later.</span></span>

![SQL Server-exemplaar maken](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="068c3-192">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="068c3-192">Create a SQL Database</span></span>

<span data-ttu-id="068c3-193">In de **SQL-Database configureren** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="068c3-193">In the **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="068c3-194">Gebruik de standaardwaarde gegenereerd **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="068c3-194">Keep the default generated **Database Name**.</span></span>
* <span data-ttu-id="068c3-195">In **Verbindingsreeksnaam**, type *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="068c3-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="068c3-196">Deze naam moet overeenkomen met de verbindingsreeks waarnaar wordt verwezen in *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="068c3-196">This name must match the connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="068c3-197">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="068c3-197">Select **OK**.</span></span>

![SQL-Database configureren](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="068c3-199">De **Create App Service** dialoogvenster resources weergegeven die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="068c3-199">The **Create App Service** dialog shows the resources you've created.</span></span> <span data-ttu-id="068c3-200">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="068c3-200">Click **Create**.</span></span> 

![de resources die u hebt gemaakt](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="068c3-202">Zodra de wizard is voltooid voor het maken van de Azure-resources, wordt uw ASP.NET-app gepubliceerd naar Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-202">Once the wizard finishes creating the Azure resources, it  publishes your ASP.NET app to Azure.</span></span> <span data-ttu-id="068c3-203">De standaardbrowser wordt gestart met de URL van de geïmplementeerde app.</span><span class="sxs-lookup"><span data-stu-id="068c3-203">Your default browser is launched with the URL to the deployed app.</span></span> 

<span data-ttu-id="068c3-204">Enkele taakitems toevoegen.</span><span class="sxs-lookup"><span data-stu-id="068c3-204">Add a few to-do items.</span></span>

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="068c3-206">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="068c3-206">Congratulations!</span></span> <span data-ttu-id="068c3-207">Uw ASP.NET-toepassing voor gegevensgestuurde wordt live in Azure App Service uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="068c3-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-the-sql-database-locally"></a><span data-ttu-id="068c3-208">Toegang tot de SQL-Database lokaal</span><span class="sxs-lookup"><span data-stu-id="068c3-208">Access the SQL Database locally</span></span>

<span data-ttu-id="068c3-209">Visual Studio kunt u bekijken en beheren van uw nieuwe SQL-Database eenvoudig in de **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-209">Visual Studio lets you explore and manage your new SQL Database easily in the **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="068c3-210">Een databaseverbinding maken</span><span class="sxs-lookup"><span data-stu-id="068c3-210">Create a database connection</span></span>

<span data-ttu-id="068c3-211">Van de **weergave** selecteert u **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-211">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="068c3-212">Aan de bovenkant van **SQL Server Object Explorer**, klikt u op de **SQL-Server toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="068c3-212">At the top of **SQL Server Object Explorer**, click the **Add SQL Server** button.</span></span>

### <a name="configure-the-database-connection"></a><span data-ttu-id="068c3-213">Verbinding met de database configureren</span><span class="sxs-lookup"><span data-stu-id="068c3-213">Configure the database connection</span></span>

<span data-ttu-id="068c3-214">In de **Connect** dialoogvenster, vouw de **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="068c3-214">In the **Connect** dialog, expand the **Azure** node.</span></span> <span data-ttu-id="068c3-215">Uw SQL-Database-exemplaren in Azure worden hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="068c3-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="068c3-216">Selecteer de `DotNetAppSqlDb` SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="068c3-216">Select the `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="068c3-217">De verbinding die u eerder hebt gemaakt, wordt automatisch gevuld onderaan.</span><span class="sxs-lookup"><span data-stu-id="068c3-217">The connection you created earlier is automatically filled at the bottom.</span></span>

<span data-ttu-id="068c3-218">Typ het wachtwoord van de databasebeheerder u eerder hebt gemaakt en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="068c3-218">Type the database administrator password you created earlier and click **Connect**.</span></span>

![Databaseverbinding vanuit Visual Studio configureren](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="068c3-220">Clientverbinding van uw computer toestaan</span><span class="sxs-lookup"><span data-stu-id="068c3-220">Allow client connection from your computer</span></span>

<span data-ttu-id="068c3-221">De **maken van een nieuwe firewallregel** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="068c3-221">The **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="068c3-222">Uw exemplaar van SQL-Database kunt standaard alleen verbindingen van Azure-services, zoals uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="068c3-223">Voor verbinding met uw database, een firewallregel in het exemplaar van SQL-Database te maken.</span><span class="sxs-lookup"><span data-stu-id="068c3-223">To connect to your database, create a firewall rule in the SQL Database instance.</span></span> <span data-ttu-id="068c3-224">De firewallregel kan het openbare IP-adres van uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="068c3-224">The firewall rule allows the public IP address of your local computer.</span></span>

<span data-ttu-id="068c3-225">Het dialoogvenster is al ingevuld met het openbare IP-adres van uw computer.</span><span class="sxs-lookup"><span data-stu-id="068c3-225">The dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="068c3-226">Zorg ervoor dat **mijn client-IP toevoegen** is geselecteerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="068c3-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Firewall voor SQL Database-instantie instellen](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="068c3-228">Zodra de Visual Studio is gemaakt van de firewallinstelling voor uw exemplaar van SQL-Database, de verbinding wordt weergegeven in **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-228">Once Visual Studio finishes creating the firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="068c3-229">Hier kunt u de meest voorkomende uitvoeren databasebewerkingen, zoals het uitvoeren van query's maken, weergaven en opgeslagen procedures en meer.</span><span class="sxs-lookup"><span data-stu-id="068c3-229">Here, you can perform the most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="068c3-230">Met de rechtermuisknop op de `Todoes` tabel en selecteer **weergavegegevens**.</span><span class="sxs-lookup"><span data-stu-id="068c3-230">Right-click on the `Todoes` table and select **View Data**.</span></span> 

![Objecten van de SQL-Database verkennen](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="068c3-232">App kunt bijwerken met Code First-migraties</span><span class="sxs-lookup"><span data-stu-id="068c3-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="068c3-233">U kunt de vertrouwde hulpprogramma's in Visual Studio gebruiken om bij te werken van uw database en web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-233">You can use the familiar tools in Visual Studio to update your database and web app in Azure.</span></span> <span data-ttu-id="068c3-234">In deze stap kunt u Code First-migraties in Entity Framework een wijziging aanbrengen in uw databaseschema en deze publiceren naar Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-234">In this step, you use Code First Migrations in Entity Framework to make a change to your database schema and publish it to Azure.</span></span>

<span data-ttu-id="068c3-235">Zie voor meer informatie over het gebruik van Entity Framework Code First-migraties [aan de slag met Entity Framework 6 Code First met MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="068c3-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="068c3-236">Uw gegevensmodel bijwerken</span><span class="sxs-lookup"><span data-stu-id="068c3-236">Update your data model</span></span>

<span data-ttu-id="068c3-237">Open _Models\Todo.cs_ code-editor.</span><span class="sxs-lookup"><span data-stu-id="068c3-237">Open _Models\Todo.cs_ in the code editor.</span></span> <span data-ttu-id="068c3-238">De volgende eigenschap toevoegen aan de `ToDo` klasse:</span><span class="sxs-lookup"><span data-stu-id="068c3-238">Add the following property to the `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="068c3-239">Code First-migraties lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="068c3-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="068c3-240">Voer enkele opdrachten om updates voor uw lokale database.</span><span class="sxs-lookup"><span data-stu-id="068c3-240">Run a few commands to make updates to your local database.</span></span> 

<span data-ttu-id="068c3-241">Van de **extra** menu, klikt u op **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="068c3-241">From the **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="068c3-242">Schakel in het venster Package Manager Console Code First-migraties:</span><span class="sxs-lookup"><span data-stu-id="068c3-242">In the Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="068c3-243">Toevoegen van een migratie:</span><span class="sxs-lookup"><span data-stu-id="068c3-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="068c3-244">De lokale database-update:</span><span class="sxs-lookup"><span data-stu-id="068c3-244">Update the local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="068c3-245">Type `Ctrl+F5` de app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="068c3-245">Type `Ctrl+F5` to run the app.</span></span> <span data-ttu-id="068c3-246">Test de bewerken, details en koppelingen maken.</span><span class="sxs-lookup"><span data-stu-id="068c3-246">Test the edit, details, and create links.</span></span>

<span data-ttu-id="068c3-247">Als de toepassing wordt geladen zonder fouten, is de Code First-migraties van voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="068c3-247">If the application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="068c3-248">Echter uw pagina nog steeds ziet er hetzelfde omdat uw toepassingslogica wordt deze nieuwe eigenschap niet nog gebruikt.</span><span class="sxs-lookup"><span data-stu-id="068c3-248">However, your page still looks the same because your application logic is not using this new property yet.</span></span> 

### <a name="use-the-new-property"></a><span data-ttu-id="068c3-249">De nieuwe eigenschap te gebruiken</span><span class="sxs-lookup"><span data-stu-id="068c3-249">Use the new property</span></span>

<span data-ttu-id="068c3-250">Enkele wijzigingen aanbrengen in uw code te gebruiken de `Done` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="068c3-250">Make some changes in your code to use the `Done` property.</span></span> <span data-ttu-id="068c3-251">Voor het gemak in deze zelfstudie alleen gaat u wijzigt de `Index` en `Create` weergaven om te zien van de eigenschap in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="068c3-251">For simplicity in this tutorial, you're only going to change the `Index` and `Create` views to see the property in action.</span></span>

<span data-ttu-id="068c3-252">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="068c3-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="068c3-253">Zoek de `Create()` methode en voeg `Done` aan de lijst met eigenschappen in de `Bind` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="068c3-253">Find the `Create()` method and add `Done` to the list of properties in the `Bind` attribute.</span></span> <span data-ttu-id="068c3-254">Wanneer u bent klaar, uw `Create()` methodehandtekening lijkt op de volgende code:</span><span class="sxs-lookup"><span data-stu-id="068c3-254">When you're done, your `Create()` method signature looks like the following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="068c3-255">Open _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="068c3-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="068c3-256">In de code Razor ziet u een `<div class="form-group">` element die gebruikmaakt van `model.Description`, en vervolgens een andere `<div class="form-group">` element die gebruikmaakt van `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="068c3-256">In the Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="068c3-257">Direct na deze twee elementen toevoegen `<div class="form-group">` element die gebruikmaakt van `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="068c3-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

```csharp
<div class="form-group">
    @Html.LabelFor(model => model.Done, htmlAttributes: new { @class = "control-label col-md-2" })
    <div class="col-md-10">
        <div class="checkbox">
            @Html.EditorFor(model => model.Done)
            @Html.ValidationMessageFor(model => model.Done, "", new { @class = "text-danger" })
        </div>
    </div>
</div>
```

<span data-ttu-id="068c3-258">Open _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="068c3-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="068c3-259">Zoeken naar de lege `<th></th>` element.</span><span class="sxs-lookup"><span data-stu-id="068c3-259">Search for the empty `<th></th>` element.</span></span> <span data-ttu-id="068c3-260">Voeg de volgende Razor-code net boven dit element:</span><span class="sxs-lookup"><span data-stu-id="068c3-260">Just above this element, add the following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="068c3-261">Zoek de `<td>` element met de `Html.ActionLink()` Help-methoden.</span><span class="sxs-lookup"><span data-stu-id="068c3-261">Find the `<td>` element that contains the `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="068c3-262">Voeg de volgende Razor-code net boven dit element:</span><span class="sxs-lookup"><span data-stu-id="068c3-262">Just above this element, add the following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="068c3-263">Dit is alles wat u wilt zien van de wijzigingen in de `Index` en `Create` weergaven.</span><span class="sxs-lookup"><span data-stu-id="068c3-263">That's all you need to see the changes in the `Index` and `Create` views.</span></span> 

<span data-ttu-id="068c3-264">Type `Ctrl+F5` de app uitvoert.</span><span class="sxs-lookup"><span data-stu-id="068c3-264">Type `Ctrl+F5` to run the app.</span></span>

<span data-ttu-id="068c3-265">U kunt nu een taakitem toegevoegd en controleer of **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="068c3-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="068c3-266">Vervolgens moet het weergegeven in uw startpagina als een item voltooid.</span><span class="sxs-lookup"><span data-stu-id="068c3-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="068c3-267">Houd er rekening mee dat de `Edit` weergave niet de `Done` veld, omdat u niet wijzigen de `Edit` weergeven.</span><span class="sxs-lookup"><span data-stu-id="068c3-267">Remember that the `Edit` view doesn't show the `Done` field, because you didn't change the `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="068c3-268">Code First-migraties in Azure inschakelen</span><span class="sxs-lookup"><span data-stu-id="068c3-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="068c3-269">Nu dat uw code wijzigen werkt, met inbegrip van de database wilt migreren, moet u deze publiceren naar uw Azure-web-app en uw SQL-Database te werken met Code First-migraties.</span><span class="sxs-lookup"><span data-stu-id="068c3-269">Now that your code change works, including database migration, you publish it to your Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="068c3-270">Net zoals, met de rechtermuisknop op uw project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="068c3-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="068c3-271">Klik op **instellingen** om de wizard publish te openen.</span><span class="sxs-lookup"><span data-stu-id="068c3-271">Click **Settings** to open the publish wizard.</span></span>

![Open publicatie-instellingen](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="068c3-273">Klik in de wizard op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="068c3-273">In the wizard, click **Next**.</span></span>

<span data-ttu-id="068c3-274">Zorg ervoor dat de verbindingsreeks voor de SQL-Database is gevuld **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="068c3-274">Make sure that the connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="068c3-275">Mogelijk moet u selecteert de **myToDoAppDb** database uit de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="068c3-275">You may need to select the **myToDoAppDb** database from the dropdown.</span></span> 

<span data-ttu-id="068c3-276">Selecteer **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**, klikt u vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="068c3-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Code First-migraties inschakelen in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="068c3-278">Uw wijzigingen publiceren</span><span class="sxs-lookup"><span data-stu-id="068c3-278">Publish your changes</span></span>

<span data-ttu-id="068c3-279">Nu dat u Code First-migraties in uw Azure-web-app hebt ingeschakeld, moet u uw codewijzigingen publiceren.</span><span class="sxs-lookup"><span data-stu-id="068c3-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="068c3-280">Klik op de publicatiepagina op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="068c3-280">In the publish page, click **Publish**.</span></span>

<span data-ttu-id="068c3-281">Selecteer en probeer het opnieuw toe te voegen taakitems **gedaan**, en ze moeten worden weergegeven in uw startpagina als een item voltooid.</span><span class="sxs-lookup"><span data-stu-id="068c3-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Azure-web-app na de eerste Code-migratie](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="068c3-283">Uw bestaande taakitems nog steeds worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="068c3-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="068c3-284">Wanneer u uw ASP.NET-toepassing opnieuw publiceren, is er geen bestaande gegevens in de SQL-Database verloren.</span><span class="sxs-lookup"><span data-stu-id="068c3-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="068c3-285">Bovendien Code First-migraties alleen het schema van de wijzigingen en laat uw bestaande gegevens intact.</span><span class="sxs-lookup"><span data-stu-id="068c3-285">Also, Code First Migrations only changes the data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="068c3-286">Toepassingslogboeken Stream</span><span class="sxs-lookup"><span data-stu-id="068c3-286">Stream application logs</span></span>

<span data-ttu-id="068c3-287">U kunt tracering berichten streamen rechtstreeks vanuit uw Azure-web-app met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="068c3-287">You can stream tracing messages directly from your Azure web app to Visual Studio.</span></span>

<span data-ttu-id="068c3-288">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="068c3-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="068c3-289">Elke actie begint met een `Trace.WriteLine()` methode.</span><span class="sxs-lookup"><span data-stu-id="068c3-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="068c3-290">Deze code wordt toegevoegd aan hoe u traceringsberichten toevoegen aan uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-290">This code is added to show you how to add trace messages to your Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="068c3-291">Open Server Explorer</span><span class="sxs-lookup"><span data-stu-id="068c3-291">Open Server Explorer</span></span>

<span data-ttu-id="068c3-292">Van de **weergave** selecteert u **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-292">From the **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="068c3-293">U kunt logboekregistratie configureren voor uw Azure-web-app in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="068c3-294">Streaming-logboek inschakelen</span><span class="sxs-lookup"><span data-stu-id="068c3-294">Enable log streaming</span></span>

<span data-ttu-id="068c3-295">In **Server Explorer**, vouw **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="068c3-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="068c3-296">Vouw de **myResourceGroup** resourcegroep, u hebt gemaakt tijdens het maken van de Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-296">Expand the **myResourceGroup** resource group, you created when you first created the Azure web app.</span></span>

<span data-ttu-id="068c3-297">Met de rechtermuisknop op uw Azure-web-app en selecteer **Streaming logboeken bekijken**.</span><span class="sxs-lookup"><span data-stu-id="068c3-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Streaming-logboek inschakelen](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="068c3-299">De logboeken worden nu gestreamd naar de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="068c3-299">The logs are now streamed into the **Output** window.</span></span> 

![In het uitvoervenster streaming logboek](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="068c3-301">Echter, u Zie geen berichten traceren nog.</span><span class="sxs-lookup"><span data-stu-id="068c3-301">However, you don't see any of the trace messages yet.</span></span> <span data-ttu-id="068c3-302">Dat omdat wanneer u eerst selecteert **Streaming logboeken bekijken**, stelt uw Azure-web-app van de tracering naar `Error`, die alleen legt foutgebeurtenissen vast in (met de `Trace.TraceError()` methode).</span><span class="sxs-lookup"><span data-stu-id="068c3-302">That's because when you first select **View Streaming Logs**, your Azure web app sets the trace level to `Error`, which only logs error events (with the `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="068c3-303">De traceringsniveaus wijzigen</span><span class="sxs-lookup"><span data-stu-id="068c3-303">Change trace levels</span></span>

<span data-ttu-id="068c3-304">Als u wilt wijzigen van de traceringsniveaus voor andere traceringsberichten uitvoeren, gaat u terug naar **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="068c3-304">To change the trace levels to output other trace messages, go back to **Server Explorer**.</span></span>

<span data-ttu-id="068c3-305">Opnieuw met de rechtermuisknop op uw Azure-web-app en selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="068c3-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="068c3-306">In de **toepassingslogboeken (bestandssysteem)** vervolgkeuzelijst **uitgebreid**.</span><span class="sxs-lookup"><span data-stu-id="068c3-306">In the **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="068c3-307">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="068c3-307">Click **Save**.</span></span>

![Wijzig het traceringsniveau in uitgebreid](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="068c3-309">U kunt experimenteren met verschillende traceringsniveaus om te zien welke typen berichten worden weergegeven voor elk bedreigingsniveau.</span><span class="sxs-lookup"><span data-stu-id="068c3-309">You can experiment with different trace levels to see what types of messages are displayed for each level.</span></span> <span data-ttu-id="068c3-310">Bijvoorbeeld, de **informatie** niveau omvat alle logboeken die zijn gemaakt door `Trace.TraceInformation()`, `Trace.TraceWarning()`, en `Trace.TraceError()`, maar niet de logboeken die zijn gemaakt door `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="068c3-310">For example, the **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="068c3-311">In uw browser probeert op te klikken om de toepassing van de lijst met taken in Azure.</span><span class="sxs-lookup"><span data-stu-id="068c3-311">In your browser, try clicking around the to-do list application in Azure.</span></span> <span data-ttu-id="068c3-312">Nu de traceringsberichten worden gestreamd naar de **uitvoer** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="068c3-312">The trace messages are now streamed to the **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="068c3-313">Logboek streaming stoppen</span><span class="sxs-lookup"><span data-stu-id="068c3-313">Stop log streaming</span></span>

<span data-ttu-id="068c3-314">Als u wilt de streaming-log service stopt, klikt u op de **bewaking stopt** knop in de **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="068c3-314">To stop the log-streaming service, click the **Stop monitoring** button in the **Output** window.</span></span>

![Logboek streaming stoppen](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="068c3-316">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="068c3-316">Manage your Azure web app</span></span>

<span data-ttu-id="068c3-317">Ga naar de [Azure-portal](https://portal.azure.com) om te zien van de web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="068c3-317">Go to the [Azure portal](https://portal.azure.com) to see the web app you created.</span></span> 



<span data-ttu-id="068c3-318">Klik vanuit het linkermenu op **App Service** en klik op de naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-318">From the left menu, click **App Service**, then click the name of your Azure web app.</span></span>

![Navigatie in de portal naar de Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="068c3-320">U bevindt zich in uw web-app-pagina.</span><span class="sxs-lookup"><span data-stu-id="068c3-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="068c3-321">Standaard ziet u de portal de **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="068c3-321">By default, the portal shows the **Overview** page.</span></span> <span data-ttu-id="068c3-322">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="068c3-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="068c3-323">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="068c3-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="068c3-324">De tabbladen aan de linkerkant van de pagina's worden weergegeven de andere configuratie dat kunt u openen.</span><span class="sxs-lookup"><span data-stu-id="068c3-324">The tabs on the left side of the page show the different configuration pages you can open.</span></span> 

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="068c3-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="068c3-326">Next steps</span></span>

<span data-ttu-id="068c3-327">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="068c3-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="068c3-328">Maken van een SQL-Database in Azure</span><span class="sxs-lookup"><span data-stu-id="068c3-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="068c3-329">Een ASP.NET-app verbinden met SQL Database</span><span class="sxs-lookup"><span data-stu-id="068c3-329">Connect an ASP.NET app to SQL Database</span></span>
> * <span data-ttu-id="068c3-330">De app implementeren in Azure</span><span class="sxs-lookup"><span data-stu-id="068c3-330">Deploy the app to Azure</span></span>
> * <span data-ttu-id="068c3-331">Bijwerken van het gegevensmodel en de app implementeren</span><span class="sxs-lookup"><span data-stu-id="068c3-331">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="068c3-332">Logboeken van de stroom van Azure naar uw terminal</span><span class="sxs-lookup"><span data-stu-id="068c3-332">Stream logs from Azure to your terminal</span></span>
> * <span data-ttu-id="068c3-333">De app in de Azure portal beheren</span><span class="sxs-lookup"><span data-stu-id="068c3-333">Manage the app in the Azure portal</span></span>

<span data-ttu-id="068c3-334">Ga naar de volgende zelfstudie voor meer informatie over hoe u een aangepaste DNS-naam toegewezen aan de web-app.</span><span class="sxs-lookup"><span data-stu-id="068c3-334">Advance to the next tutorial to learn how to map a custom DNS name to the web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="068c3-335">Een bestaande aangepaste DNS-naam toewijzen aan Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="068c3-335">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
