---
title: Azure SQL Database back-ups opslaan voor maximaal tien jaar | Microsoft Docs
description: Meer informatie over hoe Azure SQL Database opslaan back-ups ondersteunt maximaal tien jaar.
keywords: 
services: sql-database
documentationcenter: 
author: anosov1960
manager: jhubbard
editor: 
ms.assetid: 66fdb8b8-5903-4d3a-802e-af08d204566e
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 12/22/2016
ms.author: sashan
ms.openlocfilehash: 25e651203f804fbf32d632b5f83145a3f3f72a7f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="store-azure-sql-database-backups-for-up-to-10-years"></a><span data-ttu-id="e769d-103">Azure SQL Database back-ups voor maximaal tien jaar opslaan</span><span class="sxs-lookup"><span data-stu-id="e769d-103">Store Azure SQL Database backups for up to 10 years</span></span>
<span data-ttu-id="e769d-104">Veel toepassingen hebben regelgeving, compatibiliteit of andere zakelijke doeleinden die vereisen dat u voor het bewaren van back-ups buiten de 7 35 dagen geleverd door de Azure SQL Database [automatische back-ups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-104">Many applications have regulatory, compliance, or other business purposes that require you to retain database backups beyond the 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="e769d-105">Met behulp van de lange termijn bewaren van back-functie kunt u uw back-ups van SQL database opslaan in een Azure Recovery Services-kluis voor maximaal tien jaar.</span><span class="sxs-lookup"><span data-stu-id="e769d-105">By using the long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up to 10 years.</span></span> <span data-ttu-id="e769d-106">U kunt maximaal 1000 databases per kluis opslaan.</span><span class="sxs-lookup"><span data-stu-id="e769d-106">You can store up to 1,000 databases per vault.</span></span> <span data-ttu-id="e769d-107">Vervolgens kunt u back-up selecteren in de kluis om het te herstellen als een nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="e769d-107">You then can select any backup in the vault to restore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e769d-108">Lange bewaartermijn van de back-up is momenteel in preview en beschikbaar zijn in de volgende gebieden: Australië-Oost, Australië-Zuidoost, Brazilië-Zuid, VS-midden, Oost-Azië, VS-Oost, VS-Oost 2, India centraal, India-Zuid, Japan-Oost, Japan-West, Noordelijk Centraal, VS, Noord Europa, Zuid-centraal VS, Zuidoost-Azië, West-Europa en VS-West.</span><span class="sxs-lookup"><span data-stu-id="e769d-108">Long-term backup retention is currently in preview and available in the following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="e769d-109">U kunt maximaal 200 databases per kluis inschakelen tijdens een periode van 24 uur.</span><span class="sxs-lookup"><span data-stu-id="e769d-109">You can enable up to 200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="e769d-110">Het is raadzaam dat u een afzonderlijke kluis voor elke server om te minimaliseren, de impact van deze limiet.</span><span class="sxs-lookup"><span data-stu-id="e769d-110">We recommend that you use a separate vault for each server to minimize the impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="e769d-111">De werking van de back-up op lange termijn bewaren van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="e769d-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="e769d-112">Met bewaren van back-up op lange termijn, kunt u een SQL database-server koppelen aan een Azure Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="e769d-113">In de dezelfde Azure-abonnement dat de SQL-server gemaakt en in dezelfde geografische regio en resourcegroep, moet u de kluis maken.</span><span class="sxs-lookup"><span data-stu-id="e769d-113">You must create the vault in the same Azure subscription that created the SQL server and in the same geographic region and resource group.</span></span> 
* <span data-ttu-id="e769d-114">Configureert u een bewaarbeleid voor elke database.</span><span class="sxs-lookup"><span data-stu-id="e769d-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="e769d-115">Het beleid zorgt ervoor dat de wekelijkse volledige back-ups moeten worden gekopieerd naar de Recovery Services-kluis en bewaard voor de opgegeven bewaarperiode (maximaal 10 jaar).</span><span class="sxs-lookup"><span data-stu-id="e769d-115">The policy causes the weekly full database backups to be copied to the Recovery Services vault and retained for the specified retention period (up to 10 years).</span></span> 
* <span data-ttu-id="e769d-116">Vervolgens kunt u de database uit een van deze back-ups herstellen naar een nieuwe database in een willekeurige server in het abonnement.</span><span class="sxs-lookup"><span data-stu-id="e769d-116">You can then restore the database from any of these backups to a new database in any server in the subscription.</span></span> <span data-ttu-id="e769d-117">Azure-opslag maakt een kopie van de bestaande back-ups en het exemplaar heeft geen invloed van de prestaties op de bestaande database.</span><span class="sxs-lookup"><span data-stu-id="e769d-117">Azure storage creates a copy from existing backups, and the copy has no performance impact on the existing database.</span></span>

> [!TIP]
> <span data-ttu-id="e769d-118">Zie voor een uitleg handleiding [en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-118">For a how-to guide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="e769d-119">Lange bewaartermijn van de back-up inschakelen</span><span class="sxs-lookup"><span data-stu-id="e769d-119">Enable long-term backup retention</span></span>

<span data-ttu-id="e769d-120">Lange bewaartermijn van back-up voor een database configureren:</span><span class="sxs-lookup"><span data-stu-id="e769d-120">To configure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="e769d-121">Maak een Azure Recovery Services-kluis in dezelfde regio, abonnement en resourcegroep als uw SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="e769d-121">Create an Azure Recovery Services vault in the same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="e769d-122">De server naar de kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="e769d-122">Register the server to the vault.</span></span>
3. <span data-ttu-id="e769d-123">Maak een beleid voor Azure Recovery Services-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="e769d-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="e769d-124">Het beveiligingsbeleid van toepassing op de databases die langdurig bewaren van back-up vereisen.</span><span class="sxs-lookup"><span data-stu-id="e769d-124">Apply the protection policy to the databases that require long-term backup retention.</span></span>

<span data-ttu-id="e769d-125">Als u wilt configureren, beheren en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis, voert u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e769d-125">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="e769d-126">Met de Azure portal: klik op **lange bewaartermijn van de back-**, selecteert u een database en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="e769d-126">Using the Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selecteer een database voor lange bewaartermijn van de back-up](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="e769d-128">Met behulp van PowerShell: Ga naar [en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-128">Using PowerShell: Go to [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-the-long-term-backup-retention-feature"></a><span data-ttu-id="e769d-129">Een database die opgeslagen met de functie voor de lange termijn bewaren van back-up terugzetten</span><span class="sxs-lookup"><span data-stu-id="e769d-129">Restore a database that's stored with the long-term backup retention feature</span></span>

<span data-ttu-id="e769d-130">Herstellen vanuit back-up op lange termijn bewaren van back-up:</span><span class="sxs-lookup"><span data-stu-id="e769d-130">To recover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="e769d-131">Lijst van de kluis waarin de back-up is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e769d-131">List the vault where the backup is stored.</span></span>
2. <span data-ttu-id="e769d-132">Lijst van de container die is gekoppeld aan uw logische server.</span><span class="sxs-lookup"><span data-stu-id="e769d-132">List the container that is mapped to your logical server.</span></span>
3. <span data-ttu-id="e769d-133">Lijst van de gegevensbron in de kluis die is gekoppeld aan uw database.</span><span class="sxs-lookup"><span data-stu-id="e769d-133">List the data source within the vault that is mapped to your database.</span></span>
4. <span data-ttu-id="e769d-134">Lijst van de herstelpunten die beschikbaar zijn voor het herstellen.</span><span class="sxs-lookup"><span data-stu-id="e769d-134">List the recovery points that are available to restore.</span></span>
5. <span data-ttu-id="e769d-135">Herstel de database van het herstelpunt dat naar de doelserver in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="e769d-135">Restore the database from the recovery point to the target server within your subscription.</span></span>

<span data-ttu-id="e769d-136">Als u wilt configureren, beheren en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis, voert u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e769d-136">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of the following:</span></span>

* <span data-ttu-id="e769d-137">Met de Azure portal: Ga naar [lange Backup-bewaartermijn met de Azure portal beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-137">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="e769d-138">Met behulp van PowerShell: Ga naar [lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-138">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="e769d-139">Prijzen voor lange bewaartermijn van de back-ophalen</span><span class="sxs-lookup"><span data-stu-id="e769d-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="e769d-140">Lange bewaartermijn van back-up van een SQL-database wordt in rekening gebracht volgens de [Azure Backup-services prijzen tarieven](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="e769d-140">Long-term backup retention of a SQL database is charged according to the [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="e769d-141">Nadat de SQL database-server naar de kluis is geregistreerd, wordt u in rekening gebracht voor de totale opslag die wordt gebruikt door de wekelijkse back-ups zijn opgeslagen in de kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-141">After the SQL database server is registered to the vault, you are charged for the total storage that's used by the weekly backups stored in the vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="e769d-142">Beschikbare back-ups weergeven die zijn opgeslagen in lange bewaartermijn van de back-up</span><span class="sxs-lookup"><span data-stu-id="e769d-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="e769d-143">Als u wilt configureren, beheren en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis met behulp van de Azure-portal, voert u een van de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="e769d-143">To configure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using the Azure portal, do either of the following:</span></span>

* <span data-ttu-id="e769d-144">Met de Azure portal: Ga naar [lange Backup-bewaartermijn met de Azure portal beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-144">Using the Azure portal: Go to [Manage long-term backup retention using the Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="e769d-145">Met behulp van PowerShell: Ga naar [lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-145">Using PowerShell: Go to [Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="e769d-146">Lange bewaartermijn uitschakelen</span><span class="sxs-lookup"><span data-stu-id="e769d-146">Disable long-term retention</span></span>

<span data-ttu-id="e769d-147">De recovery-service wordt automatisch het opruimen van de back-ups op basis van het opgegeven bewaarbeleid verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e769d-147">The recovery service automatically handles the cleanup of backups based on the provided retention policy.</span></span> 

<span data-ttu-id="e769d-148">Als u wilt stoppen met het verzenden van de back-ups voor een specifieke database naar de kluis, verwijder het bewaarbeleid voor die database.</span><span class="sxs-lookup"><span data-stu-id="e769d-148">To stop sending the backups for a specific database to the vault, remove the retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="e769d-149">De back-ups die zich al in de kluis worden hierdoor niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="e769d-149">The backups that are already in the vault are unaffected.</span></span> <span data-ttu-id="e769d-150">Ze worden automatisch verwijderd door de herstelservice wanneer de bewaartermijn is verstreken.</span><span class="sxs-lookup"><span data-stu-id="e769d-150">They are automatically deleted by the recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="e769d-151">Lange bewaartermijn in back-Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="e769d-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="e769d-152">**Kan ik handmatig specifieke back-ups in de kluis verwijderen?**</span><span class="sxs-lookup"><span data-stu-id="e769d-152">**Can I manually delete specific backups in the vault?**</span></span>

<span data-ttu-id="e769d-153">Momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="e769d-153">Not currently.</span></span> <span data-ttu-id="e769d-154">Back-ups van ruimt de kluis automatisch wanneer de bewaartermijn is verlopen.</span><span class="sxs-lookup"><span data-stu-id="e769d-154">The vault automatically cleans up backups when the retention period has expired.</span></span>

<span data-ttu-id="e769d-155">**Kan ik mijn server voor het opslaan van back-ups naar meer dan één kluis registreren?**</span><span class="sxs-lookup"><span data-stu-id="e769d-155">**Can I register my server to store backups to more than one vault?**</span></span>

<span data-ttu-id="e769d-156">Nee, kunt u back-ups naar slechts één kluis momenteel opslaan op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="e769d-156">No, you can currently store backups to only one vault at a time.</span></span>

<span data-ttu-id="e769d-157">**Kan ik een kluis en de server hebben met verschillende abonnementen?**</span><span class="sxs-lookup"><span data-stu-id="e769d-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="e769d-158">Nee, de kluis en de server moeten zich in hetzelfde abonnement en dezelfde resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="e769d-158">No, currently the vault and server must be in the same subscription and resource group.</span></span>

<span data-ttu-id="e769d-159">**Kan ik een kluis die ik in een regio die verschilt van mijn server regio gemaakt gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="e769d-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="e769d-160">Nee, de kluis en de server, moet in dezelfde regio kopie tijd minimaliseren en verkeer kosten te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="e769d-160">No, the vault and server must be in the same region to minimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="e769d-161">**Hoeveel databases kan ik opslaan in een kluis?**</span><span class="sxs-lookup"><span data-stu-id="e769d-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="e769d-162">Op dit moment kunnen ondersteuning we voor maximaal 1000 databases per kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-162">Currently, we support up to 1,000 databases per vault.</span></span> 

<span data-ttu-id="e769d-163">**Het aantal kluizen kan ik maken per abonnement?**</span><span class="sxs-lookup"><span data-stu-id="e769d-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="e769d-164">U kunt maximaal 25 kluizen per abonnement maken.</span><span class="sxs-lookup"><span data-stu-id="e769d-164">You can create up to 25 vaults per subscription.</span></span>

<span data-ttu-id="e769d-165">**Hoeveel databases kan ik per dag per kluis configureren?**</span><span class="sxs-lookup"><span data-stu-id="e769d-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="e769d-166">U kunt 200 databases per dag per kluis instellen.</span><span class="sxs-lookup"><span data-stu-id="e769d-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="e769d-167">**Werkt langdurig bewaren van back-up met elastische pools?**</span><span class="sxs-lookup"><span data-stu-id="e769d-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="e769d-168">Ja.</span><span class="sxs-lookup"><span data-stu-id="e769d-168">Yes.</span></span> <span data-ttu-id="e769d-169">Elke database in de groep kan worden geconfigureerd met het bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="e769d-169">Any database in the pool can be configured with the retention policy.</span></span>

<span data-ttu-id="e769d-170">**Kan ik een kiezen voor de tijd waarop de back-up is gemaakt?**</span><span class="sxs-lookup"><span data-stu-id="e769d-170">**Can I choose the time at which the backup is created?**</span></span>

<span data-ttu-id="e769d-171">Nee, bepaalt de SQL-Database het back-upschema minimaliseren de invloed van de prestaties van uw databases.</span><span class="sxs-lookup"><span data-stu-id="e769d-171">No, SQL Database controls the backup schedule to minimize the performance impact on your databases.</span></span>

<span data-ttu-id="e769d-172">**Ik heb transparante gegevensversleuteling is ingeschakeld voor de database. Kan ik deze met de kluis gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="e769d-172">**I have transparent data encryption enabled for my database. Can I use it with the vault?**</span></span> 

<span data-ttu-id="e769d-173">Ja, transparante gegevensversleuteling wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e769d-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="e769d-174">U kunt de database herstellen uit de kluis, zelfs als de oorspronkelijke database niet meer bestaat.</span><span class="sxs-lookup"><span data-stu-id="e769d-174">You can restore the database from the vault even if the original database no longer exists.</span></span>

<span data-ttu-id="e769d-175">**Wat gebeurt er met de back-ups in de kluis als mijn abonnement wordt onderbroken?**</span><span class="sxs-lookup"><span data-stu-id="e769d-175">**What happens with the backups in the vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="e769d-176">Als uw abonnement wordt onderbroken, wordt de bestaande databases en de back-ups behouden.</span><span class="sxs-lookup"><span data-stu-id="e769d-176">If your subscription is suspended, we retain the existing databases and backups.</span></span> <span data-ttu-id="e769d-177">Nieuwe back-ups worden niet gekopieerd naar de kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-177">New backups are not copied to the vault.</span></span> <span data-ttu-id="e769d-178">Nadat u het abonnement opnieuw activeert, hervat de service back-ups kopiëren naar de kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-178">After you reactivate the subscription, the service resumes copying backups to the vault.</span></span> <span data-ttu-id="e769d-179">Uw kluis wordt toegankelijk is voor de bewerkingen voor het herstellen met behulp van de back-ups die zijn gekopieerd er voordat u het abonnement is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="e769d-179">Your vault becomes accessible to the restore operations by using the backups that were copied there before the subscription was suspended.</span></span> 

<span data-ttu-id="e769d-180">**Krijg ik toegang tot de back-upbestanden voor SQL-database zodat ik kan downloaden of deze naar de SQL-server terugzetten?**</span><span class="sxs-lookup"><span data-stu-id="e769d-180">**Can I get access to the SQL database backup files so I can download or restore them to the SQL server?**</span></span>

<span data-ttu-id="e769d-181">Nee, momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="e769d-181">No, not currently.</span></span>

<span data-ttu-id="e769d-182">**Is het mogelijk om meerdere planningen (dagelijks, wekelijks, maandelijks, jaarlijks) binnen een bewaarbeleid SQL.**</span><span class="sxs-lookup"><span data-stu-id="e769d-182">**Is it possible to have multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="e769d-183">Nee, meerdere schema's zijn momenteel alleen beschikbaar voor back-ups van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="e769d-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="e769d-184">**Wat gebeurt er als we langdurig bewaren van back-up voor een database die is een secundaire actieve geo-replicatie-database hebt ingesteld?**</span><span class="sxs-lookup"><span data-stu-id="e769d-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="e769d-185">Omdat er geen back-ups op replica's onderneemt, is er momenteel geen optie voor het bewaren van de lange termijn back-up op secundaire databases.</span><span class="sxs-lookup"><span data-stu-id="e769d-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="e769d-186">Het is echter belangrijk dat gebruikers langdurig bewaren van back-up op een secundaire actieve geo-replicatie-database instellen voor de volgende redenen:</span><span class="sxs-lookup"><span data-stu-id="e769d-186">However, it is important for users to set up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="e769d-187">Wanneer een failover gebeurt en de database een primaire database wordt, duurt we een volledige back-up, die is geüpload naar de kluis.</span><span class="sxs-lookup"><span data-stu-id="e769d-187">When a failover happens and the database becomes a primary database, we take a full backup, which is uploaded to vault.</span></span>
* <span data-ttu-id="e769d-188">Er is geen extra kosten verbonden aan de klant voor het instellen van langdurig bewaren van back-up op een secundaire database.</span><span class="sxs-lookup"><span data-stu-id="e769d-188">There is no extra cost to the customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e769d-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e769d-189">Next steps</span></span>
<span data-ttu-id="e769d-190">Omdat de databaseback-ups voorkomen dat gegevens per ongeluk beschadigd of verwijderd, zijn ze een essentieel onderdeel van een zakelijke continuïteit en noodherstelplan.</span><span class="sxs-lookup"><span data-stu-id="e769d-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="e769d-191">Zie voor meer informatie over de andere SQL-Database-oplossingen voor bedrijfscontinuïteit, [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="e769d-191">To learn about the other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
