---
title: aaaRestore een Azure SQL Data Warehouse (PowerShell) | Microsoft Docs
description: PowerShell-taken voor het herstellen van een Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: ac62f154-c8b0-4c33-9c42-f480808aa1d2
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: aa29a315080b1ed477cc6a051ce15a3202630cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a><span data-ttu-id="d35b7-103">Herstellen van een Azure SQL datawarehouse (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="d35b7-103">Restore an Azure SQL Data Warehouse (PowerShell)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d35b7-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="d35b7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d35b7-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="d35b7-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="d35b7-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="d35b7-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="d35b7-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="d35b7-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="d35b7-108">In dit artikel leert u hoe toorestore een Azure SQL Data Warehouse met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d35b7-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using PowerShell.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d35b7-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d35b7-109">Before you begin</span></span>
<span data-ttu-id="d35b7-110">**Controleer of de capaciteit van de DTU.**</span><span class="sxs-lookup"><span data-stu-id="d35b7-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="d35b7-111">Elke SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) met een standaard DTU-quotum.</span><span class="sxs-lookup"><span data-stu-id="d35b7-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="d35b7-112">Voordat u een SQL Data Warehouse herstelt kunt, te controleren die Hallo die uw SQL-server heeft onvoldoende resterende DTU-quotum voor Hallo-database wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="d35b7-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="d35b7-113">toolearn hoe toocalculate DTU overbodig of toorequest meer DTU Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="d35b7-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

### <a name="install-powershell"></a><span data-ttu-id="d35b7-114">PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="d35b7-114">Install PowerShell</span></span>
<span data-ttu-id="d35b7-115">In de volgorde toouse Azure PowerShell gebruiken met SQL Data Warehouse moet u tooinstall Azure PowerShell-versie 1.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d35b7-115">In order toouse Azure PowerShell with SQL Data Warehouse, you will need tooinstall Azure PowerShell version 1.0 or greater.</span></span>  <span data-ttu-id="d35b7-116">U kunt uw versie controleren door te voeren **Get-Module - ListAvailable-Name AzureRM**.</span><span class="sxs-lookup"><span data-stu-id="d35b7-116">You can check your version by running **Get-Module -ListAvailable -Name AzureRM**.</span></span>  <span data-ttu-id="d35b7-117">de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="d35b7-117">hello latest version can be installed from  [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>  <span data-ttu-id="d35b7-118">Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].</span><span class="sxs-lookup"><span data-stu-id="d35b7-118">For more information on installing hello latest version, see [How tooinstall and configure Azure PowerShell][How tooinstall and configure Azure PowerShell].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="d35b7-119">Herstel de database van een actieve of onderbroken</span><span class="sxs-lookup"><span data-stu-id="d35b7-119">Restore an active or paused database</span></span>
<span data-ttu-id="d35b7-120">een database van een momentopname toorestore gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell-cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d35b7-120">toorestore a database from a snapshot use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] PowerShell cmdlet.</span></span>

1. <span data-ttu-id="d35b7-121">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d35b7-121">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="d35b7-122">Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="d35b7-122">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="d35b7-123">Selecteer Hallo-abonnement met Hallo database toobe hersteld.</span><span class="sxs-lookup"><span data-stu-id="d35b7-123">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="d35b7-124">Lijst Hallo herstelpunten voor Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="d35b7-124">List hello restore points for hello database.</span></span>
5. <span data-ttu-id="d35b7-125">Kies Hallo gewenst herstelpunt Hallo RestorePointCreationDate gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d35b7-125">Pick hello desired restore point using hello RestorePointCreationDate.</span></span>
6. <span data-ttu-id="d35b7-126">Hallo database toohello gewenst herstelpunt herstellen.</span><span class="sxs-lookup"><span data-stu-id="d35b7-126">Restore hello database toohello desired restore point.</span></span>
7. <span data-ttu-id="d35b7-127">Controleer of Hallo hersteld database online is.</span><span class="sxs-lookup"><span data-stu-id="d35b7-127">Verify that hello restored database is online.</span></span>

```Powershell

$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# List hello last 10 database restore points
((Get-AzureRMSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName ($DatabaseName).RestorePointCreationDate)[-10 .. -1]

# Or list all restore points
Get-AzureRmSqlDatabaseRestorePoints -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Get hello specific database toorestore
$Database = Get-AzureRmSqlDatabase -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Pick desired restore point using RestorePointCreationDate
$PointInTime="<RestorePointCreationDate>"  

# Restore database from a restore point
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromPointInTimeBackup –PointInTime $PointInTime -ResourceGroupName $Database.ResourceGroupName -ServerName $Database.$ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $Database.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status

```

> [!NOTE]
> <span data-ttu-id="d35b7-128">Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d35b7-128">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="d35b7-129">Een verwijderde database herstellen</span><span class="sxs-lookup"><span data-stu-id="d35b7-129">Restore a deleted database</span></span>
<span data-ttu-id="d35b7-130">een verwijderde database toorestore gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d35b7-130">toorestore a deleted database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="d35b7-131">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d35b7-131">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="d35b7-132">Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="d35b7-132">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="d35b7-133">Selecteer Hallo-abonnement met Hallo verwijderd database toobe hersteld.</span><span class="sxs-lookup"><span data-stu-id="d35b7-133">Select hello subscription that contains hello deleted database toobe restored.</span></span>
4. <span data-ttu-id="d35b7-134">Hallo specifieke verwijderd database ophalen.</span><span class="sxs-lookup"><span data-stu-id="d35b7-134">Get hello specific deleted database.</span></span>
5. <span data-ttu-id="d35b7-135">Hallo verwijderde database herstellen.</span><span class="sxs-lookup"><span data-stu-id="d35b7-135">Restore hello deleted database.</span></span>
6. <span data-ttu-id="d35b7-136">Controleer of Hallo hersteld database online is.</span><span class="sxs-lookup"><span data-stu-id="d35b7-136">Verify that hello restored database is online.</span></span>

```Powershell
$SubscriptionName="<YourSubscriptionName>"
$ResourceGroupName="<YourResourceGroupName>"
$ServerName="<YourServerNameWithoutURLSuffixSeeNote>"  # Without database.windows.net
$DatabaseName="<YourDatabaseName>"
$NewDatabaseName="<YourDatabaseName>"

Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

# Get hello deleted database toorestore
$DeletedDatabase = Get-AzureRmSqlDeletedDatabaseBackup -ResourceGroupName $ResourceGroupName -ServerName $ServerName -DatabaseName $DatabaseName

# Restore deleted database
$RestoredDatabase = Restore-AzureRmSqlDatabase –FromDeletedDatabaseBackup –DeletionDate $DeletedDatabase.DeletionDate -ResourceGroupName $DeletedDatabase.ResourceGroupName -ServerName $DeletedDatabase.ServerName -TargetDatabaseName $NewDatabaseName –ResourceId $DeletedDatabase.ResourceID

# Verify hello status of restored database
$RestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="d35b7-137">Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d35b7-137">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a><span data-ttu-id="d35b7-138">Herstellen van een Azure-geografische regio</span><span class="sxs-lookup"><span data-stu-id="d35b7-138">Restore from an Azure geographical region</span></span>
<span data-ttu-id="d35b7-139">een database toorecover gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d35b7-139">toorecover a database, use hello [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase] cmdlet.</span></span>

1. <span data-ttu-id="d35b7-140">Open Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d35b7-140">Open Windows PowerShell.</span></span>
2. <span data-ttu-id="d35b7-141">Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="d35b7-141">Connect tooyour Azure account and list all hello subscriptions associated with your account.</span></span>
3. <span data-ttu-id="d35b7-142">Selecteer Hallo-abonnement met Hallo database toobe hersteld.</span><span class="sxs-lookup"><span data-stu-id="d35b7-142">Select hello subscription that contains hello database toobe restored.</span></span>
4. <span data-ttu-id="d35b7-143">Hallo-database die u wilt dat toorecover ophalen.</span><span class="sxs-lookup"><span data-stu-id="d35b7-143">Get hello database you want toorecover.</span></span>
5. <span data-ttu-id="d35b7-144">Aanvraag voor het herstel voor database Hallo Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="d35b7-144">Create hello recovery request for hello database.</span></span>
6. <span data-ttu-id="d35b7-145">Controleer of Hallo status van Hallo geo herstelde database.</span><span class="sxs-lookup"><span data-stu-id="d35b7-145">Verify hello status of hello geo-restored database.</span></span>

```Powershell
Login-AzureRmAccount
Get-AzureRmSubscription
Select-AzureRmSubscription -SubscriptionName "<Subscription_name>"

# Get hello database you want toorecover
$GeoBackup = Get-AzureRmSqlDatabaseGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourServerName>" -DatabaseName "<YourDatabaseName>"

# Recover database
$GeoRestoredDatabase = Restore-AzureRmSqlDatabase –FromGeoBackup -ResourceGroupName "<YourResourceGroupName>" -ServerName "<YourTargetServer>" -TargetDatabaseName "<NewDatabaseName>" –ResourceId $GeoBackup.ResourceID

# Verify that hello geo-restored database is online
$GeoRestoredDatabase.status
```

> [!NOTE]
> <span data-ttu-id="d35b7-146">tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d35b7-146">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

<span data-ttu-id="d35b7-147">Hallo herstelde database zal worden ingeschakeld voor TDE als Hallo brondatabase TDE ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d35b7-147">hello recovered database will be TDE-enabled if hello source database is TDE-enabled.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d35b7-148">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d35b7-148">Next steps</span></span>
<span data-ttu-id="d35b7-149">Lees Hallo toolearn over Hallo zakelijke continuïteit functies van Azure SQL Database-edities [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="d35b7-149">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery

<!--MSDN references-->
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
