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
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="c70ca-103">Een Azure SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="c70ca-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c70ca-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="c70ca-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="c70ca-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="c70ca-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="c70ca-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c70ca-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="c70ca-107">Deze zelfstudie wordt hello Azure portal toocreate een SQL Data Warehouse met voorbeelddatabase AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c70ca-107">This tutorial uses hello Azure portal toocreate a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c70ca-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c70ca-108">Prerequisites</span></span>
<span data-ttu-id="c70ca-109">tooget gestart, moet u de:</span><span class="sxs-lookup"><span data-stu-id="c70ca-109">tooget started, you need:</span></span>

* <span data-ttu-id="c70ca-110">**Azure-account**: Ga naar [gratis proefversie van Azure] [ Azure Free Trial] of [Azure-tegoed met MSDN] [ MSDN Azure Credits] toocreate een account.</span><span class="sxs-lookup"><span data-stu-id="c70ca-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] toocreate an account.</span></span>
* <span data-ttu-id="c70ca-111">**Azure SQL-server**: Zie [maken van een Azure SQL database met hello Azure-portal] [ Create an Azure SQL database in hello Azure portal] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c70ca-111">**Azure SQL server**:  See [Create an Azure SQL database with hello Azure portal][Create an Azure SQL database in hello Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="c70ca-112">Het maken van een SQL Data Warehouse kan een nieuwe factureerbare service tot gevolg hebben.</span><span class="sxs-lookup"><span data-stu-id="c70ca-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="c70ca-113">Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c70ca-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="c70ca-114">Een SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="c70ca-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="c70ca-115">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c70ca-115">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c70ca-116">Klik op **+ Nieuw** > **Databases** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="c70ca-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Maken](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="c70ca-118">In Hallo **SQL Data Warehouse** blade invullen Hallo-informatie die nodig is, drukt u vervolgens op toocreate 'Maken'.</span><span class="sxs-lookup"><span data-stu-id="c70ca-118">In hello **SQL Data Warehouse** blade, fill in hello information needed, then press 'Create' toocreate.</span></span>

    ![Database maken](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="c70ca-120">**Server**: we raden u aan om eerst de server te selecteren.</span><span class="sxs-lookup"><span data-stu-id="c70ca-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="c70ca-121">**Databasenaam**: Hallo-naam die is gebruikt tooreference Hallo SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c70ca-121">**Database name**: hello name that is used tooreference hello SQL Data Warehouse.</span></span>  <span data-ttu-id="c70ca-122">Het moet uniek toohello-server.</span><span class="sxs-lookup"><span data-stu-id="c70ca-122">It must be unique toohello server.</span></span>
   * <span data-ttu-id="c70ca-123">**Prestaties**: we raden u aan om te beginnen met 400 [DWU's][DWU].</span><span class="sxs-lookup"><span data-stu-id="c70ca-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="c70ca-124">U kunt verplaatsen Hallo schuifregelaar toohello links of rechts tooadjust Hallo prestaties van uw datawarehouse of schaal omhoog of omlaag na het maken.</span><span class="sxs-lookup"><span data-stu-id="c70ca-124">You can move hello slider toohello left or right tooadjust hello performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="c70ca-125">toolearn meer informatie over dwu's, Zie onze documentatie op [schalen](sql-data-warehouse-manage-compute-overview.md) of onze [pagina met prijzen][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="c70ca-125">toolearn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="c70ca-126">**Abonnement**: Selecteer Hallo [abonnement] die deze SQL Data Warehouse wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="c70ca-126">**Subscription**: Select hello [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="c70ca-127">**Resourcegroep**: [resourcegroepen] [ Resource group] zijn containers ontworpen toohelp u een verzameling Azure-resources beheren.</span><span class="sxs-lookup"><span data-stu-id="c70ca-127">**Resource group**: [Resource groups][Resource group] are containers designed toohelp you manage a collection of Azure resources.</span></span> <span data-ttu-id="c70ca-128">Meer informatie over [resourcegroepen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c70ca-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="c70ca-129">**Bron selecteren**: klik op **Bron selecteren** > **Voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="c70ca-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="c70ca-130">Azure wordt automatisch gevuld Hallo **voorbeeld selecteren** optie met AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="c70ca-130">Azure automatically populates hello **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c70ca-131">de standaardsortering Hallo voor een SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="c70ca-131">hello default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="c70ca-132">Als een andere sortering is vereist, [T-SQL] [ T-SQL] mag gebruikte toocreate Hallo database met een andere sortering.</span><span class="sxs-lookup"><span data-stu-id="c70ca-132">If a different collation is needed, [T-SQL][T-SQL] can be used toocreate hello database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="c70ca-133">Klik op **maken** toocreate uw SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c70ca-133">Click **Create** toocreate your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="c70ca-134">Wacht enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="c70ca-134">Wait for a few minutes.</span></span> <span data-ttu-id="c70ca-135">Wanneer uw datawarehouse klaar is, u moet worden geretourneerd toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c70ca-135">When your data warehouse is ready, you should be returned toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c70ca-136">U kunt uw SQL Data Warehouse vinden op uw dashboard, vermeld in de SQL-Databases of groep die u hebt gebruikt toocreate in Hallo resource deze.</span><span class="sxs-lookup"><span data-stu-id="c70ca-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in hello resource group that you used toocreate it.</span></span>

    ![portalweergave](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="c70ca-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c70ca-138">Next steps</span></span>
<span data-ttu-id="c70ca-139">Nu u een SQL Data Warehouse hebt gemaakt, bent u gereed te[Connect](sql-data-warehouse-connect-overview.md) en beginnen met het uitvoeren van query's.</span><span class="sxs-lookup"><span data-stu-id="c70ca-139">Now that you have created a SQL Data Warehouse, you are ready too[Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="c70ca-140">gegevens in SQL Data Warehouse tooload Zie Hallo [laden overzicht](sql-data-warehouse-overview-load.md).</span><span class="sxs-lookup"><span data-stu-id="c70ca-140">tooload data into SQL Data Warehouse, see hello [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="c70ca-141">Als u een bestaande database tooSQL Data Warehouse toomigrate probeert, raadpleegt u Hallo [Migratieoverzicht](sql-data-warehouse-overview-migrate.md) of gebruik [migratieprogramma](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="c70ca-141">If you are trying toomigrate an existing database tooSQL Data Warehouse, see hello [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="c70ca-142">Firewallregels kunnen ook worden geconfigureerd met behulp van Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="c70ca-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="c70ca-143">Zie [sp_set_firewall_rule][sp_set_firewall_rule] en [sp_set_database_firewall_rule][sp_set_database_firewall_rule] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c70ca-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="c70ca-144">Het is ook een goed idee toolook op Hallo [Best practices][Best practices].</span><span class="sxs-lookup"><span data-stu-id="c70ca-144">It's also a great idea toolook at hello [Best practices][Best practices].</span></span>

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
