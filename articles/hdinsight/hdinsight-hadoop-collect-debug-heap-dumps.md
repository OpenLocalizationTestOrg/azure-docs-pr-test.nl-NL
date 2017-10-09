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
# <a name="collect-heap-dumps-in-blob-storage-toodebug-and-analyze-hadoop-services"></a><span data-ttu-id="98ece-103">Heap crashdumps in Blob storage toodebug verzamelen en analyseren van Hadoop-services</span><span class="sxs-lookup"><span data-stu-id="98ece-103">Collect heap dumps in Blob storage toodebug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="98ece-104">Dumpbestanden voor heap bevatten een momentopname van de toepassing hello geheugen, met inbegrip van waarden van variabelen Hallo gelijktijdig Hallo Hallo dump is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98ece-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="98ece-105">Ze zijn daarom nuttig voor het oplossen van problemen die tijdens runtime optreden.</span><span class="sxs-lookup"><span data-stu-id="98ece-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="98ece-106">Dumpbestanden voor heap kunnen automatisch worden verzameld voor Hadoop-services en in Azure Blob storage-account van een gebruiker onder HDInsightHeapDumps Hallo geplaatst /.</span><span class="sxs-lookup"><span data-stu-id="98ece-106">Heap dumps can be automatically collected for Hadoop services and placed inside hello Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="98ece-107">Hallo-verzameling van heap dumpbestanden voor verschillende services moet zijn ingeschakeld voor services op afzonderlijke clusters.</span><span class="sxs-lookup"><span data-stu-id="98ece-107">hello collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="98ece-108">Hallo standaardwaarde voor deze functie is toobe uitgeschakeld voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="98ece-108">hello default for this feature is toobe off for a cluster.</span></span> <span data-ttu-id="98ece-109">Deze dumpbestanden heap kunnen oplopen, dus aangeraden toomonitor Hallo Blob storage-account waarin ze worden opgeslagen na inschakeling van Hallo verzameling is.</span><span class="sxs-lookup"><span data-stu-id="98ece-109">These heap dumps can be large, so it is advisable toomonitor hello Blob storage account where they are being saved once hello collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="98ece-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="98ece-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="98ece-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="98ece-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="98ece-112">Hallo-informatie in dit artikel is alleen van toepassing op basis van tooWindows HDInsight.</span><span class="sxs-lookup"><span data-stu-id="98ece-112">hello information in this article only applies tooWindows-based HDInsight.</span></span> <span data-ttu-id="98ece-113">Zie voor meer informatie op Linux gebaseerde HDInsight [inschakelen heap dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="98ece-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="98ece-114">In aanmerking komende services voor heap dumpbestanden</span><span class="sxs-lookup"><span data-stu-id="98ece-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="98ece-115">U kunt de heap dumpbestanden voor Hallo na services inschakelen:</span><span class="sxs-lookup"><span data-stu-id="98ece-115">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="98ece-116">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="98ece-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="98ece-117">**hive** -hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="98ece-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="98ece-118">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="98ece-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="98ece-119">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="98ece-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="98ece-120">**hdfs** -datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="98ece-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="98ece-121">Configuratie-elementen waarmee heap dumpbestanden</span><span class="sxs-lookup"><span data-stu-id="98ece-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="98ece-122">tooturn op heap dumpbestanden voor een service, moet u tooset Hallo juiste configuratie-elementen in de sectie Hallo voor de service, die wordt opgegeven met **service_name**.</span><span class="sxs-lookup"><span data-stu-id="98ece-122">tooturn on heap dumps for a service, you need tooset hello appropriate configuration elements in hello section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="98ece-123">waarde van Hallo **service_name** kan bestaan uit een Hallo services hier vermeld: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, of namenode.</span><span class="sxs-lookup"><span data-stu-id="98ece-123">hello value of **service_name** can be any of hello services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="98ece-124">Met Azure PowerShell inschakelen</span><span class="sxs-lookup"><span data-stu-id="98ece-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="98ece-125">Bijvoorbeeld: tooturn op heap dumpbestanden via Azure PowerShell voor jobhistoryserver, kunt u Hallo script volgen:</span><span class="sxs-lookup"><span data-stu-id="98ece-125">For example, tooturn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use hello following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="98ece-126">Schakel met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="98ece-126">Enable using .NET SDK</span></span>
<span data-ttu-id="98ece-127">Bijvoorbeeld: tooturn op heap dumpbestanden via hello Azure HDInsight .NET SDK voor jobhistoryserver, kunt u Hallo code te volgen:</span><span class="sxs-lookup"><span data-stu-id="98ece-127">For example, tooturn on heap dumps by using hello Azure HDInsight .NET SDK for jobhistoryserver, you can use hello following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
