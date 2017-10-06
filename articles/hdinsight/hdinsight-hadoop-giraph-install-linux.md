---
title: aaaInstall en Giraph op HDInsight (Hadoop) - Azure gebruiken | Microsoft Docs
description: Meer informatie over hoe tooinstall Giraph op Linux gebaseerde HDInsight-clusters met behulp van scriptacties. Scriptacties kunnen u toocustomize Hallo cluster tijdens het maken, door het wijzigen van de configuratie van het cluster of het installeren van hulpprogramma's en services.
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
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="20678-104">Giraph installeren op HDInsight Hadoop-clusters en Giraph tooprocess grootschalige grafieken gebruiken</span><span class="sxs-lookup"><span data-stu-id="20678-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="20678-105">Meer informatie over hoe tooinstall Apache Giraph op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="20678-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="20678-106">Hallo script actie functie van HDInsight kunt u toocustomize uw cluster een bash-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="20678-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="20678-107">Scripts kunnen gebruikte toocustomize clusters worden tijdens en na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="20678-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20678-108">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="20678-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="20678-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="20678-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="20678-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="20678-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="20678-111"><a name="whatis"></a>Wat is Giraph</span><span class="sxs-lookup"><span data-stu-id="20678-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="20678-112">[Apache Giraph](http://giraph.apache.org/) kunt u tooperform grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="20678-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="20678-113">Grafieken model relaties tussen objecten.</span><span class="sxs-lookup"><span data-stu-id="20678-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="20678-114">Hallo-verbindingen tussen routers op een groot netwerk, zoals Internet Hallo of relaties tussen mensen op sociale netwerken.</span><span class="sxs-lookup"><span data-stu-id="20678-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="20678-115">Grafiek verwerking kunt u tooreason over Hallo relaties tussen de objecten in een grafiek, zoals:</span><span class="sxs-lookup"><span data-stu-id="20678-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="20678-116">Identificeren van mogelijke vrienden op basis van uw huidige relaties.</span><span class="sxs-lookup"><span data-stu-id="20678-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="20678-117">Identificerende Hallo kortste afstand tussen twee computers in een netwerk.</span><span class="sxs-lookup"><span data-stu-id="20678-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="20678-118">Berekenen Hallo pagina positie van webpagina's.</span><span class="sxs-lookup"><span data-stu-id="20678-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="20678-119">Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund: Microsoft Support helpt tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.</span><span class="sxs-lookup"><span data-stu-id="20678-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="20678-120">Aangepaste onderdelen, zoals Giraph, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="20678-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="20678-121">Microsoft Support mogelijk kunnen tooresolving Hallo probleem.</span><span class="sxs-lookup"><span data-stu-id="20678-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="20678-122">Als dat niet het geval is, moet u contact opnemen met open-source community's waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="20678-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="20678-123">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="20678-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="20678-124">Welke Hallo script doet</span><span class="sxs-lookup"><span data-stu-id="20678-124">What hello script does</span></span>

<span data-ttu-id="20678-125">Dit script voert Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="20678-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="20678-126">Giraph te worden geïnstalleerd`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="20678-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="20678-127">Kopieën Hallo `giraph-examples.jar` bestandsopslag toodefault (WASB) voor uw cluster:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="20678-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="20678-128"><a name="install"></a>Giraph met behulp van scriptacties installeren</span><span class="sxs-lookup"><span data-stu-id="20678-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="20678-129">Een voorbeeld script tooinstall Giraph op een HDInsight-cluster is beschikbaar op Hallo locatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="20678-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="20678-130">Deze sectie bevat instructies over hoe toouse voorbeeldscript Hallo tijdens het Hallo-cluster maken met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="20678-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="20678-131">Een scriptactie kan worden toegepast met behulp van een Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="20678-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="20678-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="20678-132">Azure PowerShell</span></span>
> * <span data-ttu-id="20678-133">Hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="20678-133">hello Azure CLI</span></span>
> * <span data-ttu-id="20678-134">Hallo HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="20678-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="20678-135">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="20678-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="20678-136">U kunt ook script acties tooalready actieve clusters toepassen.</span><span class="sxs-lookup"><span data-stu-id="20678-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="20678-137">Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="20678-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="20678-138">Beginnen met het maken van een cluster met behulp van de stappen in Hallo [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md), maar niet maken uitvoert.</span><span class="sxs-lookup"><span data-stu-id="20678-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="20678-139">Op Hallo **optionele configuratie** blade Selecteer **scriptacties**, en geef Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="20678-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="20678-140">**NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="20678-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="20678-141">**SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="20678-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="20678-142">**HEAD**: deze vermelding controleren</span><span class="sxs-lookup"><span data-stu-id="20678-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="20678-143">**WERKNEMER**: laat u dit item niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="20678-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="20678-144">**ZOOKEEPER**: laat u dit item niet ingeschakeld</span><span class="sxs-lookup"><span data-stu-id="20678-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="20678-145">**PARAMETERS**: dit veld leeg laten</span><span class="sxs-lookup"><span data-stu-id="20678-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="20678-146">Hallo Hallo onderaan in **scriptacties**, hello gebruiken **Selecteer** knop toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="20678-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="20678-147">Gebruik tot slot Hallo **Selecteer** knop onderin Hallo Hallo **optionele configuratie** blade toosave Hallo optionele configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="20678-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="20678-148">Doorgaan met het Hallo-cluster maken, zoals beschreven in [maken Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20678-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="20678-149"><a name="usegiraph"></a>Hoe gebruik Giraph in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="20678-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="20678-150">Zodra Hallo-cluster is gemaakt, gebruikt u Hallo stappen toorun hello SimpleShortestPathsComputation voorbeeld is opgenomen in Giraph te volgen.</span><span class="sxs-lookup"><span data-stu-id="20678-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="20678-151">In dit voorbeeld wordt Hallo basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementatie voor het vinden van Hallo kortste pad tussen de objecten in een grafiek.</span><span class="sxs-lookup"><span data-stu-id="20678-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="20678-152">Verbinding maken met toohello HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="20678-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="20678-153">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="20678-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="20678-154">Gebruik Hallo volgende opdracht toocreate uit een bestand met de naam **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="20678-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="20678-155">Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="20678-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="20678-156">Deze gegevens beschrijft de relatie tussen de objecten in een gerichte grafiek, met behulp van notatie Hallo `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="20678-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="20678-157">Elke regel vertegenwoordigt een relatie tussen een `source_id` object en een of meer `dest_id` objecten.</span><span class="sxs-lookup"><span data-stu-id="20678-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="20678-158">Hallo `edge_value` kunnen worden beschouwd als Hallo sterkte of de afstand van de verbinding tussen Hallo `source_id` en `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="20678-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="20678-159">Getekend, en met Hallo waarde (gewicht) als Hallo afstand tussen de objecten, Hallo gegevens als volgt uitzien Hallo-diagram te volgen:</span><span class="sxs-lookup"><span data-stu-id="20678-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt getekend als cirkels met verschillende afstand tussen regels](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="20678-161">Gebruik-bestand Hallo toosave **Ctrl + X**, vervolgens **Y**, en tot slot **Enter** tooaccept Hallo-bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="20678-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="20678-162">Gebruik Hallo toostore Hallo gegevens naar de primaire opslag voor uw HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="20678-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="20678-163">Hallo SimpleShortestPathsComputation voorbeeld met behulp van de volgende opdracht Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="20678-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="20678-164">Hallo-parameters die worden gebruikt met deze opdracht worden beschreven in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="20678-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="20678-165">Parameter</span><span class="sxs-lookup"><span data-stu-id="20678-165">Parameter</span></span> | <span data-ttu-id="20678-166">Wat het doet</span><span class="sxs-lookup"><span data-stu-id="20678-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="20678-167">Hallo jar-bestand met de Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="20678-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="20678-168">Hallo klasse gebruikt toostart Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="20678-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="20678-169">Hallo-voorbeeld dat wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="20678-169">hello example that is used.</span></span> <span data-ttu-id="20678-170">In dit voorbeeld wordt de kortste pad Hallo tussen ID 1 en alle andere id's in de grafiek Hallo berekend.</span><span class="sxs-lookup"><span data-stu-id="20678-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="20678-171">Hallo headnode voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="20678-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="20678-172">Hallo invoerindeling toouse voor Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="20678-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="20678-173">Hallo invoergegevens bestand.</span><span class="sxs-lookup"><span data-stu-id="20678-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="20678-174">Hallo uitvoer-indeling.</span><span class="sxs-lookup"><span data-stu-id="20678-174">hello output format.</span></span> <span data-ttu-id="20678-175">In dit voorbeeld-ID en -waarde als tekst zonder opmaak.</span><span class="sxs-lookup"><span data-stu-id="20678-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="20678-176">Hallo uitvoerlocatie.</span><span class="sxs-lookup"><span data-stu-id="20678-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="20678-177">Hallo aantal werknemers toouse.</span><span class="sxs-lookup"><span data-stu-id="20678-177">hello number of workers toouse.</span></span> <span data-ttu-id="20678-178">In dit voorbeeld 2.</span><span class="sxs-lookup"><span data-stu-id="20678-178">In this example, 2.</span></span> |

    <span data-ttu-id="20678-179">Zie voor meer informatie over deze en andere parameters gebruikt met Giraph voorbeelden Hallo [Giraph Quick Start](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="20678-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="20678-180">Zodra het Hallo-taak is voltooid, Hallo resultaten worden opgeslagen in Hallo **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="20678-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="20678-181">Hallo uitvoer bestandsnamen beginnen met **onderdeel-m -** en eindigen met een getal dat aangeeft Hallo eerst tweede, enzovoort-bestand.</span><span class="sxs-lookup"><span data-stu-id="20678-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="20678-182">Hallo opdrachtuitvoer tooview Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="20678-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="20678-183">Hallo-uitvoer moet worden weergegeven vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="20678-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="20678-184">Hallo SimpleShortestPathComputation voorbeeld is vastgelegde toostart met object-ID 1 en Hallo kortste pad tooother objecten zoeken.</span><span class="sxs-lookup"><span data-stu-id="20678-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="20678-185">Hallo-uitvoer is in de indeling van Hallo `destination_id` en `distance`.</span><span class="sxs-lookup"><span data-stu-id="20678-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="20678-186">Hallo `distance` Hallo waarde (of gewicht) van Hallo randen afgelegd ligt tussen object-ID 1 en Hallo doel-ID.</span><span class="sxs-lookup"><span data-stu-id="20678-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="20678-187">U kunt deze gegevens te visualiseren, Hallo resultaten controleren door onderweg Hallo kortste paden tussen de 1-ID en alle andere objecten.</span><span class="sxs-lookup"><span data-stu-id="20678-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="20678-188">Hallo kortste pad tussen ID 1 en 4-ID is 5.</span><span class="sxs-lookup"><span data-stu-id="20678-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="20678-189">Deze waarde is de totale afstand Hallo tussen <span style="color:orange">ID 1 en 3</span>, en vervolgens <span style="color:red">ID 3 en 4</span>.</span><span class="sxs-lookup"><span data-stu-id="20678-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Tekenen van objecten als cirkels met de kortste paden tussen getekend](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="20678-191">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="20678-191">Next steps</span></span>

* <span data-ttu-id="20678-192">[Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="20678-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="20678-193">[Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="20678-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
