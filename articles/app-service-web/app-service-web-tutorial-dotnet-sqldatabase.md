---
title: een ASP.NET-app in Azure met SQL-Database aaaBuild | Microsoft Docs
description: Meer informatie over hoe een ASP.NET-tooget app in Azure, werken met verbinding tooa SQL-Database.
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
ms.openlocfilehash: d21c2bc404bfe038608c17e5a94d96847153002c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-aspnet-app-in-azure-with-sql-database"></a><span data-ttu-id="799ae-103">Een ASP.NET-app in Azure met SQL-Database maken</span><span class="sxs-lookup"><span data-stu-id="799ae-103">Build an ASP.NET app in Azure with SQL Database</span></span>

<span data-ttu-id="799ae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) biedt een uiterst schaalbare webhostingservice met self-patchfunctie.</span><span class="sxs-lookup"><span data-stu-id="799ae-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="799ae-105">Deze zelfstudie leert u hoe toodeploy een gegevensgestuurde ASP.NET web-app in Azure en te verbinden[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span><span class="sxs-lookup"><span data-stu-id="799ae-105">This tutorial shows you how toodeploy a data-driven ASP.NET web app in Azure and connect it too[Azure SQL Database](../sql-database/sql-database-technical-overview.md).</span></span> <span data-ttu-id="799ae-106">Wanneer u klaar bent, hebt u een ASP.NET-app uitgevoerd in de [Azure App Service](../app-service/app-service-value-prop-what-is.md) en tooSQL Database verbonden.</span><span class="sxs-lookup"><span data-stu-id="799ae-106">When you're finished, you have a ASP.NET app running in [Azure App Service](../app-service/app-service-value-prop-what-is.md) and connected tooSQL Database.</span></span>

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="799ae-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="799ae-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="799ae-109">Maken van een SQL-Database in Azure</span><span class="sxs-lookup"><span data-stu-id="799ae-109">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="799ae-110">Verbinding maken met een ASP.NET-app tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="799ae-110">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="799ae-111">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="799ae-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="799ae-112">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="799ae-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="799ae-113">Logboeken van de stroom van Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="799ae-113">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="799ae-114">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="799ae-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="799ae-115">Vereisten</span><span class="sxs-lookup"><span data-stu-id="799ae-115">Prerequisites</span></span>

<span data-ttu-id="799ae-116">toocomplete in deze zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="799ae-116">toocomplete this tutorial:</span></span>

* <span data-ttu-id="799ae-117">Installeer [Visual Studio 2017](https://www.visualstudio.com/downloads/) Hello werkbelastingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="799ae-117">Install [Visual Studio 2017](https://www.visualstudio.com/downloads/) with hello following workloads:</span></span>
  - <span data-ttu-id="799ae-118">**ASP.NET- en web-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="799ae-118">**ASP.NET and web development**</span></span>
  - <span data-ttu-id="799ae-119">**Azure-ontwikkeling**</span><span class="sxs-lookup"><span data-stu-id="799ae-119">**Azure development**</span></span>

  ![ASP.NET- en web-ontwikkeling en Azure-ontwikkeling (onder Web en cloud)](media/app-service-web-tutorial-dotnet-sqldatabase/workloads.png)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="799ae-121">Hallo voorbeeld downloaden</span><span class="sxs-lookup"><span data-stu-id="799ae-121">Download hello sample</span></span>

<span data-ttu-id="799ae-122">[Hallo-voorbeeldproject downloaden](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="799ae-122">[Download hello sample project](https://github.com/Azure-Samples/dotnet-sqldb-tutorial/archive/master.zip).</span></span>

<span data-ttu-id="799ae-123">Pak (uitpakken) Hallo *dotnet-sqldb-zelfstudie-master.zip* bestand.</span><span class="sxs-lookup"><span data-stu-id="799ae-123">Extract (unzip) hello  *dotnet-sqldb-tutorial-master.zip* file.</span></span>

<span data-ttu-id="799ae-124">Hallo-voorbeeldproject bevat een eenvoudige [ASP.NET MVC](https://www.asp.net/mvc) CRUD (maken-lezen-update-verwijderen) met behulp van app [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="799ae-124">hello sample project contains a basic [ASP.NET MVC](https://www.asp.net/mvc) CRUD (create-read-update-delete) app using [Entity Framework Code First](/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="run-hello-app"></a><span data-ttu-id="799ae-125">Hallo-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="799ae-125">Run hello app</span></span>

<span data-ttu-id="799ae-126">Open Hallo *dotnet-sqldb-zelfstudie-master/DotNetAppSqlDb.sln* bestand in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="799ae-126">Open hello *dotnet-sqldb-tutorial-master/DotNetAppSqlDb.sln* file in Visual Studio.</span></span> 

<span data-ttu-id="799ae-127">Type `Ctrl+F5` toorun Hallo app zonder foutopsporing.</span><span class="sxs-lookup"><span data-stu-id="799ae-127">Type `Ctrl+F5` toorun hello app without debugging.</span></span> <span data-ttu-id="799ae-128">Hallo-app wordt weergegeven in de browser.</span><span class="sxs-lookup"><span data-stu-id="799ae-128">hello app is displayed in your default browser.</span></span> <span data-ttu-id="799ae-129">Selecteer Hallo **nieuw** koppelen en maken van een paar *taak* items.</span><span class="sxs-lookup"><span data-stu-id="799ae-129">Select hello **Create New** link and create a couple *to-do* items.</span></span> 

![Het dialoogvenster Nieuw ASP.NET-project](media/app-service-web-tutorial-dotnet-sqldatabase/local-app-in-browser.png)

<span data-ttu-id="799ae-131">Test Hallo **bewerken**, **Details**, en **verwijderen** koppelingen.</span><span class="sxs-lookup"><span data-stu-id="799ae-131">Test hello **Edit**, **Details**, and **Delete** links.</span></span>

<span data-ttu-id="799ae-132">Hallo app gebruikmaakt van een database context tooconnect met Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="799ae-132">hello app uses a database context tooconnect with hello database.</span></span> <span data-ttu-id="799ae-133">In dit voorbeeld wordt de databasecontext Hallo maakt gebruik van een verbindingsreeks met de naam `MyDbConnection`.</span><span class="sxs-lookup"><span data-stu-id="799ae-133">In this sample, hello database context uses a connection string named `MyDbConnection`.</span></span> <span data-ttu-id="799ae-134">Hallo-verbindingsreeks is ingesteld in Hallo *Web.config* bestands- en waarnaar wordt verwezen in Hallo *Models/MyDatabaseContext.cs* bestand.</span><span class="sxs-lookup"><span data-stu-id="799ae-134">hello connection string is set in hello *Web.config* file and referenced in hello *Models/MyDatabaseContext.cs* file.</span></span> <span data-ttu-id="799ae-135">naam van verbindingsreeks Hello wordt later in Hallo zelfstudie tooconnect hello Azure-web-app tooan Azure SQL Database gebruikt.</span><span class="sxs-lookup"><span data-stu-id="799ae-135">hello connection string name is used later in hello tutorial tooconnect hello Azure web app tooan Azure SQL Database.</span></span> 

## <a name="publish-tooazure-with-sql-database"></a><span data-ttu-id="799ae-136">TooAzure met SQL Database publiceren</span><span class="sxs-lookup"><span data-stu-id="799ae-136">Publish tooAzure with SQL Database</span></span>

<span data-ttu-id="799ae-137">In Hallo **Solution Explorer**, met de rechtermuisknop op uw **DotNetAppSqlDb** project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="799ae-137">In hello **Solution Explorer**, right-click your **DotNetAppSqlDb** project and select **Publish**.</span></span>

![Publiceren vanuit Solution Explorer](./media/app-service-web-tutorial-dotnet-sqldatabase/solution-explorer-publish.png)

<span data-ttu-id="799ae-139">Zorg ervoor dat **Microsoft Azure App Service** is geselecteerd en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="799ae-139">Make sure that **Microsoft Azure App Service** is selected and click **Publish**.</span></span>

![Publiceren vanaf de projectoverzichtspagina](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-to-app-service.png)

<span data-ttu-id="799ae-141">Publicatie wordt geopend Hallo **Create App Service** dialoogvenster waarmee u alle hello Azure-resources u toorun moet uw ASP.NET-web-app in Azure.</span><span class="sxs-lookup"><span data-stu-id="799ae-141">Publishing opens hello **Create App Service** dialog, which helps you create all hello Azure resources you need toorun your ASP.NET web app in Azure.</span></span>

### <a name="sign-in-tooazure"></a><span data-ttu-id="799ae-142">Meld u aan tooAzure</span><span class="sxs-lookup"><span data-stu-id="799ae-142">Sign in tooAzure</span></span>

<span data-ttu-id="799ae-143">In Hallo **Create App Service** dialoogvenster, klikt u op **account toevoegen**, en vervolgens weer aanmelden tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="799ae-143">In hello **Create App Service** dialog, click **Add an account**, and then sign in tooyour Azure subscription.</span></span> <span data-ttu-id="799ae-144">Als u al bent aangemeld bij een Microsoft-account, moet u ervoor zorgen dat dit account uw Azure-abonnement bevat.</span><span class="sxs-lookup"><span data-stu-id="799ae-144">If you're already signed into a Microsoft account, make sure that account holds your Azure subscription.</span></span> <span data-ttu-id="799ae-145">Als Hallo ondertekend in Microsoft-account niet uw Azure-abonnement hebt, klikt u erop tooadd Hallo juiste account.</span><span class="sxs-lookup"><span data-stu-id="799ae-145">If hello signed-in Microsoft account doesn't have your Azure subscription, click it tooadd hello correct account.</span></span>
   
![Meld u aan tooAzure](./media/app-service-web-tutorial-dotnet-sqldatabase/sign-in-azure.png)

<span data-ttu-id="799ae-147">Nadat u bent aangemeld, bent u klaar toocreate die alle bronnen die u nodig hebt voor uw Azure-web-app in dit dialoogvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="799ae-147">Once signed in, you're ready toocreate all hello resources you need for your Azure web app in this dialog.</span></span>

### <a name="configure-hello-web-app-name"></a><span data-ttu-id="799ae-148">Hallo web-appnaam configureren</span><span class="sxs-lookup"><span data-stu-id="799ae-148">Configure hello web app name</span></span>

<span data-ttu-id="799ae-149">Hallo gegenereerd web-appnaam behouden of deze tooanother unieke naam wijzigen (geldige tekens zijn `a-z`, `0-9`, en `-`).</span><span class="sxs-lookup"><span data-stu-id="799ae-149">You can keep hello generated web app name, or change it tooanother unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="799ae-150">Hallo web-appnaam wordt gebruikt als onderdeel van Hallo standaard-URL voor uw app (`<app_name>.azurewebsites.net`, waarbij `<app_name>` is de naam van uw web-app).</span><span class="sxs-lookup"><span data-stu-id="799ae-150">hello web app name is used as part of hello default URL for your app (`<app_name>.azurewebsites.net`, where `<app_name>` is your web app name).</span></span> <span data-ttu-id="799ae-151">Hallo web-appnaam moet toobe uniek zijn in alle apps in Azure.</span><span class="sxs-lookup"><span data-stu-id="799ae-151">hello web app name needs toobe unique across all apps in Azure.</span></span> 

![Het dialoogvenster app service maken](media/app-service-web-tutorial-dotnet-sqldatabase/wan.png)

### <a name="create-a-resource-group"></a><span data-ttu-id="799ae-153">Een resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="799ae-153">Create a resource group</span></span>

[!INCLUDE [resource-group](../../includes/resource-group.md)]

<span data-ttu-id="799ae-154">Volgende te**resourcegroep**, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="799ae-154">Next too**Resource Group**, click **New**.</span></span>

![Volgende tooResource groep, klikt u op Nieuw.](media/app-service-web-tutorial-dotnet-sqldatabase/new_rg2.png)

<span data-ttu-id="799ae-156">Naam Hallo resourcegroep **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="799ae-156">Name hello resource group **myResourceGroup**.</span></span>

> [!NOTE]
> <span data-ttu-id="799ae-157">Klik niet op **maken**.</span><span class="sxs-lookup"><span data-stu-id="799ae-157">Do not click **Create**.</span></span> <span data-ttu-id="799ae-158">U moet eerst tooset van een SQL-Database in een later stadium.</span><span class="sxs-lookup"><span data-stu-id="799ae-158">You first need tooset up a SQL Database in a later step.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="799ae-159">Een App Service-plan maken</span><span class="sxs-lookup"><span data-stu-id="799ae-159">Create an App Service plan</span></span>

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="799ae-160">Volgende te**App Service-Plan**, klikt u op **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="799ae-160">Next too**App Service Plan**, click **New**.</span></span> 

<span data-ttu-id="799ae-161">In Hallo **App Service-Plan configureren** dialoogvenster Hallo nieuwe App Service-abonnement met Hallo volgende instellingen configureren:</span><span class="sxs-lookup"><span data-stu-id="799ae-161">In hello **Configure App Service Plan** dialog, configure hello new App Service plan with hello following settings:</span></span>

![Een App Service-plan maken](./media/app-service-web-tutorial-dotnet-sqldatabase/configure-app-service-plan.png)

| <span data-ttu-id="799ae-163">Instelling</span><span class="sxs-lookup"><span data-stu-id="799ae-163">Setting</span></span>  | <span data-ttu-id="799ae-164">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="799ae-164">Suggested value</span></span> | <span data-ttu-id="799ae-165">Voor meer informatie</span><span class="sxs-lookup"><span data-stu-id="799ae-165">For more information</span></span> |
| ----------------- | ------------ | ----|
|<span data-ttu-id="799ae-166">**App Service-abonnement**</span><span class="sxs-lookup"><span data-stu-id="799ae-166">**App Service Plan**</span></span>| <span data-ttu-id="799ae-167">myAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="799ae-167">myAppServicePlan</span></span> | [<span data-ttu-id="799ae-168">App Service-abonnementen</span><span class="sxs-lookup"><span data-stu-id="799ae-168">App Service plans</span></span>](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) |
|<span data-ttu-id="799ae-169">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="799ae-169">**Location**</span></span>| <span data-ttu-id="799ae-170">West-Europa</span><span class="sxs-lookup"><span data-stu-id="799ae-170">West Europe</span></span> | [<span data-ttu-id="799ae-171">Azure-regio's</span><span class="sxs-lookup"><span data-stu-id="799ae-171">Azure regions</span></span>](https://azure.microsoft.com/regions/) |
|<span data-ttu-id="799ae-172">**Grootte**</span><span class="sxs-lookup"><span data-stu-id="799ae-172">**Size**</span></span>| <span data-ttu-id="799ae-173">Gratis</span><span class="sxs-lookup"><span data-stu-id="799ae-173">Free</span></span> | [<span data-ttu-id="799ae-174">Prijscategorieën</span><span class="sxs-lookup"><span data-stu-id="799ae-174">Pricing tiers</span></span>](https://azure.microsoft.com/pricing/details/app-service/)|

### <a name="create-a-sql-server-instance"></a><span data-ttu-id="799ae-175">Maak een SQL Server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="799ae-175">Create a SQL Server instance</span></span>

<span data-ttu-id="799ae-176">Voordat u een database maakt, moet u een [logische Azure SQL Database-server](../sql-database/sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="799ae-176">Before creating a database, you need an [Azure SQL Database logical server](../sql-database/sql-database-features.md).</span></span> <span data-ttu-id="799ae-177">Een logische server bevat een groep met databases die worden beheerd als groep.</span><span class="sxs-lookup"><span data-stu-id="799ae-177">A logical server contains a group of databases managed as a group.</span></span>

<span data-ttu-id="799ae-178">Selecteer **verkennen extra Azure-services**.</span><span class="sxs-lookup"><span data-stu-id="799ae-178">Select **Explore additional Azure services**.</span></span>

![Naam van web-app configureren](media/app-service-web-tutorial-dotnet-sqldatabase/web-app-name.png)

<span data-ttu-id="799ae-180">In Hallo **Services** en klik op Hallo  **+**  pictogram volgende te**SQL-Database**.</span><span class="sxs-lookup"><span data-stu-id="799ae-180">In hello **Services** tab, click hello **+** icon next too**SQL Database**.</span></span> 

![Hallo-Services op het tabblad pictogram + Hallo volgende tooSQL Database.](media/app-service-web-tutorial-dotnet-sqldatabase/sql.png)

<span data-ttu-id="799ae-182">In Hallo **SQL-Database configureren** dialoogvenster, klikt u op **nieuw** volgende te**SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="799ae-182">In hello **Configure SQL Database** dialog, click **New** next too**SQL Server**.</span></span> 

<span data-ttu-id="799ae-183">Er wordt een unieke naam gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="799ae-183">A unique server name is generated.</span></span> <span data-ttu-id="799ae-184">Deze naam wordt gebruikt als onderdeel van Hallo standaard-URL voor de logische server `<server_name>.database.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="799ae-184">This name is used as part of hello default URL for your logical server, `<server_name>.database.windows.net`.</span></span> <span data-ttu-id="799ae-185">Het moet uniek zijn in alle exemplaren van logische server in Azure.</span><span class="sxs-lookup"><span data-stu-id="799ae-185">It must be unique across all logical server instances in Azure.</span></span> <span data-ttu-id="799ae-186">U kunt Hallo servernaam wijzigen, maar voor deze zelfstudie Hallo gegenereerde waarde behouden.</span><span class="sxs-lookup"><span data-stu-id="799ae-186">You can change hello server name, but for this tutorial, keep hello generated value.</span></span>

<span data-ttu-id="799ae-187">Toevoegen van een gebruikersnaam voor de beheerder en het wachtwoord en selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="799ae-187">Add an administrator username and password, and then select **OK**.</span></span> <span data-ttu-id="799ae-188">Zie voor de vereisten voor wachtwoordcomplexiteit, [wachtwoordbeleid](/sql/relational-databases/security/password-policy).</span><span class="sxs-lookup"><span data-stu-id="799ae-188">For password complexity requirements, see [Password Policy](/sql/relational-databases/security/password-policy).</span></span>

<span data-ttu-id="799ae-189">Deze gebruikersnaam en wachtwoord onthouden.</span><span class="sxs-lookup"><span data-stu-id="799ae-189">Remember this username and password.</span></span> <span data-ttu-id="799ae-190">U moet ze toomanage Hallo logische server later-instantie.</span><span class="sxs-lookup"><span data-stu-id="799ae-190">You need them toomanage hello logical server instance later.</span></span>

![SQL Server-exemplaar maken](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database-server.png)

### <a name="create-a-sql-database"></a><span data-ttu-id="799ae-192">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="799ae-192">Create a SQL Database</span></span>

<span data-ttu-id="799ae-193">In Hallo **SQL-Database configureren** dialoogvenster:</span><span class="sxs-lookup"><span data-stu-id="799ae-193">In hello **Configure SQL Database** dialog:</span></span> 

* <span data-ttu-id="799ae-194">Hallo standaard gegenereerde houden **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="799ae-194">Keep hello default generated **Database Name**.</span></span>
* <span data-ttu-id="799ae-195">In **Verbindingsreeksnaam**, type *MyDbConnection*.</span><span class="sxs-lookup"><span data-stu-id="799ae-195">In **Connection String Name**, type *MyDbConnection*.</span></span> <span data-ttu-id="799ae-196">Deze naam moet overeenkomen met de verbindingsreeks Hallo waarnaar wordt verwezen in *Models/MyDatabaseContext.cs*.</span><span class="sxs-lookup"><span data-stu-id="799ae-196">This name must match hello connection string that is referenced in *Models/MyDatabaseContext.cs*.</span></span>
* <span data-ttu-id="799ae-197">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="799ae-197">Select **OK**.</span></span>

![SQL-Database configureren](media/app-service-web-tutorial-dotnet-sqldatabase/configure-sql-database.png)

<span data-ttu-id="799ae-199">Hallo **Create App Service** dialoogvenster Hallo resources weergegeven die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="799ae-199">hello **Create App Service** dialog shows hello resources you've created.</span></span> <span data-ttu-id="799ae-200">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="799ae-200">Click **Create**.</span></span> 

![Hallo-resources die u hebt gemaakt](media/app-service-web-tutorial-dotnet-sqldatabase/app_svc_plan_done.png)

<span data-ttu-id="799ae-202">Zodra het Hallo-wizard is voltooid hello Azure-resources maken, wordt uw ASP.NET-app tooAzure gepubliceerd.</span><span class="sxs-lookup"><span data-stu-id="799ae-202">Once hello wizard finishes creating hello Azure resources, it  publishes your ASP.NET app tooAzure.</span></span> <span data-ttu-id="799ae-203">De standaardbrowser wordt gestart met Hallo URL toohello geïmplementeerd app.</span><span class="sxs-lookup"><span data-stu-id="799ae-203">Your default browser is launched with hello URL toohello deployed app.</span></span> 

<span data-ttu-id="799ae-204">Enkele taakitems toevoegen.</span><span class="sxs-lookup"><span data-stu-id="799ae-204">Add a few to-do items.</span></span>

![Gepubliceerde ASP.NET-toepassing in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/azure-app-in-browser.png)

<span data-ttu-id="799ae-206">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="799ae-206">Congratulations!</span></span> <span data-ttu-id="799ae-207">Uw ASP.NET-toepassing voor gegevensgestuurde wordt live in Azure App Service uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="799ae-207">Your data-driven ASP.NET application is running live in Azure App Service.</span></span>

## <a name="access-hello-sql-database-locally"></a><span data-ttu-id="799ae-208">Toegang tot lokaal Hallo SQL-Database</span><span class="sxs-lookup"><span data-stu-id="799ae-208">Access hello SQL Database locally</span></span>

<span data-ttu-id="799ae-209">Visual Studio kunt u bekijken en beheren van uw nieuwe SQL-Database eenvoudig in Hallo **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-209">Visual Studio lets you explore and manage your new SQL Database easily in hello **SQL Server Object Explorer**.</span></span>

### <a name="create-a-database-connection"></a><span data-ttu-id="799ae-210">Een databaseverbinding maken</span><span class="sxs-lookup"><span data-stu-id="799ae-210">Create a database connection</span></span>

<span data-ttu-id="799ae-211">Van Hallo **weergave** selecteert u **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-211">From hello **View** menu, select **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="799ae-212">Hallo boven aan het **SQL Server Object Explorer**, klikt u op Hallo **SQL-Server toevoegen** knop.</span><span class="sxs-lookup"><span data-stu-id="799ae-212">At hello top of **SQL Server Object Explorer**, click hello **Add SQL Server** button.</span></span>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="799ae-213">Hallo-databaseverbinding configureren</span><span class="sxs-lookup"><span data-stu-id="799ae-213">Configure hello database connection</span></span>

<span data-ttu-id="799ae-214">In Hallo **Connect** dialoogvenster Vouw Hallo **Azure** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="799ae-214">In hello **Connect** dialog, expand hello **Azure** node.</span></span> <span data-ttu-id="799ae-215">Uw SQL-Database-exemplaren in Azure worden hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="799ae-215">All your SQL Database instances in Azure are listed here.</span></span>

<span data-ttu-id="799ae-216">Selecteer Hallo `DotNetAppSqlDb` SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="799ae-216">Select hello `DotNetAppSqlDb` SQL Database.</span></span> <span data-ttu-id="799ae-217">Hallo-verbinding die u eerder hebt gemaakt, wordt automatisch gevuld Hallo onderaan.</span><span class="sxs-lookup"><span data-stu-id="799ae-217">hello connection you created earlier is automatically filled at hello bottom.</span></span>

<span data-ttu-id="799ae-218">Typ Hallo database administrator-wachtwoord die u eerder hebt gemaakt en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="799ae-218">Type hello database administrator password you created earlier and click **Connect**.</span></span>

![Databaseverbinding vanuit Visual Studio configureren](./media/app-service-web-tutorial-dotnet-sqldatabase/connect-to-sql-database.png)

### <a name="allow-client-connection-from-your-computer"></a><span data-ttu-id="799ae-220">Clientverbinding van uw computer toestaan</span><span class="sxs-lookup"><span data-stu-id="799ae-220">Allow client connection from your computer</span></span>

<span data-ttu-id="799ae-221">Hallo **maken van een nieuwe firewallregel** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="799ae-221">hello **Create a new firewall rule** dialog is opened.</span></span> <span data-ttu-id="799ae-222">Uw exemplaar van SQL-Database kunt standaard alleen verbindingen van Azure-services, zoals uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="799ae-222">By default, your SQL Database instance only allows connections from Azure services, such as your Azure web app.</span></span> <span data-ttu-id="799ae-223">tooconnect tooyour database, maakt u een firewallregel in Hallo SQL Database-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="799ae-223">tooconnect tooyour database, create a firewall rule in hello SQL Database instance.</span></span> <span data-ttu-id="799ae-224">Hallo firewallregel kunt Hallo openbaar IP-adres van uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="799ae-224">hello firewall rule allows hello public IP address of your local computer.</span></span>

<span data-ttu-id="799ae-225">dialoogvenster Hallo is al ingevuld met het openbare IP-adres van uw computer.</span><span class="sxs-lookup"><span data-stu-id="799ae-225">hello dialog is already filled with your computer's public IP address.</span></span>

<span data-ttu-id="799ae-226">Zorg ervoor dat **mijn client-IP toevoegen** is geselecteerd en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="799ae-226">Make sure that **Add my client IP** is selected and click **OK**.</span></span> 

![Firewall voor SQL Database-instantie instellen](./media/app-service-web-tutorial-dotnet-sqldatabase/sql-set-firewall.png)

<span data-ttu-id="799ae-228">Zodra de Visual Studio is voltooid Hallo firewall-instellingen voor uw exemplaar van SQL-Database maken, de verbinding wordt weergegeven in **SQL Server Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-228">Once Visual Studio finishes creating hello firewall setting for your SQL Database instance, your connection shows up in **SQL Server Object Explorer**.</span></span>

<span data-ttu-id="799ae-229">Hier kunt u uitvoeren Hallo meest voorkomende databasebewerkingen, zoals het uitvoeren van query's maken, weergaven en opgeslagen procedures en meer.</span><span class="sxs-lookup"><span data-stu-id="799ae-229">Here, you can perform hello most common database operations, such as run queries, create views and stored procedures, and more.</span></span> 

<span data-ttu-id="799ae-230">Met de rechtermuisknop op Hallo `Todoes` tabel en selecteer **weergavegegevens**.</span><span class="sxs-lookup"><span data-stu-id="799ae-230">Right-click on hello `Todoes` table and select **View Data**.</span></span> 

![Objecten van de SQL-Database verkennen](./media/app-service-web-tutorial-dotnet-sqldatabase/explore-sql-database.png)

## <a name="update-app-with-code-first-migrations"></a><span data-ttu-id="799ae-232">App kunt bijwerken met Code First-migraties</span><span class="sxs-lookup"><span data-stu-id="799ae-232">Update app with Code First Migrations</span></span>

<span data-ttu-id="799ae-233">U kunt Hallo vertrouwde hulpprogramma's in Visual Studio tooupdate uw database en web-app in Azure gebruiken.</span><span class="sxs-lookup"><span data-stu-id="799ae-233">You can use hello familiar tools in Visual Studio tooupdate your database and web app in Azure.</span></span> <span data-ttu-id="799ae-234">In deze stap maakt u gebruik Code First-migraties in Entity Framework toomake een wijziging tooyour-databaseschema en tooAzure publiceren.</span><span class="sxs-lookup"><span data-stu-id="799ae-234">In this step, you use Code First Migrations in Entity Framework toomake a change tooyour database schema and publish it tooAzure.</span></span>

<span data-ttu-id="799ae-235">Zie voor meer informatie over het gebruik van Entity Framework Code First-migraties [aan de slag met Entity Framework 6 Code First met MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span><span class="sxs-lookup"><span data-stu-id="799ae-235">For more information about using Entity Framework Code First Migrations, see [Getting Started with Entity Framework 6 Code First using MVC 5](https://docs.microsoft.com/aspnet/mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application).</span></span>

### <a name="update-your-data-model"></a><span data-ttu-id="799ae-236">Uw gegevensmodel bijwerken</span><span class="sxs-lookup"><span data-stu-id="799ae-236">Update your data model</span></span>

<span data-ttu-id="799ae-237">Open _Models\Todo.cs_ in Hallo code-editor.</span><span class="sxs-lookup"><span data-stu-id="799ae-237">Open _Models\Todo.cs_ in hello code editor.</span></span> <span data-ttu-id="799ae-238">Hallo eigenschap toohello na toevoegen `ToDo` klasse:</span><span class="sxs-lookup"><span data-stu-id="799ae-238">Add hello following property toohello `ToDo` class:</span></span>

```csharp
public bool Done { get; set; }
```

### <a name="run-code-first-migrations-locally"></a><span data-ttu-id="799ae-239">Code First-migraties lokaal uitvoeren</span><span class="sxs-lookup"><span data-stu-id="799ae-239">Run Code First Migrations locally</span></span>

<span data-ttu-id="799ae-240">Voer enkele opdrachten toomake updates tooyour lokale database.</span><span class="sxs-lookup"><span data-stu-id="799ae-240">Run a few commands toomake updates tooyour local database.</span></span> 

<span data-ttu-id="799ae-241">Van Hallo **extra** menu, klikt u op **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="799ae-241">From hello **Tools** menu, click **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="799ae-242">Schakel in het venster Package Manager Console Hallo, Code First-migraties:</span><span class="sxs-lookup"><span data-stu-id="799ae-242">In hello Package Manager Console window, enable Code First Migrations:</span></span>

```PowerShell
Enable-Migrations
```

<span data-ttu-id="799ae-243">Toevoegen van een migratie:</span><span class="sxs-lookup"><span data-stu-id="799ae-243">Add a migration:</span></span>

```PowerShell
Add-Migration AddProperty
```

<span data-ttu-id="799ae-244">Hallo lokale database bijwerken:</span><span class="sxs-lookup"><span data-stu-id="799ae-244">Update hello local database:</span></span>

```PowerShell
Update-Database
```

<span data-ttu-id="799ae-245">Type `Ctrl+F5` toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="799ae-245">Type `Ctrl+F5` toorun hello app.</span></span> <span data-ttu-id="799ae-246">Test Hallo details, bewerken en maken van koppelingen.</span><span class="sxs-lookup"><span data-stu-id="799ae-246">Test hello edit, details, and create links.</span></span>

<span data-ttu-id="799ae-247">Als de toepassing hello wordt geladen zonder fouten, is de Code First-migraties van voltooid zijn.</span><span class="sxs-lookup"><span data-stu-id="799ae-247">If hello application loads without errors, then Code First Migrations has succeeded.</span></span> <span data-ttu-id="799ae-248">Uw pagina nog steeds uitstraling kunt u echter Hallo op dezelfde omdat uw toepassingslogica wordt deze nieuwe eigenschap niet nog gebruikt.</span><span class="sxs-lookup"><span data-stu-id="799ae-248">However, your page still looks hello same because your application logic is not using this new property yet.</span></span> 

### <a name="use-hello-new-property"></a><span data-ttu-id="799ae-249">De nieuwe eigenschap hello te gebruiken</span><span class="sxs-lookup"><span data-stu-id="799ae-249">Use hello new property</span></span>

<span data-ttu-id="799ae-250">Enkele wijzigingen aanbrengen in uw code toouse hello `Done` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="799ae-250">Make some changes in your code toouse hello `Done` property.</span></span> <span data-ttu-id="799ae-251">Voor het gemak in deze zelfstudie gaat u alleen toochange hello `Index` en `Create` toosee Hallo eigenschap weergaven in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="799ae-251">For simplicity in this tutorial, you're only going toochange hello `Index` and `Create` views toosee hello property in action.</span></span>

<span data-ttu-id="799ae-252">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="799ae-252">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="799ae-253">Hallo zoeken `Create()` methode en voeg `Done` toohello lijst met eigenschappen in Hallo `Bind` kenmerk.</span><span class="sxs-lookup"><span data-stu-id="799ae-253">Find hello `Create()` method and add `Done` toohello list of properties in hello `Bind` attribute.</span></span> <span data-ttu-id="799ae-254">Wanneer u bent klaar, uw `Create()` methodehandtekening ziet eruit als Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="799ae-254">When you're done, your `Create()` method signature looks like hello following code:</span></span>

```csharp
public ActionResult Create([Bind(Include = "id,Description,CreatedDate,Done")] Todo todo)
```

<span data-ttu-id="799ae-255">Open _Views\Todos\Create.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="799ae-255">Open _Views\Todos\Create.cshtml_.</span></span>

<span data-ttu-id="799ae-256">In Hallo Razor code, ziet u een `<div class="form-group">` element die gebruikmaakt van `model.Description`, en vervolgens een andere `<div class="form-group">` element die gebruikmaakt van `model.CreatedDate`.</span><span class="sxs-lookup"><span data-stu-id="799ae-256">In hello Razor code, you should see a `<div class="form-group">` element that uses `model.Description`, and then another `<div class="form-group">` element that uses `model.CreatedDate`.</span></span> <span data-ttu-id="799ae-257">Direct na deze twee elementen toevoegen `<div class="form-group">` element die gebruikmaakt van `model.Done`:</span><span class="sxs-lookup"><span data-stu-id="799ae-257">Immediately following these two elements, add another `<div class="form-group">` element that uses `model.Done`:</span></span>

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

<span data-ttu-id="799ae-258">Open _Views\Todos\Index.cshtml_.</span><span class="sxs-lookup"><span data-stu-id="799ae-258">Open _Views\Todos\Index.cshtml_.</span></span>

<span data-ttu-id="799ae-259">Zoeken naar Hallo leeg `<th></th>` element.</span><span class="sxs-lookup"><span data-stu-id="799ae-259">Search for hello empty `<th></th>` element.</span></span> <span data-ttu-id="799ae-260">Net boven dit element toevoegen Hallo Razor code te volgen:</span><span class="sxs-lookup"><span data-stu-id="799ae-260">Just above this element, add hello following Razor code:</span></span>

```csharp
<th>
    @Html.DisplayNameFor(model => model.Done)
</th>
```

<span data-ttu-id="799ae-261">Hallo zoeken `<td>` element met Hallo `Html.ActionLink()` Help-methoden.</span><span class="sxs-lookup"><span data-stu-id="799ae-261">Find hello `<td>` element that contains hello `Html.ActionLink()` helper methods.</span></span> <span data-ttu-id="799ae-262">Net boven dit element toevoegen Hallo Razor code te volgen:</span><span class="sxs-lookup"><span data-stu-id="799ae-262">Just above this element, add hello following Razor code:</span></span>

```csharp
<td>
    @Html.DisplayFor(modelItem => item.Done)
</td>
```

<span data-ttu-id="799ae-263">Dit is alles wat u toosee Hallo wijzigingen in Hallo moet `Index` en `Create` weergaven.</span><span class="sxs-lookup"><span data-stu-id="799ae-263">That's all you need toosee hello changes in hello `Index` and `Create` views.</span></span> 

<span data-ttu-id="799ae-264">Type `Ctrl+F5` toorun Hallo app.</span><span class="sxs-lookup"><span data-stu-id="799ae-264">Type `Ctrl+F5` toorun hello app.</span></span>

<span data-ttu-id="799ae-265">U kunt nu een taakitem toegevoegd en controleer of **gedaan**.</span><span class="sxs-lookup"><span data-stu-id="799ae-265">You can now add a to-do item and check **Done**.</span></span> <span data-ttu-id="799ae-266">Vervolgens moet het weergegeven in uw startpagina als een item voltooid.</span><span class="sxs-lookup"><span data-stu-id="799ae-266">Then it should show up in your homepage as a completed item.</span></span> <span data-ttu-id="799ae-267">Houd er rekening mee dat Hallo `Edit` weergave niet Hallo `Done` veld, omdat u niet Hallo wijzigen `Edit` weergeven.</span><span class="sxs-lookup"><span data-stu-id="799ae-267">Remember that hello `Edit` view doesn't show hello `Done` field, because you didn't change hello `Edit` view.</span></span>

### <a name="enable-code-first-migrations-in-azure"></a><span data-ttu-id="799ae-268">Code First-migraties in Azure inschakelen</span><span class="sxs-lookup"><span data-stu-id="799ae-268">Enable Code First Migrations in Azure</span></span>

<span data-ttu-id="799ae-269">Nu dat uw code wijzigen werkt, met inbegrip van de database wilt migreren, kunt u deze tooyour Azure-web-app publiceren en uw SQL-Database te werken met Code First-migraties.</span><span class="sxs-lookup"><span data-stu-id="799ae-269">Now that your code change works, including database migration, you publish it tooyour Azure web app and update your SQL Database with Code First Migrations too.</span></span>

<span data-ttu-id="799ae-270">Net zoals, met de rechtermuisknop op uw project en selecteer **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="799ae-270">Just like before, right-click your project and select **Publish**.</span></span>

<span data-ttu-id="799ae-271">Klik op **instellingen** tooopen Hallo wizard publiceren.</span><span class="sxs-lookup"><span data-stu-id="799ae-271">Click **Settings** tooopen hello publish wizard.</span></span>

![Open publicatie-instellingen](./media/app-service-web-tutorial-dotnet-sqldatabase/publish-settings.png)

<span data-ttu-id="799ae-273">Klik in de wizard Hallo op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="799ae-273">In hello wizard, click **Next**.</span></span>

<span data-ttu-id="799ae-274">Zorg ervoor dat deze Hallo-verbindingsreeks voor de SQL-Database wordt ingevuld **MyDatabaseContext (MyDbConnection)**.</span><span class="sxs-lookup"><span data-stu-id="799ae-274">Make sure that hello connection string for your SQL Database is populated in **MyDatabaseContext (MyDbConnection)**.</span></span> <span data-ttu-id="799ae-275">Mogelijk moet u tooselect hello **myToDoAppDb** database uit de vervolgkeuzelijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="799ae-275">You may need tooselect hello **myToDoAppDb** database from hello dropdown.</span></span> 

<span data-ttu-id="799ae-276">Selecteer **uitvoeren Code First-migraties (wordt uitgevoerd op de start van toepassing)**, klikt u vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="799ae-276">Select **Execute Code First Migrations (runs on application start)**, then click **Save**.</span></span>

![Code First-migraties inschakelen in Azure-web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/enable-migrations.png)

### <a name="publish-your-changes"></a><span data-ttu-id="799ae-278">Uw wijzigingen publiceren</span><span class="sxs-lookup"><span data-stu-id="799ae-278">Publish your changes</span></span>

<span data-ttu-id="799ae-279">Nu dat u Code First-migraties in uw Azure-web-app hebt ingeschakeld, moet u uw codewijzigingen publiceren.</span><span class="sxs-lookup"><span data-stu-id="799ae-279">Now that you enabled Code First Migrations in your Azure web app, publish your code changes.</span></span>

<span data-ttu-id="799ae-280">In Hallo pagina publiceren, klikt u op **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="799ae-280">In hello publish page, click **Publish**.</span></span>

<span data-ttu-id="799ae-281">Selecteer en probeer het opnieuw toe te voegen taakitems **gedaan**, en ze moeten worden weergegeven in uw startpagina als een item voltooid.</span><span class="sxs-lookup"><span data-stu-id="799ae-281">Try adding to-do items again and select **Done**, and they should show up in your homepage as a completed item.</span></span>

![Azure-web-app na de eerste Code-migratie](./media/app-service-web-tutorial-dotnet-sqldatabase/this-one-is-done.png)

<span data-ttu-id="799ae-283">Uw bestaande taakitems nog steeds worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="799ae-283">All your existing to-do items are still displayed.</span></span> <span data-ttu-id="799ae-284">Wanneer u uw ASP.NET-toepassing opnieuw publiceren, is er geen bestaande gegevens in de SQL-Database verloren.</span><span class="sxs-lookup"><span data-stu-id="799ae-284">When you republish your ASP.NET application, existing data in your SQL Database is not lost.</span></span> <span data-ttu-id="799ae-285">Bovendien Code First-migraties Hallo gegevensschema alleen verandert en uw bestaande gegevens intact blijft.</span><span class="sxs-lookup"><span data-stu-id="799ae-285">Also, Code First Migrations only changes hello data schema and leaves your existing data intact.</span></span>


## <a name="stream-application-logs"></a><span data-ttu-id="799ae-286">Toepassingslogboeken Stream</span><span class="sxs-lookup"><span data-stu-id="799ae-286">Stream application logs</span></span>

<span data-ttu-id="799ae-287">U kunt tracering berichten rechtstreeks vanuit uw Azure-web-app tooVisual Studio streamen.</span><span class="sxs-lookup"><span data-stu-id="799ae-287">You can stream tracing messages directly from your Azure web app tooVisual Studio.</span></span>

<span data-ttu-id="799ae-288">Open _Controllers\TodosController.cs_.</span><span class="sxs-lookup"><span data-stu-id="799ae-288">Open _Controllers\TodosController.cs_.</span></span>

<span data-ttu-id="799ae-289">Elke actie begint met een `Trace.WriteLine()` methode.</span><span class="sxs-lookup"><span data-stu-id="799ae-289">Each action starts with a `Trace.WriteLine()` method.</span></span> <span data-ttu-id="799ae-290">Deze code wordt toegevoegd tooshow u hoe tooadd trace berichten tooyour Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="799ae-290">This code is added tooshow you how tooadd trace messages tooyour Azure web app.</span></span>

### <a name="open-server-explorer"></a><span data-ttu-id="799ae-291">Open Server Explorer</span><span class="sxs-lookup"><span data-stu-id="799ae-291">Open Server Explorer</span></span>

<span data-ttu-id="799ae-292">Van Hallo **weergave** selecteert u **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-292">From hello **View** menu, select **Server Explorer**.</span></span> <span data-ttu-id="799ae-293">U kunt logboekregistratie configureren voor uw Azure-web-app in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-293">You can configure logging for your Azure web app in **Server Explorer**.</span></span> 

### <a name="enable-log-streaming"></a><span data-ttu-id="799ae-294">Streaming-logboek inschakelen</span><span class="sxs-lookup"><span data-stu-id="799ae-294">Enable log streaming</span></span>

<span data-ttu-id="799ae-295">In **Server Explorer**, vouw **Azure** > **App Service**.</span><span class="sxs-lookup"><span data-stu-id="799ae-295">In **Server Explorer**, expand **Azure** > **App Service**.</span></span>

<span data-ttu-id="799ae-296">Vouw Hallo **myResourceGroup** resourcegroep, u hebt gemaakt tijdens het maken van hello Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="799ae-296">Expand hello **myResourceGroup** resource group, you created when you first created hello Azure web app.</span></span>

<span data-ttu-id="799ae-297">Met de rechtermuisknop op uw Azure-web-app en selecteer **Streaming logboeken bekijken**.</span><span class="sxs-lookup"><span data-stu-id="799ae-297">Right-click your Azure web app and select **View Streaming Logs**.</span></span>

![Streaming-logboek inschakelen](./media/app-service-web-tutorial-dotnet-sqldatabase/stream-logs.png)

<span data-ttu-id="799ae-299">Hallo logboeken worden nu gestreamd naar Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="799ae-299">hello logs are now streamed into hello **Output** window.</span></span> 

![In het uitvoervenster streaming logboek](./media/app-service-web-tutorial-dotnet-sqldatabase/log-streaming-pane.png)

<span data-ttu-id="799ae-301">Echter, u niet ziet van Hallo traceringsberichten nog.</span><span class="sxs-lookup"><span data-stu-id="799ae-301">However, you don't see any of hello trace messages yet.</span></span> <span data-ttu-id="799ae-302">Dat omdat wanneer u eerst selecteert **Streaming logboeken bekijken**, uw Azure-web-app stelt het traceringsniveau hello te`Error`, die alleen legt foutgebeurtenissen vast in (Hello `Trace.TraceError()` methode).</span><span class="sxs-lookup"><span data-stu-id="799ae-302">That's because when you first select **View Streaming Logs**, your Azure web app sets hello trace level too`Error`, which only logs error events (with hello `Trace.TraceError()` method).</span></span>

### <a name="change-trace-levels"></a><span data-ttu-id="799ae-303">De traceringsniveaus wijzigen</span><span class="sxs-lookup"><span data-stu-id="799ae-303">Change trace levels</span></span>

<span data-ttu-id="799ae-304">toochange hello trace niveaus toooutput andere traceringsberichten, gaat u terug te**Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="799ae-304">toochange hello trace levels toooutput other trace messages, go back too**Server Explorer**.</span></span>

<span data-ttu-id="799ae-305">Opnieuw met de rechtermuisknop op uw Azure-web-app en selecteer **instellingen**.</span><span class="sxs-lookup"><span data-stu-id="799ae-305">Right-click your Azure web app again and select **Settings**.</span></span>

<span data-ttu-id="799ae-306">In Hallo **toepassingslogboeken (bestandssysteem)** vervolgkeuzelijst **uitgebreid**.</span><span class="sxs-lookup"><span data-stu-id="799ae-306">In hello **Application Logging (File System)** dropdown, select **Verbose**.</span></span> <span data-ttu-id="799ae-307">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="799ae-307">Click **Save**.</span></span>

![Niveau tooVerbose tracering wijzigen](./media/app-service-web-tutorial-dotnet-sqldatabase/trace-level-verbose.png)

> [!TIP]
> <span data-ttu-id="799ae-309">U kunt experimenteren met verschillende trace niveaus toosee welke soorten berichten worden weergegeven voor elk bedreigingsniveau.</span><span class="sxs-lookup"><span data-stu-id="799ae-309">You can experiment with different trace levels toosee what types of messages are displayed for each level.</span></span> <span data-ttu-id="799ae-310">Bijvoorbeeld, Hallo **informatie** niveau omvat alle logboeken die zijn gemaakt door `Trace.TraceInformation()`, `Trace.TraceWarning()`, en `Trace.TraceError()`, maar niet de logboeken die zijn gemaakt door `Trace.WriteLine()`.</span><span class="sxs-lookup"><span data-stu-id="799ae-310">For example, hello **Information** level includes all logs created by `Trace.TraceInformation()`, `Trace.TraceWarning()`, and `Trace.TraceError()`, but not logs created by `Trace.WriteLine()`.</span></span>
>
>

<span data-ttu-id="799ae-311">In de browser probeert te klikken op rond Hallo taak lijst toepassing in Azure.</span><span class="sxs-lookup"><span data-stu-id="799ae-311">In your browser, try clicking around hello to-do list application in Azure.</span></span> <span data-ttu-id="799ae-312">Hallo traceringsberichten worden nu gestreamd toohello **uitvoer** venster in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="799ae-312">hello trace messages are now streamed toohello **Output** window in Visual Studio.</span></span>

```
Application: 2017-04-06T23:30:41  PID[8132] Verbose     GET /Todos/Index
Application: 2017-04-06T23:30:43  PID[8132] Verbose     GET /Todos/Create
Application: 2017-04-06T23:30:53  PID[8132] Verbose     POST /Todos/Create
Application: 2017-04-06T23:30:54  PID[8132] Verbose     GET /Todos/Index
```



### <a name="stop-log-streaming"></a><span data-ttu-id="799ae-313">Logboek streaming stoppen</span><span class="sxs-lookup"><span data-stu-id="799ae-313">Stop log streaming</span></span>

<span data-ttu-id="799ae-314">toostop Hallo logboek streaming-service, klikt u op Hallo **bewaking stopt** knop in Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="799ae-314">toostop hello log-streaming service, click hello **Stop monitoring** button in hello **Output** window.</span></span>

![Logboek streaming stoppen](./media/app-service-web-tutorial-dotnet-sqldatabase/stop-streaming.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="799ae-316">Uw Azure-web-app beheren</span><span class="sxs-lookup"><span data-stu-id="799ae-316">Manage your Azure web app</span></span>

<span data-ttu-id="799ae-317">Ga toohello [Azure-portal](https://portal.azure.com) toosee Hallo web-app die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="799ae-317">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span> 



<span data-ttu-id="799ae-318">In het linkermenu hello, klikt u op **App Service**, klikt u op Hallo-naam van uw Azure-web-app.</span><span class="sxs-lookup"><span data-stu-id="799ae-318">From hello left menu, click **App Service**, then click hello name of your Azure web app.</span></span>

![Navigatie in de portal tooAzure web-app](./media/app-service-web-tutorial-dotnet-sqldatabase/access-portal.png)

<span data-ttu-id="799ae-320">U bevindt zich in uw web-app-pagina.</span><span class="sxs-lookup"><span data-stu-id="799ae-320">You have landed in your web app's page.</span></span> 

<span data-ttu-id="799ae-321">Standaard Hallo portal weergegeven Hallo **overzicht** pagina.</span><span class="sxs-lookup"><span data-stu-id="799ae-321">By default, hello portal shows hello **Overview** page.</span></span> <span data-ttu-id="799ae-322">Deze pagina geeft u een overzicht van hoe uw app presteert.</span><span class="sxs-lookup"><span data-stu-id="799ae-322">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="799ae-323">Hier kunt u ook algemene beheertaken uitvoeren, zoals bladeren, stoppen, starten, opnieuw opstarten en verwijderen.</span><span class="sxs-lookup"><span data-stu-id="799ae-323">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="799ae-324">Hallo tabbladen aan de linkerkant Hallo van Hallo pagina bevatten Hallo verschillende configuratiepagina's die u kunt openen.</span><span class="sxs-lookup"><span data-stu-id="799ae-324">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span> 

![App Service-pagina in Azure Portal](./media/app-service-web-tutorial-dotnet-sqldatabase/web-app-blade.png)

[!INCLUDE [Clean up section](../../includes/clean-up-section-portal-web-app.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="799ae-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="799ae-326">Next steps</span></span>

<span data-ttu-id="799ae-327">In deze zelfstudie heeft u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="799ae-327">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="799ae-328">Maken van een SQL-Database in Azure</span><span class="sxs-lookup"><span data-stu-id="799ae-328">Create a SQL Database in Azure</span></span>
> * <span data-ttu-id="799ae-329">Verbinding maken met een ASP.NET-app tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="799ae-329">Connect an ASP.NET app tooSQL Database</span></span>
> * <span data-ttu-id="799ae-330">Hallo app tooAzure implementeren</span><span class="sxs-lookup"><span data-stu-id="799ae-330">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="799ae-331">Hallo-gegevensmodel bijwerken en Hallo app implementeren</span><span class="sxs-lookup"><span data-stu-id="799ae-331">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="799ae-332">Logboeken van de stroom van Azure tooyour terminal</span><span class="sxs-lookup"><span data-stu-id="799ae-332">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="799ae-333">Hallo-app in hello Azure-portal beheren</span><span class="sxs-lookup"><span data-stu-id="799ae-333">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="799ae-334">De volgende zelfstudie toolearn toohello gaan hoe toomap een aangepaste DNS-Server name toohello web-app.</span><span class="sxs-lookup"><span data-stu-id="799ae-334">Advance toohello next tutorial toolearn how toomap a custom DNS name toohello web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="799ae-335">Toewijzen van een bestaande aangepaste DNS-naam tooAzure Web-Apps</span><span class="sxs-lookup"><span data-stu-id="799ae-335">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
