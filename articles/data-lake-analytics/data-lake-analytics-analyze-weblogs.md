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
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Websitelogboeken analyseren met Azure Data Lake Analytics
Meer informatie over hoe tooanalyze websitelogboeken met behulp van Data Lake Analytics, vooral bij het vinden van welke verwijzingen is gedetecteerd fouten tijdens het toovisit Hallo website.

## <a name="prerequisites"></a>Vereisten
* **Visual Studio 2015 of Visual Studio 2013**.
* **[Data Lake Tools voor Visual Studio](http://aka.ms/adltoolsvs)**.

    Wanneer Data Lake Tools voor Visual Studio is geïnstalleerd, ziet u een **Data Lake** item in Hallo **extra** menu in Visual Studio:

    ![U-SQL Visual Studio-menu](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Basiskennis van Data Lake Analytics en Data Lake Tools voor Visual Studio Hallo**. tooget gestart, Zie:

  * [U-SQL-script met Data Lake tools voor Visual Studio ontwikkelen](data-lake-analytics-data-lake-tools-get-started.md).
* **Een Data Lake Analytics-account.**  Zie [een Azure Data Lake Analytics-account maken](data-lake-analytics-get-started-portal.md).
* **Hallo sample data toohello Data Lake Analytics-account uploaden.** Zie [bestanden met voorbeeldgegevens toocopy](data-lake-analytics-get-started-portal.md).

    een Data Lake Analytics-taak toorun, moet u enkele gegevens. Hoewel Hallo Data Lake Tools ondersteuning biedt voor uploaden van gegevens, gebruikt u Hallo portal tooupload Hallo sample data toomake deze zelfstudie gemakkelijker toofollow.

## <a name="connect-tooazure"></a>Verbinding maken met tooAzure
Voordat u kunt bouwen en testen van de U-SQL-scripts, moet u eerst tooAzure verbinden.

**tooconnect tooData Lake Analytics**

1. Open Visual Studio.
2. Klik op **Data Lake > Opties en instellingen**.
3. Klik op **aanmelden**, of **gebruiker wijzigen** als iemand heeft aangemeld en volg de instructies Hallo.
4. Klik op **OK** tooclose Hallo opties en instellingen dialoogvenster.

**toobrowse uw Data Lake Analytics-accounts**

1. Open in Visual Studio **Server Explorer** door press **CTRL + ALT + S**.
2. Vouw in **Server Explorer** achtereenvolgens **Azure** en **Data Lake Analytics** uit. U ziet een lijst met uw Data Lake Analytics-accounts, als u die hebt. U kunt vanuit Hallo studio Data Lake Analytics-accounts maken. toocreate een account, Zie [aan de slag met Azure Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md) of [aan de slag met Azure Data Lake Analytics met Azure PowerShell](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>U-SQL-toepassing ontwikkelen
Een U-SQL-toepassing is meestal een U-SQL-script. toolearn meer informatie over U-SQL, Zie [aan de slag met U-SQL](data-lake-analytics-u-sql-get-started.md).

U kunt aanvullende gebruiker gedefinieerde operators toohello toepassing toevoegen.  Zie voor meer informatie [ontwikkelen van U-SQL door de gebruiker gedefinieerde operators voor Data Lake Analytics-taken](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate en het verzenden van een Data Lake Analytics-taak**

1. Klik op Hallo **bestand > Nieuw > Project**.
2. Hallo-Project U-SQL-type selecteren.

    ![nieuw U-SQL Visual Studio-project](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Klik op **OK**. Visual studio maakt een oplossing met een bestand Script.usql.
4. Voer Hallo script in Hallo Script.usql-bestand te volgen:

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

    toounderstand hello U-SQL, Zie [aan de slag met Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).    
5. Voeg een nieuw U-SQL-script tooyour project en voer de volgende Hallo:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Ga terug toohello eerste U-SQL-script en volgende toohello **indienen** knop, geeft u uw Analytics-account.
7. Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Build Script**. Controleer of Hallo resulteert in het deelvenster Hallo-uitvoer.
8. Ga naar **Solution Explorer**, klik met de rechtermuisknop op **Script.usql** en klik vervolgens op **Submit Script**.
9. Controleer of Hallo **Analytics-Account** is Hallo één waar toorun Hallo taak en klik vervolgens op **indienen**. Resultaat van het verzenden en een koppeling naar de taak zijn beschikbaar in Hallo Data Lake Tools voor Visual Studio resultatenvenster wanneer Hallo verzenden is voltooid.
10. Wacht totdat het Hallo-taak is voltooid.  Als Hallo-taak is mislukt, waarschijnlijk ontbreken Hallo bronbestand.  Zie sectie voor vereisten Hallo van deze zelfstudie. Zie voor aanvullende informatie voor probleemoplossing [Monitor en Azure Data Lake Analytics-taken oplossen](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Wanneer het Hallo-taak is voltooid, ziet u Hallo scherm te volgen:

    ![Data lake analytics analyseren weblogboeken websitelogboeken](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Herhaal stap 7 - 10 voor **Script1.usql**.

**toosee hello taakuitvoer**

1. Van **Server Explorer**, vouw **Azure**, vouw **Data Lake Analytics**, vouw uw Data Lake Analytics-account, vouw **Opslagaccounts**, met de rechtermuisknop op Hallo standaard Data Lake Storage-account en klik vervolgens op **Explorer**.
2. Dubbelklik op **voorbeelden** tooopen Hallo map en dubbelklik vervolgens op **uitvoer**.
3. Dubbelklik op **UnsuccessfulResponsees.log**.
4. U kunt ook Hallo uitvoerbestand binnen Hallo grafiekweergave van Hallo taak in de volgorde toonavigate dubbelklikken direct toohello uitvoer.

## <a name="see-also"></a>Zie ook
tooget de slag met Data Lake Analytics met verschillende hulpprogramma's, Zie:

* [Aan de slag met Data Lake Analytics met Azure Portal](data-lake-analytics-get-started-portal.md)
* [Aan de slag met Data Lake Analytics met Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Aan de slag met Data Lake Analytics met .NET SDK](data-lake-analytics-get-started-net-sdk.md)
