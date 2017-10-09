---
title: aaaSpark BI hulpmiddelen voor gegevensvisualisatie met op Azure HDInsight | Microsoft Docs
description: Hulpmiddelen voor gegevensvisualisatie voor analyses met Apache Spark BI op HDInsight-clusters gebruiken
keywords: Apache spark bi, spark bi, spark gegevensvisualisatie, spark business intelligence
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark BI hulpmiddelen voor gegevensvisualisatie gebruiken met Azure HDInsight

Meer informatie over hoe toouse gegevensvisualisatie hulpmiddelen zoals Power BI en Tableau tooanalyze een onbewerkte voorbeeldgegevensset met BI van Apache Spark in HDInsight-clusters.

> [!NOTE]
> Connectiviteit met BI-tools die worden beschreven in dit artikel wordt niet ondersteund op 2.1 Spark op Azure HDInsight 3.6 Preview. Alleen Spark versie 1.6 en 2.0 (HDInsight 3.4 3.5 respectievelijk) worden ondersteund.
>

Deze zelfstudie is ook beschikbaar als een Jupyter-notebook in een HDInsight Spark-cluster. Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren. tooperform hello zelfstudie uit binnen een laptop, een Spark-cluster maken, een Jupyter-notebook starten (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), en voer vervolgens de notebook Hallo **gebruik BI-tools met Apache Spark in HDInsight.ipynb** onder Hallo **Python**  map.

## <a name="prerequisites"></a>Vereisten

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Gegevens voorbereiden voor Spark gegevensvisualisatie

In deze sectie gebruiken we Hallo [Jupyter](https://jupyter.org) laptop van een HDInsight Spark-cluster toorun taken die uw onbewerkte voorbeeldgegevens en deze opslaan in een tabel. Hallo voorbeeldgegevens is een CSV-bestand (hvac.csv) beschikbaar in alle clusters standaard. Wanneer uw gegevens wordt opgeslagen als een tabel, in de volgende sectie Hallo we gebruik BI extra tooconnect toohello tabel en gegevensvisualisaties uitvoeren.

> [!NOTE]
> Als u uitvoert Hallo stappen in dit artikel na het voltooien van de instructies in Hallo [interactieve query's uitvoeren op een HDInsight Spark-cluster](hdinsight-apache-spark-load-data-run-query.md), kunt u tooStep 8 hieronder overslaan.
>

1. Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   

2. Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   > [!NOTE]
   > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Maak een notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

    ![Een Jupyter-notebook maken voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "een Jupyter-notebook maken voor Apache Spark BI")

4. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.

    ![Geef een naam voor de notebook Hallo voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "Geef een naam voor de notebook Hallo voor Apache Spark BI")

5. Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert. U kunt starten door het Hallo-typen die nodig zijn voor dit scenario te importeren. Hallo cursor toodo dus plaats in Hallo cel en druk op **SHIFT + ENTER**.

        from pyspark.sql import *

6. Laad voorbeeldgegevens in een tijdelijke tabel. Wanneer u een Spark-cluster in HDInsight, Hallo voorbeeldgegevensbestand, maakt **hvac.csv**, is het opslagaccount gekopieerde toohello gekoppeld onder **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    In een lege cel, plak Hallo volgende codefragment en druk op **SHIFT + ENTER**. In dit fragment Hallo gegevens geregistreerd in een tabel met de naam **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))

        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Controleer of dat deze Hallo-tabel is gemaakt. U kunt Hallo `%%sql` toorun Hive-query's rechtstreeks magic. Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Ziet u uitvoer zoals hieronder weergegeven:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Alleen Hallo tabellen waarvoor false onder Hallo **isTemporary** kolom hive-tabellen die zijn opgeslagen in het Hallo-metastore en toegankelijk zijn vanuit Hallo BI-hulpprogramma's zijn. In deze zelfstudie we verbinding maken met toohello **hvac** tabel is gemaakt.

8. Controleren of dat deze tabel Hallo Hallo bedoeld gegevens bevat. Kopieer in een lege cel in de notebook Hallo Hallo volgende codefragment en druk op **SHIFT + ENTER**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Hallo-notebook toorelease Hallo resources afgesloten. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.

## <a name="powerbi"></a>Gebruik Power BI voor Spark gegevensvisualisatie

> [!NOTE]
> Deze sectie geldt alleen voor Spark 1.6 op HDInsight 3.4 en Spark 2.0 op HDInsight 3.5.
>
>

Wanneer u Hallo gegevens hebt opgeslagen als een tabel, kunt u Power BI tooconnect toohello gegevens gebruiken en deze toocreate rapporten, visualiseren dashboards, enzovoort.

1. Zorg ervoor dat u hebt toegang tooPower BI. U krijgt een abonnement gratis preview van Power BI van [http://www.powerbi.com/](http://www.powerbi.com/).

2. Aanmelden te[Power BI](http://www.powerbi.com/).

3. Hallo onder aan het linkerdeelvenster hello, klik op **gegevens ophalen**.

4. Op Hallo **gegevens ophalen** pagina onder **importeren of verbinding maken tooData**, voor **Databases**, klikt u op **ophalen**.

    ![Ophalen van gegevens in Power BI voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "gegevens in Power BI voor Apache Spark BI ophalen")

5. Klik op volgende welkomstscherm **Spark op Azure HDInsight** en klik vervolgens op **Connect**. Voer desgevraagd Hallo cluster-URL (`mysparkcluster.azurehdinsight.net`) en Hallo referenties tooconnect toohello cluster.

    ![Verbinding maken met tooApache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI verbinding")

    Na het Hallo-verbinding tot stand is gebracht, wordt in Power BI start importeren van gegevens uit Hallo Spark-cluster in HDInsight.

6. Power BI Hallo gegevens worden geïmporteerd en voegt een **Spark** gegevensset onder Hallo **gegevenssets** kop. Klik op Hallo gegevensset tooopen een nieuw werkblad toovisualize Hallo-gegevens. U kunt ook Hallo werkblad opslaan als een rapport. een werkblad van Hallo toosave **bestand** menu, klikt u op **opslaan**.

    ![Apache Spark BI-tegel in Power BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Apache Spark BI-tegel in Power BI-dashboard")
7. U ziet dat Hallo **velden** lijst aan de rechterkant Hallo Hallo bevat **hvac** tabel die u eerder hebt gemaakt. Vouw Hallo tabel toosee Hallo velden in de tabel hello, zoals u eerder in de notebook hebt gedefinieerd.

      ![Lijst met tabellen op Apache Spark BI-dashboard](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "lijst tabellen op de Apache Spark BI-dashboard")

8. Bouw een visualisatie tooshow Hallo verschil tussen doel temperatuur- en werkelijke temperatuur voor elk gebouw. gegevens van toovisualize wilt, schakelt u **vlakdiagram** (weergegeven in rood kader). slepen en neerzetten Hallo-as Hallo toodefine **BuildingID** veld onder **as**, en **ActualTemp**/**TargetTemp** velden onder **waarde**.

    ![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")

9. Standaard bevat Hallo visualisatie Hallo som voor **ActualTemp** en **TargetTemp**. Selecteer voor beide velden uit de vervolgkeuzelijst Hallo Hallo **gemiddelde** tooget gemiddeld werkelijke en doel temperaturen voor beide gebouwen.

    ![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")

10. Uw gegevensvisualisatie moet vergelijkbaar toohello in Hallo schermafbeelding. Plaats de cursor op Hallo visualisatie tooget knopinfo met relevante gegevens.

    ![Spark maken met behulp van Apache Spark BI gegevensvisualisaties](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "gegevensvisualisaties Spark maken met behulp van Apache Spark BI")

11. Klik op **opslaan** van Hallo bovenste menu en geef de rapportnaam van een. U kunt ook visual Hallo vastmaken. Wanneer u een visualisatie vastmaken, wordt opgeslagen op uw dashboard zodat u de laatste waarde in een oogopslag Hallo kunt bijhouden.

   U kunt zoveel visualisaties als u wilt voor toevoegen Hallo dezelfde gegevensset en een pincode ze toohello dashboard voor een momentopname van uw gegevens. Spark-clusters in HDInsight zijn ook verbonden tooPower BI met direct connect. Dit zorgt ervoor dat Power BI altijd Hallo de meeste recente gegevens van uw cluster heeft zodat u geen tooschedule wordt vernieuwd voor Hallo gegevensset hoeft.

## <a name="tableau"></a>Tableau bureaublad gebruiken voor Spark gegevensvisualisatie

> [!NOTE]
> Deze sectie geldt alleen voor 1.5.2 Spark-clusters die zijn gemaakt in Azure HDInsight.
>
>

1. Installeer [Tableau bureaublad](http://www.tableau.com/products/desktop) op Hallo-computer waarop u deze zelfstudie voor Apache Spark BI uitvoert.

2. Zorg ervoor dat deze computer ook Microsoft Spark ODBC-stuurprogramma geïnstalleerd. U kunt installeren stuurprogramma Hallo van [hier](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Start Tableau bureaublad. Klik in het linkerdeelvenster Hallo uit de lijst Hallo van server tooconnect, **Spark SQL**. Als Spark SQL niet wordt weergegeven in het linkerdeelvenster Hallo standaard, kunt u deze vinden door te klikken op **meer Servers**.
2. Hallo Spark SQL-verbinding in het dialoogvenster, Hallo waarden zoals weergegeven in de schermafbeelding hello, op en klik vervolgens op **OK**.

    ![Verbinding maken met tooa cluster voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Connect tooa cluster voor Apache Spark BI")

    Hallo verificatie vervolgkeuzelijsten **Microsoft Azure HDInsight-Service** als optie alleen als u Hallo geïnstalleerd [ODBC-stuurprogramma van Microsoft Spark](http://go.microsoft.com/fwlink/?LinkId=616229) op Hallo-computer.
3. Op de volgende scherm Hallo van Hallo **Schema** omlaag, klikt u op Hallo **vinden** pictogram en klik vervolgens op **standaard**.

    ![Schema voor Apache Spark BI vinden](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "schema voor Apache Spark BI zoeken")
4. Voor Hallo **tabel** veld, klikt u op Hallo **vinden** pictogram opnieuw toolist alle Hallo Hive-tabellen die beschikbaar zijn in het Hallo-cluster. U ziet Hallo **hvac** tabel eerder met Hallo laptop hebt gemaakt.

    ![Tabel niet vinden voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "tabel voor Apache Spark BI zoeken")
5. Slepen en neerzetten Hallo tabel toohello bovenste vak op Hallo rechts. Tableau hello gegevens worden geïmporteerd en worden Hallo schema als gemarkeerde door Hallo rood kader weergegeven.

    ![Tabellen tooTableau toevoegen voor Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "tabellen tooTableau voor Apache Spark BI toevoegen")
6. Klik op Hallo **Sheet1** op Hallo linksonder tabblad. Controleer een visualisatie waarin Hallo gemiddelde doel en de werkelijke temperaturen voor alle gebouwen voor elke datum. Sleep **datum** en **gebouw-ID** te**kolommen** en **werkelijke Temp**/**doel Temp**te**rijen**. Onder **aanhalingstekens**, selecteer **gebied** toouse voor Spark gegevensvisualisatie een toewijzing van gebied.

     ![Toevoegen van velden voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "velden voor Spark gegevensvisualisatie toevoegen")
7. Standaard Hallo temperatuur velden worden weergegeven als de statistische functie. Als u in plaats daarvan tooshow Hallo gemiddelde temperatuur wilt, kunt u doen in vervolgkeuzelijst hello, zoals hieronder wordt weergegeven.

    ![Gemiddelde temperatuur voor Spark gegevensvisualisatie nemen](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "gemiddelde temperatuur voor Spark gegevensvisualisatie duren")

8. U kunt ook super-opleggen één temperatuur kaart Hallo meer dan andere tooget een beter idee van verschil tussen het doel en de werkelijke temperaturen. Hallo muis toohello hoek van Hallo lagere gebied kaart verplaatsen totdat u Hallo ingang shape gemarkeerd in een rode cirkel wordt weergegeven. Sleep Hallo toewijzen toohello andere kaart op Hallo boven- en release Hallo muis wanneer er Hallo vorm in rode rechthoek gemarkeerd.

    ![Samenvoegen van kaarten voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "samenvoegen toegewezen voor Spark gegevensvisualisatie")

     De weergave van uw gegevens moet wijzigen, zoals weergegeven in de schermafbeelding Hallo:

    ![Tableau uitvoer voor Spark gegevensvisualisatie](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau uitvoer voor Spark gegevensvisualisatie")
9. Klik op **opslaan** toosave Hallo werkblad. U kunt dashboards maken en toevoegen van een of meer werkbladen tooit.

## <a name="next-steps"></a>Volgende stappen

Tot nu toe hebt u geleerd hoe toocreate een cluster, Spark gegevens frames tooquery gegevens maken en vervolgens toegang tot die gegevens vanuit BI-tools. U kunt nu zoeken op instructies over hoe toomanage Hallo clusterbronnen en taken die worden uitgevoerd in een HDInsight Spark-cluster voor foutopsporing.

* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

