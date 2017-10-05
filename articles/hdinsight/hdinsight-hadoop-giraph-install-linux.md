---
title: Installeren en gebruiken van Giraph op HDInsight (Hadoop) - Azure | Microsoft Docs
description: Informatie over het installeren van Giraph op Linux gebaseerde HDInsight-clusters met behulp van scriptacties. Scriptacties kunnen u het cluster tijdens het maken, aanpassen door het wijzigen van de configuratie van het cluster of het installeren van hulpprogramma's en services.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="3f05e-104">Giraph installeren op HDInsight Hadoop-clusters en Giraph gebruiken voor het verwerken van grootschalige grafieken</span><span class="sxs-lookup"><span data-stu-id="3f05e-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="3f05e-105">Informatie over het installeren van Apache Giraph op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3f05e-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="3f05e-106">Het script actie-onderdeel van HDInsight kunt u voor het aanpassen van het cluster een bash-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="3f05e-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="3f05e-107">Scripts kunnen worden gebruikt voor het aanpassen van clusters tijdens en na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="3f05e-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3f05e-108">De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="3f05e-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3f05e-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="3f05e-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3f05e-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3f05e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3f05e-111"><a name="whatis"></a>Wat is Giraph</span><span class="sxs-lookup"><span data-stu-id="3f05e-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="3f05e-112">[Apache Giraph](http://giraph.apache.org/) Hiermee kunt u grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3f05e-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="3f05e-113">Grafieken model relaties tussen objecten.</span><span class="sxs-lookup"><span data-stu-id="3f05e-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="3f05e-114">De verbindingen tussen routers op een grote netwerk, zoals Internet of relaties tussen personen op sociale netwerken.</span><span class="sxs-lookup"><span data-stu-id="3f05e-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="3f05e-115">Grafiek verwerking kunt u tot reden van de relaties tussen de objecten in een grafiek, zoals:</span><span class="sxs-lookup"><span data-stu-id="3f05e-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="3f05e-116">Identificeren van mogelijke vrienden op basis van uw huidige relaties.</span><span class="sxs-lookup"><span data-stu-id="3f05e-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="3f05e-117">Identificeren van de kortste afstand tussen twee computers in een netwerk.</span><span class="sxs-lookup"><span data-stu-id="3f05e-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="3f05e-118">Berekenen van de positie van de pagina van webpagina's.</span><span class="sxs-lookup"><span data-stu-id="3f05e-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="3f05e-119">Onderdelen van het HDInsight-cluster worden volledig ondersteund: Microsoft Support helpt te isoleren en het oplossen van problemen met betrekking tot deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="3f05e-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="3f05e-120">Aangepaste onderdelen, zoals Giraph, ontvangt binnen commercieel redelijke ondersteuning u helpen het probleem verder op te lossen.</span><span class="sxs-lookup"><span data-stu-id="3f05e-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="3f05e-121">Microsoft Support kunt u mogelijk het oplossen van het probleem.</span><span class="sxs-lookup"><span data-stu-id="3f05e-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="3f05e-122">Als dat niet het geval is, moet u contact opnemen met open-source community's waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="3f05e-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="3f05e-123">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="3f05e-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="3f05e-124">Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="3f05e-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="3f05e-125">Wat het script doet</span><span class="sxs-lookup"><span data-stu-id="3f05e-125">What the script does</span></span>

<span data-ttu-id="3f05e-126">Dit script voert de volgende handelingen uit:</span><span class="sxs-lookup"><span data-stu-id="3f05e-126">This script performs the following actions:</span></span>

* <span data-ttu-id="3f05e-127">Giraph om te worden geïnstalleerd`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="3f05e-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="3f05e-128">Kopieert de `giraph-examples.jar` bestand standaard storage (WASB) voor uw cluster:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="3f05e-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="3f05e-129"><a name="install"></a>Giraph met behulp van scriptacties installeren</span><span class="sxs-lookup"><span data-stu-id="3f05e-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="3f05e-130">Een voorbeeld van een script Giraph installeren op een HDInsight-cluster is beschikbaar op de volgende locatie:</span><span class="sxs-lookup"><span data-stu-id="3f05e-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="3f05e-131">Deze sectie geeft instructies voor het gebruik van het voorbeeldscript tijdens het maken van het cluster met behulp van de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="3f05e-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3f05e-132">Een scriptactie kan worden toegepast met behulp van een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="3f05e-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="3f05e-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3f05e-133">Azure PowerShell</span></span>
> * <span data-ttu-id="3f05e-134">De Azure CLI</span><span class="sxs-lookup"><span data-stu-id="3f05e-134">The Azure CLI</span></span>
> * <span data-ttu-id="3f05e-135">De HDInsight-SDK voor .NET</span><span class="sxs-lookup"><span data-stu-id="3f05e-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="3f05e-136">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="3f05e-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="3f05e-137">U kunt ook scriptacties toepassen op clusters al wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3f05e-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="3f05e-138">Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3f05e-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="3f05e-139">Beginnen met het maken van een cluster met behulp van de stappen in [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md), maar niet maken uitvoert.</span><span class="sxs-lookup"><span data-stu-id="3f05e-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="3f05e-140">Op de **optionele configuratie** blade Selecteer **scriptacties**, en geef de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="3f05e-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="3f05e-141">**NAAM**: een beschrijvende naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="3f05e-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="3f05e-142">**SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="3f05e-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="3f05e-143">**HEAD**: deze vermelding controleren</span><span class="sxs-lookup"><span data-stu-id="3f05e-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="3f05e-144">**WERKNEMER**: laat u dit item niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3f05e-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3f05e-145">**ZOOKEEPER**: laat u dit item niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="3f05e-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3f05e-146">**PARAMETERS**: dit veld leeg laten</span><span class="sxs-lookup"><span data-stu-id="3f05e-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="3f05e-147">Aan de onderkant van de **scriptacties**, gebruiken de **Selecteer** om op te slaan van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="3f05e-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="3f05e-148">Gebruik tot slot de **Selecteer** knop aan de onderkant van de **optionele configuratie** blade informatie optionele configuratie wilt opslaan.</span><span class="sxs-lookup"><span data-stu-id="3f05e-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="3f05e-149">Doorgaan met het maken van het cluster, zoals beschreven in [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3f05e-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="3f05e-150"><a name="usegiraph"></a>Hoe gebruik Giraph in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="3f05e-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="3f05e-151">Zodra het cluster is gemaakt, gebruikt u de volgende stappen uit om uit te voeren in het voorbeeld SimpleShortestPathsComputation is opgenomen in Giraph.</span><span class="sxs-lookup"><span data-stu-id="3f05e-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="3f05e-152">In dit voorbeeld wordt het basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementatie voor het vinden van het kortste pad tussen de objecten in een grafiek.</span><span class="sxs-lookup"><span data-stu-id="3f05e-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="3f05e-153">Maak verbinding met het HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="3f05e-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3f05e-154">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="3f05e-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3f05e-155">Gebruik de volgende opdracht voor het maken van een bestand met de naam **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="3f05e-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="3f05e-156">Gebruik de volgende tekst als de inhoud van dit bestand:</span><span class="sxs-lookup"><span data-stu-id="3f05e-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="3f05e-157">Deze gegevens worden beschreven van een relatie tussen de objecten in een gerichte grafiek, via de indeling `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="3f05e-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="3f05e-158">Elke regel vertegenwoordigt een relatie tussen een `source_id` object en een of meer `dest_id` objecten.</span><span class="sxs-lookup"><span data-stu-id="3f05e-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="3f05e-159">De `edge_value` kunnen worden beschouwd als de sterkte of de afstand van de verbinding tussen `source_id` en `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="3f05e-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="3f05e-160">Getekend, en met de waarde (gewicht) als de afstand tussen de objecten, de gegevens kan eruitzien als in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="3f05e-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt getekend als cirkels met verschillende afstand tussen regels](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="3f05e-162">Gebruiken om het bestand opslaat, **Ctrl + X**, klikt u vervolgens **Y**, en tot slot **Enter** te accepteren van de bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="3f05e-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="3f05e-163">Gebruik de volgende gegevens opslaan in de primaire opslag voor uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="3f05e-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="3f05e-164">Voer het SimpleShortestPathsComputation voorbeeld met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="3f05e-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="3f05e-165">De parameters voor deze opdracht worden beschreven in de volgende tabel:</span><span class="sxs-lookup"><span data-stu-id="3f05e-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="3f05e-166">Parameter</span><span class="sxs-lookup"><span data-stu-id="3f05e-166">Parameter</span></span> | <span data-ttu-id="3f05e-167">Wat het doet</span><span class="sxs-lookup"><span data-stu-id="3f05e-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="3f05e-168">Het jar-bestand met de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3f05e-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="3f05e-169">De klasse die wordt gebruikt voor het starten van de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3f05e-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="3f05e-170">Het voorbeeld dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3f05e-170">The example that is used.</span></span> <span data-ttu-id="3f05e-171">In dit voorbeeld wordt het kortste pad tussen de 1-ID en alle andere id's in de grafiek berekend.</span><span class="sxs-lookup"><span data-stu-id="3f05e-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="3f05e-172">De headnode voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="3f05e-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="3f05e-173">De invoerindeling voor de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="3f05e-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="3f05e-174">Het bestand invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="3f05e-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="3f05e-175">De indeling van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="3f05e-175">The output format.</span></span> <span data-ttu-id="3f05e-176">In dit voorbeeld-ID en -waarde als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="3f05e-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="3f05e-177">De uitvoerlocatie.</span><span class="sxs-lookup"><span data-stu-id="3f05e-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="3f05e-178">Het aantal werknemers kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f05e-178">The number of workers to use.</span></span> <span data-ttu-id="3f05e-179">In dit voorbeeld 2.</span><span class="sxs-lookup"><span data-stu-id="3f05e-179">In this example, 2.</span></span> |

    <span data-ttu-id="3f05e-180">Zie voor meer informatie over deze en andere parameters gebruikt met Giraph voorbeelden de [Giraph Quick Start](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="3f05e-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="3f05e-181">Zodra de taak is voltooid, de resultaten worden opgeslagen in de **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="3f05e-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="3f05e-182">De naam van het uitvoerbestand beginnen met **onderdeel-m -** en moet eindigen met een getal dat aangeeft van de eerste, tweede, enzovoort-bestand.</span><span class="sxs-lookup"><span data-stu-id="3f05e-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="3f05e-183">Gebruik de volgende opdracht om de uitvoer weer te geven:</span><span class="sxs-lookup"><span data-stu-id="3f05e-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="3f05e-184">De uitvoer ziet er ongeveer de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3f05e-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="3f05e-185">De SimpleShortestPathComputation voorbeeld is harde code vastgelegd beginnen met object-ID 1 en de kortste route naar andere objecten.</span><span class="sxs-lookup"><span data-stu-id="3f05e-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="3f05e-186">De uitvoer is in de indeling van `destination_id` en `distance`.</span><span class="sxs-lookup"><span data-stu-id="3f05e-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="3f05e-187">De `distance` is de waarde (of het gewicht) van de randen afgelegd tussen object-ID 1 en de doel-ID.</span><span class="sxs-lookup"><span data-stu-id="3f05e-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="3f05e-188">Deze gegevens te visualiseren, kunt u de resultaten controleren door de kortste paden onderweg tussen ID 1 en alle andere objecten.</span><span class="sxs-lookup"><span data-stu-id="3f05e-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="3f05e-189">Het kortste pad tussen 1-ID en -ID 4 is 5.</span><span class="sxs-lookup"><span data-stu-id="3f05e-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="3f05e-190">Deze waarde is de totale afstand tussen <span style="color:orange">ID 1 en 3</span>, en vervolgens <span style="color:red">ID 3 en 4</span>.</span><span class="sxs-lookup"><span data-stu-id="3f05e-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Tekenen van objecten als cirkels met de kortste paden tussen getekend](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="3f05e-192">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f05e-192">Next steps</span></span>

* <span data-ttu-id="3f05e-193">[Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3f05e-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="3f05e-194">[Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3f05e-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
