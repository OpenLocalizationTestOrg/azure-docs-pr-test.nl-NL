---
title: een Azure SQL Database geografisch verspreide oplossing aaaImplement | Microsoft Docs
description: Meer informatie over tooconfigure uw Azure SQL Database en de toepassing voor failover tooa gerepliceerd database en failover testen.
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,business continuity
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/26/2017
ms.author: carlrab
ms.openlocfilehash: 9295d33c669405108a1a64ef1e7cb77f582773a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="implement-a-geo-distributed-database"></a><span data-ttu-id="b02da-103">Een database geografisch verspreide implementeren</span><span class="sxs-lookup"><span data-stu-id="b02da-103">Implement a geo-distributed database</span></span>

<span data-ttu-id="b02da-104">In deze zelfstudie een Azure SQL-database en de toepassing voor failover-tooa externe regio configureren en vervolgens uw plan failover te testen.</span><span class="sxs-lookup"><span data-stu-id="b02da-104">In this tutorial, you configure an Azure SQL database and application for failover tooa remote region, and then test your failover plan.</span></span> <span data-ttu-id="b02da-105">Procedures voor:</span><span class="sxs-lookup"><span data-stu-id="b02da-105">You learn how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="b02da-106">Maken van databasegebruikers en machtigingen verlenen</span><span class="sxs-lookup"><span data-stu-id="b02da-106">Create database users and grant them permissions</span></span>
> * <span data-ttu-id="b02da-107">Een firewallregel op databaseniveau instellen</span><span class="sxs-lookup"><span data-stu-id="b02da-107">Set up a database-level firewall rule</span></span>
> * <span data-ttu-id="b02da-108">Maak een [geo-replicatie failover-groep](sql-database-geo-replication-overview.md)</span><span class="sxs-lookup"><span data-stu-id="b02da-108">Create a [geo-replication failover group](sql-database-geo-replication-overview.md)</span></span>
> * <span data-ttu-id="b02da-109">Maken en het compileren van een Java-toepassing tooquery een Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="b02da-109">Create and compile a Java application tooquery an Azure SQL database</span></span>
> * <span data-ttu-id="b02da-110">Uitvoeren van een herstel na noodgevallen detailanalyse</span><span class="sxs-lookup"><span data-stu-id="b02da-110">Perform a disaster recovery drill</span></span>

<span data-ttu-id="b02da-111">Als u een Azure-abonnement geen [een gratis account maken](https://azure.microsoft.com/free/) voordat u begint.</span><span class="sxs-lookup"><span data-stu-id="b02da-111">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="b02da-112">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b02da-112">Prerequisites</span></span>

<span data-ttu-id="b02da-113">toocomplete in deze zelfstudie, zorg ervoor dat Hallo volgende vereisten zijn voltooid:</span><span class="sxs-lookup"><span data-stu-id="b02da-113">toocomplete this tutorial, make sure hello following prerequisites are completed:</span></span>

- <span data-ttu-id="b02da-114">Laatste geïnstalleerde Hallo [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="b02da-114">Installed hello latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs).</span></span> 
- <span data-ttu-id="b02da-115">Een Azure SQL database geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b02da-115">Installed an Azure SQL database.</span></span> <span data-ttu-id="b02da-116">In deze zelfstudie wordt de voorbeelddatabase van AdventureWorksLT Hallo met de naam **mySampleDatabase** van een van deze snel aan de slag:</span><span class="sxs-lookup"><span data-stu-id="b02da-116">This tutorial uses hello AdventureWorksLT sample database with a name of **mySampleDatabase** from one of these quick starts:</span></span>

   - [<span data-ttu-id="b02da-117">Database maken - Portal</span><span class="sxs-lookup"><span data-stu-id="b02da-117">Create DB - Portal</span></span>](sql-database-get-started-portal.md)
   - [<span data-ttu-id="b02da-118">Database maken - CLI</span><span class="sxs-lookup"><span data-stu-id="b02da-118">Create DB - CLI</span></span>](sql-database-get-started-cli.md)
   - [<span data-ttu-id="b02da-119">Database maken - PowerShell</span><span class="sxs-lookup"><span data-stu-id="b02da-119">Create DB - PowerShell</span></span>](sql-database-get-started-powershell.md)

- <span data-ttu-id="b02da-120">Een methode tooexecute SQL hebt geïdentificeerd-scripts uitvoeren op uw database, kunt u een van de volgende hulpprogramma's voor query Hallo:</span><span class="sxs-lookup"><span data-stu-id="b02da-120">Have identified a method tooexecute SQL scripts against your database, you can use one of hello following query tools:</span></span>
   - <span data-ttu-id="b02da-121">query-editor in Hallo Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b02da-121">hello query editor in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b02da-122">Zie voor meer informatie over het gebruik van Hallo query-editor in Azure-portal Hallo [Connect en query Query-Editor met](sql-database-get-started-portal.md#query-the-sql-database).</span><span class="sxs-lookup"><span data-stu-id="b02da-122">For more information on using hello query editor in hello Azure portal, see [Connect and query using Query Editor](sql-database-get-started-portal.md#query-the-sql-database).</span></span>
   - <span data-ttu-id="b02da-123">de nieuwste versie Hallo van [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), dit is een geïntegreerde omgeving voor het beheren van elke SQL-infrastructuur van tooSQL van SQL Server-Database voor Microsoft Windows.</span><span class="sxs-lookup"><span data-stu-id="b02da-123">hello newest version of [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms), which is an integrated environment for managing any SQL infrastructure, from SQL Server tooSQL Database for Microsoft Windows.</span></span>
   - <span data-ttu-id="b02da-124">Hallo nieuwste versie van [Visual Studio Code](https://code.visualstudio.com/docs), die een grafische code-editor voor Linux, Mac OS, en Windows die ondersteuning biedt voor extensies, met inbegrip Hallo [mssql-extensie](https://aka.ms/mssql-marketplace) voor query's in Microsoft SQL Server , Azure SQL Database en SQL datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="b02da-124">hello newest version of [Visual Studio Code](https://code.visualstudio.com/docs), which is a graphical code editor for Linux, macOS, and Windows that supports extensions, including hello [mssql extension](https://aka.ms/mssql-marketplace) for querying Microsoft SQL Server, Azure SQL Database, and SQL Data Warehouse.</span></span> <span data-ttu-id="b02da-125">Zie voor meer informatie over het gebruik van dit hulpprogramma met Azure SQL Database [Connect en query met de Code van de VS](sql-database-connect-query-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="b02da-125">For more information on using this tool with Azure SQL Database, see [Connect and query with VS Code](sql-database-connect-query-vscode.md).</span></span> 

## <a name="create-database-users-and-grant-permissions"></a><span data-ttu-id="b02da-126">Maken van databasegebruikers en machtigingen verlenen</span><span class="sxs-lookup"><span data-stu-id="b02da-126">Create database users and grant permissions</span></span>

<span data-ttu-id="b02da-127">Verbinding maken met database tooyour en Maak gebruikersaccounts met behulp van een Hallo hulpmiddelen voor query's te volgen:</span><span class="sxs-lookup"><span data-stu-id="b02da-127">Connect tooyour database and create user accounts using one of hello following query tools:</span></span>

- <span data-ttu-id="b02da-128">Hallo Query-editor in hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="b02da-128">hello Query editor in hello Azure portal</span></span>
- <span data-ttu-id="b02da-129">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="b02da-129">SQL Server Management Studio</span></span>
- <span data-ttu-id="b02da-130">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b02da-130">Visual Studio Code</span></span>

<span data-ttu-id="b02da-131">Deze gebruikersaccounts repliceren automatisch tooyour secundaire server (en gesynchroniseerd blijven).</span><span class="sxs-lookup"><span data-stu-id="b02da-131">These user accounts replicate automatically tooyour secondary server (and be kept in sync).</span></span> <span data-ttu-id="b02da-132">toouse SQL Server Management Studio of Visual Studio Code, moet u mogelijk een firewallregel tooconfigure als u verbinding maakt vanaf een client op een IP-adres waarvoor u nog niet hebt geconfigureerd een firewall.</span><span class="sxs-lookup"><span data-stu-id="b02da-132">toouse SQL Server Management Studio or Visual Studio Code, you may need tooconfigure a firewall rule if you are connecting from a client at an IP address for which you have not yet configured a firewall.</span></span> <span data-ttu-id="b02da-133">Zie voor gedetailleerde stappen [maken van een firewallregel op serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="b02da-133">For detailed steps, see [Create a server-level firewall rule](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>

- <span data-ttu-id="b02da-134">Uitvoeren in een query-venster Hallo query toocreate twee accounts voor gebruikers in uw database te volgen.</span><span class="sxs-lookup"><span data-stu-id="b02da-134">In a query window, execute hello following query toocreate two user accounts in your database.</span></span> <span data-ttu-id="b02da-135">Dit script verleent **db_owner** machtigingen toohello **app_admin** -account en verleent **Selecteer** en **UPDATE** machtigingen toohello **app_user** account.</span><span class="sxs-lookup"><span data-stu-id="b02da-135">This script grants **db_owner** permissions toohello **app_admin** account and grants **SELECT** and **UPDATE** permissions toohello **app_user** account.</span></span> 

   ```sql
   CREATE USER app_admin WITH PASSWORD = 'ChangeYourPassword1';
   --Add SQL user toodb_owner role
   ALTER ROLE db_owner ADD MEMBER app_admin; 
   --Create additional SQL user
   CREATE USER app_user WITH PASSWORD = 'ChangeYourPassword1';
   --grant permission tooSalesLT schema
   GRANT SELECT, INSERT, DELETE, UPDATE ON SalesLT.Product tooapp_user;
   ```

## <a name="create-database-level-firewall"></a><span data-ttu-id="b02da-136">Firewallregel op databaseniveau maken</span><span class="sxs-lookup"><span data-stu-id="b02da-136">Create database-level firewall</span></span>

<span data-ttu-id="b02da-137">Maak een [firewallregel op databaseniveau](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) voor uw SQL-database.</span><span class="sxs-lookup"><span data-stu-id="b02da-137">Create a [database-level firewall rule](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-set-database-firewall-rule-azure-sql-database) for your SQL database.</span></span> <span data-ttu-id="b02da-138">Deze firewallregel op databaseniveau repliceert automatisch toohello secundaire server die u in deze zelfstudie maakt.</span><span class="sxs-lookup"><span data-stu-id="b02da-138">This database-level firewall rule replicates automatically toohello secondary server that you create in this tutorial.</span></span> <span data-ttu-id="b02da-139">Gebruik voor eenvoud (in deze zelfstudie) Hallo openbaar IP-adres van Hallo-computer waarop u Hallo stappen in deze zelfstudie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="b02da-139">For simplicity (in this tutorial), use hello public IP address of hello computer on which you are performing hello steps in this tutorial.</span></span> <span data-ttu-id="b02da-140">toodetermine hello IP-adres voor Hallo serverniveau firewallregel voor de huidige computer, Zie [maken van een firewall serverniveau](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span><span class="sxs-lookup"><span data-stu-id="b02da-140">toodetermine hello IP address used for hello server-level firewall rule for your current computer, see [Create a server-level firewall](sql-database-get-started-portal.md#create-a-server-level-firewall-rule).</span></span>  

- <span data-ttu-id="b02da-141">Hallo query te volgen, Hallo IP-adressen vervangen door een geschikte IP-adressen voor uw omgeving Hallo vervangen Hallo vorige query in het venster openen query.</span><span class="sxs-lookup"><span data-stu-id="b02da-141">In your open query window, replace hello previous query with hello following query, replacing hello IP addresses with hello appropriate IP addresses for your environment.</span></span>  

   ```sql
   -- Create database-level firewall setting for your public IP address
   EXECUTE sp_set_database_firewall_rule @name = N'myGeoReplicationFirewallRule',@start_ip_address = '0.0.0.0', @end_ip_address = '0.0.0.0';
   ```

## <a name="create-an-active-geo-replication-auto-failover-group"></a><span data-ttu-id="b02da-142">Een actieve geo-replicatie automatische failover-groep maken</span><span class="sxs-lookup"><span data-stu-id="b02da-142">Create an active geo-replication auto failover group</span></span> 

<span data-ttu-id="b02da-143">Met Azure PowerShell maken een [actieve geo-replicatie automatische failover groep](sql-database-geo-replication-overview.md) tussen uw bestaande Azure SQL-server en Hallo nieuwe Azure SQL-server in een Azure-regio leeg en voeg vervolgens uw voorbeeld database toohello failover-groep.</span><span class="sxs-lookup"><span data-stu-id="b02da-143">Using Azure PowerShell, create an [active geo-replication auto failover group](sql-database-geo-replication-overview.md) between your existing Azure SQL server and hello new empty Azure SQL server in an Azure region, and then add your sample database toohello failover group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b02da-144">Deze cmdlets vereist Azure PowerShell 4.0.</span><span class="sxs-lookup"><span data-stu-id="b02da-144">These cmdlets require Azure PowerShell 4.0.</span></span> [!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install-no-ssh.md)]
>

1. <span data-ttu-id="b02da-145">Variabelen voor de PowerShell-scripts met Hallo waarden voor uw bestaande server en de voorbeelddatabase vullen en geef een globaal unieke waarde voor failover-groepsnaam op.</span><span class="sxs-lookup"><span data-stu-id="b02da-145">Populate variables for your PowerShell scripts using hello values for your existing server and sample database, and provide a globally unique value for failover group name.</span></span>

   ```powershell
   $adminlogin = "ServerAdmin"
   $password = "ChangeYourAdminPassword1"
   $myresourcegroupname = "<your resource group name>"
   $mylocation = "<your resource group location>"
   $myservername = "<your existing server name>"
   $mydatabasename = "mySampleDatabase"
   $mydrlocation = "<your disaster recovery location>"
   $mydrservername = "<your disaster recovery server name>"
   $myfailovergroupname = "<your unique failover group name>"
   ```

2. <span data-ttu-id="b02da-146">Een leeg back-server maken in uw regio failover.</span><span class="sxs-lookup"><span data-stu-id="b02da-146">Create an empty backup server in your failover region.</span></span>

   ```powershell
   $mydrserver = New-AzureRmSqlServer -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername `
      -Location $mydrlocation `
      -SqlAdministratorCredentials $(New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $adminlogin, $(ConvertTo-SecureString -String $password -AsPlainText -Force))
   $mydrserver   
   ```

3. <span data-ttu-id="b02da-147">Een groep failover tussen twee servers Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="b02da-147">Create a failover group between hello two servers.</span></span>

   ```powershell
   $myfailovergroup = New-AzureRMSqlDatabaseFailoverGroup `
      –ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -PartnerServerName $mydrservername  `
      –FailoverGroupName $myfailovergroupname `
      –FailoverPolicy Automatic `
      -GracePeriodWithDataLossHours 2
   $myfailovergroup   
   ```

4. <span data-ttu-id="b02da-148">Uw database toohello failover-groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b02da-148">Add your database toohello failover group.</span></span>

   ```powershell
   $myfailovergroup = Get-AzureRmSqlDatabase `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $myservername `
      -DatabaseName $mydatabasename | `
    Add-AzureRmSqlDatabaseToFailoverGroup `
      -ResourceGroupName $myresourcegroupname ` `
      -ServerName $myservername `
      -FailoverGroupName $myfailovergroupname
   $myfailovergroup   
   ```

## <a name="install-java-software"></a><span data-ttu-id="b02da-149">Java-software installeren</span><span class="sxs-lookup"><span data-stu-id="b02da-149">Install Java software</span></span>

<span data-ttu-id="b02da-150">Hallo stappen in deze sectie wordt ervan uitgegaan dat u bekend bent met het ontwikkelen van u Java gebruikt en nieuwe tooworking met Azure SQL Database worden.</span><span class="sxs-lookup"><span data-stu-id="b02da-150">hello steps in this section assume that you are familiar with developing using Java and are new tooworking with Azure SQL Database.</span></span> 

### <a name="mac-os"></a><span data-ttu-id="b02da-151">**Mac OS**</span><span class="sxs-lookup"><span data-stu-id="b02da-151">**Mac OS**</span></span>
<span data-ttu-id="b02da-152">Open de terminal en navigeer van tooa directory waar u van plan bent een Java-project te maken.</span><span class="sxs-lookup"><span data-stu-id="b02da-152">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="b02da-153">Installeer **brew** en **Maven** hiertoe Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b02da-153">Install **brew** and **Maven** by entering hello following commands:</span></span> 

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
brew update
brew install maven
```

<span data-ttu-id="b02da-154">Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer **Mac OS**, en volg Hallo gedetailleerde instructies voor het configureren van Java en Maven in stap 1.2 en 1.3.</span><span class="sxs-lookup"><span data-stu-id="b02da-154">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **MacOS**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

### <a name="linux-ubuntu"></a><span data-ttu-id="b02da-155">**Linux (Ubuntu)**</span><span class="sxs-lookup"><span data-stu-id="b02da-155">**Linux (Ubuntu)**</span></span>
<span data-ttu-id="b02da-156">Open de terminal en navigeer van tooa directory waar u van plan bent een Java-project te maken.</span><span class="sxs-lookup"><span data-stu-id="b02da-156">Open your terminal and navigate tooa directory where you plan on creating your Java project.</span></span> <span data-ttu-id="b02da-157">Installeer **Maven** hiertoe Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="b02da-157">Install **Maven** by entering hello following commands:</span></span>

```bash
sudo apt-get install maven
```

<span data-ttu-id="b02da-158">Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer **Ubuntu**, en volg Hallo gedetailleerde instructies voor het configureren van Java en Maven in stap 1.2, 1.3 en 1.4.</span><span class="sxs-lookup"><span data-stu-id="b02da-158">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select **Ubuntu**, and then follow hello detailed instructions for configuring Java and Maven in step 1.2, 1.3, and 1.4.</span></span>

### <a name="windows"></a><span data-ttu-id="b02da-159">**Windows**</span><span class="sxs-lookup"><span data-stu-id="b02da-159">**Windows**</span></span>
<span data-ttu-id="b02da-160">Installeer [Maven](https://maven.apache.org/download.cgi) met Hallo officiële installer.</span><span class="sxs-lookup"><span data-stu-id="b02da-160">Install [Maven](https://maven.apache.org/download.cgi) using hello official installer.</span></span> <span data-ttu-id="b02da-161">Gebruik Maven toohelp afhankelijkheden beheren, bouwen, testen en uw Java-project uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b02da-161">Use Maven toohelp manage dependencies, build, test, and run your Java project.</span></span> <span data-ttu-id="b02da-162">Ga voor gedetailleerde richtlijnen voor het installeren en configureren van Java en Maven omgeving Hallo [bouwen van een app met SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), selecteer **Java**, selecteer Windows en volg Hallo gedetailleerde instructies voor Java en de Maven geconfigureerd in stap 1.2 en 1.3.</span><span class="sxs-lookup"><span data-stu-id="b02da-162">For detailed guidance on installing and configuring Java and Maven environment, go hello [Build an app using SQL Server](https://www.microsoft.com/sql-server/developer-get-started/), select **Java**, select Windows, and then follow hello detailed instructions for configuring Java and Maven in step 1.2 and 1.3.</span></span>

## <a name="create-sqldbsample-project"></a><span data-ttu-id="b02da-163">SqlDbSample-project maken</span><span class="sxs-lookup"><span data-stu-id="b02da-163">Create SqlDbSample project</span></span>

1. <span data-ttu-id="b02da-164">In de opdrachtconsole hello (zoals Bash), een Maven-project te maken.</span><span class="sxs-lookup"><span data-stu-id="b02da-164">In hello command console (such as Bash), create a Maven project.</span></span> 
   ```bash
   mvn archetype:generate "-DgroupId=com.sqldbsamples" "-DartifactId=SqlDbSample" "-DarchetypeArtifactId=maven-archetype-quickstart" "-Dversion=1.0.0"
   ```
2. <span data-ttu-id="b02da-165">Type **Y** en klik op **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b02da-165">Type **Y** and click **Enter**.</span></span>
3. <span data-ttu-id="b02da-166">Wijzig de mappen in het nieuwe project.</span><span class="sxs-lookup"><span data-stu-id="b02da-166">Change directories into your newly created project.</span></span>

   ```bash
   cd SqlDbSamples
   ```

4. <span data-ttu-id="b02da-167">Open uw favoriete editor met Hallo pom.xml-bestand in de projectmap.</span><span class="sxs-lookup"><span data-stu-id="b02da-167">Using your favorite editor, open hello pom.xml file in your project folder.</span></span> 

5. <span data-ttu-id="b02da-168">Hallo Microsoft JDBC-stuurprogramma voor SQL Server-afhankelijkheid tooyour Maven-project via uw favoriete teksteditor toevoegen en kopiëren en plakken Hallo volgende regels in uw pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="b02da-168">Add hello Microsoft JDBC Driver for SQL Server dependency tooyour Maven project by opening your favorite text editor and copying and pasting hello following lines into your pom.xml file.</span></span> <span data-ttu-id="b02da-169">Hallo bestaande waarden vooraf ingevuld in het Hallo-bestand niet overschrijven.</span><span class="sxs-lookup"><span data-stu-id="b02da-169">Do not overwrite hello existing values prepopulated in hello file.</span></span> <span data-ttu-id="b02da-170">Hallo JDBC afhankelijkheid moet binnen Hallo groter 'afhankelijkheden' sectie () worden geplakt.</span><span class="sxs-lookup"><span data-stu-id="b02da-170">hello JDBC dependency must be pasted within hello larger “dependencies” section ( ).</span></span>   

   ```xml
   <dependency>
     <groupId>com.microsoft.sqlserver</groupId>
     <artifactId>mssql-jdbc</artifactId>
    <version>6.1.0.jre8</version>
   </dependency>
   ```

6. <span data-ttu-id="b02da-171">Hallo-versie van Java-project toocompile Hallo tegen door toe te voegen na de sectie 'Eigenschappen' in hello pom.xml-bestand na Hallo 'afhankelijkheden' sectie Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="b02da-171">Specify hello version of Java toocompile hello project against by adding hello following “properties” section into hello pom.xml file after hello "dependencies" section.</span></span> 

   ```xml
   <properties>
     <maven.compiler.source>1.8</maven.compiler.source>
     <maven.compiler.target>1.8</maven.compiler.target>
   </properties>
   ```
7. <span data-ttu-id="b02da-172">Voeg de volgende Hallo 'maken' sectie Hallo pom.xml-bestand na Hallo 'Eigenschappen' sectie toosupport manifestbestanden in potten.</span><span class="sxs-lookup"><span data-stu-id="b02da-172">Add hello following "build" section into hello pom.xml file after hello "properties" section toosupport manifest files in jars.</span></span>       

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.apache.maven.plugins</groupId>
         <artifactId>maven-jar-plugin</artifactId>
         <version>3.0.0</version>
         <configuration>
           <archive>
             <manifest>
               <mainClass>com.sqldbsamples.App</mainClass>
             </manifest>
           </archive>
        </configuration>
       </plugin>
     </plugins>
   </build>
   ```
8. <span data-ttu-id="b02da-173">Opslaan en sluiten Hallo pom.xml-bestand.</span><span class="sxs-lookup"><span data-stu-id="b02da-173">Save and close hello pom.xml file.</span></span>
9. <span data-ttu-id="b02da-174">Open Hallo App.java-bestand (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) en Hallo inhoud vervangen door Hallo inhoud te volgen.</span><span class="sxs-lookup"><span data-stu-id="b02da-174">Open hello App.java file (C:\apache-maven-3.5.0\SqlDbSample\src\main\java\com\sqldbsamples\App.java) and replace hello contents with hello following contents.</span></span> <span data-ttu-id="b02da-175">Hallo failover groepsnaam vervangen door Hallo-naam voor de failover-groep.</span><span class="sxs-lookup"><span data-stu-id="b02da-175">Replace hello failover group name with hello name for your failover group.</span></span> <span data-ttu-id="b02da-176">Als u Hallo waarden voor de databasenaam hello, gebruiker of wachtwoord hebt gewijzigd, moet u deze waarden ook wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b02da-176">If you have changed hello values for hello database name, user, or password, change those values as well.</span></span>

   ```java
   package com.sqldbsamples;

   import java.sql.Connection;
   import java.sql.Statement;
   import java.sql.PreparedStatement;
   import java.sql.ResultSet;
   import java.sql.Timestamp;
   import java.sql.DriverManager;
   import java.util.Date;
   import java.util.concurrent.TimeUnit;

   public class App {

      private static final String FAILOVER_GROUP_NAME = "myfailovergroupname";
  
      private static final String DB_NAME = "mySampleDatabase";
      private static final String USER = "app_user";
      private static final String PASSWORD = "ChangeYourPassword1";

      private static final String READ_WRITE_URL = String.format("jdbc:sqlserver://%s.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);
      private static final String READ_ONLY_URL = String.format("jdbc:sqlserver://%s.secondary.database.windows.net:1433;database=%s;user=%s;password=%s;encrypt=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;", FAILOVER_GROUP_NAME, DB_NAME, USER, PASSWORD);

      public static void main(String[] args) {
         System.out.println("#######################################");
         System.out.println("## GEO DISTRIBUTED DATABASE TUTORIAL ##");
         System.out.println("#######################################");
         System.out.println(""); 

         int highWaterMark = getHighWaterMarkId();

         try {
            for(int i = 1; i < 1000; i++) {
                //  loop will run for about 1 hour
                System.out.print(i + ": insert on primary " + (insertData((highWaterMark + i))?"successful":"failed"));
                TimeUnit.SECONDS.sleep(1);
                System.out.print(", read from secondary " + (selectData((highWaterMark + i))?"successful":"failed") + "\n");
                TimeUnit.SECONDS.sleep(3);
            }
         } catch(Exception e) {
            e.printStackTrace();
      }
   }

   private static boolean insertData(int id) {
      // Insert data into hello product table with a unique product name that we can use toofind hello product again later
      String sql = "INSERT INTO SalesLT.Product (Name, ProductNumber, Color, StandardCost, ListPrice, SellStartDate) VALUES (?,?,?,?,?,?);";

      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         pstmt.setInt(2, 200989 + id + 10000);
         pstmt.setString(3, "Blue");
         pstmt.setDouble(4, 75.00);
         pstmt.setDouble(5, 89.99);
         pstmt.setTimestamp(6, new Timestamp(new Date().getTime()));
         return (1 == pstmt.executeUpdate());
      } catch (Exception e) {
         return false;
      }
   }

   private static boolean selectData(int id) {
      // Query hello data that was previously inserted into hello primary database from hello geo replicated database
      String sql = "SELECT Name, Color, ListPrice FROM SalesLT.Product WHERE Name = ?";

      try (Connection connection = DriverManager.getConnection(READ_ONLY_URL); 
              PreparedStatement pstmt = connection.prepareStatement(sql)) {
         pstmt.setString(1, "BrandNewProduct" + id);
         try (ResultSet resultSet = pstmt.executeQuery()) {
            return resultSet.next();
         }
      } catch (Exception e) {
         return false;
      }
   }

   private static int getHighWaterMarkId() {
      // Query hello high water mark id that is stored in hello table toobe able toomake unique inserts 
      String sql = "SELECT MAX(ProductId) FROM SalesLT.Product";
      int result = 1;
        
      try (Connection connection = DriverManager.getConnection(READ_WRITE_URL); 
              Statement stmt = connection.createStatement();
              ResultSet resultSet = stmt.executeQuery(sql)) {
         if (resultSet.next()) {
             result =  resultSet.getInt(1);
            }
         } catch (Exception e) {
          e.printStackTrace();
         }
         return result;
      }
   }
   ```
6. <span data-ttu-id="b02da-177">Opslaan en sluiten Hallo App.java bestand.</span><span class="sxs-lookup"><span data-stu-id="b02da-177">Save and close hello App.java file.</span></span>

## <a name="compile-and-run-hello-sqldbsample-project"></a><span data-ttu-id="b02da-178">Compileren en Hallo SqlDbSample project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b02da-178">Compile and run hello SqlDbSample project</span></span>

1. <span data-ttu-id="b02da-179">In de opdrachtconsole hello, toofollowing opdracht niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b02da-179">In hello command console, execute toofollowing command.</span></span>

   ```bash
   mvn package
   ```
2. <span data-ttu-id="b02da-180">Als u klaar bent uitvoeren Hallo opdracht toorun Hallo toepassing (deze wordt uitgevoerd voor ongeveer 1 uur tenzij u handmatig stopt) te volgen:</span><span class="sxs-lookup"><span data-stu-id="b02da-180">When finished, execute hello following command toorun hello application (it runs for about 1 hour unless you stop it manually):</span></span>

   ```bash
   mvn -q -e exec:java "-Dexec.mainClass=com.sqldbsamples.App"
   
   #######################################
   ## GEO DISTRIBUTED DATABASE TUTORIAL ##
   #######################################

   1. insert on primary successful, read from secondary successful
   2. insert on primary successful, read from secondary successful
   3. insert on primary successful, read from secondary successful
   ```

## <a name="perform-disaster-recovery-drill"></a><span data-ttu-id="b02da-181">Disaster recovery inzoomen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b02da-181">Perform disaster recovery drill</span></span>

1. <span data-ttu-id="b02da-182">Handmatige failover van de groep failover-aanroep.</span><span class="sxs-lookup"><span data-stu-id="b02da-182">Call manual failover of failover group.</span></span> 

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $mydrservername `
   -FailoverGroupName $myfailovergroupname
   ```

2. <span data-ttu-id="b02da-183">Houd rekening met Hallo resultaten van de toepassing tijdens de failover.</span><span class="sxs-lookup"><span data-stu-id="b02da-183">Observe hello application results during failover.</span></span> <span data-ttu-id="b02da-184">Sommige voegt mislukt tijdens het Hallo DNS-cache wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="b02da-184">Some inserts fail while hello DNS cache refreshes.</span></span>     

3. <span data-ttu-id="b02da-185">Ontdek welke rol u uw herstel na noodgevallen server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b02da-185">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $mydrserver.ReplicationRole
   ```

4. <span data-ttu-id="b02da-186">Failback.</span><span class="sxs-lookup"><span data-stu-id="b02da-186">Failback.</span></span>

   ```powershell
   Switch-AzureRMSqlDatabaseFailoverGroup `
   -ResourceGroupName $myresourcegroupname  `
   -ServerName $myservername `
   -FailoverGroupName $myfailovergroupname
   ```

5. <span data-ttu-id="b02da-187">Hallo resultaten van de toepassing tijdens de failback zien.</span><span class="sxs-lookup"><span data-stu-id="b02da-187">Observe hello application results during failback.</span></span> <span data-ttu-id="b02da-188">Sommige voegt mislukt tijdens het Hallo DNS-cache wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="b02da-188">Some inserts fail while hello DNS cache refreshes.</span></span>     

6. <span data-ttu-id="b02da-189">Ontdek welke rol u uw herstel na noodgevallen server wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b02da-189">Find out which role your disaster recovery server is performing.</span></span>

   ```powershell
   $fileovergroup = Get-AzureRMSqlDatabaseFailoverGroup `
      -FailoverGroupName $myfailovergroupname `
      -ResourceGroupName $myresourcegroupname `
      -ServerName $mydrservername
   $fileovergroup.ReplicationRole
   ```
## <a name="next-steps"></a><span data-ttu-id="b02da-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b02da-190">Next steps</span></span> 

<span data-ttu-id="b02da-191">Zie voor meer informatie [actieve geo-replicatie en failover groepen](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b02da-191">For more information, see [Active geo-replication and failover groups](sql-database-geo-replication-overview.md).</span></span>
