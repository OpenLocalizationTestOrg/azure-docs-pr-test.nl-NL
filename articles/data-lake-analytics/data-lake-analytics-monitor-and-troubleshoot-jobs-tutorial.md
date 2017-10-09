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
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Azure Data Lake Analytics-taken via Azure Portal oplossen
Meer informatie over hoe toouse hello Azure Portal tootroubleshoot Data Lake Analytics-taken.

In deze zelfstudie maakt u een ontbrekende bron bestand probleem instellen, en gebruikt hello Azure Portal tootroubleshoot Hallo probleem.

## <a name="submit-a-data-lake-analytics-job"></a>Een Data Lake Analytics-taak verzenden

Hallo volgende U-SQL-taak verzenden:

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
    
Hallo bronbestand gedefinieerd in het Hallo-script is **/Samples/Data/SearchLog.tsv1**, dit moet waar **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Hallo-taak oplossen

**toosee alle taken Hallo**

1. Hallo Azure-portal, klik op **Microsoft Azure** in de linkerbovenhoek Hallo.
2. Klik op de tegel Hallo met de naam van uw Data Lake Analytics-account.  Hallo taak overzicht wordt weergegeven op Hallo **Jobbeheer** tegel.

    ![Beheer van Azure Data Lake Analytics-taak](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    Hallo taak Management biedt u een overzicht van de taakstatus Hallo. Er is een mislukte taak.
3. Klik op Hallo **Jobbeheer** tegel toosee Hallo taken. Hallo-taken zijn onderverdeeld in **met**, **in de wachtrij geplaatst**, en **beëindigd**. U ziet de mislukte taak in Hallo **beëindigd** sectie. Het moet eerste certificaat in de lijst Hallo zijn. Wanneer u een groot aantal taken hebt, kunt u **Filter** toohelp u toolocate taken.

    ![Azure Data Lake Analytics-filter-taken](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Klik op de mislukte taak Hallo van Hallo lijst tooopen Hallo taakdetails in een nieuwe blade:

    ![Azure Data Lake Analytics taak is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Kennisgeving Hallo **opnieuw indienen** knop. Nadat u Hallo probleem hebt opgelost, kunt u de taak Hallo opnieuw indienen.
5. Klik op de gemarkeerde onderdeel van Hallo vorige schermafbeelding tooopen Hallo foutgegevens.  U ziet ongeveer als volgt:

    ![Azure Data Lake Analytics taakdetails is mislukt](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Het vertelt u Hallo bronmap is niet gevonden.
6. Klik op **Script dubbele**.
7. Update Hallo **FROM** pad toohello volgende:

    ' / Samples/Data/SearchLog.tsv '
8. Klik op **Taak verzenden**.

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Aan de slag met Azure Data Lake Analytics met Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Aan de slag met Azure Data Lake Analytics en U-SQL Visual Studio gebruiken](data-lake-analytics-u-sql-get-started.md)
* [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md)
