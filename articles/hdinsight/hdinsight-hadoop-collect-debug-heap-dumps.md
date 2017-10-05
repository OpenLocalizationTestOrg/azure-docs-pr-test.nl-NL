---
title: Fouten opsporen en analyseren van Hadoop-services met heap dumpbestanden - Azure | Microsoft Docs
description: Automatisch verzamelen heap dumpbestanden voor Hadoop-services en plaats in de Azure Blob storage-account voor foutopsporing en analyse.
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
ms.openlocfilehash: 6d1d4d47d279eb7a1f0bf1f587445683f0ace7a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="f8292-103">Collect heap dumpen in Blob storage opsporen en analyseren van Hadoop-services</span><span class="sxs-lookup"><span data-stu-id="f8292-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="f8292-104">Dumpbestanden voor heap bevatten een momentopname van de toepassing geheugen, met inbegrip van de waarden van variabelen op het moment dat de dump is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f8292-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="f8292-105">Ze zijn daarom nuttig voor het oplossen van problemen die tijdens runtime optreden.</span><span class="sxs-lookup"><span data-stu-id="f8292-105">So they are useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="f8292-106">Dumpbestanden voor heap kunnen automatisch worden verzameld voor Hadoop-services en in de Azure Blob storage-account van een gebruiker onder HDInsightHeapDumps geplaatst /.</span><span class="sxs-lookup"><span data-stu-id="f8292-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="f8292-107">De verzameling van heap dumpbestanden voor verschillende services moet zijn ingeschakeld voor services op afzonderlijke clusters.</span><span class="sxs-lookup"><span data-stu-id="f8292-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="f8292-108">De standaardwaarde voor deze functie is te zijn uitgeschakeld voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="f8292-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="f8292-109">Deze dumpbestanden heap kunnen oplopen, zodat u aangeraden wordt te controleren van de Blob storage-account waarin ze worden opgeslagen na inschakeling van de verzameling.</span><span class="sxs-lookup"><span data-stu-id="f8292-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f8292-110">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f8292-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f8292-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f8292-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="f8292-112">De informatie in dit artikel is alleen van toepassing op HDInsight op basis van Windows.</span><span class="sxs-lookup"><span data-stu-id="f8292-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="f8292-113">Zie voor meer informatie op Linux gebaseerde HDInsight [inschakelen heap dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="f8292-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="f8292-114">In aanmerking komende services voor heap dumpbestanden</span><span class="sxs-lookup"><span data-stu-id="f8292-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="f8292-115">U kunt de heap dumpbestanden voor de volgende services inschakelen:</span><span class="sxs-lookup"><span data-stu-id="f8292-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="f8292-116">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="f8292-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="f8292-117">**hive** -hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="f8292-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="f8292-118">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="f8292-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="f8292-119">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="f8292-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="f8292-120">**hdfs** -datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="f8292-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="f8292-121">Configuratie-elementen waarmee heap dumpbestanden</span><span class="sxs-lookup"><span data-stu-id="f8292-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="f8292-122">Als u wilt inschakelen heap dumpbestanden voor een service, moet u de juiste configuratie-elementen in de sectie voor de service, die wordt opgegeven met instellen **service_name**.</span><span class="sxs-lookup"><span data-stu-id="f8292-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="f8292-123">De waarde van **service_name** kan een van de services hier vermeld: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, of namenode.</span><span class="sxs-lookup"><span data-stu-id="f8292-123">The value of **service_name** can be any of the services listed here: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="f8292-124">Met Azure PowerShell inschakelen</span><span class="sxs-lookup"><span data-stu-id="f8292-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="f8292-125">Bijvoorbeeld, als u wilt inschakelen heap dumpbestanden via Azure PowerShell voor jobhistoryserver, kunt u het volgende script:</span><span class="sxs-lookup"><span data-stu-id="f8292-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you can use the following script:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="f8292-126">Schakel met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f8292-126">Enable using .NET SDK</span></span>
<span data-ttu-id="f8292-127">Bijvoorbeeld, als u wilt heap dumpbestanden inschakelen met behulp van de Azure HDInsight .NET SDK voor jobhistoryserver, kunt u de volgende code:</span><span class="sxs-lookup"><span data-stu-id="f8292-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you can use the following code:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
