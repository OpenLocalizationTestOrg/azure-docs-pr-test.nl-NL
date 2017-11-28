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
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="12152-105">Beheren van de rekencapaciteit in Azure SQL Data Warehouse (Azure-portal)</span><span class="sxs-lookup"><span data-stu-id="12152-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12152-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="12152-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="12152-107">Portal</span><span class="sxs-lookup"><span data-stu-id="12152-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="12152-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12152-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="12152-109">REST</span><span class="sxs-lookup"><span data-stu-id="12152-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="12152-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="12152-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="12152-111">De rekencapaciteit schaal</span><span class="sxs-lookup"><span data-stu-id="12152-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="12152-112">toochange bronnen berekenen:</span><span class="sxs-lookup"><span data-stu-id="12152-112">toochange compute resources:</span></span>

1. <span data-ttu-id="12152-113">Open Hallo [Azure-portal][Azure portal], opent u de database en klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="12152-113">Open hello [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Klik op schaal][1]
2. <span data-ttu-id="12152-115">Hallo Scale blade Hallo schuifregelaar naar links of naar rechts toochange hello DWU-instelling.</span><span class="sxs-lookup"><span data-stu-id="12152-115">In hello Scale blade, move hello slider left or right toochange hello DWU setting.</span></span>

    ![Schuifregelaar][2]
3. <span data-ttu-id="12152-117">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="12152-117">Click **Save**.</span></span> <span data-ttu-id="12152-118">Er verschijnt een bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="12152-118">A confirmation message appears.</span></span> <span data-ttu-id="12152-119">Klik op **Ja** tooconfirm of **geen** toocancel.</span><span class="sxs-lookup"><span data-stu-id="12152-119">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Op Opslaan klikken][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="12152-121">De rekencapaciteit onderbreken</span><span class="sxs-lookup"><span data-stu-id="12152-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="12152-122">een database toopause:</span><span class="sxs-lookup"><span data-stu-id="12152-122">toopause a database:</span></span>

1. <span data-ttu-id="12152-123">Open Hallo [Azure-portal] [ Azure portal] en open uw database.</span><span class="sxs-lookup"><span data-stu-id="12152-123">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="12152-124">U ziet dat de status van Hallo **Online**.</span><span class="sxs-lookup"><span data-stu-id="12152-124">Notice that hello Status is **Online**.</span></span>

    ![Onlinestatus][6]
2. <span data-ttu-id="12152-126">toosuspend berekenings- en geheugenbronnen kost, klikt u op **onderbreken**, en vervolgens een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="12152-126">toosuspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="12152-127">Klik op **Ja** tooconfirm of **geen** toocancel.</span><span class="sxs-lookup"><span data-stu-id="12152-127">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Onderbreken bevestigen][7]
3. <span data-ttu-id="12152-129">Hoewel SQL Data Warehouse wordt gestart Hallo-database, is het Hallo status **onderbreken**.</span><span class="sxs-lookup"><span data-stu-id="12152-129">While SQL Data Warehouse is starting hello database, hello status is **Pausing**.</span></span>
4. <span data-ttu-id="12152-130">Wanneer de status van de Hallo is **onderbroken**, Hallo onderbreken wordt uitgevoerd en u bent niet meer in rekening worden gebracht dwu's.</span><span class="sxs-lookup"><span data-stu-id="12152-130">When hello status is **Paused**, hello pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Status onderbreken][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="12152-132">Compute hervatten</span><span class="sxs-lookup"><span data-stu-id="12152-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="12152-133">een database tooresume:</span><span class="sxs-lookup"><span data-stu-id="12152-133">tooresume a database:</span></span>

1. <span data-ttu-id="12152-134">Open Hallo [Azure-portal] [ Azure portal] en open uw database.</span><span class="sxs-lookup"><span data-stu-id="12152-134">Open hello [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="12152-135">U ziet dat de status van Hallo **onderbroken**.</span><span class="sxs-lookup"><span data-stu-id="12152-135">Notice that hello Status is **Paused**.</span></span>

    ![Database onderbreken][4]
2. <span data-ttu-id="12152-137">Klik op de database van de tooresume hello **Start**, en vervolgens een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="12152-137">tooresume hello database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="12152-138">Klik op **Ja** tooconfirm of **geen** toocancel.</span><span class="sxs-lookup"><span data-stu-id="12152-138">Click **yes** tooconfirm or **no** toocancel.</span></span>

    ![Bevestig hervatten][5]
3. <span data-ttu-id="12152-140">Terwijl SQL Data Warehouse Hallo database gestart wordt, wordt de status Hallo 'Hervat'.</span><span class="sxs-lookup"><span data-stu-id="12152-140">While SQL Data Warehouse is starting hello database, hello status is "Resuming".</span></span>
4. <span data-ttu-id="12152-141">Wanneer de status van de Hallo is **online**, Hallo-database is gereed.</span><span class="sxs-lookup"><span data-stu-id="12152-141">When hello status is **online**, hello database is ready.</span></span>

    ![Onlinestatus][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="12152-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12152-143">Next steps</span></span>
<span data-ttu-id="12152-144">Zie voor meer informatie [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="12152-144">For more information, see [Management overview][Management overview].</span></span>

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
