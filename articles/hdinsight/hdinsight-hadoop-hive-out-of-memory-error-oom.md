---
title: een component buiten geheugenfout in Azure HDInsight aaaFix | Microsoft Docs
description: Herstel van een component buiten geheugenfout in HDInsight. Hallo klant scenario is een query voor veel grote tabellen.
keywords: buiten-geheugeninstellingen fout, OOM, Hive
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="4c8f2-105">Herstel van een component buiten geheugenfout in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="4c8f2-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="4c8f2-106">Meer informatie over hoe een component buiten geheugenfout toofix verwerken wanneer grote tabellen met het configureren van instellingen voor Hive-geheugen.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="4c8f2-107">Hive-query uitvoeren op grote tabellen</span><span class="sxs-lookup"><span data-stu-id="4c8f2-107">Run Hive query against large tables</span></span>

<span data-ttu-id="4c8f2-108">Een klant een Hive-query is uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="4c8f2-109">Sommige nuances van deze query:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-109">Some nuances of this query:</span></span>

* <span data-ttu-id="4c8f2-110">T1 is een alias tooa big tabel, Tabel1, waarvoor veel kolommen van het type tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="4c8f2-111">Andere tabellen zijn niet die groot maar hoeven veel kolommen.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="4c8f2-112">Alle tabellen zijn lid te worden van elkaar worden verbonden, in sommige gevallen met meerdere kolommen in TABLE1 en anderen.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="4c8f2-113">Hallo Hive-query duurde 26 minuten toofinish op een knooppunt 24 A3 HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="4c8f2-114">Hallo klant opgemerkt Hallo waarschuwingsberichten te volgen:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="4c8f2-115">Met behulp van Hallo Tez-uitvoeringsengine.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="4c8f2-116">Hallo dezelfde query uitgevoerd gedurende 15 minuten en vervolgens heeft Hallo volgende fout:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="4c8f2-117">Hallo fout blijft wanneer u een grotere virtuele machine (bijvoorbeeld D12).</span><span class="sxs-lookup"><span data-stu-id="4c8f2-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="4c8f2-118">Hallo onvoldoende geheugen beschikbaar voor foutopsporing</span><span class="sxs-lookup"><span data-stu-id="4c8f2-118">Debug hello out of memory error</span></span>

<span data-ttu-id="4c8f2-119">Onze support en engineeringteams samen gevonden Hallo problemen veroorzaakt Hallo onvoldoende geheugen beschikbaar was een [bekend probleem dat wordt beschreven in Hallo Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="4c8f2-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="4c8f2-120">Hallo **hive.auto.convert.join.noconditionaltask** in Hallo hive-site.xml bestand te is ingesteld**true**:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="4c8f2-121">Is het waarschijnlijk kaart join was Hallo oorzaak Hallo Java Heap ruimte onze van geheugenfout.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="4c8f2-122">Zoals uitgelegd in Hallo blogbericht [Hadoop Yarn-geheugeninstellingen in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx)wanneer daadwerkelijk toohello Tez container van Tez-uitvoeringsengine gebruikte Hallo heap ruimte gebruikt is.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="4c8f2-123">Zie Hallo installatiekopie beschrijving Hallo Tez container geheugen te volgen.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-123">See hello following image describing hello Tez container memory.</span></span>

![Tez container geheugen diagram: Hive-fout: onvoldoende geheugen](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="4c8f2-125">Als Hallo blogbericht wordt voorgesteld, Hallo na twee geheugeninstellingen Hallo container geheugen voor Hallo heap definiëren: **hive.tez.container.size** en **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="4c8f2-126">Uit onze ervaring betekent Hallo buiten geheugen-uitzondering niet dat Hallo container is te klein.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="4c8f2-127">Betekent dit Hallo Java, heap-grootte (hive.tez.java.opts) is te klein.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="4c8f2-128">Dus als er onvoldoende geheugen, u tooincrease proberen kunt **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="4c8f2-129">Indien nodig moet u wellicht tooincrease **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="4c8f2-130">Hallo **java.opts** instelling moet ongeveer 80% van **container.size**.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="4c8f2-131">Hallo-instelling **hive.tez.java.opts** moet altijd kleiner zijn dan **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="4c8f2-132">Omdat een machine D12 28GB geheugen heeft, we besloten toouse een grootte van de container van 10GB (10240MB) en toojava.opts 80% toewijzen:</span><span class="sxs-lookup"><span data-stu-id="4c8f2-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="4c8f2-133">Met de nieuwe instellingen Hallo Hallo-query is uitgevoerd onder 10 minuten.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4c8f2-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4c8f2-134">Next steps</span></span>

<span data-ttu-id="4c8f2-135">Ophalen van een OOM fout betekent niet dat Hallo container is te klein.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="4c8f2-136">In plaats daarvan moet u de geheugeninstellingen Hallo configureren zodat hello, heap-grootte is toegenomen en ten minste 80% van de grootte van het systeemgeheugen Hallo container.</span><span class="sxs-lookup"><span data-stu-id="4c8f2-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="4c8f2-137">Zie voor het optimaliseren van Hive-query's [optimaliseren Hive-query's voor Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="4c8f2-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
