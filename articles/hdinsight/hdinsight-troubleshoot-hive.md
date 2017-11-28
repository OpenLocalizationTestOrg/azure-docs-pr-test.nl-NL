---
title: aaaTroubleshoot Hive met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Hive en Azure HDInsight toocommon.
keywords: HDInsight, Hive, veelgestelde vragen over Azure, probleemoplossingsgids, veelgestelde vragen
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="8d448-104">Hive oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8d448-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="8d448-105">Meer informatie over de vragen Hallo en hun oplossingen bij het werken met Apache Hive nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="8d448-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="8d448-106">Hoe ik een Hive-metastore exporteren en importeren op een ander cluster</span><span class="sxs-lookup"><span data-stu-id="8d448-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="8d448-107">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="8d448-107">Resolution steps</span></span>

1. <span data-ttu-id="8d448-108">Verbinding toohello HDInsight-cluster via een Secure Shell (SSH)-client.</span><span class="sxs-lookup"><span data-stu-id="8d448-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="8d448-109">Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="8d448-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="8d448-110">Hallo volgende opdracht op Hallo HDInsight-cluster waaruit u tooexport hello metastore wilt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8d448-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="8d448-111">Met deze opdracht genereert u een bestand met de naam allatables.sql.</span><span class="sxs-lookup"><span data-stu-id="8d448-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="8d448-112">Hallo bestand alltables.sql toohello nieuwe HDInsight-cluster te kopiëren en voer vervolgens Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d448-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="8d448-113">Hallo-code in de stappen voor het oplossen van Hallo wordt ervan uitgegaan dat gegevens op het nieuwe cluster Hallo paden zijn dezelfde Hallo als Hallo gegevenspaden op Hallo oude cluster.</span><span class="sxs-lookup"><span data-stu-id="8d448-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="8d448-114">Als de gegevenspaden Hallo verschillend zijn, kunt u handmatig bewerken Hallo gegenereerd alltables.sql bestand tooreflect eventuele wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="8d448-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="8d448-115">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d448-115">Additional reading</span></span>

- [<span data-ttu-id="8d448-116">Verbinding tooan HDInsight-cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="8d448-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="8d448-117">Hoe ga ik Hive logboeken naar op een cluster</span><span class="sxs-lookup"><span data-stu-id="8d448-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="8d448-118">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="8d448-118">Resolution steps</span></span>

1. <span data-ttu-id="8d448-119">Verbinding toohello HDInsight-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="8d448-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="8d448-120">Zie voor meer informatie **lezen van aanvullende**.</span><span class="sxs-lookup"><span data-stu-id="8d448-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="8d448-121">clientlogboeken tooview Hive, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d448-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="8d448-122">tooview Hive metastore logboeken Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d448-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="8d448-123">tooview Hiveserver, gebruikt u Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d448-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="8d448-124">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d448-124">Additional reading</span></span>

- [<span data-ttu-id="8d448-125">Verbinding tooan HDInsight-cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="8d448-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="8d448-126">Hoe ik Hallo Hive-shell met specifieke configuraties die op een cluster starten</span><span class="sxs-lookup"><span data-stu-id="8d448-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="8d448-127">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="8d448-127">Resolution steps</span></span>

1. <span data-ttu-id="8d448-128">Geef een sleutel-waardepaar configuratie wanneer u Hallo Hive-shell start.</span><span class="sxs-lookup"><span data-stu-id="8d448-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="8d448-129">Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="8d448-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="8d448-130">toolist alle effectieve configuraties op Hive-shell, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d448-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="8d448-131">Gebruik bijvoorbeeld Hallo Hive-opdrachtshell toostart volgen met de logboekregistratie voor foutopsporing is ingeschakeld op het Hallo-console:</span><span class="sxs-lookup"><span data-stu-id="8d448-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="8d448-132">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d448-132">Additional reading</span></span>

- [<span data-ttu-id="8d448-133">Hive-configuratie-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="8d448-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="8d448-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Hoe analyseer ik Tez DAG gegevens op een cluster kritiek pad</span><span class="sxs-lookup"><span data-stu-id="8d448-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="8d448-135">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="8d448-135">Resolution steps</span></span>
 
1. <span data-ttu-id="8d448-136">een Apache Tez tooanalyze omgeleid acyclische grafiek (DAG) in een cluster kritieke grafiek, toohello HDInsight-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="8d448-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="8d448-137">Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="8d448-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="8d448-138">Voer bij een opdrachtprompt Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d448-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="8d448-139">toolist andere analyzers die kunnen worden gebruikt tooanalyze Tez-DAG Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d448-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="8d448-140">Als eerste argument hello, moet u een voorbeeldprogramma opgeven.</span><span class="sxs-lookup"><span data-stu-id="8d448-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="8d448-141">Namen van geldig programma zijn onder andere:</span><span class="sxs-lookup"><span data-stu-id="8d448-141">Valid program names include:</span></span>
    - <span data-ttu-id="8d448-142">**ContainerReuseAnalyzer**: details van de container opnieuw kunnen worden gebruikt in een DAG afdrukken</span><span class="sxs-lookup"><span data-stu-id="8d448-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="8d448-143">**CriticalPath**: Find Hallo kritieke pad van een DAG</span><span class="sxs-lookup"><span data-stu-id="8d448-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="8d448-144">**LocalityAnalyzer**: details in een DAG plaats afdrukken</span><span class="sxs-lookup"><span data-stu-id="8d448-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="8d448-145">**ShuffleTimeAnalyzer**: Hallo willekeurige volgorde tijd details in een DAG analyseren</span><span class="sxs-lookup"><span data-stu-id="8d448-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="8d448-146">**SkewAnalyzer**: Hallo scheeftrekken details in een DAG analyseren</span><span class="sxs-lookup"><span data-stu-id="8d448-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="8d448-147">**SlowNodeAnalyzer**: details knooppunt in een DAG afdrukken</span><span class="sxs-lookup"><span data-stu-id="8d448-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="8d448-148">**SlowTaskIdentifier**: afdrukken trage taakdetails in een DAG</span><span class="sxs-lookup"><span data-stu-id="8d448-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="8d448-149">**SlowestVertexAnalyzer**: traagste hoekpunt details in een DAG afdrukken</span><span class="sxs-lookup"><span data-stu-id="8d448-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="8d448-150">**SpillAnalyzer**: gelekt details afdrukken in een DAG</span><span class="sxs-lookup"><span data-stu-id="8d448-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="8d448-151">**TaskConcurrencyAnalyzer**: afdrukken Hallo taakdetails gelijktijdigheid van taken in een DAG</span><span class="sxs-lookup"><span data-stu-id="8d448-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="8d448-152">**VertexLevelCriticalPathAnalyzer**: Find Hallo kritieke pad op hoekpunt niveau in een DAG</span><span class="sxs-lookup"><span data-stu-id="8d448-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="8d448-153">Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d448-153">Additional reading</span></span>

- [<span data-ttu-id="8d448-154">Verbinding tooan HDInsight-cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="8d448-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="8d448-155">Hoe kan ik Tez DAG gegevens downloaden vanaf een cluster</span><span class="sxs-lookup"><span data-stu-id="8d448-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="8d448-156">Stappen voor het oplossen</span><span class="sxs-lookup"><span data-stu-id="8d448-156">Resolution steps</span></span>

<span data-ttu-id="8d448-157">Er zijn twee manieren toocollect hello Tez DAG gegevens:</span><span class="sxs-lookup"><span data-stu-id="8d448-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="8d448-158">Vanaf de opdrachtregel Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d448-158">From hello command line:</span></span>
 
    <span data-ttu-id="8d448-159">Verbinding toohello HDInsight-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="8d448-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="8d448-160">Voer Hallo volgende opdracht achter de opdrachtprompt Hallo:</span><span class="sxs-lookup"><span data-stu-id="8d448-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="8d448-161">Hallo Ambari Tez weergave gebruiken:</span><span class="sxs-lookup"><span data-stu-id="8d448-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="8d448-162">Ga tooAmbari.</span><span class="sxs-lookup"><span data-stu-id="8d448-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="8d448-163">Ga tooTez weergave (onder Hallo tegels pictogram in de rechterbovenhoek Hallo).</span><span class="sxs-lookup"><span data-stu-id="8d448-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="8d448-164">Selecteer Hallo gewenste tooview DAG.</span><span class="sxs-lookup"><span data-stu-id="8d448-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="8d448-165">Selecteer **downloaden van gegevens**.</span><span class="sxs-lookup"><span data-stu-id="8d448-165">Select **Download data**.</span></span>

### <span data-ttu-id="8d448-166"><a name="additional-reading-end"></a>Aanvullende bronnen</span><span class="sxs-lookup"><span data-stu-id="8d448-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="8d448-167">Verbinding tooan HDInsight-cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="8d448-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






