---
title: aaaManage rekencapaciteit in Azure SQL Data Warehouse (Azure-portal) | Microsoft Docs
description: Azure portal taken toomanage rekenkracht. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten compute-bronnen toosave kosten.
services: sql-data-warehouse
documentationcenter: NA
author: hirokib
manager: jhubbard
editor: 
ms.assetid: 233b0da5-4abd-4d1d-9586-4ccc5f50b071
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: elbutter;barbkess
ms.openlocfilehash: b2e84b3763e97ce88c190eecfb64b2d06f727229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a>Beheren van de rekencapaciteit in Azure SQL Data Warehouse (Azure-portal)
> [!div class="op_single_selector"]
> * [Overzicht](sql-data-warehouse-manage-compute-overview.md)
> * [Portal](sql-data-warehouse-manage-compute-portal.md)
> * [PowerShell](sql-data-warehouse-manage-compute-powershell.md)
> * [REST](sql-data-warehouse-manage-compute-rest-api.md)
> * [TSQL](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a>De rekencapaciteit schaal
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

toochange bronnen berekenen:

1. Open Hallo [Azure-portal][Azure portal], opent u de database en klik op **Scale**.

    ![Klik op schaal][1]
2. Hallo Scale blade Hallo schuifregelaar naar links of naar rechts toochange hello DWU-instelling.

    ![Schuifregelaar][2]
3. Klik op **Opslaan**. Er verschijnt een bevestigingsbericht. Klik op **Ja** tooconfirm of **geen** toocancel.

    ![Op Opslaan klikken][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a>De rekencapaciteit onderbreken
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

een database toopause:

1. Open Hallo [Azure-portal] [ Azure portal] en open uw database. U ziet dat de status van Hallo **Online**.

    ![Onlinestatus][6]
2. toosuspend berekenings- en geheugenbronnen kost, klikt u op **onderbreken**, en vervolgens een bevestigingsbericht weergegeven. Klik op **Ja** tooconfirm of **geen** toocancel.

    ![Onderbreken bevestigen][7]
3. Hoewel SQL Data Warehouse wordt gestart Hallo-database, is het Hallo status **onderbreken**.
4. Wanneer de status van de Hallo is **onderbroken**, Hallo onderbreken wordt uitgevoerd en u bent niet meer in rekening worden gebracht dwu's.

    ![Status onderbreken][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a>Compute hervatten
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

een database tooresume:

1. Open Hallo [Azure-portal] [ Azure portal] en open uw database. U ziet dat de status van Hallo **onderbroken**.

    ![Database onderbreken][4]
2. Klik op de database van de tooresume hello **Start**, en vervolgens een bevestigingsbericht weergegeven. Klik op **Ja** tooconfirm of **geen** toocancel.

    ![Bevestig hervatten][5]
3. Terwijl SQL Data Warehouse Hallo database gestart wordt, wordt de status Hallo 'Hervat'.
4. Wanneer de status van de Hallo is **online**, Hallo-database is gereed.

    ![Onlinestatus][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie [Beheeroverzicht][Management overview].

<!--Image references-->
[1]: ./media/sql-data-warehouse-manage-compute-portal/click-scale.png
[2]: ./media/sql-data-warehouse-manage-compute-portal/move-slider.png
[3]: ./media/sql-data-warehouse-manage-compute-portal/click-save.png
[4]: ./media/sql-data-warehouse-manage-compute-portal/resume-database.png
[5]: ./media/sql-data-warehouse-manage-compute-portal/resume-confirm.png
[6]: ./media/sql-data-warehouse-manage-compute-portal/pause-database.png
[7]: ./media/sql-data-warehouse-manage-compute-portal/pause-confirm.png

<!--Article references-->
[Management overview]: ./sql-data-warehouse-overview-manage.md
[Manage compute overview]: ./sql-data-warehouse-manage-compute-overview.md

<!--MSDN references-->


<!--Other Web references-->

[Azure portal]: http://portal.azure.com/
