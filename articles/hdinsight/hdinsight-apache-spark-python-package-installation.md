---
title: Actie - pakketten voor Python installeren met Jupyter op Azure HDInsight script | Microsoft Docs
description: Stapsgewijze instructies voor het gebruik van de scriptactie voor het configureren van Jupyter-notebooks met HDInsight Spark-clusters externe python-pakketten gebruiken.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 20cf384c96d4ff4eaf064c8880ad128d521fb9bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-script-action-to-install-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Scriptactie gebruiken voor het installeren van externe Python-pakketten voor Jupyter-notebooks in Apache Spark-clusters in HDInsight
> [!div class="op_single_selector"]
> * [Met behulp van de cel verwerkt Magic-pakket](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Met behulp van de scriptactie](hdinsight-apache-spark-python-package-installation.md)
>
>

Informatie over het gebruik van scriptacties voor het configureren van een Apache Spark-cluster in HDInsight (Linux) gebruiken van externe, community bijgedragen **python** pakketten die niet out-of-the-box opgenomen in het cluster.

> [!NOTE]
> U kunt ook een Jupyter-notebook configureren met behulp van `%%configure` magic externe pakketten gebruiken. Zie voor instructies [externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

U kunt zoeken in de [package index](https://pypi.python.org/pypi) voor de volledige lijst met pakketten die beschikbaar zijn. U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen. Bijvoorbeeld, kunt u pakketten beschikbaar gesteld via installeren [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) of [conda smidse](https://conda-forge.github.io/feedstocks.html).

In dit artikel leert u hoe u installeert de [TensorFlow](https://www.tensorflow.org/) van het pakket met Script Actoin op het cluster en wordt via de Jupyter-notebook gebruikt.

## <a name="prerequisites"></a>Vereisten
U hebt het volgende:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Als u nog geen een Spark-cluster in HDInsight Linux, kunt u scriptacties uitvoeren tijdens het maken van het cluster. Ga naar de documentatie op [het gebruik van aangepaste scriptacties](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Externe pakketten gebruiken met Jupyter-notebooks

1. Klik vanuit de [Azure Portal](https://portal.azure.com/), vanaf het startboard, op de tegel voor uw Spark-cluster (als u deze aan het startboard hebt vastgemaakt). U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.   

2. Klik in de blade Spark-cluster op **scriptacties** onder **gebruik**. De aangepaste actie uitgevoerd installeert die TensorFlow in de hoofdknooppunten en worker-knooppunten. Het script bash kan worden verwezen vanuit: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh gaat u naar de documentatie op [het gebruik van aangepaste scriptacties](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Er zijn twee python-installaties in het cluster. Spark gebruikt de Anaconda python-installatie zich bevindt op `/usr/bin/anaconda/bin`. Met de installatie in uw aangepaste acties via verwijzen naar `/usr/bin/anaconda/bin/pip` en `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Open een PySpark Jupyter-notebook

    ![Een nieuwe Jupyter-notebook maken](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Een nieuwe Jupyter-notebook maken")

4. Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled.pynb. Klik bovenaan op de naam van de notebook en wijzig deze in een beschrijvende naam.

    ![Een naam opgeven voor de notebook](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "Een naam opgeven voor de notebook")

5. U gaat nu `import tensorflow` en een Hallo wereld-voorbeeld uitvoeren. 

    Code kopiëren:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    Het resultaat ziet er als volgt:
    
    ![De uitvoering van code TensorFlow](./media/hdinsight-apache-spark-python-package-installation/execution.png "code TensorFlow uitvoeren")



## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [Externe pakketten gebruiken met Jupyter-notebooks in Apache Spark-clusters in HDInsight](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor het Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
