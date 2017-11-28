---
title: Een SQL Data Warehouse maken in Azure Portal | Microsoft Docs
description: Leer hoe u een Azure SQL Data Warehouse maakt in Azure Portal
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
ms.openlocfilehash: 24ed2d8bad3090e378acf2a42fb909dee0a8517b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-azure-sql-data-warehouse"></a><span data-ttu-id="b36b0-103">Een Azure SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="b36b0-103">Create an Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b36b0-104">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="b36b0-104">Azure portal</span></span>](sql-data-warehouse-get-started-provision.md)
> * [<span data-ttu-id="b36b0-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="b36b0-105">TSQL</span></span>](sql-data-warehouse-get-started-create-database-tsql.md)
> * [<span data-ttu-id="b36b0-106">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b36b0-106">PowerShell</span></span>](sql-data-warehouse-get-started-provision-powershell.md)
>
>

<span data-ttu-id="b36b0-107">In deze zelfstudie gebruikt u Azure Portal om een SQL Data Warehouse te maken die een AdventureWorksDW-voorbeelddatabase bevat.</span><span class="sxs-lookup"><span data-stu-id="b36b0-107">This tutorial uses the Azure portal to create a SQL Data Warehouse that contains an AdventureWorksDW sample database.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b36b0-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b36b0-108">Prerequisites</span></span>
<span data-ttu-id="b36b0-109">Om aan de slag te gaan, hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="b36b0-109">To get started, you need:</span></span>

* <span data-ttu-id="b36b0-110">**Azure-account**: ga naar [Gratis proefversie van Azure][Azure Free Trial] of [Azure-tegoed met MSDN][MSDN Azure Credits] om een account te maken.</span><span class="sxs-lookup"><span data-stu-id="b36b0-110">**Azure account**: Visit [Azure Free Trial][Azure Free Trial] or [MSDN Azure Credits][MSDN Azure Credits] to create an account.</span></span>
* <span data-ttu-id="b36b0-111">**Azure SQL Server**: zie [Een Azure SQL Database met Azure Portal maken][Create an Azure SQL database in the Azure portal] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b36b0-111">**Azure SQL server**:  See [Create an Azure SQL database with the Azure portal][Create an Azure SQL database in the Azure portal] for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="b36b0-112">Het maken van een SQL Data Warehouse kan een nieuwe factureerbare service tot gevolg hebben.</span><span class="sxs-lookup"><span data-stu-id="b36b0-112">Creating a SQL Data Warehouse might result in a new billable service.</span></span>  <span data-ttu-id="b36b0-113">Zie [Prijzen van SQL Data Warehouse][SQL Data Warehouse pricing] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b36b0-113">See [SQL Data Warehouse pricing][SQL Data Warehouse pricing] for more details.</span></span>
>
>

## <a name="create-a-sql-data-warehouse"></a><span data-ttu-id="b36b0-114">Een SQL Data Warehouse maken</span><span class="sxs-lookup"><span data-stu-id="b36b0-114">Create a SQL Data Warehouse</span></span>
1. <span data-ttu-id="b36b0-115">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b36b0-115">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b36b0-116">Klik op **+ Nieuw** > **Databases** > **SQL Data Warehouse**.</span><span class="sxs-lookup"><span data-stu-id="b36b0-116">Click **+ New** > **Databases** > **SQL Data Warehouse**.</span></span>

    ![Maken](./media/sql-data-warehouse-get-started-provision/create-sample.gif)
3. <span data-ttu-id="b36b0-118">Vul op de blade **SQL Data Warehouse** de benodigde informatie in en druk op Maken.</span><span class="sxs-lookup"><span data-stu-id="b36b0-118">In the **SQL Data Warehouse** blade, fill in the information needed, then press 'Create' to create.</span></span>

    ![Database maken](./media/sql-data-warehouse-get-started-provision/create-database.png)

   * <span data-ttu-id="b36b0-120">**Server**: we raden u aan om eerst de server te selecteren.</span><span class="sxs-lookup"><span data-stu-id="b36b0-120">**Server**: We recommend you select your server first.</span></span>  
   * <span data-ttu-id="b36b0-121">**Databasenaam**: de naam die wordt gebruikt om naar de SQL Data Warehouse te verwijzen.</span><span class="sxs-lookup"><span data-stu-id="b36b0-121">**Database name**: The name that is used to reference the SQL Data Warehouse.</span></span>  <span data-ttu-id="b36b0-122">De waarde moet uniek zijn op de server.</span><span class="sxs-lookup"><span data-stu-id="b36b0-122">It must be unique to the server.</span></span>
   * <span data-ttu-id="b36b0-123">**Prestaties**: we raden u aan om te beginnen met 400 [DWU's][DWU].</span><span class="sxs-lookup"><span data-stu-id="b36b0-123">**Performance**: We recommend starting with 400 [DWUs][DWU].</span></span> <span data-ttu-id="b36b0-124">U kunt de schuifregelaar naar links of rechts bewegen om de prestaties van uw datawarehouse aan te passen, of u kunt later omhoog of omlaag schalen.</span><span class="sxs-lookup"><span data-stu-id="b36b0-124">You can move the slider to the left or right to adjust the performance of your data warehouse, or scale up or down after creation.</span></span>  <span data-ttu-id="b36b0-125">Meer informatie over DWU's vindt u in onze documentatie over [schalen](sql-data-warehouse-manage-compute-overview.md) of op onze [pagina met prijzen][SQL Data Warehouse pricing].</span><span class="sxs-lookup"><span data-stu-id="b36b0-125">To learn more about DWUs, see our documentation on [scaling](sql-data-warehouse-manage-compute-overview.md) or our [pricing page][SQL Data Warehouse pricing].</span></span>
   * <span data-ttu-id="b36b0-126">**Abonnement**: selecteer het [abonnement] waaronder deze SQL Data Warehouse wordt gefactureerd.</span><span class="sxs-lookup"><span data-stu-id="b36b0-126">**Subscription**: Select the [subscription] that this SQL Data Warehouse will bill to.</span></span>
   * <span data-ttu-id="b36b0-127">**Resourcegroep**: [resourcegroepen][Resource group] zijn containers die speciaal zijn ontworpen om u te helpen bij het beheren van een verzameling Azure-resources.</span><span class="sxs-lookup"><span data-stu-id="b36b0-127">**Resource group**: [Resource groups][Resource group] are containers designed to help you manage a collection of Azure resources.</span></span> <span data-ttu-id="b36b0-128">Meer informatie over [resourcegroepen](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b36b0-128">Learn more about [resource groups](../azure-resource-manager/resource-group-overview.md).</span></span>
   * <span data-ttu-id="b36b0-129">**Bron selecteren**: klik op **Bron selecteren** > **Voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="b36b0-129">**Select source**: Click **Select source** > **Sample**.</span></span> <span data-ttu-id="b36b0-130">Azure vult de optie **Select sample** (Selecteer voorbeeld) automatisch in met AdventureWorksDW.</span><span class="sxs-lookup"><span data-stu-id="b36b0-130">Azure automatically populates the **Select sample** option with AdventureWorksDW.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b36b0-131">De standaardsortering voor een SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span><span class="sxs-lookup"><span data-stu-id="b36b0-131">The default collation for a SQL Data Warehouse is SQL_Latin1_General_CP1_CI_AS.</span></span> <span data-ttu-id="b36b0-132">Als er een andere sortering is vereist, kan met [T-SQL][T-SQL] een andere sortering voor de database worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b36b0-132">If a different collation is needed, [T-SQL][T-SQL] can be used to create the database with a different collation.</span></span>
   >
   >

1. <span data-ttu-id="b36b0-133">Klik op **Maken** om uw SQL Data Warehouse te maken.</span><span class="sxs-lookup"><span data-stu-id="b36b0-133">Click **Create** to create your SQL Data Warehouse.</span></span>
2. <span data-ttu-id="b36b0-134">Wacht enkele minuten.</span><span class="sxs-lookup"><span data-stu-id="b36b0-134">Wait for a few minutes.</span></span> <span data-ttu-id="b36b0-135">Wanneer uw datawarehouse klaar is, keert u terug naar [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b36b0-135">When your data warehouse is ready, you should be returned to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b36b0-136">U vindt de SQL Data Warehouse op het dashboard onder de SQL-databases, of in de resourcegroep die u hebt gebruikt om deze te maken.</span><span class="sxs-lookup"><span data-stu-id="b36b0-136">You can find your SQL Data Warehouse on your dashboard, listed under your SQL Databases, or in the resource group that you used to create it.</span></span>

    ![portalweergave](./media/sql-data-warehouse-get-started-provision/database-portal-view.png)

[!INCLUDE [SQL Database create server](../../includes/sql-database-create-new-server-firewall-portal.md)]

## <a name="next-steps"></a><span data-ttu-id="b36b0-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b36b0-138">Next steps</span></span>
<span data-ttu-id="b36b0-139">Nu u een SQL Data Warehouse hebt gemaakt, kunt u [verbinding maken](sql-data-warehouse-connect-overview.md) en query's gaan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b36b0-139">Now that you have created a SQL Data Warehouse, you are ready to [Connect](sql-data-warehouse-connect-overview.md) and begin querying.</span></span>

<span data-ttu-id="b36b0-140">Zie [Loading overview](sql-data-warehouse-overview-load.md) (Laden: overzicht) als u gegevens in SQL Data Warehouse wilt laden.</span><span class="sxs-lookup"><span data-stu-id="b36b0-140">To load data into SQL Data Warehouse, see the [loading overview](sql-data-warehouse-overview-load.md).</span></span>

<span data-ttu-id="b36b0-141">Als u een bestaande database probeert te migreren naar SQL Data Warehouse, raadpleeg dan [Migration overview](sql-data-warehouse-overview-migrate.md) (Migreren: overzicht) of gebruik het [Migratieprogramma](sql-data-warehouse-migrate-migration-utility.md).</span><span class="sxs-lookup"><span data-stu-id="b36b0-141">If you are trying to migrate an existing database to SQL Data Warehouse, see the [Migration overview](sql-data-warehouse-overview-migrate.md) or use [Migration Utility](sql-data-warehouse-migrate-migration-utility.md).</span></span>

<span data-ttu-id="b36b0-142">Firewallregels kunnen ook worden geconfigureerd met behulp van Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="b36b0-142">Firewall rules can also be configured using Transact-SQL.</span></span> <span data-ttu-id="b36b0-143">Zie [sp_set_firewall_rule][sp_set_firewall_rule] en [sp_set_database_firewall_rule][sp_set_database_firewall_rule] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b36b0-143">For more information, see [sp_set_firewall_rule][sp_set_firewall_rule] and [sp_set_database_firewall_rule][sp_set_database_firewall_rule].</span></span>

<span data-ttu-id="b36b0-144">Het is ook een goed idee om te kijken naar de [Aanbevolen procedures][Best practices].</span><span class="sxs-lookup"><span data-stu-id="b36b0-144">It's also a great idea to look at the [Best practices][Best practices].</span></span>

<!--Article references-->
[Create an Azure SQL database in the Azure portal]: ../sql-database/sql-database-get-started.md
[Create an Azure SQL database with PowerShell]: ../sql-database/sql-database-create-and-configure-database-powershell
[resource groups]: ../azure-resource-manager/resource-group-template-deploy-portal.md
[Best practices]: sql-data-warehouse-best-practices.md
[DWU]: sql-data-warehouse-overview-what-is.md
<span data-ttu-id="b36b0-145">[abonnement]: ../azure-glossary-cloud-terminology.md#subscription</span><span class="sxs-lookup"><span data-stu-id="b36b0-145">[subscription]: ../azure-glossary-cloud-terminology.md#subscription</span></span>
[resource group]: ../azure-glossary-cloud-terminology.md#resource-group
[T-SQL]: ./sql-data-warehouse-get-started-create-database-tsql.md

<!--MSDN references-->
[sp_set_firewall_rule]: https://msdn.microsoft.com/library/dn270017.aspx
[sp_set_database_firewall_rule]: https://msdn.microsoft.com/library/dn270010.aspx

<!--Other Web references-->
[SQL Data Warehouse pricing]: https://azure.microsoft.com/pricing/details/sql-data-warehouse/
[Azure Free Trial]: https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F
[MSDN Azure Credits]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F
