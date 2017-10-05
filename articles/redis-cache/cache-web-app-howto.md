---
title: Een web-app maken met Redis Cache | Microsoft Docs
description: Informatie over het maken van een web-app met Redis-cache
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
ms.openlocfilehash: f23f71cc01eccf17d36885f786de9a7517606803
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-create-a-web-app-with-redis-cache"></a><span data-ttu-id="53e87-103">Een web-app maken met Redis-Cache</span><span class="sxs-lookup"><span data-stu-id="53e87-103">How to create a Web App with Redis Cache</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="53e87-104">.NET</span><span class="sxs-lookup"><span data-stu-id="53e87-104">.NET</span></span>](cache-dotnet-how-to-use-azure-redis-cache.md)
> * [<span data-ttu-id="53e87-105">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="53e87-105">ASP.NET</span></span>](cache-web-app-howto.md)
> * [<span data-ttu-id="53e87-106">Node.js</span><span class="sxs-lookup"><span data-stu-id="53e87-106">Node.js</span></span>](cache-nodejs-get-started.md)
> * [<span data-ttu-id="53e87-107">Java</span><span class="sxs-lookup"><span data-stu-id="53e87-107">Java</span></span>](cache-java-get-started.md)
> * [<span data-ttu-id="53e87-108">Python</span><span class="sxs-lookup"><span data-stu-id="53e87-108">Python</span></span>](cache-python-get-started.md)
> 
> 

<span data-ttu-id="53e87-109">In deze zelfstudie ziet u hoe u een ASP.NET-webtoepassing maakt en implementeert in een web-app in Azure App Service met behulp van Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="53e87-109">This tutorial shows how to create and deploy an ASP.NET web application to a web app in Azure App Service using Visual Studio 2017.</span></span> <span data-ttu-id="53e87-110">In de voorbeeldtoepassing wordt een lijst met teamstatistieken uit een database weergegeven. U maakt kennis met verschillende manieren waarop u Azure Redis-cache kunt gebruiken om gegevens op te slaan in en op te halen uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-110">The sample application displays a list of team statistics from a database and shows different ways to use Azure Redis Cache to store and retrieve data from the cache.</span></span> <span data-ttu-id="53e87-111">Wanneer u de zelfstudie hebt voltooid, hebt u een actieve web-app die naar een database leest en schrijft. Deze web-app is geoptimaliseerd met Azure Redis-cache en wordt gehost in Azure.</span><span class="sxs-lookup"><span data-stu-id="53e87-111">When you complete the tutorial you'll have a running web app that reads and writes to a database, optimized with Azure Redis Cache, and hosted in Azure.</span></span>

<span data-ttu-id="53e87-112">U leert het volgende:</span><span class="sxs-lookup"><span data-stu-id="53e87-112">You'll learn:</span></span>

* <span data-ttu-id="53e87-113">Een ASP.NET MVC 5-webtoepassing maken in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53e87-113">How to create an ASP.NET MVC 5 web application in Visual Studio.</span></span>
* <span data-ttu-id="53e87-114">Toegang krijgen tot gegevens uit een database met behulp van Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="53e87-114">How to access data from a database using Entity Framework.</span></span>
* <span data-ttu-id="53e87-115">De doorvoer van gegevens verbeteren en de belasting van de database verminderen door gegevens op te slaan en op te halen met Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-115">How to improve data throughput and reduce database load by storing and retrieving data using Azure Redis Cache.</span></span>
* <span data-ttu-id="53e87-116">Een in Redis gesorteerde set gebruiken om de beste vijf teams op te halen.</span><span class="sxs-lookup"><span data-stu-id="53e87-116">How to use a Redis sorted set to retrieve the top 5 teams.</span></span>
* <span data-ttu-id="53e87-117">De Azure-resources voor de toepassing inrichten met een Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="53e87-117">How to provision the Azure resources for the application using a Resource Manager template.</span></span>
* <span data-ttu-id="53e87-118">De toepassing publiceren in Azure met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53e87-118">How to publish the application to Azure using Visual Studio.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53e87-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="53e87-119">Prerequisites</span></span>
<span data-ttu-id="53e87-120">U hebt het volgende nodig om deze zelfstudie te voltooien:</span><span class="sxs-lookup"><span data-stu-id="53e87-120">To complete the tutorial, you must have the following prerequisites.</span></span>

* [<span data-ttu-id="53e87-121">Azure-account</span><span class="sxs-lookup"><span data-stu-id="53e87-121">Azure account</span></span>](#azure-account)
* [<span data-ttu-id="53e87-122">Visual Studio 2017 met de Azure SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="53e87-122">Visual Studio 2017 with the Azure SDK for .NET</span></span>](#visual-studio-2017-with-the-azure-sdk-for-net)

### <a name="azure-account"></a><span data-ttu-id="53e87-123">Azure-account</span><span class="sxs-lookup"><span data-stu-id="53e87-123">Azure account</span></span>
<span data-ttu-id="53e87-124">U hebt een Azure-account nodig om deze zelfstudie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="53e87-124">You need an Azure account to complete the tutorial.</span></span> <span data-ttu-id="53e87-125">U kunt:</span><span class="sxs-lookup"><span data-stu-id="53e87-125">You can:</span></span>

* <span data-ttu-id="53e87-126">[Gratis een Azure-account openen](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="53e87-126">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="53e87-127">U ontvangt tegoed dat kan worden gebruikt om betaalde Azure-services uit te proberen.</span><span class="sxs-lookup"><span data-stu-id="53e87-127">You get credits that can be used to try out paid Azure services.</span></span> <span data-ttu-id="53e87-128">Zelfs nadat het tegoed is gebruikt, kunt u het account houden en de gratis Azure-services en -functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53e87-128">Even after the credits are used up, you can keep the account and use free Azure services and features.</span></span>
* <span data-ttu-id="53e87-129">[Uw voordelen als Visual Studio-abonnee activeren](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="53e87-129">[Activate Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=redis_cache_hero).</span></span> <span data-ttu-id="53e87-130">Via uw MSDN-abonnement ontvangt u elke maand tegoeden die u voor betaalde Azure-services kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53e87-130">Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

### <a name="visual-studio-2017-with-the-azure-sdk-for-net"></a><span data-ttu-id="53e87-131">Visual Studio 2017 met de Azure SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="53e87-131">Visual Studio 2017 with the Azure SDK for .NET</span></span>
<span data-ttu-id="53e87-132">De zelfstudie is geschreven voor Visual Studio 2017 met de [Azure-SDK voor .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span><span class="sxs-lookup"><span data-stu-id="53e87-132">The tutorial is written for Visual Studio 2017 with the [Azure SDK for .NET](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes#azuretools).</span></span> <span data-ttu-id="53e87-133">De Azure SDK 2.9.5 is opgenomen in het installatieprogramma voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53e87-133">The Azure SDK 2.9.5 is included with the Visual Studio installer.</span></span>

<span data-ttu-id="53e87-134">Als u Visual Studio 2015 hebt, kunt u de zelfstudie volgen met de [Azure SDK voor .NET](../dotnet-sdk.md) 2.8.2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="53e87-134">If you have Visual Studio 2015, you can follow the tutorial with the [Azure SDK for .NET](../dotnet-sdk.md) 2.8.2 or later.</span></span> <span data-ttu-id="53e87-135">[Download hier de nieuwste Azure-SDK voor Visual Studio 2015](http://go.microsoft.com/fwlink/?linkid=518003).</span><span class="sxs-lookup"><span data-stu-id="53e87-135">[Download the latest Azure SDK for Visual Studio 2015 here](http://go.microsoft.com/fwlink/?linkid=518003).</span></span> <span data-ttu-id="53e87-136">Als u Visual Studio nog niet hebt, wordt dit automatisch geïnstalleerd samen met de SDK.</span><span class="sxs-lookup"><span data-stu-id="53e87-136">Visual Studio is automatically installed with the SDK if you don't already have it.</span></span> <span data-ttu-id="53e87-137">Sommige schermen zien er mogelijk anders uit dan wordt weergegeven in de afbeeldingen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="53e87-137">Some screens may look different from the illustrations shown in this tutorial.</span></span>

<span data-ttu-id="53e87-138">Als u Visual Studio 2013 hebt, kunt u [de nieuwste Azure-SDK voor Visual Studio 2013 downloaden](http://go.microsoft.com/fwlink/?LinkID=324322).</span><span class="sxs-lookup"><span data-stu-id="53e87-138">If you have Visual Studio 2013, you can [download the latest Azure SDK for Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=324322).</span></span> <span data-ttu-id="53e87-139">Sommige schermen zien er mogelijk anders uit dan wordt weergegeven in de afbeeldingen in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="53e87-139">Some screens may look different from the illustrations shown in this tutorial.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="53e87-140">Het Visual Studio-project maken</span><span class="sxs-lookup"><span data-stu-id="53e87-140">Create the Visual Studio project</span></span>
1. <span data-ttu-id="53e87-141">Open Visual Studio en klik op **File**, **New**, **Project**.</span><span class="sxs-lookup"><span data-stu-id="53e87-141">Open Visual Studio and click **File**, **New**, **Project**.</span></span>
2. <span data-ttu-id="53e87-142">Vouw het knooppunt **Visual C#** uit in de lijst **Templates**, selecteer **Cloud** en klik op **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="53e87-142">Expand the **Visual C#** node in the **Templates** list, select **Cloud**, and click **ASP.NET Web Application**.</span></span> <span data-ttu-id="53e87-143">Zorg ervoor dat **.NET Framework 4.5.2** of hoger is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="53e87-143">Ensure that **.NET Framework 4.5.2** or higher is selected.</span></span>  <span data-ttu-id="53e87-144">Typ **ContosoTeamStats** in het tekstvak **Name**. Klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="53e87-144">Type **ContosoTeamStats** into the **Name** textbox and click **OK**.</span></span>
   
    ![Project maken][cache-create-project]
3. <span data-ttu-id="53e87-146">Selecteer **MVC** als het projecttype.</span><span class="sxs-lookup"><span data-stu-id="53e87-146">Select **MVC** as the project type.</span></span> 

    <span data-ttu-id="53e87-147">Zorg ervoor dat **Geen verificatie** is opgegeven voor de instellingen bij **Verificatie**.</span><span class="sxs-lookup"><span data-stu-id="53e87-147">Ensure that **No Authentication** is specified for the **Authentication** settings.</span></span> <span data-ttu-id="53e87-148">Afhankelijk van uw versie van Visual Studio kan de standaardwaarde op iets anders zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="53e87-148">Depending on your version of Visual Studio, the default may be set to something else.</span></span> <span data-ttu-id="53e87-149">Als u deze wilt wijzigen, klikt u op **Verificatie wijzigen** en selecteert u **Geen verificatie**.</span><span class="sxs-lookup"><span data-stu-id="53e87-149">To change it, click **Change Authentication** and select **No Authentication**.</span></span>

    <span data-ttu-id="53e87-150">Als u de zelfstudie volgt met Visual Studio 2015, schakel dan het selectievakje **Host in de cloud** in.</span><span class="sxs-lookup"><span data-stu-id="53e87-150">If you are following along with Visual Studio 2015, clear the **Host in the cloud** checkbox.</span></span> <span data-ttu-id="53e87-151">In de volgende stappen in deze zelfstudie [richt u de Azure-resources in](#provision-the-azure-resources) en [publiceert u de toepassing in Azure](#publish-the-application-to-azure).</span><span class="sxs-lookup"><span data-stu-id="53e87-151">You'll [provision the Azure resources](#provision-the-azure-resources) and [publish the application to Azure](#publish-the-application-to-azure) in subsequent steps in the tutorial.</span></span> <span data-ttu-id="53e87-152">Voor een voorbeeld van een App Service-web-app die is ingericht vanuit Visual Studio door **Host in the cloud** aangevinkt te laten, bekijkt u [Aan de slag met web-apps in Azure App Service met ASP.NET en Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="53e87-152">For an example of provisioning an App Service web app from Visual Studio by leaving **Host in the cloud** checked, see [Get started with Web Apps in Azure App Service, using ASP.NET and Visual Studio](../app-service-web/app-service-web-get-started-dotnet.md).</span></span>
   
    ![De projectsjabloon selecteren][cache-select-template]
4. <span data-ttu-id="53e87-154">Klik op **OK** om het project te maken.</span><span class="sxs-lookup"><span data-stu-id="53e87-154">Click **OK** to create the project.</span></span>

## <a name="create-the-aspnet-mvc-application"></a><span data-ttu-id="53e87-155">De ASP.NET MVC-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="53e87-155">Create the ASP.NET MVC application</span></span>
<span data-ttu-id="53e87-156">In dit gedeelte van de zelfstudie maakt u de basistoepassing die teamstatistieken leest en weergeeft vanuit een database.</span><span class="sxs-lookup"><span data-stu-id="53e87-156">In this section of the tutorial, you'll create the basic application that reads and displays team statistics from a database.</span></span>

* [<span data-ttu-id="53e87-157">Het Entity Framework NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-157">Add the Entity Framework NuGet package</span></span>](#add-the-entity-framework-nuget-package)
* [<span data-ttu-id="53e87-158">Het model toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-158">Add the model</span></span>](#add-the-model)
* [<span data-ttu-id="53e87-159">De controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-159">Add the controller</span></span>](#add-the-controller)
* [<span data-ttu-id="53e87-160">De weergaven configureren</span><span class="sxs-lookup"><span data-stu-id="53e87-160">Configure the views</span></span>](#configure-the-views)

### <a name="add-the-entity-framework-nuget-package"></a><span data-ttu-id="53e87-161">Het Entity Framework NuGet-pakket toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-161">Add the Entity Framework NuGet package</span></span>

1. <span data-ttu-id="53e87-162">Klik in het menu **Extra** op **NuGet Package Manager**, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="53e87-162">Click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="53e87-163">Voer de volgende opdracht uit in het venster **Pakketbeheerconsole**.</span><span class="sxs-lookup"><span data-stu-id="53e87-163">Run the following command from the **Package Manager Console** window.</span></span>
    
    ```
    Install-Package EntityFramework
    ```

<span data-ttu-id="53e87-164">Meer informatie over dit pakket vindt u op de NuGet-pagina [EntityFramework](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="53e87-164">For more information about this package, see the [EntityFramework](https://www.nuget.org/packages/EntityFramework/) NuGet page.</span></span>

### <a name="add-the-model"></a><span data-ttu-id="53e87-165">Het model toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-165">Add the model</span></span>
1. <span data-ttu-id="53e87-166">Klik in **Solution Explorer** met de rechtermuisknop op **Models** en kies **Add**, **Class**.</span><span class="sxs-lookup"><span data-stu-id="53e87-166">Right-click **Models** in **Solution Explorer**, and choose **Add**, **Class**.</span></span> 
   
    ![Het model toevoegen][cache-model-add-class]
2. <span data-ttu-id="53e87-168">Voer `Team` in als de naam van de klasse en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="53e87-168">Enter `Team` for the class name and click **Add**.</span></span>
   
    ![De modelklasse toevoegen][cache-model-add-class-dialog]
3. <span data-ttu-id="53e87-170">Vervang de `using`-instructies boven aan het bestand `Team.cs` door de volgende `using`-instructies.</span><span class="sxs-lookup"><span data-stu-id="53e87-170">Replace the `using` statements at the top of the `Team.cs` file with the following `using` statements.</span></span>

    ```c#
    using System;
    using System.Collections.Generic;
    using System.Data.Entity;
    using System.Data.Entity.SqlServer;
    ```


1. <span data-ttu-id="53e87-171">Vervang de definitie van klasse `Team` door het volgende codefragment. Dit fragment bevat een bijgewerkte definitie voor klasse `Team` en een aantal andere helperklassen van Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="53e87-171">Replace the definition of the `Team` class with the following code snippet that contains an updated `Team` class definition as well as some other Entity Framework helper classes.</span></span> <span data-ttu-id="53e87-172">Zie [Code First naar een nieuwe database](https://msdn.microsoft.com/data/jj193542) voor meer informatie over de Code First-aanpak voor Entity Framework die in deze zelfstudie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="53e87-172">For more information on the code first approach to Entity Framework that's used in this tutorial, see [Code first to a new database](https://msdn.microsoft.com/data/jj193542).</span></span>

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


1. <span data-ttu-id="53e87-173">Dubbelklik in **Solution Explorer** op **web.config** om het bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="53e87-173">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="53e87-175">Voeg de volgende `connectionStrings`-sectie toe.</span><span class="sxs-lookup"><span data-stu-id="53e87-175">Add the following `connectionStrings` section.</span></span> <span data-ttu-id="53e87-176">De naam van de verbindingsreeks moet overeenkomen met de naam van de contextklasse van de Entity Framework-database. Dit is `TeamContext`.</span><span class="sxs-lookup"><span data-stu-id="53e87-176">The name of the connection string must match the name of the Entity Framework database context class which is `TeamContext`.</span></span>

    ```xml
    <connectionStrings>
        <add name="TeamContext" connectionString="Data Source=(LocalDB)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\Teams.mdf;Integrated Security=True"     providerName="System.Data.SqlClient" />
    </connectionStrings>
    ```

    <span data-ttu-id="53e87-177">U kunt de nieuwe `connectionStrings`-sectie toevoegen zodat deze achter `configSections` staat, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-177">You can add the new `connectionStrings` section so that it follows `configSections`, as shown in the following example.</span></span>

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
    > <span data-ttu-id="53e87-178">De verbindingsreeks kan afwijken, afhankelijk van de versie van Visual Studio en de SQL Server Express-editie die zijn gebruikt voor het voltooien van de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="53e87-178">Your connection string may be different depending on the version of Visual Studio and SQL Server Express edition used to complete the tutorial.</span></span> <span data-ttu-id="53e87-179">De web.config-sjabloon moet overeenkomstig uw installatie worden geconfigureerd. Het kan `Data Source`-vermeldingen zoals `(LocalDB)\v11.0` (van SQL Server Express 2012) of `Data Source=(LocalDB)\MSSQLLocalDB` (van SQL Server Express 2014 en hoger) bevatten.</span><span class="sxs-lookup"><span data-stu-id="53e87-179">The web.config template should be configured to match your installation, and may contain `Data Source` entries like `(LocalDB)\v11.0` (from SQL Server Express 2012) or `Data Source=(LocalDB)\MSSQLLocalDB` (from SQL Server Express 2014 and newer).</span></span> <span data-ttu-id="53e87-180">Zie [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) voor meer informatie over verbindingsreeksen en SQL Express-versies.</span><span class="sxs-lookup"><span data-stu-id="53e87-180">For more information about connection strings and SQL Express versions, see [SQL Server 2016 Express LocalDB](https://docs.microsoft.com/sql/database-engine/configure-windows/sql-server-2016-express-localdb) .</span></span>

### <a name="add-the-controller"></a><span data-ttu-id="53e87-181">De controller toevoegen</span><span class="sxs-lookup"><span data-stu-id="53e87-181">Add the controller</span></span>
1. <span data-ttu-id="53e87-182">Druk op **F6** om het project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="53e87-182">Press **F6** to build the project.</span></span> 
2. <span data-ttu-id="53e87-183">Klik in **Solution Explorer** met de rechtermuisknop op de map **Controllers** en kies vervolgens **Add**, **Controller**.</span><span class="sxs-lookup"><span data-stu-id="53e87-183">In **Solution Explorer**, right-click the **Controllers** folder and choose **Add**, **Controller**.</span></span>
   
    ![Controller toevoegen][cache-add-controller]
3. <span data-ttu-id="53e87-185">Kies **MVC 5 Controller with views, using Entity Framework** en klik op **Add**.</span><span class="sxs-lookup"><span data-stu-id="53e87-185">Choose **MVC 5 Controller with views, using Entity Framework**, and click **Add**.</span></span> <span data-ttu-id="53e87-186">Als er een foutbericht wordt weergegeven nadat u op **Add** hebt geklikt, zorgt u ervoor dat u eerst het project bouwt.</span><span class="sxs-lookup"><span data-stu-id="53e87-186">If you get an error after clicking **Add**, ensure that you have built the project first.</span></span>
   
    ![Controllerklasse toevoegen][cache-add-controller-class]
4. <span data-ttu-id="53e87-188">Selecteer in de vervolgkeuzelijst **Model class** de optie **Team (ContosoTeamStats.Models)**.</span><span class="sxs-lookup"><span data-stu-id="53e87-188">Select **Team (ContosoTeamStats.Models)** from the **Model class** drop-down list.</span></span> <span data-ttu-id="53e87-189">Selecteer in de vervolgkeuzelijst **Data context class** de optie **TeamContext (ContosoTeamStats.Models)**.</span><span class="sxs-lookup"><span data-stu-id="53e87-189">Select **TeamContext (ContosoTeamStats.Models)** from the **Data context class** drop-down list.</span></span> <span data-ttu-id="53e87-190">Typ `TeamsController` in het tekstvak voor de naam van de **Controller** (als dit niet automatisch wordt ingevuld).</span><span class="sxs-lookup"><span data-stu-id="53e87-190">Type `TeamsController` in the **Controller** name textbox (if it is not automatically populated).</span></span> <span data-ttu-id="53e87-191">Klik op **Add** om de controllerklasse te maken en de standaardweergaven toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="53e87-191">Click **Add** to create the controller class and add the default views.</span></span>
   
    ![Controller configureren][cache-configure-controller]
5. <span data-ttu-id="53e87-193">Vouw in **Solution Explorer** het bestand **Global.asax** uit en dubbelklik op **Global.asax.cs** om het te openen.</span><span class="sxs-lookup"><span data-stu-id="53e87-193">In **Solution Explorer**, expand **Global.asax** and double-click **Global.asax.cs** to open it.</span></span>
   
    ![Global.asax.cs][cache-global-asax]
6. <span data-ttu-id="53e87-195">Voeg boven aan het bestand, onder de andere `using`-instructies, de volgende twee `using`-instructies toe.</span><span class="sxs-lookup"><span data-stu-id="53e87-195">Add the following two `using` statements at the top of the file under the other `using` statements.</span></span>

    ```c#
    using System.Data.Entity;
    using ContosoTeamStats.Models;
    ```


1. <span data-ttu-id="53e87-196">Voeg de volgende regel code toe aan het einde van de `Application_Start`-methode.</span><span class="sxs-lookup"><span data-stu-id="53e87-196">Add the following line of code at the end of the `Application_Start` method.</span></span>

    ```c#
    Database.SetInitializer<TeamContext>(new TeamInitializer());
    ```


1. <span data-ttu-id="53e87-197">Vouw in **Solution Explorer** `App_Start` uit en dubbelklik op `RouteConfig.cs`.</span><span class="sxs-lookup"><span data-stu-id="53e87-197">In **Solution Explorer**, expand `App_Start` and double-click `RouteConfig.cs`.</span></span>
   
    ![RouteConfig.cs][cache-RouteConfig-cs]
2. <span data-ttu-id="53e87-199">Vervang `controller = "Home"` in de volgende code in de `RegisterRoutes`-methode door `controller = "Teams"`, zoals weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-199">Replace `controller = "Home"` in the following code in the `RegisterRoutes` method with `controller = "Teams"` as shown in the following example.</span></span>

    ```c#
    routes.MapRoute(
        name: "Default",
        url: "{controller}/{action}/{id}",
        defaults: new { controller = "Teams", action = "Index", id = UrlParameter.Optional }
    );
    ```


### <a name="configure-the-views"></a><span data-ttu-id="53e87-200">De weergaven configureren</span><span class="sxs-lookup"><span data-stu-id="53e87-200">Configure the views</span></span>
1. <span data-ttu-id="53e87-201">Vouw in **Solution Explorer** de map **Views** uit. Vouw vervolgens de map **Shared** uit en dubbelklik op **_Layout.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="53e87-201">In **Solution Explorer**, expand the **Views** folder and then the **Shared** folder, and double-click **_Layout.cshtml**.</span></span> 
   
    ![_Layout.cshtml][cache-layout-cshtml]
2. <span data-ttu-id="53e87-203">Wijzig de inhoud van het element `title` en vervang `My ASP.NET Application` door `Contoso Team Stats`, zoals weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-203">Change the contents of the `title` element and replace `My ASP.NET Application` with `Contoso Team Stats` as shown in the following example.</span></span>

    ```html
    <title>@ViewBag.Title - Contoso Team Stats</title>
    ```


1. <span data-ttu-id="53e87-204">Werk in de sectie `body` de eerste instructie `Html.ActionLink` bij, vervang `Application name` door `Contoso Team Stats` en vervang `Home` door `Teams`.</span><span class="sxs-lookup"><span data-stu-id="53e87-204">In the `body` section, update the first `Html.ActionLink` statement and replace `Application name` with `Contoso Team Stats` and replace `Home` with `Teams`.</span></span>
   
   * <span data-ttu-id="53e87-205">Voor: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="53e87-205">Before: `@Html.ActionLink("Application name", "Index", "Home", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
   * <span data-ttu-id="53e87-206">Na: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span><span class="sxs-lookup"><span data-stu-id="53e87-206">After: `@Html.ActionLink("Contoso Team Stats", "Index", "Teams", new { area = "" }, new { @class = "navbar-brand" })`</span></span>
     
     ![Codewijzigingen][cache-layout-cshtml-code]
2. <span data-ttu-id="53e87-208">Druk op **Ctrl+F5** om de toepassing op te bouwen en uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="53e87-208">Press **Ctrl+F5** to build and run the application.</span></span> <span data-ttu-id="53e87-209">Deze versie van de toepassing leest de resultaten rechtstreeks uit de database.</span><span class="sxs-lookup"><span data-stu-id="53e87-209">This version of the application reads the results directly from the database.</span></span> <span data-ttu-id="53e87-210">De acties **Nieuw**, **Bewerken**, **Details** en **Verwijderen** zijn automatisch aan de toepassing toegevoegd door de structuur **MVC 5 Controller with views, using Entity Framework**.</span><span class="sxs-lookup"><span data-stu-id="53e87-210">Note the **Create New**, **Edit**, **Details**, and **Delete** actions that were automatically added to the application by the **MVC 5 Controller with views, using Entity Framework** scaffold.</span></span> <span data-ttu-id="53e87-211">In het volgende gedeelte van de zelfstudie voegt u Redis-cache toe om de gegevenstoegang te optimaliseren en om extra functies te bieden voor de toepassing.</span><span class="sxs-lookup"><span data-stu-id="53e87-211">In the next section of the tutorial you'll add Redis Cache to optimize the data access and provide additional features to the application.</span></span>

![Beginnerstoepassing][cache-starter-application]

## <a name="configure-the-application-to-use-redis-cache"></a><span data-ttu-id="53e87-213">De toepassing configureren voor het gebruik van Redis-cache</span><span class="sxs-lookup"><span data-stu-id="53e87-213">Configure the application to use Redis Cache</span></span>
<span data-ttu-id="53e87-214">In dit gedeelte van de zelfstudie configureert u de voorbeeldtoepassing om met behulp van de cacheclient [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) Contoso-teamstatistieken op te slaan en op te halen uit een exemplaar van de Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-214">In this section of the tutorial, you'll configure the sample application to store and retrieve Contoso team statistics from an Azure Redis Cache instance by using the [StackExchange.Redis](https://github.com/StackExchange/StackExchange.Redis) cache client.</span></span>

* [<span data-ttu-id="53e87-215">De toepassing configureren voor gebruik van StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="53e87-215">Configure the application to use StackExchange.Redis</span></span>](#configure-the-application-to-use-stackexchangeredis)
* [<span data-ttu-id="53e87-216">De klasse TeamsController zodanig bijwerken dat deze resultaten retourneert uit de cache of de database</span><span class="sxs-lookup"><span data-stu-id="53e87-216">Update the TeamsController class to return results from the cache or the database</span></span>](#update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database)
* [<span data-ttu-id="53e87-217">De methoden Maken, Bewerken en Verwijderen bijwerken voor gebruik met de cache</span><span class="sxs-lookup"><span data-stu-id="53e87-217">Update the Create, Edit, and Delete methods to work with the cache</span></span>](#update-the-create-edit-and-delete-methods-to-work-with-the-cache)
* [<span data-ttu-id="53e87-218">De weergave Teamindex bijwerken voor gebruik met de cache</span><span class="sxs-lookup"><span data-stu-id="53e87-218">Update the Teams Index view to work with the cache</span></span>](#update-the-teams-index-view-to-work-with-the-cache)

### <a name="configure-the-application-to-use-stackexchangeredis"></a><span data-ttu-id="53e87-219">De toepassing configureren voor gebruik van StackExchange.Redis</span><span class="sxs-lookup"><span data-stu-id="53e87-219">Configure the application to use StackExchange.Redis</span></span>
1. <span data-ttu-id="53e87-220">Als u in Visual Studio een clienttoepassing wilt configureren met het NuGet-pakket StackExchange.Redis, klikt u in het menu **Extra** op **NuGet Package Manager**, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="53e87-220">To configure a client application in Visual Studio using the StackExchange.Redis NuGet package, click **NuGet Package Manager**, **Package Manager Console** from the **Tools** menu.</span></span>
2. <span data-ttu-id="53e87-221">Voer de volgende opdracht uit vanuit het venster `Package Manager Console`.</span><span class="sxs-lookup"><span data-stu-id="53e87-221">Run the following command from the `Package Manager Console` window.</span></span>
    
    ```
    Install-Package StackExchange.Redis
    ```
   
    <span data-ttu-id="53e87-222">Het NuGet-pakket downloadt de vereiste assembly-verwijzingen voor de clienttoepassing en voegt deze toe om met de cacheclient StackExchange.Redis toegang te krijgen tot de Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-222">The NuGet package downloads and adds the required assembly references for your client application to access Azure Redis Cache with the StackExchange.Redis cache client.</span></span> <span data-ttu-id="53e87-223">Als u een versie met een sterke naam van de `StackExchange.Redis`-clientbibliotheek verkiest, installeert u het `StackExchange.Redis.StrongName`-pakket.</span><span class="sxs-lookup"><span data-stu-id="53e87-223">If you prefer to use a strong-named version of the `StackExchange.Redis` client library, install the `StackExchange.Redis.StrongName` package.</span></span>
3. <span data-ttu-id="53e87-224">Vouw in **Solution Explorer** de map **Controllers** uit en dubbelklik op **TeamsController.cs** om dit bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="53e87-224">In **Solution Explorer**, expand the **Controllers** folder and double-click **TeamsController.cs** to open it.</span></span>
   
    ![TeamsController][cache-teamscontroller]
4. <span data-ttu-id="53e87-226">Voeg de volgende twee `using`-instructies toe aan **TeamsController.cs**.</span><span class="sxs-lookup"><span data-stu-id="53e87-226">Add the following two `using` statements to **TeamsController.cs**.</span></span>

    ```c#   
    using System.Configuration;
    using StackExchange.Redis;
    ```

5. <span data-ttu-id="53e87-227">Voeg de volgende twee eigenschappen toe aan de klasse `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="53e87-227">Add the following two properties to the `TeamsController` class.</span></span>

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

6. <span data-ttu-id="53e87-228">Maak op uw computer een bestand met de naam `WebAppPlusCacheAppSecrets.config`. Sla het op een locatie op die niet wordt ingecheckt met de broncode van uw voorbeeldtoepassing, mocht u besluiten deze ergens in te checken.</span><span class="sxs-lookup"><span data-stu-id="53e87-228">Create a file on your computer named `WebAppPlusCacheAppSecrets.config` and place it in a location that won't be checked in with the source code of your sample application, should you decide to check it in somewhere.</span></span> <span data-ttu-id="53e87-229">In dit voorbeeld bevindt het bestand `AppSettingsSecrets.config` zich op de locatie `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span><span class="sxs-lookup"><span data-stu-id="53e87-229">In this example the `AppSettingsSecrets.config` file is located at `C:\AppSecrets\WebAppPlusCacheAppSecrets.config`.</span></span>
   
    <span data-ttu-id="53e87-230">Bewerk het bestand `WebAppPlusCacheAppSecrets.config` en voeg de volgende inhoud toe.</span><span class="sxs-lookup"><span data-stu-id="53e87-230">Edit the `WebAppPlusCacheAppSecrets.config` file and add the following contents.</span></span> <span data-ttu-id="53e87-231">Als u de toepassing lokaal uitvoert, wordt deze informatie gebruikt om verbinding te maken met uw exemplaar van Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-231">If you run the application locally this information is used to connect to your Azure Redis Cache instance.</span></span> <span data-ttu-id="53e87-232">Verderop in de zelfstudie richt u een exemplaar van Azure Redis-cache in en werkt u de cachenaam en het wachtwoord bij.</span><span class="sxs-lookup"><span data-stu-id="53e87-232">Later in the tutorial you'll provision an Azure Redis Cache instance and update the cache name and password.</span></span> <span data-ttu-id="53e87-233">Als u de voorbeeldtoepassing niet lokaal wilt uitvoeren, kunt u het maken van dit bestand en de hierop volgende stappen die naar het bestand verwijzen, overslaan. Wanneer u in Azure implementeert, haalt de toepassing de verbindingsgegevens van de cache namelijk op uit de app-instelling voor de web-app en niet uit dit bestand.</span><span class="sxs-lookup"><span data-stu-id="53e87-233">If you don't plan to run the sample application locally you can skip the creation of this file and the subsequent steps that reference the file, because when you deploy to Azure the application retrieves the cache connection information from the app setting for the Web App and not from this file.</span></span> <span data-ttu-id="53e87-234">Aangezien de `WebAppPlusCacheAppSecrets.config` niet samen met uw toepassing in Azure wordt geïmplementeerd, hebt u deze niet nodig, tenzij u de toepassing lokaal wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="53e87-234">Since the `WebAppPlusCacheAppSecrets.config` is not deployed to Azure with your application, you don't need it unless you are going to run the application locally.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="53e87-235">Dubbelklik in **Solution Explorer** op **web.config** om het bestand te openen.</span><span class="sxs-lookup"><span data-stu-id="53e87-235">In **Solution Explorer**, double-click **web.config** to open it.</span></span>
   
    ![Web.config][cache-web-config]
2. <span data-ttu-id="53e87-237">Voeg het volgende `file`-kenmerk toe aan het element `appSettings`.</span><span class="sxs-lookup"><span data-stu-id="53e87-237">Add the following `file` attribute to the `appSettings` element.</span></span> <span data-ttu-id="53e87-238">Als u een andere bestandsnaam of -locatie gebruikt, vervang deze waarden dan door de waarden die in het voorbeeld worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="53e87-238">If you used a different file name or location, substitute those values for the ones shown in the example.</span></span>
   
   * <span data-ttu-id="53e87-239">Voor: `<appSettings>`</span><span class="sxs-lookup"><span data-stu-id="53e87-239">Before: `<appSettings>`</span></span>
   * <span data-ttu-id="53e87-240">Na: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span><span class="sxs-lookup"><span data-stu-id="53e87-240">After: ` <appSettings file="C:\AppSecrets\WebAppPlusCacheAppSecrets.config">`</span></span>
     
   <span data-ttu-id="53e87-241">De ASP.NET-runtime voegt de inhoud van het externe bestand samen met de opmaak van het element `<appSettings>`.</span><span class="sxs-lookup"><span data-stu-id="53e87-241">The ASP.NET runtime merges the contents of the external file with the markup in the `<appSettings>` element.</span></span> <span data-ttu-id="53e87-242">Als het opgegeven bestand niet kan worden gevonden, negeert de runtime het bestandskenmerk.</span><span class="sxs-lookup"><span data-stu-id="53e87-242">The runtime ignores the file attribute if the specified file cannot be found.</span></span> <span data-ttu-id="53e87-243">Uw geheimen (de verbindingsreeks naar uw cache) worden niet opgenomen in de broncode van de toepassing.</span><span class="sxs-lookup"><span data-stu-id="53e87-243">Your secrets (the connection string to your cache) are not included as part of the source code for the application.</span></span> <span data-ttu-id="53e87-244">Wanneer u uw web-app in Azure implementeert, wordt het bestand `WebAppPlusCacheAppSecrests.config` niet geïmplementeerd (dat is de bedoeling).</span><span class="sxs-lookup"><span data-stu-id="53e87-244">When you deploy your web app to Azure, the `WebAppPlusCacheAppSecrests.config` file won't be deployed (that's what you want).</span></span> <span data-ttu-id="53e87-245">Er zijn verschillende manieren om deze geheimen op te geven in Azure. In deze zelfstudie worden ze automatisch voor u geconfigureerd wanneer u in een latere stap van de zelfstudie [de Azure-resources inricht](#provision-the-azure-resources).</span><span class="sxs-lookup"><span data-stu-id="53e87-245">There are several ways to specify these secrets in Azure, and in this tutorial they are configured automatically for you when you [provision the Azure resources](#provision-the-azure-resources) in a subsequent tutorial step.</span></span> <span data-ttu-id="53e87-246">Raadpleeg [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure) (Aanbevolen procedures voor het implementeren van wachtwoorden en andere gevoelige gegevens naar ASP.NET en Azure App Service) voor meer informatie over het werken met geheimen in Azure.</span><span class="sxs-lookup"><span data-stu-id="53e87-246">For more information about working with secrets in Azure, see [Best practices for deploying passwords and other sensitive data to ASP.NET and Azure App Service](http://www.asp.net/identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure).</span></span>

### <a name="update-the-teamscontroller-class-to-return-results-from-the-cache-or-the-database"></a><span data-ttu-id="53e87-247">De klasse TeamsController zodanig bijwerken dat deze resultaten retourneert uit de cache of de database</span><span class="sxs-lookup"><span data-stu-id="53e87-247">Update the TeamsController class to return results from the cache or the database</span></span>
<span data-ttu-id="53e87-248">In dit voorbeeld worden teamstatistieken opgehaald uit de database of uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-248">In this sample, team statistics can be retrieved from the database or from the cache.</span></span> <span data-ttu-id="53e87-249">Teamstatistieken worden opgeslagen in de cache als een geserialiseerde `List<Team>` en ook als een gesorteerde set met Redis-gegevenstypen.</span><span class="sxs-lookup"><span data-stu-id="53e87-249">Team statistics are stored in the cache as a serialized `List<Team>`, and also as a sorted set using Redis data types.</span></span> <span data-ttu-id="53e87-250">Bij het ophalen van items uit een gesorteerde set kunt u een query uitvoeren voor sommige items, voor alle items of alleen voor bepaalde items.</span><span class="sxs-lookup"><span data-stu-id="53e87-250">When retrieving items from a sorted set, you can retrieve some, all, or query for certain items.</span></span> <span data-ttu-id="53e87-251">In dit voorbeeld voert u een query uit voor de gesorteerde set voor de beste vijf teams, op basis van het aantal overwinningen.</span><span class="sxs-lookup"><span data-stu-id="53e87-251">In this sample you'll query the sorted set for the top 5 teams ranked by number of wins.</span></span>

> [!NOTE]
> <span data-ttu-id="53e87-252">Het is niet vereist om de teamstatistieken in verschillende indelingen in de cache op te slaan om de Azure Redis-cache te kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53e87-252">It is not required to store the team statistics in multiple formats in the cache in order to use Azure Redis Cache.</span></span> <span data-ttu-id="53e87-253">In deze zelfstudie wordt gebruikgemaakt van meerdere indelingen ter illustratie van de verschillende manieren en gegevenstypen die u kunt gebruiken om gegevens in de cache op te slaan.</span><span class="sxs-lookup"><span data-stu-id="53e87-253">This tutorial uses multiple formats to demonstrate some of the different ways and different data types you can use to cache data.</span></span>
> 
> 

1. <span data-ttu-id="53e87-254">Voeg bovenaan, bij de andere `using`-instructies, de volgende `using`-instructies toe aan het `TeamsController.cs`-bestand.</span><span class="sxs-lookup"><span data-stu-id="53e87-254">Add the following `using` statements to the `TeamsController.cs` file at the top with the other `using` statements.</span></span>

    ```c#   
    using System.Diagnostics;
    using Newtonsoft.Json;
    ```

2. <span data-ttu-id="53e87-255">Vervang de huidige implementatie van de `public ActionResult Index()`-methode door de volgende implementatie.</span><span class="sxs-lookup"><span data-stu-id="53e87-255">Replace the current `public ActionResult Index()` method implementation with the following implementation.</span></span>

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

            case "clearCache": // Clear the results from the cache.
                ClearCachedTeams();
                break;

            case "rebuildDB": // Rebuild the database with sample data.
                RebuildDB();
                break;
        }

        // Measure the time it takes to retrieve the results.
        Stopwatch sw = Stopwatch.StartNew();

        switch(resultType)
        {
            case "teamsSortedSet": // Retrieve teams from sorted set.
                teams = GetFromSortedSet();
                break;

            case "teamsSortedSetTop5": // Retrieve the top 5 teams from the sorted set.
                teams = GetFromSortedSetTop5();
                break;

            case "teamsList": // Retrieve teams from the cached List<Team>.
                teams = GetFromList();
                break;

            case "fromDB": // Retrieve results from the database.
            default:
                teams = GetFromDB();
                break;
        }

        sw.Stop();
        double ms = sw.ElapsedTicks / (Stopwatch.Frequency / (1000.0));

        // Add the elapsed time of the operation to the ViewBag.msg.
        ViewBag.msg += " MS: " + ms.ToString();

        return View(teams);
    }
    ```


1. <span data-ttu-id="53e87-256">Voeg de volgende drie methoden voor de klasse `TeamsController` toe om de actietypen `playGames`, `clearCache` en `rebuildDB` te implementeren uit de switch-instructie die in het vorige codefragment is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="53e87-256">Add the following three methods to the `TeamsController` class to implement the `playGames`, `clearCache`, and `rebuildDB` action types from the switch statement added in the previous code snippet.</span></span>
   
    <span data-ttu-id="53e87-257">De `PlayGames`-methode werkt de teamstatistieken bij door een seizoen aan wedstrijden te simuleren, slaat de resultaten vervolgens op in de database en wist de nu verouderde gegevens uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-257">The `PlayGames` method updates the team statistics by simulating a season of games, saves the results to the database, and clears the now outdated data from the cache.</span></span>

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

    <span data-ttu-id="53e87-258">De `RebuildDB`-methode initialiseert de database opnieuw met de standaardset teams, genereert statistieken voor ze en wist de nu verouderde gegevens uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-258">The `RebuildDB` method reinitializes the database with the default set of teams, generates statistics for them, and clears the now outdated data from the cache.</span></span>

    ```c#
    void RebuildDB()
    {
        ViewBag.msg += "Rebuilding DB. ";
        // Delete and re-initialize the database with sample data.
        db.Database.Delete();
        db.Database.Initialize(true);

        // Clear any cached results
        ClearCachedTeams();
    }
    ```

    <span data-ttu-id="53e87-259">De `ClearCachedTeams`-methode verwijdert opgeslagen teamstatistieken uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-259">The `ClearCachedTeams` method removes any cached team statistics from the cache.</span></span>

    ```c#
    void ClearCachedTeams()
    {
        IDatabase cache = Connection.GetDatabase();
        cache.KeyDelete("teamsList");
        cache.KeyDelete("teamsSortedSet");
        ViewBag.msg += "Team data removed from cache. ";
    } 
    ```


1. <span data-ttu-id="53e87-260">Voeg de volgende vier methoden toe aan klasse `TeamsController` om de verschillende manieren voor het ophalen van teamstatistieken uit de cache en de database te implementeren.</span><span class="sxs-lookup"><span data-stu-id="53e87-260">Add the following four methods to the `TeamsController` class to implement the various ways of retrieving the team statistics from the cache and the database.</span></span> <span data-ttu-id="53e87-261">Alle methoden retourneren een `List<Team>`, die vervolgens wordt weergegeven in de weergave.</span><span class="sxs-lookup"><span data-stu-id="53e87-261">Each of these methods returns a `List<Team>` which is then displayed by the view.</span></span>
   
    <span data-ttu-id="53e87-262">De `GetFromDB`-methode leest de teamstatistieken uit de database.</span><span class="sxs-lookup"><span data-stu-id="53e87-262">The `GetFromDB` method reads the team statistics from the database.</span></span>
   
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

    <span data-ttu-id="53e87-263">De `GetFromList`-methode leest de teamstatistieken uit de cache als een geserialiseerde `List<Team>`.</span><span class="sxs-lookup"><span data-stu-id="53e87-263">The `GetFromList` method reads the team statistics from cache as a serialized `List<Team>`.</span></span> <span data-ttu-id="53e87-264">Als er een cache ontbreekt, worden de teamstatistieken gelezen uit de database en vervolgens voor later gebruik opgeslagen in de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-264">If there is a cache miss, the team statistics are read from the database and then stored in the cache for next time.</span></span> <span data-ttu-id="53e87-265">In dit voorbeeld wordt gebruikgemaakt van JSON.NET-serialisatie om de .NET-objecten naar en uit de cache te serialiseren.</span><span class="sxs-lookup"><span data-stu-id="53e87-265">In this sample we're using JSON.NET serialization to serialize the .NET objects to and from the cache.</span></span> <span data-ttu-id="53e87-266">Zie [Werken met .NET-objecten in Azure Redis-cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="53e87-266">For more information, see [How to work with .NET objects in Azure Redis Cache](cache-dotnet-how-to-use-azure-redis-cache.md#work-with-net-objects-in-the-cache).</span></span>

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

            ViewBag.msg += "Storing results to cache. ";
            cache.StringSet("teamsList", JsonConvert.SerializeObject(teams));
        }
        return teams;
    }
    ```

    <span data-ttu-id="53e87-267">De `GetFromSortedSet`-methode leest de teamstatistieken uit een in de cache opgeslagen gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="53e87-267">The `GetFromSortedSet` method reads the team statistics from a cached sorted set.</span></span> <span data-ttu-id="53e87-268">Als er een cache ontbreekt, worden de teamstatistieken uit de database gelezen en als een gesorteerde set opgeslagen in de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-268">If there is a cache miss, the team statistics are read from the database and stored in the cache as a sorted set.</span></span>

    ```c#
    List<Team> GetFromSortedSet()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();
        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
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

            ViewBag.msg += "Storing results to cache. ";
            foreach (var t in teams)
            {
                Console.WriteLine("Adding to sorted set: {0} - {1}", t.Name, t.Wins);
                cache.SortedSetAdd("teamsSortedSet", JsonConvert.SerializeObject(t), t.Wins);
            }
        }
        return teams;
    }
    ```

    <span data-ttu-id="53e87-269">De `GetFromSortedSetTop5`-methode leest de beste vijf teams uit de in de cache opgeslagen gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="53e87-269">The `GetFromSortedSetTop5` method reads the top 5 teams from the cached sorted set.</span></span> <span data-ttu-id="53e87-270">Deze methode begint met het controleren van de cache op de aanwezigheid van de `teamsSortedSet`-sleutel.</span><span class="sxs-lookup"><span data-stu-id="53e87-270">It starts by checking the cache for the existence of the `teamsSortedSet` key.</span></span> <span data-ttu-id="53e87-271">Als deze sleutel niet aanwezig is, wordt de `GetFromSortedSet`-methode aangeroepen om de teamstatistieken te lezen en op te slaan in de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-271">If this key is not present, the `GetFromSortedSet` method is called to read the team statistics and store them in the cache.</span></span> <span data-ttu-id="53e87-272">Vervolgens wordt de in de cache opgeslagen gesorteerde set bevraagd om de beste vijf teams op te halen. Deze worden daarna geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="53e87-272">Next, the cached sorted set is queried for the top 5 teams which are returned.</span></span>

    ```c#
    List<Team> GetFromSortedSetTop5()
    {
        List<Team> teams = null;
        IDatabase cache = Connection.GetDatabase();

        // If the key teamsSortedSet is not present, this method returns a 0 length collection.
        var teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        if(teamsSortedSet.Count() == 0)
        {
            // Load the entire sorted set into the cache.
            GetFromSortedSet();

            // Retrieve the top 5 teams.
            teamsSortedSet = cache.SortedSetRangeByRankWithScores("teamsSortedSet", stop: 4, order: Order.Descending);
        }

        ViewBag.msg += "Retrieving top 5 teams from cache. ";
        // Get the top 5 teams from the sorted set
        teams = new List<Team>();
        foreach (var team in teamsSortedSet)
        {
            teams.Add(JsonConvert.DeserializeObject<Team>(team.Element));
        }
        return teams;
    }
    ```

### <a name="update-the-create-edit-and-delete-methods-to-work-with-the-cache"></a><span data-ttu-id="53e87-273">De methoden Maken, Bewerken en Verwijderen bijwerken voor gebruik met de cache</span><span class="sxs-lookup"><span data-stu-id="53e87-273">Update the Create, Edit, and Delete methods to work with the cache</span></span>
<span data-ttu-id="53e87-274">De ondersteuningscode die als onderdeel van dit voorbeeld is gegenereerd, bevat de methoden om teams toe te voegen, te bewerken en te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="53e87-274">The scaffolding code that was generated as part of this sample includes methods to add, edit, and delete teams.</span></span> <span data-ttu-id="53e87-275">Telkens wanneer er een team wordt toegevoegd, bewerkt of verwijderd, raken de gegevens in de cache verouderd.</span><span class="sxs-lookup"><span data-stu-id="53e87-275">Anytime a team is added, edited, or removed, the data in the cache becomes outdated.</span></span> <span data-ttu-id="53e87-276">In deze sectie bewerkt u deze drie methoden, zodat de in de cache opgeslagen teams worden gewist en de cache synchroon loopt met de database.</span><span class="sxs-lookup"><span data-stu-id="53e87-276">In this section you'll modify these three methods to clear the cached teams so that the cache won't be out of sync with the database.</span></span>

1. <span data-ttu-id="53e87-277">Blader naar de `Create(Team team)`-methode in de klasse `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="53e87-277">Browse to the `Create(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="53e87-278">Voeg een aanroep toe aan de `ClearCachedTeams`-methode, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-278">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Create
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Create([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Teams.Add(team);
            db.SaveChanges();
            // When a team is added, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }

        return View(team);
    }
    ```


1. <span data-ttu-id="53e87-279">Blader naar de `Edit(Team team)`-methode in de klasse `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="53e87-279">Browse to the `Edit(Team team)` method in the `TeamsController` class.</span></span> <span data-ttu-id="53e87-280">Voeg een aanroep toe aan de `ClearCachedTeams`-methode, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-280">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Edit/5
    // To protect from overposting attacks, please enable the specific properties you want to bind to, for 
    // more details see http://go.microsoft.com/fwlink/?LinkId=317598.
    [HttpPost]
    [ValidateAntiForgeryToken]
    public ActionResult Edit([Bind(Include = "ID,Name,Wins,Losses,Ties")] Team team)
    {
        if (ModelState.IsValid)
        {
            db.Entry(team).State = EntityState.Modified;
            db.SaveChanges();
            // When a team is edited, the cache is out of date.
            // Clear the cached teams.
            ClearCachedTeams();
            return RedirectToAction("Index");
        }
        return View(team);
    }
    ```


1. <span data-ttu-id="53e87-281">Blader naar de `DeleteConfirmed(int id)`-methode in de klasse `TeamsController`.</span><span class="sxs-lookup"><span data-stu-id="53e87-281">Browse to the `DeleteConfirmed(int id)` method in the `TeamsController` class.</span></span> <span data-ttu-id="53e87-282">Voeg een aanroep toe aan de `ClearCachedTeams`-methode, zoals wordt weergegeven in het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="53e87-282">Add a call to the `ClearCachedTeams` method, as shown in the following example.</span></span>

    ```c#
    // POST: Teams/Delete/5
    [HttpPost, ActionName("Delete")]
    [ValidateAntiForgeryToken]
    public ActionResult DeleteConfirmed(int id)
    {
        Team team = db.Teams.Find(id);
        db.Teams.Remove(team);
        db.SaveChanges();
        // When a team is deleted, the cache is out of date.
        // Clear the cached teams.
        ClearCachedTeams();
        return RedirectToAction("Index");
    }
    ```


### <a name="update-the-teams-index-view-to-work-with-the-cache"></a><span data-ttu-id="53e87-283">De weergave Teamindex bijwerken voor gebruik met de cache</span><span class="sxs-lookup"><span data-stu-id="53e87-283">Update the Teams Index view to work with the cache</span></span>
1. <span data-ttu-id="53e87-284">Vouw in **Solution Explorer** de map **Views** uit. Vouw vervolgens de map **Teams** uit en dubbelklik op **Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="53e87-284">In **Solution Explorer**, expand the **Views** folder, then the **Teams** folder, and double-click **Index.cshtml**.</span></span>
   
    ![Index.cshtml][cache-views-teams-index-cshtml]
2. <span data-ttu-id="53e87-286">Zoek boven in het bestand naar het volgende alinea-element.</span><span class="sxs-lookup"><span data-stu-id="53e87-286">Near the top of the file, look for the following paragraph element.</span></span>
   
    ![Actietabel][cache-teams-index-table]
   
    <span data-ttu-id="53e87-288">Dit is de koppeling waarmee u een nieuw team kunt maken.</span><span class="sxs-lookup"><span data-stu-id="53e87-288">This is the link to create a new team.</span></span> <span data-ttu-id="53e87-289">Vervang het alinea-element door de volgende tabel.</span><span class="sxs-lookup"><span data-stu-id="53e87-289">Replace the paragraph element with the following table.</span></span> <span data-ttu-id="53e87-290">Deze tabel bevat actiekoppelingen waarmee u een nieuw team kunt maken, een nieuw seizoen wedstrijden kunt spelen, de cache kunt wissen, de teams in verschillende indelingen kunt ophalen uit de cache, de teams kunt ophalen uit de database en de database opnieuw kunt opbouwen met de nieuwe voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="53e87-290">This table has action links for creating a new team, playing a new season of games, clearing the cache, retrieving the teams from the cache in several formats, retrieving the teams from the database, and rebuilding the database with fresh sample data.</span></span>

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


1. <span data-ttu-id="53e87-291">Ga naar de onderkant van het bestand **Index.cshtml** en voeg het volgende `tr`-element toe, zodat dit de laatste rij in de laatste tabel in het bestand is.</span><span class="sxs-lookup"><span data-stu-id="53e87-291">Scroll to the bottom of the **Index.cshtml** file and add the following `tr` element so that it is the last row in the last table in the file.</span></span>
   
    ```html
    <tr><td colspan="5">@ViewBag.Msg</td></tr>
    ```
   
    <span data-ttu-id="53e87-292">Deze rij toont de waarde van `ViewBag.Msg`, die een statusrapport over de huidige bewerking bevat.</span><span class="sxs-lookup"><span data-stu-id="53e87-292">This row displays the value of `ViewBag.Msg` which contains a status report about the current operation.</span></span> <span data-ttu-id="53e87-293">De `ViewBag.Msg` wordt ingesteld wanneer u op een van de actiekoppelingen uit de vorige stap klikt.</span><span class="sxs-lookup"><span data-stu-id="53e87-293">The `ViewBag.Msg` is set when you click any of the action links from the previous step.</span></span>   
   
    ![Statusbericht][cache-status-message]
2. <span data-ttu-id="53e87-295">Druk op **F6** om het project te bouwen.</span><span class="sxs-lookup"><span data-stu-id="53e87-295">Press **F6** to build the project.</span></span>

## <a name="provision-the-azure-resources"></a><span data-ttu-id="53e87-296">De Azure-resources inrichten</span><span class="sxs-lookup"><span data-stu-id="53e87-296">Provision the Azure resources</span></span>
<span data-ttu-id="53e87-297">Als u uw toepassing in Azure wilt hosten, moet u eerst de Azure-services inrichten die vereist zijn voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="53e87-297">To host your application in Azure, you must first provision the Azure services that your application requires.</span></span> <span data-ttu-id="53e87-298">De voorbeeldtoepassing in deze zelfstudie maakt gebruik van de volgende Azure-services.</span><span class="sxs-lookup"><span data-stu-id="53e87-298">The sample application in this tutorial uses the following Azure services.</span></span>

* <span data-ttu-id="53e87-299">Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="53e87-299">Azure Redis Cache</span></span>
* <span data-ttu-id="53e87-300">App Service-web-app</span><span class="sxs-lookup"><span data-stu-id="53e87-300">App Service Web App</span></span>
* <span data-ttu-id="53e87-301">SQL Database</span><span class="sxs-lookup"><span data-stu-id="53e87-301">SQL Database</span></span>

<span data-ttu-id="53e87-302">Als u deze services wilt implementeren in een nieuwe of bestaande resourcegroep naar keuze, klikt u op de knop **Deploy to Azure**.</span><span class="sxs-lookup"><span data-stu-id="53e87-302">To deploy these services to a new or existing resource group of your choice, click the following **Deploy to Azure** button.</span></span>

<span data-ttu-id="53e87-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="53e87-303">[![Deploy to Azure][deploybutton]](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-web-app-redis-cache-sql-database%2Fazuredeploy.json)</span></span>

<span data-ttu-id="53e87-304">De knop **Deploy to Azure** gebruikt de sjabloon voor de [Azure-snelstartgids](https://github.com/Azure/azure-quickstart-templates) [Een web-app maken plus Redis-cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) om deze services in te richten en de verbindingsreeks in te stellen voor de SQL Database, evenals de toepassingsinstelling voor de verbindingsreeks voor de Azure Redis-cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-304">This **Deploy to Azure** button uses the [Create a Web App plus Redis Cache plus SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/201-web-app-redis-cache-sql-database) [Azure Quickstart](https://github.com/Azure/azure-quickstart-templates) template to provision these services and set the connection string for the SQL Database and the application setting for the Azure Redis Cache connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="53e87-305">Als u geen Azure-account hebt, kunt u binnen een paar minuten [een gratis Azure-account maken](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero).</span><span class="sxs-lookup"><span data-stu-id="53e87-305">If you don't have an Azure account, you can [create a free Azure account](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=redis_cache_hero) in just a couple of minutes.</span></span>
> 
> 

<span data-ttu-id="53e87-306">Als u op de knop **Deploy to Azure** klikt, wordt u naar de Azure-portal geleid en start het proces voor het maken van de resources die in de sjabloon worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="53e87-306">Clicking the **Deploy to Azure** button takes you to the Azure portal and initiates the process of creating the resources described by the template.</span></span>

![Implementeren in Azure][cache-deploy-to-azure-step-1]

1. <span data-ttu-id="53e87-308">Selecteer in de sectie **Basisbeginselen** het Azure-abonnement dat u wilt gebruiken. Selecteer daarnaast een bestaande resourcegroep of maak een nieuwe, en geef de locatie van de resourcegroep op.</span><span class="sxs-lookup"><span data-stu-id="53e87-308">In the **Basics** section, select the Azure subscription to use, and select an existing resource group or create a new one, and specify the resource group location.</span></span>
2. <span data-ttu-id="53e87-309">Geef in de sectie **Instellingen** de **aanmeldingsnaam van een beheerder** op (gebruik niet **admin**), het **wachtwoord van de beheerdersaanmelding** en de **Databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="53e87-309">In the **Settings** section, specify an **Administrator Login** (don't use **admin**), **Administrator Login Password**, and **Database Name**.</span></span> <span data-ttu-id="53e87-310">De andere parameters zijn geconfigureerd voor een gratis App Service-hostingplan en voor opties met lagere kosten voor de SQL Database en de Azure Redis-cache (deze worden niet geleverd met een gratis laag).</span><span class="sxs-lookup"><span data-stu-id="53e87-310">The other parameters are configured for a free App Service hosting plan, and lower-cost options for the SQL Database and Azure Redis Cache, which don't come with a free tier.</span></span>

    ![Implementeren in Azure][cache-deploy-to-azure-step-2]

3. <span data-ttu-id="53e87-312">Schuif na het configureren van de gewenste instellingen naar het einde van de pagina, lees de voorwaarden en bepalingen, en schakel het selectievakje **Ik ga akkoord met de bovenstaande voorwaarden** in.</span><span class="sxs-lookup"><span data-stu-id="53e87-312">After configuring the desired settings, scroll to the end of the page, read the terms and conditions, and check the **I agree to the terms and conditions stated above** checkbox.</span></span>
4. <span data-ttu-id="53e87-313">Klik op **Kopen** om te beginnen met het inrichten van de resources.</span><span class="sxs-lookup"><span data-stu-id="53e87-313">To begin provisioning the resources, click **Purchase**.</span></span>

<span data-ttu-id="53e87-314">Als u de voortgang van uw implementatie wilt bekijken, klikt u op het meldingspictogram en vervolgens op **Implementatie gestart**.</span><span class="sxs-lookup"><span data-stu-id="53e87-314">To view the progress of your deployment, click the notification icon and click **Deployment started**.</span></span>

![Implementatie gestart][cache-deployment-started]

<span data-ttu-id="53e87-316">U kunt de status van uw implementatie bekijken op de blade **Microsoft.Template**.</span><span class="sxs-lookup"><span data-stu-id="53e87-316">You can view the status of your deployment on the **Microsoft.Template** blade.</span></span>

![Implementeren in Azure][cache-deploy-to-azure-step-3]

<span data-ttu-id="53e87-318">Wanneer het inrichten is voltooid, kunt u uw toepassing in Azure publiceren vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="53e87-318">When provisioning is complete, you can publish your application to Azure from Visual Studio.</span></span>

> [!NOTE]
> <span data-ttu-id="53e87-319">Eventuele fouten die zich tijdens het inrichtingsproces voordoen, worden weergegeven op de blade **Microsoft.Template**.</span><span class="sxs-lookup"><span data-stu-id="53e87-319">Any errors that may occur during the provisioning process are displayed on the **Microsoft.Template** blade.</span></span> <span data-ttu-id="53e87-320">Veelvoorkomende fouten zijn te veel SQL Servers of te veel gratis App Service-hostingplannen per abonnement.</span><span class="sxs-lookup"><span data-stu-id="53e87-320">Common errors are too many SQL Servers or too many Free App Service hosting plans per subscription.</span></span> <span data-ttu-id="53e87-321">Los eventuele fouten op en start het proces opnieuw door te klikken op **Opnieuw implementeren** op de blade **Microsoft.Template** of op de knop **Implementeren in Azure** in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="53e87-321">Resolve any errors and restart the process by clicking **Redeploy** on the **Microsoft.Template** blade or the **Deploy to Azure** button in this tutorial.</span></span>
> 
> 

## <a name="publish-the-application-to-azure"></a><span data-ttu-id="53e87-322">De toepassing publiceren in Azure</span><span class="sxs-lookup"><span data-stu-id="53e87-322">Publish the application to Azure</span></span>
<span data-ttu-id="53e87-323">In deze stap van de zelfstudie publiceert u de toepassing in Azure en voert u deze uit in de cloud.</span><span class="sxs-lookup"><span data-stu-id="53e87-323">In this step of the tutorial, you'll publish the application to Azure and run it in the cloud.</span></span>

1. <span data-ttu-id="53e87-324">Klik in Visual Studio met de rechtermuisknop op het project **ContosoTeamStats** en kies **Publish**.</span><span class="sxs-lookup"><span data-stu-id="53e87-324">Right-click the **ContosoTeamStats** project in Visual Studio and choose **Publish**.</span></span>
   
    ![Publiceren][cache-publish-app]
2. <span data-ttu-id="53e87-326">Klik op **Microsoft Azure App Service**, kies **Bestaande selecteren** en klik op **Publiceren**.</span><span class="sxs-lookup"><span data-stu-id="53e87-326">Click **Microsoft Azure App Service**, choose **Select Existing**, and click **Publish**.</span></span>
   
    ![Publiceren][cache-publish-to-app-service]
3. <span data-ttu-id="53e87-328">Selecteer het abonnement dat u hebt gebruikt bij het maken van de Azure-resources, vouw de resourcegroep met de resources uit en selecteer de gewenste web-app.</span><span class="sxs-lookup"><span data-stu-id="53e87-328">Select the subscription used when creating the Azure resources, expand the resource group containing the resources, and select the desired Web App.</span></span> <span data-ttu-id="53e87-329">Als u de knop **Implementeren in Azure** hebt gebruikt, begint de naam van uw web-app met **webSite**, gevolgd door een aantal extra tekens.</span><span class="sxs-lookup"><span data-stu-id="53e87-329">If you used the **Deploy to Azure** button your Web App name starts with **webSite** followed by some additional characters.</span></span>
   
    ![Web-app selecteren][cache-select-web-app]
4. <span data-ttu-id="53e87-331">Klik op **OK** om het publicatieproces te starten.</span><span class="sxs-lookup"><span data-stu-id="53e87-331">Click **OK** to begin the publishing process.</span></span> <span data-ttu-id="53e87-332">Na enkele ogenblikken wordt het publicatieproces voltooid. Er wordt een browservenster geopend waarin de voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="53e87-332">After a few moments the publishing process completes and a browser is launched with the running sample application.</span></span> <span data-ttu-id="53e87-333">Als er tijdens het valideren of publiceren een DNS-fout optreedt en het inrichtingsproces voor de Azure-resources voor de toepassing nog maar net is voltooid, wacht dan even en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="53e87-333">If you get a DNS error when validating or publishing, and the provisioning process for the Azure resources for the application has just recently completed, wait a moment and try again.</span></span>
   
    ![Cache toegevoegd][cache-added-to-application]

<span data-ttu-id="53e87-335">De volgende tabel beschrijft elke actiekoppeling in de voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="53e87-335">The following table describes each action link from the sample application.</span></span>

| <span data-ttu-id="53e87-336">Actie</span><span class="sxs-lookup"><span data-stu-id="53e87-336">Action</span></span> | <span data-ttu-id="53e87-337">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="53e87-337">Description</span></span> |
| --- | --- |
| <span data-ttu-id="53e87-338">Create New</span><span class="sxs-lookup"><span data-stu-id="53e87-338">Create New</span></span> |<span data-ttu-id="53e87-339">Een nieuw team maken</span><span class="sxs-lookup"><span data-stu-id="53e87-339">Create a new Team.</span></span> |
| <span data-ttu-id="53e87-340">Play Season</span><span class="sxs-lookup"><span data-stu-id="53e87-340">Play Season</span></span> |<span data-ttu-id="53e87-341">Speel een seizoen wedstrijden, werk de teamstatistieken bij en wis eventuele verouderde teamgegevens uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-341">Play a season of games, update the team stats, and clear any outdated team data from the cache.</span></span> |
| <span data-ttu-id="53e87-342">Clear Cache</span><span class="sxs-lookup"><span data-stu-id="53e87-342">Clear Cache</span></span> |<span data-ttu-id="53e87-343">Wis de teamstatistieken uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-343">Clear the team stats from the cache.</span></span> |
| <span data-ttu-id="53e87-344">List from Cache</span><span class="sxs-lookup"><span data-stu-id="53e87-344">List from Cache</span></span> |<span data-ttu-id="53e87-345">Haal de teamstatistieken op uit de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-345">Retrieve the team stats from the cache.</span></span> <span data-ttu-id="53e87-346">Als er een cache ontbreekt, moet u de statistieken uit de database laden en in de cache opslaan voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="53e87-346">If there is a cache miss, load the stats from the database and save to the cache for next time.</span></span> |
| <span data-ttu-id="53e87-347">Sorted Set from Cache</span><span class="sxs-lookup"><span data-stu-id="53e87-347">Sorted Set from Cache</span></span> |<span data-ttu-id="53e87-348">Haal de teamstatistieken op uit de cache met behulp van een gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="53e87-348">Retrieve the team stats from the cache using a sorted set.</span></span> <span data-ttu-id="53e87-349">Als er een cache ontbreekt, moet u de statistieken uit de database laden en met behulp van een gesorteerde set opslaan in de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-349">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="53e87-350">Top 5 Teams from Cache</span><span class="sxs-lookup"><span data-stu-id="53e87-350">Top 5 Teams from Cache</span></span> |<span data-ttu-id="53e87-351">Haal de beste vijf teams op uit de cache met behulp van een gesorteerde set.</span><span class="sxs-lookup"><span data-stu-id="53e87-351">Retrieve the top 5 teams from the cache using a sorted set.</span></span> <span data-ttu-id="53e87-352">Als er een cache ontbreekt, moet u de statistieken uit de database laden en met behulp van een gesorteerde set opslaan in de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-352">If there is a cache miss, load the stats from the database and save to the cache using a sorted set.</span></span> |
| <span data-ttu-id="53e87-353">Load from DB</span><span class="sxs-lookup"><span data-stu-id="53e87-353">Load from DB</span></span> |<span data-ttu-id="53e87-354">Haal de teamstatistieken op uit de database.</span><span class="sxs-lookup"><span data-stu-id="53e87-354">Retrieve the team stats from the database.</span></span> |
| <span data-ttu-id="53e87-355">Rebuild DB</span><span class="sxs-lookup"><span data-stu-id="53e87-355">Rebuild DB</span></span> |<span data-ttu-id="53e87-356">Bouw de database opnieuw en laad deze opnieuw met voorbeeldgegevens van de teams.</span><span class="sxs-lookup"><span data-stu-id="53e87-356">Rebuild the database and reload it with sample team data.</span></span> |
| <span data-ttu-id="53e87-357">Edit/Details/Delete</span><span class="sxs-lookup"><span data-stu-id="53e87-357">Edit / Details / Delete</span></span> |<span data-ttu-id="53e87-358">Bewerk een team, geef details van een team weer en verwijder een team.</span><span class="sxs-lookup"><span data-stu-id="53e87-358">Edit a team, view details for a team, delete a team.</span></span> |

<span data-ttu-id="53e87-359">Klik op een aantal acties en experimenteer met het ophalen van de gegevens vanuit de verschillende bronnen.</span><span class="sxs-lookup"><span data-stu-id="53e87-359">Click some of the actions and experiment with retrieving the data from the different sources.</span></span> <span data-ttu-id="53e87-360">Let op de verschillen in de tijd die nodig is om de gegevens op de diverse manieren op te halen uit de database en de cache.</span><span class="sxs-lookup"><span data-stu-id="53e87-360">Not the differences in the time it takes to complete the various ways of retrieving the data from the database and the cache.</span></span>

## <a name="delete-the-resources-when-you-are-finished-with-the-application"></a><span data-ttu-id="53e87-361">De resources verwijderen wanneer u klaar bent met de toepassing</span><span class="sxs-lookup"><span data-stu-id="53e87-361">Delete the resources when you are finished with the application</span></span>
<span data-ttu-id="53e87-362">Wanneer u klaar bent met de voorbeeldtoepassing uit de zelfstudie, kunt u de Azure-resources die u hebt gebruikt, verwijderen om kosten en resources te besparen.</span><span class="sxs-lookup"><span data-stu-id="53e87-362">When you are finished with the sample tutorial application, you can delete the Azure resources used in order to conserve cost and resources.</span></span> <span data-ttu-id="53e87-363">Als u de knop **Implementeren in Azure** in de sectie [De Azure-resources inrichten](#provision-the-azure-resources) hebt gebruikt en alle resources zich in dezelfde resourcegroep bevinden, kunt u deze in één keer verwijderen door de resourcegroep te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="53e87-363">If you use the **Deploy to Azure** button in the [Provision the Azure resources](#provision-the-azure-resources) section and all of your resources are contained in the same resource group, you can delete them together in one operation by deleting the resource group.</span></span>

1. <span data-ttu-id="53e87-364">Meld u aan bij de [Azure-portal](https://portal.azure.com) en klik op **Resourcegroepen**.</span><span class="sxs-lookup"><span data-stu-id="53e87-364">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>
2. <span data-ttu-id="53e87-365">Typ de naam van de resourcegroep in het tekstvak **Items filteren...**.</span><span class="sxs-lookup"><span data-stu-id="53e87-365">Type the name of your resource group into the **Filter items...** textbox.</span></span>
3. <span data-ttu-id="53e87-366">Klik op **...** aan de rechterkant van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="53e87-366">Click **...** to the right of your resource group.</span></span>
4. <span data-ttu-id="53e87-367">Klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="53e87-367">Click **Delete**.</span></span>
   
    ![Verwijderen][cache-delete-resource-group]
5. <span data-ttu-id="53e87-369">Typ de naam van de resourcegroep en klik op **Verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="53e87-369">Type the name of your resource group and click **Delete**.</span></span>
   
    ![De verwijdering bevestigen][cache-delete-confirm]

<span data-ttu-id="53e87-371">Na enkele ogenblikken worden de resourcegroep en alle ingesloten bronnen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="53e87-371">After a few moments the resource group and all of its contained resources are deleted.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53e87-372">Houd er rekening mee dat het verwijderen van een resourcegroep niet ongedaan kan worden gemaakt, en dat de resourcegroep en alle bijbehorende resources permanent worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="53e87-372">Note that deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="53e87-373">Zorg ervoor dat u niet per ongeluk de verkeerde resourcegroep of resources verwijdert.</span><span class="sxs-lookup"><span data-stu-id="53e87-373">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="53e87-374">Als u de resources voor het hosten van dit voorbeeld in een bestaande resourcegroep hebt gemaakt, kunt u elke resource afzonderlijk verwijderen via hun respectievelijke blades.</span><span class="sxs-lookup"><span data-stu-id="53e87-374">If you created the resources for hosting this sample inside an existing resource group, you can delete each resource individually from their respective blades.</span></span>
> 
> 

## <a name="run-the-sample-application-on-your-local-machine"></a><span data-ttu-id="53e87-375">De voorbeeldtoepassing uitvoeren op uw lokale computer</span><span class="sxs-lookup"><span data-stu-id="53e87-375">Run the sample application on your local machine</span></span>
<span data-ttu-id="53e87-376">Als u de toepassing lokaal wilt uitvoeren op uw computer, hebt u een exemplaar van Azure Redis-cache nodig waarin u de gegevens kunt opslaan.</span><span class="sxs-lookup"><span data-stu-id="53e87-376">To run the application locally on your machine, you need an Azure Redis Cache instance in which to cache your data.</span></span> 

* <span data-ttu-id="53e87-377">Als u uw toepassing in Azure hebt gepubliceerd, zoals beschreven in het vorige gedeelte, kunt u het exemplaar van Azure Redis-cache gebruiken dat tijdens die stap is ingericht.</span><span class="sxs-lookup"><span data-stu-id="53e87-377">If you have published your application to Azure as described in the previous section, you can use the Azure Redis Cache instance that was provisioned during that step.</span></span>
* <span data-ttu-id="53e87-378">Als u een ander bestaand exemplaar van Azure Redis-cache hebt, kunt u dit gebruiken om het voorbeeld lokaal uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="53e87-378">If you have another existing Azure Redis Cache instance, you can use that to run this sample locally.</span></span>
* <span data-ttu-id="53e87-379">Als u een exemplaar van Azure Redis-cache moet maken, kunt u de stappen volgen in [Een cache maken](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span><span class="sxs-lookup"><span data-stu-id="53e87-379">If you need to create an Azure Redis Cache instance, you can follow the steps in [Create a cache](cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache).</span></span>

<span data-ttu-id="53e87-380">Nadat u de cache die u wilt gebruiken, hebt geselecteerd of gemaakt, kunt u naar de cache in de Azure-portal bladeren en de [hostnaam](cache-configure.md#properties) en de [toegangssleutels](cache-configure.md#access-keys) voor uw cache ophalen.</span><span class="sxs-lookup"><span data-stu-id="53e87-380">Once you have selected or created the cache to use, browse to the cache in the Azure portal and retrieve the [host name](cache-configure.md#properties) and [access keys](cache-configure.md#access-keys) for your cache.</span></span> <span data-ttu-id="53e87-381">Zie [Redis-cache-instellingen configureren](cache-configure.md#configure-redis-cache-settings) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="53e87-381">For instructions, see [Configure Redis cache settings](cache-configure.md#configure-redis-cache-settings).</span></span>

1. <span data-ttu-id="53e87-382">Open het bestand `WebAppPlusCacheAppSecrets.config` dat u hebt gemaakt tijdens de stap [De toepassing configureren voor het gebruik van Redis-cache](#configure-the-application-to-use-redis-cache) in deze zelfstudie. Gebruik hiervoor een editor naar keuze.</span><span class="sxs-lookup"><span data-stu-id="53e87-382">Open the `WebAppPlusCacheAppSecrets.config` file that you created during the [Configure the application to use Redis Cache](#configure-the-application-to-use-redis-cache) step of this tutorial using the editor of your choice.</span></span>
2. <span data-ttu-id="53e87-383">Bewerk het kenmerk `value` en vervang `MyCache.redis.cache.windows.net` door de [hostnaam](cache-configure.md#properties) van de cache. Geef vervolgens de [primaire of secundaire sleutel](cache-configure.md#access-keys) van uw cache op als wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="53e87-383">Edit the `value` attribute and replace `MyCache.redis.cache.windows.net` with the [host name](cache-configure.md#properties) of your cache, and specify either the [primary or secondary key](cache-configure.md#access-keys) of your cache as the password.</span></span>

    ```xml
    <appSettings>
      <add key="CacheConnection" value="MyCache.redis.cache.windows.net,abortConnect=false,ssl=true,password=..."/>
    </appSettings>
    ```


1. <span data-ttu-id="53e87-384">Druk op **Ctrl+F5** om de toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="53e87-384">Press **Ctrl+F5** to run the application.</span></span>

> [!NOTE]
> <span data-ttu-id="53e87-385">Houd er rekening mee dat de toepassing en de database lokaal worden uitgevoerd en dat de Redis-cache wordt gehost in Azure. Hierdoor kan het lijken alsof de cache minder goed presteert dan de database.</span><span class="sxs-lookup"><span data-stu-id="53e87-385">Note that because the application, including the database, is running locally and the Redis Cache is hosted in Azure, the cache may appear to under-perform the database.</span></span> <span data-ttu-id="53e87-386">Voor optimale prestaties moeten de clienttoepassing en het exemplaar van Azure Redis-cache zich op dezelfde locatie bevinden.</span><span class="sxs-lookup"><span data-stu-id="53e87-386">For best performance, the client application and Azure Redis Cache instance should be in the same location.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="53e87-387">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53e87-387">Next steps</span></span>
* <span data-ttu-id="53e87-388">Meer informatie over [hoe u aan de slag gaat met ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) vindt u op de website van [ASP.NET](http://asp.net/).</span><span class="sxs-lookup"><span data-stu-id="53e87-388">Learn more about [Getting Started with ASP.NET MVC 5](http://www.asp.net/mvc/overview/getting-started/introduction/getting-started) on the [ASP.NET](http://asp.net/) site.</span></span>
* <span data-ttu-id="53e87-389">Zie [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) (Een ASP.NET-web-app maken en implementeren in Azure App Service) van de [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect[-demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/) voor meer voorbeelden van het maken van een ASP.NET Web-App in de App Service.</span><span class="sxs-lookup"><span data-stu-id="53e87-389">For more examples of creating an ASP.NET Web App in App Service, see [Create and deploy an ASP.NET web app in Azure App Service](https://github.com/Microsoft/HealthClinic.biz/wiki/Create-and-deploy-an-ASP.NET-web-app-in-Azure-App-Service) from the [HealthClinic.biz](https://github.com/Microsoft/HealthClinic.biz) 2015 Connect [demo](https://blogs.msdn.microsoft.com/visualstudio/2015/12/08/connectdemos-2015-healthclinic-biz/).</span></span>
  * <span data-ttu-id="53e87-390">Voor meer introductiehandleidingen van de demo van HealthClinic.biz, verwijzen wij u naar [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span><span class="sxs-lookup"><span data-stu-id="53e87-390">For more quickstarts from the HealthClinic.biz demo, see [Azure Developer Tools Quickstarts](https://github.com/Microsoft/HealthClinic.biz/wiki/Azure-Developer-Tools-Quickstarts).</span></span>
* <span data-ttu-id="53e87-391">Meer informatie over de Entity Framework-werkwijze [Code First voor een nieuwe database](https://msdn.microsoft.com/data/jj193542) die in deze zelfstudie wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="53e87-391">Learn more about the [Code first to a new database](https://msdn.microsoft.com/data/jj193542) approach to Entity Framework that's used in this tutorial.</span></span>
* <span data-ttu-id="53e87-392">Meer informatie over [web-apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="53e87-392">Learn more about [web apps in Azure App Service](../app-service-web/app-service-web-overview.md).</span></span>
* <span data-ttu-id="53e87-393">Meer informatie over het [controleren](cache-how-to-monitor.md) van uw cache in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="53e87-393">Learn how to [monitor](cache-how-to-monitor.md) your cache in the Azure portal.</span></span>
* <span data-ttu-id="53e87-394">De premiumfuncties van de Azure Redis-cache verkennen</span><span class="sxs-lookup"><span data-stu-id="53e87-394">Explore Azure Redis Cache premium features</span></span>
  
  * [<span data-ttu-id="53e87-395">Persistentie configureren voor een Premium Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="53e87-395">How to configure persistence for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-persistence.md)
  * [<span data-ttu-id="53e87-396">Clustering configureren voor een Premium Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="53e87-396">How to configure clustering for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-clustering.md)
  * [<span data-ttu-id="53e87-397">Virtual Network-ondersteuning configureren voor een Premium Azure Redis-cache</span><span class="sxs-lookup"><span data-stu-id="53e87-397">How to configure Virtual Network support for a Premium Azure Redis Cache</span></span>](cache-how-to-premium-vnet.md)
  * <span data-ttu-id="53e87-398">Raadpleeg [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) (Veelgestelde vragen over Azure Redis-caches) voor meer informatie over de grootte, doorvoer en bandbreedte van premiumcaches.</span><span class="sxs-lookup"><span data-stu-id="53e87-398">See the [Azure Redis Cache FAQ](cache-faq.md#what-redis-cache-offering-and-size-should-i-use) for more details about size, throughput, and bandwidth with premium caches.</span></span>

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

