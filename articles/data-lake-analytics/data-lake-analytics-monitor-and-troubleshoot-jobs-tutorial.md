---
title: Azure Data Lake Analytics-taken aaaTroubleshoot met Azure Portal | Microsoft Docs
description: 'Meer informatie over hoe toouse hello Azure Portal tootroubleshoot Data Lake Analytics-taken. '
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
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a><span data-ttu-id="a7158-103">Azure Data Lake Analytics-taken via Azure Portal oplossen</span><span class="sxs-lookup"><span data-stu-id="a7158-103">Troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>
<span data-ttu-id="a7158-104">Meer informatie over hoe toouse hello Azure Portal tootroubleshoot Data Lake Analytics-taken.</span><span class="sxs-lookup"><span data-stu-id="a7158-104">Learn how toouse hello Azure Portal tootroubleshoot Data Lake Analytics jobs.</span></span>

<span data-ttu-id="a7158-105">In deze zelfstudie maakt u een ontbrekende bron bestand probleem instellen, en gebruikt hello Azure Portal tootroubleshoot Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="a7158-105">In this tutorial, you will setup a missing source file problem, and use hello Azure Portal tootroubleshoot hello problem.</span></span>

## <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="a7158-106">Een Data Lake Analytics-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="a7158-106">Submit a Data Lake Analytics job</span></span>

<span data-ttu-id="a7158-107">Hallo volgende U-SQL-taak verzenden:</span><span class="sxs-lookup"><span data-stu-id="a7158-107">Submit hello following U-SQL job:</span></span>

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
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
<span data-ttu-id="a7158-108">Hallo bronbestand gedefinieerd in het Hallo-script is **/Samples/Data/SearchLog.tsv1**, dit moet waar **/Samples/Data/SearchLog.tsv**.</span><span class="sxs-lookup"><span data-stu-id="a7158-108">hello source file defined in hello script is **/Samples/Data/SearchLog.tsv1**, where it should be **/Samples/Data/SearchLog.tsv**.</span></span>


## <a name="troubleshoot-hello-job"></a><span data-ttu-id="a7158-109">Hallo-taak oplossen</span><span class="sxs-lookup"><span data-stu-id="a7158-109">Troubleshoot hello job</span></span>

<span data-ttu-id="a7158-110">**toosee alle taken Hallo**</span><span class="sxs-lookup"><span data-stu-id="a7158-110">**toosee all hello jobs**</span></span>

1. <span data-ttu-id="a7158-111">Hallo Azure-portal, klik op **Microsoft Azure** in de linkerbovenhoek Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7158-111">From hello Azure portal, click **Microsoft Azure** in hello upper left corner.</span></span>
2. <span data-ttu-id="a7158-112">Klik op de tegel Hallo met de naam van uw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="a7158-112">Click hello tile with your Data Lake Analytics account name.</span></span>  <span data-ttu-id="a7158-113">Hallo taak overzicht wordt weergegeven op Hallo **Jobbeheer** tegel.</span><span class="sxs-lookup"><span data-stu-id="a7158-113">hello job summary is shown on hello **Job Management** tile.</span></span>

    ![Beheer van Azure Data Lake Analytics-taak](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    <span data-ttu-id="a7158-115">Hallo taak Management biedt u een overzicht van de taakstatus Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7158-115">hello job Management gives you a glance of hello job status.</span></span> <span data-ttu-id="a7158-116">Er is een mislukte taak.</span><span class="sxs-lookup"><span data-stu-id="a7158-116">Notice there is a failed job.</span></span>
3. <span data-ttu-id="a7158-117">Klik op Hallo **Jobbeheer** tegel toosee Hallo taken.</span><span class="sxs-lookup"><span data-stu-id="a7158-117">Click hello **Job Management** tile toosee hello jobs.</span></span> <span data-ttu-id="a7158-118">Hallo-taken zijn onderverdeeld in **met**, **in de wachtrij geplaatst**, en **beëindigd**.</span><span class="sxs-lookup"><span data-stu-id="a7158-118">hello jobs are categorized in **Running**, **Queued**, and **Ended**.</span></span> <span data-ttu-id="a7158-119">U ziet de mislukte taak in Hallo **beëindigd** sectie.</span><span class="sxs-lookup"><span data-stu-id="a7158-119">You shall see your failed job in hello **Ended** section.</span></span> <span data-ttu-id="a7158-120">Het moet eerste certificaat in de lijst Hallo zijn.</span><span class="sxs-lookup"><span data-stu-id="a7158-120">It shall be first one in hello list.</span></span> <span data-ttu-id="a7158-121">Wanneer u een groot aantal taken hebt, kunt u **Filter** toohelp u toolocate taken.</span><span class="sxs-lookup"><span data-stu-id="a7158-121">When you have a lot of jobs, you can click **Filter** toohelp you toolocate jobs.</span></span>

    ![Azure Data Lake Analytics-filter-taken](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. <span data-ttu-id="a7158-123">Klik op de mislukte taak Hallo van Hallo lijst tooopen Hallo taakdetails in een nieuwe blade:</span><span class="sxs-lookup"><span data-stu-id="a7158-123">Click hello failed job from hello list tooopen hello job details in a new blade:</span></span>

    ![Azure Data Lake Analytics taak is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    <span data-ttu-id="a7158-125">Kennisgeving Hallo **opnieuw indienen** knop.</span><span class="sxs-lookup"><span data-stu-id="a7158-125">Notice hello **Resubmit** button.</span></span> <span data-ttu-id="a7158-126">Nadat u Hallo probleem hebt opgelost, kunt u de taak Hallo opnieuw indienen.</span><span class="sxs-lookup"><span data-stu-id="a7158-126">After you fix hello problem, you can resubmit hello job.</span></span>
5. <span data-ttu-id="a7158-127">Klik op de gemarkeerde onderdeel van Hallo vorige schermafbeelding tooopen Hallo foutgegevens.</span><span class="sxs-lookup"><span data-stu-id="a7158-127">Click highlighted part from hello previous screenshot tooopen hello error details.</span></span>  <span data-ttu-id="a7158-128">U ziet ongeveer als volgt:</span><span class="sxs-lookup"><span data-stu-id="a7158-128">You shall see something like:</span></span>

    ![Azure Data Lake Analytics taakdetails is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    <span data-ttu-id="a7158-130">Het vertelt u Hallo bronmap is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="a7158-130">It tells you hello source folder is not found.</span></span>
6. <span data-ttu-id="a7158-131">Klik op **Script dubbele**.</span><span class="sxs-lookup"><span data-stu-id="a7158-131">Click **Duplicate Script**.</span></span>
7. <span data-ttu-id="a7158-132">Update Hallo **FROM** pad toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a7158-132">Update hello **FROM** path toohello following:</span></span>

    <span data-ttu-id="a7158-133">' / Samples/Data/SearchLog.tsv '</span><span class="sxs-lookup"><span data-stu-id="a7158-133">"/Samples/Data/SearchLog.tsv"</span></span>
8. <span data-ttu-id="a7158-134">Klik op **Taak verzenden**.</span><span class="sxs-lookup"><span data-stu-id="a7158-134">Click **Submit Job**.</span></span>

## <a name="see-also"></a><span data-ttu-id="a7158-135">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a7158-135">See also</span></span>
* [<span data-ttu-id="a7158-136">Overzicht van Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="a7158-136">Azure Data Lake Analytics overview</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="a7158-137">Aan de slag met Azure Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a7158-137">Get started with Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="a7158-138">Aan de slag met Azure Data Lake Analytics en U-SQL Visual Studio gebruiken</span><span class="sxs-lookup"><span data-stu-id="a7158-138">Get started with Azure Data Lake Analytics and U-SQL using Visual Studio</span></span>](data-lake-analytics-u-sql-get-started.md)
* [<span data-ttu-id="a7158-139">Azure Data Lake Analytics beheren met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="a7158-139">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
