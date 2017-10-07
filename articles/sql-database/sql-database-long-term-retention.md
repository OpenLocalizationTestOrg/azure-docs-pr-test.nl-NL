---
title: aaaStore Azure SQL Database back-ups voor up too10 jaar | Microsoft Docs
description: Meer informatie over hoe Azure SQL Database ondersteunt opslag back-ups voor up too10 jaar.
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
ms.openlocfilehash: 5825ebd4e3bd66b59b13aea603d377ef814a1df3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="store-azure-sql-database-backups-for-up-too10-years"></a><span data-ttu-id="0c308-103">Azure SQL Database back-ups opslaan voor up too10 jaar</span><span class="sxs-lookup"><span data-stu-id="0c308-103">Store Azure SQL Database backups for up too10 years</span></span>
<span data-ttu-id="0c308-104">Veel toepassingen hebben regelgeving, compatibiliteit of andere zakelijke doeleinden die vereisen dat u tooretain databaseback-ups buiten Hallo 7 35 dagen geleverd door de Azure SQL Database [automatische back-ups](sql-database-automated-backups.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-104">Many applications have regulatory, compliance, or other business purposes that require you tooretain database backups beyond hello 7-35 days provided by Azure SQL Database [automatic backups](sql-database-automated-backups.md).</span></span> <span data-ttu-id="0c308-105">Hallo op lange termijn bewaren van back-functie gebruikt, kunt u uw back-ups van SQL database opslaan in een Azure Recovery Services-kluis voor up too10 jaar.</span><span class="sxs-lookup"><span data-stu-id="0c308-105">By using hello long-term backup retention feature, you can store your SQL database backups in an Azure Recovery Services vault for up too10 years.</span></span> <span data-ttu-id="0c308-106">U kunt opslaan van too1, 000 databases per kluis.</span><span class="sxs-lookup"><span data-stu-id="0c308-106">You can store up too1,000 databases per vault.</span></span> <span data-ttu-id="0c308-107">Vervolgens kunt u back-up in Hallo kluis toorestore als een nieuwe database.</span><span class="sxs-lookup"><span data-stu-id="0c308-107">You then can select any backup in hello vault toorestore it as a new database.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0c308-108">Lange bewaartermijn van de back-up is momenteel in preview en beschikbaar zijn in de volgende regio's Hallo: Australië-Oost, Australië-Zuidoost, Brazilië-Zuid, VS-midden, Oost-Azië, VS-Oost, VS-Oost 2, India centraal, India-Zuid, Japan-Oost, Japan-West, Noordelijk Centraal, VS, Noord Europa, Zuid-centraal VS, Zuidoost-Azië, West-Europa en VS-West.</span><span class="sxs-lookup"><span data-stu-id="0c308-108">Long-term backup retention is currently in preview and available in hello following regions: Australia East, Australia Southeast, Brazil South, Central US, East Asia, East US, East US 2, India Central, India South, Japan East, Japan West, North Central US, North Europe, South Central US, Southeast Asia, West Europe, and West US.</span></span>
>

> [!NOTE]
> <span data-ttu-id="0c308-109">U kunt inschakelen van de databases too200 per kluis gedurende een periode van 24 uur.</span><span class="sxs-lookup"><span data-stu-id="0c308-109">You can enable up too200 databases per vault during a 24-hour period.</span></span> <span data-ttu-id="0c308-110">Het is raadzaam dat u een afzonderlijke kluis voor elke server toominimize Hallo gevolgen van deze limiet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0c308-110">We recommend that you use a separate vault for each server toominimize hello impact of this limit.</span></span> 
> 

## <a name="how-sql-database-long-term-backup-retention-works"></a><span data-ttu-id="0c308-111">De werking van de back-up op lange termijn bewaren van SQL-Database</span><span class="sxs-lookup"><span data-stu-id="0c308-111">How SQL Database long-term backup retention works</span></span>

<span data-ttu-id="0c308-112">Met bewaren van back-up op lange termijn, kunt u een SQL database-server koppelen aan een Azure Recovery Services-kluis.</span><span class="sxs-lookup"><span data-stu-id="0c308-112">With long-term backup retention, you can associate a SQL database server with an Azure Recovery Services vault.</span></span> 

* <span data-ttu-id="0c308-113">U moet Hallo kluis maken in dezelfde Azure-abonnement dat Hallo SQL-server gemaakt Hallo en Hallo in dezelfde geografische regio en resource-groep.</span><span class="sxs-lookup"><span data-stu-id="0c308-113">You must create hello vault in hello same Azure subscription that created hello SQL server and in hello same geographic region and resource group.</span></span> 
* <span data-ttu-id="0c308-114">Configureert u een bewaarbeleid voor elke database.</span><span class="sxs-lookup"><span data-stu-id="0c308-114">You then configure a retention policy for any database.</span></span> <span data-ttu-id="0c308-115">Hallo beleid oorzaken Hallo wekelijkse volledige databaseback-ups toobe gekopieerd toohello Recovery Services-kluis en bewaard voor de opgegeven bewaarperiode hello (omhoog too10 jaar).</span><span class="sxs-lookup"><span data-stu-id="0c308-115">hello policy causes hello weekly full database backups toobe copied toohello Recovery Services vault and retained for hello specified retention period (up too10 years).</span></span> 
* <span data-ttu-id="0c308-116">Vervolgens kunt u Hallo database terugzetten vanuit een van deze back-ups tooa nieuwe database in een willekeurige server in het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="0c308-116">You can then restore hello database from any of these backups tooa new database in any server in hello subscription.</span></span> <span data-ttu-id="0c308-117">Azure-opslag maakt een kopie van de bestaande back-ups en Hallo-exemplaar heeft geen invloed prestaties op Hallo bestaande database.</span><span class="sxs-lookup"><span data-stu-id="0c308-117">Azure storage creates a copy from existing backups, and hello copy has no performance impact on hello existing database.</span></span>

> [!TIP]
> <span data-ttu-id="0c308-118">Zie voor een hoe tooguide [en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-118">For a how-tooguide, see [Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="enable-long-term-backup-retention"></a><span data-ttu-id="0c308-119">Lange bewaartermijn van de back-up inschakelen</span><span class="sxs-lookup"><span data-stu-id="0c308-119">Enable long-term backup retention</span></span>

<span data-ttu-id="0c308-120">tooconfigure lange Backup-bewaartermijn voor een database:</span><span class="sxs-lookup"><span data-stu-id="0c308-120">tooconfigure long-term backup retention for a database:</span></span>

1. <span data-ttu-id="0c308-121">Een Azure Recovery Services-kluis maken in Hallo dezelfde regio, abonnement en resource-groep als uw SQL database-server.</span><span class="sxs-lookup"><span data-stu-id="0c308-121">Create an Azure Recovery Services vault in hello same region, subscription, and resource group as your SQL database server.</span></span> 
2. <span data-ttu-id="0c308-122">Hallo server toohello kluis registreren.</span><span class="sxs-lookup"><span data-stu-id="0c308-122">Register hello server toohello vault.</span></span>
3. <span data-ttu-id="0c308-123">Maak een beleid voor Azure Recovery Services-beveiliging.</span><span class="sxs-lookup"><span data-stu-id="0c308-123">Create an Azure Recovery Services protection policy.</span></span>
4. <span data-ttu-id="0c308-124">Toepassing hello beveiliging beleid toohello databases waarvoor het langdurig bewaren van back-up.</span><span class="sxs-lookup"><span data-stu-id="0c308-124">Apply hello protection policy toohello databases that require long-term backup retention.</span></span>

<span data-ttu-id="0c308-125">tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis en voer een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="0c308-125">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="0c308-126">Azure-portal met behulp van Hallo: klik op **lange bewaartermijn van de back-**, selecteert u een database en klik vervolgens op **configureren**.</span><span class="sxs-lookup"><span data-stu-id="0c308-126">Using hello Azure portal: Click **Long-term backup retention**, select a database, and then click **Configure**.</span></span> 

   ![Selecteer een database voor lange bewaartermijn van de back-up](./media/sql-database-get-started-backup-recovery/select-database-for-long-term-backup-retention.png)

* <span data-ttu-id="0c308-128">Met behulp van PowerShell: Ga te[en herstel van back-up op lange termijn bewaren van Azure SQL Database configureren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-128">Using PowerShell: Go too[Configure and restore from Azure SQL Database long-term backup retention](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="restore-a-database-thats-stored-with-hello-long-term-backup-retention-feature"></a><span data-ttu-id="0c308-129">Herstellen van een database die opgeslagen met Hallo op lange termijn bewaren van back-functie</span><span class="sxs-lookup"><span data-stu-id="0c308-129">Restore a database that's stored with hello long-term backup retention feature</span></span>

<span data-ttu-id="0c308-130">toorecover van back-up op lange termijn bewaren van back-up:</span><span class="sxs-lookup"><span data-stu-id="0c308-130">toorecover from a long-term backup retention backup:</span></span>

1. <span data-ttu-id="0c308-131">Lijst Hallo kluis waar Hallo back-up is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="0c308-131">List hello vault where hello backup is stored.</span></span>
2. <span data-ttu-id="0c308-132">Lijst Hallo-container die is toegewezen tooyour logische server.</span><span class="sxs-lookup"><span data-stu-id="0c308-132">List hello container that is mapped tooyour logical server.</span></span>
3. <span data-ttu-id="0c308-133">Hallo lijstgegevensbron binnen Hallo kluis die is toegewezen tooyour-database.</span><span class="sxs-lookup"><span data-stu-id="0c308-133">List hello data source within hello vault that is mapped tooyour database.</span></span>
4. <span data-ttu-id="0c308-134">Lijst Hallo herstelpunten die toorestore beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="0c308-134">List hello recovery points that are available toorestore.</span></span>
5. <span data-ttu-id="0c308-135">Hallo-database terugzetten vanaf Hallo herstelpunt toohello doelserver binnen uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="0c308-135">Restore hello database from hello recovery point toohello target server within your subscription.</span></span>

<span data-ttu-id="0c308-136">tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis en voer een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="0c308-136">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault, do either of hello following:</span></span>

* <span data-ttu-id="0c308-137">Azure-portal met behulp van Hallo: Ga te[beheren op lange termijn bewaren van back-up met behulp van Azure-portal Hallo](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-137">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="0c308-138">Met behulp van PowerShell: Ga te[lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-138">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="get-pricing-for-long-term-backup-retention"></a><span data-ttu-id="0c308-139">Prijzen voor lange bewaartermijn van de back-ophalen</span><span class="sxs-lookup"><span data-stu-id="0c308-139">Get pricing for long-term backup retention</span></span>

<span data-ttu-id="0c308-140">Lange bewaartermijn van back-up van een SQL-database wordt in rekening gebracht volgens toohello [Azure Backup-services prijzen tarieven](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="0c308-140">Long-term backup retention of a SQL database is charged according toohello [Azure backup services pricing rates](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="0c308-141">Nadat de Hallo SQL database-server is geregistreerd toohello kluis, worden in rekening gebracht voor Hallo totale opslag die wordt gebruikt door Hallo wekelijkse back-ups opgeslagen in de kluis Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c308-141">After hello SQL database server is registered toohello vault, you are charged for hello total storage that's used by hello weekly backups stored in hello vault.</span></span>

## <a name="view-available-backups-that-are-stored-in-long-term-backup-retention"></a><span data-ttu-id="0c308-142">Beschikbare back-ups weergeven die zijn opgeslagen in lange bewaartermijn van de back-up</span><span class="sxs-lookup"><span data-stu-id="0c308-142">View available backups that are stored in long-term backup retention</span></span>

<span data-ttu-id="0c308-143">tooconfigure, beheren, en een database herstellen via langdurig bewaren van back-up van automatische back-ups in een Azure Recovery Services-kluis via hello Azure-portal, een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="0c308-143">tooconfigure, manage, and restore a database from long-term backup retention of automated backups in an Azure Recovery Services vault by using hello Azure portal, do either of hello following:</span></span>

* <span data-ttu-id="0c308-144">Azure-portal met behulp van Hallo: Ga te[beheren op lange termijn bewaren van back-up met behulp van Azure-portal Hallo](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-144">Using hello Azure portal: Go too[Manage long-term backup retention using hello Azure portal](sql-database-long-term-backup-retention-configure.md).</span></span> 

* <span data-ttu-id="0c308-145">Met behulp van PowerShell: Ga te[lange Backup-bewaartermijn met behulp van PowerShell beheren](sql-database-long-term-backup-retention-configure.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-145">Using PowerShell: Go too[Manage long-term backup retention using PowerShell](sql-database-long-term-backup-retention-configure.md).</span></span>

## <a name="disable-long-term-retention"></a><span data-ttu-id="0c308-146">Lange bewaartermijn uitschakelen</span><span class="sxs-lookup"><span data-stu-id="0c308-146">Disable long-term retention</span></span>

<span data-ttu-id="0c308-147">Hallo-recovery-service verwerkt automatisch opschonen van back-ups op basis van opgegeven bewaarbeleid Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0c308-147">hello recovery service automatically handles hello cleanup of backups based on hello provided retention policy.</span></span> 

<span data-ttu-id="0c308-148">toostop verzenden Hallo-back-ups voor een specifieke database toohello-kluis verwijderen Hallo bewaarbeleid voor die database.</span><span class="sxs-lookup"><span data-stu-id="0c308-148">toostop sending hello backups for a specific database toohello vault, remove hello retention policy for that database.</span></span>
  
```
Set-AzureRmSqlDatabaseBackupLongTermRetentionPolicy -ResourceGroupName 'RG1' -ServerName 'Server1' -DatabaseName 'DB1' -State 'Disabled' -ResourceId $policy.Id
```

> [!NOTE]
> <span data-ttu-id="0c308-149">Hallo back-ups die zich al in de kluis Hallo worden hierdoor niet beïnvloed.</span><span class="sxs-lookup"><span data-stu-id="0c308-149">hello backups that are already in hello vault are unaffected.</span></span> <span data-ttu-id="0c308-150">Ze worden automatisch verwijderd door de herstelservice Hallo wanneer de bewaartermijn is verstreken.</span><span class="sxs-lookup"><span data-stu-id="0c308-150">They are automatically deleted by hello recovery service when their retention period expires.</span></span>

## <a name="long-term-backup-retention-faq"></a><span data-ttu-id="0c308-151">Lange bewaartermijn in back-Veelgestelde vragen</span><span class="sxs-lookup"><span data-stu-id="0c308-151">Long-term backup retention FAQ</span></span>

<span data-ttu-id="0c308-152">**Kan ik specifieke back-ups in de kluis Hallo handmatig verwijderen?**</span><span class="sxs-lookup"><span data-stu-id="0c308-152">**Can I manually delete specific backups in hello vault?**</span></span>

<span data-ttu-id="0c308-153">Momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="0c308-153">Not currently.</span></span> <span data-ttu-id="0c308-154">back-ups ruimt Hallo kluis automatisch wanneer Hallo bewaarperiode is verlopen.</span><span class="sxs-lookup"><span data-stu-id="0c308-154">hello vault automatically cleans up backups when hello retention period has expired.</span></span>

<span data-ttu-id="0c308-155">**Kan ik mijn server toostore back-ups toomore dan een kluis registreren?**</span><span class="sxs-lookup"><span data-stu-id="0c308-155">**Can I register my server toostore backups toomore than one vault?**</span></span>

<span data-ttu-id="0c308-156">U kunt een kluis voor back-ups tooonly Nee, momenteel opslaan op een tijdstip.</span><span class="sxs-lookup"><span data-stu-id="0c308-156">No, you can currently store backups tooonly one vault at a time.</span></span>

<span data-ttu-id="0c308-157">**Kan ik een kluis en de server hebben met verschillende abonnementen?**</span><span class="sxs-lookup"><span data-stu-id="0c308-157">**Can I have a vault and server in different subscriptions?**</span></span>

<span data-ttu-id="0c308-158">Nee, momenteel Hallo kluis en server moeten zich op Hallo hetzelfde abonnement en de resource-groep.</span><span class="sxs-lookup"><span data-stu-id="0c308-158">No, currently hello vault and server must be in hello same subscription and resource group.</span></span>

<span data-ttu-id="0c308-159">**Kan ik een kluis die ik in een regio die verschilt van mijn server regio gemaakt gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="0c308-159">**Can I use a vault that I created in a region that's different from my server’s region?**</span></span>

<span data-ttu-id="0c308-160">Nee, Hallo kluis en server moeten zich in Hallo dezelfde regio toominimize tijd kopiëren en te voorkomen dat verkeer kosten.</span><span class="sxs-lookup"><span data-stu-id="0c308-160">No, hello vault and server must be in hello same region toominimize copy time and avoid traffic charges.</span></span>

<span data-ttu-id="0c308-161">**Hoeveel databases kan ik opslaan in een kluis?**</span><span class="sxs-lookup"><span data-stu-id="0c308-161">**How many databases can I store in one vault?**</span></span>

<span data-ttu-id="0c308-162">Op dit moment ondersteunen we up too1, 000 databases per kluis.</span><span class="sxs-lookup"><span data-stu-id="0c308-162">Currently, we support up too1,000 databases per vault.</span></span> 

<span data-ttu-id="0c308-163">**Het aantal kluizen kan ik maken per abonnement?**</span><span class="sxs-lookup"><span data-stu-id="0c308-163">**How many vaults can I create per subscription?**</span></span>

<span data-ttu-id="0c308-164">U kunt maken van too25 kluizen per abonnement.</span><span class="sxs-lookup"><span data-stu-id="0c308-164">You can create up too25 vaults per subscription.</span></span>

<span data-ttu-id="0c308-165">**Hoeveel databases kan ik per dag per kluis configureren?**</span><span class="sxs-lookup"><span data-stu-id="0c308-165">**How many databases can I configure per day per vault?**</span></span>

<span data-ttu-id="0c308-166">U kunt 200 databases per dag per kluis instellen.</span><span class="sxs-lookup"><span data-stu-id="0c308-166">You can set up 200 databases per day per vault.</span></span>

<span data-ttu-id="0c308-167">**Werkt langdurig bewaren van back-up met elastische pools?**</span><span class="sxs-lookup"><span data-stu-id="0c308-167">**Does long-term backup retention work with elastic pools?**</span></span>

<span data-ttu-id="0c308-168">Ja.</span><span class="sxs-lookup"><span data-stu-id="0c308-168">Yes.</span></span> <span data-ttu-id="0c308-169">Elke database in de groep Hallo kan worden geconfigureerd met Hallo bewaarbeleid.</span><span class="sxs-lookup"><span data-stu-id="0c308-169">Any database in hello pool can be configured with hello retention policy.</span></span>

<span data-ttu-id="0c308-170">**Kan ik kiezen Hallo tijdstip waarop Hallo back-up is gemaakt?**</span><span class="sxs-lookup"><span data-stu-id="0c308-170">**Can I choose hello time at which hello backup is created?**</span></span>

<span data-ttu-id="0c308-171">Nee, bepaalt de SQL-Database Hallo back-upschema toominimize Hallo invloed op de prestaties van uw databases.</span><span class="sxs-lookup"><span data-stu-id="0c308-171">No, SQL Database controls hello backup schedule toominimize hello performance impact on your databases.</span></span>

<span data-ttu-id="0c308-172">**Ik heb transparante gegevensversleuteling is ingeschakeld voor de database. Kan ik deze met de kluis hello gebruiken?**</span><span class="sxs-lookup"><span data-stu-id="0c308-172">**I have transparent data encryption enabled for my database. Can I use it with hello vault?**</span></span> 

<span data-ttu-id="0c308-173">Ja, transparante gegevensversleuteling wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0c308-173">Yes, transparent data encryption is supported.</span></span> <span data-ttu-id="0c308-174">Zelfs als de oorspronkelijke database Hallo niet meer bestaat, kunt u uit de kluis Hallo Hallo-database herstellen.</span><span class="sxs-lookup"><span data-stu-id="0c308-174">You can restore hello database from hello vault even if hello original database no longer exists.</span></span>

<span data-ttu-id="0c308-175">**Wat gebeurt er met Hallo back-ups in de kluis Hallo als mijn abonnement wordt onderbroken?**</span><span class="sxs-lookup"><span data-stu-id="0c308-175">**What happens with hello backups in hello vault if my subscription is suspended?**</span></span> 

<span data-ttu-id="0c308-176">Als uw abonnement wordt onderbroken, behouden we Hallo bestaande databases en de back-ups.</span><span class="sxs-lookup"><span data-stu-id="0c308-176">If your subscription is suspended, we retain hello existing databases and backups.</span></span> <span data-ttu-id="0c308-177">Nieuwe back-ups zijn niet gekopieerd toohello kluis.</span><span class="sxs-lookup"><span data-stu-id="0c308-177">New backups are not copied toohello vault.</span></span> <span data-ttu-id="0c308-178">Nadat u Hallo abonnement opnieuw activeert, hervat Hallo service kluis voor back-ups toohello kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0c308-178">After you reactivate hello subscription, hello service resumes copying backups toohello vault.</span></span> <span data-ttu-id="0c308-179">Uw kluis wordt toegankelijk toohello herstelbewerkingen met behulp van Hallo back-ups die zijn gekopieerd er voordat het Hallo-abonnement is onderbroken.</span><span class="sxs-lookup"><span data-stu-id="0c308-179">Your vault becomes accessible toohello restore operations by using hello backups that were copied there before hello subscription was suspended.</span></span> 

<span data-ttu-id="0c308-180">**Krijg ik toegang tot toohello SQL database back-upbestanden zodat ik kan downloaden of ze toohello SQL server herstellen?**</span><span class="sxs-lookup"><span data-stu-id="0c308-180">**Can I get access toohello SQL database backup files so I can download or restore them toohello SQL server?**</span></span>

<span data-ttu-id="0c308-181">Nee, momenteel niet.</span><span class="sxs-lookup"><span data-stu-id="0c308-181">No, not currently.</span></span>

<span data-ttu-id="0c308-182">**Is het mogelijk toohave meerdere plant (dagelijks, wekelijks, maandelijks, jaarlijks) binnen een bewaarbeleid SQL.**</span><span class="sxs-lookup"><span data-stu-id="0c308-182">**Is it possible toohave multiple schedules (daily, weekly, monthly, yearly) within a SQL retention policy.**</span></span>

<span data-ttu-id="0c308-183">Nee, meerdere schema's zijn momenteel alleen beschikbaar voor back-ups van virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="0c308-183">No, multiple schedules are currently available only for virtual machine backups.</span></span>

<span data-ttu-id="0c308-184">**Wat gebeurt er als we langdurig bewaren van back-up voor een database die is een secundaire actieve geo-replicatie-database hebt ingesteld?**</span><span class="sxs-lookup"><span data-stu-id="0c308-184">**What if we set up long-term backup retention on a database that is an active geo-replication secondary database?**</span></span>

<span data-ttu-id="0c308-185">Omdat er geen back-ups op replica's onderneemt, is er momenteel geen optie voor het bewaren van de lange termijn back-up op secundaire databases.</span><span class="sxs-lookup"><span data-stu-id="0c308-185">Because we don't take backups on replicas, there is currently no option for long-term backup retention on secondary databases.</span></span> <span data-ttu-id="0c308-186">Het is echter belangrijk voor gebruikers tooset up langdurig bewaren van back-up op een secundaire actieve geo-replicatie-database om deze redenen:</span><span class="sxs-lookup"><span data-stu-id="0c308-186">However, it is important for users tooset up long-term backup retention on an active geo-replication secondary database for these reasons:</span></span>
* <span data-ttu-id="0c308-187">Wanneer een failover gebeurt en Hallo-database een primaire database wordt, duurt we een volledige back-up, namelijk geüploade toovault.</span><span class="sxs-lookup"><span data-stu-id="0c308-187">When a failover happens and hello database becomes a primary database, we take a full backup, which is uploaded toovault.</span></span>
* <span data-ttu-id="0c308-188">Er is geen extra kosten toohello klant voor het instellen van langdurig bewaren van back-up op een secundaire database.</span><span class="sxs-lookup"><span data-stu-id="0c308-188">There is no extra cost toohello customer for setting up long-term backup retention on a secondary database.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0c308-189">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0c308-189">Next steps</span></span>
<span data-ttu-id="0c308-190">Omdat de databaseback-ups voorkomen dat gegevens per ongeluk beschadigd of verwijderd, zijn ze een essentieel onderdeel van een zakelijke continuïteit en noodherstelplan.</span><span class="sxs-lookup"><span data-stu-id="0c308-190">Because database backups protect data from accidental corruption or deletion, they're an essential part of any business continuity and disaster recovery strategy.</span></span> <span data-ttu-id="0c308-191">toolearn over andere SQL-Database-oplossingen voor bedrijfscontinuïteit hello, Zie [Business continuity overview](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="0c308-191">toolearn about hello other SQL Database business-continuity solutions, see [Business continuity overview](sql-database-business-continuity.md).</span></span>
