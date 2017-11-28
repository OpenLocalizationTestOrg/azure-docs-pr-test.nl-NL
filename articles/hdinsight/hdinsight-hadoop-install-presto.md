---
title: aaaInstall functie in Azure HDInsight Linux-clusters | Microsoft Docs
description: Meer informatie over hoe tooinstall functie en Airpal op Linux gebaseerde HDInsight Hadoop-clusters met behulp van scriptacties.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: nitinme
ms.openlocfilehash: 5d54d0efc3e5fdc6f5a8d3a94ad2f61d16df24c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-presto-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="fc5b1-103">Installeren en gebruiken Presto op HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="fc5b1-103">Install and use Presto on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="fc5b1-104">In dit onderwerp leert u hoe tooinstall functie op HDInsight Hadoop-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-104">In this topic, you learn how tooinstall Presto on HDInsight Hadoop clusters by using Script Action.</span></span> <span data-ttu-id="fc5b1-105">U leert ook hoe tooinstall Airpal op een bestaand Presto HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-105">You also learn how tooinstall Airpal on an existing Presto HDInsight cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fc5b1-106">Hallo stappen in dit document vereisen een **HDInsight 3.5 Hadoop-cluster** die gebruikmaakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-106">hello steps in this document require an **HDInsight 3.5 Hadoop cluster** that uses Linux.</span></span> <span data-ttu-id="fc5b1-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fc5b1-108">Zie voor meer informatie [versies van HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-108">For more information, see [HDInsight versions](hdinsight-component-versioning.md).</span></span>

## <a name="what-is-presto"></a><span data-ttu-id="fc5b1-109">Wat is Presto?</span><span class="sxs-lookup"><span data-stu-id="fc5b1-109">What is Presto?</span></span>
<span data-ttu-id="fc5b1-110">[Presto](https://prestodb.io/overview.html) is een snelle gedistribueerde SQL query-engine voor big data.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-110">[Presto](https://prestodb.io/overview.html) is a fast distributed SQL query engine for big data.</span></span> <span data-ttu-id="fc5b1-111">Functie is geschikt voor petabytes aan gegevens interactieve query's naar.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-111">Presto is suitable for interactive querying of petabytes of data.</span></span> <span data-ttu-id="fc5b1-112">Zie voor meer informatie over Hallo onderdelen van de functie en hoe ze samenwerken [Presto concepten](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-112">For more information on hello components of Presto and how they work together, see [Presto concepts](https://github.com/prestodb/presto/blob/master/presto-docs/src/main/sphinx/overview/concepts.rst).</span></span>

> [!WARNING]
> <span data-ttu-id="fc5b1-113">Onderdelen van Hallo HDInsight-cluster worden volledig ondersteund en Microsoft Support zal helpen tooisolate en oplossen van problemen met gerelateerde toothese onderdelen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-113">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
> 
> <span data-ttu-id="fc5b1-114">Aangepaste onderdelen, zoals de functie, ontvangen binnen commercieel redelijke ondersteuning toohelp u toofurther Hallo probleem op te lossen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-114">Custom components, such as Presto, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="fc5b1-115">Dit kan leiden tot het oplossen van Hallo probleem of vragen dat u tooengage beschikbare kanalen voor Hallo openen bron technologieën waar grondige kennis van deze technologie kan worden gevonden.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-115">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="fc5b1-116">Bijvoorbeeld: Er zijn veel community-sites die kunnen worden gebruikt, zoals: [MSDN-forum voor HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Ook hebben Apache projecten project-sites op [http://apache.org](http://apache.org), bijvoorbeeld: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-116">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>
> 
> 


## <a name="install-presto-using-script-action"></a><span data-ttu-id="fc5b1-117">Met behulp van de scriptactie functie installeren</span><span class="sxs-lookup"><span data-stu-id="fc5b1-117">Install Presto using script action</span></span>

<span data-ttu-id="fc5b1-118">Deze sectie bevat instructies over hoe toouse Hallo voorbeeldscript bij het maken van een nieuw cluster met behulp van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-118">This section provides instructions on how toouse hello sample script when creating a new cluster by using hello Azure portal.</span></span> 

1. <span data-ttu-id="fc5b1-119">Start met het inrichten van een cluster met behulp van de stappen in Hallo [Provision Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-119">Start provisioning a cluster by using hello steps in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span> <span data-ttu-id="fc5b1-120">Zorg ervoor dat u met behulp van Hallo Hallo-cluster maakt **aangepaste** stroom voor het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-120">Make sure you create hello cluster using hello **Custom** cluster creation flow.</span></span> <span data-ttu-id="fc5b1-121">U moet ervoor zorgen dat Hallo-cluster dat u maakt aan Hallo volgens de vereisten voldoet.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-121">You must ensure that hello cluster you create meets hello following requirements.</span></span>

    <span data-ttu-id="fc5b1-122">a.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-122">a.</span></span> <span data-ttu-id="fc5b1-123">Het moet een Hadoop-cluster met HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-123">It must be a Hadoop cluster with HDInsight version 3.5.</span></span>

    <span data-ttu-id="fc5b1-124">b.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-124">b.</span></span> <span data-ttu-id="fc5b1-125">Azure Storage moet als gegevensarchief Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-125">It must use Azure Storage as hello data store.</span></span> <span data-ttu-id="fc5b1-126">Met Presto op een cluster die gebruikmaakt van Azure Data Lake Store als opslagoptie Hallo is nog niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-126">Using Presto on a cluster that uses Azure Data Lake Store as hello storage option is not yet supported.</span></span> 

    ![Maken van het HDInsight-cluster met aangepaste opties](./media/hdinsight-hadoop-install-presto/hdinsight-install-custom.png)

2. <span data-ttu-id="fc5b1-128">Op Hallo **geavanceerde instellingen** blade Selecteer **scriptacties**, en geef Hallo informatie hieronder:</span><span class="sxs-lookup"><span data-stu-id="fc5b1-128">On hello **Advanced settings** blade, select **Script Actions**, and provide hello information below:</span></span>
   
   * <span data-ttu-id="fc5b1-129">**NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-129">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="fc5b1-130">**Bash-script-URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span><span class="sxs-lookup"><span data-stu-id="fc5b1-130">**Bash script URI**: `https://raw.githubusercontent.com/hdinsight/presto-hdinsight/master/installpresto.sh`</span></span>
   * <span data-ttu-id="fc5b1-131">**HEAD**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="fc5b1-131">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="fc5b1-132">**WERKNEMER**: Schakel deze optie</span><span class="sxs-lookup"><span data-stu-id="fc5b1-132">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="fc5b1-133">**ZOOKEEPER**: Schakel dit selectievakje</span><span class="sxs-lookup"><span data-stu-id="fc5b1-133">**ZOOKEEPER**: Clear this check box</span></span>
   * <span data-ttu-id="fc5b1-134">**PARAMETERS**: dit veld leeg laten</span><span class="sxs-lookup"><span data-stu-id="fc5b1-134">**PARAMETERS**: Leave this field blank</span></span>


3. <span data-ttu-id="fc5b1-135">Hallo Hallo onderaan in **scriptacties** blade, klikt u op Hallo **selecteren** knop toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-135">At hello bottom of hello **Script Actions** blade, click hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="fc5b1-136">Tot slot op Hallo **Selecteer** knop onderin Hallo Hallo **geavanceerde instellingen** blade toosave Hallo configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-136">Finally, click  hello **Select** button at hello bottom of hello **Advanced Settings** blade toosave hello configuration information.</span></span>

4. <span data-ttu-id="fc5b1-137">Doorgaan Hallo cluster inrichten, zoals beschreven in [Provision Linux gebaseerde HDInsight-clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-137">Continue provisioning hello cluster as described in [Provision Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="fc5b1-138">Gebruikte tooapply scriptacties kunnen ook worden door Azure PowerShell, hello Azure CLI, Hallo HDInsight .NET SDK of Azure Resource Manager-sjablonen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-138">Azure PowerShell, hello Azure CLI, hello HDInsight .NET SDK, or Azure Resource Manager templates can also be used tooapply script actions.</span></span> <span data-ttu-id="fc5b1-139">U kunt ook script acties tooalready actieve clusters toepassen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-139">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="fc5b1-140">Zie voor meer informatie [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-140">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>
    > 
    > 

## <a name="use-presto-with-hdinsight"></a><span data-ttu-id="fc5b1-141">Functie gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="fc5b1-141">Use Presto with HDInsight</span></span>

<span data-ttu-id="fc5b1-142">Voer Hallo stappen toouse functie in een HDInsight-cluster te volgen nadat u hebt geïnstalleerd met behulp van Hallo stappen die hierboven worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-142">Perform hello following steps toouse Presto in an HDInsight cluster after you have installed it using hello steps described above.</span></span>

1. <span data-ttu-id="fc5b1-143">Verbinding maken met toohello HDInsight-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="fc5b1-143">Connect toohello HDInsight cluster using SSH:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="fc5b1-144">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-144">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
     

2. <span data-ttu-id="fc5b1-145">Hallo Presto shell met behulp van de volgende opdracht Hallo starten.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-145">Start hello Presto shell using hello following command.</span></span>
   
        presto --schema default

3. <span data-ttu-id="fc5b1-146">Een query uitvoeren op een voorbeeldtabel **hivesampletable**, die beschikbaar zijn op alle HDInsight-clusters standaard is.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-146">Run a query on a sample table, **hivesampletable**, which is available on all HDInsight clusters by default.</span></span>
   
        select count (*) from hivesampletable;
   
    <span data-ttu-id="fc5b1-147">Standaard [Hive](https://prestodb.io/docs/current/connector/hive.html) en [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors voor de functie al zijn geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-147">By default, [Hive](https://prestodb.io/docs/current/connector/hive.html) and [TPCH](https://prestodb.io/docs/current/connector/tpch.html) connectors for Presto are already configured.</span></span> <span data-ttu-id="fc5b1-148">Hive-connector is geconfigureerde toouse Hallo standaard geïnstalleerd Hive installatie, zodat alle Hallo tabellen vanuit Hive wordt automatisch zichtbaar in de functie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-148">Hive connector is configured toouse hello default installed Hive installation, so all hello tables from Hive will be automatically visible in Presto.</span></span>

    <span data-ttu-id="fc5b1-149">Zie voor een gedetailleerde beschrijving van hoe u de functie kunt gebruiken, [Presto documentatie](https://prestodb.io/docs/current/index.html).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-149">For a detailed description on how you can use Presto, see [Presto documentation](https://prestodb.io/docs/current/index.html).</span></span>

## <a name="use-airpal-with-presto"></a><span data-ttu-id="fc5b1-150">Airpal gebruiken met de functie</span><span class="sxs-lookup"><span data-stu-id="fc5b1-150">Use Airpal with Presto</span></span>

<span data-ttu-id="fc5b1-151">[Airpal](https://github.com/airbnb/airpal#airpal) is een open source web gebaseerde QueryInterface voor de functie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-151">[Airpal](https://github.com/airbnb/airpal#airpal) is an open-source web-based query interface for Presto.</span></span> <span data-ttu-id="fc5b1-152">Zie voor meer informatie over Airpal [Airpal documentatie](https://github.com/airbnb/airpal#airpal).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-152">For more information on Airpal, see [Airpal documentation](https://github.com/airbnb/airpal#airpal).</span></span>

<span data-ttu-id="fc5b1-153">In dit gedeelte kijken we Hallo stappen te**Airpal installeren op Hallo edgenode** van een HDInsight Hadoop-cluster dat al functie heeft geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-153">In this section, we look at hello steps too**install Airpal on hello edgenode** of an HDInsight Hadoop cluster, that already has Presto installed.</span></span> <span data-ttu-id="fc5b1-154">Dit zorgt ervoor dat Hallo Airpal webinterface query beschikbaar is via Hallo Internet.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-154">This ensures that hello Airpal web query interface is available over hello Internet.</span></span>

1. <span data-ttu-id="fc5b1-155">Gebruik van SSH verbinding toohello headnode van Hallo HDInsight-cluster met Presto zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="fc5b1-155">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="fc5b1-156">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-156">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fc5b1-157">Nadat u verbonden bent, Hallo volgende opdracht worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-157">Once you are connected, run hello following command.</span></span>

        sudo slider registry  --name presto1 --getexp presto 
   
    <span data-ttu-id="fc5b1-158">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="fc5b1-158">You should see an output like hello following:</span></span>

        {
            "coordinator_address" : [ {
                "value" : "10.0.0.12:9090",
                "level" : "application",
                "updatedTime" : "Mon Apr 03 20:13:41 UTC 2017"
        } ]

3. <span data-ttu-id="fc5b1-159">Houd er rekening mee Hallo-waarde voor Hallo van Hallo uitvoer **waarde** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-159">From hello output, note hello value for hello **value** property.</span></span> <span data-ttu-id="fc5b1-160">U moet dit tijdens het installeren van Airpal op Hallo cluster edgenode.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-160">You will need this while installing Airpal on hello cluster edgenode.</span></span> <span data-ttu-id="fc5b1-161">Is van de uitvoer Hallo boven Hallo-waarde die u moet **10.0.0.12:9090**.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-161">From hello output above, hello value that you will need is **10.0.0.12:9090**.</span></span>

4. <span data-ttu-id="fc5b1-162">Hallo-sjabloon gebruiken  **[hier](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)**  toocreate een HDInsight cluster edgenode en Hallo waarden opgeven, zoals wordt weergegeven in de volgende schermafbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-162">Use hello template **[here](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fhdinsight%2Fpresto-hdinsight%2Fmaster%2Fairpal-deploy.json)** toocreate an HDInsight cluster edgenode and provide hello values as shown in hello following screenshot.</span></span>

    ![HDInsight installatie Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-install-airpal.png)

5. <span data-ttu-id="fc5b1-164">Klik op **Kopen**.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-164">Click **Purchase**.</span></span>

6. <span data-ttu-id="fc5b1-165">Als de Hallo wijzigingen zijn toegepast toohello clusterconfiguratie, kunt u Hallo Airpal webinterface openen met behulp van Hallo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-165">Once hello changes are applied toohello cluster configuration, you can access hello Airpal web interface by using hello following steps.</span></span>

    <span data-ttu-id="fc5b1-166">a.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-166">a.</span></span> <span data-ttu-id="fc5b1-167">Cluster-blade hello, klikt u op **toepassingen**.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-167">From hello cluster blade, click **Applications**.</span></span>

    ![HDInsight starten Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal.png)

    <span data-ttu-id="fc5b1-169">b.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-169">b.</span></span> <span data-ttu-id="fc5b1-170">Van Hallo **geïnstalleerde Apps** blade, klikt u op **Portal** tegen airpal.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-170">From hello **Installed Apps** blade, click **Portal** against airpal.</span></span>

    ![HDInsight starten Airpal op Presto cluster](./media/hdinsight-hadoop-install-presto/hdinsight-presto-launch-airpal-1.png)

    <span data-ttu-id="fc5b1-172">c.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-172">c.</span></span> <span data-ttu-id="fc5b1-173">Voer desgevraagd Hallo-referenties die u hebt opgegeven tijdens het maken van Hallo HDInsight Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-173">When prompted, enter hello admin credentials that you specified while creating hello HDInsight Hadoop cluster.</span></span>

## <a name="customize-a-presto-installation-on-hdinsight-cluster"></a><span data-ttu-id="fc5b1-174">De installatie van een Presto op HDInsight-cluster aanpassen</span><span class="sxs-lookup"><span data-stu-id="fc5b1-174">Customize a Presto installation on HDInsight cluster</span></span>

<span data-ttu-id="fc5b1-175">Nadat u de functie op een HDInsight Hadoop-cluster hebt geïnstalleerd, kunt u Hallo installatie toomake wijzigingen zoals het update-geheugeninstellingen aanpassen, wijzigt connectors, enzovoort. Voer Hallo dus toodo stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-175">After you have installed Presto on an HDInsight Hadoop cluster, you can customize hello installation toomake changes such as update memory settings, change connectors, etc. Perform hello following steps toodo so.</span></span>

1. <span data-ttu-id="fc5b1-176">Gebruik van SSH verbinding toohello headnode van Hallo HDInsight-cluster met Presto zijn geïnstalleerd:</span><span class="sxs-lookup"><span data-stu-id="fc5b1-176">Using SSH, connect toohello headnode of hello HDInsight cluster that has Presto installed:</span></span>
   
        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="fc5b1-177">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-177">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="fc5b1-178">De configuratiewijzigingen aanbrengen in Hallo bestand `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-178">Make your configuration changes in hello file `/var/lib/presto/presto-hdinsight-master/appConfig-default.json`.</span></span> <span data-ttu-id="fc5b1-179">Zie voor meer informatie over Presto configuratie [Presto configuratie voor YARN gebaseerde clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-179">For more information on Presto configuration, see [Presto configuration for YARN-based clusters](https://prestodb.io/presto-yarn/installation-yarn-configuration-options.html).</span></span>

3. <span data-ttu-id="fc5b1-180">Stop en kill Hallo actieve sessie van de functie.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-180">Stop and kill hello current running instance of Presto.</span></span>

        sudo slider stop presto1 --force
        sudo slider destroy presto1 --force

4. <span data-ttu-id="fc5b1-181">Start een nieuw exemplaar van de functie met Hallo aanpassing.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-181">Start a new instance of Presto with hello customization.</span></span>

       sudo slider create presto1 --template /var/lib/presto/presto-hdinsight-master/appConfig-default.json --resources /var/lib/presto/presto-hdinsight-master/resources-default.json

5. <span data-ttu-id="fc5b1-182">Wacht tot Hallo nieuwe exemplaar toobe gereed en noteer het adres van presto coördinator.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-182">Wait for hello new instance toobe ready and note presto coordinator address.</span></span>


       sudo slider registry --name presto1 --getexp presto

## <a name="generate-benchmark-data-for-hdinsight-clusters-that-run-presto"></a><span data-ttu-id="fc5b1-183">Benchmark-gegevens voor HDInsight-clusters met Presto genereren</span><span class="sxs-lookup"><span data-stu-id="fc5b1-183">Generate benchmark data for HDInsight clusters that run Presto</span></span>

<span data-ttu-id="fc5b1-184">TPC DS is Hallo industriestandaard voor het meten van de prestaties van veel besluit ondersteuning voor systemen, met inbegrip van big-datasystemen Hallo.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-184">TPC-DS is hello industry standard for measuring hello performance of many decision support systems, including big data systems.</span></span> <span data-ttu-id="fc5b1-185">U kunt Presto op HDInsight-clusters toogenerate gegevens gebruiken en evalueren hoe worden vergeleken met uw eigen HDInsight benchmark-gegevens.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-185">You can use Presto on HDInsight clusters toogenerate data and evaluate how it compares with your own HDInsight benchmark data.</span></span> <span data-ttu-id="fc5b1-186">Zie voor meer informatie [hier](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-186">For more information, see [here](https://github.com/hdinsight/tpcds-datagen-as-hive-query/blob/master/README.md).</span></span>



## <a name="see-also"></a><span data-ttu-id="fc5b1-187">Zie ook</span><span class="sxs-lookup"><span data-stu-id="fc5b1-187">See also</span></span>
* <span data-ttu-id="fc5b1-188">[Installeren en gebruiken van Hue op HDInsight-clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-188">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="fc5b1-189">HUE is een webgebruikersinterface waardoor u eenvoudig toocreate, uitvoeren en sla Pig en Hive-taken, ook als bladeren Hallo standaard opslag voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-189">Hue is a web UI that makes it easy toocreate, run and save Pig and Hive jobs, as well as browse hello default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="fc5b1-190">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-190">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="fc5b1-191">Cluster aanpassing tooinstall die giraph op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-191">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="fc5b1-192">Giraph kunt u tooperform grafiek verwerken met behulp van Hadoop, en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-192">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="fc5b1-193">[Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="fc5b1-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="fc5b1-194">Cluster aanpassing tooinstall die solr op HDInsight Hadoop-clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-194">Use cluster customization tooinstall Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="fc5b1-195">Solr kunt u krachtige zoekopdrachten tooperform opgeslagen gegevens.</span><span class="sxs-lookup"><span data-stu-id="fc5b1-195">Solr allows you tooperform powerful search operations on stored data.</span></span>

[hdinsight-install-r]: hdinsight-hadoop-r-scripts-linux.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
