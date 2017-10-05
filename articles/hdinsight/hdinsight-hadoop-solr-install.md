---
title: Installeert met een scriptactie Solr op Hadoop-cluster - Azure | Microsoft Docs
description: Informatie over het aanpassen van HDInsight-cluster met Solr met behulp van de scriptactie.
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
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="4d7e7-103">Installeren en gebruiken van Solr op Windows gebaseerde HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="4d7e7-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="4d7e7-104">Informatie over het aanpassen van HDInsight op basis van Windows-cluster met Solr met behulp van de scriptactie en Solr gebruiken om te zoeken van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d7e7-105">De stappen in dit document wordt alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4d7e7-106">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="4d7e7-107">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4d7e7-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="4d7e7-109">Zie voor meer informatie over het gebruik van Solr met een cluster op basis van Linux [installeert en gebruikt Solr op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="4d7e7-110">U kunt Solr installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="4d7e7-111">Een voorbeeld van een script Solr installeren op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="4d7e7-112">Het voorbeeldscript werkt alleen met HDInsight-cluster versie 3.1.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="4d7e7-113">Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="4d7e7-114">Het voorbeeldscript gebruikt in dit onderwerp maakt een Solr op basis van Windows-cluster met een specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="4d7e7-115">Als u wilt configureren van het cluster Solr met verschillende verzamelingen, shards, schema's, replica's, enz., moet u het script en de binaire bestanden Solr dienovereenkomstig wijzigen.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="4d7e7-116">**Verwante artikelen**</span><span class="sxs-lookup"><span data-stu-id="4d7e7-116">**Related articles**</span></span>

* [<span data-ttu-id="4d7e7-117">Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4d7e7-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="4d7e7-118">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="4d7e7-119">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="4d7e7-120">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="4d7e7-121">Wat is Solr?</span><span class="sxs-lookup"><span data-stu-id="4d7e7-121">What is Solr?</span></span>
<span data-ttu-id="4d7e7-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="4d7e7-123">Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr de zoekmogelijkheden snel gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="4d7e7-124">Solr met portal installeren</span><span class="sxs-lookup"><span data-stu-id="4d7e7-124">Install Solr using portal</span></span>
1. <span data-ttu-id="4d7e7-125">Beginnen met het maken van een cluster met behulp van de **aangepast maken** optie, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="4d7e7-126">Op de **scriptacties** pagina van de wizard, klikt u op **scriptactie toevoegen** om details te verstrekken over de scriptactie, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="4d7e7-127">![Scriptactie gebruiken voor het aanpassen van een cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "scriptactie gebruiken voor het aanpassen van een cluster")</span><span class="sxs-lookup"><span data-stu-id="4d7e7-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="4d7e7-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4d7e7-128">Property</span></span></th><th><span data-ttu-id="4d7e7-129">Waarde</span><span class="sxs-lookup"><span data-stu-id="4d7e7-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="4d7e7-130">Naam</span><span class="sxs-lookup"><span data-stu-id="4d7e7-130">Name</span></span></td>
            <td><span data-ttu-id="4d7e7-131">Geef een naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-131">Specify a name for the script action.</span></span> <span data-ttu-id="4d7e7-132">Bijvoorbeeld: <b>installeren Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="4d7e7-133">Script-URI</span><span class="sxs-lookup"><span data-stu-id="4d7e7-133">Script URI</span></span></td>
            <td><span data-ttu-id="4d7e7-134">Geef de URI Uniform Resource Identifier () naar het script dat wordt opgeroepen voor het aanpassen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="4d7e7-135">Bijvoorbeeld: <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="4d7e7-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="4d7e7-136">Soort knooppunt</span><span class="sxs-lookup"><span data-stu-id="4d7e7-136">Node Type</span></span></td>
            <td><span data-ttu-id="4d7e7-137">Geef op de knooppunten waarop het script aanpassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="4d7e7-138">U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b>.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="4d7e7-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="4d7e7-139">Parameters</span></span></td>
            <td><span data-ttu-id="4d7e7-140">Geef de parameters op, indien vereist door het script.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="4d7e7-141">Het script voor het installeren van Solr vereist geen parameters, zodat u kunt dit leeg laten.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="4d7e7-142">U kunt meer dan één scriptactie meerdere om onderdelen te installeren op het cluster toevoegen.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="4d7e7-143">Nadat u de scripts hebt toegevoegd, klikt u op het vinkje om te beginnen met het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="4d7e7-144">Solr gebruiken</span><span class="sxs-lookup"><span data-stu-id="4d7e7-144">Use Solr</span></span>
<span data-ttu-id="4d7e7-145">U moet beginnen met het indexeren Solr met enkele gegevensbestanden.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="4d7e7-146">U kunt vervolgens Solr zoekquery's uitvoeren op de geïndexeerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="4d7e7-147">Voer de volgende stappen voor het gebruik van Solr in een HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="4d7e7-148">**Remote Desktop Protocol (RDP) naar extern gebruik in het HDInsight-cluster met Solr geïnstalleerd**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="4d7e7-149">Vanuit de Azure-portal, moet u extern bureaublad inschakelen voor het cluster dat u hebt gemaakt met Solr geïnstalleerd en vervolgens extern in het cluster.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="4d7e7-150">Zie voor instructies [verbinding maken met HDInsight-clusters met RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="4d7e7-151">**Index Solr door gegevensbestanden uploaden**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="4d7e7-152">Wanneer u de index Solr, plaatst u documenten in die u zoeken wilt op.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="4d7e7-153">Om te indexeren Solr, RDP gebruikt om externe bij het cluster, gaat u naar het bureaublad, open de Hadoop-opdrachtregel en navigeer naar **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="4d7e7-154">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="4d7e7-155">Op de console ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="4d7e7-156">Het hulpprogramma post.jar Solr met twee voorbeelddocumenten indexeert **solr.xml** en **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="4d7e7-157">Het hulpprogramma post.jar en de voorbeelddocumenten zijn beschikbaar met Solr-installatie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="4d7e7-158">**Het dashboard Solr gebruiken om te zoeken binnen de geïndexeerde documenten**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="4d7e7-159">In de RDP-sessie met de HDInsight-cluster, opent u Internet Explorer en start het dashboard Solr op **solr-http://headnodehost:8983 / #/**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="4d7e7-160">In het linkerdeelvenster van de **Core Selector** vervolgkeuzelijst, selecteer **collection1**, en binnen die, op **Query**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="4d7e7-161">Als u bijvoorbeeld om te selecteren en retourneren van alle documenten in Solr, bieden de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="4d7e7-162">In de **q** tekst Voer  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="4d7e7-163">Hiermee wordt de documenten die zijn geïndexeerd in Solr retourneren.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="4d7e7-164">Als u zoeken naar een specifieke tekenreeks binnen de documenten wilt, kunt u deze tekenreeks hier invoeren.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="4d7e7-165">In de **wt** tekst Selecteer indeling van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="4d7e7-166">Standaard is **json**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-166">Default is **json**.</span></span> <span data-ttu-id="4d7e7-167">Klik op **-Query uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="4d7e7-168">![Scriptactie gebruiken voor het aanpassen van een cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "een query uitvoeren op Solr dashboard")</span><span class="sxs-lookup"><span data-stu-id="4d7e7-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="4d7e7-169">De uitvoer retourneert de twee documenten die we voor indexeren Solr gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="4d7e7-170">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
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
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
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
4. <span data-ttu-id="4d7e7-171">**Aanbevolen: Back-up van de geïndexeerde gegevens van Solr naar Azure Blob-opslag die is gekoppeld aan het HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="4d7e7-172">Als een goede gewoonte back u-up de geïndexeerde gegevens van de clusterknooppunten Solr naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="4d7e7-173">Voer de volgende stappen uit om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="4d7e7-174">Open Internet Explorer in de RDP-sessie en wijst u de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="4d7e7-175">U ziet een antwoord als volgt:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="4d7e7-176">Navigeer in de externe sessie naar {SOLR_HOME}\{verzameling} \data.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="4d7e7-177">Voor het cluster is gemaakt via het voorbeeldscript, moet dit **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="4d7e7-178">Op deze locatie ziet u een momentopnamemap is gemaakt met een naam die lijkt op  **momentopname.* tijdstempel***.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="4d7e7-179">De snapshotmap ZIP en dit uploaden naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="4d7e7-180">Navigeer naar de locatie van de momentopnamemap met de volgende opdracht vanaf de opdrachtregel Hadoop:</span><span class="sxs-lookup"><span data-stu-id="4d7e7-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="4d7e7-181">Met deze opdracht wordt de momentopname gekopieerd naar /example/data/onder de container binnen het standaard opslagaccount die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="4d7e7-182">Solr met Aure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="4d7e7-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="4d7e7-183">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="4d7e7-184">Het voorbeeld laat zien hoe Spark met Azure PowerShell installeren.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="4d7e7-185">U moet aanpassen van het script te gebruiken [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="4d7e7-186">Solr met .NET SDK installeren</span><span class="sxs-lookup"><span data-stu-id="4d7e7-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="4d7e7-187">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="4d7e7-188">Het voorbeeld laat zien hoe Spark met de .NET SDK installeren.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="4d7e7-189">U moet aanpassen van het script te gebruiken [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="4d7e7-190">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4d7e7-190">See also</span></span>
* [<span data-ttu-id="4d7e7-191">Installeren en gebruiken van Solr op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4d7e7-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="4d7e7-192">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="4d7e7-193">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="4d7e7-194">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="4d7e7-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="4d7e7-195">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="4d7e7-196">[R installeren op HDInsight-clusters][hdinsight-install-r]: scriptactie voorbeeld over het installeren van R.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="4d7e7-197">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install.md): scriptactie voorbeeld over het installeren van Giraph.</span><span class="sxs-lookup"><span data-stu-id="4d7e7-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
