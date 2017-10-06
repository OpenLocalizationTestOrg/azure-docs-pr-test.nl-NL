---
title: aaaUse scriptactie tooinstall Solr op Hadoop-cluster - Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-cluster met Solr met behulp van de scriptactie.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="a29ba-103">Installeren en gebruiken van Solr op Windows gebaseerde HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="a29ba-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="a29ba-104">Meer informatie over hoe toocustomize HDInsight op basis van Windows-cluster met Solr met behulp van de scriptactie en hoe toouse Solr toosearch gegevens.</span><span class="sxs-lookup"><span data-stu-id="a29ba-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a29ba-105">Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="a29ba-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="a29ba-106">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="a29ba-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="a29ba-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="a29ba-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a29ba-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a29ba-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="a29ba-109">Zie voor meer informatie over het gebruik van Solr met een cluster op basis van Linux [installeert en gebruikt Solr op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a29ba-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="a29ba-110">U kunt Solr installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*.</span><span class="sxs-lookup"><span data-stu-id="a29ba-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="a29ba-111">Een voorbeeld script tooinstall Solr op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="a29ba-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="a29ba-112">Hallo-voorbeeldscript werkt alleen met HDInsight-cluster versie 3.1.</span><span class="sxs-lookup"><span data-stu-id="a29ba-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="a29ba-113">Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a29ba-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="a29ba-114">een cluster Solr op basis van Windows maakt Hello voorbeeldscript gebruikt in dit onderwerp met een specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="a29ba-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="a29ba-115">Als u wilt tooconfigure hello Solr cluster met verschillende verzamelingen, shards, schema's, replica's, enz., moet u Hallo script en Solr binaire bestanden dienovereenkomstig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a29ba-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="a29ba-116">**Verwante artikelen**</span><span class="sxs-lookup"><span data-stu-id="a29ba-116">**Related articles**</span></span>

* [<span data-ttu-id="a29ba-117">Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="a29ba-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="a29ba-118">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="a29ba-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="a29ba-119">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="a29ba-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="a29ba-120">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="a29ba-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="a29ba-121">Wat is Solr?</span><span class="sxs-lookup"><span data-stu-id="a29ba-121">What is Solr?</span></span>
<span data-ttu-id="a29ba-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens.</span><span class="sxs-lookup"><span data-stu-id="a29ba-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="a29ba-123">Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr zoekmogelijkheden Hallo tooquickly ophalen Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="a29ba-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="a29ba-124">Solr met portal installeren</span><span class="sxs-lookup"><span data-stu-id="a29ba-124">Install Solr using portal</span></span>
1. <span data-ttu-id="a29ba-125">Beginnen met het maken van een cluster met behulp van Hallo **aangepast maken** optie, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a29ba-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="a29ba-126">Op Hallo **scriptacties** pagina van wizard hello, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="a29ba-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="a29ba-127">![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize scriptactie gebruik een cluster")</span><span class="sxs-lookup"><span data-stu-id="a29ba-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="a29ba-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a29ba-128">Property</span></span></th><th><span data-ttu-id="a29ba-129">Waarde</span><span class="sxs-lookup"><span data-stu-id="a29ba-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="a29ba-130">Naam</span><span class="sxs-lookup"><span data-stu-id="a29ba-130">Name</span></span></td>
            <td><span data-ttu-id="a29ba-131">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="a29ba-131">Specify a name for hello script action.</span></span> <span data-ttu-id="a29ba-132">Bijvoorbeeld: <b>installeren Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="a29ba-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="a29ba-133">Script-URI</span><span class="sxs-lookup"><span data-stu-id="a29ba-133">Script URI</span></span></td>
            <td><span data-ttu-id="a29ba-134">Geef Hallo Uniform Resource Identifier (URI) toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a29ba-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="a29ba-135">Bijvoorbeeld: <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="a29ba-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="a29ba-136">Soort knooppunt</span><span class="sxs-lookup"><span data-stu-id="a29ba-136">Node Type</span></span></td>
            <td><span data-ttu-id="a29ba-137">Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a29ba-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="a29ba-138">U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b>.</span><span class="sxs-lookup"><span data-stu-id="a29ba-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="a29ba-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="a29ba-139">Parameters</span></span></td>
            <td><span data-ttu-id="a29ba-140">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="a29ba-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="a29ba-141">Hallo script tooinstall Solr vereist geen parameters, zodat u kunt dit leeg laten.</span><span class="sxs-lookup"><span data-stu-id="a29ba-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="a29ba-142">U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a29ba-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="a29ba-143">Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart Hallo cluster maken.</span><span class="sxs-lookup"><span data-stu-id="a29ba-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="a29ba-144">Solr gebruiken</span><span class="sxs-lookup"><span data-stu-id="a29ba-144">Use Solr</span></span>
<span data-ttu-id="a29ba-145">U moet beginnen met het indexeren Solr met enkele gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="a29ba-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="a29ba-146">U kunt vervolgens Solr toorun zoekquery's op Hallo geïndexeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="a29ba-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="a29ba-147">Voer Hallo stappen toouse Solr in een HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="a29ba-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="a29ba-148">**Remote Desktop Protocol (RDP) tooremote in Hallo HDInsight-cluster gebruiken met Solr geïnstalleerd**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="a29ba-149">Van hello Azure-portal, moet u extern bureaublad inschakelen voor u met Solr hello geïnstalleerd en vervolgens afstand verbinding met cluster gemaakt Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a29ba-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="a29ba-150">Zie voor instructies [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="a29ba-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="a29ba-151">**Index Solr door gegevensbestanden uploaden**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="a29ba-152">Wanneer u de index Solr, plaatst u documenten in die u wellicht toosearch op.</span><span class="sxs-lookup"><span data-stu-id="a29ba-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="a29ba-153">tooindex Solr, gebruik RDP tooremote Hallo-cluster met toohello bureaublad navigeren, opent u Hallo Hadoop vanaf de opdrachtregel en navigeer te**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="a29ba-154">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a29ba-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="a29ba-155">Hier ziet u uitvoer volgen op Hallo console Hallo:</span><span class="sxs-lookup"><span data-stu-id="a29ba-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="a29ba-156">Hallo post.jar hulpprogramma Solr met twee voorbeelddocumenten indexeert **solr.xml** en **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="a29ba-157">Hallo post.jar hulpprogramma en Hallo voorbeelddocumenten zijn beschikbaar met Solr installatie.</span><span class="sxs-lookup"><span data-stu-id="a29ba-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="a29ba-158">**Gebruik Hallo Solr dashboard toosearch binnen Hallo geïndexeerde documenten**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="a29ba-159">In Hallo RDP-sessie toohello HDInsight-cluster, opent u Internet Explorer en openen Hallo Solr-dashboard **solr-http://headnodehost:8983 / #/**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="a29ba-160">Vanuit linkerdeelvenster Hallo van Hallo **Core Selector** vervolgkeuzelijst, selecteer **collection1**, en binnen die, op **Query**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="a29ba-161">Als een voorbeeld, tooselect en terug bieden alle Hallo documenten in de Solr, Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="a29ba-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="a29ba-162">In Hallo **q** tekst Voer  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="a29ba-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="a29ba-163">Hiermee wordt alle Hallo-documenten die zijn geïndexeerd in Solr retourneren.</span><span class="sxs-lookup"><span data-stu-id="a29ba-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="a29ba-164">Als u toosearch voor een specifieke tekenreeks binnen Hallo documenten wilt, kunt u hier die tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="a29ba-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="a29ba-165">In Hallo **wt** tekstvak, selecteer Hallo uitvoerindeling.</span><span class="sxs-lookup"><span data-stu-id="a29ba-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="a29ba-166">Standaard is **json**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-166">Default is **json**.</span></span> <span data-ttu-id="a29ba-167">Klik op **-Query uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="a29ba-168">![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "een query uitvoeren op Solr dashboard")</span><span class="sxs-lookup"><span data-stu-id="a29ba-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="a29ba-169">Hallo uitvoer retourneert Hallo twee documenten die we voor indexering Solr gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a29ba-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="a29ba-170">Hallo uitvoer lijkt op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="a29ba-170">hello output resembles hello following:</span></span>

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
4. <span data-ttu-id="a29ba-171">**Aanbevolen: Back-up Hallo geïndexeerde gegevens van Solr tooAzure Blob-opslag die is gekoppeld aan de HDInsight-cluster Hallo**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="a29ba-172">Als een goede gewoonte back u-up Hallo geïndexeerde gegevens vanaf Hallo Solr clusterknooppunten naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="a29ba-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="a29ba-173">Voer Hallo dus toodo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a29ba-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="a29ba-174">Open Internet Explorer en punt toohello volgende URL in Hallo RDP-sessie:</span><span class="sxs-lookup"><span data-stu-id="a29ba-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="a29ba-175">U ziet een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="a29ba-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="a29ba-176">In de externe sessie hello, te navigeren {SOLR_HOME}\{verzameling} \data.</span><span class="sxs-lookup"><span data-stu-id="a29ba-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="a29ba-177">Voor Hallo-cluster is gemaakt via het voorbeeldscript hello, moet dit **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="a29ba-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="a29ba-178">Op deze locatie ziet u een momentopnamemap is gemaakt met een naam vergelijkbaar te**momentopname.* tijdstempel***.</span><span class="sxs-lookup"><span data-stu-id="a29ba-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="a29ba-179">ZIP-snapshotmap hello en upload het tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="a29ba-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="a29ba-180">Navigeer toohello locatie van de snapshotmap Hallo met behulp van de volgende opdracht Hallo vanaf Hallo Hadoop-opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="a29ba-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="a29ba-181">Met deze opdracht kopieën te/voorbeeld/momentopnamegegevens Hallo/onder Hallo-container binnen Hallo standaard Storage-account die is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="a29ba-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="a29ba-182">Solr met Aure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="a29ba-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="a29ba-183">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="a29ba-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="a29ba-184">Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a29ba-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="a29ba-185">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="a29ba-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="a29ba-186">Solr met .NET SDK installeren</span><span class="sxs-lookup"><span data-stu-id="a29ba-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="a29ba-187">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="a29ba-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="a29ba-188">Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="a29ba-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="a29ba-189">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="a29ba-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="a29ba-190">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a29ba-190">See also</span></span>
* [<span data-ttu-id="a29ba-191">Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="a29ba-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="a29ba-192">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="a29ba-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="a29ba-193">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="a29ba-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="a29ba-194">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="a29ba-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="a29ba-195">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark.</span><span class="sxs-lookup"><span data-stu-id="a29ba-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="a29ba-196">[R installeren op HDInsight-clusters][hdinsight-install-r]: scriptactie voorbeeld over het installeren van R.</span><span class="sxs-lookup"><span data-stu-id="a29ba-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="a29ba-197">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install.md): scriptactie voorbeeld over het installeren van Giraph.</span><span class="sxs-lookup"><span data-stu-id="a29ba-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
