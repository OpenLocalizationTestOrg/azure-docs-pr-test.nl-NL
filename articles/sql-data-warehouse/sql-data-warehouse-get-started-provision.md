---
title: een SQL Data Warehouse in hello Azure-portal aaaCreate | Microsoft Docs
description: Meer informatie over hoe toocreate een Azure SQL Data Warehouse in hello Azure-portal
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
tags: azure-sql-data-warehouse
ms.assetid: 552e496e-d560-419c-9996-6bbc80c521cb
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: create
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: f5be6e3f2936e3af9d099854a468f8ce66fd8fbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a>Een Azure SQL Data Warehouse maken
> [!div class="op_single_selector"]
> * [Azure Portal](sql-data-warehouse-get-started-provision.md)
> * [TSQL](sql-data-warehouse-get-started-create-database-tsql.md)
> * [PowerShell](sql-data-warehouse-get-started-provision-powershell.md)
>
>

Deze zelfstudie wordt hello Azure portal toocreate een SQL Data Warehouse met voorbeelddatabase AdventureWorksDW.

## <a name="prerequisites"></a>Vereisten
tooget gestart, moet u de:

* **Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.
* **Azure SQL-server**: Zie [maken van een Azure SQL database met hello Azure-portal] [ Create an Azure SQL database in hello Azure portal] voor meer informatie.

> [!NOTE]
> Het maken van een SQL Data Warehouse kan een nieuwe factureerbare service tot gevolg hebben.  Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie.
>
>

## <a name="create-a-sql-data-warehouse"></a>Een SQL Data Warehouse maken
1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op **+ Nieuw** > **Databases** > **SQL Data Warehouse**.

    ![Maken](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. In Hallo **SQL Data Warehouse** blade invullen Hallo-informatie die nodig is, drukt u vervolgens op toocreate 'Maken'.

    ![Database maken](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * **Server**: we raden u aan om eerst de server te selecteren.  
   * **Databasenaam**: Hallo-naam die is gebruikt tooreference Hallo SQL Data Warehouse.  Het moet uniek toohello-server.
   * **Prestaties**: we raden u aan om te beginnen met 400 [DWU's][DWU]. U kunt verplaatsen Hallo schuifregelaar toohello links of rechts tooadjust Hallo prestaties van uw datawarehouse of schaal omhoog of omlaag na het maken.  toolearn meer informatie over dwu's, Zie onze documentatie op [schalen](sql-data-warehouse-manage-compute-overview.md) of onze [pagina met prijzen][SQL Data Warehouse pricing].
   * **Abonnement**: Selecteer Hallo [abonnement] die deze SQL Data Warehouse wordt gefactureerd.
   * **Resourcegroep**: [resourcegroepen] [ Resource group] zijn containers ontworpen toohelp u een verzameling Azure-resources beheren. Meer informatie over [resourcegroepen](../azure-resource-manager/resource-group-overview.md).
   * **Bron selecteren**: klik op **Bron selecteren** > **Voorbeeld**. Azure wordt automatisch gevuld Hallo **voorbeeld selecteren** optie met AdventureWorksDW.

   > [!NOTE]
   > de standaardsortering Hallo voor een SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS. Als een andere sortering is vereist, [T-SQL] [ T-SQL] mag gebruikte toocreate Hallo database met een andere sortering.
   >
   >

1. Klik op **maken** toocreate uw SQL Data Warehouse.
2. Wacht enkele minuten. Wanneer uw datawarehouse klaar is, u moet worden geretourneerd toohello [Azure-portal](https://portal.azure.com). U kunt uw SQL Data Warehouse vinden op uw dashboard, vermeld in de SQL-Databases of groep die u hebt gebruikt toocreate in Hallo resource deze.

    ![portalweergave](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a>Volgende stappen
Nu u een SQL Data Warehouse hebt gemaakt, bent u gereed te[Connect](sql-data-warehouse-connect-overview.md) en beginnen met het uitvoeren van query's.

gegevens in SQL Data Warehouse tooload Zie Hallo [laden overzicht](sql-data-warehouse-overview-load.md).

Als u een bestaande database tooSQL Data Warehouse toomigrate probeert, raadpleegt u Hallo [Migratieoverzicht](sql-data-warehouse-overview-migrate.md) of gebruik [migratieprogramma](sql-data-warehouse-migrate-migration-utility.md).

Firewallregels kunnen ook worden geconfigureerd met behulp van Transact-SQL. Zie [sp_set_firewall_rule][sp_set_firewall_rule] en [sp_set_database_firewall_rule][sp_set_database_firewall_rule] voor meer informatie.

Het is ook een goed idee toolook op Hallo [Best practices][Best practices].

<!--Article references-->
[Create an Azure SQL database in hello Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
[abonnement]: ../azure-glossary-cloud-terminology.md#subscription
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
