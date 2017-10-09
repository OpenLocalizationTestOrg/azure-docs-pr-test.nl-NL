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
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>U-SQL-scripts ontwikkelen met Data Lake-tools voor Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Meer informatie over hoe definiëren toouse Visual Studio toocreate Azure Data Lake Analytics-accounts,-taken in [U-SQL](data-lake-analytics-u-sql-get-started.md), en het verzenden van taken toohello Data Lake Analytics-service. Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor meer informatie over Data Lake Analytics.


## <a name="prerequisites"></a>Vereisten

* **Visual Studio**: alle versies behalve Express worden ondersteund.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **Microsoft Azure SDK voor .NET** versie 2.7.1 of hoger.  Installeren met behulp van Hallo [webplatforminstallatieprogramma](http://www.microsoft.com/web/downloads/platform.aspx).
* Een **Data Lake Analytics**-account. toocreate een account, Zie [aan de slag met Azure Data Lake Analytics met Azure portal](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Azure Data Lake-tools voor Visual Studio installeren 

Download en installeer Azure Data Lake Tools voor Visual Studio [van Downloadcentrum Hallo](http://aka.ms/adltoolsvs). Na installatie moet u zich het volgende realiseren:
* Hallo **Server Explorer** > **Azure** knooppunt bevat een **Data Lake Analytics** knooppunt. 
* Hallo **extra** menu heeft een **Data Lake** item.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Tooan Azure Data Lake Analytics-account koppelen

1. Open Visual Studio.
2. Open Server Explorer via **Weergave** > **Server Explorer**.
3. Klik met de rechtermuisknop op **Azure**. Selecteer vervolgens **tooMicrosoft Azure-abonnement verbinden** en volg de instructies Hallo.
4. In Server Explorer selecteert u **Azure** > **Data Lake Analytics**. U ziet een lijst met uw Data Lake Analytics-accounts.


## <a name="write-your-first-u-sql-script"></a>Uw eerste U-SQL-script schrijven

na de tekst Hello is een eenvoudige U-SQL-script. Definieert een kleine gegevensset- en schrijfbewerkingen die gegevensset toohello default Data Lake Store als een bestand aangeroepen `/data.csv`.

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

### <a name="submit-a-data-lake-analytics-job"></a>Een Data Lake Analytics-taak verzenden

1. Selecteer **Bestand** > **Nieuw** > **Project**.

2. Selecteer Hallo **U-SQL Project** Typ en klik op **OK**. Visual Studio maakt een oplossing met een **Script.usql**-bestand.

3. Hallo vorige script in Hallo plakken **Script.usql** venster.

4. In Hallo linkerbovenhoek Hallo **Script.usql** venster Hallo Data Lake Analytics-account opgeven.

    ![U-SQL Visual Studio-project verzenden](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. In Hallo linkerbovenhoek Hallo **Script.usql** Selecteer **indienen**.
6. Controleer of Hallo **Analytics-Account**, en selecteer vervolgens **indienen**. Verzending van resultaten zijn beschikbaar in Hallo Data Lake Tools voor Visual Studio-resultaten nadat Hallo verzending voltooid is.

    ![U-SQL Visual Studio-project verzenden](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello meest recente taak status en vernieuw welkomstscherm, klikt u op **vernieuwen**. Wanneer het Hallo-taak is voltooid, wordt een melding weergegeven Hallo **Taakgrafiek**, **bewerkingen voor metagegevens**, **State History**, en **Diagnostics**:

    ![Prestatiegrafiek U-SQL Visual Studio Data Lake Analytics-taak](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Taak samenvatting** geeft samenvatting van de taak Hallo Hallo.   
   * **Taakdetails** bevat meer informatie over het Hallo-taak, waaronder script hello, bronnen en hoekpunten.
   * **Taakgrafiek** Hallo voortgang van Hallo taak visualiseren.
   * **Bewerkingen voor metagegevens** toont alle Hallo-acties die zijn uitgevoerd op Hallo U-SQL-catalogus.
   * **Gegevens** ziet u alle Hallo invoer en uitvoer.
   * **Diagnostische gegevens** biedt een geavanceerde analyse van de taakuitvoering en de prestatieoptimalisatie.

### <a name="toocheck-job-state"></a>toocheck taakstatus

1. In Server Explorer selecteert u **Azure** > **Data Lake Analytics**. 
2. Vouw Hallo Data Lake Analytics-accountnaam.
3. Dubbelklik op **Taken**.
4. Selecteer Hallo-taak die u eerder hebt verzonden.

### <a name="toosee-hello-output-of-a-job"></a>toosee hello uitvoer van een taak

1. Blader in Server Explorer toohello taak die u hebt ingediend.
2. Klik op Hallo **gegevens** tabblad.
3. In Hallo **taak uitvoer** tabblad, selecteer Hallo `"/data.csv"` bestand.

## <a name="next-steps"></a>Volgende stappen

* [U-SQL-scripts uitvoeren op uw eigen werkstation voor tests en foutopsporing](data-lake-analytics-data-lake-tools-local-run.md)
* [Problemen met C#-code oplossen in U-SQL-taken](data-lake-analytics-debug-u-sql-jobs.md)
* [Hello Azure Data Lake Tools voor Visual Studio Code gebruiken](data-lake-analytics-data-lake-tools-for-vscode.md)
