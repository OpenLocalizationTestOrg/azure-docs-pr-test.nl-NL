---
title: aaaTroubleshoot Spark met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Spark en Azure HDInsight toocommon.
keywords: Azure HDInsight, Spark, veelgestelde vragen, het oplossen van de handleiding, bekende problemen, de configuratie van de toepassing, Ambari
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a><span data-ttu-id="ad75a-104">Spark oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad75a-104">Troubleshoot Spark by using Azure HDInsight</span></span>

<span data-ttu-id="ad75a-105">Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache Spark nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="ad75a-105">Learn about hello top issues and their resolutions when working with Apache Spark payloads in Apache Ambari.</span></span>

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a><span data-ttu-id="ad75a-106">Hoe kan ik een Spark-toepassing configureren met behulp van Ambari op clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-106">How do I configure a Spark application by using Ambari on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ad75a-107">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="ad75a-107">Resolution steps</span></span>

<span data-ttu-id="ad75a-108">Hallo configuratiewaarden voor deze procedure zijn eerder in HDInsight ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ad75a-108">hello configuration values for this procedure were previously set in HDInsight.</span></span> <span data-ttu-id="ad75a-109">Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ad75a-109">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

1. <span data-ttu-id="ad75a-110">Selecteer in de lijst Hallo van clusters, **Spark2**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-110">In hello list of clusters, select **Spark2**.</span></span>

    ![Selecteer de cluster in lijst](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. <span data-ttu-id="ad75a-112">Selecteer Hallo **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ad75a-112">Select hello **Configs** tab.</span></span>

    ![Selecteer Hallo Configs tabblad](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. <span data-ttu-id="ad75a-114">Selecteer in de lijst Hallo van configuraties, **standaardinstellingen van aangepaste spark2**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-114">In hello list of configurations, select **Custom-spark2-defaults**.</span></span>

    ![Selecteer de aangepaste-spark-standaardinstellingen](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. <span data-ttu-id="ad75a-116">Zoek naar Hallo waarde instellen dat u nodig hebt tooadjust, zoals **spark.executor.memory**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-116">Look for hello value setting that you need tooadjust, such as **spark.executor.memory**.</span></span> <span data-ttu-id="ad75a-117">In dit geval Hallo waarde van **4608m** is te hoog.</span><span class="sxs-lookup"><span data-stu-id="ad75a-117">In this case, hello value of **4608m** is too high.</span></span>

    ![Selecteer Hallo spark.executor.memory veld](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. <span data-ttu-id="ad75a-119">Set Hallo waarde toohello aanbevolen instelling.</span><span class="sxs-lookup"><span data-stu-id="ad75a-119">Set hello value toohello recommended setting.</span></span> <span data-ttu-id="ad75a-120">Hallo waarde **2048m** voor deze instelling wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="ad75a-120">hello value **2048m** is recommended for this setting.</span></span>

    ![Wijziging waarde too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. <span data-ttu-id="ad75a-122">Hallo waarde opslaan en sla vervolgens Hallo-configuratie.</span><span class="sxs-lookup"><span data-stu-id="ad75a-122">Save hello value, and then save hello configuration.</span></span> <span data-ttu-id="ad75a-123">Selecteer op de werkbalk Hallo **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-123">On hello toolbar, select **Save**.</span></span>

    ![Hallo-instelling en configuratie opslaan](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    <span data-ttu-id="ad75a-125">U wordt gewaarschuwd als alle configuraties aandacht vereisen.</span><span class="sxs-lookup"><span data-stu-id="ad75a-125">You are notified if any configurations need attention.</span></span> <span data-ttu-id="ad75a-126">Houd er rekening mee Hallo-items en selecteer vervolgens **toch doorgaan**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-126">Note hello items, and then select **Proceed Anyway**.</span></span> 

    ![Selecteer wilt u toch doorgaan](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    <span data-ttu-id="ad75a-128">Voeg een opmerking over Hallo configuratiewijzigingen en selecteer vervolgens **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-128">Write a note about hello configuration changes, and then select **Save**.</span></span>

    ![Voer een opmerking over Hallo wijzigingen](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. <span data-ttu-id="ad75a-130">Telkens wanneer een configuratie wordt opgeslagen, wordt u gevraagd toorestart Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ad75a-130">Whenever a configuration is saved, you are prompted toorestart hello service.</span></span> <span data-ttu-id="ad75a-131">Selecteer **opnieuw**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-131">Select **Restart**.</span></span>

    ![Opnieuw opstarten selecteren](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    <span data-ttu-id="ad75a-133">Bevestig Hallo opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="ad75a-133">Confirm hello restart.</span></span>

    ![Selecteer bevestigen alle opnieuw starten](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    <span data-ttu-id="ad75a-135">Hallo-processen die worden uitgevoerd, kunt u bekijken.</span><span class="sxs-lookup"><span data-stu-id="ad75a-135">You can review hello processes that are running.</span></span>

    ![Bekijk actieve processen](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. <span data-ttu-id="ad75a-137">U kunt configuraties kunt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ad75a-137">You can add configurations.</span></span> <span data-ttu-id="ad75a-138">Selecteer in de lijst Hallo van configuraties, **standaardinstellingen van aangepaste spark2**, en selecteer vervolgens **eigenschap toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-138">In hello list of configurations, select **Custom-spark2-defaults**, and then select **Add Property**.</span></span>

    ![Selecteer een eigenschap toevoegen](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. <span data-ttu-id="ad75a-140">Een nieuwe eigenschap definiëren.</span><span class="sxs-lookup"><span data-stu-id="ad75a-140">Define a new property.</span></span> <span data-ttu-id="ad75a-141">U kunt één eigenschap definiëren met behulp van een dialoogvenster voor specifieke instellingen, bijvoorbeeld Hallo-gegevenstype.</span><span class="sxs-lookup"><span data-stu-id="ad75a-141">You can define a single property by using a dialog box for specific settings such as hello data type.</span></span> <span data-ttu-id="ad75a-142">Of u kunt meerdere eigenschappen definiëren met behulp van één definitie per regel.</span><span class="sxs-lookup"><span data-stu-id="ad75a-142">Or, you can define multiple properties by using one definition per line.</span></span> 

    <span data-ttu-id="ad75a-143">In dit voorbeeld Hallo **spark.driver.memory** eigenschap is gedefinieerd met een waarde van **4g**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-143">In this example, hello **spark.driver.memory** property is defined with a value of **4g**.</span></span>

    ![Nieuwe eigenschap definiëren](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. <span data-ttu-id="ad75a-145">Hallo-configuratie op te slaan en Hallo-service vervolgens opnieuw te starten zoals beschreven in stap 6 en 7.</span><span class="sxs-lookup"><span data-stu-id="ad75a-145">Save hello configuration, and then restart hello service as described in steps 6 and 7.</span></span>

<span data-ttu-id="ad75a-146">Deze wijzigingen zijn hele cluster, maar kunnen worden genegeerd wanneer u Hallo Spark taak indient.</span><span class="sxs-lookup"><span data-stu-id="ad75a-146">These changes are cluster-wide but can be overridden when you submit hello Spark job.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="ad75a-147">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad75a-147">Additional reading</span></span>

[<span data-ttu-id="ad75a-148">Verzending van de taak Spark in HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-148">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a><span data-ttu-id="ad75a-149">Hoe kan ik een Spark-toepassing configureren met behulp van een Jupyter-notebook in clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-149">How do I configure a Spark application by using a Jupyter notebook on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ad75a-150">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="ad75a-150">Resolution steps</span></span>

1. <span data-ttu-id="ad75a-151">Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ad75a-151">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="ad75a-152">In de eerste cel Hallo van Hallo Jupyter-notebook na Hallo **%% configureren** richtlijn Hallo Spark-configuraties in geldige JSON-indeling opgeven.</span><span class="sxs-lookup"><span data-stu-id="ad75a-152">In hello first cell of hello Jupyter notebook, after hello **%%configure** directive, specify hello Spark configurations in valid JSON format.</span></span> <span data-ttu-id="ad75a-153">De werkelijke waarden Hallo zo nodig wijzigen:</span><span class="sxs-lookup"><span data-stu-id="ad75a-153">Change hello actual values as necessary:</span></span>

    ![Een configuratie toevoegen](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a><span data-ttu-id="ad75a-155">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad75a-155">Additional reading</span></span>

[<span data-ttu-id="ad75a-156">Verzending van de taak Spark in HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-156">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a><span data-ttu-id="ad75a-157">Hoe kan ik een Spark-toepassing configureren met behulp van Livy op clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-157">How do I configure a Spark application by using Livy on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ad75a-158">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="ad75a-158">Resolution steps</span></span>

1. <span data-ttu-id="ad75a-159">Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ad75a-159">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span> 

2. <span data-ttu-id="ad75a-160">Hallo Spark toepassing tooLivy verzenden met behulp van een REST-client, zoals cURL.</span><span class="sxs-lookup"><span data-stu-id="ad75a-160">Submit hello Spark application tooLivy by using a REST client like cURL.</span></span> <span data-ttu-id="ad75a-161">Gebruik een opdracht vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="ad75a-161">Use a command similar toohello following.</span></span> <span data-ttu-id="ad75a-162">De werkelijke waarden Hallo zo nodig wijzigen:</span><span class="sxs-lookup"><span data-stu-id="ad75a-162">Change hello actual values as necessary:</span></span>

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a><span data-ttu-id="ad75a-163">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad75a-163">Additional reading</span></span>

[<span data-ttu-id="ad75a-164">Verzending van de taak Spark in HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-164">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a><span data-ttu-id="ad75a-165">Hoe configureer een toepassing met behulp van spark indienen Spark op clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-165">How do I configure a Spark application by using spark-submit on clusters</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="ad75a-166">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="ad75a-166">Resolution steps</span></span>

1. <span data-ttu-id="ad75a-167">Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).</span><span class="sxs-lookup"><span data-stu-id="ad75a-167">toodetermine which Spark configurations need toobe set and toowhat values, see [What causes a Spark application OutofMemoryError exception](#what-causes-a-spark-application-outofmemoryerror-exception).</span></span>

2. <span data-ttu-id="ad75a-168">Spark-shell start met behulp van een opdracht vergelijkbare toohello volgende.</span><span class="sxs-lookup"><span data-stu-id="ad75a-168">Launch spark-shell by using a command similar toohello following.</span></span> <span data-ttu-id="ad75a-169">Hallo werkelijke waarde van Hallo configuraties zo nodig wijzigen:</span><span class="sxs-lookup"><span data-stu-id="ad75a-169">Change hello actual value of hello configurations as necessary:</span></span> 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a><span data-ttu-id="ad75a-170">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad75a-170">Additional reading</span></span>

[<span data-ttu-id="ad75a-171">Verzending van de taak Spark in HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ad75a-171">Spark job submission on HDInsight clusters</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a><span data-ttu-id="ad75a-172">Wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt</span><span class="sxs-lookup"><span data-stu-id="ad75a-172">What causes a Spark application OutofMemoryError exception</span></span>

### <a name="detailed-description"></a><span data-ttu-id="ad75a-173">Gedetailleerde beschrijving</span><span class="sxs-lookup"><span data-stu-id="ad75a-173">Detailed description</span></span>

<span data-ttu-id="ad75a-174">Hallo Spark toepassing mislukt met de volgende typen van niet-onderschepte uitzonderingen Hallo:</span><span class="sxs-lookup"><span data-stu-id="ad75a-174">hello Spark application fails, with hello following types of uncaught exceptions:</span></span>

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a><span data-ttu-id="ad75a-175">Mogelijke oorzaak</span><span class="sxs-lookup"><span data-stu-id="ad75a-175">Probable cause</span></span>

<span data-ttu-id="ad75a-176">Hallo meest waarschijnlijke oorzaak van deze uitzondering is dat niet voldoende geheugen toohello Java virtuele machines (JVMs) wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="ad75a-176">hello most likely cause of this exception is that not enough heap memory is allocated toohello Java virtual machines (JVMs).</span></span> <span data-ttu-id="ad75a-177">Deze JVMs worden gestart als Executor of stuurprogramma's als onderdeel van Hallo Spark-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad75a-177">These JVMs are launched as executors or drivers as part of hello Spark application.</span></span> 

### <a name="resolution-steps"></a><span data-ttu-id="ad75a-178">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="ad75a-178">Resolution steps</span></span>

1. <span data-ttu-id="ad75a-179">Maximale grootte van Hallo gegevens Hallo Spark toepassing ingangen Hallo bepalen.</span><span class="sxs-lookup"><span data-stu-id="ad75a-179">Determine hello maximum size of hello data hello Spark application handles.</span></span> <span data-ttu-id="ad75a-180">U kunt een schatting op basis van de maximale grootte Hallo van Hallo invoergegevens Hallo tussenliggende gegevens die wordt geproduceerd door transformeren Hallo invoergegevens en Hallo uitvoergegevens die wordt gemaakt bij het Hallo-toepassing is verder Hallo tussenliggende gegevens transformeren.</span><span class="sxs-lookup"><span data-stu-id="ad75a-180">You can make a guess based on hello maximum size of hello input data, hello intermediate data that's produced by transforming hello input data, and hello output data that's produced when hello application is further transforming hello intermediate data.</span></span> <span data-ttu-id="ad75a-181">Dit proces is een iteratief als u een initiële formele schatting niet maken.</span><span class="sxs-lookup"><span data-stu-id="ad75a-181">This process can be an iterative if you can't make an initial formal guess.</span></span> 

2. <span data-ttu-id="ad75a-182">Zorg ervoor dat Hallo HDInsight-cluster dat u gaat toouse heeft onvoldoende bronnen in termen van geheugen en kernen tooaccommodate Hallo Spark toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad75a-182">Make sure that hello HDInsight cluster that you're going toouse has enough resources in terms of memory and cores tooaccommodate hello Spark application.</span></span> <span data-ttu-id="ad75a-183">U kunt dit vaststellen door Hallo cluster metrische gegevens sectie van de gebruikersinterface van YARN Hallo Hallo waarden weer te geven van **geheugen gebruikt** vs. **Totaal geheugen**, en **VCores gebruikt** vs. **Totaal aantal VCores**.</span><span class="sxs-lookup"><span data-stu-id="ad75a-183">You can determine this by viewing hello cluster metrics section of hello YARN UI for hello values of **Memory Used** vs. **Memory Total**, and **VCores Used** vs. **VCores Total**.</span></span>

3. <span data-ttu-id="ad75a-184">Hallo Spark volgende configuraties tooappropriate waarden, dit mag niet meer dan 90% van het beschikbare geheugen Hallo en kernen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="ad75a-184">Set hello following Spark configurations tooappropriate values, which should not exceed 90% of hello available memory and cores.</span></span> <span data-ttu-id="ad75a-185">Hallo-waarden moet binnen de geheugenvereisten Hallo Hallo Spark-toepassing:</span><span class="sxs-lookup"><span data-stu-id="ad75a-185">hello values should be well within hello memory requirements of hello Spark application:</span></span> 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    <span data-ttu-id="ad75a-186">tooget hello Totaal geheugen gebruikt door alle Executor, Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ad75a-186">tooget hello total memory used by all executors, run hello following command:</span></span> 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    <span data-ttu-id="ad75a-187">tooget hello Totaal geheugen gebruikt door het Hallo-stuurprogramma Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ad75a-187">tooget hello total memory used by hello driver, run hello following command:</span></span>
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a><span data-ttu-id="ad75a-188">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="ad75a-188">Additional reading</span></span>

- [<span data-ttu-id="ad75a-189">Overzicht van Spark geheugen</span><span class="sxs-lookup"><span data-stu-id="ad75a-189">Spark memory management overview</span></span>](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [<span data-ttu-id="ad75a-190">Fouten opsporen in een Spark-toepassing op een HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="ad75a-190">Debug a Spark application on an HDInsight cluster</span></span>](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

