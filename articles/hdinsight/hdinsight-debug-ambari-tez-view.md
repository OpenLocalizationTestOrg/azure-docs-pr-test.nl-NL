---
title: aaaUse Ambari Tez weergave met HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse hello Ambari Tez toodebug Tez-taken weergeven op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="c77be-103">Ambari-weergaven toodebug Tez-taken op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="c77be-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="c77be-104">Hallo Ambari-Webgebruikersinterface voor HDInsight bevat een Tez-weergave die kan worden gebruikt toounderstand en foutopsporing functies die gebruikmaken van Tez.</span><span class="sxs-lookup"><span data-stu-id="c77be-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="c77be-105">Hallo Tez weergave kunt u toovisualize Hallo taak, zoals een grafiek van verbonden items Inzoomen op elk item en statistieken en logboekregistratie informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="c77be-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c77be-106">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="c77be-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c77be-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="c77be-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c77be-108">Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c77be-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c77be-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c77be-109">Prerequisites</span></span>

* <span data-ttu-id="c77be-110">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c77be-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c77be-111">Zie voor stapsgewijze instructies voor het maken van een cluster, [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c77be-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="c77be-112">Een moderne webbrowser met ondersteuning voor HTML5.</span><span class="sxs-lookup"><span data-stu-id="c77be-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="c77be-113">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="c77be-113">Understanding Tez</span></span>

<span data-ttu-id="c77be-114">Tez is een uitbreidbaar framework voor gegevensverwerking in Hadoop. deze groter snelheden dan traditionele MapReduce-verwerking biedt.</span><span class="sxs-lookup"><span data-stu-id="c77be-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="c77be-115">Voor Linux gebaseerde HDInsight-clusters is het standaard-engine Hallo voor Hive.</span><span class="sxs-lookup"><span data-stu-id="c77be-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="c77be-116">Tez maakt een omgeleid acyclische grafiek (DAG) die worden beschreven Hallo volgorde van acties die zijn vereist voor taken.</span><span class="sxs-lookup"><span data-stu-id="c77be-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="c77be-117">Afzonderlijke acties hoekpunten worden genoemd en het uitvoeren van een stukje Hallo algemene taak.</span><span class="sxs-lookup"><span data-stu-id="c77be-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="c77be-118">Hallo werkelijke uitvoering van Hallo werk beschreven door een hoekpunt een taak wordt aangeroepen en kan worden verdeeld over meerdere knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="c77be-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="c77be-119">Understanding Hallo Tez weergeven</span><span class="sxs-lookup"><span data-stu-id="c77be-119">Understanding hello Tez view</span></span>

<span data-ttu-id="c77be-120">Hallo Tez-weergave bevat zowel historische gegevens en informatie over processen die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c77be-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="c77be-121">Deze informatie laat zien hoe een taak wordt verdeeld tussen verschillende clusters.</span><span class="sxs-lookup"><span data-stu-id="c77be-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="c77be-122">Wordt ook gebruikt door taken en hoekpunten tellers en informatie over de fout gerelateerd toohello taak.</span><span class="sxs-lookup"><span data-stu-id="c77be-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="c77be-123">Kan deze u nuttige informatie in de volgende scenario's Hallo aanbieden:</span><span class="sxs-lookup"><span data-stu-id="c77be-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="c77be-124">Bewaking langlopende processen, weer te geven, Hallo voortgang van de kaart en taken te verminderen.</span><span class="sxs-lookup"><span data-stu-id="c77be-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="c77be-125">Historische gegevens voor de geslaagde of mislukte processen toolearn analyseren hoe verwerking kan worden verbeterd of waarom is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c77be-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="c77be-126">Genereren van een DAG</span><span class="sxs-lookup"><span data-stu-id="c77be-126">Generate a DAG</span></span>

<span data-ttu-id="c77be-127">Hallo Tez-weergave alleen gegevens bevat als een taak die gebruikmaakt van Hallo Tez-engine is momenteel wordt uitgevoerd of is eerder is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c77be-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="c77be-128">Eenvoudige Hive-query's kunnen worden opgelost zonder Tez.</span><span class="sxs-lookup"><span data-stu-id="c77be-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="c77be-129">Meer complexe query's die wilt filteren, groeperen, rangschikken, joins, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="c77be-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="c77be-130">Hallo Tez-engine gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c77be-130">use hello Tez engine.</span></span>

<span data-ttu-id="c77be-131">Volgende stappen toorun een Hive-query die gebruikmaakt van Tez hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="c77be-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="c77be-132">Navigeer in een webbrowser, toohttps://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c77be-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="c77be-133">Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **weergaven** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c77be-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="c77be-134">Dit pictogram ziet er als een reeks van de kwadraten uit.</span><span class="sxs-lookup"><span data-stu-id="c77be-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="c77be-135">Selecteer in de vervolgkeuzelijst Hallo die wordt weergegeven, **Hive-weergave**.</span><span class="sxs-lookup"><span data-stu-id="c77be-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Hive-weergave selecteren](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="c77be-137">Wanneer Hallo Hive-weergave wordt geladen plakken Hallo volgende query uitvoeren op Hallo Query-Editor en klik vervolgens op **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="c77be-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="c77be-138">Zodra Hallo-taak is voltooid, ziet u Hallo uitvoer weergegeven in Hallo **resultaten queryproces** sectie.</span><span class="sxs-lookup"><span data-stu-id="c77be-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="c77be-139">Hallo resultaten moeten vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="c77be-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="c77be-140">Selecteer Hallo **logboek** tabblad. Ziet u informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="c77be-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="c77be-141">Hallo opslaan **App-id** waarde, zoals deze waarde wordt gebruikt in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c77be-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="c77be-142">Gebruik Hallo Tez weergeven</span><span class="sxs-lookup"><span data-stu-id="c77be-142">Use hello Tez View</span></span>

1. <span data-ttu-id="c77be-143">Selecteer Hallo Hallo menu bovenaan Hallo Hallo pagina **weergaven** pictogram.</span><span class="sxs-lookup"><span data-stu-id="c77be-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="c77be-144">Selecteer in de vervolgkeuzelijst Hallo die wordt weergegeven, **Tez weergave**.</span><span class="sxs-lookup"><span data-stu-id="c77be-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Tez weergave selecteren](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="c77be-146">Als Hallo Tez weergave wordt geladen, ziet u een lijst met hive-query's die momenteel worden uitgevoerd, of zijn uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="c77be-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Alle dag 's](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="c77be-148">Als u slechts één vermelding hebt, is het voor Hallo-query die u hebt uitgevoerd in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="c77be-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="c77be-149">Als u meerdere vermeldingen hebt, kunt u zoeken met behulp van Hallo velden bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="c77be-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="c77be-150">Selecteer Hallo **Query-ID** voor een Hive-query.</span><span class="sxs-lookup"><span data-stu-id="c77be-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="c77be-151">Informatie over het Hallo-query wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="c77be-151">Information about hello query is displayed.</span></span>

    ![Details van de DAG](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="c77be-153">Hallo tabbladen op deze pagina kunt u tooview Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="c77be-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="c77be-154">**Details van een query**: meer informatie over Hallo Hive-query.</span><span class="sxs-lookup"><span data-stu-id="c77be-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="c77be-155">**Tijdlijn**: informatie over hoe lang duurde in elke fase van de verwerking.</span><span class="sxs-lookup"><span data-stu-id="c77be-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="c77be-156">**Configuraties**: Hallo-configuratie voor deze query gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c77be-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="c77be-157">Van __Query Details__ kunt u Hallo koppelingen toofind informatie over Hallo __toepassing__ of Hallo __DAG__ voor deze query.</span><span class="sxs-lookup"><span data-stu-id="c77be-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="c77be-158">Hallo __toepassing__ koppeling geeft informatie weer over Hallo YARN-toepassing voor deze query.</span><span class="sxs-lookup"><span data-stu-id="c77be-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="c77be-159">Hier kunt u Hallo YARN-Logboeken openen.</span><span class="sxs-lookup"><span data-stu-id="c77be-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="c77be-160">Hallo __DAG__ koppeling geeft informatie weer over Hallo gerichte acyclische grafiek voor deze query.</span><span class="sxs-lookup"><span data-stu-id="c77be-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="c77be-161">Hier kunt u een grafische weergave van Hallo DAG weergeven.</span><span class="sxs-lookup"><span data-stu-id="c77be-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="c77be-162">U kunt ook informatie over Hallo hoekpunten binnen Hallo DAG vinden.</span><span class="sxs-lookup"><span data-stu-id="c77be-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c77be-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c77be-163">Next Steps</span></span>

<span data-ttu-id="c77be-164">U hebt geleerd hoe toouse hello Tez bekijken, meer informatie over [met behulp van Hive in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c77be-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="c77be-165">Zie voor meer technische informatie op Tez hello [Tez-pagina op Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="c77be-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="c77be-166">Zie voor meer informatie over het gebruik van Ambari met HDInsight [beheren HDInsight-clusters met Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="c77be-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
