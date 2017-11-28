---
title: Hive-bibliotheken aaaAdd tijdens het HDInsight-cluster maken - Azure | Microsoft Docs
description: Meer informatie over hoe tooadd Hive-bibliotheken (jar-bestanden), tooan HDInsight-cluster tijdens het maken van het cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 2fd74b8d-c006-45c6-a9e2-72ff5d2d978a
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2e028a07c3248205def0789af2c262a0774a8f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="add-custom-hive-libraries-when-creating-your-hdinsight-cluster"></a><span data-ttu-id="e4663-103">Aangepaste Hive-bibliotheken toevoegen bij het maken van uw HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="e4663-103">Add custom Hive libraries when creating your HDInsight cluster</span></span>

<span data-ttu-id="e4663-104">Als er bibliotheken die u vaak met Hive in HDInsight gebruikt, is dit document bevat informatie over het gebruik van een scriptactie toopre load Hallo bibliotheken tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="e4663-104">If you have libraries that you use frequently with Hive on HDInsight, this document contains information on using a Script Action toopre-load hello libraries during cluster creation.</span></span> <span data-ttu-id="e4663-105">Bibliotheken toegevoegd met Hallo stappen in dit document wereldwijd beschikbaar zijn in de Hive - er is geen toouse nodig [JAR toevoegen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload ze.</span><span class="sxs-lookup"><span data-stu-id="e4663-105">Libraries added using hello steps in this document are globally available in Hive - there is no need toouse [ADD JAR](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Cli) tooload them.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="e4663-106">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="e4663-106">How it works</span></span>

<span data-ttu-id="e4663-107">Wanneer u een cluster maakt, kunt u eventueel een scriptactie die een script wordt uitgevoerd op de clusterknooppunten Hallo terwijl ze worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e4663-107">When creating a cluster, you can optionally specify a Script Action that runs a script on hello cluster nodes while they are being created.</span></span> <span data-ttu-id="e4663-108">Hallo-script in dit document accepteert één parameter, die een WASB-locatie met Hallo-bibliotheken (opgeslagen als jar-bestanden) toobe vooraf is geladen.</span><span class="sxs-lookup"><span data-stu-id="e4663-108">hello script in this document accepts a single parameter, which is a WASB location that contains hello libraries (stored as jar files) toobe pre-loaded.</span></span>

<span data-ttu-id="e4663-109">Tijdens het maken van het cluster Hallo script Hallo bestanden inventariseert, kopieert u ze toohello `/usr/lib/customhivelibs/` directory op de knooppunten hoofd- en werkrollen, worden deze vervolgens toegevoegd toohello `hive.aux.jars.path` eigenschap in Hallo `core-site.xml` bestand.</span><span class="sxs-lookup"><span data-stu-id="e4663-109">During cluster creation, hello script enumerates hello files, copies them toohello `/usr/lib/customhivelibs/` directory on head and worker nodes, then adds them toohello `hive.aux.jars.path` property in hello `core-site.xml` file.</span></span> <span data-ttu-id="e4663-110">Op Linux gebaseerde clusters werkt het ook Hallo `hive-env.sh` bestand met de Hallo-locatie van Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="e4663-110">On Linux-based clusters, it also updates hello `hive-env.sh` file with hello location of hello files.</span></span>

> [!NOTE]
> <span data-ttu-id="e4663-111">Met behulp van scriptacties Hallo in dit artikel maakt Hallo bibliotheken beschikbaar zijn in Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="e4663-111">Using hello script actions in this article makes hello libraries available in hello following scenarios:</span></span>
>
> * <span data-ttu-id="e4663-112">**HDInsight op basis van Linux** : wanneer met behulp van een client Hive Hallo **WebHCat**, en **HiveServer2**.</span><span class="sxs-lookup"><span data-stu-id="e4663-112">**Linux-based HDInsight** - when using hello a Hive client, **WebHCat**, and **HiveServer2**.</span></span>
> * <span data-ttu-id="e4663-113">**HDInsight op basis van Windows** : wanneer met behulp van Hallo Hive-client en **WebHCat**.</span><span class="sxs-lookup"><span data-stu-id="e4663-113">**Windows-based HDInsight** - when using hello Hive client and **WebHCat**.</span></span>

## <a name="hello-script"></a><span data-ttu-id="e4663-114">Hallo-script</span><span class="sxs-lookup"><span data-stu-id="e4663-114">hello script</span></span>

<span data-ttu-id="e4663-115">**De locatie van script**</span><span class="sxs-lookup"><span data-stu-id="e4663-115">**Script location**</span></span>

<span data-ttu-id="e4663-116">Voor **op basis van Linux-clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span><span class="sxs-lookup"><span data-stu-id="e4663-116">For **Linux-based clusters**: [https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh)</span></span>

<span data-ttu-id="e4663-117">Voor **Windows gebaseerde clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span><span class="sxs-lookup"><span data-stu-id="e4663-117">For **Windows-based clusters**: [https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1](https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4663-118">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e4663-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e4663-119">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4663-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="e4663-120">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="e4663-120">**Requirements**</span></span>

* <span data-ttu-id="e4663-121">Hallo scripts moet toegepaste tooboth hello **hoofdknooppunten** en **Worker-knooppunten**.</span><span class="sxs-lookup"><span data-stu-id="e4663-121">hello scripts must be applied tooboth hello **Head nodes** and **Worker nodes**.</span></span>

* <span data-ttu-id="e4663-122">Hallo potten die u wenst tooinstall moeten worden opgeslagen in Azure Blob Storage in een **enkele container**.</span><span class="sxs-lookup"><span data-stu-id="e4663-122">hello jars you wish tooinstall must be stored in Azure Blob Storage in a **single container**.</span></span>

* <span data-ttu-id="e4663-123">Hallo Hallo-bibliotheek met jar-bestanden met storage-account **moet** toohello gekoppelde HDInsight-cluster worden tijdens het maken van.</span><span class="sxs-lookup"><span data-stu-id="e4663-123">hello storage account containing hello library of jar files **must** be linked toohello HDInsight cluster during creation.</span></span> <span data-ttu-id="e4663-124">Moet het standaardopslagaccount hello of een account toegevoegd via __optionele configuratie__.</span><span class="sxs-lookup"><span data-stu-id="e4663-124">It must either be hello default storage account, or an account added through __optional configuration__.</span></span>

* <span data-ttu-id="e4663-125">Hallo WASB pad toohello container moet worden opgegeven als een parameter toohello scriptactie.</span><span class="sxs-lookup"><span data-stu-id="e4663-125">hello WASB path toohello container must be specified as a parameter toohello Script Action.</span></span> <span data-ttu-id="e4663-126">Bijvoorbeeld, als hello potten worden opgeslagen in een container met de naam **bibliotheken** op een opslagaccount met de naam **mystorage**, Hallo-parameter zouden worden  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="e4663-126">For example, if hello jars are stored in a container named **libs** on a storage account named **mystorage**, hello parameter would be **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="e4663-127">Dit document wordt ervan uitgegaan dat u hebt al een opslagaccount, blob-container en maken geüploade Hallo bestanden tooit.</span><span class="sxs-lookup"><span data-stu-id="e4663-127">This document assumes that you have already create a storage account, blob container, and uploaded hello files tooit.</span></span>
  >
  > <span data-ttu-id="e4663-128">Als u geen opslagaccount hebt gemaakt, kunt u doen via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e4663-128">If you have not created a storage account, you can do so through hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e4663-129">U kunt vervolgens een hulpprogramma zoals gebruiken [Azure Opslagverkenner](http://storageexplorer.com/) toocreate een container in het Hallo-account en het uploaden van bestanden tooit.</span><span class="sxs-lookup"><span data-stu-id="e4663-129">You can then use a utility such as [Azure Storage Explorer](http://storageexplorer.com/) toocreate a container in hello account and upload files tooit.</span></span>

## <a name="create-a-cluster-using-hello-script"></a><span data-ttu-id="e4663-130">Een cluster met behulp van Hallo script maken</span><span class="sxs-lookup"><span data-stu-id="e4663-130">Create a cluster using hello script</span></span>

> [!NOTE]
> <span data-ttu-id="e4663-131">Hallo stappen te volgen maken een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4663-131">hello following steps create a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e4663-132">selecteert u een cluster op basis van Windows toocreate **Windows** cluster als Hallo OS bij het maken van Hallo-cluster en hello (PowerShell) voor Windows script gebruiken in plaats van Hallo bash-scripts.</span><span class="sxs-lookup"><span data-stu-id="e4663-132">toocreate a Windows-based cluster, select **Windows** as hello cluster OS when creating hello cluster, and use hello Windows (PowerShell) script instead of hello bash script.</span></span>
>
> <span data-ttu-id="e4663-133">U kunt ook Azure PowerShell of Hallo HDInsight .NET SDK toocreate een cluster met behulp van dit script gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e4663-133">You can also use Azure PowerShell or hello HDInsight .NET SDK toocreate a cluster using this script.</span></span> <span data-ttu-id="e4663-134">Zie voor meer informatie over het gebruik van deze methoden [aanpassen HDInsight-clusters met scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e4663-134">For more information on using these methods, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="e4663-135">Start met het inrichten van een cluster met behulp van de stappen in Hallo [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md), maar inrichting niet voltooid.</span><span class="sxs-lookup"><span data-stu-id="e4663-135">Start provisioning a cluster by using hello steps in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md), but do not complete provisioning.</span></span>

2. <span data-ttu-id="e4663-136">Op Hallo **optionele configuratie** blade Selecteer **scriptacties**, en geef Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="e4663-136">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="e4663-137">**NAAM**: Voer een beschrijvende naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4663-137">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="e4663-138">**SCRIPT-URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span><span class="sxs-lookup"><span data-stu-id="e4663-138">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsetupcustomhivelibsv01/setup-customhivelibs-v01.sh</span></span>

   * <span data-ttu-id="e4663-139">**HEAD**: Schakel deze optie.</span><span class="sxs-lookup"><span data-stu-id="e4663-139">**HEAD**: Check this option.</span></span>

   * <span data-ttu-id="e4663-140">**WERKNEMER**: Schakel deze optie.</span><span class="sxs-lookup"><span data-stu-id="e4663-140">**WORKER**: Check this option.</span></span>

   * <span data-ttu-id="e4663-141">**ZOOKEEPER**: leeg laten.</span><span class="sxs-lookup"><span data-stu-id="e4663-141">**ZOOKEEPER**: Leave this blank.</span></span>

   * <span data-ttu-id="e4663-142">**PARAMETERS**: Hallo WASB adres toohello container en storage-account invoeren dat Hallo potten bevat.</span><span class="sxs-lookup"><span data-stu-id="e4663-142">**PARAMETERS**: Enter hello WASB address toohello container and storage account that contains hello jars.</span></span> <span data-ttu-id="e4663-143">Bijvoorbeeld:  **wasb://libs@mystorage.blob.core.windows.net/** .</span><span class="sxs-lookup"><span data-stu-id="e4663-143">For example, **wasb://libs@mystorage.blob.core.windows.net/**.</span></span>

3. <span data-ttu-id="e4663-144">Hallo Hallo onderaan in **scriptacties**, hello gebruiken **Selecteer** knop toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="e4663-144">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span>

4. <span data-ttu-id="e4663-145">Op Hallo **optionele configuratie** blade Selecteer **gekoppelde Storage-Accounts** en selecteer Hallo **van een sleutel opslag** koppeling.</span><span class="sxs-lookup"><span data-stu-id="e4663-145">On hello **Optional Configuration** blade, select **Linked Storage Accounts** and select hello **Add a storage key** link.</span></span> <span data-ttu-id="e4663-146">Selecteer opslagaccount Hallo Hallo potten met en gebruik vervolgens Hallo **Selecteer** knoppen toosave instellingen en return Hallo **optionele configuratie** blade.</span><span class="sxs-lookup"><span data-stu-id="e4663-146">Select hello storage account that contains hello jars, and then use hello **select** buttons toosave settings and return hello **Optional Configuration** blade.</span></span>

5. <span data-ttu-id="e4663-147">Gebruik Hallo **Selecteer** knop onderin Hallo Hallo **optionele configuratie** blade toosave Hallo optionele configuratie-informatie.</span><span class="sxs-lookup"><span data-stu-id="e4663-147">Use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

6. <span data-ttu-id="e4663-148">Doorgaan Hallo cluster inrichten, zoals beschreven in [HDInsight-clusters inrichten op Linux](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="e4663-148">Continue provisioning hello cluster as described in [Provision HDInsight clusters on Linux](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="e4663-149">Zodra het maken van clusters is voltooid, u kunt toouse Hallo potten toegevoegd via dit script uit Hive zonder toouse Hallo worden `ADD JAR` instructie.</span><span class="sxs-lookup"><span data-stu-id="e4663-149">Once cluster creation finishes, you are able toouse hello jars added through this script from Hive without having toouse hello `ADD JAR` statement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4663-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e4663-150">Next steps</span></span>

<span data-ttu-id="e4663-151">Zie voor meer informatie over het werken met Hive [Hive gebruiken met HDInsight](hdinsight-use-hive.md)</span><span class="sxs-lookup"><span data-stu-id="e4663-151">For more information on working with Hive, see [Use Hive with HDInsight](hdinsight-use-hive.md)</span></span>
