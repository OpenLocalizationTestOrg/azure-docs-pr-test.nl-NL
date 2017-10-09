---
title: Interactieve Hive in HDInsight - Azure aaaUse | Microsoft Docs
description: Meer informatie over hoe toouse interactieve (Hive op LLAP) Hive in HDInsight.
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
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a>Interactieve Hive in HDInsight (Preview) gebruiken
Interactieve (ook Hive [Lange Live en proces](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is een nieuwe HDInsight [type cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).  Interactieve Hive kan in het cachegeheugen die Hive-query's kunt u veel meer interactieve en sneller. Deze nieuwe functie kunt HDInsight een Hallo wereld meeste zodat, flexibele en open Big Data-oplossingen op Hallo cloud met caches van in het geheugen (met Hive en Spark) en geavanceerde analyses via diepe integratie met R-Services. 

Hallo interactieve Hive cluster wijkt af van Hallo Hadoop-cluster. Het bevat alleen Hallo Hive-service. 

> [!NOTE]
> MapReduce, Pig, Sqoop, Oozie en andere services wordt binnenkort van dit clustertype worden verwijderd.
> Hallo Hive-service in Hallo interactieve Hive-cluster is alleen toegankelijk via Hallo Ambari Hive-weergave, Beeline en Hive ODBC. Deze niet toegankelijk is via Hive-console, Templeton, Azure CLI en Azure PowerShell. 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a>Een interactieve Hive-cluster maken
Interactieve Hive-cluster wordt alleen ondersteund op Linux gebaseerde clusters. Zie voor meer informatie over het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

## <a name="execute-hive-from-interactive-hive"></a>Component van interactieve Hive uitvoeren
Er zijn verschillende opties voor het uitvoeren van Hive-query's:

* Uitvoeren van Hive met Hallo Ambari Hive-weergave
  
    Zie voor informatie over het gebruik van Hive-weergave Hallo Hallo [gebruik Hallo Hive-weergave met Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).
* Uitvoeren van Hive met Beeline
  
    Zie voor informatie over het gebruik van Beeline op HDInsight hello [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).
  
    U Beeline van headnode hello of een lege edge-knooppunt.  Beeline gebruik van een leeg edge-knooppunt wordt aanbevolen.  Zie voor meer informatie over het maken van een HDInsight-cluster met een leeg edgenode [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).
* Uitvoeren van Hive via Hive ODBC
  
    Zie voor informatie over het gebruik van Hive ODBC Hallo [tooHadoop Excel verbinding maken met de Hallo Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md).

**toofind hello JDBC-verbindingsreeks:**

1. Meld u aan met behulp van de URL na Hallo tooAmbari: https://<ClusterName>. AzureHDInsight.net.
2. Klik op **Hive** in het linkermenu Hallo.
3. Klik op Hallo gemarkeerd pictogram toocopy Hallo URL:
   
   ![HDInsight Hadoop Hive interactieve LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a>Zie ook
* [Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): meer informatie over hoe toocreate interactieve Hive-clusters in HDInsight.
* [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md): meer informatie over hoe toouse Beeline toosubmit Hive-query's.
* [Verbinding maken met Excel tooHadoop met Hallo Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md): meer informatie over hoe tooconnect Excel tooHive.

