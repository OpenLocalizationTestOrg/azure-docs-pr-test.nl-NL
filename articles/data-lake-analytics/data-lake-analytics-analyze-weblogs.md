---
title: Websitelogboeken analyseren met Azure Data Lake Analytics | Microsoft Docs
description: 'Informatie over het websitelogboeken analyseren met Data Lake Analytics. '
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
ms.openlocfilehash: 25fbbe97d26491fc421f4821315761c18e523ec8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a><span data-ttu-id="ed953-103">Websitelogboeken analyseren met Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ed953-103">Analyze Website logs using Azure Data Lake Analytics</span></span>
<span data-ttu-id="ed953-104">Informatie over het websitelogboeken analyseren met Data Lake Analytics, met name op fouten die verwijzingen is gedetecteerd tijdens het naar de website te controleren.</span><span class="sxs-lookup"><span data-stu-id="ed953-104">Learn how to analyze website logs using Data Lake Analytics, especially on finding out which referrers ran into errors when they tried to visit the website.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed953-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ed953-105">Prerequisites</span></span>
* <span data-ttu-id="ed953-106">**Visual Studio 2015 of Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="ed953-106">**Visual Studio 2015 or Visual Studio 2013**.</span></span>
* <span data-ttu-id="ed953-107">**[Data Lake Tools voor Visual Studio](http://aka.ms/adltoolsvs)**.</span><span class="sxs-lookup"><span data-stu-id="ed953-107">**[Data Lake Tools for Visual Studio](http://aka.ms/adltoolsvs)**.</span></span>

    <span data-ttu-id="ed953-108">Wanneer Data Lake Tools voor Visual Studio is geïnstalleerd, ziet u een **Data Lake** item in de **extra** menu in Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="ed953-108">Once Data Lake Tools for Visual Studio is installed, you will see a **Data Lake** item in the **Tools** menu in Visual Studio:</span></span>

    ![U-SQL Visual Studio-menu](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* <span data-ttu-id="ed953-110">**Basiskennis van Data Lake Analytics en Data Lake Tools voor Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="ed953-110">**Basic knowledge of Data Lake Analytics and the Data Lake Tools for Visual Studio**.</span></span> <span data-ttu-id="ed953-111">Zie het volgende om te beginnen:</span><span class="sxs-lookup"><span data-stu-id="ed953-111">To get started, see:</span></span>

  * <span data-ttu-id="ed953-112">[U-SQL-script met Data Lake tools voor Visual Studio ontwikkelen](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-112">[Develop U-SQL script using Data Lake tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="ed953-113">**Een Data Lake Analytics-account.**</span><span class="sxs-lookup"><span data-stu-id="ed953-113">**A Data Lake Analytics account.**</span></span>  <span data-ttu-id="ed953-114">Zie [een Azure Data Lake Analytics-account maken](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-114">See [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md).</span></span>
* <span data-ttu-id="ed953-115">**Upload de voorbeeldgegevens naar het Data Lake Analytics-account.**</span><span class="sxs-lookup"><span data-stu-id="ed953-115">**Upload the sample data to the Data Lake Analytics account.**</span></span> <span data-ttu-id="ed953-116">Zie [kopiëren van bestanden met voorbeeldgegevens](data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-116">See [To copy sample data files](data-lake-analytics-get-started-portal.md).</span></span>

    <span data-ttu-id="ed953-117">Om een Data Lake Analytics-taak uit te voeren, hebt u enkele gegevens nodig.</span><span class="sxs-lookup"><span data-stu-id="ed953-117">To run a Data Lake Analytics job, you will need some data.</span></span> <span data-ttu-id="ed953-118">Hoewel Data Lake Tools ondersteuning biedt voor het uploaden van gegevens, gebruikt u de portal om de voorbeeldgegevens te uploaden. Zo is deze zelfstudie gemakkelijker te volgen.</span><span class="sxs-lookup"><span data-stu-id="ed953-118">Even though the Data Lake Tools supports uploading data, you will use the portal to upload the sample data to make this tutorial easier to follow.</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="ed953-119">Verbinding maken met Azure</span><span class="sxs-lookup"><span data-stu-id="ed953-119">Connect to Azure</span></span>
<span data-ttu-id="ed953-120">Voordat u kunt bouwen en testen van de U-SQL-scripts, moet u eerst verbinding met Azure.</span><span class="sxs-lookup"><span data-stu-id="ed953-120">Before you can build and test any U-SQL scripts, you must first connect to Azure.</span></span>

<span data-ttu-id="ed953-121">**Verbinding maken met Data Lake Analytics**</span><span class="sxs-lookup"><span data-stu-id="ed953-121">**To connect to Data Lake Analytics**</span></span>

1. <span data-ttu-id="ed953-122">Open Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ed953-122">Open Visual Studio.</span></span>
2. <span data-ttu-id="ed953-123">Klik op **Data Lake > Opties en instellingen**.</span><span class="sxs-lookup"><span data-stu-id="ed953-123">Click **Data Lake > Options and Settings**.</span></span>
3. <span data-ttu-id="ed953-124">Klik op **aanmelden**, of **gebruiker wijzigen** als iemand anders heeft aangemeld en volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="ed953-124">Click **Sign In**, or **Change User** if someone has signed in, and follow the instructions.</span></span>
4. <span data-ttu-id="ed953-125">Klik op **OK** om het dialoogvenster Opties en instellingen te sluiten.</span><span class="sxs-lookup"><span data-stu-id="ed953-125">Click **OK** to close the Options and Settings dialog.</span></span>

<span data-ttu-id="ed953-126">**Om te bladeren van uw Data Lake Analytics-accounts**</span><span class="sxs-lookup"><span data-stu-id="ed953-126">**To browse your Data Lake Analytics accounts**</span></span>

1. <span data-ttu-id="ed953-127">Open in Visual Studio **Server Explorer** door press **CTRL + ALT + S**.</span><span class="sxs-lookup"><span data-stu-id="ed953-127">From Visual Studio, open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
2. <span data-ttu-id="ed953-128">Vouw in **Server Explorer** achtereenvolgens **Azure** en **Data Lake Analytics** uit.</span><span class="sxs-lookup"><span data-stu-id="ed953-128">From **Server Explorer**, expand **Azure**, and then expand **Data Lake Analytics**.</span></span> <span data-ttu-id="ed953-129">U ziet een lijst met uw Data Lake Analytics-accounts, als u die hebt.</span><span class="sxs-lookup"><span data-stu-id="ed953-129">You shall see a list of your Data Lake Analytics accounts if there are any.</span></span> <span data-ttu-id="ed953-130">U kunt vanuit de studio Data Lake Analytics-accounts maken.</span><span class="sxs-lookup"><span data-stu-id="ed953-130">You cannot create Data Lake Analytics accounts from the studio.</span></span> <span data-ttu-id="ed953-131">Zie [Aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md) of [Aan de slag met Azure Data Lake Analytics met Azure PowerShell](data-lake-analytics-get-started-powershell.md) voor meer informatie over het maken van een account.</span><span class="sxs-lookup"><span data-stu-id="ed953-131">To create an account, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md) or [Get Started with Azure Data Lake Analytics using Azure PowerShell](data-lake-analytics-get-started-powershell.md).</span></span>

## <a name="develop-u-sql-application"></a><span data-ttu-id="ed953-132">U-SQL-toepassing ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ed953-132">Develop U-SQL application</span></span>
<span data-ttu-id="ed953-133">Een U-SQL-toepassing is meestal een U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="ed953-133">A U-SQL application is mostly a U-SQL script.</span></span> <span data-ttu-id="ed953-134">Zie voor meer informatie over U-SQL, [aan de slag met U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-134">To learn more about U-SQL, see [Get started with U-SQL](data-lake-analytics-u-sql-get-started.md).</span></span>

<span data-ttu-id="ed953-135">U kunt de gebruiker gedefinieerde operators toevoeging toevoegen aan de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ed953-135">You can add addition user-defined operators to the application.</span></span>  <span data-ttu-id="ed953-136">Zie voor meer informatie [ontwikkelen van U-SQL door de gebruiker gedefinieerde operators voor Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-136">For more information, see [Develop U-SQL user defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>

<span data-ttu-id="ed953-137">**Een Data Lake Analytics-taak maken en verzenden**</span><span class="sxs-lookup"><span data-stu-id="ed953-137">**To create and submit a Data Lake Analytics job**</span></span>

1. <span data-ttu-id="ed953-138">Klik op de **bestand > Nieuw > Project**.</span><span class="sxs-lookup"><span data-stu-id="ed953-138">Click the **File > New > Project**.</span></span>
2. <span data-ttu-id="ed953-139">Selecteer het type Project U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ed953-139">Select the U-SQL Project type.</span></span>

    ![nieuw U-SQL Visual Studio-project](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. <span data-ttu-id="ed953-141">Klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="ed953-141">Click **OK**.</span></span> <span data-ttu-id="ed953-142">Visual studio maakt een oplossing met een bestand Script.usql.</span><span class="sxs-lookup"><span data-stu-id="ed953-142">Visual studio creates a solution with a Script.usql file.</span></span>
4. <span data-ttu-id="ed953-143">Voer het volgende script in het bestand Script.usql:</span><span class="sxs-lookup"><span data-stu-id="ed953-143">Enter the following script into the Script.usql file:</span></span>

        // Create a database for easy reuse, so you don't need to read from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from the weblog file with the correct schema.
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

    <span data-ttu-id="ed953-144">Zie voor informatie over de U-SQL, [aan de slag met Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-144">To understand the U-SQL, see [Get started with Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>    
5. <span data-ttu-id="ed953-145">Een nieuw U-SQL-script toevoegen aan uw project en voer de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="ed953-145">Add a new U-SQL script to your project and enter the following:</span></span>

        // Query the referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        TO @"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. <span data-ttu-id="ed953-146">Schakel terug naar het eerste U-SQL-script en vervolgens naar de **indienen** knop, geeft u uw Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="ed953-146">Switch back to the first U-SQL script and next to the **Submit** button, specify your Analytics account.</span></span>
7. <span data-ttu-id="ed953-147">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Build Script**.</span><span class="sxs-lookup"><span data-stu-id="ed953-147">From **Solution Explorer**, right click **Script.usql**, and then click **Build Script**.</span></span> <span data-ttu-id="ed953-148">Controleer de resultaten in het deelvenster Uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ed953-148">Verify the results in the Output pane.</span></span>
8. <span data-ttu-id="ed953-149">Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Submit Script**.</span><span class="sxs-lookup"><span data-stu-id="ed953-149">From **Solution Explorer**, right click **Script.usql**, and then click **Submit Script**.</span></span>
9. <span data-ttu-id="ed953-150">Controleer of de **Analytics-Account** is waar u de taak uitvoeren en klik vervolgens op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="ed953-150">Verify the **Analytics Account** is the one where you want to run the job, and then click **Submit**.</span></span> <span data-ttu-id="ed953-151">Het resultaat van het verzenden en de koppeling naar de taak zijn beschikbaar in het resultaatvenster van Data Lake Tools voor Visual Studio wanneer het verzenden is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ed953-151">Submission results and job link are available in the Data Lake Tools for Visual Studio Results window when the submission is completed.</span></span>
10. <span data-ttu-id="ed953-152">Wacht totdat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ed953-152">Wait until the job is completed successfully.</span></span>  <span data-ttu-id="ed953-153">Als de taak is mislukt, waarschijnlijk ontbreken het bronbestand.</span><span class="sxs-lookup"><span data-stu-id="ed953-153">If the job failed, it is most likely missing the source file.</span></span>  <span data-ttu-id="ed953-154">Zie de sectie vereisten van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ed953-154">Please see the Prerequisite section of this tutorial.</span></span> <span data-ttu-id="ed953-155">Zie voor aanvullende informatie voor probleemoplossing [Monitor en Azure Data Lake Analytics-taken oplossen](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="ed953-155">For additional troubleshooting information, see [Monitor and troubleshoot Azure Data Lake Analytics jobs](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).</span></span>

    <span data-ttu-id="ed953-156">Als de taak is voltooid, ziet u het volgende scherm:</span><span class="sxs-lookup"><span data-stu-id="ed953-156">When the job is completed, you shall see the following screen:</span></span>

    ![Data lake analytics analyseren weblogboeken websitelogboeken](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. <span data-ttu-id="ed953-158">Herhaal stap 7 - 10 voor **Script1.usql**.</span><span class="sxs-lookup"><span data-stu-id="ed953-158">Now repeat steps 7- 10 for **Script1.usql**.</span></span>

<span data-ttu-id="ed953-159">**De taakuitvoer weergeven**</span><span class="sxs-lookup"><span data-stu-id="ed953-159">**To see the job output**</span></span>

1. <span data-ttu-id="ed953-160">Ga naar **Server Explorer**, vouw **Azure** uit, vouw **Data Lake Analytics** uit, vouw uw Data Lake Analytics-account uit, vouw **Storage Accounts** uit, klik met de rechtermuisknop op het Data Lake Storage-standaardaccount en klik vervolgens op **Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ed953-160">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Storage Accounts**, right-click the default Data Lake Storage account, and then click **Explorer**.</span></span>
2. <span data-ttu-id="ed953-161">Dubbelklik op **voorbeelden** open de map en dubbelklikt u vervolgens op **uitvoer**.</span><span class="sxs-lookup"><span data-stu-id="ed953-161">Double-click **Samples** to open the folder, and then double-click **Outputs**.</span></span>
3. <span data-ttu-id="ed953-162">Dubbelklik op **UnsuccessfulResponsees.log**.</span><span class="sxs-lookup"><span data-stu-id="ed953-162">Double-click **UnsuccessfulResponsees.log**.</span></span>
4. <span data-ttu-id="ed953-163">U kunt ook het uitvoerbestand binnen de grafiekweergave van de taak dubbelklikken om gaat u rechtstreeks naar de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ed953-163">You can also double-click the output file inside the graph view of the job in order to navigate directly to the output.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed953-164">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ed953-164">See also</span></span>
<span data-ttu-id="ed953-165">Om aan de slag te gaan met Data Lake Analytics met verschillende hulpprogramma's, zie:</span><span class="sxs-lookup"><span data-stu-id="ed953-165">To get started with Data Lake Analytics using different tools, see:</span></span>

* [<span data-ttu-id="ed953-166">Aan de slag met Data Lake Analytics met Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ed953-166">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="ed953-167">Aan de slag met Data Lake Analytics met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ed953-167">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
* [<span data-ttu-id="ed953-168">Aan de slag met Data Lake Analytics met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="ed953-168">Get started with Data Lake Analytics using .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
