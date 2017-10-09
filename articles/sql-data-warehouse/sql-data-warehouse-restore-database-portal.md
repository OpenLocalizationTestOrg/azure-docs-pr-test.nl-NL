---
title: aaaRestore Azure SQL Data Warehouse (Azure-portal) | Microsoft Docs
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
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="449a0-103">Herstellen van Azure SQL Data Warehouse (portal)</span><span class="sxs-lookup"><span data-stu-id="449a0-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="449a0-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="449a0-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="449a0-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="449a0-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="449a0-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="449a0-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="449a0-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="449a0-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="449a0-108">In dit artikel leert u hoe toorestore Azure SQL Data Warehouse met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="449a0-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="449a0-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="449a0-109">Before you begin</span></span>
<span data-ttu-id="449a0-110">**Controleer of de capaciteit van de DTU.**</span><span class="sxs-lookup"><span data-stu-id="449a0-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="449a0-111">Elk exemplaar van SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) waarvoor een standaardquotum gegevensdoorvoer unit (DTU).</span><span class="sxs-lookup"><span data-stu-id="449a0-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="449a0-112">Voordat u SQL Data Warehouse herstellen kunt, Controleer of uw SQL server onvoldoende resterende DTU-quotum voor Hallo-database die u wilt herstellen.</span><span class="sxs-lookup"><span data-stu-id="449a0-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="449a0-113">toolearn hoe toocalculate DTU-quotum of toorequest meer dtu's, Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="449a0-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="449a0-114">Herstel de database van een actieve of onderbroken</span><span class="sxs-lookup"><span data-stu-id="449a0-114">Restore an active or paused database</span></span>
<span data-ttu-id="449a0-115">een database toorestore:</span><span class="sxs-lookup"><span data-stu-id="449a0-115">toorestore a database:</span></span>

1. <span data-ttu-id="449a0-116">Meld u aan toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="449a0-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="449a0-117">Selecteer in het linkerdeelvenster Hallo **Bladeren**, en selecteer vervolgens **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="449a0-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="449a0-119">Zoek uw server en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="449a0-119">Find your server, and then select it.</span></span>

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="449a0-121">Hallo-exemplaar van SQL Data Warehouse vinden dat u wilt toorestore uit en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="449a0-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Hallo-exemplaar van SQL Data Warehouse toorestore selecteren](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="449a0-123">Selecteer bovenaan Hallo Hallo Data Warehouse blade, **herstellen**.</span><span class="sxs-lookup"><span data-stu-id="449a0-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Selecteer herstellen](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="449a0-125">Geef een nieuwe **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="449a0-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="449a0-126">Meest recente Selecteer Hallo **herstelpunt**.</span><span class="sxs-lookup"><span data-stu-id="449a0-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="449a0-127">Zorg ervoor dat u de meest recente herstelpunt Hallo kiezen.</span><span class="sxs-lookup"><span data-stu-id="449a0-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="449a0-128">Omdat herstelpunten worden weergegeven in Coordinated Universal Time (UTC), is de standaardoptie Hallo mogelijk niet de meest recente herstelpunt Hallo.</span><span class="sxs-lookup"><span data-stu-id="449a0-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Selecteer een herstelpunt](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="449a0-130">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="449a0-130">Select **OK**.</span></span>
9. <span data-ttu-id="449a0-131">Hallo-database terugzetten proces wordt gestart en u kunt **meldingen** toomonitor Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="449a0-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="449a0-132">Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="449a0-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="449a0-133">Een verwijderde database herstellen</span><span class="sxs-lookup"><span data-stu-id="449a0-133">Restore a deleted database</span></span>
<span data-ttu-id="449a0-134">een verwijderde database toorestore:</span><span class="sxs-lookup"><span data-stu-id="449a0-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="449a0-135">Meld u aan toohello [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="449a0-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="449a0-136">Selecteer in het linkerdeelvenster Hallo **Bladeren**, en selecteer vervolgens **SQL-servers**.</span><span class="sxs-lookup"><span data-stu-id="449a0-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="449a0-138">Zoek uw server en selecteert u vervolgens.</span><span class="sxs-lookup"><span data-stu-id="449a0-138">Find your server, and then select it.</span></span>

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="449a0-140">Schuif omlaag toohello **Operations** sectie op de blade van uw server.</span><span class="sxs-lookup"><span data-stu-id="449a0-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="449a0-141">Selecteer Hallo **databases verwijderd** tegel.</span><span class="sxs-lookup"><span data-stu-id="449a0-141">Select hello **Deleted databases** tile.</span></span>

    ![Hallo verwijderde databases tegel selecteren](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="449a0-143">Selecteer Hallo gewenste toorestore database verwijderd.</span><span class="sxs-lookup"><span data-stu-id="449a0-143">Select hello deleted database that you want toorestore.</span></span>

    ![Selecteer een database toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="449a0-145">Geef een nieuwe **databasenaam**.</span><span class="sxs-lookup"><span data-stu-id="449a0-145">Specify a new **Database name**.</span></span>

    ![Een naam voor de database Hallo toevoegen](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="449a0-147">Selecteer **OK**.</span><span class="sxs-lookup"><span data-stu-id="449a0-147">Select **OK**.</span></span>
9. <span data-ttu-id="449a0-148">Hallo-database terugzetten proces wordt gestart en u kunt **meldingen** toomonitor Hallo proces.</span><span class="sxs-lookup"><span data-stu-id="449a0-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="449a0-149">tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="449a0-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="449a0-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="449a0-150">Next steps</span></span>
<span data-ttu-id="449a0-151">toolearn over Hallo zakelijke continuïteit functies van Azure SQL Database-edities worden gelezen Hallo [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="449a0-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
