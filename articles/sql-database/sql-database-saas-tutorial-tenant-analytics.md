---
title: aaaRun analytics query's op meerdere Azure SQL-databases | Microsoft Docs
description: Gegevens ophalen uit de tenant-databases in een database analytics voor offline-analyse
keywords: zelfstudie sql-database
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="8f926-104">Gegevens ophalen uit de tenant-databases in een database analytics voor offline-analyse</span><span class="sxs-lookup"><span data-stu-id="8f926-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="8f926-105">In deze zelfstudie maakt u een taak elastische toorun een query uitgevoerd op elke tenant-database.</span><span class="sxs-lookup"><span data-stu-id="8f926-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="8f926-106">Hallo taak ticket verkoopgegevens extraheert en laadt deze in een analytics-database (of het datawarehouse) voor analyse.</span><span class="sxs-lookup"><span data-stu-id="8f926-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="8f926-107">Hallo analytics-database is vervolgens tooextract inzicht in deze dagelijkse operationele gegevens van alle tenants opgevraagd.</span><span class="sxs-lookup"><span data-stu-id="8f926-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="8f926-108">In deze zelfstudie leert u het volgende:</span><span class="sxs-lookup"><span data-stu-id="8f926-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f926-109">Hallo tenant analytics-database maken</span><span class="sxs-lookup"><span data-stu-id="8f926-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="8f926-110">Een geplande taak tooretrieve gegevens maken en vullen Hallo analytics-database</span><span class="sxs-lookup"><span data-stu-id="8f926-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="8f926-111">toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten wordt voldaan:</span><span class="sxs-lookup"><span data-stu-id="8f926-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="8f926-112">Hallo Wingtip SaaS-app wordt geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="8f926-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="8f926-113">Zie toodeploy in minder dan vijf minuten [implementeren en verkennen Hallo Wingtip SaaS-toepassing](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="8f926-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="8f926-114">Azure PowerShell is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8f926-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="8f926-115">Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8f926-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="8f926-116">Hallo meest recente versie van SQL Server Management Studio (SSMS) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8f926-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="8f926-117">SSMS downloaden en installeren</span><span class="sxs-lookup"><span data-stu-id="8f926-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="8f926-118">Operational Analytics-patroon van tenant</span><span class="sxs-lookup"><span data-stu-id="8f926-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="8f926-119">Een van de grote kansen Hallo met SaaS-toepassingen is toouse Hallo uitgebreide tenant gegevens die zijn opgeslagen in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f926-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="8f926-120">Gebruik deze gegevens toogain inzichten Hallo bewerking en het gebruik van uw toepassing en uw tenants.</span><span class="sxs-lookup"><span data-stu-id="8f926-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="8f926-121">Deze gegevens kunt leiden functie ontwikkeling, bruikbaarheid verbeteringen en andere investeringen in Hallo-app en -platform.</span><span class="sxs-lookup"><span data-stu-id="8f926-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="8f926-122">U kunt gemakkelijk toegang tot deze gegevens krijgen in een database met meerdere tenants, maar dit is niet zo gemakkelijk als de gegevens op schaal zijn gedistribueerd over misschien wel duizenden databases.</span><span class="sxs-lookup"><span data-stu-id="8f926-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="8f926-123">Een benadering tooaccessing deze gegevens zijn toouse elastische taken, waarmee de queryresultaten retourneren van resultaat van taak uitvoering toobe vastgelegd in een Uitvoerdatabase en tabel.</span><span class="sxs-lookup"><span data-stu-id="8f926-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="8f926-124">Hallo Wingtip toepassingsscripts ophalen</span><span class="sxs-lookup"><span data-stu-id="8f926-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="8f926-125">Hallo Wingtip SaaS-scripts en broncode van toepassing zijn beschikbaar in Hallo [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="8f926-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="8f926-126">[Stappen toodownload Hallo Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="8f926-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="8f926-127">Implementeer een database voor de analytics-resultaten van de tenant</span><span class="sxs-lookup"><span data-stu-id="8f926-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="8f926-128">Deze zelfstudie moet u een database geïmplementeerde toocapture Hallo resultaat is van een taak uitvoeren van scripts query's retourneren van resultaten bevatten toohave.</span><span class="sxs-lookup"><span data-stu-id="8f926-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="8f926-129">We maken hiervoor een database met de naam tenantanalytics.</span><span class="sxs-lookup"><span data-stu-id="8f926-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="8f926-130">Open... \\Learning-Modules\\operationele Analytics\\Tenant Analytics\\*Demo TenantAnalyticsDB.ps1* in Hallo *PowerShell ISE* en instellen Hallo waarde te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f926-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="8f926-131">**$DemoScenario** = **2** *Operational analytics-database implementeren*</span><span class="sxs-lookup"><span data-stu-id="8f926-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="8f926-132">Druk op **F5** toorun hello demoscript (die Hallo aanroepen *implementeren TenantAnalyticsDB.ps1* script) die Hallo tenant analytics-database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f926-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="8f926-133">Sommige gegevens voor Hallo demo maken</span><span class="sxs-lookup"><span data-stu-id="8f926-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="8f926-134">Open... \\Learning-Modules\\operationele Analytics\\Tenant Analytics\\*Demo TenantAnalyticsDB.ps1* in Hallo *PowerShell ISE* en instellen Hallo waarde te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f926-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="8f926-135">**$DemoScenario** = **1** *Tickets kopen voor voorstellingen bij alle theaters*</span><span class="sxs-lookup"><span data-stu-id="8f926-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="8f926-136">Druk op **F5** toorun Hallo script en ticket Historie inkoop te maken.</span><span class="sxs-lookup"><span data-stu-id="8f926-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="8f926-137">Maken van een geplande taak tooretrieve tenant analytics over ticket aankopen</span><span class="sxs-lookup"><span data-stu-id="8f926-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="8f926-138">Dit script maakt een taak tooretrieve ticket-aankoopgegevens van alle tenants.</span><span class="sxs-lookup"><span data-stu-id="8f926-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="8f926-139">Zodra samengevoegd in één tabel, kunt u uitgebreide begrijpelijke manier mee metrische gegevens over ticket patronen aanschaffen via Hallo tenants toegang.</span><span class="sxs-lookup"><span data-stu-id="8f926-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="8f926-140">Open SSMS en verbind toohello catalogus -&lt;gebruiker&gt;. database.windows.net server</span><span class="sxs-lookup"><span data-stu-id="8f926-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="8f926-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="8f926-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="8f926-142">Wijzig &lt;gebruiker&gt;, gebruik Hallo-gebruikersnaam gebruikt wanneer u geïmplementeerd Hallo Wingtip SaaS app Hallo boven aan het Hallo-script **sp\_toevoegen\_doel\_groep\_lid** en **sp\_toevoegen\_taakstap**</span><span class="sxs-lookup"><span data-stu-id="8f926-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="8f926-143">Klik met de rechtermuisknop, selecteer **verbinding**, en maak verbinding toohello catalogus -&lt;gebruiker&gt;. database.windows.net server, indien nog niet verbonden</span><span class="sxs-lookup"><span data-stu-id="8f926-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="8f926-144">Zorg ervoor dat u bent verbonden toohello **jobaccount** database en druk op **F5** Hallo-script uit te voeren</span><span class="sxs-lookup"><span data-stu-id="8f926-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="8f926-145">**SP\_toevoegen\_doel\_groep** Hallo doelgroepnaam maakt *TenantGroup*, nu we tooadd doelleden moeten.</span><span class="sxs-lookup"><span data-stu-id="8f926-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="8f926-146">**SP\_toevoegen\_doel\_groep\_lid** voegt een *server* doeltype lid, die alle databases binnen die server (Opmerking Dit is Hallo customer1 - acht &lt;Gebruiker&gt; -server op Hallo tenant databases met) op het moment van taak uitvoering moet worden opgenomen in Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="8f926-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="8f926-147">**sp\_add\_job** maakt een nieuwe wekelijks geplande taak met de naam “Ticket Purchases from all Tenants”</span><span class="sxs-lookup"><span data-stu-id="8f926-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="8f926-148">**SP\_toevoegen\_taakstap** Hallo taakstap met T-SQL-opdracht tekst tooretrieve alle aankoopgegevens voor Hallo ticket maakt van alle tenants en kopiëren Hallo retourneren resultaten in een tabel met de naam  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="8f926-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="8f926-149">Hallo resterende weergaven in Hallo script weergegeven Hallo bestaan Hallo-objecten en uitvoeren van de monitor-taak.</span><span class="sxs-lookup"><span data-stu-id="8f926-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="8f926-150">Bekijk Hallo statuswaarde van Hallo **lifecycle** kolom toomonitor Hallo status.</span><span class="sxs-lookup"><span data-stu-id="8f926-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="8f926-151">Eenmaal is voltooid, Hallo-taak is voltooid voor alle databases van de tenant en hello twee extra databases met Hallo verwijzen naar tabel.</span><span class="sxs-lookup"><span data-stu-id="8f926-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="8f926-152">Correct functioneert Hallo script moet resulteren in vergelijkbare resultaten:</span><span class="sxs-lookup"><span data-stu-id="8f926-152">Successfully running hello script should result in similar results:</span></span>

![resultaten](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="8f926-154">Een taak tooretrieve samenvatting aantal ticket van alle tenants koopt maken</span><span class="sxs-lookup"><span data-stu-id="8f926-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="8f926-155">Dit script maakt een taak tooretrieve som van alle ticket aankopen van alle tenants.</span><span class="sxs-lookup"><span data-stu-id="8f926-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="8f926-156">Open van SSMS en maak verbinding toohello *catalogus -&lt;gebruiker&gt;. database.windows.net* server</span><span class="sxs-lookup"><span data-stu-id="8f926-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="8f926-157">Open Hallo bestand... \\Learning-Modules\\inrichten en catalogus\\operationele Analytics\\Tenant Analytics\\*resultaten TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="8f926-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="8f926-158">Wijzig &lt;gebruiker&gt;, gebruik Hallo-gebruikersnaam gebruikt wanneer u geïmplementeerd in Hallo-script in Hallo Hallo Wingtip SaaS-app **sp\_toevoegen\_taakstap** opgeslagen procedure</span><span class="sxs-lookup"><span data-stu-id="8f926-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="8f926-159">Klik met de rechtermuisknop, selecteer **verbinding**, en maak verbinding toohello catalogus -&lt;gebruiker&gt;. database.windows.net server, indien nog niet verbonden</span><span class="sxs-lookup"><span data-stu-id="8f926-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="8f926-160">Zorg ervoor dat u bent verbonden toohello **tenantanalytics** database en druk op **F5** Hallo-script uit te voeren</span><span class="sxs-lookup"><span data-stu-id="8f926-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="8f926-161">Correct functioneert Hallo script moet resulteren in vergelijkbare resultaten:</span><span class="sxs-lookup"><span data-stu-id="8f926-161">Successfully running hello script should result in similar results:</span></span>

![resultaten](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="8f926-163">**sp\_add\_job** maakt een nieuwe wekelijks geplande taak met de naam “ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="8f926-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="8f926-164">**SP\_toevoegen\_taakstap** Hallo taakstap met T-SQL-opdracht tekst tooretrieve alle aankoopgegevens voor Hallo ticket maakt van alle tenants en kopiëren Hallo retourneren resultaten in een tabel met de naam CountofTicketOrders</span><span class="sxs-lookup"><span data-stu-id="8f926-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="8f926-165">Hallo resterende weergaven in Hallo script weergegeven Hallo bestaan Hallo-objecten en uitvoeren van de monitor-taak.</span><span class="sxs-lookup"><span data-stu-id="8f926-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="8f926-166">Bekijk Hallo statuswaarde van Hallo **lifecycle** kolom toomonitor Hallo status.</span><span class="sxs-lookup"><span data-stu-id="8f926-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="8f926-167">Eenmaal is voltooid, Hallo-taak is voltooid voor alle databases van de tenant en hello twee extra databases met Hallo verwijzen naar tabel.</span><span class="sxs-lookup"><span data-stu-id="8f926-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8f926-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8f926-168">Next steps</span></span>

<span data-ttu-id="8f926-169">In deze zelfstudie hebt u het volgende geleerd:</span><span class="sxs-lookup"><span data-stu-id="8f926-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8f926-170">U hebt een tenant analytics-database geïmplementeerd</span><span class="sxs-lookup"><span data-stu-id="8f926-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="8f926-171">Een geplande taak tooretrieve analytische gegevens maken voor tenants</span><span class="sxs-lookup"><span data-stu-id="8f926-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="8f926-172">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="8f926-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8f926-173">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8f926-173">Additional resources</span></span>

* <span data-ttu-id="8f926-174">Aanvullende [zelfstudies waarin voort op Hallo Wingtip SaaS-toepassing bouwen](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="8f926-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="8f926-175">Elastische taken</span><span class="sxs-lookup"><span data-stu-id="8f926-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
