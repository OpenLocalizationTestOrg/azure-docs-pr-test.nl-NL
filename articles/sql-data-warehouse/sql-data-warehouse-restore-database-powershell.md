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
# <a name="restore-an-azure-sql-data-warehouse-powershell"></a>Herstellen van een Azure SQL datawarehouse (PowerShell)
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

In dit artikel leert u hoe toorestore een Azure SQL Data Warehouse met behulp van PowerShell.

## <a name="before-you-begin"></a>Voordat u begint
**Controleer of de capaciteit van de DTU.** Elke SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) met een standaard DTU-quotum.  Voordat u een SQL Data Warehouse herstelt kunt, te controleren die Hallo die uw SQL-server heeft onvoldoende resterende DTU-quotum voor Hallo-database wordt hersteld. toolearn hoe toocalculate DTU overbodig of toorequest meer DTU Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].

### <a name="install-powershell"></a>PowerShell installeren
In de volgorde toouse Azure PowerShell gebruiken met SQL Data Warehouse moet u tooinstall Azure PowerShell-versie 1.0 of hoger.  U kunt uw versie controleren door te voeren **Get-Module - ListAvailable-Name AzureRM**.  de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].

## <a name="restore-an-active-or-paused-database"></a>Herstel de database van een actieve of onderbroken
een database van een momentopname toorestore gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] PowerShell-cmdlet.

1. Open Windows PowerShell.
2. Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.
3. Selecteer Hallo-abonnement met Hallo database toobe hersteld.
4. Lijst Hallo herstelpunten voor Hallo-database.
5. Kies Hallo gewenst herstelpunt Hallo RestorePointCreationDate gebruiken.
6. Hallo database toohello gewenst herstelpunt herstellen.
7. Controleer of Hallo hersteld database online is.

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
> Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Een verwijderde database herstellen
een verwijderde database toorestore gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Open Windows PowerShell.
2. Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.
3. Selecteer Hallo-abonnement met Hallo verwijderd database toobe hersteld.
4. Hallo specifieke verwijderd database ophalen.
5. Hallo verwijderde database herstellen.
6. Controleer of Hallo hersteld database online is.

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
> Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].
> 
> 

## <a name="restore-from-an-azure-geographical-region"></a>Herstellen van een Azure-geografische regio
een database toorecover gebruiken Hallo [Restore-AzureRmSqlDatabase] [ Restore-AzureRmSqlDatabase] cmdlet.

1. Open Windows PowerShell.
2. Verbind tooyour Azure-account en lijst van alle Hallo abonnementen die zijn gekoppeld aan uw account.
3. Selecteer Hallo-abonnement met Hallo database toobe hersteld.
4. Hallo-database die u wilt dat toorecover ophalen.
5. Aanvraag voor het herstel voor database Hallo Hallo maken.
6. Controleer of Hallo status van Hallo geo herstelde database.

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
> tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].
> 
> 

Hallo herstelde database zal worden ingeschakeld voor TDE als Hallo brondatabase TDE ingeschakeld.

## <a name="next-steps"></a>Volgende stappen
Lees Hallo toolearn over Hallo zakelijke continuïteit functies van Azure SQL Database-edities [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].

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
