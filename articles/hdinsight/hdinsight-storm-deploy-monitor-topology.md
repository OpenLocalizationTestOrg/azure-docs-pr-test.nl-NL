---
title: "aaaDeploy en beheren van Apache Storm-topologieën op HDInsight | Microsoft Docs"
description: "Ontdek hoe toodeploy, bewaken en beheren van Apache Storm-topologieën op HDInsight met behulp van Hallo Storm-Dashboard. Hadoop-hulpprogramma's voor Visual Studio gebruiken."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="aecde-104">Implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="aecde-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="aecde-105">Hallo Storm-Dashboard kunt u tooeasily implementeren en uitvoeren van Apache Storm-topologieën tooyour HDInsight-cluster met behulp van uw webbrowser.</span><span class="sxs-lookup"><span data-stu-id="aecde-105">hello Storm Dashboard allows you tooeasily deploy and run Apache Storm topologies tooyour HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="aecde-106">U kunt ook Hallo dashboard toomonitor gebruiken en beheren van actieve topologieën.</span><span class="sxs-lookup"><span data-stu-id="aecde-106">You can also use hello dashboard toomonitor and manage running topologies.</span></span> <span data-ttu-id="aecde-107">Als u Visual Studio gebruikt, geef Hallo HDInsight Tools voor Visual Studio soortgelijke functies in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aecde-107">If you use Visual Studio, hello HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="aecde-108">Hallo Storm-Dashboard en Hallo Storm-onderdelen in HDInsight Tools Hallo afhankelijk Hallo Storm REST API, die gebruikt toocreate worden kunnen uw eigen oplossingen bewaking en beheer.</span><span class="sxs-lookup"><span data-stu-id="aecde-108">hello Storm Dashboard and hello Storm features in hello HDInsight Tools rely on hello Storm REST API, which can be used toocreate your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aecde-109">Hallo stappen in dit document moet een Storm op HDInsight-cluster dat gebruik maakt van Windows hello-besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="aecde-109">hello steps in this document require a Storm on HDInsight cluster that uses Windows as hello operating system.</span></span> <span data-ttu-id="aecde-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="aecde-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aecde-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="aecde-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="aecde-112">Zie voor meer informatie over het implementeren en beheren van Storm-topologieën met een HDInsight-cluster dat gebruik maakt van Linux [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="aecde-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aecde-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aecde-113">Prerequisites</span></span>

* <span data-ttu-id="aecde-114">**Apache Storm op HDInsight** -Zie [aan de slag met Apache Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started.md) voor stapsgewijze instructies voor het maken van een cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="aecde-115">Voor Hallo **Storm-Dashboard**: een moderne webbrowser met ondersteuning voor HTML5.</span><span class="sxs-lookup"><span data-stu-id="aecde-115">For hello **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="aecde-116">Voor **Visual Studio** -SDK van Azure 2.5.1 of hoger en hello HDInsight Tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="aecde-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and hello HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="aecde-117">Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall en Hallo HDInsight tools voor Visual Studio configureren.</span><span class="sxs-lookup"><span data-stu-id="aecde-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall and configure hello HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="aecde-118">Een van de volgende versies van Visual Studio Hallo:</span><span class="sxs-lookup"><span data-stu-id="aecde-118">One of hello following versions of Visual Studio:</span></span>

  * <span data-ttu-id="aecde-119">Visual Studio 2012 met Update 4</span><span class="sxs-lookup"><span data-stu-id="aecde-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="aecde-120">Visual Studio 2013 met Update 4 of Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="aecde-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="aecde-121">Visual Studio 2015 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="aecde-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="aecde-122">Visual Studio 2017 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="aecde-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="aecde-123">Storm-Dashboard</span><span class="sxs-lookup"><span data-stu-id="aecde-123">Storm Dashboard</span></span>

<span data-ttu-id="aecde-124">Hallo Storm-Dashboard is een webpagina die beschikbaar is op uw Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-124">hello Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="aecde-125">Hallo-URL is **https://&lt;clustername >.azurehdinsight.net/**, waarbij **clustername** Hallo-naam van uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-125">hello URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="aecde-126">Vanaf de bovenkant van de Hallo Hallo Storm-Dashboard, selecteert u **indienen topologie**.</span><span class="sxs-lookup"><span data-stu-id="aecde-126">From hello top of hello Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="aecde-127">Hallo-instructies op Hallo pagina toorun een voorbeeld topologie of tooupload volgen en voer een topologie die u hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aecde-127">Follow hello instructions on hello page toorun a sample topology or tooupload and run a topology that you created.</span></span>

![Hallo topologie pagina verzenden][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="aecde-129">Storm-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="aecde-129">Storm UI</span></span>

<span data-ttu-id="aecde-130">Hallo Storm-Dashboard, selecteer Hallo **Storm-gebruikersinterface** koppeling.</span><span class="sxs-lookup"><span data-stu-id="aecde-130">From hello Storm Dashboard, select hello **Storm UI** link.</span></span> <span data-ttu-id="aecde-131">Dit geeft informatie weer over Hallo-cluster in toevoeging tooany actieve topologieën.</span><span class="sxs-lookup"><span data-stu-id="aecde-131">This displays information about hello cluster, in addition tooany running topologies.</span></span>

![Hallo storm-gebruikersinterface][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="aecde-133">In sommige versies van Internet Explorer ontdekt u dat Hallo die storm-gebruikersinterface worden niet vernieuwd nadat u het eerst hebt bezocht.</span><span class="sxs-lookup"><span data-stu-id="aecde-133">With some versions of Internet Explorer, you may discover that hello Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="aecde-134">Bijvoorbeeld, kan niet worden weergegeven Hallo nieuwe topologieën die u hebt ingediend, of een topologie als actief kan worden weergegeven wanneer eerder gedeactiveerd.</span><span class="sxs-lookup"><span data-stu-id="aecde-134">For example, it may not show hello new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="aecde-135">Microsoft is op de hoogte van dit probleem en werkt aan een oplossing.</span><span class="sxs-lookup"><span data-stu-id="aecde-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="aecde-136">Hoofdpagina</span><span class="sxs-lookup"><span data-stu-id="aecde-136">Main page</span></span>

<span data-ttu-id="aecde-137">Hallo hoofdpagina Hallo Storm-gebruikersinterface biedt Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="aecde-137">hello main page of hello Storm UI provides hello following information:</span></span>

* <span data-ttu-id="aecde-138">**Cluster samenvatting**: algemene informatie over Hallo Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-138">**Cluster summary**: Basic information about hello Storm cluster.</span></span>

* <span data-ttu-id="aecde-139">**Topologie samenvatting**: een lijst met actieve topologieën.</span><span class="sxs-lookup"><span data-stu-id="aecde-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="aecde-140">Hallo-koppelingen in deze sectie tooview meer informatie over specifieke topologieën gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aecde-140">Use hello links in this section tooview more information about specific topologies.</span></span>

* <span data-ttu-id="aecde-141">**Supervisor samenvatting**: informatie over Hallo Storm supervisor.</span><span class="sxs-lookup"><span data-stu-id="aecde-141">**Supervisor summary**: Information about hello Storm supervisor.</span></span>

* <span data-ttu-id="aecde-142">**Nimbus configuratie**: Nimbus-configuratie voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-142">**Nimbus configuration**: Nimbus configuration for hello cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="aecde-143">Topologie samenvatting</span><span class="sxs-lookup"><span data-stu-id="aecde-143">Topology summary</span></span>

<span data-ttu-id="aecde-144">Wanneer u een koppeling van Hallo **Topology summary** sectie vindt u informatie over het Hallo-topologie na Hallo:</span><span class="sxs-lookup"><span data-stu-id="aecde-144">Selecting a link from hello **Topology summary** section displays hello following information about hello topology:</span></span>

* <span data-ttu-id="aecde-145">**Topologie samenvatting**: algemene informatie over het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-145">**Topology summary**: Basic information about hello topology.</span></span>

* <span data-ttu-id="aecde-146">**Topologie acties**: acties die u voor Hallo-topologie uitvoeren kunt.</span><span class="sxs-lookup"><span data-stu-id="aecde-146">**Topology actions**: Management actions that you can perform for hello topology.</span></span>

  * <span data-ttu-id="aecde-147">**Activeren**: verwerking van een gedeactiveerde topologie wordt hervat.</span><span class="sxs-lookup"><span data-stu-id="aecde-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="aecde-148">**Deactiveren**: een actieve topologie wordt onderbroken.</span><span class="sxs-lookup"><span data-stu-id="aecde-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="aecde-149">**Opnieuw verdelen**: Hallo parallelle uitvoering van Hallo-topologie wordt aangepast.</span><span class="sxs-lookup"><span data-stu-id="aecde-149">**Rebalance**: Adjusts hello parallelism of hello topology.</span></span> <span data-ttu-id="aecde-150">Nadat u het aantal knooppunten in cluster Hallo Hallo hebt gewijzigd, moet u actieve topologieën opnieuw verdelen.</span><span class="sxs-lookup"><span data-stu-id="aecde-150">You should rebalance running topologies after you have changed hello number of nodes in hello cluster.</span></span> <span data-ttu-id="aecde-151">Hierdoor kan het Hallo-topologie tooadjust parallelle uitvoering toocompensate voor Hallo verhoogd of verlaagd van het aantal knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="aecde-151">This allows hello topology tooadjust parallelism toocompensate for hello increased or decreased number of nodes in hello cluster.</span></span>

      <span data-ttu-id="aecde-152">Zie voor meer informatie [begrijpen Hallo parallelle uitvoering van een Storm-topologie (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="aecde-152">For more information, see [Understanding hello parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="aecde-153">**Kill**: een Storm-topologie wordt beëindigd nadat Hallo time-out opgegeven.</span><span class="sxs-lookup"><span data-stu-id="aecde-153">**Kill**: Terminates a Storm topology after hello specified timeout.</span></span>

* <span data-ttu-id="aecde-154">**Topology stats**: statistieken over Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-154">**Topology stats**: Statistics about hello topology.</span></span> <span data-ttu-id="aecde-155">Gebruik Hallo koppelingen in Hallo **venster** kolom tooset Hallo periode Hallo resterend posten op Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="aecde-155">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="aecde-156">**Spouts**: Hallo spouts die wordt gebruikt door het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-156">**Spouts**: hello spouts used by hello topology.</span></span> <span data-ttu-id="aecde-157">Hallo-koppelingen in deze sectie tooview meer informatie over specifieke spouts gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aecde-157">Use hello links in this section tooview more information about specific spouts.</span></span>

* <span data-ttu-id="aecde-158">**Bolts**: Hallo bolts gebruikt door het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-158">**Bolts**: hello bolts used by hello topology.</span></span> <span data-ttu-id="aecde-159">Gebruik Hallo koppelingen in deze sectie tooview meer informatie over specifieke bolts.</span><span class="sxs-lookup"><span data-stu-id="aecde-159">Use hello links in this section tooview more information about specific bolts.</span></span>

* <span data-ttu-id="aecde-160">**Topologieconfiguratie**: Hallo configuratie van de topologie Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="aecde-160">**Topology configuration**: hello configuration of hello selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="aecde-161">Spout en Bolt samenvatting</span><span class="sxs-lookup"><span data-stu-id="aecde-161">Spout and Bolt summary</span></span>

<span data-ttu-id="aecde-162">Selecteren van een spout in Hallo **Spouts** of **Bolts** secties Hallo volgende informatie over Hallo geselecteerd item wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="aecde-162">Selecting a spout from hello **Spouts** or **Bolts** sections displays hello following information about hello selected item:</span></span>

* <span data-ttu-id="aecde-163">**Overzicht van onderdelen**: algemene informatie over Hallo spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="aecde-163">**Component summary**: Basic information about hello spout or bolt.</span></span>

* <span data-ttu-id="aecde-164">**Spout/Bolt stats**: statistieken over Hallo spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="aecde-164">**Spout/Bolt stats**: Statistics about hello spout or bolt.</span></span> <span data-ttu-id="aecde-165">Gebruik Hallo koppelingen in Hallo **venster** kolom tooset Hallo periode Hallo resterend posten op Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="aecde-165">Use hello links in hello **Window** column tooset hello timeframe for hello remaining entries on hello page.</span></span>

* <span data-ttu-id="aecde-166">**Input stats** (alleen Bolts): informatie over Hallo invoerstromen verbruikt door Hallo bolt.</span><span class="sxs-lookup"><span data-stu-id="aecde-166">**Input stats** (bolt only): Information about hello input streams consumed by hello bolt.</span></span>

* <span data-ttu-id="aecde-167">**Output stats**: informatie over Hallo stromen die door dit spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="aecde-167">**Output stats**: Information about hello streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="aecde-168">**Executor**: informatie over het Hallo-exemplaren van Hallo spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="aecde-168">**Executors**: Information about hello instances of hello spout or bolt.</span></span> <span data-ttu-id="aecde-169">Selecteer Hallo **poort** vermelding voor een specifieke executor tooview een logboek van diagnostische gegevens geproduceerd voor dit exemplaar.</span><span class="sxs-lookup"><span data-stu-id="aecde-169">Select hello **Port** entry for a specific executor tooview a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="aecde-170">**Fouten**: alle informatie over de fout voor deze spout of Bolts.</span><span class="sxs-lookup"><span data-stu-id="aecde-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="aecde-171">HDInsight-hulpprogramma's voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aecde-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="aecde-172">Hallo HDInsight-hulpprogramma's kunnen worden gebruikt toosubmit C# of hybride topologieën tooyour Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-172">hello HDInsight Tools can be used toosubmit C# or hybrid topologies tooyour Storm cluster.</span></span> <span data-ttu-id="aecde-173">Hallo stappen te volgen, gebruiken een voorbeeldtoepassing.</span><span class="sxs-lookup"><span data-stu-id="aecde-173">hello following steps use a sample application.</span></span> <span data-ttu-id="aecde-174">Zie voor meer informatie over het maken van uw eigen topologieën met behulp van Hallo HDInsight Tools [C#-topologieën ontwikkelen met Hallo HDInsight Tools voor Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="aecde-174">For information about creating your own topologies by using hello HDInsight Tools, see [Develop C# topologies using hello HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="aecde-175">Gebruik Hallo volgende stappen toodeploy een voorbeeld tooyour Storm op HDInsight-cluster, en vervolgens weergeven en beheren van Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-175">Use hello following steps toodeploy a sample tooyour Storm on HDInsight cluster, then view and manage hello topology.</span></span>

1. <span data-ttu-id="aecde-176">Als u hebt niet is gebeurd Hallo meest recente versie van Hallo HDInsight Tools voor Visual Studio, Zie [aan de slag met HDInsight Tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aecde-176">If you have not already installed hello latest version of hello HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="aecde-177">Open Visual Studio, selecteer **bestand** > **nieuw** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="aecde-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="aecde-178">In Hallo **nieuw Project** dialoogvenster Vouw **geïnstalleerde** > **sjablonen**, en selecteer vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aecde-178">In hello **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="aecde-179">Selecteer in de lijst met sjablonen Hallo **Storm voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="aecde-179">From hello list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="aecde-180">Typ een naam voor de toepassing hello Hallo onderaan in het dialoogvenster voor Hallo in.</span><span class="sxs-lookup"><span data-stu-id="aecde-180">At hello bottom of hello dialog box, type a name for hello application.</span></span>

    ![Afbeelding](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="aecde-182">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="aecde-182">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aecde-183">Als u wordt gevraagd, voert u Hallo aanmeldingsreferenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="aecde-183">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="aecde-184">Als u meer dan één abonnement hebt, meldt u zich in toohello een bestand met uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-184">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="aecde-185">Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="aecde-185">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="aecde-186">U kunt controleren of Hallo verzending is voltooid met Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="aecde-186">You can monitor whether hello submission is successful by using hello **Output** window.</span></span>

6. <span data-ttu-id="aecde-187">Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën** voor Hallo cluster moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="aecde-187">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="aecde-188">Selecteer Hallo-topologie in Hallo lijst tooview informatie over Hallo topologie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aecde-188">Select hello topology from hello list tooview information about hello running topology.</span></span>

    ![monitor voor Visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="aecde-190">U kunt ook weergeven **Storm-topologieën** van **Server Explorer** door het uitbreiden van **Azure** > **HDInsight**, en klik vervolgens met de rechtermuisknop op een Storm op HDInsight-cluster en het selecteren van **weergave Storm-topologieën**.</span><span class="sxs-lookup"><span data-stu-id="aecde-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="aecde-191">Selecteer Hallo shape voor Hallo spouts of bolts tooview informatie over deze onderdelen.</span><span class="sxs-lookup"><span data-stu-id="aecde-191">Select hello shape for hello spouts or bolts tooview information about these components.</span></span> <span data-ttu-id="aecde-192">Er wordt een nieuw venster geopend voor elk item geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="aecde-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aecde-193">Hallo-naam van Hallo topologie Hallo klassenaam van Hallo-topologie is (in dit geval `HelloWord`,) met een tijdstempel toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="aecde-193">hello name of hello topology is hello class name of hello topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="aecde-194">Van Hallo **Topology Summary** weergave, selecteer **Kill** toostop Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="aecde-194">From hello **Topology Summary** view, select **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="aecde-195">Storm-topologieën blijft in uitvoering totdat ze zijn gestopt of Hallo cluster wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="aecde-195">Storm topologies continue running until they are stopped or hello cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="aecde-196">REST API</span><span class="sxs-lookup"><span data-stu-id="aecde-196">REST API</span></span>

<span data-ttu-id="aecde-197">Hallo Storm-gebruikersinterface is gebaseerd op Hallo REST API, zodat u kunt vergelijkbare management en de controlefunctionaliteit met behulp van Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="aecde-197">hello Storm UI is built on top of hello REST API, so you can perform similar management and monitoring functionality by using hello REST API.</span></span> <span data-ttu-id="aecde-198">U kunt Hallo REST-API toocreate aangepaste hulpprogramma's gebruiken voor het beheren en controleren van Storm-topologieën.</span><span class="sxs-lookup"><span data-stu-id="aecde-198">You can use hello REST API toocreate custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="aecde-199">Zie voor meer informatie [Storm UI REST-API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="aecde-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="aecde-200">Hallo is volgende informatie specifiek toousing Hallo REST-API met Apache Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aecde-200">hello following information is specific toousing hello REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="aecde-201">Basis-URI</span><span class="sxs-lookup"><span data-stu-id="aecde-201">Base URI</span></span>

<span data-ttu-id="aecde-202">Hallo basis-URI voor Hallo REST-API op HDInsight-clusters is **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, waarbij **clustername** is Hallo-naam van uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-202">hello base URI for hello REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is hello name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="aecde-203">Authentication</span><span class="sxs-lookup"><span data-stu-id="aecde-203">Authentication</span></span>

<span data-ttu-id="aecde-204">Aanvragen toohello REST-API moet gebruiken **basisverificatie**, zodat u Hallo HDInsight-cluster beheerdersnaam en het wachtwoord gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aecde-204">Requests toohello REST API must use **basic authentication**, so you use hello HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="aecde-205">Omdat basisverificatie wordt verzonden met behulp van de versleutelde tekst, moet u **altijd** toosecure-HTTPS-communicatie met de Hallo-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aecde-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS toosecure communications with hello cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="aecde-206">Waarden geretourneerd</span><span class="sxs-lookup"><span data-stu-id="aecde-206">Return values</span></span>

<span data-ttu-id="aecde-207">Informatie die wordt geretourneerd vanaf Hallo REST-API is mogelijk alleen bruikbaar uit binnen Hallo cluster of virtuele machines op Hallo hetzelfde virtuele Azure-netwerk als Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="aecde-207">Information that is returned from hello REST API may only be usable from within hello cluster or virtual machines on hello same Azure Virtual Network as hello cluster.</span></span> <span data-ttu-id="aecde-208">Hallo volledig gekwalificeerde domeinnaam (FQDN) geretourneerd voor Zookeeper-servers zijn bijvoorbeeld niet worden toegankelijk is vanaf Internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="aecde-208">For example, hello fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from hello Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aecde-209">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aecde-209">Next Steps</span></span>

<span data-ttu-id="aecde-210">Nu u hebt geleerd hoe toodeploy en monitor topologieën met behulp van Storm-Dashboard hello, kunt u nagaan hoe:</span><span class="sxs-lookup"><span data-stu-id="aecde-210">Now that you've learned how toodeploy and monitor topologies by using hello Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="aecde-211">C#-topologieën met Hallo HDInsight Tools voor Visual Studio ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="aecde-211">Develop C# topologies using hello HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="aecde-212">Java gebaseerde topologieën met Maven ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="aecde-212">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="aecde-213">Zie voor een lijst van meer voorbeeldtopologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="aecde-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
