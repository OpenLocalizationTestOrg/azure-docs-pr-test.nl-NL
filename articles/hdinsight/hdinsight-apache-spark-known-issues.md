---
title: aaaTroubleshoot problemen met Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: Meer informatie over problemen met gerelateerde tooApache Spark-clusters in Azure HDInsight en hoe toowork rond de.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="c0994-103">Bekende problemen van Apache Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="c0994-104">Dit document houdt van alle Hallo bekende problemen bij het Hallo HDInsight Spark openbare preview.</span><span class="sxs-lookup"><span data-stu-id="c0994-104">This document keeps track of all hello known issues for hello HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="c0994-105">Livy lekt interactieve sessies</span><span class="sxs-lookup"><span data-stu-id="c0994-105">Livy leaks interactive session</span></span>
<span data-ttu-id="c0994-106">Wanneer Livy opnieuw wordt gestart (van Ambari of vervaldatum tooheadnode 0 virtuele machine opnieuw opstarten) met een interactieve sessie nog steeds actief is, wordt er een sessie interactieve taak gelekt.</span><span class="sxs-lookup"><span data-stu-id="c0994-106">When Livy is restarted (from Ambari or due tooheadnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="c0994-107">Als gevolg hiervan nieuwe taken kan blijven steken bij Hallo geaccepteerde status en kan niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="c0994-107">Because of this, new jobs can stuck in hello Accepted state, and cannot be started.</span></span>

<span data-ttu-id="c0994-108">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="c0994-108">**Mitigation:**</span></span>

<span data-ttu-id="c0994-109">Hallo te volgen procedure tooworkaround Hallo probleem gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c0994-109">Use hello following procedure tooworkaround hello issue:</span></span>

1. <span data-ttu-id="c0994-110">SSH in headnode.</span><span class="sxs-lookup"><span data-stu-id="c0994-110">Ssh into headnode.</span></span> <span data-ttu-id="c0994-111">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="c0994-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c0994-112">Voer Hallo na opdracht toofind Hallo toepassing-id's van Hallo interactieve taken gestart via Livy.</span><span class="sxs-lookup"><span data-stu-id="c0994-112">Run hello following command toofind hello application IDs of hello interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="c0994-113">Hallo taak standaardnamen worden Livy als Hallo taken zijn gestart met een interactieve sessie Livy met geen expliciete namen voor Hallo opgegeven Livy-sessie gestart door de Jupyter-notebook Hallo taaknaam begint met remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="c0994-113">hello default job names will be Livy if hello jobs were started with a Livy interactive session with no explicit names specified, For hello Livy session started by Jupyter notebook, hello job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="c0994-114">Hallo opdracht tookill volgende taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c0994-114">Run hello following command tookill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="c0994-115">Nieuwe taken worden gestart met.</span><span class="sxs-lookup"><span data-stu-id="c0994-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="c0994-116">Spark geschiedenis Server is niet gestart</span><span class="sxs-lookup"><span data-stu-id="c0994-116">Spark History Server not started</span></span>
<span data-ttu-id="c0994-117">Spark geschiedenis Server is niet automatisch gestart nadat een cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c0994-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="c0994-118">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="c0994-118">**Mitigation:**</span></span> 

<span data-ttu-id="c0994-119">Handmatig Hallo geschiedenis server starten vanaf Ambari.</span><span class="sxs-lookup"><span data-stu-id="c0994-119">Manually start hello history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="c0994-120">Machtiging probleem in de logboekmap Spark</span><span class="sxs-lookup"><span data-stu-id="c0994-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="c0994-121">Wanneer hdiuser een taak met spark-submit verzendt, er is een fout java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (toestemming geweigerd) en Hallo Stuurprogrammalogboek is niet geschreven.</span><span class="sxs-lookup"><span data-stu-id="c0994-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and hello driver log is not written.</span></span> 

<span data-ttu-id="c0994-122">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="c0994-122">**Mitigation:**</span></span>

1. <span data-ttu-id="c0994-123">Hdiuser toohello Hadoop groep toevoegen.</span><span class="sxs-lookup"><span data-stu-id="c0994-123">Add hdiuser toohello Hadoop group.</span></span> 
2. <span data-ttu-id="c0994-124">Geef een 777 machtigingen op /var/log/spark na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="c0994-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="c0994-125">Hallo spark-Logboeklocatie met Ambari toobe een map met 777 machtigingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="c0994-125">Update hello spark log location using Ambari toobe a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="c0994-126">Voer spark-indienen als sudo.</span><span class="sxs-lookup"><span data-stu-id="c0994-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="c0994-127">Spark Phoenix connector wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="c0994-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="c0994-128">Hallo Spark Phoenix connector wordt momenteel niet ondersteund met een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="c0994-128">Currently, hello Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="c0994-129">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="c0994-129">**Mitigation:**</span></span>

<span data-ttu-id="c0994-130">In plaats daarvan moet u Hallo Spark-HBase-connector gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0994-130">You must use hello Spark-HBase connector instead.</span></span> <span data-ttu-id="c0994-131">Zie voor instructies [hoe toouse Spark HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="c0994-131">For instructions see [How toouse Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-toojupyter-notebooks"></a><span data-ttu-id="c0994-132">Problemen tooJupyter laptops</span><span class="sxs-lookup"><span data-stu-id="c0994-132">Issues related tooJupyter notebooks</span></span>
<span data-ttu-id="c0994-133">Hier volgen enkele bekende problemen gerelateerde tooJupyter laptops.</span><span class="sxs-lookup"><span data-stu-id="c0994-133">Following are some known issues related tooJupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="c0994-134">Laptops met niet-ASCII-tekens in bestandsnamen</span><span class="sxs-lookup"><span data-stu-id="c0994-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="c0994-135">Jupyter-notebooks die kunnen worden gebruikt in HDInsight Spark-clusters mag geen niet-ASCII-tekens in bestandsnamen.</span><span class="sxs-lookup"><span data-stu-id="c0994-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="c0994-136">Als u een bestand via Hallo Jupyter UI een niet-ASCII-bestandsnaam heeft tooupload probeert, zal mislukken achtergrond (dat wil zeggen, Jupyter kunt u Hallo-bestand uploaden, maar deze won't ofwel een zichtbaar fout genereert).</span><span class="sxs-lookup"><span data-stu-id="c0994-136">If you try tooupload a file through hello Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload hello file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="c0994-137">Fout tijdens het laden van notitieblokken van grotere</span><span class="sxs-lookup"><span data-stu-id="c0994-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="c0994-138">U ziet mogelijk een fout  **`Error loading notebook`**  wanneer het laden van laptops die groter zijn.</span><span class="sxs-lookup"><span data-stu-id="c0994-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="c0994-139">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="c0994-139">**Mitigation:**</span></span>

<span data-ttu-id="c0994-140">Als u deze fout krijgt, betekent niet dat uw gegevens is beschadigd of verloren.</span><span class="sxs-lookup"><span data-stu-id="c0994-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="c0994-141">Uw laptops zich nog steeds op schijf in `/var/lib/jupyter`, en u kunt SSH in Hallo cluster tooaccess ze.</span><span class="sxs-lookup"><span data-stu-id="c0994-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into hello cluster tooaccess them.</span></span> <span data-ttu-id="c0994-142">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="c0994-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="c0994-143">Zodra u toohello-cluster via SSH hebt gekoppeld, kunt u uw notitieblokken van uw cluster tooyour lokale computer (via SCP of WinSCP) als een back-tooprevent Hallo verlies van alle belangrijke gegevens in de notebook Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c0994-143">Once you have connected toohello cluster using SSH, you can copy your notebooks from your cluster tooyour local machine (using SCP or WinSCP) as a backup tooprevent hello loss of any important data in hello notebook.</span></span> <span data-ttu-id="c0994-144">U kunt vervolgens SSH-tunnel in uw headnode op poort 8001 tooaccess Jupyter zonder tussenkomst van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="c0994-144">You can then SSH tunnel into your headnode at port 8001 tooaccess Jupyter without going through hello gateway.</span></span>  <span data-ttu-id="c0994-145">Daar kunt u wist Hallo-uitvoer van uw laptop en sla opnieuw op toominimize Hallo notebook grootte.</span><span class="sxs-lookup"><span data-stu-id="c0994-145">From there, you can clear hello output of your notebook and re-save it toominimize hello notebook’s size.</span></span>

<span data-ttu-id="c0994-146">tooprevent deze fout voorkomen in Hallo toekomstige, moet u enkele aanbevolen procedures volgen:</span><span class="sxs-lookup"><span data-stu-id="c0994-146">tooprevent this error from happening in hello future, you must follow some best practices:</span></span>

* <span data-ttu-id="c0994-147">Het is belangrijk tookeep Hallo notebook grootte klein.</span><span class="sxs-lookup"><span data-stu-id="c0994-147">It is important tookeep hello notebook size small.</span></span> <span data-ttu-id="c0994-148">Elke uitvoer van uw Spark-taken die wordt teruggestuurd tooJupyter wordt bewaard in de notebook Hallo.</span><span class="sxs-lookup"><span data-stu-id="c0994-148">Any output from your Spark jobs that is sent back tooJupyter is persisted in hello notebook.</span></span>  <span data-ttu-id="c0994-149">Het is een best practice met Jupyter in algemene tooavoid met `.collect()` op grote RDD of dataframes; als u toopeek op een RDD inhoud wilt, overweeg in plaats daarvan uitgevoerd `.take()` of `.sample()` zodat de uitvoer te groot niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="c0994-149">It is a best practice with Jupyter in general tooavoid running `.collect()` on large RDD’s or dataframes; instead, if you want toopeek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="c0994-150">Ook als u een laptop opslaat, uitvoer Wis alle cellen tooreduce Hallo grootte.</span><span class="sxs-lookup"><span data-stu-id="c0994-150">Also, when you save a notebook, clear all output cells tooreduce hello size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="c0994-151">Laptop opstarten duurt langer dan verwacht</span><span class="sxs-lookup"><span data-stu-id="c0994-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="c0994-152">Eerste code-instructie in Jupyter-notebook met behulp van Spark magic kan meer dan een minuut duren.</span><span class="sxs-lookup"><span data-stu-id="c0994-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="c0994-153">**Uitleg:**</span><span class="sxs-lookup"><span data-stu-id="c0994-153">**Explanation:**</span></span>

<span data-ttu-id="c0994-154">Dit gebeurt omdat wanneer de eerste codecel hello wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c0994-154">This happens because when hello first code cell is run.</span></span> <span data-ttu-id="c0994-155">Op de achtergrond Hallo Hiermee initieert u sessieconfiguratie en Spark, SQL en Hive-contexten worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c0994-155">In hello background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="c0994-156">Nadat deze contexten zijn ingesteld, de eerste instructie hello wordt uitgevoerd en daarmee Hallo indruk dat Hallo-instructie een toocomplete lang duurde.</span><span class="sxs-lookup"><span data-stu-id="c0994-156">After these contexts are set, hello first statement is run and this gives hello impression that hello statement took a long time toocomplete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a><span data-ttu-id="c0994-157">De time-out voor de Jupyter-notebook in Hallo-sessie maken</span><span class="sxs-lookup"><span data-stu-id="c0994-157">Jupyter notebook timeout in creating hello session</span></span>
<span data-ttu-id="c0994-158">Wanneer het Spark-cluster heeft onvoldoende resources, wordt Hallo Spark en Pyspark kernels in Hallo Jupyter-notebook time-out bij het toocreate Hallo-sessie.</span><span class="sxs-lookup"><span data-stu-id="c0994-158">When Spark cluster is out of resources, hello Spark and Pyspark kernels in hello Jupyter notebook will timeout trying toocreate hello session.</span></span> 

<span data-ttu-id="c0994-159">**Oplossingen:**</span><span class="sxs-lookup"><span data-stu-id="c0994-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="c0994-160">Sommige resources in uw Spark-cluster door vrijmaken:</span><span class="sxs-lookup"><span data-stu-id="c0994-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="c0994-161">Stoppen van andere laptops Spark toohello gaat sluiten en stoppen menu of afsluiten in Hallo notebook explorer te klikken.</span><span class="sxs-lookup"><span data-stu-id="c0994-161">Stopping other Spark notebooks by going toohello Close and Halt menu or clicking Shutdown in hello notebook explorer.</span></span>
   * <span data-ttu-id="c0994-162">Andere toepassingen Spark YARN wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="c0994-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="c0994-163">Hallo-notebook die u toostart van probeerde opnieuw opstarten</span><span class="sxs-lookup"><span data-stu-id="c0994-163">Restart hello notebook you were trying toostart up.</span></span> <span data-ttu-id="c0994-164">Onvoldoende bronnen moeten beschikbaar zijn voor u toocreate nu een sessie.</span><span class="sxs-lookup"><span data-stu-id="c0994-164">Enough resources should be available for you toocreate a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="c0994-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c0994-165">See also</span></span>
* [<span data-ttu-id="c0994-166">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="c0994-167">Scenario's</span><span class="sxs-lookup"><span data-stu-id="c0994-167">Scenarios</span></span>
* [<span data-ttu-id="c0994-168">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="c0994-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="c0994-169">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="c0994-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="c0994-170">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="c0994-170">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="c0994-171">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="c0994-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="c0994-172">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="c0994-173">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c0994-173">Create and run applications</span></span>
* [<span data-ttu-id="c0994-174">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="c0994-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="c0994-175">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="c0994-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="c0994-176">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="c0994-176">Tools and extensions</span></span>
* [<span data-ttu-id="c0994-177">De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="c0994-177">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="c0994-178">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="c0994-178">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="c0994-179">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="c0994-180">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="c0994-181">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="c0994-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="c0994-182">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="c0994-182">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="c0994-183">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="c0994-183">Manage resources</span></span>
* [<span data-ttu-id="c0994-184">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c0994-184">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="c0994-185">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="c0994-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

