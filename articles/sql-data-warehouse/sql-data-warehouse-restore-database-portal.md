---
title: Herstellen van Azure SQL Data Warehouse (Azure-portal) | Microsoft Docs
description: Azure portal taken voor het herstellen van Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="a0644-103">Herstellen van Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="a0644-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="a0644-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="a0644-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="a0644-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="a0644-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="a0644-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="a0644-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="a0644-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="a0644-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="a0644-108">In dit artikel leert u hoe u Azure SQL Data Warehouse herstelt met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="a0644-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="a0644-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="a0644-109">Before you begin</span></span>
<span data-ttu-id="a0644-110">**Controleer of de capaciteit van de DTU.**</span><span class="sxs-lookup"><span data-stu-id="a0644-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="a0644-111">Elk exemplaar van SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) waarvoor een standaardquotum gegevensdoorvoer unit (DTU).</span><span class="sxs-lookup"><span data-stu-id="a0644-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="a0644-112">Voordat u SQL Data Warehouse herstellen kunt, Controleer of uw SQL server onvoldoende resterende DTU-quotum voor de database die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="a0644-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="a0644-113">Zie voor meer informatie over het DTU-quotum berekenen of dat er meer dtu's, [een wijziging DTU-quotum aanvragen][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="a0644-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="a0644-114">Herstel de database van een actieve of onderbroken</span><span class="sxs-lookup"><span data-stu-id="a0644-114">Restore an active or paused database</span></span>
<span data-ttu-id="a0644-115">Een database te herstellen:</span><span class="sxs-lookup"><span data-stu-id="a0644-115">To restore a database:</span></span>

1. <span data-ttu-id="a0644-116">Meld u aan bij [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a0644-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a0644-117">Selecteer in het linkerdeelvenster **Bladeren**, en selecteer vervolgens **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="a0644-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="a0644-119">Zoek uw server en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="a0644-119">Find your server, and then select it.</span></span>

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="a0644-121">Zoek het exemplaar van SQL Data Warehouse die u herstellen wilt uit en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="a0644-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Selecteer het exemplaar van SQL Data Warehouse herstellen](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="a0644-123">Selecteer boven aan de blade Data Warehouse **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="a0644-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Selecteer herstellen](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="a0644-125">Geef een nieuwe **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="a0644-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="a0644-126">Selecteer de meest recente **herstelpunt**.</span><span class="sxs-lookup"><span data-stu-id="a0644-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="a0644-127">Zorg ervoor dat u de meest recente herstelpunt kiezen.</span><span class="sxs-lookup"><span data-stu-id="a0644-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="a0644-128">Omdat herstelpunten worden weergegeven in Coordinated Universal Time (UTC), is de standaardoptie mogelijk niet de meest recente herstelpunt.</span><span class="sxs-lookup"><span data-stu-id="a0644-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Selecteer een herstelpunt](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="a0644-130">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0644-130">Select **OK**.</span></span>
9. <span data-ttu-id="a0644-131">Het proces van de database herstellen wordt gestart en u kunt **meldingen** om het proces te bewaken.</span><span class="sxs-lookup"><span data-stu-id="a0644-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="a0644-132">Nadat het herstel is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a0644-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="a0644-133">Een verwijderde database herstellen</span><span class="sxs-lookup"><span data-stu-id="a0644-133">Restore a deleted database</span></span>
<span data-ttu-id="a0644-134">Een verwijderde database herstellen:</span><span class="sxs-lookup"><span data-stu-id="a0644-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="a0644-135">Meld u aan bij [Azure Portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="a0644-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="a0644-136">Selecteer in het linkerdeelvenster **Bladeren**, en selecteer vervolgens **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="a0644-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="a0644-138">Zoek uw server en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="a0644-138">Find your server, and then select it.</span></span>

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="a0644-140">Schuif omlaag naar de **Operations** sectie op de blade van uw server.</span><span class="sxs-lookup"><span data-stu-id="a0644-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="a0644-141">Selecteer de **databases verwijderd** tegel.</span><span class="sxs-lookup"><span data-stu-id="a0644-141">Select the **Deleted databases** tile.</span></span>

    ![Selecteer de verwijderde databases tegel](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="a0644-143">Selecteer de verwijderde database die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="a0644-143">Select the deleted database that you want to restore.</span></span>

    ![Selecteer een database herstellen](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="a0644-145">Geef een nieuwe **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="a0644-145">Specify a new **Database name**.</span></span>

    ![Voeg een naam voor de database](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="a0644-147">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="a0644-147">Select **OK**.</span></span>
9. <span data-ttu-id="a0644-148">Het proces van de database herstellen wordt gestart en u kunt **meldingen** om het proces te bewaken.</span><span class="sxs-lookup"><span data-stu-id="a0644-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="a0644-149">Voor het configureren van uw database nadat het herstel is voltooid. Zie [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="a0644-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="a0644-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a0644-150">Next steps</span></span>
<span data-ttu-id="a0644-151">Lees voor meer informatie over de zakelijke continuïteit functies van Azure SQL Database-versies, de [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="a0644-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
