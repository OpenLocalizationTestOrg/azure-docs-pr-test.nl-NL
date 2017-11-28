---
title: Gebruik scriptactie Solr installeren op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Informatie over het installeren van Solr op Linux gebaseerde HDInsight Hadoop-clusters met behulp van scriptacties.
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
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="60529-103">Installeren en gebruiken van Solr op HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="60529-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="60529-104">Informatie over het installeren van Solr in Azure HDInsight met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="60529-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="60529-105">Solr is een krachtige search-platform en biedt zoekmogelijkheden op bedrijfsniveau op gegevens die worden beheerd door Hadoop.</span><span class="sxs-lookup"><span data-stu-id="60529-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="60529-106">De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="60529-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="60529-107">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="60529-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="60529-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="60529-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60529-109">Het voorbeeldscript in dit document gebruikt installeert Solr 4.9 met een specifieke configuratie.</span><span class="sxs-lookup"><span data-stu-id="60529-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="60529-110">Als u wilt configureren van het cluster Solr met verschillende verzamelingen, shards, schema's, replica's, enz., moet u het script en Solr binaire bestanden wijzigen.</span><span class="sxs-lookup"><span data-stu-id="60529-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="60529-111"><a name="whatis"></a>Wat is Solr</span><span class="sxs-lookup"><span data-stu-id="60529-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="60529-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is een platform voor het zoeken van enterprise waarmee krachtige zoekopdracht in volledige tekst van gegevens.</span><span class="sxs-lookup"><span data-stu-id="60529-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="60529-113">Hadoop kunt opslaan en beheren van de enorme hoeveelheden gegevens, biedt Apache Solr de zoekmogelijkheden snel gegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="60529-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="60529-114">Onderdelen van het HDInsight-cluster worden volledig ondersteund door Microsoft.</span><span class="sxs-lookup"><span data-stu-id="60529-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="60529-115">Aangepaste onderdelen, zoals Solr, ontvangt binnen commercieel redelijke ondersteuning u helpen het probleem verder op te lossen.</span><span class="sxs-lookup"><span data-stu-id="60529-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="60529-116">Ondersteuning van Microsoft zijn mogelijk niet kunnen oplossen van problemen met aangepaste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="60529-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="60529-117">U moet mogelijk de community's van de open-source benaderen voor hulp.</span><span class="sxs-lookup"><span data-stu-id="60529-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="60529-118">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="60529-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="60529-119">Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="60529-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="60529-120">Wat het script doet</span><span class="sxs-lookup"><span data-stu-id="60529-120">What the script does</span></span>

<span data-ttu-id="60529-121">Dit script maakt de volgende wijzigingen aan het HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="60529-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="60529-122">Solr 4.9 in geïnstalleerd`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="60529-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="60529-123">Hiermee maakt u een gebruiker **solrusr**, dat wordt gebruikt voor het uitvoeren van de service Solr</span><span class="sxs-lookup"><span data-stu-id="60529-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="60529-124">Sets **solruser** als eigenaar van`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="60529-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="60529-125">Voegt een [Upstart](http://upstart.ubuntu.com/) configuratie die Solr automatisch wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="60529-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="60529-126"><a name="install"></a>Installeren met behulp van scriptacties Solr</span><span class="sxs-lookup"><span data-stu-id="60529-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="60529-127">Een voorbeeld van een script Solr installeren op een HDInsight-cluster is beschikbaar op de volgende locatie:</span><span class="sxs-lookup"><span data-stu-id="60529-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="60529-128">Voor het maken van een cluster met Solr geïnstalleerd gebruikt u de stappen in de [HDInsight-clusters maken](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="60529-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="60529-129">Gebruik de volgende stappen voor het installeren van Solr tijdens het maken:</span><span class="sxs-lookup"><span data-stu-id="60529-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="60529-130">Van de __Cluster samenvatting__ blade, select__Advanced settings__, klikt u vervolgens __acties Script__.</span><span class="sxs-lookup"><span data-stu-id="60529-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="60529-131">Gebruik de volgende informatie voor het vullen van het formulier:</span><span class="sxs-lookup"><span data-stu-id="60529-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="60529-132">**NAAM**: een beschrijvende naam voor de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="60529-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="60529-133">**SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="60529-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="60529-134">**HEAD**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="60529-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="60529-135">**WERKNEMER**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="60529-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="60529-136">**ZOOKEEPER**: Schakel deze optie om te installeren op het knooppunt Zookeeper</span><span class="sxs-lookup"><span data-stu-id="60529-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="60529-137">**PARAMETERS**: dit veld leeg laten</span><span class="sxs-lookup"><span data-stu-id="60529-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="60529-138">Aan de onderkant van de **acties Script** blade, gebruik de **Selecteer** om op te slaan van de configuratie.</span><span class="sxs-lookup"><span data-stu-id="60529-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="60529-139">Gebruik tot slot de **volgende** terug te keren naar de __Cluster samenvatting__</span><span class="sxs-lookup"><span data-stu-id="60529-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="60529-140">Van de __Cluster samenvatting__ pagina __maken__ om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="60529-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="60529-141"><a name="usesolr"></a>Hoe gebruik Solr in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60529-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60529-142">De stappen in deze sectie laten zien basisfunctionaliteit Solr.</span><span class="sxs-lookup"><span data-stu-id="60529-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="60529-143">Zie voor meer informatie over het gebruik van Solr de [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="60529-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="60529-144">Indexgegevens</span><span class="sxs-lookup"><span data-stu-id="60529-144">Index data</span></span>

<span data-ttu-id="60529-145">Gebruik de volgende stappen bijvoorbeeld gegevens toevoegen aan Solr en deze vervolgens een query:</span><span class="sxs-lookup"><span data-stu-id="60529-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="60529-146">Maak verbinding met het HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="60529-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="60529-147">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="60529-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="60529-148">Stappen verderop in dit document wordt een SSL-tunnel verbinding maken met de webgebruikersinterface Solr gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60529-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="60529-149">Voor het gebruik van deze stappen, moet u een SSL-tunnel maakt en configureer vervolgens uw browser om het te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60529-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="60529-150">Zie voor meer informatie de [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="60529-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="60529-151">Gebruik de volgende opdrachten om Solr index voorbeeldgegevens:</span><span class="sxs-lookup"><span data-stu-id="60529-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="60529-152">De volgende uitvoer wordt geretourneerd naar de console:</span><span class="sxs-lookup"><span data-stu-id="60529-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="60529-153">De `post.jar` hulpprogramma voegt de **solr.xml** en **monitor.xml** documenten naar de index.</span><span class="sxs-lookup"><span data-stu-id="60529-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="60529-154">Gebruik de volgende opdracht om op te vragen van de Solr REST-API:</span><span class="sxs-lookup"><span data-stu-id="60529-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="60529-155">Met deze opdracht wordt gezocht **collection1** voor documenten die overeenkomen met  **\*:\***  (gecodeerd als \*% 3A\* in de query-tekenreeks).</span><span class="sxs-lookup"><span data-stu-id="60529-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="60529-156">Het volgende JSON-document is een voorbeeld van het antwoord:</span><span class="sxs-lookup"><span data-stu-id="60529-156">The following JSON document is an example of the response:</span></span>

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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="60529-157">Met behulp van het dashboard Solr</span><span class="sxs-lookup"><span data-stu-id="60529-157">Using the Solr dashboard</span></span>

<span data-ttu-id="60529-158">Het dashboard Solr is een webgebruikersinterface waarmee u werkt met Solr via uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="60529-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="60529-159">Het dashboard Solr rechtstreeks op het Internet van uw HDInsight-cluster niet wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="60529-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="60529-160">U kunt een SSH-tunnel gebruiken om deze te openen.</span><span class="sxs-lookup"><span data-stu-id="60529-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="60529-161">Zie voor meer informatie over het gebruik van een SSH-tunnel de [SSH-Tunneling gebruiken met HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="60529-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="60529-162">Wanneer u een SSH-tunnel hebt gemaakt, gebruik de volgende stappen uit om het dashboard Solr:</span><span class="sxs-lookup"><span data-stu-id="60529-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="60529-163">De hostnaam voor de primaire headnode bepalen:</span><span class="sxs-lookup"><span data-stu-id="60529-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="60529-164">SSH gebruiken voor verbinding met het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="60529-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="60529-165">Bijvoorbeeld `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="60529-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="60529-166">Zie voor meer informatie over het gebruik van SSH, het [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="60529-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="60529-167">Gebruik de volgende opdracht om de volledig gekwalificeerde hostnaam:</span><span class="sxs-lookup"><span data-stu-id="60529-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="60529-168">Met deze opdracht retourneert een waarde die vergelijkbaar is met de naam van de volgende:</span><span class="sxs-lookup"><span data-stu-id="60529-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="60529-169">De waarde die is geretourneerd, niet opslaan omdat het wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60529-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="60529-170">Verbinding maken met in uw browser **solr-http://HOSTNAME:8983 / #/**, waarbij **hostnaam** is de naam die u in de vorige stappen hebt bepaald.</span><span class="sxs-lookup"><span data-stu-id="60529-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="60529-171">De aanvraag wordt doorgestuurd via de SSH-tunnel naar de Solr webgebruikersinterface op uw cluster.</span><span class="sxs-lookup"><span data-stu-id="60529-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="60529-172">De pagina lijkt op de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="60529-172">The page appears similar to the following image:</span></span>

    ![Afbeelding van Solr dashboard](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="60529-174">Vanuit het linkerdeelvenster met de **Core Selector** vervolgkeuzelijst selecteren **collection1**.</span><span class="sxs-lookup"><span data-stu-id="60529-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="60529-175">Meerdere vermeldingen moeten ze worden weergegeven onder **collection1**.</span><span class="sxs-lookup"><span data-stu-id="60529-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="60529-176">De onderstaande vermeldingen **collection1**, selecteer **Query**.</span><span class="sxs-lookup"><span data-stu-id="60529-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="60529-177">Gebruik de volgende waarden voor het vullen van de zoekpagina:</span><span class="sxs-lookup"><span data-stu-id="60529-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="60529-178">In de **q** tekst Voer  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="60529-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="60529-179">Deze query retourneert de documenten die zijn geïndexeerd in Solr.</span><span class="sxs-lookup"><span data-stu-id="60529-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="60529-180">Als u zoeken naar een specifieke tekenreeks binnen de documenten wilt, kunt u deze tekenreeks hier invoeren.</span><span class="sxs-lookup"><span data-stu-id="60529-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="60529-181">In de **wt** tekst Selecteer indeling van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="60529-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="60529-182">Standaard is **json**.</span><span class="sxs-lookup"><span data-stu-id="60529-182">Default is **json**.</span></span>

     <span data-ttu-id="60529-183">Tot slot selecteert u de **zoekopdracht uitvoeren** knop onder aan de pate zoeken.</span><span class="sxs-lookup"><span data-stu-id="60529-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Scriptactie gebruiken voor het aanpassen van een cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="60529-185">De uitvoer retourneert twee documenten die u eerder naar de index hebt toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="60529-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="60529-186">De uitvoer is vergelijkbaar met het volgende JSON-document:</span><span class="sxs-lookup"><span data-stu-id="60529-186">The output is similar to the following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="60529-187">Starten en stoppen Solr</span><span class="sxs-lookup"><span data-stu-id="60529-187">Starting and stopping Solr</span></span>

<span data-ttu-id="60529-188">Gebruik de volgende opdrachten om handmatig te stoppen en starten Solr:</span><span class="sxs-lookup"><span data-stu-id="60529-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="60529-189">Back-upgegevens van de geïndexeerde</span><span class="sxs-lookup"><span data-stu-id="60529-189">Backup indexed data</span></span>

<span data-ttu-id="60529-190">Gebruik de volgende stappen uit voor de back-ups Solr naar de standaard-opslag voor uw cluster:</span><span class="sxs-lookup"><span data-stu-id="60529-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="60529-191">Verbinding maken met het cluster via SSH en voer vervolgens de volgende opdracht gebruiken om op te halen van de hostnaam voor het hoofdknooppunt:</span><span class="sxs-lookup"><span data-stu-id="60529-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="60529-192">Gebruik de volgende opdracht om een momentopname van de geïndexeerde gegevens te maken.</span><span class="sxs-lookup"><span data-stu-id="60529-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="60529-193">Vervang **hostnaam** met de naam die is geretourneerd door de vorige opdracht:</span><span class="sxs-lookup"><span data-stu-id="60529-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="60529-194">Het antwoord is vergelijkbaar met de volgende XML-code:</span><span class="sxs-lookup"><span data-stu-id="60529-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="60529-195">Wijzig de mappen te `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="60529-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="60529-196">Er is een submap voor elke verzameling.</span><span class="sxs-lookup"><span data-stu-id="60529-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="60529-197">De map voor elke verzameling bevat een `data` map waarin de momentopname voor de verzameling.</span><span class="sxs-lookup"><span data-stu-id="60529-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="60529-198">Gebruik de volgende opdracht voor het maken van een gecomprimeerd archief van de momentopnamemap:</span><span class="sxs-lookup"><span data-stu-id="60529-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="60529-199">Vervang de `snapshot.20150806185338855` waarden met de naam van de momentopname voor uw verzameling.</span><span class="sxs-lookup"><span data-stu-id="60529-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="60529-200">Deze opdracht maakt u een archief met de naam **snapshot.20150806185338855.tgz**, waarin de inhoud van de **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="60529-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="60529-201">Vervolgens kunt u opslaan van het archief met van het cluster primaire opslag met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="60529-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="60529-202">Zie voor meer informatie over het werken met Solr back-up en herstelbewerkingen [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="60529-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60529-203">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="60529-203">Next steps</span></span>

* <span data-ttu-id="60529-204">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="60529-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="60529-205">Aanpassing van de cluster Giraph installeren op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60529-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="60529-206">Giraph Hiermee kunt u grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60529-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="60529-207">[Hue installeren op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="60529-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="60529-208">Aanpassing van de cluster Hue installeren op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60529-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="60529-209">HUE is een set van webtoepassingen die worden gebruikt om te communiceren met een Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="60529-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
