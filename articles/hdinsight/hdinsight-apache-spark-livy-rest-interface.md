---
title: Livy Spark gebruiken voor het verzenden van taken met Spark op Azure HDInsight-cluster | Microsoft Docs
description: Informatie over het Apache Spark REST API gebruiken om Spark-taken op afstand met een Azure HDInsight-cluster te verzenden.
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
ms.openlocfilehash: e1a28d69bbf40ea3134a7899a0d2fe70e5fc9e71
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="33754-104">Apache Spark REST API gebruiken om externe taken met een HDInsight Spark-cluster te verzenden</span><span class="sxs-lookup"><span data-stu-id="33754-104">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="33754-105">Informatie over het gebruik van Livy, Apache Spark REST API, die wordt gebruikt voor het verzenden van externe taken naar een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-105">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="33754-106">Zie voor gedetailleerde documentatie [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="33754-106">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="33754-107">Hier kunt u interactieve Spark houders uitvoeren of verzenden van batchtaken worden uitgevoerd op Spark.</span><span class="sxs-lookup"><span data-stu-id="33754-107">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="33754-108">In dit artikel wordt gesproken over met behulp van Livy om batchtaken te verzenden.</span><span class="sxs-lookup"><span data-stu-id="33754-108">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="33754-109">De codefragmenten in dit artikel wordt cURL gebruiken om REST-API-aanroepen naar de Livy Spark-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="33754-109">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="33754-110">**Vereisten:**</span><span class="sxs-lookup"><span data-stu-id="33754-110">**Prerequisites:**</span></span>

* <span data-ttu-id="33754-111">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="33754-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="33754-112">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="33754-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="33754-113">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="33754-113">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="33754-114">In dit artikel wordt cURL gebruikt om te laten zien hoe u REST-API-aanroepen op basis van een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-114">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="33754-115">Een batchtaak Livy Spark verzenden</span><span class="sxs-lookup"><span data-stu-id="33754-115">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="33754-116">Voordat u een batch-job indienen, kunt u de toepassing jar in de clusteropslag die is gekoppeld aan het cluster moet uploaden.</span><span class="sxs-lookup"><span data-stu-id="33754-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="33754-117">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdrachtregelprogramma, om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="33754-117">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="33754-118">Er zijn verschillende andere clients die u gebruiken kunt om gegevens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="33754-118">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="33754-119">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="33754-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="33754-120">**Voorbeelden**:</span><span class="sxs-lookup"><span data-stu-id="33754-120">**Examples**:</span></span>

* <span data-ttu-id="33754-121">Als het jar-bestand in de clusteropslag (WASB)</span><span class="sxs-lookup"><span data-stu-id="33754-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="33754-122">Als u wilt de jar-bestandsnaam en de classname doorgeven als onderdeel van een bestand voor invoer (in dit voorbeeld input.txt)</span><span class="sxs-lookup"><span data-stu-id="33754-122">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="33754-123">Informatie over Livy Spark batches uitgevoerd op het cluster</span><span class="sxs-lookup"><span data-stu-id="33754-123">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="33754-124">**Voorbeelden**:</span><span class="sxs-lookup"><span data-stu-id="33754-124">**Examples**:</span></span>

* <span data-ttu-id="33754-125">Als u ophalen alle de Livy Spark batches uitgevoerd op het cluster wilt:</span><span class="sxs-lookup"><span data-stu-id="33754-125">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="33754-126">Als u wilt ophalen van een specifieke batch met een bepaalde batchId</span><span class="sxs-lookup"><span data-stu-id="33754-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="33754-127">Een batch-job Livy Spark verwijderen</span><span class="sxs-lookup"><span data-stu-id="33754-127">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="33754-128">**Voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="33754-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="33754-129">Livy Spark en hoge beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="33754-129">Livy Spark and high-availability</span></span>
<span data-ttu-id="33754-130">Livy biedt hoge beschikbaarheid voor Spark taken uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="33754-131">Hier volgt een aantal voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="33754-131">Here is a couple of examples.</span></span>

* <span data-ttu-id="33754-132">Als de service Livy uitvalt nadat u een taak op afstand voor een Spark-cluster hebt verzonden, blijft de taak op de achtergrond uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="33754-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="33754-133">Hier wordt een back-up, wordt de status van de taak en de rapporten weer hersteld.</span><span class="sxs-lookup"><span data-stu-id="33754-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="33754-134">Jupyter-notebooks voor HDInsight worden door Livy van stroom voorzien in de back-end.</span><span class="sxs-lookup"><span data-stu-id="33754-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="33754-135">Als een laptop een Spark-taak wordt uitgevoerd en de Livy-service opnieuw wordt gestart, blijft de notebook uitvoeren van de cellen van de code.</span><span class="sxs-lookup"><span data-stu-id="33754-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="33754-136">Een voorbeeld weergeven</span><span class="sxs-lookup"><span data-stu-id="33754-136">Show me an example</span></span>
<span data-ttu-id="33754-137">In dit gedeelte kijken we voorbeelden Livy Spark batchverwerking indienen, de voortgang van de taak en verwijder deze vervolgens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="33754-137">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="33754-138">De toepassing in dit voorbeeld we gebruiken is ontwikkeld in het artikel [maken van een zelfstandige toepassing Scala en uit te voeren op HDInsight Spark-cluster](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="33754-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="33754-139">De stappen die hier wordt ervan uitgegaan dat:</span><span class="sxs-lookup"><span data-stu-id="33754-139">The steps here assume that:</span></span>

* <span data-ttu-id="33754-140">U hebt al de jar toepassing gekopieerd naar het opslagaccount die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="33754-141">U hebt geïnstalleerd op de computer waarop u deze stappen probeert CuRL.</span><span class="sxs-lookup"><span data-stu-id="33754-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="33754-142">De volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="33754-142">Perform the following steps:</span></span>

1. <span data-ttu-id="33754-143">Laten we eerst controleren of Livy Spark wordt uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-143">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="33754-144">We kunnen dit doen door het ophalen van een lijst van het uitvoeren van batches.</span><span class="sxs-lookup"><span data-stu-id="33754-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="33754-145">Als u een taak met behulp van Livy voor de eerste keer uitvoert, moet de uitvoer nul retourneren.</span><span class="sxs-lookup"><span data-stu-id="33754-145">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="33754-146">U moet uitvoer vergelijkbaar met het volgende fragment krijgen:</span><span class="sxs-lookup"><span data-stu-id="33754-146">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="33754-147">U ziet hoe de laatste regel in de uitvoer zegt **totaal: 0**, die geen actieve batches wordt voorgesteld.</span><span class="sxs-lookup"><span data-stu-id="33754-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="33754-148">Laten we nu een batch-job indienen.</span><span class="sxs-lookup"><span data-stu-id="33754-148">Let us now submit a batch job.</span></span> <span data-ttu-id="33754-149">Het volgende fragment maakt gebruik van een bestand voor invoer (input.txt) om door te geven van de jar-naam en de naam van de klasse als parameters.</span><span class="sxs-lookup"><span data-stu-id="33754-149">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="33754-150">Als u deze stappen vanuit een Windows-computer uitvoert, is met behulp van een bestand voor invoer de aanbevolen aanpak.</span><span class="sxs-lookup"><span data-stu-id="33754-150">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="33754-151">De parameters in het bestand **input.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="33754-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="33754-152">U ziet een uitvoer die vergelijkbaar is met het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="33754-152">You should see an output similar to the  following snippet:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="33754-153">U ziet hoe de laatste regel van de uitvoer zegt **status: vanaf**.</span><span class="sxs-lookup"><span data-stu-id="33754-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="33754-154">Ook wordt, **-id: 0**.</span><span class="sxs-lookup"><span data-stu-id="33754-154">It also says, **id:0**.</span></span> <span data-ttu-id="33754-155">Hier **0** is van de batch-ID.</span><span class="sxs-lookup"><span data-stu-id="33754-155">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="33754-156">U kunt nu de status van deze specifieke batch met behulp van de batch-id ophalen</span><span class="sxs-lookup"><span data-stu-id="33754-156">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="33754-157">U ziet een uitvoer die vergelijkbaar is met het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="33754-157">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="33754-158">De uitvoer ziet u nu **status: geslaagd**, die wordt voorgesteld dat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="33754-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="33754-159">Als u wilt, kunt u nu de batch verwijderen.</span><span class="sxs-lookup"><span data-stu-id="33754-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="33754-160">U ziet een uitvoer die vergelijkbaar is met het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="33754-160">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="33754-161">De laatste regel van de uitvoer bevat de batch is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="33754-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="33754-162">Verwijderen van een taak, terwijl deze wordt uitgevoerd, de taak ook is funest.</span><span class="sxs-lookup"><span data-stu-id="33754-162">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="33754-163">Als u een taak die is voltooid, is of anderszins verwijdert worden verwijderd de taakgegevens volledig.</span><span class="sxs-lookup"><span data-stu-id="33754-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="33754-164">Gebruik van Livy Spark in HDInsight 3.5 clusters</span><span class="sxs-lookup"><span data-stu-id="33754-164">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="33754-165">3.5 HDInsight-cluster, schakelt het gebruik van lokale paden naar bestanden met voorbeeldgegevens toegang of potten standaard.</span><span class="sxs-lookup"><span data-stu-id="33754-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="33754-166">We raden u aan het gebruik van de `wasb://` pad in plaats daarvan potten openen of voorbeeldgegevens bestanden van het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="33754-167">Als u gebruiken, lokaal pad wilt, moet u de configuratie van de Ambari dienovereenkomstig bijwerken.</span><span class="sxs-lookup"><span data-stu-id="33754-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="33754-168">Dit doet u als volgt:</span><span class="sxs-lookup"><span data-stu-id="33754-168">To do so:</span></span>

1. <span data-ttu-id="33754-169">Ga naar de Ambari-portal voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="33754-170">De Ambari-Webgebruikersinterface is beschikbaar op uw HDInsight-cluster op https://**CLUSTERNAME**. azurehdidnsight.net, waarbij CLUSTERNAME de naam van het cluster is.</span><span class="sxs-lookup"><span data-stu-id="33754-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="33754-171">Klik in het linkernavigatievenster op **Livy**, en klik vervolgens op **Configs**.</span><span class="sxs-lookup"><span data-stu-id="33754-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="33754-172">Onder **livy-standaard** toevoegen de naam van de eigenschap `livy.file.local-dir-whitelist` en stel de waarde op **'/'** als u wilt toestaan dat volledige toegang tot bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="33754-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="33754-173">Als u toestaan dat alleen toegang tot een specifieke map wilt, geeft u het pad naar map als de waarde.</span><span class="sxs-lookup"><span data-stu-id="33754-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="33754-174">Verzenden van Livy taken voor een cluster binnen een virtuele Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="33754-174">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="33754-175">Als u verbinding met een HDInsight Spark-cluster uit een Azure-netwerk maakt, kunt u rechtstreeks verbinding met Livy op het cluster.</span><span class="sxs-lookup"><span data-stu-id="33754-175">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="33754-176">In dat geval moet de URL voor het eindpunt van Livy is `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="33754-176">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="33754-177">Hier **8998** is de poort waarop Livy wordt uitgevoerd op de cluster-headnode.</span><span class="sxs-lookup"><span data-stu-id="33754-177">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="33754-178">Zie voor meer informatie over de toegang tot services op niet-openbaar poorten [poorten die worden gebruikt door de services van Hadoop op HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="33754-178">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="33754-179">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="33754-179">Troubleshooting</span></span>

<span data-ttu-id="33754-180">Hier volgen enkele problemen beschreven die u tegenkomen kunt tijdens het gebruik van Livy voor verzenden van externe taak Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="33754-180">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="33754-181">Gebruik een externe jar uit de extra opslag wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="33754-181">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="33754-182">**Probleem:** als uw job Livy Spark verwijst naar een externe jar vanuit het extra opslagaccount die is gekoppeld aan het cluster, de taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="33754-182">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="33754-183">**Oplossing:** Zorg ervoor dat de jar die u wilt gebruiken beschikbaar in de standaard-opslag die is gekoppeld aan het HDInsight-cluster is.</span><span class="sxs-lookup"><span data-stu-id="33754-183">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="33754-184">Volgende stap</span><span class="sxs-lookup"><span data-stu-id="33754-184">Next step</span></span>

* [<span data-ttu-id="33754-185">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="33754-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="33754-186">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="33754-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

