---
title: Problemen met Azure Data Lake Analytics-taken via Azure Portal | Microsoft Docs
description: 'Informatie over het gebruik van de Azure Portal oplossen met Data Lake Analytics-taken. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: b9c7453cc0a94f70d0098ed83e5f127832065a62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="216ee-103">Azure Data Lake Analytics-taken via Azure Portal oplossen</span><span class="sxs-lookup"><span data-stu-id="216ee-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="216ee-104">Informatie over het gebruik van de Azure Portal oplossen met Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="216ee-104">Learn how to use the Azure Portal to troubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="216ee-105">In deze zelfstudie maakt u een ontbrekende bron bestand probleem instellen, en de Azure Portal gebruiken voor het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="216ee-105">In this tutorial, you will setup a missing source file problem, and use the Azure Portal to troubleshoot the problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="216ee-106">Een Data Lake Analytics-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="216ee-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="216ee-107">Verzenden van de volgende U-SQL-taak:</span><span class="sxs-lookup"><span data-stu-id="216ee-107">Submit the following U-SQL job:</span></span>

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   TO "/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="216ee-108">Het bronbestand gedefinieerd in het script **/Samples/Data/SearchLog.tsv1**, dit moet waar **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="216ee-108">The source file defined in the script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-the-job"></a><span data-ttu-id="216ee-109">Problemen met de taak oplossen</span><span class="sxs-lookup"><span data-stu-id="216ee-109">Troubleshoot the job</span></span>

<span data-ttu-id="216ee-110">**Voor een overzicht van alle taken**</span><span class="sxs-lookup"><span data-stu-id="216ee-110">**To see all the jobs**</span></span>

1. <span data-ttu-id="216ee-111">Klik in de Azure-portal op **Microsoft Azure** in de linkerbovenhoek.</span><span class="sxs-lookup"><span data-stu-id="216ee-111">From the Azure portal, click **Microsoft Azure** in the upper left corner.</span></span>
2. <span data-ttu-id="216ee-112">Klik op de tegel met de naam van uw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="216ee-112">Click the tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="216ee-113">De samenvatting taak wordt weergegeven op de **Jobbeheer** tegel.</span><span class="sxs-lookup"><span data-stu-id="216ee-113">The job summary is shown on the **Job Management** tile.</span></span>

    ![Beheer van Azure Data Lake Analytics-taak](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="216ee-115">De taak Management biedt u een overzicht van de status van de taak.</span><span class="sxs-lookup"><span data-stu-id="216ee-115">The job Management gives you a glance of the job status.</span></span> <span data-ttu-id="216ee-116">Er is een mislukte taak.</span><span class="sxs-lookup"><span data-stu-id="216ee-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="216ee-117">Klik op de **Jobbeheer** tegel om te zien van de taken.</span><span class="sxs-lookup"><span data-stu-id="216ee-117">Click the **Job Management** tile to see the jobs.</span></span> <span data-ttu-id="216ee-118">De taken zijn onderverdeeld in **met**, **in de wachtrij geplaatst**, en **beëindigd**.</span><span class="sxs-lookup"><span data-stu-id="216ee-118">The jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="216ee-119">U ziet de mislukte taak in de **beëindigd** sectie.</span><span class="sxs-lookup"><span data-stu-id="216ee-119">You shall see your failed job in the **Ended** section.</span></span> <span data-ttu-id="216ee-120">Het moet eerste certificaat in de lijst zijn.</span><span class="sxs-lookup"><span data-stu-id="216ee-120">It shall be first one in the list.</span></span> <span data-ttu-id="216ee-121">Wanneer u een groot aantal taken hebt, kunt u **Filter** om u te helpen u bij het zoeken van taken.</span><span class="sxs-lookup"><span data-stu-id="216ee-121">When you have a lot of jobs, you can click **Filter** to help you to locate jobs.</span></span>

    ![Azure Data Lake Analytics-filter-taken](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="216ee-123">Klik op de mislukte taak uit de lijst om de taakdetails openen in een nieuwe blade:</span><span class="sxs-lookup"><span data-stu-id="216ee-123">Click the failed job from the list to open the job details in a new blade:</span></span>

    ![Azure Data Lake Analytics taak is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="216ee-125">U ziet de **opnieuw indienen** knop.</span><span class="sxs-lookup"><span data-stu-id="216ee-125">Notice the **Resubmit** button.</span></span> <span data-ttu-id="216ee-126">Nadat u het probleem hebt opgelost, kunt u de taak opnieuw indienen.</span><span class="sxs-lookup"><span data-stu-id="216ee-126">After you fix the problem, you can resubmit the job.</span></span>
5. <span data-ttu-id="216ee-127">Klik op de gemarkeerde onderdeel in de vorige schermafbeelding details van de fout te openen.</span><span class="sxs-lookup"><span data-stu-id="216ee-127">Click highlighted part from the previous screenshot to open the error details.</span></span>  <span data-ttu-id="216ee-128">U ziet ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="216ee-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics taakdetails is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="216ee-130">Het vertelt u dat de bronmap is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="216ee-130">It tells you the source folder is not found.</span></span>
6. <span data-ttu-id="216ee-131">Klik op **Script dubbele**.</span><span class="sxs-lookup"><span data-stu-id="216ee-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="216ee-132">Update de **FROM** pad naar het volgende:</span><span class="sxs-lookup"><span data-stu-id="216ee-132">Update the **FROM** path to the following:</span></span>

    <span data-ttu-id="216ee-133">' / Samples/Data/SearchLog.tsv '</span><span class="sxs-lookup"><span data-stu-id="216ee-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="216ee-134">Klik op **Taak verzenden**.</span><span class="sxs-lookup"><span data-stu-id="216ee-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="216ee-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="216ee-135">See also</span></span>
* [<span data-ttu-id="216ee-136">Overzicht van Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="216ee-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="216ee-137">Aan de slag met Azure Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="216ee-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="216ee-138">Aan de slag met Azure Data Lake Analytics en U-SQL Visual Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="216ee-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="216ee-139">Azure Data Lake Analytics beheren met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="216ee-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
