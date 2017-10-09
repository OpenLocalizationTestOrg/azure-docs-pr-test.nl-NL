---
title: aaaGetting gestart met het synchroniseren van Azure SQL-gegevens (Preview) | Microsoft Docs
description: Deze zelfstudie helpt u aan de slag met Azure SQL-gegevenssynchronisatie (Preview).
services: sql-database
documentationcenter: 
author: douglaslms
manager: craigg
editor: 
ms.assetid: a295a768-7ff2-4a86-a253-0090281c8efa
ms.service: sql-database
ms.custom: load & move data
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/08/2017
ms.author: douglasl
ms.openlocfilehash: 666d09237e42acc23ae3c8c81e60734a413f5949
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-sql-data-sync-preview"></a><span data-ttu-id="4a7a6-103">Aan de slag met het synchroniseren van Azure SQL-gegevens (Preview)</span><span class="sxs-lookup"><span data-stu-id="4a7a6-103">Getting Started with Azure SQL Data Sync (Preview)</span></span>
<span data-ttu-id="4a7a6-104">In deze zelfstudie leert u hoe tooset up synchroniseren van Azure SQL-gegevens door te maken van een groep voor synchronisatie met hybride die zowel Azure SQL Database en SQL Server-exemplaren bevat.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-104">In this tutorial, you learn how tooset up Azure SQL Data Sync by creating a hybrid sync group that contains both Azure SQL Database and SQL Server instances.</span></span> <span data-ttu-id="4a7a6-105">nieuwe groep voor synchronisatie Hallo is volledig geconfigureerd en synchroniseert op Hallo schema dat u instelt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-105">hello new sync group is fully configured and synchronizes on hello schedule you set.</span></span>

<span data-ttu-id="4a7a6-106">Deze zelfstudie wordt ervan uitgegaan dat er ten minste enige ervaring met SQL-Database en SQL Server.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-106">This tutorial assumes that you have at least some prior experience with SQL Database and with SQL Server.</span></span> 

<span data-ttu-id="4a7a6-107">Zie voor een overzicht van de SQL-gegevenssynchronisatie [synchroniseren van gegevens](sql-database-sync-data.md).</span><span class="sxs-lookup"><span data-stu-id="4a7a6-107">For an overview of SQL Data Sync, see [Sync data](sql-database-sync-data.md).</span></span>

<span data-ttu-id="4a7a6-108">Voor volledige PowerShell-voorbeelden laten zien hoe tooconfigure synchroniseren van de SQL-gegevens, Hallo artikelen volgende zien:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-108">For complete PowerShell examples that show how tooconfigure SQL Data Sync, see hello following articles:</span></span>
-   [<span data-ttu-id="4a7a6-109">Gebruik PowerShell toosync tussen meerdere Azure SQL-databases</span><span class="sxs-lookup"><span data-stu-id="4a7a6-109">Use PowerShell toosync between multiple Azure SQL databases</span></span>](scripts/sql-database-sync-data-between-sql-databases.md)
-   [<span data-ttu-id="4a7a6-110">Gebruik PowerShell toosync tussen een Azure SQL Database en een lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-110">Use PowerShell toosync between an Azure SQL Database and a SQL Server on-premises database</span></span>](scripts/sql-database-sync-data-between-azure-onprem.md)

> [!NOTE]
> <span data-ttu-id="4a7a6-111">Hallo volledige technische documentatie voor Azure SQL synchroniseren van gegevens, voorheen ondergebracht op MSDN, is beschikbaar als een. PDF-document.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-111">hello complete technical documentation set for Azure SQL Data Sync, formerly located on MSDN, is available as a .PDF document.</span></span> <span data-ttu-id="4a7a6-112">Download deze [hier](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span><span class="sxs-lookup"><span data-stu-id="4a7a6-112">Download it [here](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true).</span></span>

## <a name="step-1---create-sync-group"></a><span data-ttu-id="4a7a6-113">Stap 1: het maken van de groep voor synchronisatie</span><span class="sxs-lookup"><span data-stu-id="4a7a6-113">Step 1 - Create sync group</span></span>

### <a name="locate-hello-data-sync-settings"></a><span data-ttu-id="4a7a6-114">Instellingen voor het synchroniseren van gegevens van Hallo vinden</span><span class="sxs-lookup"><span data-stu-id="4a7a6-114">Locate hello Data Sync settings</span></span>

1.  <span data-ttu-id="4a7a6-115">Navigeer in uw browser toohello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-115">In your browser, navigate toohello Azure portal.</span></span>

2.  <span data-ttu-id="4a7a6-116">Zoek uw SQL-databases van het Dashboard of van Hallo SQL-Databases pictogram op de werkbalk Hallo in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-116">In hello portal, locate your SQL databases from your Dashboard or from hello SQL Databases icon on hello toolbar.</span></span>

    ![Lijst met Azure SQL-databases](media/sql-database-get-started-sql-data-sync/datasync-preview-sqldbs.png)

3.  <span data-ttu-id="4a7a6-118">Op Hallo **SQL-databases** blade, selecteer Hallo bestaande SQL-database die u toouse wilt zoals Hallo hub database voor synchronisatie van gegevens. Hallo SQL databaseblade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-118">On hello **SQL databases** blade, select hello existing SQL database that you want toouse as hello hub database for Data Sync. hello SQL database blade opens.</span></span>

4.  <span data-ttu-id="4a7a6-119">Selecteer op Hallo SQL database-blade voor de geselecteerde database Hallo, **tooother databases synchroniseren**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-119">On hello SQL database blade for hello selected database, select **Sync tooother databases**.</span></span> <span data-ttu-id="4a7a6-120">Hallo gegevenssynchronisatie blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-120">hello Data Sync blade opens.</span></span>

    ![Synchronisatieoptie tooother databases](media/sql-database-get-started-sql-data-sync/datasync-preview-newsyncgroup.png)

### <a name="create-a-new-sync-group"></a><span data-ttu-id="4a7a6-122">Maak een nieuwe groep voor synchronisatie</span><span class="sxs-lookup"><span data-stu-id="4a7a6-122">Create a new Sync Group</span></span>

1.  <span data-ttu-id="4a7a6-123">Selecteer op de blade voor het synchroniseren van gegevens van Hallo **groep voor synchronisatie met nieuwe**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-123">On hello Data Sync blade, select **New Sync Group**.</span></span> <span data-ttu-id="4a7a6-124">Hallo **groep voor synchronisatie met nieuwe** er wordt een blade geopend met stap 1, **groep maken-sync**, gemarkeerde.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-124">hello **New sync group** blade opens with Step 1, **Create sync group**, highlighted.</span></span> <span data-ttu-id="4a7a6-125">Hallo **groep voor synchronisatie maken** blade ook wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-125">hello **Create Data Sync Group** blade also opens.</span></span>

2.  <span data-ttu-id="4a7a6-126">Op Hallo **groep voor synchronisatie maken** blade volgende dingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-126">On hello **Create Data Sync Group** blade, do hello following things:</span></span>

    1.  <span data-ttu-id="4a7a6-127">In Hallo **Sync groepsnaam** en voer een naam voor de nieuwe groep voor synchronisatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-127">In hello **Sync Group Name** field, enter a name for hello new sync group.</span></span>

    2.  <span data-ttu-id="4a7a6-128">In Hallo **metagegevens synchronisatiedatabase** sectie, kiest u of toocreate een nieuwe database (aanbevolen) of toouse een bestaande database.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-128">In hello **Sync Metadata Database** section, choose whether toocreate a new database (recommended) or toouse an existing database.</span></span>

        > [!NOTE]
        > <span data-ttu-id="4a7a6-129">Microsoft raadt aan dat u een nieuwe, lege database toouse zoals Hallo synchronisatiedatabase metagegevens maken.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-129">Microsoft recommends that you create a new, empty database toouse as hello Sync Metadata Database.</span></span> <span data-ttu-id="4a7a6-130">Synchroniseren van gegevens maakt tabellen in deze database en voert een regelmatige werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-130">Data Sync creates tables in this database and runs a frequent workload.</span></span> <span data-ttu-id="4a7a6-131">Deze database wordt automatisch gedeeld als Hallo metagegevens synchronisatiedatabase voor alle van de synchronisatie-groepen in de geselecteerde regio Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-131">This database is automatically shared as hello Sync Metadata Database for all of your Sync groups in hello selected region.</span></span> <span data-ttu-id="4a7a6-132">U kunt Hallo metagegevens-synchronisatiedatabase, de naam of het serviceniveau niet wijzigen zonder slepen en neerzetten.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-132">You can't change hello Sync Metadata Database, its name, or its service level without dropping it.</span></span>

        <span data-ttu-id="4a7a6-133">Als u hebt gekozen **nieuwe database**, selecteer **nieuwe database maken.**</span><span class="sxs-lookup"><span data-stu-id="4a7a6-133">If you chose **New database**, select **Create new database.**</span></span> <span data-ttu-id="4a7a6-134">Hallo **SQL-Database** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-134">hello **SQL Database** blade opens.</span></span> <span data-ttu-id="4a7a6-135">Op Hallo **SQL-Database** blade een naam geven en Hallo nieuwe database te configureren.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-135">On hello **SQL Database** blade, name and configure hello new database.</span></span> <span data-ttu-id="4a7a6-136">Selecteer vervolgens **OK**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-136">Then select **OK**.</span></span>

        <span data-ttu-id="4a7a6-137">Als u hebt gekozen **bestaande database gebruiken**, selecteer Hallo-database van Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-137">If you chose **Use existing database**, select hello database from hello list.</span></span>

    3.  <span data-ttu-id="4a7a6-138">In Hallo **automatische synchronisatie** sectie, selecteert u eerst **op** of **uit**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-138">In hello **Automatic Sync** section, first select **On** or **Off**.</span></span>

        <span data-ttu-id="4a7a6-139">Als u hebt gekozen **op**, in Hallo **Synchronisatiefrequentie** sectie, voer een getal in en selecteert u seconden, minuten, uren of dagen.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-139">If you chose **On**, in hello **Sync Frequency** section, enter a number and select Seconds, Minutes, Hours, or Days.</span></span>

        ![Geef de synchronisatiefrequentie](media/sql-database-get-started-sql-data-sync/datasync-preview-syncfreq.png)

    4.  <span data-ttu-id="4a7a6-141">In Hallo **conflictoplossing** sectie, selecteert u 'Hub wins' of "WINS-lid."</span><span class="sxs-lookup"><span data-stu-id="4a7a6-141">In hello **Conflict Resolution** section, select "Hub wins" or "Member wins."</span></span>

        ![Opgeven hoe conflicten worden opgelost](media/sql-database-get-started-sql-data-sync/datasync-preview-conflictres.png)

    5.  <span data-ttu-id="4a7a6-143">Selecteer **OK** en wachten op Hallo nieuwe synchronisatie groep toobe gemaakt en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-143">Select **OK** and wait for hello new sync group toobe created and deployed.</span></span>

## <a name="step-2---add-sync-members"></a><span data-ttu-id="4a7a6-144">Stap 2: synchronisatie leden toevoegen</span><span class="sxs-lookup"><span data-stu-id="4a7a6-144">Step 2 - Add sync members</span></span>

<span data-ttu-id="4a7a6-145">Nadat de nieuwe groep voor synchronisatie hello wordt gemaakt en geïmplementeerd, stap 2 **sync leden toevoegen**, is gemarkeerd in Hallo **groep voor synchronisatie met nieuwe** blade.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-145">After hello new sync group is created and deployed, Step 2, **Add sync members**, is highlighted in hello **New sync group** blade.</span></span>

<span data-ttu-id="4a7a6-146">In Hallo **Hub Database** sectie, voert u de bestaande referenties Hallo voor Hallo SQL Database-server op welke Hallo hub database zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-146">In hello **Hub Database** section, enter hello existing credentials for hello SQL Database server on which hello hub database is located.</span></span> <span data-ttu-id="4a7a6-147">Voer geen *nieuwe* referenties in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-147">Don't enter *new* credentials in this section.</span></span>

![Hub database is toosync groep toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-hubadded.png)

## <a name="add-an-azure-sql-database"></a><span data-ttu-id="4a7a6-149">Toevoegen van een Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="4a7a6-149">Add an Azure SQL Database</span></span>

<span data-ttu-id="4a7a6-150">In Hallo **Liddatabase** sectie eventueel een groep voor synchronisatie met Azure SQL Database toohello toevoegen door te selecteren **toevoegen van een Azure-Database**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-150">In hello **Member Database** section, optionally add an Azure SQL Database toohello sync group by selecting **Add an Azure Database**.</span></span> <span data-ttu-id="4a7a6-151">Hallo **Azure-Database configureren** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-151">hello **Configure Azure Database** blade opens.</span></span>

<span data-ttu-id="4a7a6-152">Op Hallo **Azure-Database configureren** blade volgende dingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-152">On hello **Configure Azure Database** blade, do hello following things:</span></span>

1.  <span data-ttu-id="4a7a6-153">In Hallo **Sync lidnaam** veld, Geef een naam op voor de nieuwe synchronisatie lid Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-153">In hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="4a7a6-154">Deze naam is niet hetzelfde Hallo-naam van het Hallo-database zelf.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-154">This name is distinct from hello name of hello database itself.</span></span>

2.  <span data-ttu-id="4a7a6-155">In Hallo **abonnement** optie hello Azure-abonnement voor factureringsdoeleinden die is gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-155">In hello **Subscription** field, select hello associated Azure subscription for billing purposes.</span></span>

3.  <span data-ttu-id="4a7a6-156">In Hallo **Azure SQL Server** optie Hallo bestaande SQL-databaseserver.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-156">In hello **Azure SQL Server** field, select hello existing SQL database server.</span></span>

4.  <span data-ttu-id="4a7a6-157">In Hallo **Azure SQL Database** optie Hallo bestaande SQL-database.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-157">In hello **Azure SQL Database** field, select hello existing SQL database.</span></span>

5.  <span data-ttu-id="4a7a6-158">In Hallo **Sync richtingen** bidirectionele Sync, toohello Hub, selecteer of van Hallo Hub.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-158">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

    ![Het toevoegen van een nieuwe SQL-Database sync lid](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadding.png)

6.  <span data-ttu-id="4a7a6-160">In Hallo **gebruikersnaam** en **wachtwoord** velden, Voer Hallo bestaande referenties voor Hallo SQL Database-server op welke Hallo liddatabase zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-160">In hello **Username** and **Password** fields, enter hello existing credentials for hello SQL Database server on which hello member database is located.</span></span> <span data-ttu-id="4a7a6-161">Voer geen *nieuwe* referenties in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-161">Don't enter *new* credentials in this section.</span></span>

7.  <span data-ttu-id="4a7a6-162">Selecteer **OK** en wachten op Hallo nieuwe synchronisatie lid toobe gemaakt en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-162">Select **OK** and wait for hello new sync member toobe created and deployed.</span></span>

    ![Nieuw lid van de SQL-Database-synchronisatie is toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-memberadded.png)

## <a name="add-an-on-premises-sql-server-database"></a><span data-ttu-id="4a7a6-164">Toevoegen van een lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-164">Add an on-premises SQL Server database</span></span>

<span data-ttu-id="4a7a6-165">In Hallo **Liddatabase** sectie eventueel een lokale SQL Server-groep voor synchronisatie van toohello toevoegen door te selecteren **toevoegen van een On-Premises Database**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-165">In hello **Member Database** section, optionally add an on-premises SQL Server toohello sync group by selecting **Add an On-Premises Database**.</span></span> <span data-ttu-id="4a7a6-166">Hallo **configureren On-Premises** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-166">hello **Configure On-Premises** blade opens.</span></span>

<span data-ttu-id="4a7a6-167">Op Hallo **configureren On-Premises** blade volgende dingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-167">On hello **Configure On-Premises** blade, do hello following things:</span></span>

1.  <span data-ttu-id="4a7a6-168">Selecteer **Kies Hallo Sync-Agent Gateway**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-168">Select **Choose hello Sync Agent Gateway**.</span></span> <span data-ttu-id="4a7a6-169">Hallo **Sync-Agent Selecteer** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-169">hello **Select Sync Agent** blade opens.</span></span>

    ![Kies Hallo sync-agent-gateway](media/sql-database-get-started-sql-data-sync/datasync-preview-choosegateway.png)

2.  <span data-ttu-id="4a7a6-171">Op Hallo **Kies Hallo Sync-Agent Gateway** blade kiezen of een bestaande agent toouse of maak een nieuwe agent.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-171">On hello **Choose hello Sync Agent Gateway** blade, choose whether toouse an existing agent or create a new agent.</span></span>

    <span data-ttu-id="4a7a6-172">Als u hebt gekozen **bestaande agents**, selecteer de bestaande agent uit de lijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-172">If you chose **Existing agents**, select hello existing agent from hello list.</span></span>

    <span data-ttu-id="4a7a6-173">Als u hebt gekozen **maken van een nieuwe agent**, volgende dingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-173">If you chose **Create a new agent**, do hello following things:</span></span>

    1.  <span data-ttu-id="4a7a6-174">Synchronisatie Hallo-agent clientsoftware downloaden uit Hallo koppeling en installeer deze op Hallo-computer waarop SQL Server Hallo zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-174">Download hello client sync agent software from hello link provided and install it on hello computer where hello SQL Server is located.</span></span>
 
        > [!IMPORTANT]
        > <span data-ttu-id="4a7a6-175">U hebt tooopen uitgaande TCP-poort 1433 Hallo firewall toolet Hallo client agent communiceren met Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-175">You have tooopen outbound TCP port 1433 in hello firewall toolet hello client agent communicate with hello server.</span></span>


    2.  <span data-ttu-id="4a7a6-176">Voer een naam voor Hallo-agent.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-176">Enter a name for hello agent.</span></span>

    3.  <span data-ttu-id="4a7a6-177">Selecteer **maken en sleutel genereren**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-177">Select **Create and Generate Key**.</span></span>

    4.  <span data-ttu-id="4a7a6-178">Hallo agent sleutel toohello Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-178">Copy hello agent key toohello clipboard.</span></span>
        
        ![Maken van een nieuwe sync-agent](media/sql-database-get-started-sql-data-sync/datasync-preview-selectsyncagent.png)

    5.  <span data-ttu-id="4a7a6-180">Selecteer **OK** tooclose hello **Sync-Agent Selecteer** blade.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-180">Select **OK** tooclose hello **Select Sync Agent** blade.</span></span>

    6.  <span data-ttu-id="4a7a6-181">Zoek en Hallo Sync-Agent voor Client-app uitvoeren op Hallo SQL Server-computer.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-181">On hello SQL Server computer, locate and run hello Client Sync Agent app.</span></span>

        ![Hallo gegevens synchroniseren client agent-app](media/sql-database-get-started-sql-data-sync/datasync-preview-clientagent.png)

    7.  <span data-ttu-id="4a7a6-183">Selecteer in de Hallo sync-agent app **Agentcode indienen**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-183">In hello sync agent app, select **Submit Agent Key**.</span></span> <span data-ttu-id="4a7a6-184">Hallo **synchroniseren metagegevens databaseconfiguratie** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-184">hello **Sync Metadata Database Configuration** dialog box opens.</span></span>

    8.  <span data-ttu-id="4a7a6-185">In Hallo **synchroniseren metagegevens databaseconfiguratie** in het dialoogvenster Plakken in Hallo agent sleutel is gekopieerd uit hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-185">In hello **Sync Metadata Database Configuration** dialog box, paste in hello agent key copied from hello Azure portal.</span></span> <span data-ttu-id="4a7a6-186">Bieden ook Hallo van bestaande referenties voor hello Azure SQL Database-server op welke Hallo metagegevensdatabase zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-186">Also provide hello existing credentials for hello Azure SQL Database server on which hello metadata database is located.</span></span> <span data-ttu-id="4a7a6-187">(Als u een nieuwe metagegevensdatabase gemaakt, wordt deze database is op Hallo dezelfde server als Hallo hub-database.) Selecteer **OK** en wachten op Hallo configuratie toofinish.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-187">(If you created a new metadata database, this database is on hello same server as hello hub database.) Select **OK** and wait for hello configuration toofinish.</span></span>

        ![Hallo agent sleutel- en referenties invoeren](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-enterkey.png)

        >   [!NOTE] 
        >   <span data-ttu-id="4a7a6-189">Als u een Firewallfout op dit moment krijgt, hebt u op toocreate een firewallregel op Azure tooallow inkomend verkeer van Hallo SQL Server-computer.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-189">If you get a firewall error at this point, you have toocreate a firewall rule on Azure tooallow incoming traffic from hello SQL Server computer.</span></span> <span data-ttu-id="4a7a6-190">U kunt Hallo regel maken in Hallo-portal, maar soms is het eenvoudiger toocreate het in SQL Server Management Studio (SSMS).</span><span class="sxs-lookup"><span data-stu-id="4a7a6-190">You can create hello rule manually in hello portal, but you may find it easier toocreate it in SQL Server Management Studio (SSMS).</span></span> <span data-ttu-id="4a7a6-191">Probeer in SSMS, tooconnect toohello hub-database in Azure.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-191">In SSMS, try tooconnect toohello hub database on Azure.</span></span> <span data-ttu-id="4a7a6-192">Voer de naam als \<hub_database_name\>. database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-192">Enter its name as \<hub_database_name\>.database.windows.net.</span></span> <span data-ttu-id="4a7a6-193">Volg de stappen Hallo in Hallo dialoogvenster vak tooconfigure hello Azure firewallregel.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-193">Follow hello steps in hello dialog box tooconfigure hello Azure firewall rule.</span></span> <span data-ttu-id="4a7a6-194">Ga vervolgens terug toohello Sync-Agent voor Client-app.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-194">Then return toohello Client Sync Agent app.</span></span>

    9.  <span data-ttu-id="4a7a6-195">Klik in Hallo Sync-Agent voor Client-app op **registreren** tooregister SQL Server-database met Hallo-agent.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-195">In hello Client Sync Agent app, click **Register** tooregister a SQL Server database with hello agent.</span></span> <span data-ttu-id="4a7a6-196">Hallo **SQL Server-configuratiebestand** dialoogvenster wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-196">hello **SQL Server Configuration** dialog box opens.</span></span>

        ![Toevoegen en configureren van een SQL Server-database](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-adddb.png)

    10. <span data-ttu-id="4a7a6-198">In Hallo **SQL Server-configuratiebestand** dialoogvenster Kies of tooconnect met behulp van SQL Server-verificatie of Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-198">In hello **SQL Server Configuration** dialog box, choose whether tooconnect by using SQL Server authentication or Windows authentication.</span></span> <span data-ttu-id="4a7a6-199">Als u SQL Server-verificatie hebt gekozen, voert u bestaande Hallo-referenties.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-199">If you chose SQL Server authentication, enter hello existing credentials.</span></span> <span data-ttu-id="4a7a6-200">Geef Hallo SQL Server-naam en Hallo-naam van Hallo-database die u toosync wilt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-200">Provide hello SQL Server name and hello name of hello database that you want toosync.</span></span> <span data-ttu-id="4a7a6-201">Selecteer **verbinding testen** tootest uw instellingen.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-201">Select **Test connection** tootest your settings.</span></span> <span data-ttu-id="4a7a6-202">Selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-202">Then select **Save**.</span></span> <span data-ttu-id="4a7a6-203">Hallo geregistreerde database weergegeven in de lijst Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-203">hello registered database appears in hello list.</span></span>

        ![SQL Server-database is nu geregistreerd.](media/sql-database-get-started-sql-data-sync/datasync-preview-agent-dbadded.png)

    11. <span data-ttu-id="4a7a6-205">U kunt nu Hallo Sync-Agent voor Client-app sluiten.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-205">You can now close hello Client Sync Agent app.</span></span>

    12. <span data-ttu-id="4a7a6-206">In de portal Hallo op Hallo **configureren On-Premises** blade Selecteer **Selecteer Hallo Database.**</span><span class="sxs-lookup"><span data-stu-id="4a7a6-206">In hello portal, on hello **Configure On-Premises** blade, select **Select hello Database.**</span></span> <span data-ttu-id="4a7a6-207">Hallo **Database selecteren** blade wordt geopend.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-207">hello **Select Database** blade opens.</span></span>

    13. <span data-ttu-id="4a7a6-208">Op Hallo **Database selecteren** blade in Hallo **Sync lidnaam** veld, Geef een naam op voor de nieuwe synchronisatie lid Hallo.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-208">On hello **Select Database** blade, in hello **Sync Member Name** field, provide a name for hello new sync member.</span></span> <span data-ttu-id="4a7a6-209">Deze naam is niet hetzelfde Hallo-naam van het Hallo-database zelf.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-209">This name is distinct from hello name of hello database itself.</span></span> <span data-ttu-id="4a7a6-210">Hallo-database selecteren op Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-210">Select hello database from hello list.</span></span> <span data-ttu-id="4a7a6-211">In Hallo **Sync richtingen** bidirectionele Sync, toohello Hub, selecteer of van Hallo Hub.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-211">In hello **Sync Directions** field, select Bi-directional Sync, toohello Hub, or From hello Hub.</span></span>

        ![Selecteer Hallo op de lokale database.](media/sql-database-get-started-sql-data-sync/datasync-preview-selectdb.png)

    14. <span data-ttu-id="4a7a6-213">Selecteer **OK** tooclose hello **Database selecteren** blade.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-213">Select **OK** tooclose hello **Select Database** blade.</span></span> <span data-ttu-id="4a7a6-214">Selecteer vervolgens **OK** tooclose hello **configureren On-Premises** blade en wacht Hallo nieuwe synchroniseren lid toobe gemaakt en geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-214">Then select **OK** tooclose hello **Configure On-Premises** blade and wait for hello new sync member toobe created and deployed.</span></span> <span data-ttu-id="4a7a6-215">Tot slot op **OK** tooclose hello **sync leden selecteren** blade.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-215">Finally, click **OK** tooclose hello **Select sync members** blade.</span></span>

        ![Op de lokale database toosync groep toegevoegd](media/sql-database-get-started-sql-data-sync/datasync-preview-onpremadded.png)

3.  <span data-ttu-id="4a7a6-217">tooconnect tooSQL synchroniseren van gegevens en lokale Hallo-agent, de gebruikersrol van de naam-toohello toevoegen `DataSync_Executor`.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-217">tooconnect tooSQL Data Sync and hello local agent, add your user name toohello role `DataSync_Executor`.</span></span> <span data-ttu-id="4a7a6-218">Synchroniseren van gegevens wordt deze rol op Hallo SQL Server-exemplaar gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-218">Data Sync creates this role on hello SQL Server instance.</span></span>

## <a name="step-3---configure-sync-group"></a><span data-ttu-id="4a7a6-219">Stap 3 - groep voor synchronisatie configureren</span><span class="sxs-lookup"><span data-stu-id="4a7a6-219">Step 3 - Configure sync group</span></span>

<span data-ttu-id="4a7a6-220">Nadat de nieuwe synchronisatie Hallo-groepsleden worden gemaakt en geïmplementeerd, stap 3 **groep voor synchronisatie configureren**, is gemarkeerd in Hallo **groep voor synchronisatie met nieuwe** blade.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-220">After hello new sync group members are created and deployed, Step 3, **Configure sync group**, is highlighted in hello **New sync group** blade.</span></span>

1.  <span data-ttu-id="4a7a6-221">Op Hallo **tabellen** blade, selecteer een database uit de lijst Hallo van synchronisatie leden en selecteer vervolgens **schema vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-221">On hello **Tables** blade, select a database from hello list of sync group members, and then select **Refresh schema**.</span></span>

2.  <span data-ttu-id="4a7a6-222">Selecteer in de Hallo lijst met beschikbare tabellen, Hallo tabellen die u toosync wilt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-222">From hello list of available tables, select hello tables that you want toosync.</span></span>

    ![Selecteer tabellen toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables.png)

3.  <span data-ttu-id="4a7a6-224">Standaard worden alle kolommen in tabel Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-224">By default, all columns in hello table are selected.</span></span> <span data-ttu-id="4a7a6-225">Als u niet toosync wilt Hallo alle kolommen, uitschakelen Hallo selectievakje voor dat u niet dat toosync wilt Hallo-kolommen.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-225">If you don't want toosync all hello columns, disable hello checkbox for hello columns that you don't want toosync.</span></span> <span data-ttu-id="4a7a6-226">Zorg ervoor dat tooleave Hallo primaire-sleutelkolom geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-226">Be sure tooleave hello primary key column selected.</span></span>

    ![Velden selecteren toosync](media/sql-database-get-started-sql-data-sync/datasync-preview-tables2.png)

4.  <span data-ttu-id="4a7a6-228">Tot slot selecteert **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-228">Finally, select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4a7a6-229">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4a7a6-229">Next steps</span></span>
<span data-ttu-id="4a7a6-230">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-230">Congratulations.</span></span> <span data-ttu-id="4a7a6-231">U kunt een groep voor synchronisatie met zowel een exemplaar van SQL-Database en SQL Server-database hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4a7a6-231">You have created a sync group that includes both a SQL Database instance and a SQL Server database.</span></span>

<span data-ttu-id="4a7a6-232">Zie voor meer informatie over SQL-Database en synchroniseren van de SQL-gegevens:</span><span class="sxs-lookup"><span data-stu-id="4a7a6-232">For more info about SQL Database and SQL Data Sync, see:</span></span>

-   [<span data-ttu-id="4a7a6-233">Hallo volledige gegevenssynchronisatie SQL technische documentatie downloaden</span><span class="sxs-lookup"><span data-stu-id="4a7a6-233">Download hello complete SQL Data Sync technical documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_full_documentation.pdf?raw=true)
-   [<span data-ttu-id="4a7a6-234">Hallo SQL gegevens synchroniseren REST-API-documentatie downloaden</span><span class="sxs-lookup"><span data-stu-id="4a7a6-234">Download hello SQL Data Sync REST API documentation</span></span>](https://github.com/Microsoft/sql-server-samples/raw/master/samples/features/sql-data-sync/Data_Sync_Preview_REST_API.pdf?raw=true)
-   [<span data-ttu-id="4a7a6-235">Overzicht van de SQL-Database</span><span class="sxs-lookup"><span data-stu-id="4a7a6-235">SQL Database Overview</span></span>](sql-database-technical-overview.md)
-   [<span data-ttu-id="4a7a6-236">Database-levenscyclusbeheer</span><span class="sxs-lookup"><span data-stu-id="4a7a6-236">Database Lifecycle Management</span></span>](https://msdn.microsoft.com/library/jj907294.aspx)
