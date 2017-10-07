---
title: aaaCreate SQL Data Warehouse met behulp van PowerShell | Microsoft Docs
description: SQL Data Warehouse maken met Powershell
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 97434863-7938-4129-8949-5a119f5949e3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: d8af29ec285a11285785ab5474e4dfc8c36bc3ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-sql-data-warehouse-using-powershell"></a>SQL Data Warehouse maken met PowerShell
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Dit artikel laat zien hoe toocreate een SQL Data Warehouse met behulp van PowerShell.

## <a name="prerequisites"></a>Vereisten
tooget gestart, moet u de:

* **Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.
* **Azure SQL-server**: Zie [maken van een Azure SQL database in Azure Portal Hallo] [ Create an Azure SQL database in hello Azure Portal] of [een Azure SQL database maken met PowerShell] [ Create an Azure SQL database with PowerShell] voor meer informatie.
* **Resourcegroep**: gebruik Hallo dezelfde resource groeperen als uw Azure SQL-server of Zie [hoe toocreate een resourcegroep](../azure-resource-manager/resource-group-portal.md).
* **PowerShell-versie 1.0.3 of hoger**: u kunt uw versie controleren door **Get-Module - ListAvailable-Name Azure** uit te voeren.  de meest recente versie Hallo kan worden geïnstalleerd vanaf [Microsoft Web Platform Installer][Microsoft Web Platform Installer].  Zie voor meer informatie over het installeren van de meest recente versie Hallo [hoe tooinstall en configureren van Azure PowerShell][How tooinstall and configure Azure PowerShell].

> [!NOTE]
> Het maken van een SQL Data Warehouse kan leiden tot een nieuwe factureerbare service.  Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie over prijzen.
>
>

## <a name="create-a-sql-data-warehouse"></a>Een SQL Data Warehouse maken
1. Open Windows PowerShell.
2. Deze cmdlet toologin tooAzure Resource Manager worden uitgevoerd.

    ```Powershell
    Login-AzureRmAccount
    ```
3. Selecteer het gewenste toouse voor de huidige sessie Hallo-abonnement.

    ```Powershell
    Get-AzureRmSubscription    -SubscriptionName "MySubscription" | Select-AzureRmSubscription
    ```
4. Maak database. In dit voorbeeld maakt een database met naam 'mynewsqldw' met servicedoelstellingsniveau 'DW400' toohello server met de naam 'sqldwserver1', dat zich in Hallo resourcegroep 'mywesteuroperesgp1 bevindt'.

   ```Powershell
   New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW400" -DatabaseName "mynewsqldw" -ServerName "sqldwserver1" -ResourceGroupName "mywesteuroperesgp1" -Edition "DataWarehouse" -CollationName "SQL_Latin1_General_CP1_CI_AS" -MaxSizeBytes 10995116277760
   ```

De vereiste parameters zijn:

* **RequestedServiceObjectiveName**: Hallo hoeveelheid [DWU] [ DWU] u hebt aangevraagd.  De ondersteunde waarden zijn: DW100, DW200, DW300, DW400, DW500, DW600, DW1000, DW1200, DW1500, DW2000, DW3000 en DW6000.
* **DatabaseName**: naam Hallo Hallo SQL Data Warehouse die u maakt.
* **ServerName**: Hallo-naam van Hallo-server die u gebruikt voor het maken van (moet V12 zijn).
* **ResourceGroupName**: de resourcegroep die u gebruikt.  toofind beschikbare resourcegroepen in uw abonnement gebruik Get-AzureResource.
* **Editie**: moet 'DataWarehouse' toocreate een SQL Data Warehouse.

De optionele parameters zijn:

* **CollationName**: Hallo standaardsortering als niet wordt opgegeven is SQL_Latin1_General_CP1_CI_AS.  De sortering kan niet worden gewijzigd voor een database.
* **MaxSizeBytes**: Hallo standaard maximale grootte van een database is 10 GB.

Zie voor meer informatie over de parameteropties Hallo [New-AzureRmSqlDatabase] [ New-AzureRmSqlDatabase] en [Create Database (Azure SQL Data Warehouse)][Create Database (Azure SQL Data Warehouse)].

## <a name="next-steps"></a>Volgende stappen
Nadat uw SQL Data Warehouse is voltooid de inrichting dat u wilt maken van tootry [voorbeeldgegevens te laden] [ loading sample data] of te zoeken over[ontwikkelen] [ develop] , [laden][load], of [migreren][migrate].

Als u geïnteresseerd bent in meer informatie over het artikel over het toomanage SQL Data Warehouse programmatisch uitchecken toouse [PowerShell-cmdlets en REST API's][PowerShell cmdlets and REST APIs].

<!--Image references-->

<!--Article references-->
[DWU]: ./sql-data-warehouse-overview-what-is.md
[migrate]: ./sql-data-warehouse-overview-migrate.md
[develop]: ./sql-data-warehouse-overview-develop.md
[load]: ./sql-data-warehouse-load-with-bcp.md
[loading sample data]: ./sql-data-warehouse-load-sample-databases.md
[PowerShell cmdlets and REST APIs]: ./sql-data-warehouse-reference-powershell-cmdlets.md
[firewall rules]: ../sql-database-configure-firewall-settings.md

[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[how toocreate a SQL Data Warehouse from hello Azure Portal]: ./sql-data-warehouse-get-started-provision.md
[Create an Azure SQL database in hello Azure Portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-get-started-powershell.md
[how toocreate a resource group]: ../azure-resource-manager/resource-group-template-deploy-portal.md#create-resource-group

<!--MSDN references-->
[MSDN]: https://msdn.microsoft.com/library/azure/dn546722.aspx
[New-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt619339.aspx
[Create Database (Azure SQL Data Warehouse)]: https://msdn.microsoft.com/library/mt204021.aspx

<!--Other Web references-->
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
