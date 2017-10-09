---
title: aaaDevelop U-SQL-scripts met behulp van Data Lake Tools voor Visual Studio | Microsoft Docs
description: Meer informatie over hoe tooinstall Data Lake Tools voor Visual Studio en hoe toodevelop en test U-SQL-scripts.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a><span data-ttu-id="34c4c-103">U-SQL-scripts ontwikkelen met Data Lake-tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="34c4c-103">Develop U-SQL scripts by using Data Lake Tools for Visual Studio</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


<span data-ttu-id="34c4c-104">Meer informatie over hoe definiëren toouse Visual Studio toocreate Azure Data Lake Analytics-accounts,-taken in [U-SQL](data-lake-analytics-u-sql-get-started.md), en het verzenden van taken toohello Data Lake Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="34c4c-104">Learn how toouse Visual Studio toocreate Azure Data Lake Analytics accounts, define jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs toohello Data Lake Analytics service.</span></span> <span data-ttu-id="34c4c-105">Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="34c4c-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="34c4c-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="34c4c-106">Prerequisites</span></span>

* <span data-ttu-id="34c4c-107">**Visual Studio**: alle versies behalve Express worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="34c4c-107">**Visual Studio**: All editions except Express are supported.</span></span>
    * <span data-ttu-id="34c4c-108">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="34c4c-108">Visual Studio 2017</span></span>
    * <span data-ttu-id="34c4c-109">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="34c4c-109">Visual Studio 2015</span></span>
    * <span data-ttu-id="34c4c-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="34c4c-110">Visual Studio 2013</span></span>
* <span data-ttu-id="34c4c-111">**Microsoft Azure SDK voor .NET** versie 2.7.1 of hoger.</span><span class="sxs-lookup"><span data-stu-id="34c4c-111">**Microsoft Azure SDK for .NET** version 2.7.1 or later.</span></span>  <span data-ttu-id="34c4c-112">Installeren met behulp van Hallo [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="34c4c-112">Install it by using hello [Web platform installer](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="34c4c-113">Een **Data Lake Analytics**-account.</span><span class="sxs-lookup"><span data-stu-id="34c4c-113">A **Data Lake Analytics** account.</span></span> <span data-ttu-id="34c4c-114">toocreate een account, Zie [aan de slag met Azure Data Lake Analytics met Azure portal](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="34c4c-114">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md).</span></span>

## <a name="install-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="34c4c-115">Azure Data Lake-tools voor Visual Studio installeren</span><span class="sxs-lookup"><span data-stu-id="34c4c-115">Install Azure Data Lake Tools for Visual Studio</span></span> 

<span data-ttu-id="34c4c-116">Download en installeer Azure Data Lake Tools voor Visual Studio [van Downloadcentrum Hallo](http://aka.ms/adltoolsvs).</span><span class="sxs-lookup"><span data-stu-id="34c4c-116">Download and install Azure Data Lake Tools for Visual Studio [from hello Download Center](http://aka.ms/adltoolsvs).</span></span> <span data-ttu-id="34c4c-117">Na installatie moet u zich het volgende realiseren:</span><span class="sxs-lookup"><span data-stu-id="34c4c-117">After installation, note that:</span></span>
* <span data-ttu-id="34c4c-118">Hallo **Server Explorer** > **Azure** knooppunt bevat een **Data Lake Analytics** knooppunt.</span><span class="sxs-lookup"><span data-stu-id="34c4c-118">hello **Server Explorer** > **Azure** node contains a **Data Lake Analytics** node.</span></span> 
* <span data-ttu-id="34c4c-119">Hallo **extra** menu heeft een **Data Lake** item.</span><span class="sxs-lookup"><span data-stu-id="34c4c-119">hello **Tools** menu has a **Data Lake** item.</span></span>

## <a name="connect-tooan-azure-data-lake-analytics-account"></a><span data-ttu-id="34c4c-120">Tooan Azure Data Lake Analytics-account koppelen</span><span class="sxs-lookup"><span data-stu-id="34c4c-120">Connect tooan Azure Data Lake Analytics account</span></span>

1. <span data-ttu-id="34c4c-121">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="34c4c-121">Open Visual Studio.</span></span>
2. <span data-ttu-id="34c4c-122">Open Server Explorer via **Weergave** > **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-122">Open Server Explorer by selecting **View** > **Server Explorer**.</span></span>
3. <span data-ttu-id="34c4c-123">Klik met de rechtermuisknop op **Azure**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-123">Right-click **Azure**.</span></span> <span data-ttu-id="34c4c-124">Selecteer vervolgens **tooMicrosoft Azure-abonnement verbinden** en volg de instructies Hallo.</span><span class="sxs-lookup"><span data-stu-id="34c4c-124">Then select **Connect tooMicrosoft Azure Subscription** and follow hello instructions.</span></span>
4. <span data-ttu-id="34c4c-125">In Server Explorer selecteert u **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-125">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> <span data-ttu-id="34c4c-126">U ziet een lijst met uw Data Lake Analytics-accounts.</span><span class="sxs-lookup"><span data-stu-id="34c4c-126">You see a list of your Data Lake Analytics accounts.</span></span>


## <a name="write-your-first-u-sql-script"></a><span data-ttu-id="34c4c-127">Uw eerste U-SQL-script schrijven</span><span class="sxs-lookup"><span data-stu-id="34c4c-127">Write your first U-SQL script</span></span>

<span data-ttu-id="34c4c-128">na de tekst Hello is een eenvoudige U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="34c4c-128">hello following text is a simple U-SQL script.</span></span> <span data-ttu-id="34c4c-129">Definieert een kleine gegevensset- en schrijfbewerkingen die gegevensset toohello default Data Lake Store als een bestand aangeroepen `/data.csv`.</span><span class="sxs-lookup"><span data-stu-id="34c4c-129">It defines a small dataset and writes that dataset toohello default Data Lake Store as a file called `/data.csv`.</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

### <a name="submit-a-data-lake-analytics-job"></a><span data-ttu-id="34c4c-130">Een Data Lake Analytics-taak verzenden</span><span class="sxs-lookup"><span data-stu-id="34c4c-130">Submit a Data Lake Analytics job</span></span>

1. <span data-ttu-id="34c4c-131">Selecteer **Bestand** > **Nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-131">Select **File** > **New** > **Project**.</span></span>

2. <span data-ttu-id="34c4c-132">Selecteer Hallo **U-SQL Project** Typ en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-132">Select hello **U-SQL Project** type, and then click **OK**.</span></span> <span data-ttu-id="34c4c-133">Visual Studio maakt een oplossing met een **Script.usql**-bestand.</span><span class="sxs-lookup"><span data-stu-id="34c4c-133">Visual Studio creates a solution with a **Script.usql** file.</span></span>

3. <span data-ttu-id="34c4c-134">Hallo vorige script in Hallo plakken **Script.usql** venster.</span><span class="sxs-lookup"><span data-stu-id="34c4c-134">Paste hello previous script into hello **Script.usql** window.</span></span>

4. <span data-ttu-id="34c4c-135">In Hallo linkerbovenhoek Hallo **Script.usql** venster Hallo Data Lake Analytics-account opgeven.</span><span class="sxs-lookup"><span data-stu-id="34c4c-135">In hello upper-left corner of hello **Script.usql** window, specify hello Data Lake Analytics account.</span></span>

    ![U-SQL Visual Studio-project verzenden](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. <span data-ttu-id="34c4c-137">In Hallo linkerbovenhoek Hallo **Script.usql** Selecteer **indienen**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-137">In hello upper-left corner of hello **Script.usql** window, select **Submit**.</span></span>
6. <span data-ttu-id="34c4c-138">Controleer of Hallo **Analytics-Account**, en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-138">Verify hello **Analytics Account**, and then select **Submit**.</span></span> <span data-ttu-id="34c4c-139">Verzending van resultaten zijn beschikbaar in Hallo Data Lake Tools voor Visual Studio-resultaten nadat Hallo verzending voltooid is.</span><span class="sxs-lookup"><span data-stu-id="34c4c-139">Submission results are available in hello Data Lake Tools for Visual Studio Results after hello submission is complete.</span></span>

    ![U-SQL Visual Studio-project verzenden](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. <span data-ttu-id="34c4c-141">toosee hello meest recente taak status en vernieuw welkomstscherm, klikt u op **vernieuwen**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-141">toosee hello latest job status and refresh hello screen, click **Refresh**.</span></span> <span data-ttu-id="34c4c-142">Wanneer het Hallo-taak is voltooid, wordt een melding weergegeven Hallo **Taakgrafiek**, **bewerkingen voor metagegevens**, **State History**, en **Diagnostics**:</span><span class="sxs-lookup"><span data-stu-id="34c4c-142">When hello job succeeds, it shows hello **Job Graph**, **MetaData Operations**, **State History**, and **Diagnostics**:</span></span>

    ![Prestatiegrafiek U-SQL Visual Studio Data Lake Analytics-taak](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * <span data-ttu-id="34c4c-144">**Taak samenvatting** geeft samenvatting van de taak Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="34c4c-144">**Job Summary** shows hello summary of hello job.</span></span>   
   * <span data-ttu-id="34c4c-145">**Taakdetails** bevat meer informatie over het Hallo-taak, waaronder script hello, bronnen en hoekpunten.</span><span class="sxs-lookup"><span data-stu-id="34c4c-145">**Job Details** shows more specific information about hello job, including hello script, resources, and vertices.</span></span>
   * <span data-ttu-id="34c4c-146">**Taakgrafiek** Hallo voortgang van Hallo taak visualiseren.</span><span class="sxs-lookup"><span data-stu-id="34c4c-146">**Job Graph** visualizes hello progress of hello job.</span></span>
   * <span data-ttu-id="34c4c-147">**Bewerkingen voor metagegevens** toont alle Hallo-acties die zijn uitgevoerd op Hallo U-SQL-catalogus.</span><span class="sxs-lookup"><span data-stu-id="34c4c-147">**MetaData Operations** shows all hello actions that were taken on hello U-SQL catalog.</span></span>
   * <span data-ttu-id="34c4c-148">**Gegevens** ziet u alle Hallo invoer en uitvoer.</span><span class="sxs-lookup"><span data-stu-id="34c4c-148">**Data** shows all hello inputs and outputs.</span></span>
   * <span data-ttu-id="34c4c-149">**Diagnostische gegevens** biedt een geavanceerde analyse van de taakuitvoering en de prestatieoptimalisatie.</span><span class="sxs-lookup"><span data-stu-id="34c4c-149">**Diagnostics** provides an advanced analysis for job execution and performance optimization.</span></span>

### <a name="toocheck-job-state"></a><span data-ttu-id="34c4c-150">toocheck taakstatus</span><span class="sxs-lookup"><span data-stu-id="34c4c-150">toocheck job state</span></span>

1. <span data-ttu-id="34c4c-151">In Server Explorer selecteert u **Azure** > **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-151">In Server Explorer, select **Azure** > **Data Lake Analytics**.</span></span> 
2. <span data-ttu-id="34c4c-152">Vouw Hallo Data Lake Analytics-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="34c4c-152">Expand hello Data Lake Analytics account name.</span></span>
3. <span data-ttu-id="34c4c-153">Dubbelklik op **Taken**.</span><span class="sxs-lookup"><span data-stu-id="34c4c-153">Double-click **Jobs**.</span></span>
4. <span data-ttu-id="34c4c-154">Selecteer Hallo-taak die u eerder hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="34c4c-154">Select hello job that you previously submitted.</span></span>

### <a name="toosee-hello-output-of-a-job"></a><span data-ttu-id="34c4c-155">toosee hello uitvoer van een taak</span><span class="sxs-lookup"><span data-stu-id="34c4c-155">toosee hello output of a job</span></span>

1. <span data-ttu-id="34c4c-156">Blader in Server Explorer toohello taak die u hebt ingediend.</span><span class="sxs-lookup"><span data-stu-id="34c4c-156">In Server Explorer, browse toohello job you submitted.</span></span>
2. <span data-ttu-id="34c4c-157">Klik op Hallo **gegevens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="34c4c-157">Click hello **Data** tab.</span></span>
3. <span data-ttu-id="34c4c-158">In Hallo **taak uitvoer** tabblad, selecteer Hallo `"/data.csv"` bestand.</span><span class="sxs-lookup"><span data-stu-id="34c4c-158">In hello **Job Outputs** tab, select hello `"/data.csv"` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34c4c-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="34c4c-159">Next steps</span></span>

* [<span data-ttu-id="34c4c-160">U-SQL-scripts uitvoeren op uw eigen werkstation voor tests en foutopsporing</span><span class="sxs-lookup"><span data-stu-id="34c4c-160">Run U-SQL scripts on your own workstation for testing and debugging</span></span>](data-lake-analytics-data-lake-tools-local-run.md)
* [<span data-ttu-id="34c4c-161">Problemen met C#-code oplossen in U-SQL-taken</span><span class="sxs-lookup"><span data-stu-id="34c4c-161">Debug C# code in U-SQL jobs</span></span>](data-lake-analytics-debug-u-sql-jobs.md)
* [<span data-ttu-id="34c4c-162">Hello Azure Data Lake Tools voor Visual Studio Code gebruiken</span><span class="sxs-lookup"><span data-stu-id="34c4c-162">Use hello Azure Data Lake Tools for Visual Studio Code</span></span>](data-lake-analytics-data-lake-tools-for-vscode.md)
