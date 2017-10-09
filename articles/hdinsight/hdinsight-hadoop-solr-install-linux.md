---
title: aaaUse scriptactie tooinstall Solr op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall Solr op Linux gebaseerde HDInsight Hadoop-clusters met behulp van scriptacties.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="2d3b5-103">Installeren en gebruiken van Solr op HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="2d3b5-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="2d3b5-104">Meer informatie over hoe tooinstall Solr in Azure HDInsight met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="2d3b5-105">Solr is een krachtige search-platform en biedt zoekmogelijkheden op bedrijfsniveau op gegevens die worden beheerd door Hadoop.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="2d3b5-106">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="2d3b5-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2d3b5-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d3b5-109">Solr 4.9 installeert Hallo voorbeeldscript in dit document gebruikt met een specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="2d3b5-110">Als u wilt tooconfigure hello Solr cluster met verschillende verzamelingen, shards, schema's, replica's, enz., moet u Hallo script en Solr binaire bestanden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="2d3b5-111"><a name="whatis"></a>Wat is Solr</span><span class="sxs-lookup"><span data-stu-id="2d3b5-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="2d3b5-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="2d3b5-113">Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr zoekmogelijkheden Hallo tooquickly ophalen Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="2d3b5-114">Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="2d3b5-115">Aangepaste onderdelen, zoals Solr, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="2d3b5-116">Microsoft ondersteuning mogelijk niet kunnen tooresolve problemen met aangepaste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="2d3b5-117">U moet mogelijk tooengage Hallo open-source community's voor ondersteuning.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="2d3b5-118">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="2d3b5-119">Welke Hallo script doet</span><span class="sxs-lookup"><span data-stu-id="2d3b5-119">What hello script does</span></span>

<span data-ttu-id="2d3b5-120">Dit script maakt Hallo wijzigingen toohello HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="2d3b5-121">Solr 4.9 in geïnstalleerd`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="2d3b5-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="2d3b5-122">Hiermee maakt u een gebruiker **solrusr**, namelijk gebruikte toorun hello Solr service</span><span class="sxs-lookup"><span data-stu-id="2d3b5-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="2d3b5-123">Sets **solruser** als eigenaar van Hallo`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="2d3b5-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="2d3b5-124">Voegt een [Upstart](http://upstart.ubuntu.com/) configuratie die Solr automatisch wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="2d3b5-125"><a name="install"></a>Installeren met behulp van scriptacties Solr</span><span class="sxs-lookup"><span data-stu-id="2d3b5-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="2d3b5-126">Een voorbeeld script tooinstall Solr op een HDInsight-cluster is beschikbaar op Hallo locatie te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="2d3b5-127">een cluster met Solr geïnstalleerd toocreate, gebruik Hallo stappen in Hallo [HDInsight-clusters maken](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="2d3b5-128">Gebruik tijdens het Hallo maken, Hallo stappen tooinstall Solr te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="2d3b5-129">Van Hallo __Cluster samenvatting__ blade, select__Advanced settings__, klikt u vervolgens __acties Script__.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="2d3b5-130">Hallo toopopulate Hallo formulier volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="2d3b5-131">**NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="2d3b5-132">**SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="2d3b5-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="2d3b5-133">**HEAD**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="2d3b5-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="2d3b5-134">**WERKNEMER**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="2d3b5-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="2d3b5-135">**ZOOKEEPER**: Schakel deze optie tooinstall op Hallo Zookeeper knooppunt</span><span class="sxs-lookup"><span data-stu-id="2d3b5-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="2d3b5-136">**PARAMETERS**: dit veld leeg laten</span><span class="sxs-lookup"><span data-stu-id="2d3b5-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="2d3b5-137">Hallo Hallo onderaan in **acties Script** blade, gebruik Hallo **Selecteer** knop toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="2d3b5-138">Gebruik tot slot Hallo **volgende** knop tooreturn toohello __Cluster samenvatting__</span><span class="sxs-lookup"><span data-stu-id="2d3b5-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="2d3b5-139">Van Hallo __Cluster samenvatting__ pagina __maken__ toocreate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="2d3b5-140"><a name="usesolr"></a>Hoe gebruik Solr in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2d3b5-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2d3b5-141">Hallo stappen in deze sectie laten zien basisfunctionaliteit Solr.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="2d3b5-142">Zie voor meer informatie over het gebruik van Solr hello [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="2d3b5-143">Indexgegevens</span><span class="sxs-lookup"><span data-stu-id="2d3b5-143">Index data</span></span>

<span data-ttu-id="2d3b5-144">Hallo te volgen stappen tooadd voorbeeld gegevens tooSolr gebruiken en deze vervolgens een query:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="2d3b5-145">Verbinding maken met toohello HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="2d3b5-146">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="2d3b5-147">Stappen verderop in dit document wordt een SSL-tunnel tooconnect toohello Solr webgebruikersinterface gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="2d3b5-148">toouse deze stappen, moet u een met SSL maken tunnel en configureer vervolgens uw browser toouse deze.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="2d3b5-149">Zie voor meer informatie, Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="2d3b5-150">Gebruik Hallo opdrachten toohave Solr index-voorbeeldgegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="2d3b5-151">Hallo volgende uitvoergegevens toohello console:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="2d3b5-152">Hallo `post.jar` hulpprogramma voegt Hallo **solr.xml** en **monitor.xml** documenten toohello index.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="2d3b5-153">Gebruik Hallo opdracht tooquery hello Solr REST-API te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="2d3b5-154">Met deze opdracht wordt gezocht **collection1** voor documenten die overeenkomen met  **\*:\***  (gecodeerd als \*% 3A\* in de queryreeks Hallo).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="2d3b5-155">Hallo volgende JSON-document is een voorbeeld van een antwoord Hallo:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-155">hello following JSON document is an example of hello response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="2d3b5-156">Met behulp van Hallo Solr dashboard</span><span class="sxs-lookup"><span data-stu-id="2d3b5-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="2d3b5-157">Hallo Solr dashboard is een webgebruikersinterface waarmee u toowork met Solr via uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="2d3b5-158">Hallo Solr dashboard is niet beschikbaar gemaakt rechtstreeks op Hallo Internet van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="2d3b5-159">U kunt een SSH-tunnel tooaccess deze.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="2d3b5-160">Zie voor meer informatie over het gebruik van een SSH-tunnel Hallo [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="2d3b5-161">Wanneer u een SSH-tunnel hebt ingesteld, gebruikt u Hallo stappen toouse hello Solr dashboard te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="2d3b5-162">Hallo-hostnaam voor de primaire headnode Hallo bepalen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="2d3b5-163">Gebruik SSH tooconnect toohello cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="2d3b5-164">Bijvoorbeeld `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="2d3b5-165">Zie voor meer informatie over het gebruik van SSH Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="2d3b5-166">Gebruik Hallo opdracht tooget Hallo volledig gekwalificeerde hostnaam te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="2d3b5-167">Met deze opdracht retourneert een waarde van een vergelijkbare toohello hostnaam te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="2d3b5-168">Hallo-waarde geretourneerd, niet opslaan omdat het wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="2d3b5-169">In uw browser te verbinden**solr-http://HOSTNAME:8983 / #/**, waarbij **hostnaam** is Hallo-naam die u in de vorige stappen Hallo bepaald.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="2d3b5-170">Hallo-aanvraag wordt doorgestuurd via Hallo SSH-tunnel toohello Solr webgebruikersinterface op uw cluster.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="2d3b5-171">Hallo-pagina wordt weergegeven vergelijkbaar toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-171">hello page appears similar toohello following image:</span></span>

    ![Afbeelding van Solr dashboard](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="2d3b5-173">Gebruik vanuit het linkerdeelvenster Hallo Hallo **Core Selector** vervolgkeuzelijst tooselect **collection1**.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="2d3b5-174">Meerdere vermeldingen moeten ze worden weergegeven onder **collection1**.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="2d3b5-175">Hallo vermeldingen onderstaande **collection1**, selecteer **Query**.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="2d3b5-176">Hallo waarden toopopulate Hallo zoekpagina volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="2d3b5-177">In Hallo **q** tekst Voer  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="2d3b5-178">Deze query retourneert alle Hallo-documenten die zijn geïndexeerd in Solr.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="2d3b5-179">Als u toosearch voor een specifieke tekenreeks binnen Hallo documenten wilt, kunt u hier die tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="2d3b5-180">In Hallo **wt** tekstvak, selecteer Hallo uitvoerindeling.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="2d3b5-181">Standaard is **json**.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-181">Default is **json**.</span></span>

     <span data-ttu-id="2d3b5-182">Tot slot selecteert Hallo **zoekopdracht uitvoeren** knop Hallo Hallo zoeken pate onderaan in.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="2d3b5-184">Hallo uitvoer retourneert Hallo twee documenten dat u toohello toegevoegd eerder index.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="2d3b5-185">Hallo uitvoer is vergelijkbaar toohello volgende JSON-document:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-185">hello output is similar toohello following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="2d3b5-186">Starten en stoppen Solr</span><span class="sxs-lookup"><span data-stu-id="2d3b5-186">Starting and stopping Solr</span></span>

<span data-ttu-id="2d3b5-187">Hallo opdrachten toomanually stoppen en starten Solr volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="2d3b5-188">Back-upgegevens van de geïndexeerde</span><span class="sxs-lookup"><span data-stu-id="2d3b5-188">Backup indexed data</span></span>

<span data-ttu-id="2d3b5-189">Gebruik Hallo tooback up Solr toohello standaard gegevensopslag voor uw cluster stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="2d3b5-190">Toohello-cluster via SSH verbinding en voer vervolgens Hallo opdracht tooget Hallo-hostnaam voor het hoofdknooppunt Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="2d3b5-191">Gebruik Hallo opdracht toocreate een momentopname van Hallo geïndexeerde gegevens te volgen.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="2d3b5-192">Vervang **hostnaam** met geretourneerd van de vorige opdracht Hallo Hallo-naam:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="2d3b5-193">Hallo-antwoord is vergelijkbaar toohello XML te volgen:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="2d3b5-194">Wijzig de mappen te`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="2d3b5-195">Er is een submap voor elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="2d3b5-196">De map voor elke verzameling bevat een `data` directory met Hallo-momentopname voor Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="2d3b5-197">toocreate een gecomprimeerd archief van snapshotmap hello, gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="2d3b5-198">Vervang Hallo `snapshot.20150806185338855` waarden met de naam van de Hallo van Hallo-momentopname voor uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="2d3b5-199">Deze opdracht maakt u een archief met de naam **snapshot.20150806185338855.tgz**, die inhoud Hallo Hallo bevat **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="2d3b5-200">U kunt vervolgens Hallo archief toohello van primaire clusteropslag met behulp van de volgende opdracht Hallo opslaan:</span><span class="sxs-lookup"><span data-stu-id="2d3b5-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="2d3b5-201">Zie voor meer informatie over het werken met Solr back-up en herstelbewerkingen [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2d3b5-202">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2d3b5-202">Next steps</span></span>

* <span data-ttu-id="2d3b5-203">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="2d3b5-204">Cluster aanpassing tooinstall die giraph op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="2d3b5-205">Giraph kunt u tooperform grafiek verwerken met behulp van Hadoop, en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="2d3b5-206">[Hue installeren op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2d3b5-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="2d3b5-207">Cluster aanpassing tooinstall Hue op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="2d3b5-208">HUE is dat een set van webtoepassingen toointeract gebruikt met een Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="2d3b5-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
