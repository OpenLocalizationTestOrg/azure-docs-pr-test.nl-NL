---
title: aaaEnable heap dumpbestanden voor Hadoop op HDInsight - Azure-services | Microsoft Docs
description: Schakel heap dumpbestanden voor Hadoop-services voor foutopsporing en analyse van Linux gebaseerde HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8f151adb-f687-41e4-aca0-82b551953725
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 49e30f26e1a83f19e068e9da253b5548caec70d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="enable-heap-dumps-for-hadoop-services-on-linux-based-hdinsight"></a><span data-ttu-id="ac4f2-103">Dumpbestanden voor Hadoop-services op Linux gebaseerde HDInsight heap inschakelen</span><span class="sxs-lookup"><span data-stu-id="ac4f2-103">Enable heap dumps for Hadoop services on Linux-based HDInsight</span></span>

[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="ac4f2-104">Dumpbestanden voor heap bevatten een momentopname van de toepassing hello geheugen, met inbegrip van waarden van variabelen Hallo gelijktijdig Hallo Hallo dump is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-104">Heap dumps contain a snapshot of hello application's memory, including hello values of variables at hello time hello dump was created.</span></span> <span data-ttu-id="ac4f2-105">Ze zijn daarom nuttig voor het oplossen van problemen die tijdens runtime optreden.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-105">So they are useful for diagnosing problems that occur at run-time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ac4f2-106">Hallo werken stappen in dit document alleen met HDInsight-clusters die gebruikmaken van Linux.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-106">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="ac4f2-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ac4f2-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ac4f2-109"><a name="whichServices"></a>Services</span><span class="sxs-lookup"><span data-stu-id="ac4f2-109"><a name="whichServices"></a>Services</span></span>

<span data-ttu-id="ac4f2-110">U kunt de heap dumpbestanden voor Hallo na services inschakelen:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-110">You can enable heap dumps for hello following services:</span></span>

* <span data-ttu-id="ac4f2-111">**hcatalog** -tempelton</span><span class="sxs-lookup"><span data-stu-id="ac4f2-111">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="ac4f2-112">**hive** -hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="ac4f2-112">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="ac4f2-113">**mapreduce** -jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="ac4f2-113">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="ac4f2-114">**yarn** -resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="ac4f2-114">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="ac4f2-115">**hdfs** -datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="ac4f2-115">**hdfs** - datanode, secondarynamenode, namenode</span></span>

<span data-ttu-id="ac4f2-116">U kunt ook heap dumpbestanden voor Hallo kaart inschakelen en de processen die worden uitgevoerd door HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-116">You can also enable heap dumps for hello map and reduce processes ran by HDInsight.</span></span>

## <span data-ttu-id="ac4f2-117"><a name="configuration"></a>Understanding heap dump configuratie</span><span class="sxs-lookup"><span data-stu-id="ac4f2-117"><a name="configuration"></a>Understanding heap dump configuration</span></span>

<span data-ttu-id="ac4f2-118">Dumpbestanden voor heap zijn ingeschakeld door de opties (ook wel aangeduid als kiest, of parameters) toohello JVM wanneer een service wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-118">Heap dumps are enabled by passing options (sometimes known as opts, or parameters) toohello JVM when a service is started.</span></span> <span data-ttu-id="ac4f2-119">Voor de meeste Hadoop-services, kunt u Hallo shell-script waarmee toostart Hallo service toopass deze opties wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-119">For most Hadoop services, you can modify hello shell script used toostart hello service toopass these options.</span></span>

<span data-ttu-id="ac4f2-120">In elk script is een exporteren voor  **\* \_OPTS**, toohello JVM die Hallo opties bevat die worden doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-120">In each script, there is an export for **\*\_OPTS**, which contains hello options passed toohello JVM.</span></span> <span data-ttu-id="ac4f2-121">Bijvoorbeeld in Hallo **hadoop env.sh** script, Hallo-regel die begint met `export HADOOP_NAMENODE_OPTS=` Hallo opties voor Hallo NameNode service bevat.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-121">For example, in hello **hadoop-env.sh** script, hello line that begins with `export HADOOP_NAMENODE_OPTS=` contains hello options for hello NameNode service.</span></span>

<span data-ttu-id="ac4f2-122">Overzicht en verminderen processen zijn enigszins verschillen, omdat deze bewerkingen een onderliggend proces van Hallo MapReduce-service zijn.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-122">Map and reduce processes are slightly different, as these operations are a child process of hello MapReduce service.</span></span> <span data-ttu-id="ac4f2-123">Elk toewijzen of verminder proces wordt uitgevoerd in een container onderliggend en er zijn twee vermeldingen die Hallo JVM opties bevatten.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-123">Each map or reduce process runs in a child container, and there are two entries that contain hello JVM options.</span></span> <span data-ttu-id="ac4f2-124">Beide opgenomen in **mapred site.xml**:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-124">Both contained in **mapred-site.xml**:</span></span>

* <span data-ttu-id="ac4f2-125">**mapreduce.Admin.map.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="ac4f2-125">**mapreduce.admin.map.child.java.opts**</span></span>
* <span data-ttu-id="ac4f2-126">**mapreduce.Admin.reduce.child.Java.opts**</span><span class="sxs-lookup"><span data-stu-id="ac4f2-126">**mapreduce.admin.reduce.child.java.opts**</span></span>

> [!NOTE]
> <span data-ttu-id="ac4f2-127">U wordt aangeraden met Ambari toomodify beide Hallo scripts en mapred site.xml-instellingen als Ambari verwerken wijzigingen tussen knooppunten in cluster hello te repliceren.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-127">We recommend using Ambari toomodify both hello scripts and mapred-site.xml settings, as Ambari handle replicating changes across nodes in hello cluster.</span></span> <span data-ttu-id="ac4f2-128">Zie Hallo [Ambari met behulp van](#using-ambari) sectie voor specifieke stappen.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-128">See hello [Using Ambari](#using-ambari) section for specific steps.</span></span>

### <a name="enable-heap-dumps"></a><span data-ttu-id="ac4f2-129">Heapdumps inschakelen</span><span class="sxs-lookup"><span data-stu-id="ac4f2-129">Enable heap dumps</span></span>

<span data-ttu-id="ac4f2-130">Hallo volgende optie wordt ingeschakeld heap dumpbestanden wanneer er een OutOfMemoryError optreedt:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-130">hello following option enables heap dumps when an OutOfMemoryError occurs:</span></span>

    -XX:+HeapDumpOnOutOfMemoryError

<span data-ttu-id="ac4f2-131">Hallo  **+**  geeft aan dat deze optie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-131">hello **+** indicates that this option is enabled.</span></span> <span data-ttu-id="ac4f2-132">Hallo standaard is uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-132">hello default is disabled.</span></span>

> [!WARNING]
> <span data-ttu-id="ac4f2-133">Dumpbestanden voor heap zijn niet ingeschakeld voor services van Hadoop in HDInsight standaard zoals dumpbestanden Hallo kunnen oplopen.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-133">Heap dumps are not enabled for Hadoop services on HDInsight by default, as hello dump files can be large.</span></span> <span data-ttu-id="ac4f2-134">Als u ze voor het oplossen van inschakelt, moet u ze zodra u hebt gereproduceerd Hallo probleem en de verzamelde Hallo dumpbestanden toodisable.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-134">If you do enable them for troubleshooting, remember toodisable them once you have reproduced hello problem and gathered hello dump files.</span></span>

### <a name="dump-location"></a><span data-ttu-id="ac4f2-135">Locatie van de dump</span><span class="sxs-lookup"><span data-stu-id="ac4f2-135">Dump location</span></span>

<span data-ttu-id="ac4f2-136">de standaardlocatie Hallo voor Hallo-bestand is de huidige werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-136">hello default location for hello dump file is hello current working directory.</span></span> <span data-ttu-id="ac4f2-137">U kunt bepalen wanneer hello bestand wordt opgeslagen met behulp van de volgende optie Hallo:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-137">You can control where hello file is stored using hello following option:</span></span>

    -XX:HeapDumpPath=/path

<span data-ttu-id="ac4f2-138">Bijvoorbeeld, met behulp van `-XX:HeapDumpPath=/tmp` Hallo dumpbestanden toobe opgeslagen in Hallo map directory veroorzaakt.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-138">For example, using `-XX:HeapDumpPath=/tmp` causes hello dumps toobe stored in hello /tmp directory.</span></span>

### <a name="scripts"></a><span data-ttu-id="ac4f2-139">Scripts</span><span class="sxs-lookup"><span data-stu-id="ac4f2-139">Scripts</span></span>

<span data-ttu-id="ac4f2-140">U kunt ook een script activeren wanneer een **OutOfMemoryError** optreedt.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-140">You can also trigger a script when an **OutOfMemoryError** occurs.</span></span> <span data-ttu-id="ac4f2-141">Bijvoorbeeld, is een melding activeren zodat u dat Hallo-fout weet opgetreden.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-141">For example, triggering a notification so you know that hello error has occurred.</span></span> <span data-ttu-id="ac4f2-142">Gebruik Hallo volgende optie tootrigger een script op een __OutOfMemoryError__:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-142">Use hello following option tootrigger a script on an __OutOfMemoryError__:</span></span>

    -XX:OnOutOfMemoryError=/path/to/script

> [!NOTE]
> <span data-ttu-id="ac4f2-143">Aangezien Hadoop een gedistribueerd systeem is, moet elk script dat wordt gebruikt op alle knooppunten in cluster Hallo die Hallo-service wordt uitgevoerd op worden geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-143">Since Hadoop is a distributed system, any script used must be placed on all nodes in hello cluster that hello service runs on.</span></span>
> 
> <span data-ttu-id="ac4f2-144">Hallo script moet ook worden op een locatie die toegankelijk is voor Hallo account Hallo-service wordt uitgevoerd als moet machtigingen voor uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-144">hello script must also be in a location that is accessible by hello account hello service runs as, and must provide execute permissions.</span></span> <span data-ttu-id="ac4f2-145">Bijvoorbeeld, u kunt desgewenst toostore scripts in `/usr/local/bin` en gebruik `chmod go+rx /usr/local/bin/filename.sh` toogrant lees- en schrijfrechten hebben.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-145">For example, you may wish toostore scripts in `/usr/local/bin` and use `chmod go+rx /usr/local/bin/filename.sh` toogrant read and execute permissions.</span></span>

## <a name="using-ambari"></a><span data-ttu-id="ac4f2-146">Ambari gebruiken</span><span class="sxs-lookup"><span data-stu-id="ac4f2-146">Using Ambari</span></span>

<span data-ttu-id="ac4f2-147">toomodify Hallo-configuratie voor een service, gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-147">toomodify hello configuration for a service, use hello following steps:</span></span>

1. <span data-ttu-id="ac4f2-148">Open Hallo Ambari-webgebruikersinterface voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-148">Open hello Ambari web UI for your cluster.</span></span> <span data-ttu-id="ac4f2-149">Hallo-URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-149">hello URL is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span>

    <span data-ttu-id="ac4f2-150">Wanneer u wordt gevraagd, worden geverifieerd toohello site met de accountnaam Hallo HTTP (standaard: admin) en het wachtwoord voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-150">When prompted, authenticate toohello site using hello HTTP account name (default: admin) and password for your cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="ac4f2-151">U mogelijk gevraagd een tweede maal door Ambari voor Hallo-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-151">You may be prompted a second time by Ambari for hello user name and password.</span></span> <span data-ttu-id="ac4f2-152">Als dit het geval is, voert u dezelfde naam en het wachtwoord Hallo</span><span class="sxs-lookup"><span data-stu-id="ac4f2-152">If so, enter hello same account name and password</span></span>

2. <span data-ttu-id="ac4f2-153">Hallo-lijst met aan de linkerkant Hallo Selecteer Hallo servicegebied u toomodify.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-153">Using hello list of on hello left, select hello service area you want toomodify.</span></span> <span data-ttu-id="ac4f2-154">Bijvoorbeeld: **HDFS**.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-154">For example, **HDFS**.</span></span> <span data-ttu-id="ac4f2-155">Selecteer bij Hallo center Hallo **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-155">In hello center area, select hello **Configs** tab.</span></span>

    ![Afbeelding van Ambari web met HDFS Configs tabblad is geselecteerd](./media/hdinsight-hadoop-heap-dump-linux/serviceconfig.png)

3. <span data-ttu-id="ac4f2-157">Met behulp van Hallo **Filter...**  -item, voer **kiest**.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-157">Using hello **Filter...** entry, enter **opts**.</span></span> <span data-ttu-id="ac4f2-158">Alleen items met deze tekst worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-158">Only items containing this text are displayed.</span></span>

    ![Gefilterde lijst](./media/hdinsight-hadoop-heap-dump-linux/filter.png)

4. <span data-ttu-id="ac4f2-160">Hallo zoeken  **\* \_OPTS** vermelding voor Hallo service u wilt tooenable heap dumpbestanden voor en voeg Hallo-opties wilt tooenable.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-160">Find hello **\*\_OPTS** entry for hello service you want tooenable heap dumps for, and add hello options you wish tooenable.</span></span> <span data-ttu-id="ac4f2-161">Ik heb toegevoegd in Hallo installatiekopie te volgen, `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** post:</span><span class="sxs-lookup"><span data-stu-id="ac4f2-161">In hello following image, I've added `-XX:+HeapDumpOnOutOfMemoryError -XX:HeapDumpPath=/tmp/` toohello **HADOOP\_NAMENODE\_OPTS** entry:</span></span>

    ![HADOOP_NAMENODE_OPTS met - XX: + HeapDumpOnOutOfMemoryError - XX: HeapDumpPath = / tmp /](./media/hdinsight-hadoop-heap-dump-linux/opts.png)

   > [!NOTE]
   > <span data-ttu-id="ac4f2-163">Wanneer inschakelen heap dumpbestanden voor Hallo toewijzen of onderliggend proces verminderen, zoekt u naar Hallo velden met de naam **mapreduce.admin.map.child.java.opts** en **mapreduce.admin.reduce.child.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-163">When enabling heap dumps for hello map or reduce child process, look for hello fields named **mapreduce.admin.map.child.java.opts** and **mapreduce.admin.reduce.child.java.opts**.</span></span>

    <span data-ttu-id="ac4f2-164">Gebruik Hallo **opslaan** knop toosave Hallo wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-164">Use hello **Save** button toosave hello changes.</span></span> <span data-ttu-id="ac4f2-165">U kunt een korte notitie Hallo wijzigingen met een beschrijving invoeren.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-165">You can enter a short note describing hello changes.</span></span>

5. <span data-ttu-id="ac4f2-166">Nadat de Hallo wijzigingen zijn toegepast, Hallo **opnieuw opstarten vereist** pictogram wordt weergegeven naast een of meer services.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-166">Once hello changes have been applied, hello **Restart required** icon appears beside one or more services.</span></span>

    ![opnieuw opstarten vereist het pictogram en start opnieuw op de knop](./media/hdinsight-hadoop-heap-dump-linux/restartrequiredicon.png)

6. <span data-ttu-id="ac4f2-168">Selecteer elke service die u een herstart moet en gebruik van Hallo **serviceacties** knop te**inschakelen op onderhoudsmodus**.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-168">Select each service that needs a restart, and use hello **Service Actions** button too**Turn On Maintenance Mode**.</span></span> <span data-ttu-id="ac4f2-169">Onderhoudsmodus wordt voorkomen dat waarschuwingen van Hallo-service wordt gegenereerd wanneer u deze opnieuw starten.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-169">Maintenance mode prevents alerts from being generated from hello service when you restart it.</span></span>

    ![Menu Onderhoud-modus inschakelen](./media/hdinsight-hadoop-heap-dump-linux/maintenancemode.png)

7. <span data-ttu-id="ac4f2-171">Nadat u de onderhoudsmodus hebt ingeschakeld, gebruikt u Hallo **opnieuw** knop voor Hallo-service te**alle verricht opnieuw starten**</span><span class="sxs-lookup"><span data-stu-id="ac4f2-171">Once you have enabled maintenance mode, use hello **Restart** button for hello service too**Restart All Effected**</span></span>

    ![Start opnieuw alle van invloed op een vermelding](./media/hdinsight-hadoop-heap-dump-linux/restartbutton.png)

   > [!NOTE]
   > <span data-ttu-id="ac4f2-173">vermeldingen voor Hallo Hallo **opnieuw** knop kan afwijken voor andere services.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-173">hello entries for hello **Restart** button may be different for other services.</span></span>

8. <span data-ttu-id="ac4f2-174">Zodra het Hallo-services opnieuw zijn opgestart, gebruikt u Hallo **serviceacties** te knop**inschakelen uit onderhoudsmodus**.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-174">Once hello services have been restarted, use hello **Service Actions** button too**Turn Off Maintenance Mode**.</span></span> <span data-ttu-id="ac4f2-175">Deze Ambari tooresume bewaking voor waarschuwingen voor Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="ac4f2-175">This Ambari tooresume monitoring for alerts for hello service.</span></span>

