---
title: aaaAnalyze websitelogboeken met Azure Data Lake Analytics | Microsoft Docs
description: 'Meer informatie over hoe tooanalyze websitelogboeken met Data Lake Analytics. '
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="39903-103">Websitelogboeken analyseren met Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="39903-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="39903-104">Meer informatie over hoe tooanalyze websitelogboeken met behulp van Data Lake Analytics, vooral bij het vinden van welke verwijzingen is gedetecteerd fouten tijdens het toovisit Hallo website.</span><span class="sxs-lookup"><span data-stu-id="39903-104">Learn how tooanalyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried toovisit hello website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39903-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="39903-105">Prerequisites</span></span>
* <span data-ttu-id="39903-106">**Visual Studio 2015 of Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="39903-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="39903-107">**[Data Lake Tools voor Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="39903-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="39903-108">Wanneer Data Lake Tools voor Visual Studio is geïnstalleerd, ziet u een **Data Lake** item in Hallo **extra** menu in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="39903-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in hello **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio-menu](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="39903-110">**Basiskennis van Data Lake Analytics en Data Lake Tools voor Visual Studio Hallo**.</span><span class="sxs-lookup"><span data-stu-id="39903-110">**Basic knowledge of Data Lake Analytics and hello Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="39903-111">tooget gestart, Zie:</span><span class="sxs-lookup"><span data-stu-id="39903-111">tooget started, see:</span></span>

  * <span data-ttu-id="39903-112">[U-SQL-script met Data Lake tools voor Visual Studio ontwikkelen](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39903-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="39903-113">**Een Data Lake Analytics-account.**</span><span class="sxs-lookup"><span data-stu-id="39903-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="39903-114">Zie [een Azure Data Lake Analytics-account maken](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39903-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="39903-115">**Hallo sample data toohello Data Lake Analytics-account uploaden.**</span><span class="sxs-lookup"><span data-stu-id="39903-115">**Upload hello sample data toohello Data Lake Analytics account.**</span></span> <span data-ttu-id="39903-116">Zie [bestanden met voorbeeldgegevens toocopy](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39903-116">See [toocopy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="39903-117">een Data Lake Analytics-taak toorun, moet u enkele gegevens.</span><span class="sxs-lookup"><span data-stu-id="39903-117">toorun a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="39903-118">Hoewel Hallo Data Lake Tools ondersteuning biedt voor uploaden van gegevens, gebruikt u Hallo portal tooupload Hallo sample data toomake deze zelfstudie gemakkelijker toofollow.</span><span class="sxs-lookup"><span data-stu-id="39903-118">Even though hello Data Lake Tools supports uploading data, you will use hello portal tooupload hello sample data toomake this tutorial easier toofollow.</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="39903-119">Verbinding maken met tooAzure</span><span class="sxs-lookup"><span data-stu-id="39903-119">Connect tooAzure</span></span>
<span data-ttu-id="39903-120">Voordat u kunt bouwen en testen van de U-SQL-scripts, moet u eerst tooAzure verbinden.</span><span class="sxs-lookup"><span data-stu-id="39903-120">Before you can build and test any U-SQL scripts, you must first connect tooAzure.</span></span>

<span data-ttu-id="39903-121">**tooconnect tooData Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="39903-121">**tooconnect tooData Lake Analytics**</span></span>

1. <span data-ttu-id="39903-122">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="39903-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="39903-123">Klik op **Data Lake > Opties en instellingen**.</span><span class="sxs-lookup"><span data-stu-id="39903-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="39903-124">Klik op **aanmelden**, of **gebruiker wijzigen** als iemand heeft aangemeld en volg de instructies Hallo.</span><span class="sxs-lookup"><span data-stu-id="39903-124">Click **Sign In**, or **Change User** if someone has signed in, and follow hello instructions.</span></span>
4. <span data-ttu-id="39903-125">Klik op **OK** tooclose Hallo opties en instellingen dialoogvenster.</span><span class="sxs-lookup"><span data-stu-id="39903-125">Click **OK** tooclose hello Options and Settings dialog.</span></span>

<span data-ttu-id="39903-126">**toobrowse uw Data Lake Analytics-accounts**</span><span class="sxs-lookup"><span data-stu-id="39903-126">**toobrowse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="39903-127">Open in Visual Studio **Server Explorer** door press **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="39903-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="39903-128">Vouw in **Server Explorer** achtereenvolgens **Azure** en **Data Lake Analytics** uit.</span><span class="sxs-lookup"><span data-stu-id="39903-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="39903-129">U ziet een lijst met uw Data Lake Analytics-accounts, als u die hebt.</span><span class="sxs-lookup"><span data-stu-id="39903-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="39903-130">U kunt vanuit Hallo studio Data Lake Analytics-accounts maken.</span><span class="sxs-lookup"><span data-stu-id="39903-130">You cannot create Data Lake Analytics accounts from hello studio.</span></span> <span data-ttu-id="39903-131">toocreate een account, Zie [aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md) of [aan de slag met Azure Data Lake Analytics met Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39903-131">toocreate an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="39903-132">U-SQL-toepassing ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="39903-132">Develop U-SQL application</span></span>
<span data-ttu-id="39903-133">Een U-SQL-toepassing is meestal een U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="39903-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="39903-134">toolearn meer informatie over U-SQL, Zie [aan de slag met U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39903-134">toolearn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="39903-135">U kunt aanvullende gebruiker gedefinieerde operators toohello toepassing toevoegen.</span><span class="sxs-lookup"><span data-stu-id="39903-135">You can add addition user-defined operators toohello application.</span></span>  <span data-ttu-id="39903-136">Zie voor meer informatie [ontwikkelen van U-SQL door de gebruiker gedefinieerde operators voor Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="39903-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="39903-137">**toocreate en het verzenden van een Data Lake Analytics-taak**</span><span class="sxs-lookup"><span data-stu-id="39903-137">**toocreate and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="39903-138">Klik op Hallo **bestand > Nieuw > Project**.</span><span class="sxs-lookup"><span data-stu-id="39903-138">Click hello **File > New > Project**.</span></span>
2. <span data-ttu-id="39903-139">Hallo-Project U-SQL-type selecteren.</span><span class="sxs-lookup"><span data-stu-id="39903-139">Select hello U-SQL Project type.</span></span>

    ![nieuw U-SQL Visual Studio-project](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="39903-141">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="39903-141">Click **OK**.</span></span> <span data-ttu-id="39903-142">Visual studio maakt een oplossing met een bestand Script.usql.</span><span class="sxs-lookup"><span data-stu-id="39903-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="39903-143">Voer Hallo script in Hallo Script.usql-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="39903-143">Enter hello following script into hello Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    <span data-ttu-id="39903-144">toounderstand hello U-SQL, Zie [aan de slag met Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="39903-144">toounderstand hello U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="39903-145">Voeg een nieuw U-SQL-script tooyour project en voer de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="39903-145">Add a new U-SQL script tooyour project and enter hello following:</span></span>

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="39903-146">Ga terug toohello eerste U-SQL-script en volgende toohello **indienen** knop, geeft u uw Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="39903-146">Switch back toohello first U-SQL script and next toohello **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="39903-147">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="39903-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="39903-148">Controleer of Hallo resulteert in het deelvenster Hallo-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="39903-148">Verify hello results in hello Output pane.</span></span>
8. <span data-ttu-id="39903-149">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="39903-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="39903-150">Controleer of Hallo **Analytics-Account** is Hallo één waar toorun Hallo taak en klik vervolgens op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="39903-150">Verify hello **Analytics Account** is hello one where you want toorun hello job, and then click **Submit**.</span></span> <span data-ttu-id="39903-151">Resultaat van het verzenden en een koppeling naar de taak zijn beschikbaar in Hallo Data Lake Tools voor Visual Studio resultatenvenster wanneer Hallo verzenden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="39903-151">Submission results and job link are available in hello Data Lake Tools for Visual Studio Results window when hello submission is completed.</span></span>
10. <span data-ttu-id="39903-152">Wacht totdat het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="39903-152">Wait until hello job is completed successfully.</span></span>  <span data-ttu-id="39903-153">Als Hallo-taak is mislukt, waarschijnlijk ontbreken Hallo bronbestand.</span><span class="sxs-lookup"><span data-stu-id="39903-153">If hello job failed, it is most likely missing hello source file.</span></span>  <span data-ttu-id="39903-154">Zie sectie voor vereisten Hallo van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="39903-154">Please see hello Prerequisite section of this tutorial.</span></span> <span data-ttu-id="39903-155">Zie voor aanvullende informatie voor probleemoplossing [Monitor en Azure Data Lake Analytics-taken oplossen](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="39903-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="39903-156">Wanneer het Hallo-taak is voltooid, ziet u Hallo scherm te volgen:</span><span class="sxs-lookup"><span data-stu-id="39903-156">When hello job is completed, you shall see hello following screen:</span></span>

    ![Data lake analytics analyseren weblogboeken websitelogboeken](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="39903-158">Herhaal stap 7 - 10 voor **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="39903-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="39903-159">**toosee hello taakuitvoer**</span><span class="sxs-lookup"><span data-stu-id="39903-159">**toosee hello job output**</span></span>

1. <span data-ttu-id="39903-160">Van **Server Explorer**, vouw **Azure**, vouw **Data Lake Analytics**, vouw uw Data Lake Analytics-account, vouw **Opslagaccounts**, met de rechtermuisknop op Hallo standaard Data Lake Storage-account en klik vervolgens op **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="39903-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click hello default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="39903-161">Dubbelklik op **voorbeelden** tooopen Hallo map en dubbelklik vervolgens op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="39903-161">Double-click **Samples** tooopen hello folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="39903-162">Dubbelklik op **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="39903-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="39903-163">U kunt ook Hallo uitvoerbestand binnen Hallo grafiekweergave van Hallo taak in de volgorde toonavigate dubbelklikken direct toohello uitvoer.</span><span class="sxs-lookup"><span data-stu-id="39903-163">You can also double-click hello output file inside hello graph view of hello job in order toonavigate directly toohello output.</span></span>

## <a name="see-also"></a><span data-ttu-id="39903-164">Zie ook</span><span class="sxs-lookup"><span data-stu-id="39903-164">See also</span></span>
<span data-ttu-id="39903-165">tooget de slag met Data Lake Analytics met verschillende hulpprogramma's, Zie:</span><span class="sxs-lookup"><span data-stu-id="39903-165">tooget started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="39903-166">Aan de slag met Data Lake Analytics met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39903-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="39903-167">Aan de slag met Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="39903-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="39903-168">Aan de slag met Data Lake Analytics met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="39903-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
