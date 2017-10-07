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
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="d6bb9-103">Herstellen van een Azure SQL datawarehouse (REST-API)</span><span class="sxs-lookup"><span data-stu-id="d6bb9-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="d6bb9-104">[Overzicht][Overview]</span><span class="sxs-lookup"><span data-stu-id="d6bb9-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="d6bb9-105">[Portal][Portal]</span><span class="sxs-lookup"><span data-stu-id="d6bb9-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="d6bb9-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="d6bb9-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="d6bb9-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="d6bb9-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="d6bb9-108">In dit artikel leert u hoe een Azure SQL Data Warehouse met toorestore Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="d6bb9-109">Voordat u begint</span><span class="sxs-lookup"><span data-stu-id="d6bb9-109">Before you begin</span></span>
<span data-ttu-id="d6bb9-110">**Controleer of de capaciteit van de DTU.**</span><span class="sxs-lookup"><span data-stu-id="d6bb9-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="d6bb9-111">Elke SQL Data Warehouse wordt gehost door een SQL-server (bijvoorbeeld myserver.database.windows.net) met een standaard DTU-quotum.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="d6bb9-112">Voordat u een SQL Data Warehouse herstelt kunt, te controleren die Hallo die uw SQL-server heeft onvoldoende resterende DTU-quotum voor Hallo-database wordt hersteld.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="d6bb9-113">toolearn hoe toocalculate DTU overbodig of toorequest meer DTU Zie [een wijziging DTU-quotum aanvragen][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="d6bb9-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="d6bb9-114">Herstel de database van een actieve of onderbroken</span><span class="sxs-lookup"><span data-stu-id="d6bb9-114">Restore an active or paused database</span></span>
<span data-ttu-id="d6bb9-115">een database toorestore:</span><span class="sxs-lookup"><span data-stu-id="d6bb9-115">toorestore a database:</span></span>

1. <span data-ttu-id="d6bb9-116">Hallo lijst ophalen van herstelpunten voor database met Hallo herstelpunten voor Database Get-bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="d6bb9-117">Het terugzetten starten met behulp van Hallo [Create database terugzetten aanvraag] [ Create database restore request] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="d6bb9-118">Hallo-status van uw terugzetten bijhouden met de Hallo [bewerking databasestatus] [ Database operation status] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="d6bb9-119">Nadat het Hallo terugzetten is voltooid, kunt u de herstelde database configureren door [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d6bb9-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="d6bb9-120">Een verwijderde database herstellen</span><span class="sxs-lookup"><span data-stu-id="d6bb9-120">Restore a deleted database</span></span>
<span data-ttu-id="d6bb9-121">een verwijderde database toorestore:</span><span class="sxs-lookup"><span data-stu-id="d6bb9-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="d6bb9-122">Overzicht van de verwijderde databases met behulp van Hallo [lijst terug te zetten databases verwijderd] [ List restorable dropped databases] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="d6bb9-123">Hallo details ophalen voor de gewenste Hallo verwijderde database toorestore met behulp van Hallo [Get terug te zetten database verwijderd] [ Get restorable dropped database] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="d6bb9-124">Het terugzetten starten met behulp van Hallo [Create database terugzetten aanvraag] [ Create database restore request] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="d6bb9-125">Hallo-status van uw terugzetten bijhouden met de Hallo [bewerking databasestatus] [ Database operation status] bewerking.</span><span class="sxs-lookup"><span data-stu-id="d6bb9-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="d6bb9-126">tooconfigure uw database nadat Hallo terugzetten is voltooid, Zie [uw database na herstel configureren][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="d6bb9-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d6bb9-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6bb9-127">Next steps</span></span>
<span data-ttu-id="d6bb9-128">Lees Hallo toolearn over Hallo zakelijke continuïteit functies van Azure SQL Database-edities [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="d6bb9-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
