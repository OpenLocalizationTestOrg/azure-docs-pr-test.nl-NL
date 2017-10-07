---
title: aaaRestore een Azure SQL Data Warehouse (REST-API) | Microsoft Docs
description: REST-API-taken voor het herstellen van een Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a>Herstellen van een Azure SQL datawarehouse (REST-API)
> [!div class="op_single_selector"]
> * [Overzicht][Overview]
> * [Portal][Portal]
> * [PowerShell][PowerShell]
> * [REST][REST]
> 
> 

In dit artikel leert u hoe een Azure SQL Data Warehouse met toorestore Hallo REST-API.

## <a name="before-you-begin"></a>Voordat u begint
**Controleer of de capaciteit van de DTU.** Elke SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) met een standaard DTU-quotum.  Voordat u een SQL Data Warehouse herstelt kunt, te controleren die Hallo die uw SQL-server heeft onvoldoende resterende DTU-quotum voor Hallo-database wordt hersteld. toolearn hoe toocalculate DTU overbodig of toorequest meer DTU Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].

## <a name="restore-an-active-or-paused-database"></a>Herstel de database van een actieve of onderbroken
een database toorestore:

1. Hallo lijst ophalen van herstelpunten voor database met Hallo herstelpunten voor Database Get-bewerking.
2. Het terugzetten starten met behulp van Hallo [Create database terugzetten aanvraag] [ Create database restore request] bewerking.
3. Hallo-status van uw terugzetten bijhouden met de Hallo [bewerking databasestatus] [ Database operation status] bewerking.

> [!NOTE]
> Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].
> 
> 

## <a name="restore-a-deleted-database"></a>Een verwijderde database herstellen
een verwijderde database toorestore:

1. Overzicht van de verwijderde databases met behulp van Hallo [lijst terug te zetten databases verwijderd] [ List restorable dropped databases] bewerking.
2. Hallo details ophalen voor de gewenste Hallo verwijderde database toorestore met behulp van Hallo [Get terug te zetten database verwijderd] [ Get restorable dropped database] bewerking.
3. Het terugzetten starten met behulp van Hallo [Create database terugzetten aanvraag] [ Create database restore request] bewerking.
4. Hallo-status van uw terugzetten bijhouden met de Hallo [bewerking databasestatus] [ Database operation status] bewerking.

> [!NOTE]
> tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].
> 
> 

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

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
