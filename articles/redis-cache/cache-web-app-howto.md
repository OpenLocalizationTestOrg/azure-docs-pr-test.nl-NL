---
title: aaaHow toocreate een Web-App met Redis-Cache | Microsoft Docs
description: Meer informatie over hoe toocreate een Web-App met Redis-Cache
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: 454e23d7-a99b-4e6e-8dd7-156451d2da7c
ms.service: cache
ms.workload: tbd
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: hero-article
ms.date: 05/09/2017
ms.author: sdanie
ms.openlocfilehash: d3e6df97b06fdf9032570dc360944be4bd7715de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-web-app-with-redis-cache"></a><span data-ttu-id="38f01-103">Hoe toocreate een Web-App met Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-103">How toocreate a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="38f01-104">.NET</span><span class="sxs-lookup"><span data-stu-id="38f01-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="38f01-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="38f01-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="38f01-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="38f01-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="38f01-107">Java</span><span class="sxs-lookup"><span data-stu-id="38f01-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="38f01-108">Python</span><span class="sxs-lookup"><span data-stu-id="38f01-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="38f01-109">Deze zelfstudie laat zien hoe toocreate en implementeren van een ASP.NET web application tooa web-app in Azure App Service met behulp van Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="38f01-109">This tutorial shows how toocreate and deploy an ASP.NET web application tooa web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="38f01-110">Hallo-voorbeeldtoepassing geeft een lijst met teamstatistieken uit een database en toont de verschillende manieren toouse Azure Redis-Cache toostore en gegevens ophalen uit de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-110">hello sample application displays a list of team statistics from a database and shows different ways toouse Azure Redis Cache toostore and retrieve data from hello cache.</span></span> <span data-ttu-id="38f01-111">Wanneer u Hallo-zelfstudie hebt voltooid hebt u een actieve WebApp die leest en schrijft tooa database geoptimaliseerd met Azure Redis-Cache en wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="38f01-111">When you complete hello tutorial you'll have a running web app that reads and writes tooa database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="38f01-112">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="38f01-112">You'll learn:</span></span>

* <span data-ttu-id="38f01-113">Hoe toocreate een ASP.NET MVC 5-webtoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38f01-113">How toocreate an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="38f01-114">Hoe tooaccess gegevens uit een database met behulp van Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="38f01-114">How tooaccess data from a database using Entity Framework.</span></span>
* <span data-ttu-id="38f01-115">Hoe tooimprove gegevensdoorvoer en belasting van de database te verminderen door opslaan en ophalen van gegevens met behulp van Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-115">How tooimprove data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="38f01-116">Hoe toouse een in Redis gesorteerde set tooretrieve Hallo bovenste 5 teams.</span><span class="sxs-lookup"><span data-stu-id="38f01-116">How toouse a Redis sorted set tooretrieve hello top 5 teams.</span></span>
* <span data-ttu-id="38f01-117">Tooprovision Hallo hoe Azure-resources voor Hallo-toepassing met een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="38f01-117">How tooprovision hello Azure resources for hello application using a Resource Manager template.</span></span>
* <span data-ttu-id="38f01-118">Hoe Hallo toopublish tooAzure van toepassing met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="38f01-118">How toopublish hello application tooAzure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38f01-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="38f01-119">Prerequisites</span></span>
<span data-ttu-id="38f01-120">toocomplete hello zelfstudie, moet u Hallo na vereisten hebben.</span><span class="sxs-lookup"><span data-stu-id="38f01-120">toocomplete hello tutorial, you must have hello following prerequisites.</span></span>

* [<span data-ttu-id="38f01-121">Azure-account</span><span class="sxs-lookup"><span data-stu-id="38f01-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="38f01-122">Visual Studio 2017 Hello Azure SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="38f01-122">Visual Studio 2017 with hello Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="38f01-123">Azure-account</span><span class="sxs-lookup"><span data-stu-id="38f01-123">Azure account</span></span>
<span data-ttu-id="38f01-124">U hebt een Azure-account toocomplete Hallo zelfstudie nodig.</span><span class="sxs-lookup"><span data-stu-id="38f01-124">You need an Azure account toocomplete hello tutorial.</span></span> <span data-ttu-id="38f01-125">U kunt:</span><span class="sxs-lookup"><span data-stu-id="38f01-125">You can:</span></span>

* <span data-ttu-id="38f01-126">[Gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="38f01-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="38f01-127">U ontvangt tegoed dat gebruikte tootry uit betaald Azure-services worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="38f01-127">You get credits that can be used tootry out paid Azure services.</span></span> <span data-ttu-id="38f01-128">Zelfs nadat Hallo tegoed is gebruikt, kunt u Hallo account houden en gratis Azure-services en functies gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38f01-128">Even after hello credits are used up, you can keep hello account and use free Azure services and features.</span></span>
* <span data-ttu-id="38f01-129">[Uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="38f01-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="38f01-130">Via uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="38f01-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-hello-azure-sdk-for-net"></a><span data-ttu-id="38f01-131">Visual Studio 2017 Hello Azure SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="38f01-131">Visual Studio 2017 with hello Azure SDK for .NET</span></span>
<span data-ttu-id="38f01-132">Hallo-zelfstudie is geschreven voor Visual Studio 2017 Hello [Azure SDK voor .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="38f01-132">hello tutorial is written for Visual Studio 2017 with hello [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="38f01-133">Hello Azure SDK 2.9.5 is opgenomen in Visual Studio-installatieprogramma Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-133">hello Azure SDK 2.9.5 is included with hello Visual Studio installer.</span></span>

<span data-ttu-id="38f01-134">Als u Visual Studio 2015 hebt, kunt u de zelfstudie Hallo Hello [Azure SDK voor .NET](../dotnet-sdk.md) 2.8.2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="38f01-134">If you have Visual Studio 2015, you can follow hello tutorial with hello [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="38f01-135">[Download Hallo nieuwste Azure SDK voor Visual Studio 2015 hier](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="38f01-135">[Download hello latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="38f01-136">Visual Studio wordt automatisch geïnstalleerd met Hallo SDK als u nog geen hebt.</span><span class="sxs-lookup"><span data-stu-id="38f01-136">Visual Studio is automatically installed with hello SDK if you don't already have it.</span></span> <span data-ttu-id="38f01-137">Sommige schermen zien er mogelijk anders uit Hallo illustraties wordt weergegeven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38f01-137">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

<span data-ttu-id="38f01-138">Als u Visual Studio 2013 hebt, kunt u [downloaden hello nieuwste Azure SDK voor Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="38f01-138">If you have Visual Studio 2013, you can [download hello latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="38f01-139">Sommige schermen zien er mogelijk anders uit Hallo illustraties wordt weergegeven in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38f01-139">Some screens may look different from hello illustrations shown in this tutorial.</span></span>

## <a name="create-hello-visual-studio-project"></a><span data-ttu-id="38f01-140">Hallo Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="38f01-140">Create hello Visual Studio project</span></span>
1. <span data-ttu-id="38f01-141">Open Visual Studio en klik op **File**, **New**, **Project**.</span><span class="sxs-lookup"><span data-stu-id="38f01-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="38f01-142">Vouw Hallo **Visual C#** knooppunt in Hallo **sjablonen** selecteert **Cloud**, en klik op **ASP.NET-webtoepassing**.</span><span class="sxs-lookup"><span data-stu-id="38f01-142">Expand hello **Visual C#** node in hello **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="38f01-143">Zorg ervoor dat **.NET Framework 4.5.2** of hoger is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="38f01-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="38f01-144">Type **ContosoTeamStats** in Hallo **naam** tekstvak en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="38f01-144">Type **ContosoTeamStats** into hello **Name** textbox and click **OK**.</span></span>
   
    ![Project maken][cache-create-project]
3. <span data-ttu-id="38f01-146">Selecteer **MVC** als Hallo projecttype.</span><span class="sxs-lookup"><span data-stu-id="38f01-146">Select **MVC** as hello project type.</span></span> 

    <span data-ttu-id="38f01-147">Zorg ervoor dat **geen verificatie** is opgegeven voor Hallo **verificatie** instellingen.</span><span class="sxs-lookup"><span data-stu-id="38f01-147">Ensure that **No Authentication** is specified for hello **Authentication** settings.</span></span> <span data-ttu-id="38f01-148">Afhankelijk van uw versie van Visual Studio kan Hallo standaard toosomething anders worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="38f01-148">Depending on your version of Visual Studio, hello default may be set toosomething else.</span></span> <span data-ttu-id="38f01-149">toochange, klikt u op **verificatie wijzigen** en selecteer **geen verificatie**.</span><span class="sxs-lookup"><span data-stu-id="38f01-149">toochange it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="38f01-150">Als u samen met Visual Studio 2015 volgt, schakelt u Hallo **hosten in de cloud Hallo** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="38f01-150">If you are following along with Visual Studio 2015, clear hello **Host in hello cloud** checkbox.</span></span> <span data-ttu-id="38f01-151">U zult [inrichten hello Azure-resources](#provision-the-azure-resources) en [publiceren Hallo toepassing tooAzure](#publish-the-application-to-azure) bij volgende stappen in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-151">You'll [provision hello Azure resources](#provision-the-azure-resources) and [publish hello application tooAzure](#publish-the-application-to-azure) in subsequent steps in hello tutorial.</span></span> <span data-ttu-id="38f01-152">Voor een voorbeeld van een App Service-web-app vanuit Visual Studio wordt ingericht door **hosten in de cloud Hallo** dit selectievakje inschakelt, Zie [aan de slag met Web-Apps in Azure App Service met ASP.NET en Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="38f01-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in hello cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![De projectsjabloon selecteren][cache-select-template]
4. <span data-ttu-id="38f01-154">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="38f01-154">Click **OK** toocreate hello project.</span></span>

## <a name="create-hello-aspnet-mvc-application"></a><span data-ttu-id="38f01-155">Hallo ASP.NET MVC-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="38f01-155">Create hello ASP.NET MVC application</span></span>
<span data-ttu-id="38f01-156">In deze sectie van Hallo zelfstudie maakt u eenvoudige Hallo-toepassing die wordt gelezen en wordt de teamstatistieken uit een database.</span><span class="sxs-lookup"><span data-stu-id="38f01-156">In this section of hello tutorial, you'll create hello basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="38f01-157">Hallo Entity Framework NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-157">Add hello Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="38f01-158">Hallo model toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-158">Add hello model</span></span>](#add-the-model)
* [<span data-ttu-id="38f01-159">Hallo controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-159">Add hello controller</span></span>](#add-the-controller)
* [<span data-ttu-id="38f01-160">Hallo-weergaven configureren</span><span class="sxs-lookup"><span data-stu-id="38f01-160">Configure hello views</span></span>](#configure-the-views)

### <a name="add-hello-entity-framework-nuget-package"></a><span data-ttu-id="38f01-161">Hallo Entity Framework NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-161">Add hello Entity Framework NuGet package</span></span>

1. <span data-ttu-id="38f01-162">Klik op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.</span><span class="sxs-lookup"><span data-stu-id="38f01-162">Click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="38f01-163">Voer hello na de opdracht van Hallo **Package Manager Console** venster.</span><span class="sxs-lookup"><span data-stu-id="38f01-163">Run hello following command from hello **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="38f01-164">Zie voor meer informatie over dit pakket Hallo [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet-pagina.</span><span class="sxs-lookup"><span data-stu-id="38f01-164">For more information about this package, see hello [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-hello-model"></a><span data-ttu-id="38f01-165">Hallo model toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-165">Add hello model</span></span>
1. <span data-ttu-id="38f01-166">Klik in **Solution Explorer** met de rechtermuisknop op **Models** en kies **Add**, **Class**.</span><span class="sxs-lookup"><span data-stu-id="38f01-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Het model toevoegen][cache-model-add-class]
2. <span data-ttu-id="38f01-168">Voer `Team` voor Hallo klassenaam en klik op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="38f01-168">Enter `Team` for hello class name and click **Add**.</span></span>
   
    ![De modelklasse toevoegen][cache-model-add-class-dialog]
3. <span data-ttu-id="38f01-170">Vervang Hallo `using` instructies boven Hallo Hallo `Team.cs` bestand met de volgende Hallo `using` instructies.</span><span class="sxs-lookup"><span data-stu-id="38f01-170">Replace hello `using` statements at hello top of hello `Team.cs` file with hello following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="38f01-171">Hallo-definitie Hallo vervangen `Team` klasse met het volgende codefragment bevat een bijgewerkte Hallo `Team` klasse definition, evenals een aantal andere helperklassen van Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="38f01-171">Replace hello definition of hello `Team` class with hello following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="38f01-172">Zie voor meer informatie over Hallo code eerste benadering tooEntity Framework die wordt gebruikt in deze zelfstudie [Code eerste tooa nieuwe database](https://msdn.microsoft.com/data/jj193542).</span><span class="sxs-lookup"><span data-stu-id="38f01-172">For more information on hello code first approach tooEntity Framework that's used in this tutorial, see [Code first tooa new database](https://msdn.microsoft.com/data/jj193542).</span></span>

    ```c#
    public class Team
    {
        public int ID { get; set; }
        public string Name { get; set; }
        public int Wins { get; set; }
        public int Losses { get; set; }
        public int Ties { get; set; }
    
        static public void PlayGames(IEnumerable<Team> teams)
        {
            // Simple random generation of statistics.
            Random r = new Random();
    
            foreach (var t in teams)
            {
                t.Wins = r.Next(33);
                t.Losses = r.Next(33);
                t.Ties = r.Next(0, 5);
            }
        }
    }
    
    public class TeamContext : DbContext
    {
        public TeamContext()
            : base("TeamContext")
        {
        }
    
        public DbSet<Team> Teams { get; set; }
    }
    
    public class TeamInitializer : CreateDatabaseIfNotExists<TeamContext>
    {
        protected override void Seed(TeamContext context)
        {
            var teams = new List<Team>
            {
                new Team{Name="Adventure Works Cycles"},
                new Team{Name="Alpine Ski House"},
                new Team{Name="Blue Yonder Airlines"},
                new Team{Name="Coho Vineyard"},
                new Team{Name="Contoso, Ltd."},
                new Team{Name="Fabrikam, Inc."},
                new Team{Name="Lucerne Publishing"},
                new Team{Name="Northwind Traders"},
                new Team{Name="Consolidated Messenger"},
                new Team{Name="Fourth Coffee"},
                new Team{Name="Graphic Design Institute"},
                new Team{Name="Nod Publishers"}
            };
    
            Team.PlayGames(teams);
    
            teams.ForEach(t => context.Teams.Add(t));
            context.SaveChanges();
        }
    }
    
    public class TeamConfiguration : DbConfiguration
    {
        public TeamConfiguration()
        {
            SetExecutionStrategy("System.Data.SqlClient", () => new SqlAzureExecutionStrategy());
        }
    }
    ```


1. <span data-ttu-id="38f01-173">In **Solution Explorer**, dubbelklikt u op **web.config** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="38f01-173">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="38f01-175">Voeg de volgende Hallo `connectionStrings` sectie.</span><span class="sxs-lookup"><span data-stu-id="38f01-175">Add hello following `connectionStrings` section.</span></span> <span data-ttu-id="38f01-176">Hallo-naam van de verbindingsreeks Hallo moet overeenkomen met naam van de Hallo Hallo Entity Framework database contextklasse die `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="38f01-176">hello name of hello connection string must match hello name of hello Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="38f01-177">U kunt nieuwe Hallo toevoegen `connectionStrings` sectie zodat het achter `configSections`, zoals weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-177">You can add hello new `connectionStrings` section so that it follows `configSections`, as shown in hello following example.</span></span>

    ```xml
    <configuration>
      <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
      </configSections>
      <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
      </connectionStrings>
      ...
      ```

    > [!NOTE]
    > <span data-ttu-id="38f01-178">De verbindingsreeks kan afwijken, afhankelijk van het Hallo-versie van Visual Studio en SQL Server Express edition toocomplete Hallo zelfstudie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="38f01-178">Your connection string may be different depending on hello version of Visual Studio and SQL Server Express edition used toocomplete hello tutorial.</span></span> <span data-ttu-id="38f01-179">Hallo web.config sjabloon moet geconfigureerde toomatch uw installatie, en mogen bevatten `Data Source` vermeldingen, zoals `(LocalDB)\v11.0` (van SQL Server Express 2012) of `Data Source=(LocalDB)\MSSQLLocalDB` (vanuit SQL Server Express 2014 en nieuwer).</span><span class="sxs-lookup"><span data-stu-id="38f01-179">hello web.config template should be configured toomatch your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="38f01-180">Zie [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) voor meer informatie over verbindingsreeksen en SQL Express-versies.</span><span class="sxs-lookup"><span data-stu-id="38f01-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-hello-controller"></a><span data-ttu-id="38f01-181">Hallo controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="38f01-181">Add hello controller</span></span>
1. <span data-ttu-id="38f01-182">Druk op **F6** toobuild Hallo project.</span><span class="sxs-lookup"><span data-stu-id="38f01-182">Press **F6** toobuild hello project.</span></span> 
2. <span data-ttu-id="38f01-183">In **Solution Explorer**, klik met de rechtermuisknop Hallo **domeincontrollers** map en kies **toevoegen**, **Controller**.</span><span class="sxs-lookup"><span data-stu-id="38f01-183">In **Solution Explorer**, right-click hello **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Controller toevoegen][cache-add-controller]
3. <span data-ttu-id="38f01-185">Kies **MVC 5 Controller with views, using Entity Framework** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="38f01-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="38f01-186">Als u een fout optreedt wanneer u op **toevoegen**, zorg ervoor dat u Hallo project eerst hebt gebouwd.</span><span class="sxs-lookup"><span data-stu-id="38f01-186">If you get an error after clicking **Add**, ensure that you have built hello project first.</span></span>
   
    ![Controllerklasse toevoegen][cache-add-controller-class]
4. <span data-ttu-id="38f01-188">Selecteer **Team (ContosoTeamStats.Models)** van Hallo **Modelklasse** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38f01-188">Select **Team (ContosoTeamStats.Models)** from hello **Model class** drop-down list.</span></span> <span data-ttu-id="38f01-189">Selecteer **TeamContext (ContosoTeamStats.Models)** van Hallo **Data context class** vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="38f01-189">Select **TeamContext (ContosoTeamStats.Models)** from hello **Data context class** drop-down list.</span></span> <span data-ttu-id="38f01-190">Type `TeamsController` in Hallo **Controller** naam textbox (indien dit niet automatisch wordt ingevuld).</span><span class="sxs-lookup"><span data-stu-id="38f01-190">Type `TeamsController` in hello **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="38f01-191">Klik op **toevoegen** toocreate controllerklasse Hallo en Hallo standaardweergaven toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="38f01-191">Click **Add** toocreate hello controller class and add hello default views.</span></span>
   
    ![Controller configureren][cache-configure-controller]
5. <span data-ttu-id="38f01-193">In **Solution Explorer**, vouw **Global.asax** en dubbelklikt u op **Global.asax.cs** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="38f01-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** tooopen it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="38f01-195">Na twee Hallo toevoegen `using` instructies Hallo boven aan het bestand onder andere Hallo Hallo `using` instructies.</span><span class="sxs-lookup"><span data-stu-id="38f01-195">Add hello following two `using` statements at hello top of hello file under hello other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="38f01-196">Toevoegen van de volgende regel code achter Hallo HALLO hallo `Application_Start` methode.</span><span class="sxs-lookup"><span data-stu-id="38f01-196">Add hello following line of code at hello end of hello `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="38f01-197">Vouw in **Solution Explorer** `App_Start` uit en dubbelklik op `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="38f01-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="38f01-199">Vervang `controller = "Home"` in de volgende code in Hallo Hallo `RegisterRoutes` methode met `controller = "Teams"` zoals weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="38f01-199">Replace `controller = "Home"` in hello following code in hello `RegisterRoutes` method with `controller = "Teams"` as shown in hello following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-hello-views"></a><span data-ttu-id="38f01-200">Hallo-weergaven configureren</span><span class="sxs-lookup"><span data-stu-id="38f01-200">Configure hello views</span></span>
1. <span data-ttu-id="38f01-201">In **Solution Explorer**, vouw Hallo **weergaven** map en klik vervolgens op Hallo **gedeelde** map uit en dubbelklik op **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="38f01-201">In **Solution Explorer**, expand hello **Views** folder and then hello **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="38f01-203">Hallo-inhoud van Hallo wijzigen `title` element en vervang `My ASP.NET Application` met `Contoso Team Stats` zoals weergegeven in Hallo voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="38f01-203">Change hello contents of hello `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in hello following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="38f01-204">In Hallo `body` sectie, Hallo eerst bijwerken `Html.ActionLink` -instructie en vervang `Application name` met `Contoso Team Stats` en vervang `Home` met `Teams`.</span><span class="sxs-lookup"><span data-stu-id="38f01-204">In hello `body` section, update hello first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="38f01-205">Voor: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="38f01-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="38f01-206">Na: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="38f01-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Codewijzigingen][cache-layout-cshtml-code]
2. <span data-ttu-id="38f01-208">Druk op **Ctrl + F5** toobuild en Voer Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-208">Press **Ctrl+F5** toobuild and run hello application.</span></span> <span data-ttu-id="38f01-209">Deze versie van de toepassing hello leest Hallo resultaten rechtstreeks uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="38f01-209">This version of hello application reads hello results directly from hello database.</span></span> <span data-ttu-id="38f01-210">Opmerking Hallo **nieuw**, **bewerken**, **Details**, en **verwijderen** acties die automatisch zijn toohello toepassing toegevoegd door Hallo **MVC 5 Controller with views, using Entity Framework** scaffold.</span><span class="sxs-lookup"><span data-stu-id="38f01-210">Note hello **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added toohello application by hello **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="38f01-211">In de volgende sectie Hallo van Hallo zelfstudie voegt u Redis-Cache toooptimize Hallo gegevens openen en bieden extra functies toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-211">In hello next section of hello tutorial you'll add Redis Cache toooptimize hello data access and provide additional features toohello application.</span></span>

![Beginnerstoepassing][cache-starter-application]

## <a name="configure-hello-application-toouse-redis-cache"></a><span data-ttu-id="38f01-213">Hallo toepassing toouse Redis-Cache configureren</span><span class="sxs-lookup"><span data-stu-id="38f01-213">Configure hello application toouse Redis Cache</span></span>
<span data-ttu-id="38f01-214">In deze sectie van de zelfstudie hello, past u Hallo voorbeeld toepassing toostore configureren en ophalen van de Contoso-teamstatistieken uit een Azure Redis-Cache-exemplaar met behulp van Hallo [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cacheclient.</span><span class="sxs-lookup"><span data-stu-id="38f01-214">In this section of hello tutorial, you'll configure hello sample application toostore and retrieve Contoso team statistics from an Azure Redis Cache instance by using hello [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="38f01-215">Hallo toepassing toouse StackExchange.Redis configureren</span><span class="sxs-lookup"><span data-stu-id="38f01-215">Configure hello application toouse StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="38f01-216">Hallo TeamsController klasse tooreturn resultaten uit Hallo cache of Hallo-database bijwerken</span><span class="sxs-lookup"><span data-stu-id="38f01-216">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="38f01-217">Hallo maken, bewerken, bijwerken en verwijderen van de methoden toowork met Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="38f01-217">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="38f01-218">Hallo Teamindex weergave toowork bijwerken met Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="38f01-218">Update hello Teams Index view toowork with hello cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-hello-application-toouse-stackexchangeredis"></a><span data-ttu-id="38f01-219">Hallo toepassing toouse StackExchange.Redis configureren</span><span class="sxs-lookup"><span data-stu-id="38f01-219">Configure hello application toouse StackExchange.Redis</span></span>
1. <span data-ttu-id="38f01-220">tooconfigure een clienttoepassing in Visual Studio met Hallo NuGet-pakket StackExchange.Redis, klikt u op **NuGet Package Manager**, **Package Manager Console** van Hallo **extra** menu.</span><span class="sxs-lookup"><span data-stu-id="38f01-220">tooconfigure a client application in Visual Studio using hello StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from hello **Tools** menu.</span></span>
2. <span data-ttu-id="38f01-221">Voer hello na de opdracht van Hallo `Package Manager Console` venster.</span><span class="sxs-lookup"><span data-stu-id="38f01-221">Run hello following command from hello `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="38f01-222">assembly-verwijzingen Hallo NuGet-pakket downloadt en voegt Hallo vereist voor uw client-toepassing tooaccess Azure Redis-Cache met Hallo StackExchange.Redis cacheclient.</span><span class="sxs-lookup"><span data-stu-id="38f01-222">hello NuGet package downloads and adds hello required assembly references for your client application tooaccess Azure Redis Cache with hello StackExchange.Redis cache client.</span></span> <span data-ttu-id="38f01-223">Als u liever een versie met sterke naam Hallo toouse `StackExchange.Redis` clientbibliotheek, installatie Hallo `StackExchange.Redis.StrongName` pakket.</span><span class="sxs-lookup"><span data-stu-id="38f01-223">If you prefer toouse a strong-named version of hello `StackExchange.Redis` client library, install hello `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="38f01-224">In **Solution Explorer**, vouw Hallo **domeincontrollers** map en dubbelklik op **TeamsController.cs** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="38f01-224">In **Solution Explorer**, expand hello **Controllers** folder and double-click **TeamsController.cs** tooopen it.</span></span>
   
    ![TeamsController][cache-teamscontroller]
4. <span data-ttu-id="38f01-226">Na twee Hallo toevoegen `using` instructies te**TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="38f01-226">Add hello following two `using` statements too**TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="38f01-227">Toevoegen van de volgende twee eigenschappen toohello Hallo `TeamsController` klasse.</span><span class="sxs-lookup"><span data-stu-id="38f01-227">Add hello following two properties toohello `TeamsController` class.</span></span>

    ```c#   
    // Redis Connection string info
    private static Lazy<ConnectionMultiplexer> lazyConnection = new Lazy<ConnectionMultiplexer>(() =>
    {
        string cacheConnection = ConfigurationManager.AppSettings["CacheConnection"].ToString();
        return ConnectionMultiplexer.Connect(cacheConnection);
    });
    
    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }
    ```

6. <span data-ttu-id="38f01-228">Maak een bestand op uw computer met de naam `WebAppPlusCacheAppSecrets.config` en plaats deze in een locatie die niet wordt ingecheckt met Hallo broncode van uw voorbeeldtoepassing, mocht u toocheck besluiten deze ergens in.</span><span class="sxs-lookup"><span data-stu-id="38f01-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with hello source code of your sample application, should you decide toocheck it in somewhere.</span></span> <span data-ttu-id="38f01-229">In dit voorbeeld Hallo `AppSettingsSecrets.config` bestand bevindt zich op `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="38f01-229">In this example hello `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="38f01-230">Hallo bewerken `WebAppPlusCacheAppSecrets.config` bestand en voeg Hallo inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="38f01-230">Edit hello `WebAppPlusCacheAppSecrets.config` file and add hello following contents.</span></span> <span data-ttu-id="38f01-231">Als u de toepassing hello lokaal uitvoert is deze informatie gebruikt tooconnect tooyour Azure Redis-Cache-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="38f01-231">If you run hello application locally this information is used tooconnect tooyour Azure Redis Cache instance.</span></span> <span data-ttu-id="38f01-232">Verderop in de zelfstudie Hallo u inrichten van een Azure Redis-Cache-exemplaar en Hallo-cache en het wachtwoord bijwerken.</span><span class="sxs-lookup"><span data-stu-id="38f01-232">Later in hello tutorial you'll provision an Azure Redis Cache instance and update hello cache name and password.</span></span> <span data-ttu-id="38f01-233">Als u niet van plan toorun Hallo-voorbeeldtoepassing bent lokaal u Hallo maken van dit bestand kunt overslaan en Hallo hierop volgende stappen die verwijzen naar Hallo-bestand, omdat wanneer u tooAzure Hallo toepassing implementeert Hallo cache verbindingsgegevens opgehaald uit Hallo app instelling voor Hallo Web-App en niet uit dit bestand.</span><span class="sxs-lookup"><span data-stu-id="38f01-233">If you don't plan toorun hello sample application locally you can skip hello creation of this file and hello subsequent steps that reference hello file, because when you deploy tooAzure hello application retrieves hello cache connection information from hello app setting for hello Web App and not from this file.</span></span> <span data-ttu-id="38f01-234">Sinds Hallo `WebAppPlusCacheAppSecrets.config` niet is geïmplementeerd tooAzure met uw toepassing hoeft tenzij u toorun Hallo toepassing lokaal gaat.</span><span class="sxs-lookup"><span data-stu-id="38f01-234">Since hello `WebAppPlusCacheAppSecrets.config` is not deployed tooAzure with your application, you don't need it unless you are going toorun hello application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="38f01-235">In **Solution Explorer**, dubbelklikt u op **web.config** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="38f01-235">In **Solution Explorer**, double-click **web.config** tooopen it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="38f01-237">Voeg de volgende Hallo `file` toohello kenmerk `appSettings` element.</span><span class="sxs-lookup"><span data-stu-id="38f01-237">Add hello following `file` attribute toohello `appSettings` element.</span></span> <span data-ttu-id="38f01-238">Als u een andere naam of locatie gebruikt, vervangen door deze waarden Hallo die wordt weergegeven in Hallo voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="38f01-238">If you used a different file name or location, substitute those values for hello ones shown in hello example.</span></span>
   
   * <span data-ttu-id="38f01-239">Voor: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="38f01-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="38f01-240">Na: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="38f01-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="38f01-241">Hallo ASP.NET-runtime voegt Hallo inhoud van extern bestand met aantekeningen in Hallo HALLO hallo samen `<appSettings>` element.</span><span class="sxs-lookup"><span data-stu-id="38f01-241">hello ASP.NET runtime merges hello contents of hello external file with hello markup in hello `<appSettings>` element.</span></span> <span data-ttu-id="38f01-242">Hallo runtime negeert Hallo file-kenmerk als Hallo opgegeven bestand kan niet worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="38f01-242">hello runtime ignores hello file attribute if hello specified file cannot be found.</span></span> <span data-ttu-id="38f01-243">Uw geheimen (Hallo verbinding tooyour tekenreekscache) zijn niet opgenomen als onderdeel van de broncode Hallo voor Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-243">Your secrets (hello connection string tooyour cache) are not included as part of hello source code for hello application.</span></span> <span data-ttu-id="38f01-244">Wanneer u uw web-app tooAzure implementeert, Hallo `WebAppPlusCacheAppSecrests.config` bestand niet geïmplementeerd (dat wil zeggen naar wens).</span><span class="sxs-lookup"><span data-stu-id="38f01-244">When you deploy your web app tooAzure, hello `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="38f01-245">Er zijn verschillende manieren toospecify deze geheime gegevens in Azure, en in deze zelfstudie ze zijn geconfigureerd automatisch voor u wanneer u [inrichten hello Azure-resources](#provision-the-azure-resources) in een latere stap van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38f01-245">There are several ways toospecify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision hello Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="38f01-246">Zie voor meer informatie over het werken met geheimen in Azure [aanbevolen procedures voor het implementeren van wachtwoorden en andere gevoelige gegevens tooASP.NET en Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span><span class="sxs-lookup"><span data-stu-id="38f01-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data tooASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-hello-teamscontroller-class-tooreturn-results-from-hello-cache-or-hello-database"></a><span data-ttu-id="38f01-247">Hallo TeamsController klasse tooreturn resultaten uit Hallo cache of Hallo-database bijwerken</span><span class="sxs-lookup"><span data-stu-id="38f01-247">Update hello TeamsController class tooreturn results from hello cache or hello database</span></span>
<span data-ttu-id="38f01-248">In dit voorbeeld kunnen teamstatistieken uit de database Hallo of uit de cache Hallo worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="38f01-248">In this sample, team statistics can be retrieved from hello database or from hello cache.</span></span> <span data-ttu-id="38f01-249">Teamstatistieken worden opgeslagen in cache als een geserialiseerde Hallo `List<Team>`, en ook als een gesorteerde set met Redis-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="38f01-249">Team statistics are stored in hello cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="38f01-250">Bij het ophalen van items uit een gesorteerde set kunt u een query uitvoeren voor sommige items, voor alle items of alleen voor bepaalde items.</span><span class="sxs-lookup"><span data-stu-id="38f01-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="38f01-251">In dit voorbeeld voert u een query Hallo gesorteerd set voor Hallo bovenste 5 teams door het aantal wins gerangschikt.</span><span class="sxs-lookup"><span data-stu-id="38f01-251">In this sample you'll query hello sorted set for hello top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="38f01-252">Het is niet vereist toostore hello teamstatistieken in verschillende indelingen in de cache Hallo in volgorde toouse Azure Redis-Cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-252">It is not required toostore hello team statistics in multiple formats in hello cache in order toouse Azure Redis Cache.</span></span> <span data-ttu-id="38f01-253">Deze zelfstudie wordt gebruikgemaakt van meerdere indelingen toodemonstrate enkele van de verschillende manieren Hallo en verschillende gegevenstypen kunt u toocache gegevens.</span><span class="sxs-lookup"><span data-stu-id="38f01-253">This tutorial uses multiple formats toodemonstrate some of hello different ways and different data types you can use toocache data.</span></span>
> 
> 

1. <span data-ttu-id="38f01-254">Voeg de volgende Hallo `using` instructies toohello `TeamsController.cs` bestand boven Hallo Hello andere `using` instructies.</span><span class="sxs-lookup"><span data-stu-id="38f01-254">Add hello following `using` statements toohello `TeamsController.cs` file at hello top with hello other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="38f01-255">Hallo huidige vervangen `public ActionResult Index()` methode-implementatie met Hallo na implementatie.</span><span class="sxs-lookup"><span data-stu-id="38f01-255">Replace hello current `public ActionResult Index()` method implementation with hello following implementation.</span></span>

    ```c#
    // GET: Teams
    public ActionResult Index(string actionType, string resultType)
    {
        List<Team> teams = null;

        switch(actionType)
        {
            case "playGames": // Play a new season of games.
                PlayGames();
                break;

            case "clearCache": // Clear hello results from hello cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild hello database with sample data.
                RebuildDB();
                break;
        }

        // Measure hello time it takes tooretrieve hello results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve hello top 5 teams from hello sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from hello cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from hello database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add hello elapsed time of hello operation toohello ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="38f01-256">Toevoegen van de volgende drie methoden toohello hello `TeamsController` klasse tooimplement hello `playGames`, `clearCache`, en `rebuildDB` actietypen van Hallo instructie toegevoegd in het vorige codefragment Hallo switch.</span><span class="sxs-lookup"><span data-stu-id="38f01-256">Add hello following three methods toohello `TeamsController` class tooimplement hello `playGames`, `clearCache`, and `rebuildDB` action types from hello switch statement added in hello previous code snippet.</span></span>
   
    <span data-ttu-id="38f01-257">Hallo `PlayGames` methode Hallo teamstatistieken bijgewerkt door een seizoen wedstrijden te simuleren, slaat Hallo resultaten toohello database en wist Hallo nu verouderde gegevens uit de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-257">hello `PlayGames` method updates hello team statistics by simulating a season of games, saves hello results toohello database, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void PlayGames()
    {
        ViewBag.msg += "Updating team statistics. ";
        // Play a "season" of games.
        var teams = from t in db.Teams
                    select t;

        Team.PlayGames(teams);

        db.SaveChanges();

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="38f01-258">Hallo `RebuildDB` methode opnieuw Hallo database met Hallo standaardset teams, genereert statistieken voor ze en wist Hallo nu verouderde gegevens uit de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-258">hello `RebuildDB` method reinitializes hello database with hello default set of teams, generates statistics for them, and clears hello now outdated data from hello cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize hello database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="38f01-259">Hallo `ClearCachedTeams` methode verwijdert opgeslagen teamstatistieken uit de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-259">hello `ClearCachedTeams` method removes any cached team statistics from hello cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="38f01-260">Toevoegen van de volgende vier methoden toohello hello `TeamsController` klasse tooimplement Hallo verschillende manieren voor het ophalen van teamstatistieken Hallo van Hallo-cache en Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="38f01-260">Add hello following four methods toohello `TeamsController` class tooimplement hello various ways of retrieving hello team statistics from hello cache and hello database.</span></span> <span data-ttu-id="38f01-261">Elk van deze methoden retourneert een `List<Team>` die vervolgens door Hallo weergave wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="38f01-261">Each of these methods returns a `List<Team>` which is then displayed by hello view.</span></span>
   
    <span data-ttu-id="38f01-262">Hallo `GetFromDB` methode leest de teamstatistieken Hallo uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="38f01-262">hello `GetFromDB` method reads hello team statistics from hello database.</span></span>
   
    ```c#
    List<Team> GetFromDB()
    {
        ViewBag.msg += "Results read from DB. ";
        var results = from t in db.Teams
            orderby t.Wins descending
            select t; 

        return results.ToList<Team>();
    }
    ```

    <span data-ttu-id="38f01-263">Hallo `GetFromList` methode leest de teamstatistieken Hallo uit de cache als een geserialiseerde `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="38f01-263">hello `GetFromList` method reads hello team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="38f01-264">Als er een cache ontbreekt, worden Hallo teamstatistieken gelezen uit de database Hallo en vervolgens in Hallo cache zijn opgeslagen voor later.</span><span class="sxs-lookup"><span data-stu-id="38f01-264">If there is a cache miss, hello team statistics are read from hello database and then stored in hello cache for next time.</span></span> <span data-ttu-id="38f01-265">In dit voorbeeld we maken gebruik van JSON.NET-serialisatie tooserialize Hallo .NET-objecten tooand uit Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-265">In this sample we're using JSON.NET serialization tooserialize hello .NET objects tooand from hello cache.</span></span> <span data-ttu-id="38f01-266">Zie voor meer informatie [hoe toowork met .NET-objecten in Azure Redis-Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span><span class="sxs-lookup"><span data-stu-id="38f01-266">For more information, see [How toowork with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

    ```c#
    List<Team> GetFromList()
    {
        List<Team> teams = null;

        IDatabase cache = Connection.GetDatabase();
        string serializedTeams = cache.StringGet("teamsList");
        if (!String.IsNullOrEmpty(serializedTeams))
        {
            teams = JsonConvert.DeserializeObject<List<Team>>(serializedTeams);

            ViewBag.msg += "List read from cache. ";
        }
        else
        {
            ViewBag.msg += "Teams list cache miss. ";
            // Get from database and store in cache
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="38f01-267">Hallo `GetFromSortedSet` methode leest de teamstatistieken Hallo uit een in cache opgeslagen gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="38f01-267">hello `GetFromSortedSet` method reads hello team statistics from a cached sorted set.</span></span> <span data-ttu-id="38f01-268">Als er een cache ontbreekt, worden teamstatistieken Hallo Hallo-database niet lezen en opgeslagen in de cache Hallo als een gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="38f01-268">If there is a cache miss, hello team statistics are read from hello database and stored in hello cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", order: Order.Descending);
        if (teamsSortedSet.Count() > 0)
        {
            ViewBag.msg += "Reading sorted set from cache. ";
            teams = new List<Team>();
            foreach (var t in teamsSortedSet)
            {
                Team tt = JsonConvert.DeserializeObject<Team>(t.Element);
                teams.Add(tt);
            }
        }
        else
        {
            ViewBag.msg += "Teams sorted set cache miss. ";

            // Read from DB
            teams = GetFromDB();

            ViewBag.msg += "Storing results toocache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding toosorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="38f01-269">Hallo `GetFromSortedSetTop5` methode leest Hallo bovenste 5 teams van Hallo in de cache opgeslagen gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="38f01-269">hello `GetFromSortedSetTop5` method reads hello top 5 teams from hello cached sorted set.</span></span> <span data-ttu-id="38f01-270">Deze methode begint met het Hallo-cache controleren voor Hallo bestaan Hallo `teamsSortedSet` sleutel.</span><span class="sxs-lookup"><span data-stu-id="38f01-270">It starts by checking hello cache for hello existence of hello `teamsSortedSet` key.</span></span> <span data-ttu-id="38f01-271">Als deze sleutel niet aanwezig is, Hallo `GetFromSortedSet` methode tooread hello teamstatistieken wordt genoemd en op te slaan in Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-271">If this key is not present, hello `GetFromSortedSet` method is called tooread hello team statistics and store them in hello cache.</span></span> <span data-ttu-id="38f01-272">Vervolgens hello in de cache opgeslagen gesorteerde set gevraagd voor Hallo bovenste 5 teams die worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="38f01-272">Next, hello cached sorted set is queried for hello top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If hello key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load hello entire sorted set into hello cache.
            GetFromSortedSet();

            // Retrieve hello top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get hello top 5 teams from hello sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-hello-create-edit-and-delete-methods-toowork-with-hello-cache"></a><span data-ttu-id="38f01-273">Hallo maken, bewerken, bijwerken en verwijderen van de methoden toowork met Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="38f01-273">Update hello Create, Edit, and Delete methods toowork with hello cache</span></span>
<span data-ttu-id="38f01-274">Hallo ondersteuningscode die is gegenereerd als onderdeel van dit voorbeeld bevat de methoden tooadd, bewerken en verwijderen van teams.</span><span class="sxs-lookup"><span data-stu-id="38f01-274">hello scaffolding code that was generated as part of this sample includes methods tooadd, edit, and delete teams.</span></span> <span data-ttu-id="38f01-275">Telkens wanneer een team wordt toegevoegd, bewerkt of verwijderd, verouderd Hallo-gegevens in Hallo cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-275">Anytime a team is added, edited, or removed, hello data in hello cache becomes outdated.</span></span> <span data-ttu-id="38f01-276">In deze sectie u bewerkt deze drie methoden tooclear Hallo in cache opgeslagen teams zodat Hallo-cache is niet synchroon met Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="38f01-276">In this section you'll modify these three methods tooclear hello cached teams so that hello cache won't be out of sync with hello database.</span></span>

1. <span data-ttu-id="38f01-277">Blader toohello `Create(Team team)` methode in Hallo `TeamsController` klasse.</span><span class="sxs-lookup"><span data-stu-id="38f01-277">Browse toohello `Create(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="38f01-278">Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-278">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Create
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="38f01-279">Blader toohello `Edit(Team team)` methode in Hallo `TeamsController` klasse.</span><span class="sxs-lookup"><span data-stu-id="38f01-279">Browse toohello `Edit(Team team)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="38f01-280">Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-280">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // tooprotect from overposting attacks, please enable hello specific properties you want toobind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, hello cache is out of date.
            // Clear hello cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="38f01-281">Blader toohello `DeleteConfirmed(int id)` methode in Hallo `TeamsController` klasse.</span><span class="sxs-lookup"><span data-stu-id="38f01-281">Browse toohello `DeleteConfirmed(int id)` method in hello `TeamsController` class.</span></span> <span data-ttu-id="38f01-282">Voeg een aanroep van toohello `ClearCachedTeams` methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-282">Add a call toohello `ClearCachedTeams` method, as shown in hello following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, hello cache is out of date.
        // Clear hello cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-hello-teams-index-view-toowork-with-hello-cache"></a><span data-ttu-id="38f01-283">Hallo Teamindex weergave toowork bijwerken met Hallo-cache</span><span class="sxs-lookup"><span data-stu-id="38f01-283">Update hello Teams Index view toowork with hello cache</span></span>
1. <span data-ttu-id="38f01-284">In **Solution Explorer**, vouw Hallo **weergaven** map en klik vervolgens Hallo **Teams** map uit en dubbelklik op **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="38f01-284">In **Solution Explorer**, expand hello **Views** folder, then hello **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="38f01-286">Aan de bovenkant van de Hallo van Hallo-bestand, zoek naar Hallo volgende alinea-element.</span><span class="sxs-lookup"><span data-stu-id="38f01-286">Near hello top of hello file, look for hello following paragraph element.</span></span>
   
    ![Actietabel][cache-teams-index-table]
   
    <span data-ttu-id="38f01-288">Dit is Hallo koppeling toocreate een nieuw team.</span><span class="sxs-lookup"><span data-stu-id="38f01-288">This is hello link toocreate a new team.</span></span> <span data-ttu-id="38f01-289">Hallo alinea-element met de volgende tabel Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="38f01-289">Replace hello paragraph element with hello following table.</span></span> <span data-ttu-id="38f01-290">Deze tabel bevat Actiekoppelingen voor het maken van een nieuw team, een nieuw seizoen wedstrijden, Hallo cache wissen spelen, Hallo teams ophalen uit de cache Hallo in verschillende indelingen, Hallo teams ophalen uit de database Hallo en opnieuw opbouwen van de database met de nieuwe voorbeeldgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-290">This table has action links for creating a new team, playing a new season of games, clearing hello cache, retrieving hello teams from hello cache in several formats, retrieving hello teams from hello database, and rebuilding hello database with fresh sample data.</span></span>

    ```html
    <table class="table">
        <tr>
            <td>
                @Html.ActionLink("Create New", "Create")
            </td>
            <td>
                @Html.ActionLink("Play Season", "Index", new { actionType = "playGames" })
            </td>
            <td>
                @Html.ActionLink("Clear Cache", "Index", new { actionType = "clearCache" })
            </td>
            <td>
                @Html.ActionLink("List from Cache", "Index", new { resultType = "teamsList" })
            </td>
            <td>
                @Html.ActionLink("Sorted Set from Cache", "Index", new { resultType = "teamsSortedSet" })
            </td>
            <td>
                @Html.ActionLink("Top 5 Teams from Cache", "Index", new { resultType = "teamsSortedSetTop5" })
            </td>
            <td>
                @Html.ActionLink("Load from DB", "Index", new { resultType = "fromDB" })
            </td>
            <td>
                @Html.ActionLink("Rebuild DB", "Index", new { actionType = "rebuildDB" })
            </td>
        </tr>    
    </table>
    ```


1. <span data-ttu-id="38f01-291">Scroll toohello onderaan Hallo **Index.cshtml** -bestand en voeg de volgende Hallo `tr` element zodat deze de laatste rij Hallo in Hallo laatste tabel in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="38f01-291">Scroll toohello bottom of hello **Index.cshtml** file and add hello following `tr` element so that it is hello last row in hello last table in hello file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="38f01-292">Deze rij geeft de waarde van Hallo `ViewBag.Msg` die een statusrapport over de huidige bewerking Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="38f01-292">This row displays hello value of `ViewBag.Msg` which contains a status report about hello current operation.</span></span> <span data-ttu-id="38f01-293">Hallo `ViewBag.Msg` wanneer u klikt op een van de Actiekoppelingen Hallo van de vorige stap Hallo is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="38f01-293">hello `ViewBag.Msg` is set when you click any of hello action links from hello previous step.</span></span>   
   
    ![Statusbericht][cache-status-message]
2. <span data-ttu-id="38f01-295">Druk op **F6** toobuild Hallo project.</span><span class="sxs-lookup"><span data-stu-id="38f01-295">Press **F6** toobuild hello project.</span></span>

## <a name="provision-hello-azure-resources"></a><span data-ttu-id="38f01-296">Inrichten hello Azure-resources</span><span class="sxs-lookup"><span data-stu-id="38f01-296">Provision hello Azure resources</span></span>
<span data-ttu-id="38f01-297">toohost uw toepassing in Azure, moet u eerst inrichten hello Azure-services die vereist zijn voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-297">toohost your application in Azure, you must first provision hello Azure services that your application requires.</span></span> <span data-ttu-id="38f01-298">Hallo-voorbeeldtoepassing in deze zelfstudie maakt gebruik van hello Azure-services te volgen.</span><span class="sxs-lookup"><span data-stu-id="38f01-298">hello sample application in this tutorial uses hello following Azure services.</span></span>

* <span data-ttu-id="38f01-299">Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="38f01-299">Azure Redis Cache</span></span>
* <span data-ttu-id="38f01-300">App Service-web-app</span><span class="sxs-lookup"><span data-stu-id="38f01-300">App Service Web App</span></span>
* <span data-ttu-id="38f01-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="38f01-301">SQL Database</span></span>

<span data-ttu-id="38f01-302">toodeploy deze services tooa nieuwe of bestaande resourcegroep naar keuze, klikt u op volgende Hallo **tooAzure implementeren** knop.</span><span class="sxs-lookup"><span data-stu-id="38f01-302">toodeploy these services tooa new or existing resource group of your choice, click hello following **Deploy tooAzure** button.</span></span>

<span data-ttu-id="38f01-303">[! [TooAzure implementeren] [deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="38f01-303">[![Deploy tooAzure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="38f01-304">Dit **implementeren tooAzure** knop gebruikt Hallo [maken van een Web-App plus Redis-Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) sjabloon tooprovision deze services en een set Hallo de verbindingsreeks voor Hallo SQL-Database en Hallo toepassingsinstelling voor hello Azure Redis-Cache-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="38f01-304">This **Deploy tooAzure** button uses hello [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template tooprovision these services and set hello connection string for hello SQL Database and hello application setting for hello Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="38f01-305">Als u geen Azure-account hebt, kunt u binnen een paar minuten [een gratis Azure-account maken](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="38f01-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="38f01-306">Te klikken op Hallo **tooAzure implementeren** knop gaat u verder toohello Azure-portal en initieert Hallo Hallo resources beschreven door Hallo-sjabloon maken.</span><span class="sxs-lookup"><span data-stu-id="38f01-306">Clicking hello **Deploy tooAzure** button takes you toohello Azure portal and initiates hello process of creating hello resources described by hello template.</span></span>

![TooAzure implementeren][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="38f01-308">In Hallo **basisbeginselen** sectie Selecteer toouse hello Azure-abonnement, en selecteer een bestaande resourcegroep of maak een nieuwe, en geef Hallo locatie voor resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="38f01-308">In hello **Basics** section, select hello Azure subscription toouse, and select an existing resource group or create a new one, and specify hello resource group location.</span></span>
2. <span data-ttu-id="38f01-309">In Hallo **instellingen** sectie, geeft u een **aanmeldingsnaam van de beheerder** (gebruik geen **admin**), **beheerderswachtwoord voor aanmelding**, en  **Databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="38f01-309">In hello **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="38f01-310">Hallo zijn andere parameters geconfigureerd voor een gratis App Service-hostingplan en goedkoper opties voor Hallo SQL-Database en Azure Redis-Cache, die niet geleverd met een gratis laag.</span><span class="sxs-lookup"><span data-stu-id="38f01-310">hello other parameters are configured for a free App Service hosting plan, and lower-cost options for hello SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![TooAzure implementeren][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="38f01-312">Ga na het configureren van instellingen Hallo gewenst toohello einde van de pagina Hallo lezen Hallo en voorwaarden en Hallo controleren **ik ga akkoord toohello voorwaarden bovengenoemde** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="38f01-312">After configuring hello desired settings, scroll toohello end of hello page, read hello terms and conditions, and check hello **I agree toohello terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="38f01-313">toobegin inrichting Hallo resources, klikt u op **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="38f01-313">toobegin provisioning hello resources, click **Purchase**.</span></span>

<span data-ttu-id="38f01-314">tooview hello voortgang van uw implementatie, klik op het pictogram in systeemvak Hallo en op **implementatie gestart**.</span><span class="sxs-lookup"><span data-stu-id="38f01-314">tooview hello progress of your deployment, click hello notification icon and click **Deployment started**.</span></span>

![Implementatie gestart][cache-deployment-started]

<span data-ttu-id="38f01-316">U kunt Hallo status van uw implementatie bekijken op Hallo **Microsoft.Template** blade.</span><span class="sxs-lookup"><span data-stu-id="38f01-316">You can view hello status of your deployment on hello **Microsoft.Template** blade.</span></span>

![TooAzure implementeren][cache-deploy-to-azure-step-3]

<span data-ttu-id="38f01-318">Bij het inrichten is voltooid, kunt u uw toepassing tooAzure vanuit Visual Studio kunt publiceren.</span><span class="sxs-lookup"><span data-stu-id="38f01-318">When provisioning is complete, you can publish your application tooAzure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="38f01-319">Eventuele fouten die optreden tijdens het inrichtingsproces Hallo worden weergegeven op Hallo **Microsoft.Template** blade.</span><span class="sxs-lookup"><span data-stu-id="38f01-319">Any errors that may occur during hello provisioning process are displayed on hello **Microsoft.Template** blade.</span></span> <span data-ttu-id="38f01-320">Veelvoorkomende fouten zijn te veel SQL Servers of te veel gratis App Service-hostingplannen per abonnement.</span><span class="sxs-lookup"><span data-stu-id="38f01-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="38f01-321">Los eventuele fouten en het Hallo-proces opnieuw starten door te klikken op **implementeren** op Hallo **Microsoft.Template** blade of Hallo **tooAzure implementeren** knop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38f01-321">Resolve any errors and restart hello process by clicking **Redeploy** on hello **Microsoft.Template** blade or hello **Deploy tooAzure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-hello-application-tooazure"></a><span data-ttu-id="38f01-322">Hallo toepassing tooAzure publiceren</span><span class="sxs-lookup"><span data-stu-id="38f01-322">Publish hello application tooAzure</span></span>
<span data-ttu-id="38f01-323">In deze stap van de zelfstudie Hallo u Hallo toepassing tooAzure publiceren en deze in de cloud Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="38f01-323">In this step of hello tutorial, you'll publish hello application tooAzure and run it in hello cloud.</span></span>

1. <span data-ttu-id="38f01-324">Klik met de rechtermuisknop Hallo **ContosoTeamStats** in Visual Studio-project en kies **publiceren**.</span><span class="sxs-lookup"><span data-stu-id="38f01-324">Right-click hello **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publiceren][cache-publish-app]
2. <span data-ttu-id="38f01-326">Klik op **Microsoft Azure App Service**, kies **Bestaande selecteren** en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="38f01-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publiceren][cache-publish-to-app-service]
3. <span data-ttu-id="38f01-328">Selecteer Hallo abonnement dat u gebruikt wanneer Hallo resourcegroep die Hallo resources maken hello Azure-resources, uitbreiden, en selecteer Hallo Web-App gewenst.</span><span class="sxs-lookup"><span data-stu-id="38f01-328">Select hello subscription used when creating hello Azure resources, expand hello resource group containing hello resources, and select hello desired Web App.</span></span> <span data-ttu-id="38f01-329">Als u Hallo gebruikt **implementeren tooAzure** knop de naam van uw Web-App met begint **webSite** gevolgd door een aantal extra tekens.</span><span class="sxs-lookup"><span data-stu-id="38f01-329">If you used hello **Deploy tooAzure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Web-app selecteren][cache-select-web-app]
4. <span data-ttu-id="38f01-331">Klik op **OK** toobegin Hallo publicatieproces.</span><span class="sxs-lookup"><span data-stu-id="38f01-331">Click **OK** toobegin hello publishing process.</span></span> <span data-ttu-id="38f01-332">Na enkele ogenblikken Hallo publicatieproces is voltooid en een browser wordt gestart met Hallo voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="38f01-332">After a few moments hello publishing process completes and a browser is launched with hello running sample application.</span></span> <span data-ttu-id="38f01-333">Als u een DNS-fout tijdens het valideren of publiceren en Hallo inrichtingsproces voor hello Azure-resources voor de toepassing hello is net is voltooid, wacht even en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="38f01-333">If you get a DNS error when validating or publishing, and hello provisioning process for hello Azure resources for hello application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache toegevoegd][cache-added-to-application]

<span data-ttu-id="38f01-335">Hallo beschrijft volgende tabel elke actiekoppeling in Hallo-voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-335">hello following table describes each action link from hello sample application.</span></span>

| <span data-ttu-id="38f01-336">Actie</span><span class="sxs-lookup"><span data-stu-id="38f01-336">Action</span></span> | <span data-ttu-id="38f01-337">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="38f01-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="38f01-338">Create New</span><span class="sxs-lookup"><span data-stu-id="38f01-338">Create New</span></span> |<span data-ttu-id="38f01-339">Een nieuw team maken</span><span class="sxs-lookup"><span data-stu-id="38f01-339">Create a new Team.</span></span> |
| <span data-ttu-id="38f01-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="38f01-340">Play Season</span></span> |<span data-ttu-id="38f01-341">Speel een seizoen wedstrijden, update Hallo teamstatistieken bij en wis eventuele team gegevens uit Hallo cache verouderd.</span><span class="sxs-lookup"><span data-stu-id="38f01-341">Play a season of games, update hello team stats, and clear any outdated team data from hello cache.</span></span> |
| <span data-ttu-id="38f01-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-342">Clear Cache</span></span> |<span data-ttu-id="38f01-343">Schakel Hallo teamstatistieken uit de cache Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-343">Clear hello team stats from hello cache.</span></span> |
| <span data-ttu-id="38f01-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-344">List from Cache</span></span> |<span data-ttu-id="38f01-345">Haal de teamstatistieken Hallo uit Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-345">Retrieve hello team stats from hello cache.</span></span> <span data-ttu-id="38f01-346">Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello cache opslaan voor later.</span><span class="sxs-lookup"><span data-stu-id="38f01-346">If there is a cache miss, load hello stats from hello database and save toohello cache for next time.</span></span> |
| <span data-ttu-id="38f01-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-347">Sorted Set from Cache</span></span> |<span data-ttu-id="38f01-348">Haal de teamstatistieken Hallo uit Hallo-cache met behulp van een gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="38f01-348">Retrieve hello team stats from hello cache using a sorted set.</span></span> <span data-ttu-id="38f01-349">Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello-cache met behulp van een gesorteerde set opslaan.</span><span class="sxs-lookup"><span data-stu-id="38f01-349">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="38f01-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="38f01-351">Top 5 teams Hallo ophalen uit Hallo-cache met behulp van een gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="38f01-351">Retrieve hello top 5 teams from hello cache using a sorted set.</span></span> <span data-ttu-id="38f01-352">Als er een cache ontbreekt, Hallo statistieken uit Hallo database laden en toohello-cache met behulp van een gesorteerde set opslaan.</span><span class="sxs-lookup"><span data-stu-id="38f01-352">If there is a cache miss, load hello stats from hello database and save toohello cache using a sorted set.</span></span> |
| <span data-ttu-id="38f01-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="38f01-353">Load from DB</span></span> |<span data-ttu-id="38f01-354">Haal de teamstatistieken Hallo uit Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="38f01-354">Retrieve hello team stats from hello database.</span></span> |
| <span data-ttu-id="38f01-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="38f01-355">Rebuild DB</span></span> |<span data-ttu-id="38f01-356">Hallo-database opnieuw en laad deze opnieuw met voorbeeldgegevens van het team.</span><span class="sxs-lookup"><span data-stu-id="38f01-356">Rebuild hello database and reload it with sample team data.</span></span> |
| <span data-ttu-id="38f01-357">Edit/Details/Delete</span><span class="sxs-lookup"><span data-stu-id="38f01-357">Edit / Details / Delete</span></span> |<span data-ttu-id="38f01-358">Bewerk een team, geef details van een team weer en verwijder een team.</span><span class="sxs-lookup"><span data-stu-id="38f01-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="38f01-359">Klik op een aantal Hallo acties en Experimenteer met het Hallo-gegevens ophalen uit verschillende bronnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-359">Click some of hello actions and experiment with retrieving hello data from hello different sources.</span></span> <span data-ttu-id="38f01-360">Geen Hallo verschillen in Hallo duurt toocomplete Hallo verschillende manieren voor het Hallo-gegevens ophalen uit het Hallo-database en Hallo-cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-360">Not hello differences in hello time it takes toocomplete hello various ways of retrieving hello data from hello database and hello cache.</span></span>

## <a name="delete-hello-resources-when-you-are-finished-with-hello-application"></a><span data-ttu-id="38f01-361">Hallo-resources verwijderen wanneer u klaar met de toepassing hello bent</span><span class="sxs-lookup"><span data-stu-id="38f01-361">Delete hello resources when you are finished with hello application</span></span>
<span data-ttu-id="38f01-362">Wanneer u klaar met zelfstudie voorbeeldtoepassing hello bent, kunt u hello Azure verwijderen resources die worden gebruikt in de volgorde tooconserve kosten en resources.</span><span class="sxs-lookup"><span data-stu-id="38f01-362">When you are finished with hello sample tutorial application, you can delete hello Azure resources used in order tooconserve cost and resources.</span></span> <span data-ttu-id="38f01-363">Als u Hallo **implementeren tooAzure** knop in Hallo [inrichten hello Azure-resources](#provision-the-azure-resources) sectie en al uw resources zijn opgenomen in Hallo dezelfde resourcegroep bevinden, kunt u ze verwijderen samen in één de bewerking is door het verwijderen van resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="38f01-363">If you use hello **Deploy tooAzure** button in hello [Provision hello Azure resources](#provision-the-azure-resources) section and all of your resources are contained in hello same resource group, you can delete them together in one operation by deleting hello resource group.</span></span>

1. <span data-ttu-id="38f01-364">Meld u aan toohello [Azure-portal](https://portal.azure.com) en klik op **resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="38f01-364">Sign in toohello [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="38f01-365">Hallo-typenaam van de resourcegroep in Hallo **items filteren...**  textbox.</span><span class="sxs-lookup"><span data-stu-id="38f01-365">Type hello name of your resource group into hello **Filter items...** textbox.</span></span>
3. <span data-ttu-id="38f01-366">Klik op **...**  toohello rechts van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="38f01-366">Click **...** toohello right of your resource group.</span></span>
4. <span data-ttu-id="38f01-367">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="38f01-367">Click **Delete**.</span></span>
   
    ![Verwijderen][cache-delete-resource-group]
5. <span data-ttu-id="38f01-369">Hallo-typenaam van uw resourcegroep en klik op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="38f01-369">Type hello name of your resource group and click **Delete**.</span></span>
   
    ![De verwijdering bevestigen][cache-delete-confirm]

<span data-ttu-id="38f01-371">Na enkele ogenblikken Hallo resource groep en alle ingesloten bronnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="38f01-371">After a few moments hello resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="38f01-372">Houd er rekening mee dat het verwijderen van een resourcegroep niet ongedaan worden gemaakt en Hallo resourcegroep en alle Hallo resources daarin permanent verwijderd.</span><span class="sxs-lookup"><span data-stu-id="38f01-372">Note that deleting a resource group is irreversible and that hello resource group and all hello resources in it are permanently deleted.</span></span> <span data-ttu-id="38f01-373">Zorg ervoor dat u niet per ongeluk Hallo verkeerde resourcegroep of resources verwijdert.</span><span class="sxs-lookup"><span data-stu-id="38f01-373">Make sure that you do not accidentally delete hello wrong resource group or resources.</span></span> <span data-ttu-id="38f01-374">Als u Hallo resources voor het hosten van dit voorbeeld in een bestaande resourcegroep hebt gemaakt, kunt u elke resource afzonderlijk verwijderen via hun respectievelijke blades.</span><span class="sxs-lookup"><span data-stu-id="38f01-374">If you created hello resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-hello-sample-application-on-your-local-machine"></a><span data-ttu-id="38f01-375">Hallo-voorbeeldtoepassing uitvoeren op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="38f01-375">Run hello sample application on your local machine</span></span>
<span data-ttu-id="38f01-376">toorun hello toepassing lokaal op uw computer, moet u een Azure Redis-Cache-exemplaar in welke toocache uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="38f01-376">toorun hello application locally on your machine, you need an Azure Redis Cache instance in which toocache your data.</span></span> 

* <span data-ttu-id="38f01-377">Als u kunt uw toepassing tooAzure hebt gepubliceerd, zoals beschreven in de vorige sectie hello, kunt u hello Azure Redis-Cache-exemplaar dat tijdens die stap is ingericht.</span><span class="sxs-lookup"><span data-stu-id="38f01-377">If you have published your application tooAzure as described in hello previous section, you can use hello Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="38f01-378">Als u een ander bestaand exemplaar van Azure Redis-Cache hebt, kunt u die toorun in dit voorbeeld lokaal.</span><span class="sxs-lookup"><span data-stu-id="38f01-378">If you have another existing Azure Redis Cache instance, you can use that toorun this sample locally.</span></span>
* <span data-ttu-id="38f01-379">Als u een Azure Redis-Cache-exemplaar toocreate moet, u kunt stappen Hallo in [een cache maken](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="38f01-379">If you need toocreate an Azure Redis Cache instance, you can follow hello steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="38f01-380">Zodra u hebt geselecteerd of gemaakt Hallo cache toouse, toohello cache in hello Azure-portal bladeren en ophalen van Hallo [hostnaam](cache-configure.md#properties) en [toegangssleutels](cache-configure.md#access-keys) voor uw cache.</span><span class="sxs-lookup"><span data-stu-id="38f01-380">Once you have selected or created hello cache toouse, browse toohello cache in hello Azure portal and retrieve hello [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="38f01-381">Zie [Redis-cache-instellingen configureren](cache-configure.md#configure-redis-cache-settings) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="38f01-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="38f01-382">Open Hallo `WebAppPlusCacheAppSecrets.config` -bestand dat u hebt gemaakt tijdens het Hallo [Hallo toepassing toouse Redis-Cache configureren](#configure-the-application-to-use-redis-cache) stap van deze zelfstudie met Hallo-editor van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="38f01-382">Open hello `WebAppPlusCacheAppSecrets.config` file that you created during hello [Configure hello application toouse Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using hello editor of your choice.</span></span>
2. <span data-ttu-id="38f01-383">Hallo bewerken `value` kenmerk en vervang `MyCache.redis.cache.windows.net` Hello [hostnaam](cache-configure.md#properties) van de cache en Geef ofwel Hallo [primaire of secundaire sleutel](cache-configure.md#access-keys) van de cache als Hallo wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="38f01-383">Edit hello `value` attribute and replace `MyCache.redis.cache.windows.net` with hello [host name](cache-configure.md#properties) of your cache, and specify either hello [primary or secondary key](cache-configure.md#access-keys) of your cache as hello password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="38f01-384">Druk op **Ctrl + F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="38f01-384">Press **Ctrl+F5** toorun hello application.</span></span>

> [!NOTE]
> <span data-ttu-id="38f01-385">Let op: omdat Hallo toepassing, met inbegrip van Hallo-database lokaal wordt uitgevoerd en hello Redis-Cache wordt gehost in Azure, Hallo cache lijkt toounder-Hallo database uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="38f01-385">Note that because hello application, including hello database, is running locally and hello Redis Cache is hosted in Azure, hello cache may appear toounder-perform hello database.</span></span> <span data-ttu-id="38f01-386">Voor de beste prestaties Hallo-clienttoepassing en Azure Redis-Cache-exemplaar moet Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="38f01-386">For best performance, hello client application and Azure Redis Cache instance should be in hello same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="38f01-387">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="38f01-387">Next steps</span></span>
* <span data-ttu-id="38f01-388">Meer informatie over [aan de slag met ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) op Hallo [ASP.NET](http://asp.net/) site.</span><span class="sxs-lookup"><span data-stu-id="38f01-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on hello [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="38f01-389">Zie voor meer voorbeelden van het maken van een ASP.NET-Web-App in App Service [maken en implementeren van een ASP.NET-web-app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) van Hallo [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span><span class="sxs-lookup"><span data-stu-id="38f01-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from hello [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="38f01-390">Zie voor meer snelstartgidsen van Hallo HealthClinic.biz demo [Azure Developer Tools snelstartgidsen](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="38f01-390">For more quickstarts from hello HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="38f01-391">Meer informatie over Hallo [Code eerste tooa nieuwe database](https://msdn.microsoft.com/data/jj193542) benaderen tooEntity Framework die wordt gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="38f01-391">Learn more about hello [Code first tooa new database](https://msdn.microsoft.com/data/jj193542) approach tooEntity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="38f01-392">Meer informatie over [web-apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38f01-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="38f01-393">Meer informatie over hoe te[monitor](cache-how-to-monitor.md) uw cache in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="38f01-393">Learn how too[monitor](cache-how-to-monitor.md) your cache in hello Azure portal.</span></span>
* <span data-ttu-id="38f01-394">De premiumfuncties van de Azure Redis-cache verkennen</span><span class="sxs-lookup"><span data-stu-id="38f01-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="38f01-395">Hoe tooconfigure persistentie voor een Premium Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-395">How tooconfigure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="38f01-396">Hoe tooconfigure clustering voor een Premium Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-396">How tooconfigure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="38f01-397">Hoe tooconfigure Virtual Network-ondersteuning voor een Premium Azure Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="38f01-397">How tooconfigure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="38f01-398">Zie Hallo [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches.</span><span class="sxs-lookup"><span data-stu-id="38f01-398">See hello [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

<!-- IMAGES -->
[cache-starter-application]: ./media/cache-web-app-howto/cache-starter-application.png
[cache-added-to-application]: ./media/cache-web-app-howto/cache-added-to-application.png
[cache-create-project]: ./media/cache-web-app-howto/cache-create-project.png
[cache-select-template]: ./media/cache-web-app-howto/cache-select-template.png
[cache-model-add-class]: ./media/cache-web-app-howto/cache-model-add-class.png
[cache-model-add-class-dialog]: ./media/cache-web-app-howto/cache-model-add-class-dialog.png
[cache-add-controller]: ./media/cache-web-app-howto/cache-add-controller.png
[cache-add-controller-class]: ./media/cache-web-app-howto/cache-add-controller-class.png
[cache-configure-controller]: ./media/cache-web-app-howto/cache-configure-controller.png
[cache-global-asax]: ./media/cache-web-app-howto/cache-global-asax.png
[cache-RouteConfig-cs]: ./media/cache-web-app-howto/cache-RouteConfig-cs.png
[cache-layout-cshtml]: ./media/cache-web-app-howto/cache-layout-cshtml.png
[cache-layout-cshtml-code]: ./media/cache-web-app-howto/cache-layout-cshtml-code.png
[redis-cache-manage-nuget-menu]: ./media/cache-web-app-howto/redis-cache-manage-nuget-menu.png
[redis-cache-stack-exchange-nuget]: ./media/cache-web-app-howto/redis-cache-stack-exchange-nuget.png
[cache-teamscontroller]: ./media/cache-web-app-howto/cache-teamscontroller.png
[cache-web-config]: ./media/cache-web-app-howto/cache-web-config.png
[cache-views-teams-index-cshtml]: ./media/cache-web-app-howto/cache-views-teams-index-cshtml.png
[cache-teams-index-table]: ./media/cache-web-app-howto/cache-teams-index-table.png
[cache-status-message]: ./media/cache-web-app-howto/cache-status-message.png
[deploybutton]: ./media/cache-web-app-howto/deploybutton.png
[cache-deploy-to-azure-step-1]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-1.png
[cache-deploy-to-azure-step-2]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-2.png
[cache-deploy-to-azure-step-3]: ./media/cache-web-app-howto/cache-deploy-to-azure-step-3.png
[cache-deployment-started]: ./media/cache-web-app-howto/cache-deployment-started.png
[cache-publish-app]: ./media/cache-web-app-howto/cache-publish-app.png
[cache-publish-to-app-service]: ./media/cache-web-app-howto/cache-publish-to-app-service.png
[cache-select-web-app]: ./media/cache-web-app-howto/cache-select-web-app.png
[cache-publish]: ./media/cache-web-app-howto/cache-publish.png
[cache-delete-resource-group]: ./media/cache-web-app-howto/cache-delete-resource-group.png
[cache-delete-confirm]: ./media/cache-web-app-howto/cache-delete-confirm.png

