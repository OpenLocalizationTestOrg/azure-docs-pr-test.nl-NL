---
title: "aaaDeploy en beheren van Apache Storm-topologieën op Linux gebaseerde HDInsight | Microsoft Docs"
description: "Ontdek hoe toodeploy, bewaken en beheren van Apache Storm-topologieën Hallo Storm-Dashboard met op Linux gebaseerde HDInsight. Hadoop-hulpprogramma's voor Visual Studio gebruiken."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a><span data-ttu-id="690f3-104">Implementeren en beheren van Apache Storm-topologieën op HDInsight</span><span class="sxs-lookup"><span data-stu-id="690f3-104">Deploy and manage Apache Storm topologies on HDInsight</span></span>

<span data-ttu-id="690f3-105">Informatie over Hallo basisprincipes van beheer en controle van Storm-topologieën uitgevoerd op Storm op HDInsight-clusters in dit document.</span><span class="sxs-lookup"><span data-stu-id="690f3-105">In this document, learn hello basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="690f3-106">Hallo moet stappen in dit artikel een op Linux gebaseerde Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-106">hello steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="690f3-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="690f3-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="690f3-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="690f3-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="690f3-109">Zie voor informatie over het implementeren en bewaken van topologieën op HDInsight op basis van Windows, [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Windows](hdinsight-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="690f3-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](hdinsight-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="690f3-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="690f3-110">Prerequisites</span></span>

* <span data-ttu-id="690f3-111">**Een op Linux gebaseerde Storm op HDInsight-cluster**: Zie [aan de slag met Apache Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) voor stapsgewijze instructies voor het maken van een cluster</span><span class="sxs-lookup"><span data-stu-id="690f3-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="690f3-112">(Optioneel) **Kennis van SSH en SCP**: Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="690f3-113">(Optioneel) **Visual Studio**: Azure SDK 2.5.1 of hoger en hello Data Lake Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="690f3-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and hello Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="690f3-114">Zie voor meer informatie [aan de slag met Data Lake Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-114">For more information, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="690f3-115">Een van de volgende versies van Visual Studio Hallo:</span><span class="sxs-lookup"><span data-stu-id="690f3-115">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="690f3-116">Visual Studio 2012 met [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="690f3-116">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="690f3-117">Visual Studio 2013 met [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="690f3-117">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="690f3-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="690f3-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="690f3-119">Visual Studio 2015 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="690f3-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="690f3-120">Visual Studio 2017 (alle versies).</span><span class="sxs-lookup"><span data-stu-id="690f3-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="690f3-121">Data Lake Tools voor Visual Studio 2017 worden geïnstalleerd als onderdeel van hello Azure werkbelasting.</span><span class="sxs-lookup"><span data-stu-id="690f3-121">Data Lake Tools for Visual Studio 2017 are installed as part of hello Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="690f3-122">Verzenden van een topologie: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="690f3-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="690f3-123">Hallo HDInsight-hulpprogramma's kunnen worden gebruikt toosubmit C# of hybride topologieën tooyour Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-123">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="690f3-124">Hallo stappen te volgen, gebruiken een voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="690f3-124">hello following steps use a sample application.</span></span> <span data-ttu-id="690f3-125">Zie voor meer informatie over het maken van uw eigen topologieën met behulp van Hallo HDInsight Tools [C#-topologieën ontwikkelen met Hallo HDInsight Tools voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-125">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="690f3-126">Als u hebt niet is gebeurd Hallo meest recente versie van Hallo Data Lake tools voor Visual Studio, Zie [aan de slag met Data Lake Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-126">If you have not already installed hello latest version of hello Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="690f3-127">Hallo Data Lake Tools voor Visual Studio werden voorheen Hallo HDInsight Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="690f3-127">hello Data Lake Tools for Visual Studio were formerly called hello HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="690f3-128">Data Lake Tools voor Visual Studio zijn opgenomen in Hallo __Azure werkbelasting__ voor Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="690f3-128">Data Lake Tools for Visual Studio are included in hello __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="690f3-129">Open Visual Studio, selecteer **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="690f3-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="690f3-130">In Hallo **nieuw Project** dialoogvenster Vouw **geïnstalleerde** > **sjablonen**, en selecteer vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="690f3-130">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="690f3-131">Selecteer in de lijst met sjablonen Hallo **Storm voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="690f3-131">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="690f3-132">Typ een naam voor de toepassing hello Hallo onderaan in het dialoogvenster voor Hallo in.</span><span class="sxs-lookup"><span data-stu-id="690f3-132">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Afbeelding](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="690f3-134">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="690f3-134">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="690f3-135">Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="690f3-135">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="690f3-136">Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-136">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="690f3-137">Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="690f3-137">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="690f3-138">U kunt controleren of Hallo verzending is voltooid met Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="690f3-138">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a><span data-ttu-id="690f3-139">Verzenden van een topologie: SSH en hello Storm-opdracht</span><span class="sxs-lookup"><span data-stu-id="690f3-139">Submit a topology: SSH and hello Storm command</span></span>

1. <span data-ttu-id="690f3-140">SSH tooconnect toohello HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="690f3-140">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="690f3-141">Vervang **gebruikersnaam** Hallo-naam van uw SSH-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="690f3-141">Replace **USERNAME** hello name of your SSH login.</span></span> <span data-ttu-id="690f3-142">Vervang **CLUSTERNAME** met de naam van uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="690f3-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="690f3-143">Voor meer informatie over het gebruik van SSH tooconnect tooyour HDInsight-cluster, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-143">For more information on using SSH tooconnect tooyour HDInsight cluster, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="690f3-144">Gebruik Hallo opdracht toostart een voorbeeldtopologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="690f3-144">Use hello following command toostart an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="690f3-145">Deze opdracht start Hallo WordCount-voorbeeldtopologie op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-145">This command starts hello example WordCount topology on hello cluster.</span></span> <span data-ttu-id="690f3-146">Deze topologie genereren willekeurig zinnen en aantal Hallo exemplaar van elk woord in Hallo zinnen.</span><span class="sxs-lookup"><span data-stu-id="690f3-146">This topology randomly generate sentences and count hello occurrence of each word in hello sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="690f3-147">Bij het indienen van topologie toohello cluster, moet u eerst Hallo jar-bestand met de Hallo cluster voordat u Hallo kopiëren `storm` opdracht.</span><span class="sxs-lookup"><span data-stu-id="690f3-147">When submitting topology toohello cluster, you must first copy hello jar file containing hello cluster before using hello `storm` command.</span></span> <span data-ttu-id="690f3-148">toocopy hello toohello bestandscluster, kunt u Hallo `scp` opdracht.</span><span class="sxs-lookup"><span data-stu-id="690f3-148">toocopy hello file toohello cluster, you can use hello `scp` command.</span></span> <span data-ttu-id="690f3-149">Bijvoorbeeld: `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="690f3-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="690f3-150">Hallo WordCount-voorbeeld en andere storm starter-voorbeelden zijn al opgenomen in uw cluster op `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="690f3-150">hello WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="690f3-151">Verzenden van een topologie: programmatisch</span><span class="sxs-lookup"><span data-stu-id="690f3-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="690f3-152">U kunt een topologie tooStorm op HDInsight programmatisch implementeren met communiceren met de Hallo Nimbus service die wordt gehost in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-152">You can programmatically deploy a topology tooStorm on HDInsight by communicating with hello Nimbus service hosted in your cluster.</span></span> <span data-ttu-id="690f3-153">[https://github.com/Azure-Samples/hdinsight-Java-Deploy-storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) bevat een voorbeeld van Java-toepassing die u laat zien hoe toodeploy en een topologie via Hallo Nimbus-service te starten.</span><span class="sxs-lookup"><span data-stu-id="690f3-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how toodeploy and start a topology through hello Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="690f3-154">Bewaken en beheren: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="690f3-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="690f3-155">Wanneer een topologie is verzonden met behulp van Visual Studio, Hallo **Storm-topologieën** weergeven voor Hallo cluster weer te geven.</span><span class="sxs-lookup"><span data-stu-id="690f3-155">When a topology has been successfully submitted using Visual Studio, hello **Storm Topologies** view for hello cluster appears.</span></span> <span data-ttu-id="690f3-156">Selecteer Hallo-topologie in Hallo lijst tooview informatie over Hallo topologie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-156">Select hello topology from hello list tooview information about hello running topology.</span></span>

![monitor voor Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="690f3-158">U kunt ook weergeven **Storm-topologieën** van **Server Explorer** door het uitbreiden van **Azure** > **HDInsight**, en klik vervolgens met de rechtermuisknop op een Storm op HDInsight-cluster en het selecteren van **weergave Storm-topologieën**.</span><span class="sxs-lookup"><span data-stu-id="690f3-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="690f3-159">Selecteer Hallo shape voor Hallo spouts of bolts tooview informatie over deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="690f3-159">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="690f3-160">Er wordt een nieuw venster geopend voor elk item geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="690f3-161">Deactiveren en opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="690f3-161">Deactivate and reactivate</span></span>

<span data-ttu-id="690f3-162">Een topologie deactiveren onderbreekt het totdat dit is afgesloten of opnieuw geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="690f3-163">tooperform deze bewerkingen gebruik Hallo __deactiveren__ en __opnieuw activeren__ knoppen bovenaan Hallo Hallo __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="690f3-163">tooperform these operations, use hello __Deactivate__ and __Reactivate__ buttons at hello top of hello __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="690f3-164">Opnieuw verdelen</span><span class="sxs-lookup"><span data-stu-id="690f3-164">Rebalance</span></span>

<span data-ttu-id="690f3-165">Herverdeling van een topologie kunt Hallo system toorevise Hallo parallelle uitvoering van Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-165">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="690f3-166">Als u hebt het formaat gewijzigd Hallo cluster tooadd meer notities, kan herverdeling bijvoorbeeld een topologie toosee Hallo nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="690f3-166">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

<span data-ttu-id="690f3-167">een topologie toorebalance gebruiken Hallo __opnieuw verdelen__ knop bovenaan Hallo Hallo __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="690f3-167">toorebalance a topology, use hello __Rebalance__ button at hello top of hello __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="690f3-168">Eerst een topologie herverdeling Hallo-topologie, deactiveert opnieuw werknemers gelijkmatig verdeeld over Hallo cluster vervolgens, tot slot wordt Hallo topologie toohello staat voordat herverdeling is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="690f3-168">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="690f3-169">Dus als Hallo topologie actief was, wordt het actieve opnieuw.</span><span class="sxs-lookup"><span data-stu-id="690f3-169">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="690f3-170">Als deze is uitgeschakeld, blijft deze gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="690f3-171">Een topologie voor afsluiten</span><span class="sxs-lookup"><span data-stu-id="690f3-171">Kill a topology</span></span>

<span data-ttu-id="690f3-172">Storm-topologieën blijft in uitvoering totdat ze zijn gestopt of Hallo cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="690f3-172">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span> <span data-ttu-id="690f3-173">een topologie toostop gebruiken Hallo __Kill__ knop bovenaan Hallo Hallo __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="690f3-173">toostop a topology, use hello __Kill__ button at hello top of hello __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a><span data-ttu-id="690f3-174">Bewaken en beheren: SSH en hello Storm-opdracht</span><span class="sxs-lookup"><span data-stu-id="690f3-174">Monitor and manage: SSH and hello Storm command</span></span>

<span data-ttu-id="690f3-175">Hallo `storm` hulpprogramma kunt u toowork met actieve topologieën vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="690f3-175">hello `storm` utility allows you toowork with running topologies from hello command line.</span></span> <span data-ttu-id="690f3-176">Gebruik `storm -h` voor een volledige lijst met opdrachten.</span><span class="sxs-lookup"><span data-stu-id="690f3-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="690f3-177">Lijst met topologieën</span><span class="sxs-lookup"><span data-stu-id="690f3-177">List topologies</span></span>

<span data-ttu-id="690f3-178">Hallo opdracht toolist na alle actieve topologieën gebruiken:</span><span class="sxs-lookup"><span data-stu-id="690f3-178">Use hello following command toolist all running topologies:</span></span>

    storm list

<span data-ttu-id="690f3-179">Met deze opdracht retourneert informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="690f3-179">This command returns information similar toohello following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="690f3-180">Deactiveren en opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="690f3-180">Deactivate and reactivate</span></span>

<span data-ttu-id="690f3-181">Een topologie deactiveren onderbreekt het totdat dit is afgesloten of opnieuw geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="690f3-182">Gebruik Hallo opdracht toodeactivate te volgen en opnieuw activeren:</span><span class="sxs-lookup"><span data-stu-id="690f3-182">Use hello following command toodeactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="690f3-183">Voor het afsluiten van een actieve topologie</span><span class="sxs-lookup"><span data-stu-id="690f3-183">Kill a running topology</span></span>

<span data-ttu-id="690f3-184">Storm-topologieën, na het starten, gaat u verder uitgevoerd totdat deze wordt gestopt.</span><span class="sxs-lookup"><span data-stu-id="690f3-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="690f3-185">toostop een topologie Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="690f3-185">toostop a topology, use hello following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="690f3-186">Opnieuw verdelen</span><span class="sxs-lookup"><span data-stu-id="690f3-186">Rebalance</span></span>

<span data-ttu-id="690f3-187">Herverdeling van een topologie kunt Hallo system toorevise Hallo parallelle uitvoering van Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-187">Rebalancing a topology allows hello system toorevise hello parallelism of hello topology.</span></span> <span data-ttu-id="690f3-188">Als u hebt het formaat gewijzigd Hallo cluster tooadd meer notities, kan herverdeling bijvoorbeeld een topologie toosee Hallo nieuwe knooppunten.</span><span class="sxs-lookup"><span data-stu-id="690f3-188">For example, if you have resized hello cluster tooadd more notes, rebalancing allows a topology toosee hello new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="690f3-189">Eerst een topologie herverdeling Hallo-topologie, deactiveert opnieuw werknemers gelijkmatig verdeeld over Hallo cluster vervolgens, tot slot wordt Hallo topologie toohello staat voordat herverdeling is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="690f3-189">Rebalancing a topology first deactivates hello topology, then redistributes workers evenly across hello cluster, then finally returns hello topology toohello state it was in before rebalancing occurred.</span></span> <span data-ttu-id="690f3-190">Dus als Hallo topologie actief was, wordt het actieve opnieuw.</span><span class="sxs-lookup"><span data-stu-id="690f3-190">So if hello topology was active, it becomes active again.</span></span> <span data-ttu-id="690f3-191">Als deze is uitgeschakeld, blijft deze gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="690f3-192">Bewaken en beheren: Storm-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="690f3-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="690f3-193">Hallo Storm-gebruikersinterface biedt een webinterface voor het werken met actieve topologieën en is opgenomen op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-193">hello Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="690f3-194">tooview hello Storm-gebruikersinterface, gebruikt u een web browser tooopen **https://CLUSTERNAME.azurehdinsight.NET/stormui**, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-194">tooview hello Storm UI, use a web browser tooopen **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="690f3-195">Als u wordt gevraagd tooprovide een gebruikersnaam en wachtwoord, Voer Hallo Clusterbeheerder (admin) en het wachtwoord dat u hebt gebruikt toen maken Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-195">If asked tooprovide a user name and password, enter hello cluster administrator (admin) and password that you used when creating hello cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="690f3-196">Hoofdpagina</span><span class="sxs-lookup"><span data-stu-id="690f3-196">Main page</span></span>

<span data-ttu-id="690f3-197">Hallo hoofdpagina Hallo Storm-gebruikersinterface biedt Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="690f3-197">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="690f3-198">**Cluster samenvatting**: algemene informatie over Hallo Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-198">**Cluster summary**: Basic information about hello Storm cluster.</span></span>
* <span data-ttu-id="690f3-199">**Topologie samenvatting**: een lijst met actieve topologieën.</span><span class="sxs-lookup"><span data-stu-id="690f3-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="690f3-200">Hallo-koppelingen in deze sectie tooview meer informatie over specifieke topologieën gebruiken.</span><span class="sxs-lookup"><span data-stu-id="690f3-200">Use hello links in this section tooview more information about specific topologies.</span></span>
* <span data-ttu-id="690f3-201">**Supervisor samenvatting**: informatie over Hallo Storm supervisor.</span><span class="sxs-lookup"><span data-stu-id="690f3-201">**Supervisor summary**: Information about hello Storm supervisor.</span></span>
* <span data-ttu-id="690f3-202">**Nimbus configuratie**: Nimbus-configuratie voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-202">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="690f3-203">Topologie samenvatting</span><span class="sxs-lookup"><span data-stu-id="690f3-203">Topology summary</span></span>

<span data-ttu-id="690f3-204">Wanneer u een koppeling van Hallo **Topology summary** sectie vindt u informatie over het Hallo-topologie na Hallo:</span><span class="sxs-lookup"><span data-stu-id="690f3-204">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="690f3-205">**Topologie samenvatting**: algemene informatie over het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-205">**Topology summary**: Basic information about hello topology.</span></span>
* <span data-ttu-id="690f3-206">**Topologie acties**: acties die u voor Hallo-topologie uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="690f3-206">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="690f3-207">**Activeren**: verwerking van een gedeactiveerde topologie wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="690f3-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="690f3-208">**Deactiveren**: een actieve topologie wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="690f3-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="690f3-209">**Opnieuw verdelen**: Hallo parallelle uitvoering van Hallo-topologie wordt aangepast.</span><span class="sxs-lookup"><span data-stu-id="690f3-209">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="690f3-210">Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen.</span><span class="sxs-lookup"><span data-stu-id="690f3-210">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="690f3-211">Deze bewerking kunt Hallo topologie tooadjust parallelle uitvoering toocompensate voor Hallo verhoogd of verlaagd aantal knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-211">This operation allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

    <span data-ttu-id="690f3-212">Zie voor meer informatie <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">begrijpen Hallo parallelle uitvoering van een Storm-topologie</a>.</span><span class="sxs-lookup"><span data-stu-id="690f3-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding hello parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="690f3-213">**Kill**: een Storm-topologie wordt beëindigd nadat Hallo time-out opgegeven.</span><span class="sxs-lookup"><span data-stu-id="690f3-213">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>
* <span data-ttu-id="690f3-214">**Topology stats**: statistieken over Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-214">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="690f3-215">tooset Hallo periode Hallo resterend posten op Hallo pagina, gebruik Hallo koppelingen in Hallo **venster** kolom.</span><span class="sxs-lookup"><span data-stu-id="690f3-215">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="690f3-216">**Spouts**: Hallo spouts die wordt gebruikt door het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-216">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="690f3-217">Hallo-koppelingen in deze sectie tooview meer informatie over specifieke spouts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="690f3-217">Use hello links in this section tooview more information about specific spouts.</span></span>
* <span data-ttu-id="690f3-218">**Bolts**: Hallo bolts gebruikt door het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="690f3-218">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="690f3-219">Gebruik Hallo koppelingen in deze sectie tooview meer informatie over specifieke bolts.</span><span class="sxs-lookup"><span data-stu-id="690f3-219">Use hello links in this section tooview more information about specific bolts.</span></span>
* <span data-ttu-id="690f3-220">**Topologieconfiguratie**: Hallo configuratie van de topologie Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="690f3-220">**Topology configuration**: hello configuration of hello selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="690f3-221">Spout en Bolt samenvatting</span><span class="sxs-lookup"><span data-stu-id="690f3-221">Spout and Bolt summary</span></span>

<span data-ttu-id="690f3-222">Selecteren van een spout in Hallo **Spouts** of **Bolts** secties Hallo volgende informatie over Hallo geselecteerd item wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="690f3-222">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="690f3-223">**Overzicht van onderdelen**: algemene informatie over Hallo spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="690f3-223">**Component summary**: Basic information about hello spout or bolt.</span></span>
* <span data-ttu-id="690f3-224">**Spout/Bolt stats**: statistieken over Hallo spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="690f3-224">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="690f3-225">tooset Hallo periode Hallo resterend posten op Hallo pagina, gebruik Hallo koppelingen in Hallo **venster** kolom.</span><span class="sxs-lookup"><span data-stu-id="690f3-225">tooset hello timeframe for hello remaining entries on hello page, use hello links in hello **Window** column.</span></span>
* <span data-ttu-id="690f3-226">**Input stats** (alleen Bolts): informatie over Hallo invoerstromen verbruikt door Hallo bolt.</span><span class="sxs-lookup"><span data-stu-id="690f3-226">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>
* <span data-ttu-id="690f3-227">**Output stats**: informatie over Hallo stromen die door dit spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="690f3-227">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>
* <span data-ttu-id="690f3-228">**Executor**: informatie over het Hallo-exemplaren van Hallo spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="690f3-228">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="690f3-229">Selecteer Hallo **poort** vermelding voor een specifieke executor tooview een logboek van diagnostische gegevens geproduceerd voor dit exemplaar.</span><span class="sxs-lookup"><span data-stu-id="690f3-229">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="690f3-230">**Fouten**: alle informatie over de fout voor deze spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="690f3-230">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="690f3-231">Bewaken en beheren: REST-API</span><span class="sxs-lookup"><span data-stu-id="690f3-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="690f3-232">Hallo Storm-gebruikersinterface is gebaseerd op Hallo REST API, zodat u kunt vergelijkbare management en de controlefunctionaliteit met behulp van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="690f3-232">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="690f3-233">U kunt Hallo REST-API toocreate aangepaste hulpprogramma's gebruiken voor het beheren en controleren van Storm-topologieën.</span><span class="sxs-lookup"><span data-stu-id="690f3-233">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="690f3-234">Zie voor meer informatie [Storm UI REST-API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="690f3-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="690f3-235">Hallo is volgende informatie specifiek toousing Hallo REST-API met Apache Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="690f3-235">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="690f3-236">Hallo Storm REST-API is niet openbaar beschikbaar Hallo internet, en moet worden geopend met behulp van een SSH-tunnel toohello HDInsight-cluster hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="690f3-236">hello Storm REST API is not publicly available over hello internet, and must be accessed using an SSH tunnel toohello HDInsight cluster head node.</span></span> <span data-ttu-id="690f3-237">Zie voor meer informatie over het maken en gebruiken van een SSH-tunnel [SSH-Tunneling gebruiken tooaccess Ambari web-UI, ResourceManager JobHistory, NameNode, Oozie en andere web-UI](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling tooaccess Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="690f3-238">Basis-URI</span><span class="sxs-lookup"><span data-stu-id="690f3-238">Base URI</span></span>

<span data-ttu-id="690f3-239">Hallo basis-URI voor Hallo REST-API op Linux gebaseerde HDInsight-clusters is beschikbaar op Hallo hoofdknooppunt op **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="690f3-239">hello base URI for hello REST API on Linux-based HDInsight clusters is available on hello head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="690f3-240">Hallo-domeinnaam van het hoofdknooppunt Hallo wordt gegenereerd tijdens het maken van het cluster en is niet statisch.</span><span class="sxs-lookup"><span data-stu-id="690f3-240">hello domain name of hello head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="690f3-241">Hallo volledig gekwalificeerde domeinnaam (FQDN) voor het hoofdknooppunt van de cluster Hallo vindt u op verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="690f3-241">You can find hello fully qualified domain name (FQDN) for hello cluster head node in several different ways:</span></span>

* <span data-ttu-id="690f3-242">**Tijdens een SSH-sessie**: Gebruik de opdracht Hallo `headnode -f` van een SSH-sessie toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-242">**From an SSH session**: Use hello command `headnode -f` from an SSH session toohello cluster.</span></span>
* <span data-ttu-id="690f3-243">**Vanaf Ambari Web**: Selecteer **Services** van Hallo bovenaan pagina hello, selecteer **Storm**.</span><span class="sxs-lookup"><span data-stu-id="690f3-243">**From Ambari Web**: Select **Services** from hello top of hello page, then select **Storm**.</span></span> <span data-ttu-id="690f3-244">Van Hallo **samenvatting** tabblad **Storm UI Server**.</span><span class="sxs-lookup"><span data-stu-id="690f3-244">From hello **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="690f3-245">Hallo FQDN-naam van het Hallo-knooppunt dat Hallo Storm-gebruikersinterface en REST-API wordt uitgevoerd is bovenaan Hallo Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="690f3-245">hello FQDN of hello node that hello Storm UI and REST API is running is at hello top of hello page.</span></span>
* <span data-ttu-id="690f3-246">**Van de Ambari REST-API**: Gebruik de opdracht Hallo `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informatie over het Hallo-knooppunt dat Hallo Storm-gebruikersinterface en REST-API worden uitgevoerd op.</span><span class="sxs-lookup"><span data-stu-id="690f3-246">**From Ambari REST API**: Use hello command `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve information about hello node that hello Storm UI and REST API are running on.</span></span> <span data-ttu-id="690f3-247">Vervang **wachtwoord** met Hallo beheerderswachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-247">Replace **PASSWORD** with hello admin password for hello cluster.</span></span> <span data-ttu-id="690f3-248">Vervang **CLUSTERNAME** met de naam van de cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="690f3-248">Replace **CLUSTERNAME** with hello cluster name.</span></span> <span data-ttu-id="690f3-249">Hallo-antwoord wordt bevat Hallo 'hostnaam' vermelding Hallo FQDN-naam van het Hallo-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="690f3-249">In hello response, hello "host_name" entry contains hello FQDN of hello node.</span></span>

### <a name="authentication"></a><span data-ttu-id="690f3-250">Authentication</span><span class="sxs-lookup"><span data-stu-id="690f3-250">Authentication</span></span>

<span data-ttu-id="690f3-251">Aanvragen toohello REST-API moet gebruiken **basisverificatie**, zodat u Hallo HDInsight-cluster beheerdersnaam en het wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="690f3-251">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="690f3-252">Omdat basisverificatie wordt verzonden met behulp van de versleutelde tekst, moet u **altijd** toosecure-HTTPS-communicatie met de Hallo-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="690f3-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="690f3-253">Waarden geretourneerd</span><span class="sxs-lookup"><span data-stu-id="690f3-253">Return values</span></span>

<span data-ttu-id="690f3-254">Informatie die wordt geretourneerd vanaf Hallo REST-API is mogelijk alleen bruikbaar uit binnen Hallo cluster of virtuele machines op Hallo hetzelfde virtuele Azure-netwerk als Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="690f3-254">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="690f3-255">Hallo volledig gekwalificeerde domeinnaam (FQDN) geretourneerd voor Zookeeper servers is bijvoorbeeld niet worden toegankelijk is vanaf Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="690f3-255">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers is not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="690f3-256">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="690f3-256">Next Steps</span></span>

<span data-ttu-id="690f3-257">Nu u hebt geleerd hoe toodeploy en monitor topologieën met behulp van Storm-Dashboard hello, kunt u nagaan hoe te[ontwikkelen van Java gebaseerde topologieën met Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-257">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how too[Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="690f3-258">Zie voor een lijst van meer voorbeeldtopologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="690f3-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
