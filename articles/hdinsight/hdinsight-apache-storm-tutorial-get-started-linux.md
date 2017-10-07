---
title: aaaStorm starter-voorbeelden op Apache Storm op HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toodo big data-analyses en gegevens in realtime verwerken met behulp van Apache Storm en Hallo storm starter-voorbeelden in HDInsight.
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
ms.openlocfilehash: bb6d6549e67ca5b557f0692f98c89692a87267b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
#<a name="get-started-with-apache-storm-on-hdinsight-using-hello-storm-starter-examples"></a><span data-ttu-id="f20ef-104">Aan de slag met Apache Storm op HDInsight met behulp van Hallo storm starter-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="f20ef-104">Get started with Apache Storm on HDInsight using hello storm-starter examples</span></span>

<span data-ttu-id="f20ef-105">Meer informatie over hoe toouse Apache Storm in HDInsight met behulp Hallo storm starter-voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f20ef-105">Learn how toouse Apache Storm in HDInsight using hello storm-starter examples.</span></span>

<span data-ttu-id="f20ef-106">Apache Storm is een gedistribueerd, schaalbaar, fouttolerant en realtime berekeningssysteem voor het verwerken van gegevensstromen.</span><span class="sxs-lookup"><span data-stu-id="f20ef-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="f20ef-107">Met Storm in Azure HDInsight kunt u een op een cloud gebaseerd Storm-cluster maken dat in realtime big data-analyses uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f20ef-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f20ef-108">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f20ef-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f20ef-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f20ef-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f20ef-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="f20ef-111">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f20ef-111">**An Azure subscription**.</span></span> <span data-ttu-id="f20ef-112">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f20ef-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f20ef-113">**Kennis van SSH en SCP**.</span><span class="sxs-lookup"><span data-stu-id="f20ef-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="f20ef-114">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="f20ef-115">Een Storm-cluster maken</span><span class="sxs-lookup"><span data-stu-id="f20ef-115">Create a Storm cluster</span></span>

<span data-ttu-id="f20ef-116">Gebruik Hallo stappen toocreate een Storm op HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="f20ef-116">Use hello following steps toocreate a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="f20ef-117">Van Hallo [Azure-portal](https://portal.azure.com), selecteer **+ nieuw**, **Intelligence en analyse**, en selecteer vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="f20ef-117">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Een HDInsight-cluster maken](./media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="f20ef-119">Van Hallo **basisbeginselen** blade Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f20ef-119">From hello **Basics** blade, enter hello following information:</span></span>

    * <span data-ttu-id="f20ef-120">**Clusternaam**: Hallo-naam van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-120">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="f20ef-121">**Abonnement**: Hallo abonnement toouse selecteren.</span><span class="sxs-lookup"><span data-stu-id="f20ef-121">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="f20ef-122">**Gebruikersnaam voor aanmelding cluster** en **Cluster aanmeldingswachtwoord**: Hallo aanmelding bij het openen van Hallo-cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f20ef-122">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="f20ef-123">U gebruikt deze referenties tooaccess services zoals Hallo Ambari-Webgebruikersinterface of REST-API.</span><span class="sxs-lookup"><span data-stu-id="f20ef-123">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="f20ef-124">**Secure Shell (SSH) gebruikersnaam**: Hallo-aanmeldingsnaam die wordt gebruikt bij het openen van Hallo-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="f20ef-124">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="f20ef-125">Standaard is Hallo wachtwoord Hallo hetzelfde als Hallo aanmelding het wachtwoord van het cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-125">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="f20ef-126">**Resourcegroep**: Hallo resource groep toocreate Hallo cluster in.</span><span class="sxs-lookup"><span data-stu-id="f20ef-126">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="f20ef-127">**Locatie**: hello Azure-regio toocreate Hallo cluster in.</span><span class="sxs-lookup"><span data-stu-id="f20ef-127">**Location**: hello Azure region toocreate hello cluster in.</span></span>

    ![Abonnement selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="f20ef-129">Selecteer **type Cluster**, en vervolgens Hallo set waarden op Hallo **clusterconfiguratie** blade:</span><span class="sxs-lookup"><span data-stu-id="f20ef-129">Select **Cluster type**, and then set hello following values on hello **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="f20ef-130">**Clustertype**: Storm</span><span class="sxs-lookup"><span data-stu-id="f20ef-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="f20ef-131">**Besturingssysteem**: Linux</span><span class="sxs-lookup"><span data-stu-id="f20ef-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="f20ef-132">**Versie**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="f20ef-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="f20ef-133">**Clusterlaag**: standaard</span><span class="sxs-lookup"><span data-stu-id="f20ef-133">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="f20ef-134">Gebruik tot slot Hallo **Selecteer** knop toosave instellingen.</span><span class="sxs-lookup"><span data-stu-id="f20ef-134">Finally, use hello **Select** button toosave settings.</span></span>

    ![Clustertype selecteren](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="f20ef-136">Gebruik na het selecteren van clustertype Hallo Hallo __Selecteer__ knoptype tooset Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-136">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="f20ef-137">Gebruik vervolgens Hallo __volgende__ knop toofinish basisconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-137">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="f20ef-138">Van Hallo **opslag** blade selecteren of een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="f20ef-138">From hello **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="f20ef-139">Voor Hallo stappen in dit document, laat u Hallo andere velden op deze blade Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="f20ef-139">For hello steps in this document, leave hello other fields on this blade at hello default values.</span></span> <span data-ttu-id="f20ef-140">Gebruik Hallo __volgende__ knop toosave opslagconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-140">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Hallo-opslag-accountinstellingen voor HDInsight instellen](./media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="f20ef-142">Van Hallo **samenvatting** blade Hallo-configuratie controleren voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-142">From hello **Summary** blade, review hello configuration for hello cluster.</span></span> <span data-ttu-id="f20ef-143">Gebruik Hallo __bewerken__ koppelingen toochange alle instellingen die onjuist zijn.</span><span class="sxs-lookup"><span data-stu-id="f20ef-143">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="f20ef-144">Gebruik tot slot the__Create__ knop toocreate Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-144">Finally, use the__Create__ button toocreate hello cluster.</span></span>

    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="f20ef-146">Too20 minuten toocreate Hallo cluster kan duren.</span><span class="sxs-lookup"><span data-stu-id="f20ef-146">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="f20ef-147">Een Storm Starter-voorbeeld uitvoeren in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f20ef-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="f20ef-148">Verbinding maken met toohello HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="f20ef-148">Connect toohello HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="f20ef-149">Als u een wachtwoord toosecure uw SSH gebruikersaccount gebruikt, bent u na vragen aan gebruiker tooenter deze.</span><span class="sxs-lookup"><span data-stu-id="f20ef-149">If you used a password toosecure your SSH user account, you are prompted tooenter it.</span></span> <span data-ttu-id="f20ef-150">Als u een openbare sleutel gebruikt, kunt u moet gebruiken Hallo `-i` parameter toospecify Hallo overeenkomende persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="f20ef-150">If you used a public key, you may need use hello `-i` parameter toospecify hello matching private key.</span></span> <span data-ttu-id="f20ef-151">Bijvoorbeeld `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="f20ef-151">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="f20ef-152">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-152">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f20ef-153">Gebruik Hallo opdracht toostart een voorbeeldtopologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="f20ef-153">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="f20ef-154">In eerdere versies van HDInsight Hallo klassenaam van Hallo-topologie is `storm.starter.WordCountTopology` in plaats van `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="f20ef-154">On previous versions of HDInsight, hello class name of hello topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="f20ef-155">Deze opdracht start Hallo WordCount-voorbeeldtopologie Hallo-cluster met een beschrijvende naam voor 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="f20ef-155">This command starts hello example WordCount topology on hello cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="f20ef-156">Deze genereert willekeurig zinnen en aantal Hallo exemplaar van elk woord in Hallo zinnen.</span><span class="sxs-lookup"><span data-stu-id="f20ef-156">It randomly generates sentences and count hello occurrence of each word in hello sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f20ef-157">Bij het indienen van uw eigen topologieën toohello-cluster, moet u eerst Hallo jar-bestand met de Hallo cluster voordat u Hallo kopiëren `storm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="f20ef-157">When submitting your own topologies toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="f20ef-158">Gebruik Hallo `scp` opdrachtbestand toocopy Hallo.</span><span class="sxs-lookup"><span data-stu-id="f20ef-158">Use hello `scp` command toocopy hello file.</span></span> <span data-ttu-id="f20ef-159">Bijvoorbeeld: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="f20ef-159">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="f20ef-160">Hallo WordCount-voorbeeld en andere storm starter-voorbeelden zijn al opgenomen in uw cluster op `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="f20ef-160">hello WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="f20ef-161">Als u geïnteresseerd bent in Hallo bron voor de storm starter-voorbeelden Hallo weergeven, kunt u vinden Hallo code aan [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="f20ef-161">If you are interested in viewing hello source for hello storm-starter examples, you can find hello code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="f20ef-162">Deze koppeling is voor Storm 1.1.x, geleverd bij HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="f20ef-162">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="f20ef-163">Gebruik voor andere versies van Storm Hallo __vertakking__ knop Hallo Hallo pagina tooselect bovenaan in een andere versie van Storm.</span><span class="sxs-lookup"><span data-stu-id="f20ef-163">For other versions of Storm, use hello __Branch__ button at hello top of hello page tooselect a different Storm version.</span></span>

## <a name="monitor-hello-topology"></a><span data-ttu-id="f20ef-164">Monitor Hallo-topologie</span><span class="sxs-lookup"><span data-stu-id="f20ef-164">Monitor hello topology</span></span>

<span data-ttu-id="f20ef-165">Hallo Storm-gebruikersinterface biedt een webinterface voor het werken met actieve topologieën en is opgenomen op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-165">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="f20ef-166">Hallo stappen toomonitor Hallo topologie Hallo Storm-gebruikersinterface met volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f20ef-166">Use hello following steps toomonitor hello topology using hello Storm UI:</span></span>

1. <span data-ttu-id="f20ef-167">toodisplay hello Storm-gebruikersinterface, opent u een web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="f20ef-167">toodisplay hello Storm UI, open a web browser toohttps://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="f20ef-168">Vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-168">Replace **CLUSTERNAME** with hello name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="f20ef-169">Als u wordt gevraagd tooprovide een gebruikersnaam en wachtwoord, Voer Hallo Clusterbeheerder (admin) en het wachtwoord dat u hebt gebruikt toen maken Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-169">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

2. <span data-ttu-id="f20ef-170">Onder **Topology summary**, selecteer Hallo **wordcount** vermelding in Hallo **naam** kolom.</span><span class="sxs-lookup"><span data-stu-id="f20ef-170">Under **Topology summary**, select hello **wordcount** entry in hello **Name** column.</span></span> <span data-ttu-id="f20ef-171">Informatie over het Hallo-topologie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f20ef-171">Information about hello topology is displayed.</span></span>

    ![Storm-dashboard met informatie over de Storm-Starter WordCount-topologie.](./media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="f20ef-173">Deze pagina bevat Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f20ef-173">This page provides hello following information:</span></span>

    * <span data-ttu-id="f20ef-174">**Topology stats** -basisinformatie over Hallo topologieprestaties, geordend in tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="f20ef-174">**Topology stats** - Basic information on hello topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f20ef-175">Als u een specifiek tijdstip venster wijzigingen Hallo tijdvenster voor informatie die wordt weergegeven in andere gedeelten van Hallo pagina selecteert.</span><span class="sxs-lookup"><span data-stu-id="f20ef-175">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="f20ef-176">**Spouts** -basisinformatie over spouts, met inbegrip van Hallo laatste fout die door elke spout is geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="f20ef-176">**Spouts** - Basic information about spouts, including hello last error returned by each spout.</span></span>

    * <span data-ttu-id="f20ef-177">**Bolts**: basisinformatie over bolts.</span><span class="sxs-lookup"><span data-stu-id="f20ef-177">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="f20ef-178">**Topologieconfiguratie** -gedetailleerde informatie over de configuratie van de Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-178">**Topology configuration** - Detailed information about hello topology configuration.</span></span>

    <span data-ttu-id="f20ef-179">Deze pagina bevat ook de acties die kunnen worden uitgevoerd op Hallo-topologie:</span><span class="sxs-lookup"><span data-stu-id="f20ef-179">This page also provides actions that can be taken on hello topology:</span></span>

    * <span data-ttu-id="f20ef-180">**Activate**: de verwerking van een gedeactiveerde topologie wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="f20ef-180">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="f20ef-181">**Deactivate**: een actieve topologie wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="f20ef-181">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="f20ef-182">**Opnieuw verdelen** -Hallo parallelle uitvoering van Hallo-topologie wordt aangepast.</span><span class="sxs-lookup"><span data-stu-id="f20ef-182">**Rebalance** - Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="f20ef-183">Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen.</span><span class="sxs-lookup"><span data-stu-id="f20ef-183">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="f20ef-184">Parallelle uitvoering toocompensate voor Hallo toegenomen/afgenomen aantal knooppunten in cluster Hallo herverdeling worden aangepast.</span><span class="sxs-lookup"><span data-stu-id="f20ef-184">Rebalancing adjusts parallelism toocompensate for hello increased/decreased number of nodes in hello cluster.</span></span> <span data-ttu-id="f20ef-185">Zie voor meer informatie [begrijpen Hallo parallelle uitvoering van een Storm-topologie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="f20ef-185">For more information, see [Understanding hello parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="f20ef-186">**Kill** -beëindigt een Storm-topologie nadat Hallo time-out opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f20ef-186">**Kill** - Terminates a Storm topology after hello specified timeout.</span></span>

3. <span data-ttu-id="f20ef-187">Op deze pagina, selecteert u een vermelding uit Hallo **Spouts** of **Bolts** sectie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-187">From this page, select an entry from hello **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="f20ef-188">Informatie over het geselecteerde onderdeel hello wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f20ef-188">Information about hello selected component is displayed.</span></span>

    ![Storm-dashboard met informatie over de geselecteerde onderdelen.](./media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="f20ef-190">Deze pagina wordt weergegeven Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="f20ef-190">This page displays hello following information:</span></span>

    * <span data-ttu-id="f20ef-191">**Spout/Bolt stats** -basisinformatie over de prestaties van de component hello, geordend in tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="f20ef-191">**Spout/Bolt stats** - Basic information on hello component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f20ef-192">Als u een specifiek tijdstip venster wijzigingen Hallo tijdvenster voor informatie die wordt weergegeven in andere gedeelten van Hallo pagina selecteert.</span><span class="sxs-lookup"><span data-stu-id="f20ef-192">Selecting a specific time window changes hello time window for information displayed in other sections of hello page.</span></span>

    * <span data-ttu-id="f20ef-193">**Input stats** (alleen Bolts): informatie over onderdelen die gegevens die worden gebruikt door de bolt Hallo produceren.</span><span class="sxs-lookup"><span data-stu-id="f20ef-193">**Input stats** (bolt only) - Information on components that produce data consumed by hello bolt.</span></span>

    * <span data-ttu-id="f20ef-194">**Output stats**: informatie over gegevens die door deze bolt zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f20ef-194">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="f20ef-195">**Executors**: informatie over exemplaren van dit onderdeel.</span><span class="sxs-lookup"><span data-stu-id="f20ef-195">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="f20ef-196">**Errors**: fouten die door dit onderdeel zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="f20ef-196">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="f20ef-197">Wanneer u bekijkt hello details van een spout of bolt, selecteert u een vermelding uit Hallo **poort** kolom in Hallo **Executor** sectie tooview details voor een specifiek exemplaar van het Hallo-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="f20ef-197">When viewing hello details of a spout or bolt, select an entry from hello **Port** column in hello **Executors** section tooview details for a specific instance of hello component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="f20ef-198">In dit voorbeeld Hallo word **zeven** 1493957 keer voorkwam.</span><span class="sxs-lookup"><span data-stu-id="f20ef-198">In this example, hello word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="f20ef-199">Dit aantal is het aantal keren Hallo woord is gevonden sinds deze topologie is gestart.</span><span class="sxs-lookup"><span data-stu-id="f20ef-199">This count is how many times hello word has been encountered since this topology was started.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="f20ef-200">Hallo-topologie stoppen</span><span class="sxs-lookup"><span data-stu-id="f20ef-200">Stop hello topology</span></span>

<span data-ttu-id="f20ef-201">Toohello retourneren **Topology summary** pagina voor Hallo word-count-topologie en selecteer vervolgens Hallo **Kill** knop van Hallo **Topology actions** sectie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-201">Return toohello **Topology summary** page for hello word-count topology, and then select hello **Kill** button from hello **Topology actions** section.</span></span> <span data-ttu-id="f20ef-202">Wanneer u wordt gevraagd, voert u 10 voor Hallo seconden toowait voordat Hallo-topologie wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="f20ef-202">When prompted, enter 10 for hello seconds toowait before stopping hello topology.</span></span> <span data-ttu-id="f20ef-203">Na het Hallo-time-outperiode Hallo topologie niet meer wordt weergegeven wanneer u Hallo **Storm-gebruikersinterface** sectie van het Hallo-dashboard.</span><span class="sxs-lookup"><span data-stu-id="f20ef-203">After hello timeout period, hello topology no longer appears when you visit hello **Storm UI** section of hello dashboard.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="f20ef-204">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="f20ef-204">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="f20ef-205">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u een probleem ondervindt met het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f20ef-205">If you run into an issue with creating HDInsight cluster, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <span data-ttu-id="f20ef-206"><a id="next"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f20ef-206"><a id="next"></a>Next steps</span></span>

<span data-ttu-id="f20ef-207">In deze zelfstudie voor Apache Storm, hebt u geleerd Hallo basisbeginselen van het werken met Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f20ef-207">In this Apache Storm tutorial, you learned hello basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="f20ef-208">Vervolgens leert u hoe te[ontwikkelen van Java gebaseerde topologieën met Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f20ef-208">Next, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="f20ef-209">Als u al bekend bent met het ontwikkelen van Java gebaseerde topologieën en een bestaande topologie tooHDInsight toodeploy, Zie [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f20ef-209">If you're already familiar with developing Java-based topologies and want toodeploy an existing topology tooHDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="f20ef-210">Als u .NET-ontwikkelaar bent, kunt u C#- of hybride C#-/Java-topologieën maken met Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f20ef-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="f20ef-211">Zie [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Hadoop-hulpprogramma's voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f20ef-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="f20ef-212">Zie voor voorbeeldtopologieën die kunnen worden gebruikt met Storm op HDInsight Hallo volgen voorbeelden:</span><span class="sxs-lookup"><span data-stu-id="f20ef-212">For example topologies that can be used with Storm on HDInsight, see hello following examples:</span></span>

* [<span data-ttu-id="f20ef-213">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="f20ef-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
