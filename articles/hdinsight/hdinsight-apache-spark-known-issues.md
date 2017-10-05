---
title: Problemen oplossen met Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: Meer informatie over problemen met Apache Spark-clusters in Azure HDInsight en hoe deze te omzeilen.
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
ms.openlocfilehash: 3a493a2c35a6cdd31bb1e4ff66113a8f8d97d4f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="0451f-103">Bekende problemen van Apache Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-103">Known issues for Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="0451f-104">Dit document houdt van alle bekende problemen voor de openbare preview van HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="0451f-104">This document keeps track of all the known issues for the HDInsight Spark public preview.</span></span>  

## <a name="livy-leaks-interactive-session"></a><span data-ttu-id="0451f-105">Livy lekt interactieve sessies</span><span class="sxs-lookup"><span data-stu-id="0451f-105">Livy leaks interactive session</span></span>
<span data-ttu-id="0451f-106">Wanneer Livy opnieuw wordt gestart (van Ambari of vanwege headnode 0 virtuele machine opnieuw opstarten) met een interactieve sessie nog steeds actief is, wordt er een sessie interactieve taak gelekt.</span><span class="sxs-lookup"><span data-stu-id="0451f-106">When Livy is restarted (from Ambari or due to headnode 0 virtual machine reboot) with an interactive session still alive, an interactive job session will be leaked.</span></span> <span data-ttu-id="0451f-107">Als gevolg hiervan worden nieuwe taken kunnen vastgelopen in de status goedgekeurd en kunnen niet worden gestart.</span><span class="sxs-lookup"><span data-stu-id="0451f-107">Because of this, new jobs can stuck in the Accepted state, and cannot be started.</span></span>

<span data-ttu-id="0451f-108">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="0451f-108">**Mitigation:**</span></span>

<span data-ttu-id="0451f-109">Gebruik de volgende procedure het probleem oplossen:</span><span class="sxs-lookup"><span data-stu-id="0451f-109">Use the following procedure to workaround the issue:</span></span>

1. <span data-ttu-id="0451f-110">SSH in headnode.</span><span class="sxs-lookup"><span data-stu-id="0451f-110">Ssh into headnode.</span></span> <span data-ttu-id="0451f-111">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="0451f-111">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0451f-112">Voer de volgende opdracht om de toepassing-id's van de interactieve taken gestart via Livy vinden.</span><span class="sxs-lookup"><span data-stu-id="0451f-112">Run the following command to find the application IDs of the interactive jobs started through Livy.</span></span> 
   
        yarn application –list
   
    <span data-ttu-id="0451f-113">De standaard-taak namen Livy worden als de taken zijn gestart met een interactieve sessie Livy met geen expliciete namen opgegeven voor de Livy-sessie gestart met Jupyter-notebook, de taaknaam van de zal starten met remotesparkmagics_ *.</span><span class="sxs-lookup"><span data-stu-id="0451f-113">The default job names will be Livy if the jobs were started with a Livy interactive session with no explicit names specified, For the Livy session started by Jupyter notebook, the job name will start with remotesparkmagics_*.</span></span> 
3. <span data-ttu-id="0451f-114">Voer de volgende opdracht om deze taken af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="0451f-114">Run the following command to kill those jobs.</span></span> 
   
        yarn application –kill <Application ID>

<span data-ttu-id="0451f-115">Nieuwe taken worden gestart met.</span><span class="sxs-lookup"><span data-stu-id="0451f-115">New jobs will start running.</span></span> 

## <a name="spark-history-server-not-started"></a><span data-ttu-id="0451f-116">Spark geschiedenis Server is niet gestart</span><span class="sxs-lookup"><span data-stu-id="0451f-116">Spark History Server not started</span></span>
<span data-ttu-id="0451f-117">Spark geschiedenis Server is niet automatisch gestart nadat een cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0451f-117">Spark History Server is not started automatically after a cluster is created.</span></span>  

<span data-ttu-id="0451f-118">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="0451f-118">**Mitigation:**</span></span> 

<span data-ttu-id="0451f-119">De geschiedenis-server handmatig starten vanaf Ambari.</span><span class="sxs-lookup"><span data-stu-id="0451f-119">Manually start the history server from Ambari.</span></span>

## <a name="permission-issue-in-spark-log-directory"></a><span data-ttu-id="0451f-120">Machtiging probleem in de logboekmap Spark</span><span class="sxs-lookup"><span data-stu-id="0451f-120">Permission issue in Spark log directory</span></span>
<span data-ttu-id="0451f-121">Wanneer hdiuser een taak met spark-submit verzendt, er is een fout java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (toestemming geweigerd) en het Stuurprogrammalogboek is niet geschreven.</span><span class="sxs-lookup"><span data-stu-id="0451f-121">When hdiuser submits a job with spark-submit, there is an error java.io.FileNotFoundException: /var/log/spark/sparkdriver_hdiuser.log (Permission denied) and the driver log is not written.</span></span> 

<span data-ttu-id="0451f-122">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="0451f-122">**Mitigation:**</span></span>

1. <span data-ttu-id="0451f-123">Hdiuser toevoegen aan de Hadoop-groep.</span><span class="sxs-lookup"><span data-stu-id="0451f-123">Add hdiuser to the Hadoop group.</span></span> 
2. <span data-ttu-id="0451f-124">Geef een 777 machtigingen op /var/log/spark na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="0451f-124">Provide 777 permissions on /var/log/spark after cluster creation.</span></span> 
3. <span data-ttu-id="0451f-125">De locatie van het logboekbestand spark met Ambari moet een map met 777 machtigingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="0451f-125">Update the spark log location using Ambari to be a directory with 777 permissions.</span></span>  
4. <span data-ttu-id="0451f-126">Voer spark-indienen als sudo.</span><span class="sxs-lookup"><span data-stu-id="0451f-126">Run spark-submit as sudo.</span></span>  

## <a name="spark-phoenix-connector-is-not-supported"></a><span data-ttu-id="0451f-127">Spark Phoenix connector wordt niet ondersteund</span><span class="sxs-lookup"><span data-stu-id="0451f-127">Spark-Phoenix connector is not supported</span></span>

<span data-ttu-id="0451f-128">De connector Spark Phoenix wordt momenteel niet ondersteund met een HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="0451f-128">Currently, the Spark-Phoenix connector is not supported with an HDInsight Spark cluster.</span></span>

<span data-ttu-id="0451f-129">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="0451f-129">**Mitigation:**</span></span>

<span data-ttu-id="0451f-130">In plaats daarvan moet u de Spark-HBase-connector gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0451f-130">You must use the Spark-HBase connector instead.</span></span> <span data-ttu-id="0451f-131">Zie voor instructies [Spark-HBase-connector gebruiken](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span><span class="sxs-lookup"><span data-stu-id="0451f-131">For instructions see [How to use Spark-HBase connector](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).</span></span>

## <a name="issues-related-to-jupyter-notebooks"></a><span data-ttu-id="0451f-132">Problemen met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="0451f-132">Issues related to Jupyter notebooks</span></span>
<span data-ttu-id="0451f-133">Hier volgen enkele bekende problemen die betrekking hebben op Jupyter-notebooks.</span><span class="sxs-lookup"><span data-stu-id="0451f-133">Following are some known issues related to Jupyter notebooks.</span></span>

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a><span data-ttu-id="0451f-134">Laptops met niet-ASCII-tekens in bestandsnamen</span><span class="sxs-lookup"><span data-stu-id="0451f-134">Notebooks with non-ASCII characters in filenames</span></span>
<span data-ttu-id="0451f-135">Jupyter-notebooks die kunnen worden gebruikt in HDInsight Spark-clusters mag geen niet-ASCII-tekens in bestandsnamen.</span><span class="sxs-lookup"><span data-stu-id="0451f-135">Jupyter notebooks that can be used in Spark HDInsight clusters should not have non-ASCII characters in filenames.</span></span> <span data-ttu-id="0451f-136">Als u probeert een bestand via de UI Jupyter een niet-ASCII-bestandsnaam heeft te uploaden, zal mislukken achtergrond (dat wil zeggen, Jupyter kunt u het bestand uploadt, maar deze won't ofwel een zichtbaar fout genereert).</span><span class="sxs-lookup"><span data-stu-id="0451f-136">If you try to upload a file through the Jupyter UI which has a non-ASCII filename, it will fail silently (that is, Jupyter won’t let you upload the file, but it won’t throw a visible error either).</span></span> 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a><span data-ttu-id="0451f-137">Fout tijdens het laden van notitieblokken van grotere</span><span class="sxs-lookup"><span data-stu-id="0451f-137">Error while loading notebooks of larger sizes</span></span>
<span data-ttu-id="0451f-138">U ziet mogelijk een fout  **`Error loading notebook`**  wanneer het laden van laptops die groter zijn.</span><span class="sxs-lookup"><span data-stu-id="0451f-138">You might see an error **`Error loading notebook`** when you load notebooks that are larger in size.</span></span>  

<span data-ttu-id="0451f-139">**Risicobeperking:**</span><span class="sxs-lookup"><span data-stu-id="0451f-139">**Mitigation:**</span></span>

<span data-ttu-id="0451f-140">Als u deze fout krijgt, betekent niet dat uw gegevens is beschadigd of verloren.</span><span class="sxs-lookup"><span data-stu-id="0451f-140">If you get this error, it does not mean your data is corrupt or lost.</span></span>  <span data-ttu-id="0451f-141">Uw laptops zich nog steeds op schijf in `/var/lib/jupyter`, en u kunt SSH in het cluster toegang toe hebben.</span><span class="sxs-lookup"><span data-stu-id="0451f-141">Your notebooks are still on disk in `/var/lib/jupyter`, and you can SSH into the cluster to access them.</span></span> <span data-ttu-id="0451f-142">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="0451f-142">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="0451f-143">Wanneer u verbinding hebt gemaakt met het cluster via SSH, kunt u uw notitieblokken kopiëren van het cluster op uw lokale computer (via SCP of WinSCP) als een back-up van alle belangrijke gegevens in de notebook gegevensverlies te voorkomen.</span><span class="sxs-lookup"><span data-stu-id="0451f-143">Once you have connected to the cluster using SSH, you can copy your notebooks from your cluster to your local machine (using SCP or WinSCP) as a backup to prevent the loss of any important data in the notebook.</span></span> <span data-ttu-id="0451f-144">U kunt vervolgens SSH-tunnel in uw headnode op poort 8001 voor toegang tot Jupyter zonder tussenkomst van de gateway.</span><span class="sxs-lookup"><span data-stu-id="0451f-144">You can then SSH tunnel into your headnode at port 8001 to access Jupyter without going through the gateway.</span></span>  <span data-ttu-id="0451f-145">U kunt daar schakelt u de uitvoer van uw laptop en sla opnieuw op om de grootte van de notebook te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="0451f-145">From there, you can clear the output of your notebook and re-save it to minimize the notebook’s size.</span></span>

<span data-ttu-id="0451f-146">Om te voorkomen dat deze fout in de toekomst, moet u enkele aanbevolen procedures volgen:</span><span class="sxs-lookup"><span data-stu-id="0451f-146">To prevent this error from happening in the future, you must follow some best practices:</span></span>

* <span data-ttu-id="0451f-147">Het is belangrijk klein te houden de notebook-grootte.</span><span class="sxs-lookup"><span data-stu-id="0451f-147">It is important to keep the notebook size small.</span></span> <span data-ttu-id="0451f-148">Elke uitvoer van uw Spark-taken die worden verzonden naar Jupyter wordt bewaard in de notebook.</span><span class="sxs-lookup"><span data-stu-id="0451f-148">Any output from your Spark jobs that is sent back to Jupyter is persisted in the notebook.</span></span>  <span data-ttu-id="0451f-149">Het is een best practice met Jupyter in het algemeen om te voorkomen dat actief `.collect()` op grote RDD of dataframes; in plaats daarvan als u bekijken van een RDD inhoud wilt, kunt u overwegen uitgevoerd `.take()` of `.sample()` zodat de uitvoer te groot niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="0451f-149">It is a best practice with Jupyter in general to avoid running `.collect()` on large RDD’s or dataframes; instead, if you want to peek at an RDD’s contents, consider running `.take()` or `.sample()` so that your output doesn’t get too big.</span></span>
* <span data-ttu-id="0451f-150">Ook als u een laptop opslaat, uitvoer Wis alle cellen wilt verkleinen.</span><span class="sxs-lookup"><span data-stu-id="0451f-150">Also, when you save a notebook, clear all output cells to reduce the size.</span></span>

### <a name="notebook-initial-startup-takes-longer-than-expected"></a><span data-ttu-id="0451f-151">Laptop opstarten duurt langer dan verwacht</span><span class="sxs-lookup"><span data-stu-id="0451f-151">Notebook initial startup takes longer than expected</span></span>
<span data-ttu-id="0451f-152">Eerste code-instructie in Jupyter-notebook met behulp van Spark magic kan meer dan een minuut duren.</span><span class="sxs-lookup"><span data-stu-id="0451f-152">First code statement in Jupyter notebook using Spark magic could take more than a minute.</span></span>  

<span data-ttu-id="0451f-153">**Uitleg:**</span><span class="sxs-lookup"><span data-stu-id="0451f-153">**Explanation:**</span></span>

<span data-ttu-id="0451f-154">Dit gebeurt omdat wanneer de eerste codecel wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0451f-154">This happens because when the first code cell is run.</span></span> <span data-ttu-id="0451f-155">Op de achtergrond Hiermee initieert u sessieconfiguratie en Spark, SQL en Hive-contexten worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="0451f-155">In the background this initiates session configuration and Spark, SQL, and Hive contexts are set.</span></span> <span data-ttu-id="0451f-156">Nadat deze contexten zijn ingesteld, wordt de eerste instructie is uitgevoerd en dit de indruk dat geeft duurde de instructie lang om te voltooien.</span><span class="sxs-lookup"><span data-stu-id="0451f-156">After these contexts are set, the first statement is run and this gives the impression that the statement took a long time to complete.</span></span>

### <a name="jupyter-notebook-timeout-in-creating-the-session"></a><span data-ttu-id="0451f-157">Jupyter-notebook time-out bij het maken van de sessie</span><span class="sxs-lookup"><span data-stu-id="0451f-157">Jupyter notebook timeout in creating the session</span></span>
<span data-ttu-id="0451f-158">Wanneer het Spark-cluster heeft onvoldoende resources, wordt de Spark en Pyspark kernels in de Jupyter-notebook time-out bij het maken van de sessie.</span><span class="sxs-lookup"><span data-stu-id="0451f-158">When Spark cluster is out of resources, the Spark and Pyspark kernels in the Jupyter notebook will timeout trying to create the session.</span></span> 

<span data-ttu-id="0451f-159">**Oplossingen:**</span><span class="sxs-lookup"><span data-stu-id="0451f-159">**Mitigations:**</span></span> 

1. <span data-ttu-id="0451f-160">Sommige resources in uw Spark-cluster door vrijmaken:</span><span class="sxs-lookup"><span data-stu-id="0451f-160">Free up some resources in your Spark cluster by:</span></span>
   
   * <span data-ttu-id="0451f-161">Andere laptops Spark gestopt door te gaan naar het menu sluit en stilstand of afsluiten in de Verkenner notebook te klikken.</span><span class="sxs-lookup"><span data-stu-id="0451f-161">Stopping other Spark notebooks by going to the Close and Halt menu or clicking Shutdown in the notebook explorer.</span></span>
   * <span data-ttu-id="0451f-162">Andere toepassingen Spark YARN wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="0451f-162">Stopping other Spark applications from YARN.</span></span>
2. <span data-ttu-id="0451f-163">Start opnieuw op de notebook die u probeert te starten.</span><span class="sxs-lookup"><span data-stu-id="0451f-163">Restart the notebook you were trying to start up.</span></span> <span data-ttu-id="0451f-164">Onvoldoende bronnen moeten beschikbaar zijn voor u nu een sessie te maken.</span><span class="sxs-lookup"><span data-stu-id="0451f-164">Enough resources should be available for you to create a session now.</span></span>

## <a name="see-also"></a><span data-ttu-id="0451f-165">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0451f-165">See also</span></span>
* [<span data-ttu-id="0451f-166">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-166">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="0451f-167">Scenario's</span><span class="sxs-lookup"><span data-stu-id="0451f-167">Scenarios</span></span>
* [<span data-ttu-id="0451f-168">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="0451f-168">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="0451f-169">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="0451f-169">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="0451f-170">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="0451f-170">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="0451f-171">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="0451f-171">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="0451f-172">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-172">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="0451f-173">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0451f-173">Create and run applications</span></span>
* [<span data-ttu-id="0451f-174">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="0451f-174">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="0451f-175">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="0451f-175">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="0451f-176">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="0451f-176">Tools and extensions</span></span>
* [<span data-ttu-id="0451f-177">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="0451f-177">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="0451f-178">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="0451f-178">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="0451f-179">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-179">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="0451f-180">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-180">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="0451f-181">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="0451f-181">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="0451f-182">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="0451f-182">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="0451f-183">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="0451f-183">Manage resources</span></span>
* [<span data-ttu-id="0451f-184">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0451f-184">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="0451f-185">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="0451f-185">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

