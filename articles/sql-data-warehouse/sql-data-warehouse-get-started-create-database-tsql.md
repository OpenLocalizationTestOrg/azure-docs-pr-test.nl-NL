---
title: aaaCreate een SQL Data Warehouse met TSQL | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure SQL Data Warehouse met TSQL
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: a4e2e68e-aa9c-4dd3-abb0-f7df997d237a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: 81ef59a66c61452ff8a2aca29837f155e87d017d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-sql-data-warehouse-database-by-using-transact-sql-tsql"></a>Een SQL Data Warehouse-database maken met behulp van Transact-SQL (TSQL)
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Dit artikel laat zien hoe toocreate een SQL Data Warehouse met T-SQL.

## <a name="prerequisites"></a>Vereisten
tooget gestart, moet u de:

* **Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.
* **Azure SQL-server**: Zie [maken een logische Azure SQL Database-server met hello Azure Portal] [maken van een logische Azure SQL Database-server met hello Azure Portal] of [maken van een logische Azure SQL Database-server met PowerShell] [maken van een SQL Azure Database-logische server met PowerShell] voor meer informatie.
* **Resourcegroep**: gebruik Hallo dezelfde resource groeperen als uw Azure SQL-server of Zie [hoe toocreate een resourcegroep][how toocreate a resource group].
* **Omgeving tooexecute T-SQL**: U kunt [Visual Studio][Installing Visual Studio and SSDT], [sqlcmd][sqlcmd], of [SSMS] [ SSMS] tooexecute T-SQL.

> [!NOTE]
> Het maken van een SQL Data Warehouse kan leiden tot een nieuwe factureerbare service.  Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie over prijzen.
>
>

## <a name="create-a-database-with-visual-studio"></a>Een database maken met Visual Studio
Als u nieuwe tooVisual Studio, Zie Hallo artikel [Query Azure SQL Data Warehouse (Visual Studio)][Query Azure SQL Data Warehouse (Visual Studio)].  toostart, opent u SQL Server-Objectverkenner in Visual Studio en maak verbinding toohello-server die als host voor uw SQL Data Warehouse-database fungeert.  Eenmaal zijn verbonden, kunt u een SQL Data Warehouse maken door het uitvoeren van de volgende SQL-opdracht tegen Hallo Hallo **master** database.  Deze opdracht Hallo database MySqlDwDb gemaakt met een Serviceniveaudoelstelling van DW400 en Hallo database toogrow tooa maximale grootte van 10 TB toestaan.

```sql
CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB);
```

## <a name="create-a-database-with-sqlcmd"></a>Een database maken met sqlcmd
U kunt ook uitvoeren Hallo dezelfde opdracht met sqlcmd door te voeren Hallo bij een opdrachtprompt te volgen.

```sql
sqlcmd -S <Server Name>.database.windows.net -I -U <User> -P <Password> -Q "CREATE DATABASE MySqlDwDb COLLATE SQL_Latin1_General_CP1_CI_AS (EDITION='datawarehouse', SERVICE_OBJECTIVE = 'DW400', MAXSIZE= 10240 GB)"
```

Hallo standaardsortering als niet is opgegeven is COLLATE SQL_Latin1_General_CP1_CI_AS.  Hallo `MAXSIZE` mag tussen 250 GB en 240 TB.  Hallo `SERVICE_OBJECTIVE` mag tussen DW100 en dw2000 zijn [DWU][DWU].  Zie voor een lijst van alle geldige waarden Hallo MSDN-documentatie voor [CREATE DATABASE][CREATE DATABASE].  Zowel Hallo MAXSIZE en SERVICE_OBJECTIVE kunnen worden gewijzigd met een [ALTER DATABASE] [ ALTER DATABASE] T-SQL-opdracht.  Hallo-sortering van een database kan niet worden gewijzigd nadat de is gemaakt.   Waarschuwing moet worden gebruikt als veranderende Hallo SERVICE_OBJECTIVE als DWU gewijzigd zorgt ervoor dat het opnieuw opstarten van services, die alle query's tijdens de vlucht annuleert.  Voor een verandering van MAXSIZE hoeven services niet opnieuw te worden gestart, omdat dit een eenvoudige metagegevensbewerking is.

## <a name="next-steps"></a>Volgende stappen
Nadat uw SQL Data Warehouse is voltooid, u kunt inrichting [voorbeeldgegevens laden] [ load sample data] of te zoeken over[ontwikkelen][develop], [laden][load], of [migreren][migrate].

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[how toocreate a SQL Data Warehouse from hello Azure portal]: sql-data-warehouse-get-started-provision.md
[Query Azure SQL Data Warehouse (Visual Studio)]: sql-data-warehouse-query-visual-studio.md
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[load sample data]: sql-data-warehouse-load-sample-databases.md
[Create an Azure SQL database with hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group
[Installing Visual Studio and SSDT]: sql-data-warehouse-install-visual-studio.md
[sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--MSDN references-->
[CREATE DATABASE]: https://msdn.microsoft.com/library/mt204021.aspx
[ALTER DATABASE]: https://msdn.microsoft.com/library/mt204042.aspx
[SSMS]: https://msdn.microsoft.com/library/mt238290.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
