---
title: aaaUse Livy Spark toosubmit taken tooSpark-cluster in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Spark REST-API toosubmit Spark taken die op afstand tooan Azure HDInsight-cluster.
keywords: Apache spark rest-api, spark livy
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a><span data-ttu-id="b39ad-104">Apache Spark REST-API toosubmit externe taken tooan HDInsight Spark-cluster gebruiken</span><span class="sxs-lookup"><span data-stu-id="b39ad-104">Use Apache Spark REST API toosubmit remote jobs tooan HDInsight Spark cluster</span></span>

<span data-ttu-id="b39ad-105">Meer informatie over hoe toouse Livy, Hallo Apache Spark REST API, namelijk gebruikte toosubmit externe taken tooan Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-105">Learn how toouse Livy, hello Apache Spark REST API, which is used toosubmit remote jobs tooan Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="b39ad-106">Zie voor gedetailleerde documentatie [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="b39ad-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="b39ad-107">U kunt gebruiken Livy toorun interactieve Spark houders of batch-taken toobe uitvoeren op Spark verzenden.</span><span class="sxs-lookup"><span data-stu-id="b39ad-107">You can use Livy toorun interactive Spark shells or submit batch jobs toobe run on Spark.</span></span> <span data-ttu-id="b39ad-108">In dit artikel wordt gesproken over met behulp van Livy toosubmit batchtaken.</span><span class="sxs-lookup"><span data-stu-id="b39ad-108">This article talks about using Livy toosubmit batch jobs.</span></span> <span data-ttu-id="b39ad-109">Hallo codefragmenten in dit artikel gebruiken cURL toomake REST API-aanroepen toohello Livy Spark-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="b39ad-109">hello snippets in this article use cURL toomake REST API calls toohello Livy Spark endpoint.</span></span>

<span data-ttu-id="b39ad-110">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="b39ad-110">**Prerequisites:**</span></span>

* <span data-ttu-id="b39ad-111">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b39ad-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="b39ad-112">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="b39ad-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="b39ad-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="b39ad-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="b39ad-114">Dit artikel wordt cURL toodemonstrate hoe toomake REST-API met een HDInsight Spark-cluster aanroept.</span><span class="sxs-lookup"><span data-stu-id="b39ad-114">This article uses cURL toodemonstrate how toomake REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="b39ad-115">Een batchtaak Livy Spark verzenden</span><span class="sxs-lookup"><span data-stu-id="b39ad-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="b39ad-116">Voordat u een batch-job indienen, moet u Hallo toepassing jar op Hallo clusteropslag die is gekoppeld aan cluster Hallo uploaden.</span><span class="sxs-lookup"><span data-stu-id="b39ad-116">Before you submit a batch job, you must upload hello application jar on hello cluster storage associated with hello cluster.</span></span> <span data-ttu-id="b39ad-117">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdrachtregelprogramma, toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="b39ad-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, toodo so.</span></span> <span data-ttu-id="b39ad-118">Er zijn verschillende andere clients kunt u tooupload gegevens.</span><span class="sxs-lookup"><span data-stu-id="b39ad-118">There are various other clients you can use tooupload data.</span></span> <span data-ttu-id="b39ad-119">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b39ad-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="b39ad-120">**Voorbeelden**:</span><span class="sxs-lookup"><span data-stu-id="b39ad-120">**Examples**:</span></span>

* <span data-ttu-id="b39ad-121">Als Hallo jar-bestand zich op Hallo cluster storage (WASB)</span><span class="sxs-lookup"><span data-stu-id="b39ad-121">If hello jar file is on hello cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="b39ad-122">Als u wilt toopass Hallo jar filename en classname Hallo als onderdeel van een bestand voor invoer (in dit voorbeeld input.txt)</span><span class="sxs-lookup"><span data-stu-id="b39ad-122">If you want toopass hello jar filename and hello classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a><span data-ttu-id="b39ad-123">Informatie over Livy Spark batches uitgevoerd op Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="b39ad-123">Get information on Livy Spark batches running on hello cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="b39ad-124">**Voorbeelden**:</span><span class="sxs-lookup"><span data-stu-id="b39ad-124">**Examples**:</span></span>

* <span data-ttu-id="b39ad-125">Als u wilt dat tooretrieve alle Hallo Livy Spark batches uitgevoerd op Hallo-cluster:</span><span class="sxs-lookup"><span data-stu-id="b39ad-125">If you want tooretrieve all hello Livy Spark batches running on hello cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="b39ad-126">Als u wilt dat een specifieke batch met een bepaalde batchId tooretrieve</span><span class="sxs-lookup"><span data-stu-id="b39ad-126">If you want tooretrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="b39ad-127">Een batch-job Livy Spark verwijderen</span><span class="sxs-lookup"><span data-stu-id="b39ad-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="b39ad-128">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="b39ad-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="b39ad-129">Livy Spark en hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="b39ad-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="b39ad-130">Livy biedt hoge beschikbaarheid voor Spark taken uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-130">Livy provides high-availability for Spark jobs running on hello cluster.</span></span> <span data-ttu-id="b39ad-131">Hier volgt een aantal voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="b39ad-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="b39ad-132">Als Hallo Livy-service wordt uitgeschakeld nadat u een taak op afstand hebt verzonden tooa Spark-cluster, hello taak toorun op Hallo achtergrond blijft.</span><span class="sxs-lookup"><span data-stu-id="b39ad-132">If hello Livy service goes down after you have submitted a job remotely tooa Spark cluster, hello job continues toorun in hello background.</span></span> <span data-ttu-id="b39ad-133">Hier wordt een back-up, wordt Hallo status van taak Hallo en rapporten weer hersteld.</span><span class="sxs-lookup"><span data-stu-id="b39ad-133">When Livy is back up, it restores hello status of hello job and reports it back.</span></span>
* <span data-ttu-id="b39ad-134">Jupyter-notebooks voor HDInsight worden van stroom voorzien door Livy in Hallo back-end.</span><span class="sxs-lookup"><span data-stu-id="b39ad-134">Jupyter notebooks for HDInsight are powered by Livy in hello backend.</span></span> <span data-ttu-id="b39ad-135">Als een laptop een Spark-taak wordt uitgevoerd en Hallo Livy-service opnieuw wordt gestart, blijft de notebook Hallo toorun Hallo code cellen.</span><span class="sxs-lookup"><span data-stu-id="b39ad-135">If a notebook is running a Spark job and hello Livy service gets restarted, hello notebook continues toorun hello code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="b39ad-136">Een voorbeeld weergeven</span><span class="sxs-lookup"><span data-stu-id="b39ad-136">Show me an example</span></span>
<span data-ttu-id="b39ad-137">In deze sectie we kijken voorbeelden toouse Livy Spark toosubmit batch-job Hallo voortgang van de taak Hallo en vervolgens te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b39ad-137">In this section, we look at examples toouse Livy Spark toosubmit batch job, monitor hello progress of hello job, and then delete it.</span></span> <span data-ttu-id="b39ad-138">Hallo-toepassing in dit voorbeeld we gebruiken is een ontwikkeld in Hallo artikel Hallo [maken van een zelfstandige Scala toepassing en toorun op HDInsight Spark-cluster](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="b39ad-138">hello application we use in this example is hello one developed in hello article [Create a standalone Scala application and toorun on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="b39ad-139">Hier Hallo stappen wordt ervan uitgegaan dat:</span><span class="sxs-lookup"><span data-stu-id="b39ad-139">hello steps here assume that:</span></span>

* <span data-ttu-id="b39ad-140">U hebt al Hallo toepassing jar toohello storage-account die is gekoppeld aan cluster Hallo gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="b39ad-140">You have already copied over hello application jar toohello storage account associated with hello cluster.</span></span>
* <span data-ttu-id="b39ad-141">U hebt geïnstalleerd op Hallo-computer waarop u deze stappen probeert CuRL.</span><span class="sxs-lookup"><span data-stu-id="b39ad-141">You have CuRL installed on hello computer where you are trying these steps.</span></span>

<span data-ttu-id="b39ad-142">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b39ad-142">Perform hello following steps:</span></span>

1. <span data-ttu-id="b39ad-143">Laat het ons moet u eerst controleren of Livy Spark op Hallo cluster wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b39ad-143">Let us first verify that Livy Spark is running on hello cluster.</span></span> <span data-ttu-id="b39ad-144">We kunnen dit doen door het ophalen van een lijst van het uitvoeren van batches.</span><span class="sxs-lookup"><span data-stu-id="b39ad-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="b39ad-145">Als u een taak met behulp van Livy voor Hallo eerst uitvoert, moet Hallo uitvoer nul retourneren.</span><span class="sxs-lookup"><span data-stu-id="b39ad-145">If you are running a job using Livy for hello first time, hello output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="b39ad-146">Deze krijgt u een vergelijkbare uitvoer-toohello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="b39ad-146">You should get an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b39ad-147">U ziet hoe de laatste regel in de uitvoer van de Hallo Hallo zegt **totaal: 0**, die geen actieve batches wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="b39ad-147">Notice how hello last line in hello output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="b39ad-148">Laten we nu een batch-job indienen.</span><span class="sxs-lookup"><span data-stu-id="b39ad-148">Let us now submit a batch job.</span></span> <span data-ttu-id="b39ad-149">Hallo volgende codefragment maakt gebruik van een bestand voor invoer (input.txt) toopass Hallo jar naam en klassenaam Hallo als parameters.</span><span class="sxs-lookup"><span data-stu-id="b39ad-149">hello following snippet uses an input file (input.txt) toopass hello jar name and hello class name as parameters.</span></span> <span data-ttu-id="b39ad-150">Als u deze stappen vanuit een Windows-computer uitvoert, is met behulp van een bestand voor invoer Hallo aanbevolen benadering.</span><span class="sxs-lookup"><span data-stu-id="b39ad-150">If you are running these steps from a Windows computer, using an input file is hello recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="b39ad-151">parameters in bestand Hallo Hallo **input.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="b39ad-151">hello parameters in hello file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="b39ad-152">Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="b39ad-152">You should see an output similar toohello  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b39ad-153">U ziet hoe de laatste regel van uitvoer Hallo Hallo zegt **status: vanaf**.</span><span class="sxs-lookup"><span data-stu-id="b39ad-153">Notice how hello last line of hello output says **state:starting**.</span></span> <span data-ttu-id="b39ad-154">Ook wordt, **-id: 0**.</span><span class="sxs-lookup"><span data-stu-id="b39ad-154">It also says, **id:0**.</span></span> <span data-ttu-id="b39ad-155">Hier **0** Hallo batch-id is.</span><span class="sxs-lookup"><span data-stu-id="b39ad-155">Here, **0** is hello batch ID.</span></span>

3. <span data-ttu-id="b39ad-156">U kunt nu ophalen Hallo status van deze specifieke batch Hallo batch-id.</span><span class="sxs-lookup"><span data-stu-id="b39ad-156">You can now retrieve hello status of this specific batch using hello batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="b39ad-157">Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="b39ad-157">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b39ad-158">Hallo output wordt nu weergegeven **status: geslaagd**, die wordt voorgesteld die Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b39ad-158">hello output now shows **state:success**, which suggests that hello job was successfully completed.</span></span>

4. <span data-ttu-id="b39ad-159">Als u wilt, kunt u nu Hallo batch verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b39ad-159">If you want, you can now delete hello batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="b39ad-160">Hier ziet u een vergelijkbare uitvoer-toohello codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="b39ad-160">You should see an output similar toohello following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="b39ad-161">Hallo laatste regel van Hallo uitvoer toont dat die Hallo-batch is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b39ad-161">hello last line of hello output shows that hello batch was successfully deleted.</span></span> <span data-ttu-id="b39ad-162">Verwijderen van een taak, terwijl deze wordt uitgevoerd, ook is funest Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="b39ad-162">Deleting a job, while it is running, also kills hello job.</span></span> <span data-ttu-id="b39ad-163">Als u een taak die is voltooid, is of anderszins verwijdert worden verwijderd Hallo taakinformatie volledig.</span><span class="sxs-lookup"><span data-stu-id="b39ad-163">If you delete a job that has completed, successfully or otherwise, it deletes hello job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="b39ad-164">Gebruik van Livy Spark in HDInsight 3.5 clusters</span><span class="sxs-lookup"><span data-stu-id="b39ad-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="b39ad-165">3.5 HDInsight-cluster, schakelt het gebruik van bestanden lokaal bestand paden tooaccess met voorbeeldgegevens of potten standaard.</span><span class="sxs-lookup"><span data-stu-id="b39ad-165">HDInsight 3.5 cluster, by default, disables use of local file paths tooaccess sample data files or jars.</span></span> <span data-ttu-id="b39ad-166">We raden u toouse hello `wasb://` pad in plaats daarvan tooaccess potten of voorbeeldgegevens bestanden van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-166">We encourage you toouse hello `wasb://` path instead tooaccess jars or sample data files from hello cluster.</span></span> <span data-ttu-id="b39ad-167">Als u dat het lokale pad toouse wilt, moet u dienovereenkomstig Hallo Ambari configuratie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="b39ad-167">If you do want toouse local path, you must update hello Ambari configuration accordingly.</span></span> <span data-ttu-id="b39ad-168">toodo zodat:</span><span class="sxs-lookup"><span data-stu-id="b39ad-168">toodo so:</span></span>

1. <span data-ttu-id="b39ad-169">Ga toohello Ambari-portal voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-169">Go toohello Ambari portal for hello cluster.</span></span> <span data-ttu-id="b39ad-170">Hallo Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op https://**CLUSTERNAME**. azurehdidnsight.net, waarbij CLUSTERNAME Hallo-naam van het cluster is.</span><span class="sxs-lookup"><span data-stu-id="b39ad-170">hello Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is hello name of your cluster.</span></span>

2. <span data-ttu-id="b39ad-171">Hallo linkernavigatiebalk, klik op **Livy**, en klik vervolgens op **Configs**.</span><span class="sxs-lookup"><span data-stu-id="b39ad-171">From hello left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="b39ad-172">Onder **livy-standaard** Hallo eigenschapsnaam toevoegen `livy.file.local-dir-whitelist` en stel de waarde te**'/'** als u tooallow volledige toegang toofile systeem wilt.</span><span class="sxs-lookup"><span data-stu-id="b39ad-172">Under **livy-default** add hello property name `livy.file.local-dir-whitelist` and set it's value too**"/"** if you want tooallow full access toofile system.</span></span> <span data-ttu-id="b39ad-173">Als u tooallow toegang alleen tooa specifieke map wilt, geeft u Hallo pad toothat directory Hallo-waarde.</span><span class="sxs-lookup"><span data-stu-id="b39ad-173">If you want tooallow access only tooa specific directory, provide hello path toothat directory as hello value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="b39ad-174">Verzenden van Livy taken voor een cluster binnen een virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="b39ad-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="b39ad-175">Als u verbinding maakt met tooan HDInsight Spark-cluster uit een Azure-netwerk, kunt u rechtstreeks tooLivy op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-175">If you connect tooan HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect tooLivy on hello cluster.</span></span> <span data-ttu-id="b39ad-176">In dat geval Hallo URL voor Livy-eindpunt is `http://<IP address of hello headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="b39ad-176">In such a case, hello URL for Livy endpoint is `http://<IP address of hello headnode>:8998/batches`.</span></span> <span data-ttu-id="b39ad-177">Hier **8998** Hallo poort waarop Livy op Hallo cluster headnode wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b39ad-177">Here, **8998** is hello port on which Livy runs on hello cluster headnode.</span></span> <span data-ttu-id="b39ad-178">Zie voor meer informatie over de toegang tot services op niet-openbaar poorten [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="b39ad-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b39ad-179">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b39ad-179">Troubleshooting</span></span>

<span data-ttu-id="b39ad-180">Hier volgen enkele problemen beschreven die u tegenkomen kunt tijdens het gebruik van Livy voor externe taak verzending tooSpark clusters.</span><span class="sxs-lookup"><span data-stu-id="b39ad-180">Here are some issues that you might run into while using Livy for remote job submission tooSpark clusters.</span></span>

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a><span data-ttu-id="b39ad-181">Gebruik een externe jar van Hallo extra opslagruimte wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="b39ad-181">Using an external jar from hello additional storage is not supported</span></span>

<span data-ttu-id="b39ad-182">**Probleem:** als uw job Livy Spark verwijst naar een externe jar vanuit Hallo extra opslagaccount die is gekoppeld aan cluster hello, Hallo-taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="b39ad-182">**Problem:** If your Livy Spark job references an external jar from hello additional storage account associated with hello cluster, hello job fails.</span></span>

<span data-ttu-id="b39ad-183">**Oplossing:** Zorg ervoor dat Hallo jar gewenste toouse is beschikbaar in Hallo standaard opslag die is gekoppeld aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b39ad-183">**Resolution:** Make sure that hello jar you want toouse is available in hello default storage associated with hello HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="b39ad-184">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="b39ad-184">Next step</span></span>

* [<span data-ttu-id="b39ad-185">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="b39ad-185">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="b39ad-186">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="b39ad-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

