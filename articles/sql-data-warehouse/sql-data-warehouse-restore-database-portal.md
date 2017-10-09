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
# <a name="restore-azure-sql-data-warehouse-portal"></a>Herstellen van Azure SQL Data Warehouse (portal)
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
>
>
In dit artikel leert u hoe toorestore Azure SQL Data Warehouse met behulp van hello Azure-portal.

## <a name="before-you-begin"></a>Voordat u begint
**Controleer of de capaciteit van de DTU.** Elk exemplaar van SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) waarvoor een standaardquotum gegevensdoorvoer unit (DTU). Voordat u SQL Data Warehouse herstellen kunt, Controleer of uw SQL server onvoldoende resterende DTU-quotum voor Hallo-database die u wilt herstellen. toolearn hoe toocalculate DTU-quotum of toorequest meer dtu's, Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Herstel de database van een actieve of onderbroken
een database toorestore:

1. Meld u aan toohello [Azure-portal][Azure portal].
2. Selecteer in het linkerdeelvenster Hallo **Bladeren**, en selecteer vervolgens **SQL-servers**.

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Zoek uw server en selecteert u vervolgens.

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. Hallo-exemplaar van SQL Data Warehouse vinden dat u wilt toorestore uit en selecteert u vervolgens.

    ![Hallo-exemplaar van SQL Data Warehouse toorestore selecteren](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. Selecteer bovenaan Hallo Hallo Data Warehouse blade, **herstellen**.

    ![Selecteer herstellen](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. Geef een nieuwe **databasenaam**.
7. Meest recente Selecteer Hallo **herstelpunt**.

   Zorg ervoor dat u de meest recente herstelpunt Hallo kiezen. Omdat herstelpunten worden weergegeven in Coordinated Universal Time (UTC), is de standaardoptie Hallo mogelijk niet de meest recente herstelpunt Hallo.

      ![Selecteer een herstelpunt](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. Selecteer **OK**.
9. Hallo-database terugzetten proces wordt gestart en u kunt **meldingen** toomonitor Hallo proces.

> [!NOTE]
> Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].
>
>

## <a name="restore-a-deleted-database"></a>Een verwijderde database herstellen
een verwijderde database toorestore:

1. Meld u aan toohello [Azure-portal][Azure portal].
2. Selecteer in het linkerdeelvenster Hallo **Bladeren**, en selecteer vervolgens **SQL-servers**.

    ![Selecteer Bladeren > SQL-servers](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. Zoek uw server en selecteert u vervolgens.

    ![Selecteer de server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. Schuif omlaag toohello **Operations** sectie op de blade van uw server.
5. Selecteer Hallo **databases verwijderd** tegel.

    ![Hallo verwijderde databases tegel selecteren](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. Selecteer Hallo gewenste toorestore database verwijderd.

    ![Selecteer een database toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. Geef een nieuwe **databasenaam**.

    ![Een naam voor de database Hallo toevoegen](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. Selecteer **OK**.
9. Hallo-database terugzetten proces wordt gestart en u kunt **meldingen** toomonitor Hallo proces.

> [!NOTE]
> tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].
>
>

## <a name="next-steps"></a>Volgende stappen
toolearn over Hallo zakelijke continuïteit functies van Azure SQL Database-edities worden gelezen Hallo [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].

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
