---
title: aaaPowerShell-cmdlets voor Azure SQL Data Warehouse
description: Hallo bovenste PowerShell-cmdlets voor Azure SQL Data Warehouse vinden met inbegrip van hoe toopause en hervatten van een database.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 6f0d5772-f05f-4cc8-9749-4adb153dfd50
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: reference
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 84353b56131cf856e0724d338d7ed186fd2ceeaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-cmdlets-and-rest-apis-for-sql-data-warehouse"></a>PowerShell-cmdlets en REST-API's voor SQL Data Warehouse
Veel SQL Data Warehouse-beheertaken kunnen worden beheerd met behulp van Azure PowerShell-cmdlets of REST-API's.  Hieronder volgen enkele voorbeelden van hoe toouse PowerShell-tooautomate algemene taken in uw SQL Data Warehouse opdrachten.  Zie voor een goede voorbeelden van de REST Hallo artikel [beheren schaalbaarheid met REST][Manage scalability with REST].

> [!NOTE]
> In de volgorde toouse Azure PowerShell gebruiken met SQL Data Warehouse, moet u Azure PowerShell-versie 1.0.3 of hoger.  U kunt uw versie controleren door te voeren **Get-Module - ListAvailable-Name Azure**.  de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].
> 
> 

## <a name="get-started-with-azure-powershell-cmdlets"></a>Aan de slag met Azure PowerShell-cmdlets
1. Open Windows PowerShell.
2. Deze toosign opdrachten uitvoeren in Azure Resource Manager toohello bij Hallo PowerShell-prompt en uw abonnement te selecteren.
   
    ```PowerShell
    Login-AzureRmAccount
    Get-AzureRmSubscription
    Select-AzureRmSubscription -SubscriptionName "MySubscription"
    ```

## <a name="pause-sql-data-warehouse-example"></a>Voorbeeld van onderbreken SQL datawarehouse
Onderbreken van een database met naam 'Database02' gehost op een server met de naam "Server01."  Hallo-server zich in een Azure-resourcegroep met de naam 'ResourceGroup1'.

```Powershell
Suspend-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
```
Een variatie in dit voorbeeld doorgesluisd Hallo opgehaald object te[Suspend-AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase].  Als gevolg hiervan is Hallo-database onderbroken. de laatste opdracht Hallo toont Hallo resultaten.

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Suspend-AzureRmSqlDatabase
$resultDatabase
```

## <a name="start-sql-data-warehouse-example"></a>Start SQL datawarehouse voorbeeld
Hervatten van een database met naam 'Database02' gehost op een server met de naam "Server01." Hallo server deel uitmaakt van een resourcegroep met de naam 'ResourceGroup1'.

```Powershell
Resume-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" -DatabaseName "Database02"
```

Een variatie in dit voorbeeld haalt een database met naam 'Database02' van een server met de naam 'Server01' die is opgenomen in een resourcegroep met de naam 'ResourceGroup1'. Het object Hallo opgehaald te doorgesluisd[Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase].

```Powershell
$database = Get-AzureRmSqlDatabase –ResourceGroupName "ResourceGroup1" –ServerName "Server01" –DatabaseName "Database02"
$resultDatabase = $database | Resume-AzureRmSqlDatabase
```

> [!NOTE]
> Let op: als uw server foo.database.windows.net, "foo" gebruiken zoals Hallo - servernaam in Hallo PowerShell-cmdlets.
> 
> 

## <a name="other-supported-powershell-cmdlets"></a>Overige ondersteunde PowerShell-cmdlets
Deze PowerShell-cmdlets worden ondersteund met Azure SQL Data Warehouse.

* [Get-AzureRmSqlDatabase][Get-AzureRmSqlDatabase]
* [Get-AzureRmSqlDeletedDatabaseBackup][Get-AzureRmSqlDeletedDatabaseBackup]
* [Get-AzureRmSqlDatabaseRestorePoints][Get-AzureRmSqlDatabaseRestorePoints]
* [Nieuwe AzureRmSqlDatabase][New-AzureRmSqlDatabase]
* [Verwijder AzureRmSqlDatabase][Remove-AzureRmSqlDatabase]
* [Restore-AzureRmSqlDatabase][Restore-AzureRmSqlDatabase]
* [Resume-AzureRmSqlDatabase][Resume-AzureRmSqlDatabase]
* [SELECT-AzureRmSubscription][Select-AzureRmSubscription]
* [Set-AzureRmSqlDatabase][Set-AzureRmSqlDatabase]
* [Onderbreken AzureRmSqlDatabase][Suspend-AzureRmSqlDatabase]

## <a name="next-steps"></a>Volgende stappen
Zie voor meer voorbeelden van PowerShell:

* [Maken van een SQL Data Warehouse met behulp van PowerShell][Create a SQL Data Warehouse using PowerShell]
* [Database terugzetten][Database restore]

Zie voor andere taken die kunnen worden geautomatiseerd met PowerShell [Azure SQL Database-Cmdlets][Azure SQL Database Cmdlets]. Houd er rekening mee dat niet alle Azure SQL Database-cmdlets voor Azure SQL Data Warehouse worden ondersteund.  Zie voor een lijst van taken die kan worden geautomatiseerd met REST [bewerkingen voor Azure SQL-Databases][Operations for Azure SQL Databases].

<!--Image references-->

<!--Article references-->
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Create a SQL Data Warehouse using PowerShell]: ./sql-data-warehouse-get-started-provision-powershell.md
[Database restore]: ./sql-data-warehouse-restore-database-powershell.md
[Manage scalability with REST]: ./sql-data-warehouse-manage-compute-rest-api.md

<!--MSDN references-->
[Azure SQL Database Cmdlets]: https://msdn.microsoft.com/library/mt574084.aspx
[Operations for Azure SQL Databases]: https://msdn.microsoft.com/library/azure/dn505719.aspx
[Get-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt603648.aspx
[Get-AzureRmSqlDeletedDatabaseBackup]: https://msdn.microsoft.com/library/mt693387.aspx
[Get-AzureRmSqlDatabaseRestorePoints]: https://msdn.microsoft.com/library/mt603642.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Remove-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619368.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx
[Resume-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619347.aspx
<!-- It appears that Select-AzureRmSubscription isn't documented, so this points tooSelect-AzureSubscription -->
[Select-AzureRmSubscription]: https://msdn.microsoft.com/library/dn722499.aspx
[Set-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619433.aspx
[Suspend-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619337.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
