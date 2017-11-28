---
title: "aaaRestore één tabel vanuit back-up van Azure SQL Database | Microsoft Docs"
description: "Meer informatie over hoe toorestore één tabel vanuit Azure SQL Database back-up."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: 340b41bd-9df8-47fb-adfc-03216de38a5e
ms.service: sql-database
ms.custom: business continuity
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: 696d2ac87a70bccdf063bfecb8255723404aa5bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorestore-a-single-table-from-an-azure-sql-database-backup"></a><span data-ttu-id="c376b-103">Hoe toorestore één tabel uit een back-up van Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c376b-103">How toorestore a single table from an Azure SQL Database backup</span></span>
<span data-ttu-id="c376b-104">Een situatie waarin u sommige gegevens in een SQL-database per ongeluk hebt gewijzigd kunnen optreden en nu het gewenste toorecover Hallo één betrokken tabel.</span><span class="sxs-lookup"><span data-stu-id="c376b-104">You may encounter a situation in which you accidentally modified some data in a SQL database and now you want toorecover hello single affected table.</span></span> <span data-ttu-id="c376b-105">Dit artikel wordt beschreven hoe toorestore één tabel in een database van een SQL-Database Hallo [automatische back-ups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="c376b-105">This article describes how toorestore a single table in a database from one of hello SQL Database [automatic backups](sql-database-automated-backups.md).</span></span>

## <a name="preparation-steps-rename-hello-table-and-restore-a-copy-of-hello-database"></a><span data-ttu-id="c376b-106">Voorbereidende stappen: naam van de tabel Hallo en herstelt een kopie van het Hallo-database</span><span class="sxs-lookup"><span data-stu-id="c376b-106">Preparation steps: Rename hello table and restore a copy of hello database</span></span>
1. <span data-ttu-id="c376b-107">Hallo-tabel in uw Azure SQL-database die u wilt dat tooreplace Hallo hersteld exemplaar identificeren.</span><span class="sxs-lookup"><span data-stu-id="c376b-107">Identify hello table in your Azure SQL database that you want tooreplace with hello restored copy.</span></span> <span data-ttu-id="c376b-108">Microsoft SQL Management Studio toorename Hallo tabel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c376b-108">Use Microsoft SQL Management Studio toorename hello table.</span></span> <span data-ttu-id="c376b-109">Wijzig bijvoorbeeld Hallo tabel als &lt;tabelnaam&gt;_old.</span><span class="sxs-lookup"><span data-stu-id="c376b-109">For example, rename hello table as &lt;table name&gt;_old.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c376b-110">tooavoid wordt geblokkeerd, zorg ervoor dat er geen activiteit uitgevoerd op Hallo-tabel die u de naam wijzigt.</span><span class="sxs-lookup"><span data-stu-id="c376b-110">tooavoid being blocked, make sure that there's no activity running on hello table that you are renaming.</span></span> <span data-ttu-id="c376b-111">Als u problemen ondervindt, ervoor zorgen dat deze procedure uitvoeren tijdens een onderhoudsvenster.</span><span class="sxs-lookup"><span data-stu-id="c376b-111">If you encounter issues, make sure that perform this procedure during a maintenance window.</span></span>
   >

2. <span data-ttu-id="c376b-112">Herstellen van een back-up van uw database tooa punt in tijd dat u toorecover toousing hello wilt [Point-In_Time herstellen](sql-database-recovery-using-backups.md#point-in-time-restore) stappen.</span><span class="sxs-lookup"><span data-stu-id="c376b-112">Restore a backup of your database tooa point in time that you want toorecover toousing hello [Point-In_Time Restore](sql-database-recovery-using-backups.md#point-in-time-restore) steps.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c376b-113">Hallo-naam van de database hersteld Hallo is in Hallo DBName + tijdstempelnotatie; bijvoorbeeld: **Adventureworks2012_2016 01-01T22 12Z**.</span><span class="sxs-lookup"><span data-stu-id="c376b-113">hello name of hello restored database will be in hello DBName+TimeStamp format; for example, **Adventureworks2012_2016-01-01T22-12Z**.</span></span> <span data-ttu-id="c376b-114">Deze stap overschreven niet Hallo bestaande databasenaam op Hallo server.</span><span class="sxs-lookup"><span data-stu-id="c376b-114">This step doesn't overwrite hello existing database name on hello server.</span></span> <span data-ttu-id="c376b-115">Dit is een veiligheidsmaatregel, en het bedoeld tooallow u tooverify Hallo database teruggezet voordat ze hun huidige database verwijderen en wijzig de naam van de database hersteld Hallo voor gebruik in productieomgevingen.</span><span class="sxs-lookup"><span data-stu-id="c376b-115">This is a safety measure, and it's intended tooallow you tooverify hello restored database before they drop their current database and rename hello restored database for production use.</span></span>
   
## <a name="copying-hello-table-from-hello-restored-database-by-using-hello-sql-database-migration-tool"></a><span data-ttu-id="c376b-116">Kopiëren Hallo tabel uit Hallo database teruggezet met behulp van Hallo-hulpprogramma voor migratie van de SQL-Database</span><span class="sxs-lookup"><span data-stu-id="c376b-116">Copying hello table from hello restored database by using hello SQL Database Migration tool</span></span>

1. <span data-ttu-id="c376b-117">Download en installeer Hallo [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span><span class="sxs-lookup"><span data-stu-id="c376b-117">Download and install hello [SQL Database Migration Wizard](https://sqlazuremw.codeplex.com).</span></span>
2. <span data-ttu-id="c376b-118">Open Hallo SQL Database Migration Wizard op Hallo **Selecteer proces** pagina **Database onder analyseren/migreren**, en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c376b-118">Open hello SQL Database Migration Wizard, on hello **Select Process** page, select **Database under Analyze/Migrate**, and then click **Next**.</span></span>

   ![Migratie van de SQL-Database-wizard - proces selecteren](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/1.png)

3. <span data-ttu-id="c376b-120">In Hallo **tooServer verbinding** dialoogvenster vak, Hallo instellingen volgende van toepassing:</span><span class="sxs-lookup"><span data-stu-id="c376b-120">In hello **Connect tooServer** dialog box, apply hello following settings:</span></span>

   * <span data-ttu-id="c376b-121">Servernaam: **uw SQL server**</span><span class="sxs-lookup"><span data-stu-id="c376b-121">Server name: **Your SQL server**</span></span>
   * <span data-ttu-id="c376b-122">Verificatie: **SQL Server-verificatie**</span><span class="sxs-lookup"><span data-stu-id="c376b-122">Authentication: **SQL Server Authentication**</span></span>
   * <span data-ttu-id="c376b-123">Aanmelding: **uw aanmelding**</span><span class="sxs-lookup"><span data-stu-id="c376b-123">Login: **Your login**</span></span>
   * <span data-ttu-id="c376b-124">Wachtwoord: **uw wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="c376b-124">Password: **Your password**</span></span>
   * <span data-ttu-id="c376b-125">Database: **Master DB (alle databases vermelden)**</span><span class="sxs-lookup"><span data-stu-id="c376b-125">Database: **Master DB (List all databases)**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="c376b-126">Standaard slaat de wizard Hallo uw aanmeldingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="c376b-126">By default hello wizard saves your login information.</span></span> <span data-ttu-id="c376b-127">Als u niet wilt dat deze is, selecteert u **aanmeldingsgegevens vergeet**.</span><span class="sxs-lookup"><span data-stu-id="c376b-127">If you don't want it to, select **Forget Login Information**.</span></span>
   >
   
     ![Migratie van de SQL-Database-wizard - bron selecteren - stap 1](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/2.png)
4. <span data-ttu-id="c376b-129">In Hallo **bron selecteren** dialoogvenster, selecteer Hallo hersteld databasenaam van Hallo **voorbereidingsstappen** sectie als de bron en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c376b-129">In hello **Select Source** dialog box, select hello restored database name from hello **Preparation steps** section as your source, and then click **Next**.</span></span>
   
    ![Migratie van de SQL-Database-wizard - bron selecteren - stap 2](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/3.png)
5. <span data-ttu-id="c376b-131">In Hallo **objecten kiezen** dialoogvenster, selecteer Hallo **specifieke databaseobjecten selecteren** optie en selecteer vervolgens Hallo table(or tables) gewenste toomigrate toohello-doelserver.</span><span class="sxs-lookup"><span data-stu-id="c376b-131">In hello **Choose Objects** dialog box, select hello **Select specific database objects** option, and then select hello table(or tables) that you want toomigrate toohello target server.</span></span>
   <span data-ttu-id="c376b-132">![Migratie van de SQL-Database-wizard - objecten kiezen](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span><span class="sxs-lookup"><span data-stu-id="c376b-132">![SQL Database Migration wizard - Choose Objects](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/4.png)</span></span>
6. <span data-ttu-id="c376b-133">Op Hallo **overzicht van de Wizard Script** pagina, klikt u op **Ja** wanneer u wordt gevraagd over u klaar toogenerate een SQL-script bent.</span><span class="sxs-lookup"><span data-stu-id="c376b-133">On hello **Script Wizard Summary** page, click **Yes** when you’re prompted about whether you’re ready toogenerate a SQL script.</span></span> <span data-ttu-id="c376b-134">U hebt ook Hallo optie toosave Hallo TSQL-Script voor later gebruik.</span><span class="sxs-lookup"><span data-stu-id="c376b-134">You also have hello option toosave hello TSQL Script for later use.</span></span>
   <span data-ttu-id="c376b-135">![Migratie van de SQL-Database-wizard - samenvatting van de Wizard Script](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span><span class="sxs-lookup"><span data-stu-id="c376b-135">![SQL Database Migration wizard - Script Wizard Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/5.png)</span></span>
7. <span data-ttu-id="c376b-136">Op Hallo **samenvatting van de resultaten** pagina, klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c376b-136">On hello **Results Summary** page, click **Next**.</span></span>
   <span data-ttu-id="c376b-137">![Migratie van de SQL-Database-wizard - overzicht](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span><span class="sxs-lookup"><span data-stu-id="c376b-137">![SQL Database Migration wizard - Results Summary](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/6.png)</span></span>
8. <span data-ttu-id="c376b-138">Op Hallo **Target Server-verbinding instellen** pagina, klikt u op **tooServer verbinding**, en voer vervolgens Hallo details:</span><span class="sxs-lookup"><span data-stu-id="c376b-138">On hello **Setup Target Server Connection** page, click **Connect tooServer**, and then enter hello details as follows:</span></span>
   
   * <span data-ttu-id="c376b-139">**Servernaam**: Target server-exemplaar</span><span class="sxs-lookup"><span data-stu-id="c376b-139">**Server Name**: Target server instance</span></span>
   * <span data-ttu-id="c376b-140">**Verificatie**: **SQL Server-verificatie**.</span><span class="sxs-lookup"><span data-stu-id="c376b-140">**Authentication**: **SQL Server authentication**.</span></span> <span data-ttu-id="c376b-141">Voer uw aanmeldingsreferenties.</span><span class="sxs-lookup"><span data-stu-id="c376b-141">Enter your login credentials.</span></span>
   * <span data-ttu-id="c376b-142">**Database**: **Master DB (alle databases vermelden)**.</span><span class="sxs-lookup"><span data-stu-id="c376b-142">**Database**: **Master DB (List all databases)**.</span></span> <span data-ttu-id="c376b-143">Deze optie geeft een lijst van alle Hallo-databases op Hallo-doelserver.</span><span class="sxs-lookup"><span data-stu-id="c376b-143">This option lists all hello databases on hello target server.</span></span>
     
     ![Migratie van de SQL-Database-wizard - doel Server-verbinding instellen](./media/sql-database-cloud-migrate-restore-single-table-azure-backup/7.png)
9. <span data-ttu-id="c376b-145">Klik op **Connect**, selecteer Hallo doeldatabase die u wilt toomove Hallo tabel en klik vervolgens op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c376b-145">Click **Connect**, select hello target database that you want toomove hello table to, and then click **Next**.</span></span> <span data-ttu-id="c376b-146">Dit moet voltooien Hallo eerder gegenereerde script wordt uitgevoerd en ziet u Hallo zojuist gekopieerde toohello-doeldatabase tabel verplaatst.</span><span class="sxs-lookup"><span data-stu-id="c376b-146">This should finish running hello previously generated script, and you should see hello newly moved table copied toohello target database.</span></span>

## <a name="verification-step"></a><span data-ttu-id="c376b-147">Verificatiestap</span><span class="sxs-lookup"><span data-stu-id="c376b-147">Verification step</span></span>

- <span data-ttu-id="c376b-148">Query's en test Hallo gekopieerd zojuist tabel toomake Hallo gegevens is beschadigd.</span><span class="sxs-lookup"><span data-stu-id="c376b-148">Query and test hello newly copied table toomake sure that hello data is intact.</span></span> <span data-ttu-id="c376b-149">Na bevestiging verwijderen Hallo hernoemd formulier **voorbereidende stappen** sectie.</span><span class="sxs-lookup"><span data-stu-id="c376b-149">Upon confirmation, you can drop hello renamed table form **Preparation steps** section.</span></span> <span data-ttu-id="c376b-150">(bijvoorbeeld &lt;tabelnaam&gt;_old).</span><span class="sxs-lookup"><span data-stu-id="c376b-150">(for example, &lt;table name&gt;_old).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c376b-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c376b-151">Next steps</span></span>
[<span data-ttu-id="c376b-152">Automatische back-ups van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="c376b-152">SQL Database automatic backups</span></span>](sql-database-automated-backups.md)

