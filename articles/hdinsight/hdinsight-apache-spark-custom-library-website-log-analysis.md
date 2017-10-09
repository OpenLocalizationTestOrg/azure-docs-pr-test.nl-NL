---
title: websitelogboeken aaaAnalyze met Python-bibliotheken in Spark - Azure | Microsoft Docs
description: Deze laptop laat zien hoe de gegevens met een aangepaste bibliotheek met Spark op Azure HDInsight voor het vastleggen van tooanalyze.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a>Websitelogboeken analyseren met een aangepaste Python-bibliotheek met Spark-cluster in HDInsight

Deze laptop laat zien hoe de gegevens met een aangepaste bibliotheek met Spark in HDInsight voor het vastleggen van tooanalyze. de aangepaste bibliotheek Hello we gebruiken is een Python-bibliotheek aangeroepen **iislogparser.py**.

> [!TIP]
> Deze zelfstudie is ook beschikbaar als een Jupyter-notebook op een cluster Spark (Linux) die u in HDInsight maakt. Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren. tooperform hello zelfstudie uit binnen een laptop, een Spark-cluster maken, een Jupyter-notebook starten (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), en voer vervolgens de notebook Hallo **logboeken analyseren met behulp van een aangepaste library.ipynb Spark** onder Hallo  **PySpark** map.
>
>

**Vereisten:**

U moet Hallo volgende hebben:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="save-raw-data-as-an-rdd"></a>Onbewerkte gegevens opslaan als een RDD
In deze sectie gebruiken we Hallo [Jupyter](https://jupyter.org) laptop die is gekoppeld aan een Apache Spark-cluster in HDInsight toorun taken die uw onbewerkte voorbeeldgegevens verwerken en opslaan als een Hive-tabel. Hallo voorbeeldgegevens is een CSV-bestand (hvac.csv) beschikbaar in alle clusters standaard.

Nadat uw gegevens wordt opgeslagen als een Hive-tabel, in de volgende sectie Hallo er wordt verbinding gemaakt toohello Hive-tabel met BI-hulpprogramma's als Power BI en Tableau.

1. Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.   
2. Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   > [!NOTE]
   > U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Maak een nieuwe notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

    ![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Een nieuwe Jupyter-notebook maken")
4. Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.

    ![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Geef een naam voor de notebook Hallo")
5. Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet. Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert. U kunt starten door het Hallo-typen die vereist voor dit scenario zijn te importeren. Plak Hallo volgende codefragment in een lege cel en druk vervolgens op **SHIFT + ENTER**.

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. Maak een RDD Hallo logboek voorbeeldgegevens gebruikt al beschikbaar op Hallo-cluster. U toegang hebt tot Hallo-gegevens in die zijn gekoppeld aan het cluster op Hallo Hallo standaardopslagaccount **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. Haal die een voorbeeldlogboek ingesteld tooverify die Hallo vorige stap is voltooid.

        logs.take(5)

    U ziet een uitvoer vergelijkbare toohello volgende:

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a>Analyseren van gegevens aan het logboek met een aangepaste Python-bibliotheek
1. In bovenstaande Hallo uitvoer, de eerste paar regels Hallo Hallo koptekstgegevens opnemen en elke resterende regel overeenkomt met Hallo schema beschreven in deze header. Deze logboeken parseren kan ingewikkeld zijn. Ja, gebruiken we een aangepaste Python-bibliotheek (**iislogparser.py**) op die manier kunt dergelijke eenvoudiger logboeken parseren. Deze bibliotheek is standaard opgenomen in uw Spark-cluster in HDInsight op **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.

    Deze bibliotheek is echter niet in Hallo `PYTHONPATH` zodat we kan niet worden gebruikt door het gebruik van een instructie importeren zoals `import iislogparser`. toouse deze bibliotheek we tooall Hallo worker-knooppunten moet distribueren. Hallo volgende codefragment worden uitgevoerd.

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. `iislogparser`biedt een functie `parse_log_line` die retourneert `None` als een regel van een veldnamenrij is en een exemplaar van Hallo retourneert `LogLine` klasse als een regel worden ontdekt. Gebruik Hallo `LogLine` klasse tooextract Hallo alleen logboek regels uit Hallo RDD:

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. Ophalen van een aantal uitgepakte logboek regels tooverify die Hallo stap is voltooid.

       logLines.take(2)

   Hallo-uitvoer moet vergelijkbaar toohello volgende:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. Hallo `LogLine` op zijn beurt, is enkele nuttige methoden zoals klasse, `is_error()`, die of een logboekvermelding een foutcode heeft retourneert. Gebruik deze toocompute Hallo aantal fouten in Hallo uitgepakt logboek regels en meld u vervolgens alle Hallo fouten tooa ander bestand.

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   Hier ziet u uitvoer Hallo volgende:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. U kunt ook **Matplotlib** tooconstruct een visualisatie van Hallo-gegevens. Bijvoorbeeld, als u tooisolate Hallo oorzaak van aanvragen die gedurende lange tijd worden uitgevoerd wilt, kunt u toofind Hallo bestanden die Hallo gemiddeld tooserve voor de meeste tijd duren.
   Hallo codefragment onderstaande Hallo bovenste 25 resources die een aanvraag voor de meeste tijd tooserve duurde opgehaald.

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   Hier ziet u uitvoer Hallo volgende:

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. U kunt ook deze informatie in de vorm Hallo van tekent aanwezig. Als een eerste stap toocreate tekent laat het ons een tijdelijke tabel maakt **AverageTime**. Hallo tabel groepen Hallo registreert tijd toosee als er een ongebruikelijke latentiepieken op een willekeurig moment.

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. Vervolgens kunt u uitvoeren Hallo SQL query tooget na alle Hallo records in Hallo **AverageTime** tabel.

       %%sql -o averagetime
       SELECT * FROM AverageTime

   Hallo `%%sql` magic gevolgd door `-o averagetime` zorgt ervoor dat Hallo-uitvoer van Hallo query lokaal worden bewaard op Hallo Jupyter-server (meestal Hallo headnode van Hallo cluster). Hallo-uitvoer is doorgevoerd als een [Pandas](http://pandas.pydata.org/) dataframe Hello naam opgegeven **averagetime**.

   Hier ziet u uitvoer Hallo volgende:

   ![Uitvoer van de SQL-query](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "uitvoer van de SQL-query")

   Voor meer informatie over Hallo `%%sql` magic, Zie [Parameters ondersteund Hello %% sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).
7. U kunt nu Matplotlib gebruiken, een bibliotheek tooconstruct visualisatie van gegevens, toocreate tekent gebruikt. Omdat Hallo grafiek moet worden gemaakt van Hallo lokaal persistent **averagetime** dataframe, Hallo codefragment moet beginnen met Hallo `%%local` verwerkt Magic-pakket. Dit zorgt ervoor dat Hallo-code op Hallo Jupyter server lokaal wordt uitgevoerd.

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   Hier ziet u uitvoer Hallo volgende:

   ![Uitvoer Matplotlib](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib uitvoer")
8. Als u klaar bent met het uitvoeren van de toepassing hello moet afsluiten Hallo notebook toorelease Hallo resources. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**. Deze wordt afgesloten en sluiten Hallo notebook.

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
