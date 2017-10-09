---
title: 'Azure Portal: een SQL-database maken | Microsoft Docs'
description: Meer informatie over hoe Hallo toocreate een logische SQL Database-server, firewallregel op serverniveau en databases die in Azure-portal. U leert ook tooquery een Azure SQL database met behulp van hello Azure-portal.
keywords: zelfstudie over sql-database, een sql-database maken
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: aeb8c4c3-6ae2-45f7-b2c3-fa13e3752eed
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: portal
ms.devlang: na
ms.topic: hero-article
ms.date: 05/30/2017
ms.author: carlrab
ms.openlocfilehash: d30352d834f2007e0b6b3eabfc3c108c61479b22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-database-in-hello-azure-portal"></a><span data-ttu-id="16c09-105">Maken van een Azure SQL database in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="16c09-105">Create an Azure SQL database in hello Azure portal</span></span>

<span data-ttu-id="16c09-106">Deze zelfstudie wordt uitgelegd hoe toocreate een SQL-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="16c09-106">This quick start tutorial walks through how toocreate a SQL database in Azure.</span></span> <span data-ttu-id="16c09-107">Azure SQL-Database is een 'Database-as-a-Service' waarmee u toorun en schaal maximaal beschikbare SQL Server-databases in Hallo cloud aanbieden.</span><span class="sxs-lookup"><span data-stu-id="16c09-107">Azure SQL Database is a “Database-as-a-Service” offering that enables you toorun and scale highly available SQL Server databases in hello cloud.</span></span> <span data-ttu-id="16c09-108">Deze snel starten ziet u hoe tooget gestart door het maken van een SQL-database met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="16c09-108">This quick start shows you how tooget started by creating a SQL database using hello Azure portal.</span></span>

<span data-ttu-id="16c09-109">Als u nog geen Azure-abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="16c09-109">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-toohello-azure-portal"></a><span data-ttu-id="16c09-110">Meld u bij toohello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="16c09-110">Log in toohello Azure portal</span></span>

<span data-ttu-id="16c09-111">Meld u bij toohello [Azure-portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="16c09-111">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="16c09-112">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="16c09-112">Create a SQL database</span></span>

<span data-ttu-id="16c09-113">Een Azure SQL-database wordt gemaakt met een gedefinieerde set [reken- en opslagresources](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="16c09-113">An Azure SQL database is created with a defined set of [compute and storage resources](sql-database-service-tiers.md).</span></span> <span data-ttu-id="16c09-114">Hallo-database wordt gemaakt binnen een [Azure-resourcegroep](../azure-resource-manager/resource-group-overview.md) en in een [logische Azure SQL Database-server](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="16c09-114">hello database is created within an [Azure resource group](../azure-resource-manager/resource-group-overview.md) and in an [Azure SQL Database logical server](sql-database-features.md).</span></span> 

<span data-ttu-id="16c09-115">Volg deze stappen toocreate een SQL-database met voorbeeldgegevens van Hallo LT van Adventure Works.</span><span class="sxs-lookup"><span data-stu-id="16c09-115">Follow these steps toocreate a SQL database containing hello Adventure Works LT sample data.</span></span> 

1. <span data-ttu-id="16c09-116">Klik op Hallo **nieuw** knop gevonden op Hallo linkerbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="16c09-116">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>

2. <span data-ttu-id="16c09-117">Selecteer **Databases** van Hallo **nieuw** pagina en selecteer **SQL-Database** van Hallo **Databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="16c09-117">Select **Databases** from hello **New** page, and select **SQL Database** from hello **Databases** page.</span></span>

   ![database-1 maken](./media/sql-database-get-started-portal/create-database-1.png)

3. <span data-ttu-id="16c09-119">Hallo SQL-Database formulier invullen Hello volgende informatie, zoals wordt weergegeven op Hallo voorafgaand aan de installatiekopie:</span><span class="sxs-lookup"><span data-stu-id="16c09-119">Fill out hello SQL Database form with hello following information, as shown on hello preceding image:</span></span>   

   | <span data-ttu-id="16c09-120">Instelling</span><span class="sxs-lookup"><span data-stu-id="16c09-120">Setting</span></span>       | <span data-ttu-id="16c09-121">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="16c09-121">Suggested value</span></span> | <span data-ttu-id="16c09-122">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="16c09-122">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="16c09-123">**Databasenaam**</span><span class="sxs-lookup"><span data-stu-id="16c09-123">**Database name**</span></span> | <span data-ttu-id="16c09-124">mySampleDatabase</span><span class="sxs-lookup"><span data-stu-id="16c09-124">mySampleDatabase</span></span> | <span data-ttu-id="16c09-125">Zie [Database-id's](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) voor geldige databasenamen.</span><span class="sxs-lookup"><span data-stu-id="16c09-125">For valid database names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> | 
   | <span data-ttu-id="16c09-126">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="16c09-126">**Subscription**</span></span> | <span data-ttu-id="16c09-127">Uw abonnement</span><span class="sxs-lookup"><span data-stu-id="16c09-127">Your subscription</span></span>  | <span data-ttu-id="16c09-128">Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="16c09-128">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="16c09-129">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="16c09-129">**Resource group**</span></span>  | <span data-ttu-id="16c09-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="16c09-130">myResourceGroup</span></span> | <span data-ttu-id="16c09-131">Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen.</span><span class="sxs-lookup"><span data-stu-id="16c09-131">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="16c09-132">**Bron selecteren**</span><span class="sxs-lookup"><span data-stu-id="16c09-132">**Source source**</span></span> | <span data-ttu-id="16c09-133">Sample (AdventureWorksLT)</span><span class="sxs-lookup"><span data-stu-id="16c09-133">Sample (AdventureWorksLT)</span></span> | <span data-ttu-id="16c09-134">Hallo AdventureWorksLT schema en de gegevens laadt in de nieuwe database</span><span class="sxs-lookup"><span data-stu-id="16c09-134">Loads hello AdventureWorksLT schema and data into your new database</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="16c09-135">U moet de voorbeelddatabase Hallo op dit formulier selecteren omdat deze wordt gebruikt in Hallo rest van deze snel starten.</span><span class="sxs-lookup"><span data-stu-id="16c09-135">You must select hello sample database on this form because it is used in hello remainder of this quick start.</span></span>
   > 

4. <span data-ttu-id="16c09-136">Onder **Server**, klikt u op **vereiste instellingen configureren** en vul Hallo formulier voor SQL server (logische server) met Hallo informatie, zoals wordt weergegeven op Hallo installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="16c09-136">Under **Server**, click **Configure required settings** and fill out hello SQL server (logical server) form with hello following information, as shown on hello following image:</span></span>   

   | <span data-ttu-id="16c09-137">Instelling</span><span class="sxs-lookup"><span data-stu-id="16c09-137">Setting</span></span>       | <span data-ttu-id="16c09-138">Voorgestelde waarde</span><span class="sxs-lookup"><span data-stu-id="16c09-138">Suggested value</span></span> | <span data-ttu-id="16c09-139">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="16c09-139">Description</span></span> | 
   | ------------ | ------------------ | ------------------------------------------------- | 
   | <span data-ttu-id="16c09-140">**Servernaam**</span><span class="sxs-lookup"><span data-stu-id="16c09-140">**Server name**</span></span> | <span data-ttu-id="16c09-141">Een wereldwijd unieke naam</span><span class="sxs-lookup"><span data-stu-id="16c09-141">Any globally unique name</span></span> | <span data-ttu-id="16c09-142">Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige servernamen.</span><span class="sxs-lookup"><span data-stu-id="16c09-142">For valid server names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> | 
   | <span data-ttu-id="16c09-143">**Aanmeldgegevens van serverbeheerder**</span><span class="sxs-lookup"><span data-stu-id="16c09-143">**Server admin login**</span></span> | <span data-ttu-id="16c09-144">Een geldige naam</span><span class="sxs-lookup"><span data-stu-id="16c09-144">Any valid name</span></span> | <span data-ttu-id="16c09-145">Zie [Database-id's](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers) voor geldige aanmeldingsnamen.</span><span class="sxs-lookup"><span data-stu-id="16c09-145">For valid login names, see [Database Identifiers](https://docs.microsoft.com/en-us/sql/relational-databases/databases/database-identifiers).</span></span> |
   | <span data-ttu-id="16c09-146">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="16c09-146">**Password**</span></span> | <span data-ttu-id="16c09-147">Een geldig wachtwoord</span><span class="sxs-lookup"><span data-stu-id="16c09-147">Any valid password</span></span> | <span data-ttu-id="16c09-148">Uw wachtwoord moet ten minste 8 tekens bestaan en moet tekens bevatten uit drie van de volgende categorieën Hallo: hoofdletters, kleine letters, cijfers en en niet-alfanumerieke tekens bevatten.</span><span class="sxs-lookup"><span data-stu-id="16c09-148">Your password must have at least 8 characters and must contain characters from three of hello following categories: upper case characters, lower case characters, numbers, and and non-alphanumeric characters.</span></span> |
   | <span data-ttu-id="16c09-149">**Abonnement**</span><span class="sxs-lookup"><span data-stu-id="16c09-149">**Subscription**</span></span> | <span data-ttu-id="16c09-150">Uw abonnement</span><span class="sxs-lookup"><span data-stu-id="16c09-150">Your subscription</span></span> | <span data-ttu-id="16c09-151">Zie [Abonnementen](https://account.windowsazure.com/Subscriptions) voor meer informatie over uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="16c09-151">For details about your subscriptions, see [Subscriptions](https://account.windowsazure.com/Subscriptions).</span></span> |
   | <span data-ttu-id="16c09-152">**Resourcegroep**</span><span class="sxs-lookup"><span data-stu-id="16c09-152">**Resource group**</span></span> | <span data-ttu-id="16c09-153">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="16c09-153">myResourceGroup</span></span> | <span data-ttu-id="16c09-154">Zie [Naming conventions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions) (Naamgevingsconventies) voor geldige resourcegroepnamen.</span><span class="sxs-lookup"><span data-stu-id="16c09-154">For valid resource group names, see [Naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions).</span></span> |
   | <span data-ttu-id="16c09-155">**Locatie**</span><span class="sxs-lookup"><span data-stu-id="16c09-155">**Location**</span></span> | <span data-ttu-id="16c09-156">Een geldige locatie</span><span class="sxs-lookup"><span data-stu-id="16c09-156">Any valid location</span></span> | <span data-ttu-id="16c09-157">Zie [Azure-regio's](https://azure.microsoft.com/regions/) voor informatie over regio's.</span><span class="sxs-lookup"><span data-stu-id="16c09-157">For information about regions, see [Azure Regions](https://azure.microsoft.com/regions/).</span></span> |

   > [!IMPORTANT]
   > <span data-ttu-id="16c09-158">aanmeldgegevens van serverbeheerder Hallo en het wachtwoord dat u hier opgeeft, zijn vereiste toolog in toohello server en de databases verderop in dit snel starten.</span><span class="sxs-lookup"><span data-stu-id="16c09-158">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="16c09-159">Onthoud of noteer deze informatie voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="16c09-159">Remember or record this information for later use.</span></span> 
   >  

   ![database-server maken](./media/sql-database-get-started-portal/create-database-server.png)

5. <span data-ttu-id="16c09-161">Wanneer u Hallo formulier hebt ingevuld, klikt u op **Selecteer**.</span><span class="sxs-lookup"><span data-stu-id="16c09-161">When you have completed hello form, click **Select**.</span></span>

6. <span data-ttu-id="16c09-162">Klik op **prijscategorie** toospecify Hallo prijscategorie en prestatieniveau serviceniveau voor de nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="16c09-162">Click **Pricing tier** toospecify hello service tier and performance level for your new database.</span></span> <span data-ttu-id="16c09-163">Gebruik Hallo schuifregelaar tooselect **20 dtu's** en **250** GB aan opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="16c09-163">Use hello slider tooselect **20 DTUs** and **250** GB of storage.</span></span> <span data-ttu-id="16c09-164">Zie [Wat is een DTU?](sql-database-what-is-a-dtu.md) voor meer informatie over DTU's.</span><span class="sxs-lookup"><span data-stu-id="16c09-164">For more information on DTUs, see [What is a DTU?](sql-database-what-is-a-dtu.md).</span></span>

   ![database-s1 maken](./media/sql-database-get-started-portal/create-database-s1.png)

7. <span data-ttu-id="16c09-166">Klik na het geselecteerde Hallo hoeveelheid dtu's op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="16c09-166">After selected hello amount of DTUs, click **Apply**.</span></span>  

8. <span data-ttu-id="16c09-167">Nu u Hallo SQL-Database formulier hebt ingevuld, klikt u op **maken** tooprovision Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="16c09-167">Now that you have completed hello SQL Database form, click **Create** tooprovision hello database.</span></span> <span data-ttu-id="16c09-168">De inrichting duurt een paar minuten.</span><span class="sxs-lookup"><span data-stu-id="16c09-168">Provisioning takes a few minutes.</span></span> 

9. <span data-ttu-id="16c09-169">Op de werkbalk Hallo **meldingen** toomonitor Hallo-implementatieproces.</span><span class="sxs-lookup"><span data-stu-id="16c09-169">On hello toolbar, click **Notifications** toomonitor hello deployment process.</span></span>

   ![melding](./media/sql-database-get-started-portal/notification.png)

## <a name="create-a-server-level-firewall-rule"></a><span data-ttu-id="16c09-171">Een serverfirewallregel maken</span><span class="sxs-lookup"><span data-stu-id="16c09-171">Create a server-level firewall rule</span></span>

<span data-ttu-id="16c09-172">Hallo SQL Database-service maakt een firewall op Hallo-serverniveau waarmee wordt voorkomen dat externe toepassingen en hulpprogramma's verbinden toohello server of een database op de server Hallo tenzij een firewallregel tooopen Hallo firewall voor specifieke IP-adressen is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16c09-172">hello SQL Database service creates a firewall at hello server-level that prevents external applications and tools from connecting toohello server or any databases on hello server unless a firewall rule is created tooopen hello firewall for specific IP addresses.</span></span> <span data-ttu-id="16c09-173">Volg deze stappen toocreate een [SQL-Database firewallregel op serverniveau](sql-database-firewall-configure.md) voor uw client-IP-adressen en inschakelen van externe connectiviteit via Hallo SQL Database-firewall voor uw IP-adres.</span><span class="sxs-lookup"><span data-stu-id="16c09-173">Follow these steps toocreate a [SQL Database server-level firewall rule](sql-database-firewall-configure.md) for your client's IP address and enable external connectivity through hello SQL Database firewall for your IP address only.</span></span> 

> [!NOTE]
> <span data-ttu-id="16c09-174">SQL Database communiceert via poort 1433.</span><span class="sxs-lookup"><span data-stu-id="16c09-174">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="16c09-175">Als u tooconnect van binnen een bedrijfsnetwerk probeert, kan uitgaand verkeer via poort 1433 niet worden toegestaan door de firewall van uw netwerk.</span><span class="sxs-lookup"><span data-stu-id="16c09-175">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="16c09-176">Als dit het geval is, kunt u tooyour Azure SQL Database-server kan geen verbinding tenzij uw IT-afdeling poort 1433 wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="16c09-176">If so, you cannot connect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

1. <span data-ttu-id="16c09-177">Nadat het Hallo-implementatie is voltooid, klikt u op **SQL-databases** van Hallo links menu en klik vervolgens op **mySampleDatabase** op Hallo **SQL-databases** pagina.</span><span class="sxs-lookup"><span data-stu-id="16c09-177">After hello deployment completes, click **SQL databases** from hello left-hand menu and then click **mySampleDatabase** on hello **SQL databases** page.</span></span> <span data-ttu-id="16c09-178">Hallo overzichtspagina voor uw database wordt geopend, waarin u Hallo volledig gekwalificeerde servernaam (zoals **mynewserver20170313.database.windows.net**) en biedt opties voor verdere configuratie.</span><span class="sxs-lookup"><span data-stu-id="16c09-178">hello overview page for your database opens, showing you hello fully qualified server name (such as **mynewserver20170313.database.windows.net**) and provides options for further configuration.</span></span> <span data-ttu-id="16c09-179">Kopieer deze volledig gekwalificeerde servernaam voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="16c09-179">Copy this fully qualified server name for use later.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="16c09-180">U moet deze server volledig gekwalificeerde naam tooconnect tooyour server en de databases in de volgende snel aan de slag.</span><span class="sxs-lookup"><span data-stu-id="16c09-180">You need this fully qualified server name tooconnect tooyour server and its databases in subsequent quick starts.</span></span>
   > 

   ![servernaam](./media/sql-database-connect-query-dotnet/server-name.png) 

2. <span data-ttu-id="16c09-182">Klik op **serverfirewall ingesteld** op Hallo werkbalk zoals weergegeven in de vorige afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="16c09-182">Click **Set server firewall** on hello toolbar as shown in hello previous image.</span></span> <span data-ttu-id="16c09-183">Hallo **Firewall-instellingen** pagina voor Hallo SQL Database-server wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="16c09-183">hello **Firewall settings** page for hello SQL Database server opens.</span></span> 

   ![serverfirewallregel](./media/sql-database-get-started-portal/server-firewall-rule.png) 

3. <span data-ttu-id="16c09-185">Klik op **client-IP toevoegen** op Hallo werkbalk tooadd nieuwe firewallregel tooa van uw huidige IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="16c09-185">Click **Add client IP** on hello toolbar tooadd your current IP address tooa new firewall rule.</span></span> <span data-ttu-id="16c09-186">Een firewallregel kan poort 1433 openen voor een afzonderlijk IP-adres of voor een aantal IP-adressen.</span><span class="sxs-lookup"><span data-stu-id="16c09-186">A firewall rule can open port 1433 for a single IP address or a range of IP addresses.</span></span>

4. <span data-ttu-id="16c09-187">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="16c09-187">Click **Save**.</span></span> <span data-ttu-id="16c09-188">Een firewallregel op serverniveau is gemaakt voor uw huidige IP-adres poort 1433 op Hallo logische server te openen.</span><span class="sxs-lookup"><span data-stu-id="16c09-188">A server-level firewall rule is created for your current IP address opening port 1433 on hello logical server.</span></span>

   ![serverfirewallregel instellen](./media/sql-database-get-started-portal/server-firewall-rule-set.png) 

4. <span data-ttu-id="16c09-190">Klik op **OK** en sluit vervolgens Hallo **Firewall-instellingen** pagina.</span><span class="sxs-lookup"><span data-stu-id="16c09-190">Click **OK** and then close hello **Firewall settings** page.</span></span>

<span data-ttu-id="16c09-191">U kunt nu verbinding toohello SQL Database-server en de databases met SQL Server Management Studio of een ander hulpprogramma naar keuze van deze IP-adres met Hallo beheerder serveraccount eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16c09-191">You can now connect toohello SQL Database server and its databases using SQL Server Management Studio or another tool of your choice from this IP address using hello server admin account created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16c09-192">Toegang via Hallo SQL Database-firewall is standaard ingeschakeld voor alle Azure-services.</span><span class="sxs-lookup"><span data-stu-id="16c09-192">By default, access through hello SQL Database firewall is enabled for all Azure services.</span></span> <span data-ttu-id="16c09-193">Klik op **OFF** op deze pagina toodisable voor alle Azure-services.</span><span class="sxs-lookup"><span data-stu-id="16c09-193">Click **OFF** on this page toodisable for all Azure services.</span></span>
>

## <a name="query-hello-sql-database"></a><span data-ttu-id="16c09-194">Query Hallo SQL-database</span><span class="sxs-lookup"><span data-stu-id="16c09-194">Query hello SQL database</span></span>

<span data-ttu-id="16c09-195">Nu dat u een voorbeelddatabase in Azure gemaakt hebt, gaan we Hallo ingebouwde query hulpprogramma binnen hello Azure portal tooconfirm dat u verbinding toohello database en query Hallo gegevens maken kunt te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="16c09-195">Now that you have created a sample database in Azure, let’s use hello built-in query tool within hello Azure portal tooconfirm that you can connect toohello database and query hello data.</span></span> 

1. <span data-ttu-id="16c09-196">Hallo pagina van de SQL-Database voor uw database, klik op **extra** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="16c09-196">On hello SQL Database page for your database, click **Tools** on hello toolbar.</span></span> <span data-ttu-id="16c09-197">Hallo **extra** pagina wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="16c09-197">hello **Tools** page opens.</span></span>

   ![menu extra](./media/sql-database-get-started-portal/tools-menu.png) 

2. <span data-ttu-id="16c09-199">Klik op **Query-editor (preview)**, klikt u op Hallo **Preview-voorwaarden** selectievakje, en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="16c09-199">Click **Query editor (preview)**, click hello **Preview terms** checkbox, and then click **OK**.</span></span> <span data-ttu-id="16c09-200">pagina Hallo Query-editor wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="16c09-200">hello Query editor page opens.</span></span>

3. <span data-ttu-id="16c09-201">Klik op **aanmelding** en selecteer vervolgens desgevraagd **SQL server-verificatie** en geef aanmeldgegevens van serverbeheerder Hallo en het wachtwoord die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16c09-201">Click **Login** and then, when prompted, select **SQL server authentication** and then provide hello server admin login and password that you created earlier.</span></span>

   ![aanmelding](./media/sql-database-get-started-portal/login.png) 

4. <span data-ttu-id="16c09-203">Klik op **OK** toolog in.</span><span class="sxs-lookup"><span data-stu-id="16c09-203">Click **OK** toolog in.</span></span>

5. <span data-ttu-id="16c09-204">Nadat u bent geverifieerd, typt u de volgende query in de editor Querydeelvenster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="16c09-204">After you are authenticated, type hello following query in hello query editor pane.</span></span>

   ```sql
   SELECT TOP 20 pc.Name as CategoryName, p.name as ProductName
   FROM SalesLT.ProductCategory pc
   JOIN SalesLT.Product p
   ON pc.productcategoryid = p.productcategoryid;
   ```

6. <span data-ttu-id="16c09-205">Klik op **uitvoeren** en bekijk vervolgens de queryresultaten Hallo in Hallo **resultaten** deelvenster.</span><span class="sxs-lookup"><span data-stu-id="16c09-205">Click **Run** and then review hello query results in hello **Results** pane.</span></span>

   ![resultaten queryeditor](./media/sql-database-get-started-portal/query-editor-results.png)

7. <span data-ttu-id="16c09-207">Sluit Hallo **Query-editor** pagina en Hallo **extra** pagina.</span><span class="sxs-lookup"><span data-stu-id="16c09-207">Close hello **Query editor** page and hello **Tools** page.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="16c09-208">Resources opschonen</span><span class="sxs-lookup"><span data-stu-id="16c09-208">Clean up resources</span></span>

<span data-ttu-id="16c09-209">Als u deze resources niet nodig voor een andere Quick Start/zelfstudie (Zie [Vervolgstappen](#next-steps)), kunt u ze verwijderen door Hallo volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="16c09-209">If you don't need these resources for another quickstart/tutorial (see [Next steps](#next-steps)), you can delete them by doing hello following:</span></span>


1. <span data-ttu-id="16c09-210">Hallo links menu in hello Azure-portal en klik op **resourcegroepen** en klik vervolgens op **myResourceGroup**.</span><span class="sxs-lookup"><span data-stu-id="16c09-210">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click **myResourceGroup**.</span></span> 
2. <span data-ttu-id="16c09-211">Klik op de pagina van de groep resource **verwijderen**, type **myResourceGroup** in Hallo in het tekstvak en klik vervolgens op **verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="16c09-211">On your resource group page, click **Delete**, type **myResourceGroup** in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16c09-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="16c09-212">Next steps</span></span>

<span data-ttu-id="16c09-213">Nu u een database hebt, kunt u verbinding maken met een hulpprogramma naar keuze en hiermee query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="16c09-213">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="16c09-214">Klik op de onderstaande hulpprogramma's voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="16c09-214">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="16c09-215">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="16c09-215">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="16c09-216">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="16c09-216">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="16c09-217">.NET</span><span class="sxs-lookup"><span data-stu-id="16c09-217">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="16c09-218">PHP</span><span class="sxs-lookup"><span data-stu-id="16c09-218">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="16c09-219">Node.js</span><span class="sxs-lookup"><span data-stu-id="16c09-219">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="16c09-220">Java</span><span class="sxs-lookup"><span data-stu-id="16c09-220">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="16c09-221">Python</span><span class="sxs-lookup"><span data-stu-id="16c09-221">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="16c09-222">Ruby</span><span class="sxs-lookup"><span data-stu-id="16c09-222">Ruby</span></span>](sql-database-connect-query-ruby.md)
