---
title: aaaIntroduction tooSpark in Azure HDInsight | Microsoft Docs
description: Dit artikel bevat een inleiding tooSpark op HDInsight en Hallo verschillende scenario's waarin u Spark-cluster in HDInsight kunt gebruiken.
keywords: Wat is apache spark, spark-cluster, inleiding toospark, spark in hdinsight
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Inleiding tooSpark in HDInsight

In dit artikel biedt een inleiding tooSpark op HDInsight. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> is een parallelle verwerking van open-source framework die ondersteuning biedt voor in het geheugen verwerkingsprestaties tooboost Hallo van analytische big data-toepassingen. Spark-cluster in HDInsight is compatibel met Azure Storage (WASB) en met Azure Data Lake Store. Uw bestaande gegevens die zijn opgeslagen in Azure, kunnen dus eenvoudig worden verwerkt met behulp van een Spark-cluster.

Wanneer u Spark-cluster in HDInsight maakt, maakt u Azure-rekenresources met Spark geïnstalleerd en geconfigureerd. Het duurt ongeveer tien minuten toocreate een Spark-cluster in HDInsight. Hallo gegevens toobe verwerkt wordt opgeslagen in Azure Storage of Azure Data Lake Store. Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md).

**toocreate een Spark-cluster in HDInsight**, Zie [Snelstartgids: een Spark-cluster in HDInsight maken en uitvoeren van interactieve query met Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Wat is Apache Spark in Azure HDInsight?
Spark-clusters in HDInsight bieden een volledig beheerde Spark-service. Hier worden de voordelen vermeld van het maken van een Spark-cluster in HDInsight.

| Functie | Beschrijving |
| --- | --- |
| Het gemak van het maken van Spark-clusters |U kunt een nieuw Spark-cluster in HDInsight maken in minuten met hello Azure Portal, Azure PowerShell of Hallo HDInsight .NET SDK. Zie [Aan de slag met Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Gebruiksgemak |Spark-cluster in HDInsight bevat Jupyter- en Zeppelin-notebooks. U kunt deze voor de interactieve gegevensverwerking en -visualisatie gebruiken.|
| REST-API’s |Spark-clusters in HDInsight bevatten [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), op basis van REST-API Spark taak server tooremotely verzenden en te bewaken taken. |
| Ondersteuning voor Azure Data Lake Store | Spark-cluster in HDInsight kan worden geconfigureerd toouse Azure Data Lake Store als een extra opslagruimte, evenals de primaire opslag (alleen met 3.5 HDInsight-clusters). Zie [Overzicht van Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md) voor meer informatie over Data Lake Store. |
| Integratie met Azure-services |Spark-cluster in HDInsight wordt geleverd met een connector tooAzure Event Hubs. Klanten kunnen streamingtoepassingen met behulp van Hallo Event Hubs, daarnaast te bouwen[Kafka](http://kafka.apache.org/), die al beschikbaar is als onderdeel van Spark. |
| Ondersteuning voor R Server | U kunt een R Server op een HDInsight Spark cluster toorun R-berekeningen met Hallo snelheden die worden toegezegd voor een Spark-cluster gedistribueerde instellen. Zie [Aan de slag met R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md) voor meer informatie. |
| Integratie met IDE's van derden | HDInsight biedt invoegtoepassingen voor IDE zoals IntelliJ IDEA en Eclipse toocreate gebruiken en dienen toepassingen tooan HDInsight Spark-cluster. Zie [Azure-toolkit voor IntelliJ IDEA gebruiken](hdinsight-apache-spark-intellij-tool-plugin.md) en [Azure-toolkit voor Eclipse gebruiken](hdinsight-apache-spark-eclipse-tool-plugin.md) voor meer informatie.|
| Gelijktijdige query's |Spark-clusters in HDInsight ondersteunen gelijktijdige query's. Hierdoor kunnen meerdere query's van één gebruiker of meerdere query's van verschillende gebruikers en tooshare toepassingen dezelfde clusterresources Hallo. |
| Opslaan in cache in SSD's |U kunt kiezen om toocache gegevens in het geheugen of in SSD's gekoppeld toohello clusterknooppunten. Cachen in het geheugen biedt de beste queryprestaties hello, maar kan duur zijn. cachen in SSD's biedt een goede optie voor het verbeteren van de prestaties van query's zonder Hallo nodig toocreate een cluster met een grootte die is vereist toofit Hallo volledige gegevensset in het geheugen. |
| Integratie met BI-tools |Spark-clusters voor HDInsight bieden connectors voor BI-tools zoals [Power BI](http://www.powerbi.com/) en [Tableau](http://www.tableau.com/products/desktop) voor gegevensanalyse. |
| Vooraf geladen Anaconda-bibliotheken |Spark-clusters in HDInsight worden geleverd met Anaconda-bibliotheken die vooraf zijn geïnstalleerd. [Anaconda](http://docs.continuum.io/anaconda/) biedt sluiten too200 bibliotheken voor machine learning, data-analyse, visualisatie, enzovoort. |
| Schaalbaarheid |Maar u Hallo aantal knooppunten in het cluster tijdens het maken opgeven kunt, u wilt toogrow of Hallo toomatch clusterbelasting verkleinen. Alle HDInsight-clusters kunnen u toochange Hallo aantal knooppunten in het Hallo-cluster. Bovendien kunnen Spark-clusters zonder verlies van gegevens worden verwijderd omdat alle Hallo-gegevens worden opgeslagen in Azure Storage of de Data Lake Store. |
| 24/7 ondersteuning |Spark-clusters in HDInsight worden geleverd met 24/7 ondersteuning op bedrijfsniveau en een SLA met 99,9% beschikbaarheid. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Wat zijn Hallo gebruiksvoorbeelden voor Spark in HDInsight?
Spark-clusters in HDInsight inschakelen Hallo belangrijke scenario's te volgen.

### <a name="interactive-data-analysis-and-bi"></a>Interactieve gegevensanalyse en BI
[Bekijk een zelfstudie](hdinsight-apache-spark-use-bi-tools.md)

Met Apache Spark in HDInsight worden gegevens opgeslagen in Azure Storage of Azure Data Lake Store. Zakelijke deskundigen en besluitvormers kunnen analyseren en rapporten maken die gegevens en gebruiken van Microsoft Power BI toobuild interactieve rapporten van Hallo geanalyseerde gegevens. Analisten kunnen starten vanuit een niet-gestructureerde/semi-gestructureerde gegevens in de clusteropslag, een schema voor Hallo-gegevens met behulp van notebooks definiëren en vervolgens gegevensmodellen bouwen met behulp Microsoft Power BI. Spark-clusters in HDInsight bieden ook ondersteuning voor een aantal BI-tools van derden, zoals Tableau, wat het tot een ideaal platform maakt voor gegevensanalisten, zakelijke deskundigen en besluitvormers.

### <a name="spark-machine-learning"></a>Machine Learning in Spark
[Bekijk een zelfstudie: Gebouwtemperaturen voorspellen met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Bekijk een zelfstudie: Voedselinspectieresultaten voorspellen](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark wordt geleverd met [MLlib](http://spark.apache.org/mllib/), een bibliotheek voor machine learning die boven op Spark is gebouwd. U kunt deze bibliotheek gebruiken vanuit een Spark-cluster in HDInsight. Spark-cluster in HDInsight bevat ook Anaconda, een Python-distributie met tal van andere pakketten voor machine learning. Combineer dit met ingebouwde ondersteuning voor Jupyter- en Zeppelin-notebooks en u hebt een eersteklas omgeving voor het maken van machine learning-toepassingen.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Streaming en realtime gegevensanalyse in Spark
[Bekijk een zelfstudie](hdinsight-apache-spark-eventhub-streaming.md)

Spark-clusters in HDInsight bieden uitgebreide ondersteuning voor het bouwen van realtime analyseoplossingen. Terwijl Spark al connectors tooingest gegevens uit diverse bronnen, zoals Kafka-, Flume-, Twitter-, ZeroMQ- of TCP-sockets, voegt eersteklas ondersteuning voor het ophalen van gegevens uit Azure Event Hubs in Spark in HDInsight toe. Event Hubs zijn Hallo meest gebruikte wachtrijservices in Azure. Dankzij out-of-the-box-ondersteuning voor Event Hubs zijn Spark-clusters in HDInsight een ideaal platform voor het bouwen van een realtime analysepijplijn.

## <a name="next-steps"></a>Welke onderdelen zijn in een Spark-cluster opgenomen?
Spark-clusters in HDInsight bevatten Hallo onderdelen die beschikbaar op Hallo-clusters standaard zijn te volgen.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Omvat Spark Core, Spark SQL, Spark-streaming-API's, GraphX en MLlib.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter-notebook](https://jupyter.org)
* [Zeppelin-notebook](http://zeppelin-project.org/)

Spark in HDInsight-clusters bieden ook een [ODBC-stuurprogramma](http://go.microsoft.com/fwlink/?LinkId=616229) voor connectiviteit tooSpark clusters in HDInsight vanuit BI-tools zoals Microsoft Power BI en Tableau.

## <a name="where-do-i-start"></a>Waar moet ik beginnen?
Begin met het maken van een Spark-cluster in HDInsight. Zie [Snelstartgids: een Spark-cluster maken in HDInsight Linux en een interactieve query uitvoeren met Jupyter](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Volgende stappen
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
* [De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
* [Bekende problemen met Apache Spark in Azure HDInsight](hdinsight-apache-spark-known-issues.md).
