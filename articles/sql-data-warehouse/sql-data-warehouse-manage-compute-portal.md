---
title: Beheren van de rekencapaciteit in Azure SQL Data Warehouse (Azure-portal) | Microsoft Docs
description: Azure portal taken voor het beheren van rekencapaciteit. Het aantal rekenresources door dwu's aan te passen. Of onderbreken en hervatten rekenresources kosten besparen.
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
ms.openlocfilehash: 63888d5dd103b585cf18e4787d3e779810163e3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-compute-power-in-azure-sql-data-warehouse-azure-portal"></a><span data-ttu-id="29ebe-105">Beheren van de rekencapaciteit in Azure SQL Data Warehouse (Azure-portal)</span><span class="sxs-lookup"><span data-stu-id="29ebe-105">Manage compute power in Azure SQL Data Warehouse (Azure portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="29ebe-106">Overzicht</span><span class="sxs-lookup"><span data-stu-id="29ebe-106">Overview</span></span>](sql-data-warehouse-manage-compute-overview.md)
> * [<span data-ttu-id="29ebe-107">Portal</span><span class="sxs-lookup"><span data-stu-id="29ebe-107">Portal</span></span>](sql-data-warehouse-manage-compute-portal.md)
> * [<span data-ttu-id="29ebe-108">PowerShell</span><span class="sxs-lookup"><span data-stu-id="29ebe-108">PowerShell</span></span>](sql-data-warehouse-manage-compute-powershell.md)
> * [<span data-ttu-id="29ebe-109">REST</span><span class="sxs-lookup"><span data-stu-id="29ebe-109">REST</span></span>](sql-data-warehouse-manage-compute-rest-api.md)
> * [<span data-ttu-id="29ebe-110">TSQL</span><span class="sxs-lookup"><span data-stu-id="29ebe-110">TSQL</span></span>](sql-data-warehouse-manage-compute-tsql.md)
>
>


## <a name="scale-compute-power"></a><span data-ttu-id="29ebe-111">De rekencapaciteit schaal</span><span class="sxs-lookup"><span data-stu-id="29ebe-111">Scale compute power</span></span>
[!INCLUDE [SQL Data Warehouse scale DWUs description](../../includes/sql-data-warehouse-scale-dwus-description.md)]

<span data-ttu-id="29ebe-112">Rekenresources wijzigen:</span><span class="sxs-lookup"><span data-stu-id="29ebe-112">To change compute resources:</span></span>

1. <span data-ttu-id="29ebe-113">Open de [Azure-portal][Azure portal], opent u de database en klik op **Scale**.</span><span class="sxs-lookup"><span data-stu-id="29ebe-113">Open the [Azure portal][Azure portal], open your database, and click **Scale**.</span></span>

    ![Klik op schaal][1]
2. <span data-ttu-id="29ebe-115">In de blade Scale Verplaats de schuifregelaar naar links of rechts om de DWU-instelling te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="29ebe-115">In the Scale blade, move the slider left or right to change the DWU setting.</span></span>

    ![Schuifregelaar][2]
3. <span data-ttu-id="29ebe-117">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="29ebe-117">Click **Save**.</span></span> <span data-ttu-id="29ebe-118">Er verschijnt een bevestigingsbericht.</span><span class="sxs-lookup"><span data-stu-id="29ebe-118">A confirmation message appears.</span></span> <span data-ttu-id="29ebe-119">Klik op **Ja** om te bevestigen of **geen** om te annuleren.</span><span class="sxs-lookup"><span data-stu-id="29ebe-119">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Op Opslaan klikken][3]

<a name="pause-compute-bk"></a>

## <a name="pause-compute"></a><span data-ttu-id="29ebe-121">De rekencapaciteit onderbreken</span><span class="sxs-lookup"><span data-stu-id="29ebe-121">Pause compute</span></span>
[!INCLUDE [SQL Data Warehouse pause description](../../includes/sql-data-warehouse-pause-description.md)]

<span data-ttu-id="29ebe-122">Een database onderbreken:</span><span class="sxs-lookup"><span data-stu-id="29ebe-122">To pause a database:</span></span>

1. <span data-ttu-id="29ebe-123">Open de [Azure-portal] [ Azure portal] en open uw database.</span><span class="sxs-lookup"><span data-stu-id="29ebe-123">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="29ebe-124">U ziet dat de Status is **Online**.</span><span class="sxs-lookup"><span data-stu-id="29ebe-124">Notice that the Status is **Online**.</span></span>

    ![Onlinestatus][6]
2. <span data-ttu-id="29ebe-126">Als u wilt onderbreken berekenings-en geheugenbronnen, klikt u op **onderbreken**, en vervolgens een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29ebe-126">To suspend compute and memory resources, click **Pause**, and then a confirmation message appears.</span></span> <span data-ttu-id="29ebe-127">Klik op **Ja** om te bevestigen of **geen** om te annuleren.</span><span class="sxs-lookup"><span data-stu-id="29ebe-127">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Onderbreken bevestigen][7]
3. <span data-ttu-id="29ebe-129">Terwijl de SQL Data Warehouse met het starten van de database, de status is **onderbreken**.</span><span class="sxs-lookup"><span data-stu-id="29ebe-129">While SQL Data Warehouse is starting the database, the status is **Pausing**.</span></span>
4. <span data-ttu-id="29ebe-130">Wanneer de status is **onderbroken**, de pauze-bewerking wordt uitgevoerd en u bent niet meer in rekening worden gebracht dwu's.</span><span class="sxs-lookup"><span data-stu-id="29ebe-130">When the status is **Paused**, the pause operation is done and you are no longer being charged for DWUs.</span></span>

    ![Status onderbreken][4]

<a name="resume-compute-bk"></a>

## <a name="resume-compute"></a><span data-ttu-id="29ebe-132">Compute hervatten</span><span class="sxs-lookup"><span data-stu-id="29ebe-132">Resume compute</span></span>
[!INCLUDE [SQL Data Warehouse resume description](../../includes/sql-data-warehouse-resume-description.md)]

<span data-ttu-id="29ebe-133">Een database hervatten:</span><span class="sxs-lookup"><span data-stu-id="29ebe-133">To resume a database:</span></span>

1. <span data-ttu-id="29ebe-134">Open de [Azure-portal] [ Azure portal] en open uw database.</span><span class="sxs-lookup"><span data-stu-id="29ebe-134">Open the [Azure portal][Azure portal] and open your database.</span></span> <span data-ttu-id="29ebe-135">U ziet dat de Status is **onderbroken**.</span><span class="sxs-lookup"><span data-stu-id="29ebe-135">Notice that the Status is **Paused**.</span></span>

    ![Database onderbreken][4]
2. <span data-ttu-id="29ebe-137">Het database klikt u op hervatten **Start**, en vervolgens een bevestigingsbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="29ebe-137">To resume the database click **Start**, and then a confirmation message appears.</span></span> <span data-ttu-id="29ebe-138">Klik op **Ja** om te bevestigen of **geen** om te annuleren.</span><span class="sxs-lookup"><span data-stu-id="29ebe-138">Click **yes** to confirm or **no** to cancel.</span></span>

    ![Bevestig hervatten][5]
3. <span data-ttu-id="29ebe-140">Terwijl SQL Data Warehouse kan de database wordt gestart, wordt de status 'Hervat'.</span><span class="sxs-lookup"><span data-stu-id="29ebe-140">While SQL Data Warehouse is starting the database, the status is "Resuming".</span></span>
4. <span data-ttu-id="29ebe-141">Wanneer de status is **online**, de database is gereed.</span><span class="sxs-lookup"><span data-stu-id="29ebe-141">When the status is **online**, the database is ready.</span></span>

    ![Onlinestatus][6]

<a name="next-steps-bk"></a>

## <a name="next-steps"></a><span data-ttu-id="29ebe-143">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="29ebe-143">Next steps</span></span>
<span data-ttu-id="29ebe-144">Zie voor meer informatie [Beheeroverzicht][Management overview].</span><span class="sxs-lookup"><span data-stu-id="29ebe-144">For more information, see [Management overview][Management overview].</span></span>

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
