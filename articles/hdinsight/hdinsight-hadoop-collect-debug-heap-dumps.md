---
title: aaaDebug en analyseren van Hadoop-services met heap dumpbestanden - Azure | Microsoft Docs
description: Automatisch verzamelen heap dumpbestanden voor Hadoop-services en plaats binnen hello Azure Blob storage-account voor foutopsporing en analyse.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 70fbc2d6d97d35b0d7b1d9149673b02ae1878eb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a>Heap crashdumps in Blob storage toodebug verzamelen en analyseren van Hadoop-services
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

Dumpbestanden voor heap bevatten een momentopname van de toepassing hello geheugen, met inbegrip van waarden van variabelen Hallo gelijktijdig Hallo Hallo dump is gemaakt. Ze zijn daarom nuttig voor het oplossen van problemen die tijdens runtime optreden. Dumpbestanden voor heap kunnen automatisch worden verzameld voor Hadoop-services en in Azure Blob storage-account van een gebruiker onder HDInsightHeapDumps Hallo geplaatst /.

Hallo-verzameling van heap dumpbestanden voor verschillende services moet zijn ingeschakeld voor services op afzonderlijke clusters. Hallo standaardwaarde voor deze functie is toobe uitgeschakeld voor een cluster. Deze dumpbestanden heap kunnen oplopen, dus aangeraden toomonitor Hallo Blob storage-account waarin ze worden opgeslagen na inschakeling van Hallo verzameling is.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Hallo-informatie in dit artikel is alleen van toepassing op basis van tooWindows HDInsight. Zie voor meer informatie op Linux gebaseerde HDInsight [inschakelen heap dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)


## <a name="eligible-services-for-heap-dumps"></a>In aanmerking komende services voor heap dumpbestanden
U kunt de heap dumpbestanden voor Hallo na services inschakelen:

* **hcatalog** -tempelton
* **hive** -hiveserver2, metastore, derbyserver
* **mapreduce** -jobhistoryserver
* **yarn** -resourcemanager, nodemanager, timelineserver
* **hdfs** -datanode, secondarynamenode, namenode

## <a name="configuration-elements-that-enable-heap-dumps"></a>Configuratie-elementen waarmee heap dumpbestanden
tooturn op heap dumpbestanden voor een service, moet u tooset Hallo juiste configuratie-elementen in de sectie Hallo voor de service, die wordt opgegeven met **service_name**.

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

waarde van Hallo **service_name** kan bestaan uit een Hallo services hier vermeld: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, of namenode.

## <a name="enable-using-azure-powershell"></a>Met Azure PowerShell inschakelen
Bijvoorbeeld: tooturn op heap dumpbestanden via Azure PowerShell voor jobhistoryserver, kunt u Hallo script volgen:

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a>Schakel met .NET SDK
Bijvoorbeeld: tooturn op heap dumpbestanden via hello Azure HDInsight .NET SDK voor jobhistoryserver, kunt u Hallo code te volgen:

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
