---
title: Interactieve Hive in HDInsight - Azure gebruiken | Microsoft Docs
description: Informatie over het gebruik van interactieve (Hive op LLAP) Hive in HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Interactieve Hive in HDInsight (Preview) gebruiken
Interactieve (ook Hive [Lange Live en proces](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is een nieuwe HDInsight [type cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).  Interactieve Hive kan in het cachegeheugen die Hive-query's kunt u veel meer interactieve en sneller. Deze nieuwe functie kunt HDInsight van de wereld meeste zodat, flexibele en open Big Data-oplossingen in de cloud met caches van in het geheugen (met Hive en Spark) en geavanceerde analyses via diepe integratie met R-Services. 

Het cluster interactieve Hive wijkt af van het Hadoop-cluster. Het bevat alleen de Hive-service. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie en andere services wordt binnenkort van dit clustertype worden verwijderd.
> Het Hive-service in het cluster interactieve Hive is alleen toegankelijk via de Ambari Hive-weergave, Beeline en Hive ODBC. Deze niet toegankelijk is via Hive-console, Templeton, Azure CLI en Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Een interactieve Hive-cluster maken
Interactieve Hive-cluster wordt alleen ondersteund op Linux gebaseerde clusters. Zie voor meer informatie over het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Component van interactieve Hive uitvoeren
Er zijn verschillende opties voor het uitvoeren van Hive-query's:

* Uitvoeren van Hive met behulp van de Ambari Hive-weergave
  
    Zie voor informatie over het gebruik van de weergave Hive [de weergave Hive gebruiken met Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Uitvoeren van Hive met Beeline
  
    Zie voor informatie over het gebruik van Beeline op HDInsight [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    U Beeline gebruiken vanuit de headnode of een lege edge-knooppunt.  Beeline gebruik van een leeg edge-knooppunt wordt aanbevolen.  Zie voor meer informatie over het maken van een HDInsight-cluster met een leeg edgenode [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).
* Uitvoeren van Hive via Hive ODBC
  
    Zie voor informatie over het gebruik van Hive ODBC [verbinding maken met Excel en Hadoop met het Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md).

**De verbindingsreeks JDBC zoeken:**

1. Meld u bij de Ambari met behulp van de volgende URL: https://<ClusterName>. AzureHDInsight.net.
2. Klik op **Hive** in het menu links.
3. Klik op de gemarkeerde pictogram voor het kopiëren van de URL:
   
   ![HDInsight Hadoop Hive interactieve LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Zie ook
* [Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informatie over het maken van clusters interactieve Hive in HDInsight.
* [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md): informatie over het gebruik van Beeline Hive-query's verzenden.
* [Excel en Hadoop koppelen met het stuurprogramma Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md): meer informatie over hoe u Excel verbindt met Hive.

