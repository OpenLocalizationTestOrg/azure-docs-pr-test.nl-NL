---
title: Azure Backup voor SQL Server-werkbelastingen met Azure Backup-Server | Microsoft Docs
description: Een inleiding tot de back-ups van SQL Server-databases via Azure Backup-Server
services: backup
documentationcenter: 
author: pvrk
manager: Shivamg
editor: 
ms.assetid: c8b1f7ec-26b1-4ef0-a3f2-91aec959daea
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: pullabhk
ms.openlocfilehash: 2af9ebaa8f52690ed63406cbd85b77544d2d900d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="back-up-sql-server-to-azure-with-azure-backup-server"></a><span data-ttu-id="0531d-103">Back-up van SQL Server naar Azure met Azure Backup-Server</span><span class="sxs-lookup"><span data-stu-id="0531d-103">Back up SQL Server to Azure With Azure Backup Server</span></span>
<span data-ttu-id="0531d-104">In dit artikel begeleidt u bij de configuratiestappen voor back-up van SQL Server-databases via Microsoft Azure Backup-Server (MABS).</span><span class="sxs-lookup"><span data-stu-id="0531d-104">This article leads you through the configuration steps for backup of SQL Server databases using Microsoft Azure Backup Server (MABS).</span></span>

<span data-ttu-id="0531d-105">Het beheer van SQL Server-database back-up naar Azure en herstel van Azure omvat drie stappen:</span><span class="sxs-lookup"><span data-stu-id="0531d-105">The management of SQL Server database backup to Azure and recovery from Azure involves three steps:</span></span>

1. <span data-ttu-id="0531d-106">Maak een back-upbeleid ter bescherming van SQL Server-databases naar Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-106">Create a backup policy to protect SQL Server databases to Azure.</span></span>
2. <span data-ttu-id="0531d-107">Maken van back-ups op aanvraag naar Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-107">Create on-demand backup copies to Azure.</span></span>
3. <span data-ttu-id="0531d-108">Herstel de database uit Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-108">Recover the database from Azure.</span></span>

## <a name="before-you-start"></a><span data-ttu-id="0531d-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="0531d-109">Before you start</span></span>
<span data-ttu-id="0531d-110">Voordat u begint, zorg ervoor dat er [geïnstalleerd en de Azure Backup-Server voorbereid](backup-azure-microsoft-azure-backup.md).</span><span class="sxs-lookup"><span data-stu-id="0531d-110">Before you begin, ensure that you have [installed and prepared the Azure Backup Server](backup-azure-microsoft-azure-backup.md).</span></span>

## <a name="create-a-backup-policy-to-protect-sql-server-databases-to-azure"></a><span data-ttu-id="0531d-111">Maak een back-upbeleid ter bescherming van SQL Server-databases naar Azure</span><span class="sxs-lookup"><span data-stu-id="0531d-111">Create a backup policy to protect SQL Server databases to Azure</span></span>
1. <span data-ttu-id="0531d-112">Klik op de Azure Backup-Server-gebruikersinterface op de **beveiliging** werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0531d-112">On the Azure Backup Server UI, click the **Protection** workspace.</span></span>
2. <span data-ttu-id="0531d-113">Klik op het lint op **nieuw** een nieuwe beveiligingsgroep maken.</span><span class="sxs-lookup"><span data-stu-id="0531d-113">On the tool ribbon, click **New** to create a new protection group.</span></span>

    ![Beveiligingsgroep maken](./media/backup-azure-backup-sql/protection-group.png)
3. <span data-ttu-id="0531d-115">MABS toont het startscherm met de richtlijnen over het maken van een **beveiligingsgroep**.</span><span class="sxs-lookup"><span data-stu-id="0531d-115">MABS shows the start screen with the guidance on creating a **Protection Group**.</span></span> <span data-ttu-id="0531d-116">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-116">Click **Next**.</span></span>
4. <span data-ttu-id="0531d-117">Selecteer **Servers**.</span><span class="sxs-lookup"><span data-stu-id="0531d-117">Select **Servers**.</span></span>

    ![Type beveiligingsgroep - 'Servers' selecteren](./media/backup-azure-backup-sql/pg-servers.png)
5. <span data-ttu-id="0531d-119">Vouw de SQL Server-computer waar de databases naar een back-up aanwezig zijn.</span><span class="sxs-lookup"><span data-stu-id="0531d-119">Expand the SQL Server machine where the databases to be backed up are present.</span></span> <span data-ttu-id="0531d-120">MABS bevat verschillende gegevensbronnen die u kunnen een back-up van die server.</span><span class="sxs-lookup"><span data-stu-id="0531d-120">MABS shows various data sources that can be backed up from that server.</span></span> <span data-ttu-id="0531d-121">Vouw de **alle SQL-Shares** en selecteer de databases (in dit geval wordt geselecteerd ReportServer$ MSDPM2012 en ReportServer$ MSDPM2012TempDB) naar het back-up worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0531d-121">Expand the **All SQL Shares** and select the databases (in this case we selected ReportServer$MSDPM2012 and ReportServer$MSDPM2012TempDB) to be backed up.</span></span> <span data-ttu-id="0531d-122">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-122">Click **Next**.</span></span>

    ![SQL-database selecteren](./media/backup-azure-backup-sql/pg-databases.png)
6. <span data-ttu-id="0531d-124">Geef een naam voor de beveiligingsgroep en selecteer de **ik wil online beveiliging** selectievakje.</span><span class="sxs-lookup"><span data-stu-id="0531d-124">Provide a name for the protection group and select the **I want online Protection** checkbox.</span></span>

    ![Methode voor gegevensbeveiliging - kortetermijnbeveiliging op schijf en Online Azure](./media/backup-azure-backup-sql/pg-name.png)
7. <span data-ttu-id="0531d-126">In de **Kortetermijndoelen opgeven** scherm, bevatten de benodigde invoeren voor het maken van back-uppunten op schijf.</span><span class="sxs-lookup"><span data-stu-id="0531d-126">In the **Specify Short-Term Goals** screen, include the necessary inputs to create backup points to disk.</span></span>

    <span data-ttu-id="0531d-127">Hier ziet u dat **bewaartermijn** is ingesteld op *5 dagen*, **Synchronisatiefrequentie** is ingesteld op één keer elke *15 minuten* dit is de de frequentie waarmee back-up is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0531d-127">Here we see that **Retention range** is set to *5 days*, **Synchronization frequency** is set to once every *15 minutes* which is the frequency at which backup is taken.</span></span> <span data-ttu-id="0531d-128">**Snelle volledige back-up** is ingesteld op *20:00 uur*.</span><span class="sxs-lookup"><span data-stu-id="0531d-128">**Express Full Backup** is set to *8:00 P.M*.</span></span>

    ![Doelen voor de korte termijn](./media/backup-azure-backup-sql/pg-shortterm.png)

   > [!NOTE]
   > <span data-ttu-id="0531d-130">Op 20:00 uur (op basis van de invoer scherm) wordt een back-uppunt elke dag gemaakt door het overdragen van de gegevens die zijn gewijzigd van back-uppunt van de vorige dag 20:00 uur.</span><span class="sxs-lookup"><span data-stu-id="0531d-130">At 8:00 PM (according to the screen input) a backup point is created every day by transferring the data that has been modified from the previous day’s 8:00 PM backup point.</span></span> <span data-ttu-id="0531d-131">Dit proces wordt genoemd **snelle volledige back-up**.</span><span class="sxs-lookup"><span data-stu-id="0531d-131">This process is called **Express Full Backup**.</span></span> <span data-ttu-id="0531d-132">Tijdens de transactie logboeken worden gesynchroniseerd snelle om de 15 minuten, als er nodig is 21:00 uur: de database herstellen en vervolgens een is gemaakt door de logboeken van de laatste volledige back-up punt (8 pm in dit geval).</span><span class="sxs-lookup"><span data-stu-id="0531d-132">While the transaction logs are synchronized every 15 minutes, if there is a need to recover the database at 9:00 PM – then the point is created by replaying the logs from the last express full backup point (8pm in this case).</span></span>
   >
   >

8. <span data-ttu-id="0531d-133">Klik op **Volgende**</span><span class="sxs-lookup"><span data-stu-id="0531d-133">Click **Next**</span></span>

    <span data-ttu-id="0531d-134">MABS ziet u de totale opslagruimte beschikbaar is en de mogelijke schijfgebruik voor ruimte.</span><span class="sxs-lookup"><span data-stu-id="0531d-134">MABS shows the overall storage space available and the potential disk space utilization.</span></span>

    ![Toegewezen schijfruimte](./media/backup-azure-backup-sql/pg-storage.png)

    <span data-ttu-id="0531d-136">MABS wordt standaard één volume per gegevensbron (SQL Server-database) dat wordt gebruikt voor de eerste back-up gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0531d-136">By default, MABS creates one volume per data source (SQL Server database) which is used for the initial backup copy.</span></span> <span data-ttu-id="0531d-137">Met deze benadering beperkt de Logical Disk Manager (LDM) MABS beveiliging met 300 gegevensbronnen (SQL Server-databases).</span><span class="sxs-lookup"><span data-stu-id="0531d-137">Using this approach, the Logical Disk Manager (LDM) limits MABS protection to 300 data sources (SQL Server databases).</span></span> <span data-ttu-id="0531d-138">U kunt deze beperking omzeilen, selecteer de **dezelfde gegevens in de DPM-opslaggroep plaatsen**, optie.</span><span class="sxs-lookup"><span data-stu-id="0531d-138">To work around this limitation, select the **Co-locate data in DPM Storage Pool**, option.</span></span> <span data-ttu-id="0531d-139">Als u deze optie gebruikt, MABS maakt gebruik van één volume voor meerdere gegevensbronnen, waardoor MABS maximaal 2000 SQL-databases beveiligen.</span><span class="sxs-lookup"><span data-stu-id="0531d-139">If you use this option, MABS uses a single volume for multiple data sources, which allows MABS to protect up to 2000 SQL databases.</span></span>

    <span data-ttu-id="0531d-140">Als **volumes automatisch vergroten** optie is geselecteerd, MABS kunt account voor het toegenomen back-volume wanneer de productiegegevens groeit.</span><span class="sxs-lookup"><span data-stu-id="0531d-140">If **Automatically grow the volumes** option is selected, MABS can account for the increased backup volume as the production data grows.</span></span> <span data-ttu-id="0531d-141">Als **volumes automatisch vergroten** optie niet is geselecteerd, MABS beperkt de back-upopslag gebruikt voor de gegevensbronnen in de beveiligingsgroep.</span><span class="sxs-lookup"><span data-stu-id="0531d-141">If **Automatically grow the volumes** option is not selected, MABS limits the backup storage used to the data sources in the protection group.</span></span>
9. <span data-ttu-id="0531d-142">Beheerders de keuze van het overdragen van deze eerste back-up handmatig (uit netwerk) om overbelasting van de bandbreedte te voorkomen of via het netwerk krijgt.</span><span class="sxs-lookup"><span data-stu-id="0531d-142">Administrators are given the choice of transferring this initial backup manually (off network) to avoid bandwidth congestion or over the network.</span></span> <span data-ttu-id="0531d-143">Ze kunnen ook de tijd waarop de eerste overdracht kan zich voordoen configureren.</span><span class="sxs-lookup"><span data-stu-id="0531d-143">They can also configure the time at which the initial transfer can happen.</span></span> <span data-ttu-id="0531d-144">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-144">Click **Next**.</span></span>

    ![Methode voor eerste replicatie](./media/backup-azure-backup-sql/pg-manual.png)

    <span data-ttu-id="0531d-146">De eerste back-up is vereist voor overdracht van de gehele gegevensbron (SQL Server-database) van productieserver (SQL Server-machine) naar MABS.</span><span class="sxs-lookup"><span data-stu-id="0531d-146">The initial backup copy requires transfer of the entire data source (SQL Server database) from production server (SQL Server machine) to MABS.</span></span> <span data-ttu-id="0531d-147">Deze gegevens mogelijk te groot worden en de gegevens worden overgedragen via het netwerk kan groter zijn dan bandbreedte.</span><span class="sxs-lookup"><span data-stu-id="0531d-147">This data might be large, and transferring the data over the network could exceed bandwidth.</span></span> <span data-ttu-id="0531d-148">Om deze reden kunnen beheerders de eerste back-up overdragen: **handmatig** (met behulp van verwijderbare media) om te voorkomen dat de bandbreedte-congestie of **automatisch via het netwerk** (op een opgegeven periode).</span><span class="sxs-lookup"><span data-stu-id="0531d-148">For this reason, administrators can choose to transfer the initial backup: **Manually** (using removable media) to avoid bandwidth congestion, or **Automatically over the network** (at a specified time).</span></span>

    <span data-ttu-id="0531d-149">Nadat de eerste back-up is voltooid, zijn de rest van de back-ups incrementele back-ups op de eerste back-up.</span><span class="sxs-lookup"><span data-stu-id="0531d-149">Once the initial backup is complete, the rest of the backups are incremental backups on the initial backup copy.</span></span> <span data-ttu-id="0531d-150">Incrementele back-ups zijn meestal kort en eenvoudig worden overgebracht via het netwerk.</span><span class="sxs-lookup"><span data-stu-id="0531d-150">Incremental backups tend to be small and are easily transferred across the network.</span></span>
10. <span data-ttu-id="0531d-151">Kies wanneer u de consistentiecontrole uitvoeren en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-151">Choose when you want the consistency check to run and click **Next**.</span></span>

    ![Consistentiecontrole](./media/backup-azure-backup-sql/pg-consistent.png)

    <span data-ttu-id="0531d-153">MABS kunt uitvoeren een consistentiecontrole uit de integriteit van de back-punt.</span><span class="sxs-lookup"><span data-stu-id="0531d-153">MABS can perform a consistency check to check the integrity of the backup point.</span></span> <span data-ttu-id="0531d-154">De controlesom van de back-upbestand op de productieserver (SQL Server-machine in dit scenario) en de gegevens waarvan een back-up is gemaakt voor het bestand op MABS wordt berekend.</span><span class="sxs-lookup"><span data-stu-id="0531d-154">It calculates the checksum of the backup file on the production server (SQL Server machine in this scenario) and the backed-up data for that file at MABS.</span></span> <span data-ttu-id="0531d-155">In het geval van een conflict optreedt, wordt ervan uitgegaan dat de back-upbestand op MABS beschadigd is.</span><span class="sxs-lookup"><span data-stu-id="0531d-155">In the case of a conflict, it is assumed that the backed-up file at MABS is corrupt.</span></span> <span data-ttu-id="0531d-156">De back-upgegevens herstelt MABS door te sturen de blokken die overeenkomt met de checksum komt niet overeen.</span><span class="sxs-lookup"><span data-stu-id="0531d-156">MABS rectifies the backed-up data by sending the blocks corresponding to the checksum mismatch.</span></span> <span data-ttu-id="0531d-157">De consistentiecontrole is een prestatie-intensieve bewerking, hebben beheerders de mogelijkheid de consistentiecontrole plannen of automatisch uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0531d-157">As the consistency check is a performance-intensive operation, administrators have the option of scheduling the consistency check or running it automatically.</span></span>
11. <span data-ttu-id="0531d-158">Als u online beveiliging van de gegevensbronnen, schakelt u de databases worden beveiligd door Azure en klikt u op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-158">To specify online protection of the datasources, select the databases to be protected to Azure and click **Next**.</span></span>

    ![Selecteer de gegevensbronnen](./media/backup-azure-backup-sql/pg-sqldatabases.png)
12. <span data-ttu-id="0531d-160">Beheerders kunnen kiezen voor back-upschema en bewaarbeleidsregels die aan de behoeften van de beleidsregels van hun organisatie.</span><span class="sxs-lookup"><span data-stu-id="0531d-160">Administrators can choose backup schedules and retention policies that suit their organization policies.</span></span>

    ![Planning en retentie](./media/backup-azure-backup-sql/pg-schedule.png)

    <span data-ttu-id="0531d-162">In dit voorbeeld worden back-ups eenmaal per dag uitgevoerd op 12:00 uur en 20: 00 (onderste gedeelte van het scherm)</span><span class="sxs-lookup"><span data-stu-id="0531d-162">In this example, backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen)</span></span>

    > [!NOTE]
    > <span data-ttu-id="0531d-163">Het is raadzaam om een aantal herstelpunten op korte termijn op schijf voor een snel herstel.</span><span class="sxs-lookup"><span data-stu-id="0531d-163">It’s a good practice to have a few short-term recovery points on disk, for quick recovery.</span></span> <span data-ttu-id="0531d-164">Deze herstelpunten worden gebruikt voor 'operationeel herstel'.</span><span class="sxs-lookup"><span data-stu-id="0531d-164">These recovery points are used for “operational recovery".</span></span> <span data-ttu-id="0531d-165">Azure fungeert als een goede externe locatie met hogere Sla's en beschikbaarheid gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="0531d-165">Azure serves as a good offsite location with higher SLAs and guaranteed availability.</span></span>
    >
    >

    <span data-ttu-id="0531d-166">**Kunt u beter**: Zorg ervoor dat Azure back-ups zijn gepland na de voltooiing van de lokale schijf back-ups met behulp van DPM.</span><span class="sxs-lookup"><span data-stu-id="0531d-166">**Best Practice**: Make sure that Azure Backups are scheduled after the completion of local disk backups using DPM.</span></span> <span data-ttu-id="0531d-167">Hierdoor is de laatste schijfback-up naar Azure moet worden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="0531d-167">This enables the latest disk backup to be copied to Azure.</span></span>

13. <span data-ttu-id="0531d-168">Kies het bewaarschema voor beleid.</span><span class="sxs-lookup"><span data-stu-id="0531d-168">Choose the retention policy schedule.</span></span> <span data-ttu-id="0531d-169">De details over de werking van het bewaarbeleid zijn beschikbaar op [gebruik Azure Backup ter vervanging van uw tape-infrastructuur artikel](backup-azure-backup-cloud-as-tape.md).</span><span class="sxs-lookup"><span data-stu-id="0531d-169">The details on how the retention policy works are provided at [Use Azure Backup to replace your tape infrastructure article](backup-azure-backup-cloud-as-tape.md).</span></span>

    ![Bewaarbeleid](./media/backup-azure-backup-sql/pg-retentionschedule.png)

    <span data-ttu-id="0531d-171">In dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0531d-171">In this example:</span></span>

    * <span data-ttu-id="0531d-172">Back-ups eenmaal per dag worden uitgevoerd op 12:00 uur en 20: 00 (onderste gedeelte van het scherm) en 180 dagen worden bewaard.</span><span class="sxs-lookup"><span data-stu-id="0531d-172">Backups are taken once a day at 12:00 PM and 8 PM (bottom part of the screen) and are retained for 180 days.</span></span>
    * <span data-ttu-id="0531d-173">De back-up elke zaterdag om 12:00 uur</span><span class="sxs-lookup"><span data-stu-id="0531d-173">The backup on Saturday at 12:00 P.M.</span></span> <span data-ttu-id="0531d-174">104 weken wordt bewaard</span><span class="sxs-lookup"><span data-stu-id="0531d-174">is retained for 104 weeks</span></span>
    * <span data-ttu-id="0531d-175">De back-up op de laatste zaterdag om 12:00 uur</span><span class="sxs-lookup"><span data-stu-id="0531d-175">The backup on Last Saturday at 12:00 P.M.</span></span> <span data-ttu-id="0531d-176">60 maanden bewaard</span><span class="sxs-lookup"><span data-stu-id="0531d-176">is retained for 60 months</span></span>
    * <span data-ttu-id="0531d-177">De back-up op de laatste zaterdag maart om 12:00 uur</span><span class="sxs-lookup"><span data-stu-id="0531d-177">The backup on Last Saturday of March at 12:00 P.M.</span></span> <span data-ttu-id="0531d-178">tien jaar worden bewaard</span><span class="sxs-lookup"><span data-stu-id="0531d-178">is retained for 10 years</span></span>
14. <span data-ttu-id="0531d-179">Klik op **volgende** en selecteer de relevante optie voor het overdragen van de eerste back-up naar Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-179">Click **Next** and select the appropriate option for transferring the initial backup copy to Azure.</span></span> <span data-ttu-id="0531d-180">U kunt kiezen **automatisch via het netwerk** of **Offline back-up**.</span><span class="sxs-lookup"><span data-stu-id="0531d-180">You can choose **Automatically over the network** or **Offline Backup**.</span></span>

    * <span data-ttu-id="0531d-181">**Automatisch via het netwerk** worden de back-upgegevens naar Azure volgens het schema voor back-up is gekozen.</span><span class="sxs-lookup"><span data-stu-id="0531d-181">**Automatically over the network** transfers the backup data to Azure as per the schedule chosen for backup.</span></span>
    * <span data-ttu-id="0531d-182">Hoe **Offline back-up** works wordt uitgelegd op [Offlineback-upwerkstroom in Azure Backup](backup-azure-backup-import-export.md).</span><span class="sxs-lookup"><span data-stu-id="0531d-182">How **Offline Backup** works is explained at [Offline Backup workflow in Azure Backup](backup-azure-backup-import-export.md).</span></span>

    <span data-ttu-id="0531d-183">Kies de relevante gegevensoverdrachtmechanisme voor het verzenden van de eerste back-up naar Azure, klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-183">Choose the relevant transfer mechanism to send the initial backup copy to Azure and click **Next**.</span></span>
15. <span data-ttu-id="0531d-184">Zodra u de details van het beleid in controleren de **samenvatting** scherm, klikt u op de **groep maken** knop om de werkstroom te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0531d-184">Once you review the policy details in the **Summary** screen, click on the **Create group** button to complete the workflow.</span></span> <span data-ttu-id="0531d-185">U kunt klikken op de **sluiten** knop en de voortgang van de taak in de werkruimte bewaking.</span><span class="sxs-lookup"><span data-stu-id="0531d-185">You can click the **Close** button and monitor the job progress in Monitoring workspace.</span></span>

    ![Maken van een beveiligingsgroep In uitvoering](./media/backup-azure-backup-sql/pg-summary.png)

## <a name="on-demand-backup-of-a-sql-server-database"></a><span data-ttu-id="0531d-187">Op aanvraag back-up van een SQL Server-database</span><span class="sxs-lookup"><span data-stu-id="0531d-187">On-demand backup of a SQL Server database</span></span>
<span data-ttu-id="0531d-188">Tijdens de vorige stappen een back-upbeleid gemaakt, wordt 'herstelpunt' alleen gemaakt als de eerste back-up plaatsvindt.</span><span class="sxs-lookup"><span data-stu-id="0531d-188">While the previous steps created a backup policy, a “recovery point” is created only when the first backup occurs.</span></span> <span data-ttu-id="0531d-189">In plaats van de planner te starten wacht, wijst de stappen onder het maken van een herstel trigger handmatig.</span><span class="sxs-lookup"><span data-stu-id="0531d-189">Rather than waiting for the scheduler to kick in, the steps below trigger the creation of a recovery point manually.</span></span>

1. <span data-ttu-id="0531d-190">Wacht totdat de beveiligingsstatus van de groep bevat **OK** voor de database voordat u het herstelpunt maakt.</span><span class="sxs-lookup"><span data-stu-id="0531d-190">Wait until the protection group status shows **OK** for the database before creating the recovery point.</span></span>

    ![Leden van beveiligingsgroep](./media/backup-azure-backup-sql/sqlbackup-recoverypoint.png)
2. <span data-ttu-id="0531d-192">Met de rechtermuisknop op de database en selecteer **herstelpunt maken**.</span><span class="sxs-lookup"><span data-stu-id="0531d-192">Right-click on the database and select **Create Recovery Point**.</span></span>

    ![Online herstelpunt maken](./media/backup-azure-backup-sql/sqlbackup-createrp.png)
3. <span data-ttu-id="0531d-194">Kies **Onlinebeveiliging** in de vervolgkeuzelijst en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="0531d-194">Choose **Online Protection** in the drop-down menu and click **OK**.</span></span> <span data-ttu-id="0531d-195">Hiermee start u het maken van een herstelpunt in Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-195">This starts the creation of a recovery point in Azure.</span></span>

    ![Herstelpunt maken](./media/backup-azure-backup-sql/sqlbackup-azure.png)
4. <span data-ttu-id="0531d-197">Vindt u de voortgang van de taak in de **bewaking** werkruimte vindt u een onderhanden taak zoals die worden beschreven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="0531d-197">You can view the job progress in the **Monitoring** workspace where you'll find an in progress job like the one depicted in the next figure.</span></span>

    ![Bewaking van console](./media/backup-azure-backup-sql/sqlbackup-monitoring.png)

## <a name="recover-a-sql-server-database-from-azure"></a><span data-ttu-id="0531d-199">Een SQL Server-database herstellen van Azure</span><span class="sxs-lookup"><span data-stu-id="0531d-199">Recover a SQL Server database from Azure</span></span>
<span data-ttu-id="0531d-200">De volgende stappen zijn vereist voor het herstellen van een beveiligde entiteit (SQL Server-database) van Azure.</span><span class="sxs-lookup"><span data-stu-id="0531d-200">The following steps are required to recover a protected entity (SQL Server database) from Azure.</span></span>

1. <span data-ttu-id="0531d-201">Open de beheerconsole van de DPM-server.</span><span class="sxs-lookup"><span data-stu-id="0531d-201">Open the DPM server Management Console.</span></span> <span data-ttu-id="0531d-202">Navigeer naar **herstel** werkruimte waarin u de servers kunt zien een back-up door DPM.</span><span class="sxs-lookup"><span data-stu-id="0531d-202">Navigate to **Recovery** workspace where you can see the servers backed up by DPM.</span></span> <span data-ttu-id="0531d-203">Blader op de vereiste database (in dit geval ReportServer$ MSDPM2012).</span><span class="sxs-lookup"><span data-stu-id="0531d-203">Browse the required database (in this case ReportServer$MSDPM2012).</span></span> <span data-ttu-id="0531d-204">Selecteer een **herstel vanaf** die eindigt op **Online**.</span><span class="sxs-lookup"><span data-stu-id="0531d-204">Select a **Recovery from** time which ends with **Online**.</span></span>

    ![Herstelpunt selecteren](./media/backup-azure-backup-sql/sqlbackup-restorepoint.png)
2. <span data-ttu-id="0531d-206">Met de rechtermuisknop op de naam van de database en klik op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="0531d-206">Right-click the database name and click **Recover**.</span></span>

    ![Herstellen van Azure](./media/backup-azure-backup-sql/sqlbackup-recover.png)
3. <span data-ttu-id="0531d-208">DPM geeft de details van het herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="0531d-208">DPM shows the details of the recovery point.</span></span> <span data-ttu-id="0531d-209">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-209">Click **Next**.</span></span> <span data-ttu-id="0531d-210">Voor het overschrijven van de database, selecteert u het hersteltype **herstellen naar oorspronkelijk exemplaar van SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="0531d-210">To overwrite the database, select the recovery type **Recover to original instance of SQL Server**.</span></span> <span data-ttu-id="0531d-211">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-211">Click **Next**.</span></span>

    ![Herstellen naar oorspronkelijke locatie](./media/backup-azure-backup-sql/sqlbackup-recoveroriginal.png)

    <span data-ttu-id="0531d-213">In dit voorbeeld kan DPM herstel van de database naar een ander exemplaar van SQL Server of naar een netwerkmap zelfstandige.</span><span class="sxs-lookup"><span data-stu-id="0531d-213">In this example, DPM allows recovery of the database to another SQL Server instance or to a standalone network folder.</span></span>
4. <span data-ttu-id="0531d-214">In de **herstelopties opgeven** scherm kunt u de opties voor Systeemherstel zoals netwerkbandbreedtegebruik de bandbreedte die wordt gebruikt door de herstelbewerking beperken.</span><span class="sxs-lookup"><span data-stu-id="0531d-214">In the **Specify Recovery options** screen, you can select the recovery options like Network bandwidth usage throttling to throttle the bandwidth used by recovery.</span></span> <span data-ttu-id="0531d-215">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="0531d-215">Click **Next**.</span></span>
5. <span data-ttu-id="0531d-216">In de **samenvatting** scherm ziet u alle herstel-configuraties die tot nu toe is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="0531d-216">In the **Summary** screen, you see all the recovery configurations provided so far.</span></span> <span data-ttu-id="0531d-217">Klik op **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="0531d-217">Click **Recover**.</span></span>

    <span data-ttu-id="0531d-218">De herstelstatus ziet u de database wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="0531d-218">The Recovery status shows the database being recovered.</span></span> <span data-ttu-id="0531d-219">U kunt klikken op **sluiten** naar de wizard te sluiten en de voortgang in de **bewaking** werkruimte.</span><span class="sxs-lookup"><span data-stu-id="0531d-219">You can click **Close** to close the wizard and view the progress in the **Monitoring** workspace.</span></span>

    ![Proces voor accountherstel initiëren](./media/backup-azure-backup-sql/sqlbackup-recoverying.png)

    <span data-ttu-id="0531d-221">Nadat het herstel is voltooid, is de teruggezette database consistent-toepassing.</span><span class="sxs-lookup"><span data-stu-id="0531d-221">Once the recovery is completed, the restored database is application consistent.</span></span>

### <a name="next-steps"></a><span data-ttu-id="0531d-222">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0531d-222">Next Steps:</span></span>
<span data-ttu-id="0531d-223">• [Veelgestelde vragen over azure Backup](backup-azure-backup-faq.md)</span><span class="sxs-lookup"><span data-stu-id="0531d-223">•    [Azure Backup FAQ](backup-azure-backup-faq.md)</span></span>
