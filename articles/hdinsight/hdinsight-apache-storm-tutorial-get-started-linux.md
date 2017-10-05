---
title: Storm-Starter-voorbeelden voor Apache Storm in HDInsight - Azure | Microsoft Docs
description: Lees hoe u big data kunt analyseren en gegevens in realtime kunt verwerken met Apache Storm in HDInsight.
keywords: storm-starter, apache storm voorbeeld
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: 83fc6db1ddb43eb87e7c58684505d7196c1e53d0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="97f42-104">Aan de slag met Apache Storm in HDInsight met behulp van Storm-Starter-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="97f42-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="97f42-105">Leer hoe u Apache Storm gebruikt in HDInsight aan de hand van de Storm-Starter-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="97f42-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="97f42-106">Apache Storm is een gedistribueerd, schaalbaar, fouttolerant en realtime berekeningssysteem voor het verwerken van gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="97f42-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="97f42-107">Met Storm in Azure HDInsight kunt u een op een cloud gebaseerd Storm-cluster maken dat in realtime big data-analyses uitvoert.</span><span class="sxs-lookup"><span data-stu-id="97f42-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97f42-108">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="97f42-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="97f42-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97f42-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="97f42-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97f42-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="97f42-111">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="97f42-111">**An Azure subscription**.</span></span> <span data-ttu-id="97f42-112">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="97f42-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="97f42-113">**Kennis van SSH en SCP**.</span><span class="sxs-lookup"><span data-stu-id="97f42-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="97f42-114">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="97f42-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="97f42-115">Een Storm-cluster maken</span><span class="sxs-lookup"><span data-stu-id="97f42-115">Create a Storm cluster</span></span>

<span data-ttu-id="97f42-116">Gebruik de volgende stappen om een Storm in een HDInsight-cluster te maken:</span><span class="sxs-lookup"><span data-stu-id="97f42-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="97f42-117">In [Azure Portal](https://portal.azure.com) selecteert u **+ NIEUW**, **Intelligence en analyse** en vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="97f42-117">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Een HDInsight-cluster maken](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="97f42-119">Geef op de blade **Basisbeginselen** de volgende gegevens op:</span><span class="sxs-lookup"><span data-stu-id="97f42-119">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="97f42-120">**Clusternaam**: de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="97f42-121">**Abonnement**: selecteer het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97f42-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="97f42-122">**Aanmeldingsgebruikersnaam** en -**wachtwoord** van cluster: de aanmeldingsgegevens voor toegang tot het cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="97f42-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="97f42-123">U gebruikt deze referenties voor toegang tot services als de Ambari-webinterface of de REST-API.</span><span class="sxs-lookup"><span data-stu-id="97f42-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="97f42-124">**SSH-gebruikersnaam (Secure Shell)**: de aanmeldingsgegevens voor toegang tot het cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="97f42-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="97f42-125">Het wachtwoord is standaard hetzelfde als het aanmeldingswachtwoord van het cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="97f42-126">**Resourcegroep**: de resourcegroep waarin het cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97f42-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="97f42-127">**Locatie**: de Azure-regio waarin het cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97f42-127">**Location**: The Azure region to create the cluster in.</span></span>

    ![Abonnement selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="97f42-129">Selecteer **Clustertype** en stel de volgende waarden in op de blade **Clusterconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="97f42-129">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="97f42-130">**Clustertype**: Storm</span><span class="sxs-lookup"><span data-stu-id="97f42-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="97f42-131">**Besturingssysteem**: Linux</span><span class="sxs-lookup"><span data-stu-id="97f42-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="97f42-132">**Versie**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="97f42-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="97f42-133">**Clusterlaag**: standaard</span><span class="sxs-lookup"><span data-stu-id="97f42-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="97f42-134">Gebruik ten slotte de knop **Selecteren** om de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="97f42-134">Finally, use the **Select** button to save settings.</span></span>

    ![Clustertype selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="97f42-136">Nadat u het clustertype hebt geselecteerd, gebruikt u de knop __Selecteren__ om het clustertype te selecteren.</span><span class="sxs-lookup"><span data-stu-id="97f42-136">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="97f42-137">Gebruik vervolgens de knop __Volgende__ om de basisconfiguratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="97f42-137">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="97f42-138">Op de blade **Opslag** selecteert of maakt u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="97f42-138">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="97f42-139">Voor de stappen in dit document laat u de andere velden in deze blade op de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="97f42-139">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="97f42-140">Gebruik de knop __Volgende__ om de opslagconfiguratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="97f42-140">Use the __Next__ button to save storage configuration.</span></span>

    ![De instellingen van het opslagaccount voor HDInsight configureren](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="97f42-142">Controleer op de blade **Samenvatting** de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-142">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="97f42-143">Gebruik de koppeling __Bewerken__ om onjuiste instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="97f42-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="97f42-144">Gebruik tot slot de knop __Maken__ om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="97f42-144">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="97f42-146">Het kan tot 20 minuten duren om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="97f42-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="97f42-147">Een Storm Starter-voorbeeld uitvoeren in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97f42-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="97f42-148">Maak verbinding met het HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="97f42-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="97f42-149">Als u een wachtwoord hebt gebruikt om uw SSH gebruikersaccount te beveiligen, wordt u gevraagd het wachtwoord in te voeren.</span><span class="sxs-lookup"><span data-stu-id="97f42-149">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="97f42-150">Als u een openbare sleutel hebt gebruikt, moet u mogelijk de parameter `-i` gebruiken om de overeenkomende persoonlijke sleutel op te geven.</span><span class="sxs-lookup"><span data-stu-id="97f42-150">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="97f42-151">Bijvoorbeeld `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="97f42-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="97f42-152">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="97f42-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="97f42-153">Gebruik de volgende opdracht om een voorbeeldtopologie te starten:</span><span class="sxs-lookup"><span data-stu-id="97f42-153">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="97f42-154">In eerdere versies van HDInsight is de klassenaam van de topologie `storm.starter.WordCountTopology` in plaats van `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="97f42-154">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="97f42-155">Met deze opdracht wordt de WordCount-voorbeeldtopologie gestart op het cluster, met een beschrijvende naam voor 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="97f42-155">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="97f42-156">Het genereert willekeurig zinnen en telt het aantal keer dat elk woord in deze zinnen voorkomt.</span><span class="sxs-lookup"><span data-stu-id="97f42-156">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97f42-157">Bij het indienen van uw eigen topologieën bij het cluster moet u eerst het JAR-bestand met het cluster kopiëren voordat u de opdracht `storm` gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97f42-157">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="97f42-158">Gebruik de opdracht `scp` om het bestand te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="97f42-158">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="97f42-159">Bijvoorbeeld: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="97f42-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="97f42-160">Het WordCount-voorbeeld en andere Storm Starter-voorbeelden zijn al in uw cluster opgenomen op `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="97f42-160">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="97f42-161">Wilt u de bron van de Storm Starter-voorbeelden bekijken? U vindt de code hier: [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="97f42-161">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="97f42-162">Deze koppeling is voor Storm 1.1.x, geleverd bij HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="97f42-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="97f42-163">Gebruik voor andere versies van Storm de knop __Vertakking__ boven aan de pagina om een andere Storm-versie te selecteren.</span><span class="sxs-lookup"><span data-stu-id="97f42-163">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="97f42-164">De topologie bewaken</span><span class="sxs-lookup"><span data-stu-id="97f42-164">Monitor the topology</span></span>

<span data-ttu-id="97f42-165">De Storm-gebruikersinterface biedt een webinterface voor het werken met actieve topologieën en is opgenomen in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-165">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="97f42-166">Voer de volgende stappen uit voor het bewaken van de topologie met behulp van de Storm-gebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="97f42-166">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="97f42-167">Ga in een webbrowser naar https://CLUSTERNAME.azurehdinsight.net/stormui om de gebruikersinterface van Storm weer te geven.</span><span class="sxs-lookup"><span data-stu-id="97f42-167">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="97f42-168">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-168">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="97f42-169">Als u wordt gevraagd een gebruikersnaam en een wachtwoord op te geven, voert u de gegevens voor de clusterbeheerder (admin) en het wachtwoord in die u hebt gebruikt toen u het cluster maakte.</span><span class="sxs-lookup"><span data-stu-id="97f42-169">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="97f42-170">Selecteer onder **Topology summary** de vermelding **wordcount** in de kolom **Name**.</span><span class="sxs-lookup"><span data-stu-id="97f42-170">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="97f42-171">Er wordt informatie over de topologie weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97f42-171">Information about the topology is displayed.</span></span>

    ![Storm-dashboard met informatie over de Storm-Starter WordCount-topologie.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="97f42-173">Deze pagina bevat de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="97f42-173">This page provides the following information:</span></span>

    * <span data-ttu-id="97f42-174">**Topology stats**: basisinformatie over de topologieprestaties, geordend in tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="97f42-174">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="97f42-175">Wanneer er een specifiek tijdvenster wordt geselecteerd, verandert het tijdvenster voor informatie die wordt weergegeven in andere gedeelten van de pagina.</span><span class="sxs-lookup"><span data-stu-id="97f42-175">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="97f42-176">**Spouts**: basisinformatie over spouts, met inbegrip van de laatste fout die door elke spout is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="97f42-176">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="97f42-177">**Bolts**: basisinformatie over bolts.</span><span class="sxs-lookup"><span data-stu-id="97f42-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="97f42-178">**Topology configuration**: gedetailleerde informatie over de topologieconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="97f42-178">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="97f42-179">Deze pagina bevat ook de acties die op de topologie kunnen worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="97f42-179">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="97f42-180">**Activate**: de verwerking van een gedeactiveerde topologie wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="97f42-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="97f42-181">**Deactivate**: een actieve topologie wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="97f42-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="97f42-182">**Rebalance**: de parallelle uitvoering van de topologie wordt aangepast.</span><span class="sxs-lookup"><span data-stu-id="97f42-182">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="97f42-183">Nadat u het aantal knooppunten in het cluster hebt gewijzigd, moet u actieve topologieën opnieuw verdelen.</span><span class="sxs-lookup"><span data-stu-id="97f42-183">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="97f42-184">Met het opnieuw verdelen wordt de parallelle uitvoering aangepast om te compenseren voor het toegenomen/afgenomen aantal knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-184">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="97f42-185">Zie [Inzicht in de parallelle uitvoering van een Storm-topologie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97f42-185">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="97f42-186">**Kill**: hiermee wordt een Storm-topologie na de opgegeven time-out beëindigd.</span><span class="sxs-lookup"><span data-stu-id="97f42-186">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="97f42-187">Selecteer op deze pagina een item in de sectie **Spouts** of **Bolts**.</span><span class="sxs-lookup"><span data-stu-id="97f42-187">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="97f42-188">Er wordt informatie over het geselecteerde onderdeel weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97f42-188">Information about the selected component is displayed.</span></span>

    ![Storm-dashboard met informatie over de geselecteerde onderdelen.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="97f42-190">Deze pagina geeft de volgende informatie weer:</span><span class="sxs-lookup"><span data-stu-id="97f42-190">This page displays the following information:</span></span>

    * <span data-ttu-id="97f42-191">**Spout/Bolt stats**: basisinformatie over de prestaties van de diverse onderdelen, geordend in tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="97f42-191">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="97f42-192">Wanneer er een specifiek tijdvenster wordt geselecteerd, verandert het tijdvenster voor informatie die wordt weergegeven in andere gedeelten van de pagina.</span><span class="sxs-lookup"><span data-stu-id="97f42-192">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="97f42-193">**Input stats** (alleen bolts): informatie over onderdelen die gegevens produceren die worden verbruikt door de bolt.</span><span class="sxs-lookup"><span data-stu-id="97f42-193">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="97f42-194">**Output stats**: informatie over gegevens die door deze bolt zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="97f42-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="97f42-195">**Executors**: informatie over exemplaren van dit onderdeel.</span><span class="sxs-lookup"><span data-stu-id="97f42-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="97f42-196">**Errors**: fouten die door dit onderdeel zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="97f42-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="97f42-197">Als u details voor een specifiek exemplaar van het onderdeel wilt weergeven, selecteert u een item in de kolom **Port** in de sectie **Executor** terwijl u de details van een spout of bolt bekijkt.</span><span class="sxs-lookup"><span data-stu-id="97f42-197">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="97f42-198">In dit voorbeeld komt het woord **seven** 1.493.957 keer voor.</span><span class="sxs-lookup"><span data-stu-id="97f42-198">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="97f42-199">Dit getal is het aantal keer dat het woord is gevonden sinds deze topologie is gestart.</span><span class="sxs-lookup"><span data-stu-id="97f42-199">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="97f42-200">De topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="97f42-200">Stop the topology</span></span>

<span data-ttu-id="97f42-201">Ga terug naar de pagina **Topology summary** voor de word-count-topologie en klik vervolgens op de knop **Kill** in de sectie **Topology actions**.</span><span class="sxs-lookup"><span data-stu-id="97f42-201">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="97f42-202">Wanneer hierom wordt gevraagd, voert u 10 in voor het aantal seconden dat moet worden gewacht voordat de topologie wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="97f42-202">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="97f42-203">Na de time-outperiode wordt de topologie niet meer weergegeven als u het gedeelte **Storm UI** van het dashboard bezoekt.</span><span class="sxs-lookup"><span data-stu-id="97f42-203">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="97f42-204">Het cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="97f42-204">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="97f42-205">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u een probleem ondervindt met het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="97f42-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="97f42-206"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97f42-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="97f42-207">In deze zelfstudie voor Apache Storm hebt u de basisbeginselen van het werken met Storm op HDInsight geleerd.</span><span class="sxs-lookup"><span data-stu-id="97f42-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="97f42-208">U kunt nu gaan leren hoe u [op Java gebaseerde topologieën met Maven ontwikkelt](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="97f42-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="97f42-209">Als u al bekend bent met het ontwikkelen van op Java gebaseerde topologieën en een bestaande topologie wilt implementeren in HDInsight, raadpleegt u [Apache Storm-topologieën implementeren en beheren in HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="97f42-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="97f42-210">Als u .NET-ontwikkelaar bent, kunt u C#- of hybride C#-/Java-topologieën maken met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97f42-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="97f42-211">Zie [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Hadoop-hulpprogramma's voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97f42-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="97f42-212">Zie voor voorbeeldtopologieën die kunnen worden gebruikt met Storm op HDInsight de volgende voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="97f42-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="97f42-213">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="97f42-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
