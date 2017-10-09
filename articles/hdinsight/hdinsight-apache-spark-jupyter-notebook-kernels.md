---
title: aaaKernels voor Jupyter-notebook in Spark-clusters in Azure HDInsight | Microsoft Docs
description: Meer informatie over Hallo PySpark PySpark3 en Spark kernels voor Jupyter-notebook met Spark op Azure HDInsight-clusters.
keywords: jupyter-notebook in spark, jupyter spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Kernels voor Jupyter-notebook in Spark-clusters in Azure HDInsight 

HDInsight Spark-clusters bieden kernels die u met Jupyter-notebook in Spark Hallo gebruiken kunt voor het testen van uw toepassingen. Een kernel is een programma dat wordt uitgevoerd en interpreteert uw code. Er zijn drie kernels Hallo:

- **PySpark** - voor toepassingen die zijn geschreven in Python2
- **PySpark3** - voor toepassingen die zijn geschreven in Python3
- **Spark** - voor toepassingen die zijn geschreven in Scala

In dit artikel leert u hoe toouse deze kernels en Hallo voordelen van het gebruik ervan.

## <a name="prerequisites"></a>Vereisten

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Maken van een Jupyter-notebook in Spark HDInsight

1. Van Hallo [Azure-portal](https://portal.azure.com/), opent u het cluster.  Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) voor Hallo-instructies. Hallo-cluster wordt geopend in een nieuwe portalblade.

2. Van Hallo **snelle koppelingen** sectie, klikt u op **Cluster dashboards** tooopen hello **Cluster dashboards** blade.  Als er geen **snelkoppelingen**, klikt u op **overzicht** in Hallo linkermenu op Hallo-blade.

    ![Jupyter-notebook in Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Jupyter-notebook in Spark") 

3. Klik op **Jupyter-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.
   
   > [!NOTE]
   > U kunt ook Hallo Jupyter-notebook in Spark-cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Klik op **nieuw**, en klikt u ofwel **Pyspark**, **PySpark3**, of **Spark** toocreate een laptop. Hallo Spark kernel voor Scala-toepassingen, PySpark-kernel voor Python2 toepassingen en PySpark3 kernel voor Python3 toepassingen gebruiken.
   
    ![Kernels voor Jupyter-notebook in Spark](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "Kernels voor Jupyter-notebook in Spark") 

4. Een laptop wordt geopend met Hallo kernel die u hebt geselecteerd.

## <a name="benefits-of-using-hello-kernels"></a>Voordelen van het gebruik van Hallo kernels

Hier volgen enkele voordelen van het gebruik van Hallo nieuwe kernels op Jupyter-notebook op HDInsight Spark-clusters.

- **Voorinstelling contexten**. Met **PySpark**, **PySpark3**, of Hallo **Spark** kernels, hoeft u geen tooset Hallo Spark of Hive-contexten expliciet voordat u begint te werken met uw toepassingen. Dit zijn standaard beschikbaar. Deze contexten zijn:
   
   * **sc** : voor het Spark-context
   * **sqlContext** - voor Hive-context

    Dus hebt u geen instructies voor het toorun zoals Hallo tooset Hallo contexten te volgen:

        SC SparkContext('yarn-client') sqlContext = HiveContext(sc) =

    In plaats daarvan u rechtstreeks kunt Hallo voorinstelling contexten in uw toepassing.

- **Cel-magics**. Hallo PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt `%%` (bijvoorbeeld `%%MAGIC` <args>). Hallo magische opdracht moet worden Hallo eerste woord in een codecel en toestaan voor meerdere regels van inhoud. Hallo magische word moet Hallo eerste woord in Hallo cel. Alles voordat Hallo magic, zelfs opmerkingen toevoegen, veroorzaakt een fout.     Zie voor meer informatie over magics [hier](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Hallo bevat volgende tabel andere magics Hallo beschikbaar via Hallo kernels.

   | Verwerkt Magic-pakket | Voorbeeld | Beschrijving |
   | --- | --- | --- |
   | Help |`%%help` |Genereert een lijst met alle beschikbare Hallo-magics met voorbeeld en beschrijving |
   | Info |`%%info` |Sessie-informatie van uitvoer voor de huidige Livy eindpunt Hallo |
   | Configureren |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Hiermee configureert u Hallo parameters voor het maken van een sessie. vlag force Hallo (-f) is verplicht als een sessie al is gemaakt, waardoor die sessie Hallo is verwijderd en opnieuw gemaakt. Bekijk [van Livy POST /sessions aanvraagtekst](https://github.com/cloudera/livy#request-body) voor een lijst met geldige parameters op. Parameters moeten worden doorgegeven als een JSON-tekenreeks en moeten op de volgende regel Hallo na Hallo magic, zoals weergegeven in Hallo voorbeeldkolom. |
   | SQL |`%%sql -o <variable name>`<br> `SHOW TABLES` |Een Hive-query op Hallo sqlContext worden uitgevoerd. Als hello `-o` parameter is doorgegeven, Hallo resultaat van Hallo query wordt bewaard in Hallo %% lokale Python context als een [Pandas](http://pandas.pydata.org/) dataframe. |
   | lokale |`%%local`<br>`a=1` |Alle Hallo-code in de volgende regels wordt lokaal uitgevoerd. De sitecode moet geldige Python2 code zelfs ongeacht Hallo kernel die u gebruikt. Zo is, zelfs als u **PySpark3** of **Spark** kernels tijdens het maken van Hallo laptop, als u Hallo `%%local` magische in een cel, die cel moet alleen code bevatten, geldige Python2... |
   | logboeken |`%%logs` |Uitvoer Hallo logboeken voor de huidige Livy sessie Hallo. |
   | verwijderen |`%%delete -f -s <session number>` |Hiermee verwijdert u een bepaalde sessie van de huidige Livy eindpunt Hallo. Houd er rekening mee dat u Hallo-sessie die is gestart voor Hallo kernel zichzelf niet verwijderen. |
   | Opruimen |`%%cleanup -f` |Hiermee verwijdert u alle Hallo-sessies voor Hallo huidige Livy eindpunt, waaronder deze laptop-sessie. Hallo force vlag -f is verplicht. |

   > [!NOTE]
   > Bovendien toohello magics toegevoegd door de PySpark-kernel Hallo, u kunt ook Hallo [ingebouwde IPython magics](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics), inclusief `%%sh`. U kunt Hallo `%%sh` magic toorun scripts en codeblok op Hallo cluster headnode.
   >
   >
2. **Visualisatie automatisch**. Hallo **Pyspark** kernel visualiseren automatisch Hallo-uitvoer van Hive en SQL-query's. U kunt kiezen tussen verschillende soorten visualisaties, met inbegrip van de tabel, cirkel, regel, gebied, balk.

## <a name="parameters-supported-with-hello-sql-magic"></a>Parameters die worden ondersteund door hello %% sql verwerkt Magic-pakket
Hallo `%%sql` magic ondersteunt verschillende parameters kunt u toocontrol Hallo type uitvoer dat wordt weergegeven wanneer u query's uitvoeren. Hallo volgende tabel geeft een lijst Hallo uitvoer.

| Parameter | Voorbeeld | Beschrijving |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Gebruik deze parameter toopersist Hallo-resultaat van het Hallo-query in Hallo %% lokale Python-context, als een [Pandas](http://pandas.pydata.org/) dataframe. Hallo-naam van Hallo dataframe variabele is Hallo variabele naam die u opgeeft. |
| -q |`-q` |Gebruik deze tooturn uit visualisaties voor Hallo cel. Als u niet tooauto wilt-inhoud van een cel Hallo visualiseren en alleen wilt toocapture als een dataframe vervolgens gebruiken `-q -o <VARIABLE>`. Als u wilt dat tooturn uitschakelen visualisaties zonder Hallo resultaten opnemen (bijvoorbeeld voor het uitvoeren van een SQL-query, zoals een `CREATE TABLE` instructie), gebruik `-q` zonder op te geven een `-o` argument. |
| -m |`-m <METHOD>` |Waar **methode** is **nemen** of **voorbeeld** (standaardwaarde is **nemen**). Als u de methode Hallo **nemen**, Hallo kernel uitgelicht elementen vanaf de bovenkant Hallo van Hallo gegevens resultatenset opgegeven door MAXROWS (Zie verderop in deze tabel). Als u de methode Hallo **voorbeeld**, Hallo kernel willekeurig samples elementen van de set gegevens Hallo volgens te`-r` parameter hieronder wordt beschreven in deze tabel. |
| -r |`-r <FRACTION>` |Hier **FRACTIE** is een getal met drijvende komma tussen 0,0 en 1,0 liggen. Als Hallo voorbeeldmethode voor de SQL-query Hallo `sample`, en vervolgens Hallo kernel willekeurig samples Hallo opgegeven fractie van Hallo elementen van het Hallo-resultaat voor u ingesteld. Bijvoorbeeld, als u een SQL-query uitvoeren met Hallo argumenten `-m sample -r 0.01`, en vervolgens 1% van de Hallo Resultatenrijen willekeurig worden vastgelegd. |
| -n |`-n <MAXROWS>` |**MAXROWS** is een geheel getal. Hallo kernel beperkt het aantal rijen dat uitvoer hello te**MAXROWS**. Als **MAXROWS** is een negatief getal zoals **-1**, en vervolgens het aantal rijen in de resultatenset Hallo Hallo niet beperkt is. |

**Voorbeeld:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

Hallo-instructie hiervoor Hallo te volgen:

* Hiermee selecteert u alle records uit **hivesampletable**.
* Omdat we - q, schakelt automatisch visualisatie.
* Omdat we `-m sample -r 0.1 -n 500` het willekeurig 10% Hallo rijen in Hallo hivesampletable voorbeelden en limieten Hallo grootte van Hallo resultaat set too500 rijen.
* Ten slotte omdat we gebruikt `-o query2` Bovendien bespaart u Hallo-uitvoer in een dataframe aangeroepen **query2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Overwegingen bij het gebruik van nieuwe kernels Hallo

De kernel dat u gebruikt, verbruikt verlaten Hallo laptops met Hallo clusterbronnen.  Met deze kernels omdat Hallo contexten worden vooraf ingesteld, gewoon afgesloten Hallo notitieblokken Hallo context niet beëindigen en daarom Hallo clusterbronnen toobe blijven in gebruik. Het wordt aangeraden toouse hello **sluiten en stoppen** optie uit Hallo-notebook **bestand** menu wanneer u klaar bent met Hallo laptop, die is funest Hallo context en vervolgens uitgangen notebook Hallo.     

## <a name="show-me-some-examples"></a>Sommige voorbeelden weergeven

Als u een Jupyter-notebook opent, ziet u twee mappen op hoofdniveau Hallo beschikbaar.

* Hallo **PySpark** map bevat voorbeeldquery notitieblokken die gebruik Hallo nieuwe **Python** kernel.
* Hallo **Scala** map bevat voorbeeldquery notitieblokken die gebruik Hallo nieuwe **Spark** kernel.

U kunt openen Hallo **00 - [Lees mij eerst] Spark Magic Kernel-functies** notebook van Hallo **PySpark** of **Spark** map toolearn over andere magics Hallo beschikbaar. U kunt ook andere voorbeeldquery notitieblokken onder Hallo twee mappen toolearn hoe Hallo tooachieve verschillende scenario's met Jupyter-notebooks met HDInsight Spark-clusters.

## <a name="where-are-hello-notebooks-stored"></a>Waar kan ik Hallo notitieblokken opgeslagen?

Jupyter-notebooks toohello storage-account die is gekoppeld aan het cluster onder Hallo Hallo worden opgeslagen **/HdiNotebooks** map.  Notitieblokken, bestanden en mappen die u vanuit Jupyter maakt zijn toegankelijk is vanaf Hallo storage-account.  Bijvoorbeeld, als u Jupyter toocreate een map **mijnmap** en een laptop **myfolder/mynotebook.ipynb**, u toegang hebt tot die laptop `/HdiNotebooks/myfolder/mynotebook.ipynb` binnen Hallo-opslagaccount.  Hallo omgekeerde geldt ook, dat wil zeggen, als u een laptop uploadt direct tooyour storage-account op `/HdiNotebooks/mynotebook1.ipynb`, Hallo laptop evenals van Jupyter zichtbaar is.  Notitieblokken blijven in Hallo storage-account, zelfs nadat het Hallo-cluster is verwijderd.

Hallo manier notitieblokken toohello storage-account worden opgeslagen is compatibel met HDFS. Dus als u SSH in Hallo cluster die kunt u opdrachten voor het beheer zoals weergegeven in het volgende codefragment Hallo:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Als er problemen met toegang tot Hallo storage-account voor Hallo-cluster zijn, Hallo notitieblokken worden ook opgeslagen op Hallo headnode `/var/lib/jupyter`.

## <a name="supported-browser"></a>Ondersteunde browser

Jupyter-notebooks op HDInsight Spark-clusters worden alleen ondersteund op Google Chrome.

## <a name="feedback"></a>Feedback
nieuwe kernels Hallo zijn in de fase in ontwikkeling en zal vervallen gedurende een bepaalde periode. Dit kan ook betekenen dat API's wijzigen kan, omdat deze kernels vervallen. We zouden feedback die u hebt tijdens het gebruik van deze nieuwe kernels stellen. Dit is handig in Hallo definitieve versie van deze kernels vormgeven. U kunt feedback uw opmerkingen/onder Hallo **opmerkingen** sectie op Hallo onder aan dit artikel.

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
