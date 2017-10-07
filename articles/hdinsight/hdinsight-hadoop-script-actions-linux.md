---
title: ontwikkeling van een actie met HDInsight op basis van Linux - Azure aaaScript | Microsoft Docs
description: "Meer informatie over hoe toouse Bash scripts toocustomize Linux gebaseerde HDInsight-clusters. Hallo script actie functie van HDInsight kunt u toorun scripts tijdens of na het maken van het cluster. Scripts kunnen worden gebruikt toochange cluster configuratie-instellingen of andere software geïnstalleerd."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a><span data-ttu-id="ae6b9-105">Scripts actie te ontwikkelen met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae6b9-105">Script action development with HDInsight</span></span>

<span data-ttu-id="ae6b9-106">Meer informatie over hoe toocustomize uw HDInsight-cluster met Bash scripts.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-106">Learn how toocustomize your HDInsight cluster using Bash scripts.</span></span> <span data-ttu-id="ae6b9-107">Scriptacties zijn een manier toocustomize HDInsight tijdens of na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-107">Script actions are a way toocustomize HDInsight during or after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae6b9-108">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="ae6b9-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae6b9-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="what-are-script-actions"></a><span data-ttu-id="ae6b9-111">Wat zijn scriptacties</span><span class="sxs-lookup"><span data-stu-id="ae6b9-111">What are script actions</span></span>

<span data-ttu-id="ae6b9-112">Scriptacties Bash-scripts die Azure wordt uitgevoerd op Hallo cluster knooppunten toomake-configuratiewijzigingen zijn of software installeren.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-112">Script actions are Bash scripts that Azure runs on hello cluster nodes toomake configuration changes or install software.</span></span> <span data-ttu-id="ae6b9-113">Een scriptactie wordt uitgevoerd als basis- en biedt volledige toegang rechten toohello clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-113">A script action is executed as root, and provides full access rights toohello cluster nodes.</span></span>

<span data-ttu-id="ae6b9-114">Scriptacties kunnen worden toegepast met de volgende methoden Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-114">Script actions can be applied through hello following methods:</span></span>

| <span data-ttu-id="ae6b9-115">Gebruik deze methode tooapply een script...</span><span class="sxs-lookup"><span data-stu-id="ae6b9-115">Use this method tooapply a script...</span></span> | <span data-ttu-id="ae6b9-116">Tijdens het cluster maken...</span><span class="sxs-lookup"><span data-stu-id="ae6b9-116">During cluster creation...</span></span> | <span data-ttu-id="ae6b9-117">Op een cluster uitgevoerd...</span><span class="sxs-lookup"><span data-stu-id="ae6b9-117">On a running cluster...</span></span> |
| --- |:---:|:---:|
| <span data-ttu-id="ae6b9-118">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae6b9-118">Azure portal</span></span> |<span data-ttu-id="ae6b9-119">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-119">✓</span></span> |<span data-ttu-id="ae6b9-120">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-120">✓</span></span> |
| <span data-ttu-id="ae6b9-121">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae6b9-121">Azure PowerShell</span></span> |<span data-ttu-id="ae6b9-122">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-122">✓</span></span> |<span data-ttu-id="ae6b9-123">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-123">✓</span></span> |
| <span data-ttu-id="ae6b9-124">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ae6b9-124">Azure CLI</span></span> |&nbsp; |<span data-ttu-id="ae6b9-125">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-125">✓</span></span> |
| <span data-ttu-id="ae6b9-126">HDInsight .NET-SDK</span><span class="sxs-lookup"><span data-stu-id="ae6b9-126">HDInsight .NET SDK</span></span> |<span data-ttu-id="ae6b9-127">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-127">✓</span></span> |<span data-ttu-id="ae6b9-128">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-128">✓</span></span> |
| <span data-ttu-id="ae6b9-129">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="ae6b9-129">Azure Resource Manager Template</span></span> |<span data-ttu-id="ae6b9-130">✓</span><span class="sxs-lookup"><span data-stu-id="ae6b9-130">✓</span></span> |&nbsp; |

<span data-ttu-id="ae6b9-131">Zie voor meer informatie over het gebruik van deze methoden tooapply scriptacties [aanpassen HDInsight-clusters met behulp van scriptacties](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-131">For more information on using these methods tooapply script actions, see [Customize HDInsight clusters using script actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="ae6b9-132"><a name="bestPracticeScripting"></a>Aanbevolen procedures voor het ontwikkelen van scripts</span><span class="sxs-lookup"><span data-stu-id="ae6b9-132"><a name="bestPracticeScripting"></a>Best practices for script development</span></span>

<span data-ttu-id="ae6b9-133">Wanneer u een aangepast script voor een HDInsight-cluster ontwikkelt, zijn er enkele aanbevolen procedures tookeep rekening:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-133">When you develop a custom script for an HDInsight cluster, there are several best practices tookeep in mind:</span></span>

* [<span data-ttu-id="ae6b9-134">Doelversie Hallo Hadoop</span><span class="sxs-lookup"><span data-stu-id="ae6b9-134">Target hello Hadoop version</span></span>](#bPS1)
* [<span data-ttu-id="ae6b9-135">Doel Hallo versie van het besturingssysteem</span><span class="sxs-lookup"><span data-stu-id="ae6b9-135">Target hello OS Version</span></span>](#bps10)
* [<span data-ttu-id="ae6b9-136">Geef stabiel koppelingen tooscript resources</span><span class="sxs-lookup"><span data-stu-id="ae6b9-136">Provide stable links tooscript resources</span></span>](#bPS2)
* [<span data-ttu-id="ae6b9-137">Vooraf gecompileerde resources gebruiken</span><span class="sxs-lookup"><span data-stu-id="ae6b9-137">Use pre-compiled resources</span></span>](#bPS4)
* [<span data-ttu-id="ae6b9-138">Zorg ervoor dat Hallo cluster aanpassing script idempotent</span><span class="sxs-lookup"><span data-stu-id="ae6b9-138">Ensure that hello cluster customization script is idempotent</span></span>](#bPS3)
* [<span data-ttu-id="ae6b9-139">Zorg ervoor dat hoge beschikbaarheid van Hallo cluster-architectuur</span><span class="sxs-lookup"><span data-stu-id="ae6b9-139">Ensure high availability of hello cluster architecture</span></span>](#bPS5)
* [<span data-ttu-id="ae6b9-140">Hallo aangepaste onderdelen toouse Azure Blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="ae6b9-140">Configure hello custom components toouse Azure Blob storage</span></span>](#bPS6)
* [<span data-ttu-id="ae6b9-141">Schrijven van gegevens tooSTDOUT en STDERR</span><span class="sxs-lookup"><span data-stu-id="ae6b9-141">Write information tooSTDOUT and STDERR</span></span>](#bPS7)
* [<span data-ttu-id="ae6b9-142">ASCII-bestanden opslaan met regeleinden LF</span><span class="sxs-lookup"><span data-stu-id="ae6b9-142">Save files as ASCII with LF line endings</span></span>](#bps8)
* [<span data-ttu-id="ae6b9-143">Probeer het opnieuw logica toorecover van tijdelijke fouten gebruiken</span><span class="sxs-lookup"><span data-stu-id="ae6b9-143">Use retry logic toorecover from transient errors</span></span>](#bps9)

> [!IMPORTANT]
> <span data-ttu-id="ae6b9-144">Scriptacties moeten worden voltooid binnen 60 minuten of Hallo mislukt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-144">Script actions must complete within 60 minutes or hello process fails.</span></span> <span data-ttu-id="ae6b9-145">Tijdens het inrichten van knooppunt voert Hallo script tegelijk met andere processen installatie en configuratie.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-145">During node provisioning, hello script runs concurrently with other setup and configuration processes.</span></span> <span data-ttu-id="ae6b9-146">Concurrentie voor resources, zoals CPU-tijd of netwerk bandbreedte mogelijk Hallo script tootake langer toofinish dan in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-146">Competition for resources such as CPU time or network bandwidth may cause hello script tootake longer toofinish than it does in your development environment.</span></span>

### <span data-ttu-id="ae6b9-147"><a name="bPS1"></a>Doelversie Hallo Hadoop</span><span class="sxs-lookup"><span data-stu-id="ae6b9-147"><a name="bPS1"></a>Target hello Hadoop version</span></span>

<span data-ttu-id="ae6b9-148">Verschillende versies van HDInsight hebben verschillende versies van Hadoop-services en -onderdelen geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-148">Different versions of HDInsight have different versions of Hadoop services and components installed.</span></span> <span data-ttu-id="ae6b9-149">Als uw script een specifieke versie van een service of het onderdeel verwacht, moet u alleen Hallo script gebruiken met Hallo-versie van HDInsight die Hallo vereiste onderdelen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-149">If your script expects a specific version of a service or component, you should only use hello script with hello version of HDInsight that includes hello required components.</span></span> <span data-ttu-id="ae6b9-150">Vindt u informatie over het onderdeel-versies die zijn opgenomen in HDInsight met behulp van Hallo [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-150">You can find information on component versions included with HDInsight using hello [HDInsight component versioning](hdinsight-component-versioning.md) document.</span></span>

### <span data-ttu-id="ae6b9-151"><a name="bps10"></a>Hallo OS doelversie</span><span class="sxs-lookup"><span data-stu-id="ae6b9-151"><a name="bps10"></a> Target hello OS version</span></span>

<span data-ttu-id="ae6b9-152">Linux gebaseerde HDInsight is gebaseerd op Hallo Ubuntu Linux-distributie.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-152">Linux-based HDInsight is based on hello Ubuntu Linux distribution.</span></span> <span data-ttu-id="ae6b9-153">Verschillende versies van HDInsight, is afhankelijk van verschillende versies van Ubuntu, die de werking van uw script kunnen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-153">Different versions of HDInsight rely on different versions of Ubuntu, which may change how your script behaves.</span></span> <span data-ttu-id="ae6b9-154">Bijvoorbeeld, HDInsight 3,4 en eerder zijn gebaseerd op Ubuntu-versies die Upstart gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-154">For example, HDInsight 3.4 and earlier are based on Ubuntu versions that use Upstart.</span></span> <span data-ttu-id="ae6b9-155">Versie 3.5 is gebaseerd op Ubuntu 16.04 dat gebruikmaakt van Systemd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-155">Version 3.5 is based on Ubuntu 16.04, which uses Systemd.</span></span> <span data-ttu-id="ae6b9-156">Systemd en Upstart zijn afhankelijk van andere opdrachten, zodat uw script toowork met beide moet worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-156">Systemd and Upstart rely on different commands, so your script should be written toowork with both.</span></span>

<span data-ttu-id="ae6b9-157">HDInsight 3.4 en 3.5 nog een belangrijk verschil is dat `JAVA_HOME` tooJava 8 nu verwijst.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-157">Another important difference between HDInsight 3.4 and 3.5 is that `JAVA_HOME` now points tooJava 8.</span></span>

<span data-ttu-id="ae6b9-158">U kunt Hallo OS-versie controleren met behulp van `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-158">You can check hello OS version by using `lsb_release`.</span></span> <span data-ttu-id="ae6b9-159">Hallo volgende code laat zien hoe toodetermine als hello script wordt uitgevoerd op Ubuntu 14 of 16:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-159">hello following code demonstrates how toodetermine if hello script is running on Ubuntu 14 or 16:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

<span data-ttu-id="ae6b9-160">U vindt de volledige Hallo-script dat deze fragmenten op https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh bevat.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-160">You can find hello full script that contains these snippets at https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.</span></span>

<span data-ttu-id="ae6b9-161">Zie voor Hallo-versie van Ubuntu die wordt gebruikt door HDInsight hello [HDInsight componentversie](hdinsight-component-versioning.md) document.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-161">For hello version of Ubuntu that is used by HDInsight, see hello [HDInsight component version](hdinsight-component-versioning.md) document.</span></span>

<span data-ttu-id="ae6b9-162">toounderstand hello verschillen tussen Systemd en Upstart, Zie [Systemd voor Upstart gebruikers](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-162">toounderstand hello differences between Systemd and Upstart, see [Systemd for Upstart users](https://wiki.ubuntu.com/SystemdForUpstartUsers).</span></span>

### <span data-ttu-id="ae6b9-163"><a name="bPS2"></a>Geef stabiel koppelingen tooscript resources</span><span class="sxs-lookup"><span data-stu-id="ae6b9-163"><a name="bPS2"></a>Provide stable links tooscript resources</span></span>

<span data-ttu-id="ae6b9-164">Hallo moeten-script en de bijbehorende resources blijven beschikbaar tijdens de levensduur Hallo van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-164">hello script and associated resources must remain available throughout hello lifetime of hello cluster.</span></span> <span data-ttu-id="ae6b9-165">Deze resources zijn vereist als er nieuwe knooppunten toohello cluster worden toegevoegd tijdens het schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-165">These resources are required if new nodes are added toohello cluster during scaling operations.</span></span>

<span data-ttu-id="ae6b9-166">Hallo aanbevolen procedure is toodownload en archiveren alles in een Azure Storage-account voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-166">hello best practice is toodownload and archive everything in an Azure Storage account on your subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae6b9-167">Hallo storage-account gebruikt moet Hallo storage-standaardaccount voor Hallo cluster of een openbare, alleen-lezen container op andere storage-account.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-167">hello storage account used must be hello default storage account for hello cluster or a public, read-only container on any other storage account.</span></span>

<span data-ttu-id="ae6b9-168">Bijvoorbeeld, Hallo voorbeelden geleverd door Microsoft worden opgeslagen in Hallo [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage-account.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-168">For example, hello samples provided by Microsoft are stored in hello [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) storage account.</span></span> <span data-ttu-id="ae6b9-169">Dit is een openbaar, alleen-lezen container onderhouden door Hallo HDInsight-team.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-169">This is a public, read-only container maintained by hello HDInsight team.</span></span>

### <span data-ttu-id="ae6b9-170"><a name="bPS4"></a>Vooraf gecompileerde resources gebruiken</span><span class="sxs-lookup"><span data-stu-id="ae6b9-170"><a name="bPS4"></a>Use pre-compiled resources</span></span>

<span data-ttu-id="ae6b9-171">tooreduce Hallo tijd het duurt toorun Hallo script, te voorkomen dat de bewerkingen die bronnen van broncode compileren.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-171">tooreduce hello time it takes toorun hello script, avoid operations that compile resources from source code.</span></span> <span data-ttu-id="ae6b9-172">Bijvoorbeeld, vooraf gecompileerd bronnen en op te slaan in een blob van Azure Storage-account in Hallo hetzelfde Datacenter als HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-172">For example, pre-compile resources and store them in an Azure Storage account blob in hello same data center as HDInsight.</span></span>

### <span data-ttu-id="ae6b9-173"><a name="bPS3"></a>Zorg ervoor dat Hallo cluster aanpassing script idempotent</span><span class="sxs-lookup"><span data-stu-id="ae6b9-173"><a name="bPS3"></a>Ensure that hello cluster customization script is idempotent</span></span>

<span data-ttu-id="ae6b9-174">Scripts moet idempotent.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-174">Scripts must be idempotent.</span></span> <span data-ttu-id="ae6b9-175">Als geeft Hallo script meerdere keren wordt uitgevoerd, moet retourneren Hallo cluster toohello gelijk elke keer status.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-175">If hello script runs multiple times, it should return hello cluster toohello same state every time.</span></span>

<span data-ttu-id="ae6b9-176">Bijvoorbeeld dat een script dat wordt gewijzigd van configuratiebestanden geen dubbele vermeldingen moet toevoegen als meerdere keren uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-176">For example, a script that modifies configuration files should not add duplicate entries if ran multiple times.</span></span>

### <span data-ttu-id="ae6b9-177"><a name="bPS5"></a>Zorg ervoor dat hoge beschikbaarheid van Hallo cluster-architectuur</span><span class="sxs-lookup"><span data-stu-id="ae6b9-177"><a name="bPS5"></a>Ensure high availability of hello cluster architecture</span></span>

<span data-ttu-id="ae6b9-178">Linux gebaseerde HDInsight-clusters bieden twee hoofdknooppunten die actief zijn binnen Hallo-cluster, en scriptacties uitgevoerd op beide knooppunten.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-178">Linux-based HDInsight clusters provide two head nodes that are active within hello cluster, and script actions run on both nodes.</span></span> <span data-ttu-id="ae6b9-179">Als Hallo-onderdelen die u installeert slechts één hoofdknooppunt verwacht, Installeer geen Hallo-onderdelen op beide hoofdknooppunten.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-179">If hello components you install expect only one head node, do not install hello components on both head nodes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae6b9-180">Services die worden geleverd als onderdeel van HDInsight zijn ontworpen toofail over tussen de twee hoofdknooppunten Hallo indien nodig.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-180">Services provided as part of HDInsight are designed toofail over between hello two head nodes as needed.</span></span> <span data-ttu-id="ae6b9-181">Deze functionaliteit is niet uitgebreid toocustom onderdelen zijn geïnstalleerd via scriptacties.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-181">This functionality is not extended toocustom components installed through script actions.</span></span> <span data-ttu-id="ae6b9-182">Als u hoge beschikbaarheid voor aangepaste onderdelen nodig hebt, moet u uw eigen mechanisme failover implementeren.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-182">If you need high availability for custom components, you must implement your own failover mechanism.</span></span>

### <span data-ttu-id="ae6b9-183"><a name="bPS6"></a>Hallo aangepaste onderdelen toouse Azure Blob-opslag configureren</span><span class="sxs-lookup"><span data-stu-id="ae6b9-183"><a name="bPS6"></a>Configure hello custom components toouse Azure Blob storage</span></span>

<span data-ttu-id="ae6b9-184">Onderdelen die u op Hallo cluster installeert wellicht een standaardconfiguratie waarmee Hadoop Distributed File System (HDFS) opslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-184">Components that you install on hello cluster might have a default configuration that uses Hadoop Distributed File System (HDFS) storage.</span></span> <span data-ttu-id="ae6b9-185">HDInsight gebruikt Azure Storage of de Data Lake Store als Hallo standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-185">HDInsight uses either Azure Storage or Data Lake Store as hello default storage.</span></span> <span data-ttu-id="ae6b9-186">Beide bieden een HDFS-compatibel bestandssysteem dat gegevens behouden blijft zelfs als het Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-186">Both provide an HDFS compatible file system that persists data even if hello cluster is deleted.</span></span> <span data-ttu-id="ae6b9-187">Mogelijk moet u tooconfigure onderdelen die u installeert toouse WASB of ADL in plaats van HDFS.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-187">You may need tooconfigure components you install toouse WASB or ADL instead of HDFS.</span></span>

<span data-ttu-id="ae6b9-188">Voor de meeste bewerkingen hoeft u geen toospecify Hallo-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-188">For most operations, you do not need toospecify hello file system.</span></span> <span data-ttu-id="ae6b9-189">Hallo volgende wordt bijvoorbeeld Hallo giraph examples.jar-bestand van Hallo lokale systeem toocluster bestandsopslag gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-189">For example, hello following copies hello giraph-examples.jar file from hello local file system toocluster storage:</span></span>

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

<span data-ttu-id="ae6b9-190">In dit voorbeeld Hallo `hdfs` opdracht transparant Hallo standaard clusteropslag gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-190">In this example, hello `hdfs` command transparently uses hello default cluster storage.</span></span> <span data-ttu-id="ae6b9-191">Voor bepaalde bewerkingen moet u toospecify Hallo URI.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-191">For some operations, you may need toospecify hello URI.</span></span> <span data-ttu-id="ae6b9-192">Bijvoorbeeld: `adl:///example/jars` voor Data Lake Store of `wasb:///example/jars` voor Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-192">For example, `adl:///example/jars` for Data Lake Store or `wasb:///example/jars` for Azure Storage.</span></span>

### <span data-ttu-id="ae6b9-193"><a name="bPS7"></a>Schrijven van gegevens tooSTDOUT en STDERR</span><span class="sxs-lookup"><span data-stu-id="ae6b9-193"><a name="bPS7"></a>Write information tooSTDOUT and STDERR</span></span>

<span data-ttu-id="ae6b9-194">HDInsight uitvoer van het script dat is geschreven tooSTDOUT en STDERR registreert.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-194">HDInsight logs script output that is written tooSTDOUT and STDERR.</span></span> <span data-ttu-id="ae6b9-195">U kunt deze gegevens door middel van Hallo Ambari-webgebruikersinterface weergeven.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-195">You can view this information using hello Ambari web UI.</span></span>

> [!NOTE]
> <span data-ttu-id="ae6b9-196">Ambari is alleen beschikbaar als het Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-196">Ambari is only available if hello cluster is successfully created.</span></span> <span data-ttu-id="ae6b9-197">Als u een scriptactie tijdens het maken van het cluster en mislukt het maken, Zie sectie troubleshooting Hallo [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) voor andere manieren van de toegang tot geregistreerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-197">If you use a script action during cluster creation, and creation fails, see hello troubleshooting section [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) for other ways of accessing logged information.</span></span>

<span data-ttu-id="ae6b9-198">De meeste hulpprogramma's en installatiepakketten schrijven al informatie tooSTDOUT en STDERR, maar u aanvullende logboekregistratie tooadd kunt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-198">Most utilities and installation packages already write information tooSTDOUT and STDERR, however you may want tooadd additional logging.</span></span> <span data-ttu-id="ae6b9-199">toosend tekst tooSTDOUT, gebruik `echo`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-199">toosend text tooSTDOUT, use `echo`.</span></span> <span data-ttu-id="ae6b9-200">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-200">For example:</span></span>

```bash
echo "Getting ready tooinstall Foo"
```

<span data-ttu-id="ae6b9-201">Standaard `echo` verzendt Hallo tooSTDOUT tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-201">By default, `echo` sends hello string tooSTDOUT.</span></span> <span data-ttu-id="ae6b9-202">toodirect het tooSTDERR, Voeg `>&2` voordat `echo`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-202">toodirect it tooSTDERR, add `>&2` before `echo`.</span></span> <span data-ttu-id="ae6b9-203">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-203">For example:</span></span>

```bash
>&2 echo "An error occurred installing Foo"
```

<span data-ttu-id="ae6b9-204">Dit leidt informatie tooSTDOUT tooSTDERR (2) in plaats daarvan wordt geschreven.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-204">This redirects information written tooSTDOUT tooSTDERR (2) instead.</span></span> <span data-ttu-id="ae6b9-205">Zie voor meer informatie over i/o-omleiding [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-205">For more information on IO redirection, see [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).</span></span>

<span data-ttu-id="ae6b9-206">Zie voor meer informatie over het weergeven van informatie die wordt geregistreerd door scriptacties [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span><span class="sxs-lookup"><span data-stu-id="ae6b9-206">For more information on viewing information logged by script actions, see [Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)</span></span>

### <span data-ttu-id="ae6b9-207"><a name="bps8"></a>ASCII-bestanden opslaan met regeleinden LF</span><span class="sxs-lookup"><span data-stu-id="ae6b9-207"><a name="bps8"></a> Save files as ASCII with LF line endings</span></span>

<span data-ttu-id="ae6b9-208">Bash-scripts moeten worden opgeslagen als ASCII-indeling met regels die door LF is beëindigd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-208">Bash scripts should be stored as ASCII format, with lines terminated by LF.</span></span> <span data-ttu-id="ae6b9-209">Bestanden die worden opgeslagen als UTF-8 of CRLF gebruiken als Hallo regel beëindigen kunnen mislukken met de volgende fout Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-209">Files that are stored as UTF-8, or use CRLF as hello line ending may fail with hello following error:</span></span>

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <span data-ttu-id="ae6b9-210"><a name="bps9"></a>Probeer het opnieuw logica toorecover van tijdelijke fouten gebruiken</span><span class="sxs-lookup"><span data-stu-id="ae6b9-210"><a name="bps9"></a> Use retry logic toorecover from transient errors</span></span>

<span data-ttu-id="ae6b9-211">Bij het downloaden van bestanden met apt get- of andere acties die verzenden van gegevens over pakketten installeren Hallo van internet, Hallo-actie kan mislukken omdat tootransient netwerkfouten.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-211">When downloading files, installing packages using apt-get, or other actions that transmit data over hello internet, hello action may fail due tootransient networking errors.</span></span> <span data-ttu-id="ae6b9-212">Bijvoorbeeld, Hallo externe resource die u communiceert mogelijk Hallo-proces mislukt over tooa back-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-212">For example, hello remote resource you are communicating with may be in hello process of failing over tooa backup node.</span></span>

<span data-ttu-id="ae6b9-213">toomake uw robuuste tootransient scriptfouten u Pogingslogica kunt implementeren.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-213">toomake your script resilient tootransient errors, you can implement retry logic.</span></span> <span data-ttu-id="ae6b9-214">Hallo volgen functie laat zien hoe tooimplement Pogingslogica.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-214">hello following function demonstrates how tooimplement retry logic.</span></span> <span data-ttu-id="ae6b9-215">Het opnieuw probeert Hallo bewerking driemaal voordat deze is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-215">It retries hello operation three times before failing.</span></span>

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

<span data-ttu-id="ae6b9-216">Hallo volgende voorbeelden laten zien hoe toouse deze functie.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-216">hello following examples demonstrate how toouse this function.</span></span>

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <span data-ttu-id="ae6b9-217"><a name="helpermethods"></a>Help-methoden voor aangepaste scripts</span><span class="sxs-lookup"><span data-stu-id="ae6b9-217"><a name="helpermethods"></a>Helper methods for custom scripts</span></span>

<span data-ttu-id="ae6b9-218">Script actie Help-methoden zijn hulpprogramma's die u gebruiken kunt bij het schrijven van aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-218">Script action helper methods are utilities that you can use while writing custom scripts.</span></span> <span data-ttu-id="ae6b9-219">Deze methoden zijn opgenomen in de[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-219">These methods are contained in the[https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh) script.</span></span> <span data-ttu-id="ae6b9-220">Gebruik Hallo toodownload te volgen en ze als onderdeel van uw script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-220">Use hello following toodownload and use them as part of your script:</span></span>

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

<span data-ttu-id="ae6b9-221">Hallo helpers beschikbaar voor gebruik in uw script te volgen:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-221">hello following helpers available for use in your script:</span></span>

| <span data-ttu-id="ae6b9-222">Gebruik helper</span><span class="sxs-lookup"><span data-stu-id="ae6b9-222">Helper usage</span></span> | <span data-ttu-id="ae6b9-223">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ae6b9-223">Description</span></span> |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |<span data-ttu-id="ae6b9-224">Een bestand wordt gedownload van Hallo URI toohello opgegeven bronbestandspad.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-224">Downloads a file from hello source URI toohello specified file path.</span></span> <span data-ttu-id="ae6b9-225">Standaard wordt er een bestaand bestand niet overschreven.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-225">By default, it does not overwrite an existing file.</span></span> |
| `untar_file TARFILE DESTDIR` |<span data-ttu-id="ae6b9-226">Extraheert een tar-bestand (met behulp van `-xf`) toohello doelmap.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-226">Extracts a tar file (using `-xf`) toohello destination directory.</span></span> |
| `test_is_headnode` |<span data-ttu-id="ae6b9-227">Indien uitgevoerd op een cluster hoofdknooppunt, return 1; anders wordt 0.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-227">If ran on a cluster head node, return 1; otherwise, 0.</span></span> |
| `test_is_datanode` |<span data-ttu-id="ae6b9-228">Als het huidige knooppunt Hallo gegevensknooppunt (worker) is, retourneert een 1; anders wordt 0.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-228">If hello current node is a data (worker) node, return a 1; otherwise, 0.</span></span> |
| `test_is_first_datanode` |<span data-ttu-id="ae6b9-229">Als het huidige knooppunt Hallo Hallo eerste gegevens (worker) knooppunt (benoemde workernode0) retourneren een 1; anders wordt 0.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-229">If hello current node is hello first data (worker) node (named workernode0) return a 1; otherwise, 0.</span></span> |
| `get_headnodes` |<span data-ttu-id="ae6b9-230">Hallo volledig gekwalificeerde domeinnaam van Hallo headnodes in Hallo cluster retourneren.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-230">Return hello fully qualified domain name of hello headnodes in hello cluster.</span></span> <span data-ttu-id="ae6b9-231">De namen zijn gescheiden door komma's.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-231">Names are comma delimited.</span></span> <span data-ttu-id="ae6b9-232">Een lege tekenreeks geretourneerd bij fout.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-232">An empty string is returned on error.</span></span> |
| `get_primary_headnode` |<span data-ttu-id="ae6b9-233">Hallo volledig gekwalificeerde domeinnaam van de primaire headnode Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-233">Gets hello fully qualified domain name of hello primary headnode.</span></span> <span data-ttu-id="ae6b9-234">Een lege tekenreeks geretourneerd bij fout.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-234">An empty string is returned on error.</span></span> |
| `get_secondary_headnode` |<span data-ttu-id="ae6b9-235">Hallo volledig gekwalificeerde domeinnaam van de secundaire headnode Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-235">Gets hello fully qualified domain name of hello secondary headnode.</span></span> <span data-ttu-id="ae6b9-236">Een lege tekenreeks geretourneerd bij fout.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-236">An empty string is returned on error.</span></span> |
| `get_primary_headnode_number` |<span data-ttu-id="ae6b9-237">Hallo numeriek achtervoegsel van primaire headnode Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-237">Gets hello numeric suffix of hello primary headnode.</span></span> <span data-ttu-id="ae6b9-238">Een lege tekenreeks geretourneerd bij fout.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-238">An empty string is returned on error.</span></span> |
| `get_secondary_headnode_number` |<span data-ttu-id="ae6b9-239">Hallo numeriek achtervoegsel van de secundaire headnode Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-239">Gets hello numeric suffix of hello secondary headnode.</span></span> <span data-ttu-id="ae6b9-240">Een lege tekenreeks geretourneerd bij fout.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-240">An empty string is returned on error.</span></span> |

## <span data-ttu-id="ae6b9-241"><a name="commonusage"></a>Algemene gebruikspatronen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-241"><a name="commonusage"></a>Common usage patterns</span></span>

<span data-ttu-id="ae6b9-242">Deze sectie bevat richtlijnen over het implementeren van een aantal Hallo algemene gebruikspatronen die u tegenkomen kunt tijdens het schrijven van uw eigen aangepaste scripts.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-242">This section provides guidance on implementing some of hello common usage patterns that you might run into while writing your own custom script.</span></span>

### <a name="passing-parameters-tooa-script"></a><span data-ttu-id="ae6b9-243">Parameters doorgeven tooa script</span><span class="sxs-lookup"><span data-stu-id="ae6b9-243">Passing parameters tooa script</span></span>

<span data-ttu-id="ae6b9-244">In sommige gevallen kan het script parameters vereist.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-244">In some cases, your script may require parameters.</span></span> <span data-ttu-id="ae6b9-245">Bijvoorbeeld, moet u mogelijk Hallo beheerderswachtwoord voor Hallo cluster bij gebruik van Hallo Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-245">For example, you may need hello admin password for hello cluster when using hello Ambari REST API.</span></span>

<span data-ttu-id="ae6b9-246">Toohello script doorgegeven parameters worden aangeduid als *positieparameters*, en te worden toegewezen`$1` voor de eerste parameter Hallo `$2` voor Hallo tweede en dus eenmalige aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-246">Parameters passed toohello script are known as *positional parameters*, and are assigned too`$1` for hello first parameter, `$2` for hello second, and so-on.</span></span> <span data-ttu-id="ae6b9-247">`$0`bevat de naam Hallo van Hallo script zelf.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-247">`$0` contains hello name of hello script itself.</span></span>

<span data-ttu-id="ae6b9-248">Toohello script als parameters doorgegeven waarden moeten tussen enkele aanhalingstekens (').</span><span class="sxs-lookup"><span data-stu-id="ae6b9-248">Values passed toohello script as parameters should be enclosed by single quotes (').</span></span> <span data-ttu-id="ae6b9-249">Hiermee zorgt u ervoor dat Hallo doorgegeven waarde wordt behandeld als een letterlijke waarde.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-249">Doing so ensures that hello passed value is treated as a literal.</span></span>

### <a name="setting-environment-variables"></a><span data-ttu-id="ae6b9-250">Omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-250">Setting environment variables</span></span>

<span data-ttu-id="ae6b9-251">Instellen van een omgevingsvariabele wordt uitgevoerd door de volgende instructie Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-251">Setting an environment variable is performed by hello following statement:</span></span>

    VARIABLENAME=value

<span data-ttu-id="ae6b9-252">Waarbij VARIABELENAAM Hallo-naam van Hallo variabele is.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-252">Where VARIABLENAME is hello name of hello variable.</span></span> <span data-ttu-id="ae6b9-253">tooaccess Hallo-variabele, gebruik `$VARIABLENAME`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-253">tooaccess hello variable, use `$VARIABLENAME`.</span></span> <span data-ttu-id="ae6b9-254">Bijvoorbeeld tooassign een waarde die door een positionele parameter als een omgevingsvariabele met de naam wachtwoord, gebruikt u Hallo-instructie:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-254">For example, tooassign a value provided by a positional parameter as an environment variable named PASSWORD, you would use hello following statement:</span></span>

    PASSWORD=$1

<span data-ttu-id="ae6b9-255">Daaropvolgende toegang toohello informatie kunt vervolgens `$PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-255">Subsequent access toohello information could then use `$PASSWORD`.</span></span>

<span data-ttu-id="ae6b9-256">Omgevingsvariabelen ingesteld binnen Hallo script bestaan alleen binnen bereik Hallo van Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-256">Environment variables set within hello script only exist within hello scope of hello script.</span></span> <span data-ttu-id="ae6b9-257">In sommige gevallen moet u tooadd hele systeem omgevingsvariabelen die blijft van kracht nadat Hallo-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-257">In some cases, you may need tooadd system-wide environment variables that will persist after hello script has finished.</span></span> <span data-ttu-id="ae6b9-258">het hele systeem omgevingsvariabelen tooadd, Hallo variabele te toevoegen`/etc/environment`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-258">tooadd system-wide environment variables, add hello variable too`/etc/environment`.</span></span> <span data-ttu-id="ae6b9-259">Hallo-instructie wordt bijvoorbeeld toegevoegd `HADOOP_CONF_DIR`:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-259">For example, hello following statement adds `HADOOP_CONF_DIR`:</span></span>

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a><span data-ttu-id="ae6b9-260">Toegang tot toolocations waar Hallo aangepaste scripts worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-260">Access toolocations where hello custom scripts are stored</span></span>

<span data-ttu-id="ae6b9-261">Scripts die worden gebruikt toocustomize een cluster moet toobe opgeslagen in een van de volgende locaties Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-261">Scripts used toocustomize a cluster needs toobe stored in one of hello following locations:</span></span>

* <span data-ttu-id="ae6b9-262">Een __Azure Storage-account__ dat is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-262">An __Azure Storage account__ that is associated with hello cluster.</span></span>

* <span data-ttu-id="ae6b9-263">Een __extra opslagaccount__ die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-263">An __additional storage account__ associated with hello cluster.</span></span>

* <span data-ttu-id="ae6b9-264">Een __openbaar leesbaar URI__.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-264">A __publicly readable URI__.</span></span> <span data-ttu-id="ae6b9-265">Bijvoorbeeld, een URL toodata opgeslagen op OneDrive, Dropbox of andere hostingservice bestand.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-265">For example, a URL toodata stored on OneDrive, Dropbox, or other file hosting service.</span></span>

* <span data-ttu-id="ae6b9-266">Een __Azure Data Lake Store-account__ dat is gekoppeld aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-266">An __Azure Data Lake Store account__ that is associated with hello HDInsight cluster.</span></span> <span data-ttu-id="ae6b9-267">Zie voor meer informatie over het gebruik van Azure Data Lake Store met HDInsight [een HDInsight-cluster maken met Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-267">For more information on using Azure Data Lake Store with HDInsight, see [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="ae6b9-268">Hallo service principal HDInsight maakt gebruik van tooaccess Data Lake Store moet leestoegang toohello script hebben.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-268">hello service principal HDInsight uses tooaccess Data Lake Store must have read access toohello script.</span></span>

<span data-ttu-id="ae6b9-269">Resources die worden gebruikt door Hallo script moeten ook openbaar beschikbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-269">Resources used by hello script must also be publicly available.</span></span>

<span data-ttu-id="ae6b9-270">Hallo-bestanden opslaan in een Azure Storage-account of een Azure Data Lake Store biedt snel toegang, als beide binnen hello Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-270">Storing hello files in an Azure Storage account or Azure Data Lake Store provides fast access, as both within hello Azure network.</span></span>

> [!NOTE]
> <span data-ttu-id="ae6b9-271">Hallo URI-indeling gebruikt tooreference Hallo script is afhankelijk van Hallo-service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-271">hello URI format used tooreference hello script differs depending on hello service being used.</span></span> <span data-ttu-id="ae6b9-272">Gebruik voor storage-accounts die zijn gekoppeld aan de HDInsight-cluster Hallo `wasb://` of `wasbs://`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-272">For storage accounts associated with hello HDInsight cluster, use `wasb://` or `wasbs://`.</span></span> <span data-ttu-id="ae6b9-273">Gebruik voor openbaar leesbaar URI `http://` of `https://`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-273">For publicly readable URIs, use `http://` or `https://`.</span></span> <span data-ttu-id="ae6b9-274">Gebruik voor Data Lake Store `adl://`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-274">For Data Lake Store, use `adl://`.</span></span>

### <a name="checking-hello-operating-system-version"></a><span data-ttu-id="ae6b9-275">Hallo-besturingssysteemversie controleren</span><span class="sxs-lookup"><span data-stu-id="ae6b9-275">Checking hello operating system version</span></span>

<span data-ttu-id="ae6b9-276">Verschillende versies van HDInsight, is afhankelijk van specifieke versies van Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-276">Different versions of HDInsight rely on specific versions of Ubuntu.</span></span> <span data-ttu-id="ae6b9-277">Mogelijk zijn er verschillen tussen versies van het besturingssysteem die u in uw script controleren moet.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-277">There may be differences between OS versions that you must check for in your script.</span></span> <span data-ttu-id="ae6b9-278">U moet mogelijk een binair bestand dat is gebonden toohello versie van Ubuntu tooinstall.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-278">For example, you may need tooinstall a binary that is tied toohello version of Ubuntu.</span></span>

<span data-ttu-id="ae6b9-279">toocheck hello OS-versie, gebruik `lsb_release`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-279">toocheck hello OS version, use `lsb_release`.</span></span> <span data-ttu-id="ae6b9-280">Bijvoorbeeld toont Hallo volgende script hoe tooreference een specifieke tar-bestand, afhankelijk van de versie van het besturingssysteem Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-280">For example, hello following script demonstrates how tooreference a specific tar file depending on hello OS version:</span></span>

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <span data-ttu-id="ae6b9-281"><a name="deployScript"></a>Controlelijst voor het implementeren van een scriptactie</span><span class="sxs-lookup"><span data-stu-id="ae6b9-281"><a name="deployScript"></a>Checklist for deploying a script action</span></span>

<span data-ttu-id="ae6b9-282">Hier volgen Hallo stappen werd bij het voorbereiden van toodeploy deze scripts:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-282">Here are hello steps we took when preparing toodeploy these scripts:</span></span>

* <span data-ttu-id="ae6b9-283">Hallo-bestanden met aangepaste scripts op een locatie die toegankelijk is voor de clusterknooppunten Hallo tijdens de implementatie van Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-283">Put hello files that contain hello custom scripts in a place that is accessible by hello cluster nodes during deployment.</span></span> <span data-ttu-id="ae6b9-284">Bijvoorbeeld, Hallo standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-284">For example, hello default storage for hello cluster.</span></span> <span data-ttu-id="ae6b9-285">Bestanden kunnen ook worden opgeslagen in openbaar leesbaar hosting-services.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-285">Files can also be stored in publicly readable hosting services.</span></span>
* <span data-ttu-id="ae6b9-286">Controleer of Hallo script impotent.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-286">Verify that hello script is impotent.</span></span> <span data-ttu-id="ae6b9-287">Hierdoor kunnen de Hallo script toobe uitgevoerd meerdere keren op Hallo hetzelfde knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-287">Doing so allows hello script toobe executed multiple times on hello same node.</span></span>
* <span data-ttu-id="ae6b9-288">Gebruik een tijdelijk bestand directory map tookeep Hallo gedownloade bestanden gebruikt door Hallo scripts en vervolgens opschonen van nadat scripts hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-288">Use a temporary file directory /tmp tookeep hello downloaded files used by hello scripts and then clean them up after scripts have executed.</span></span>
* <span data-ttu-id="ae6b9-289">Als de OS-niveau instellingen of configuratiebestanden voor Hadoop-service zijn gewijzigd, kunt u toorestart HDInsight services.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-289">If OS-level settings or Hadoop service configuration files are changed, you may want toorestart HDInsight services.</span></span>

## <span data-ttu-id="ae6b9-290"><a name="runScriptAction"></a>Hoe een scriptactie toorun</span><span class="sxs-lookup"><span data-stu-id="ae6b9-290"><a name="runScriptAction"></a>How toorun a script action</span></span>

<span data-ttu-id="ae6b9-291">U kunt script acties toocustomize HDInsight-clusters met behulp van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-291">You can use script actions toocustomize HDInsight clusters using hello following methods:</span></span>

* <span data-ttu-id="ae6b9-292">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="ae6b9-292">Azure portal</span></span>
* <span data-ttu-id="ae6b9-293">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae6b9-293">Azure PowerShell</span></span>
* <span data-ttu-id="ae6b9-294">Azure Resource Manager-sjablonen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-294">Azure Resource Manager templates</span></span>
* <span data-ttu-id="ae6b9-295">Hello HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-295">hello HDInsight .NET SDK.</span></span>

<span data-ttu-id="ae6b9-296">Zie voor meer informatie over het gebruik van elke methode [hoe toouse actie script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-296">For more information on using each method, see [How toouse script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <span data-ttu-id="ae6b9-297"><a name="sampleScripts"></a>Aangepast script-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="ae6b9-297"><a name="sampleScripts"></a>Custom script samples</span></span>

<span data-ttu-id="ae6b9-298">Microsoft biedt voorbeeldscripts tooinstall onderdelen op een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-298">Microsoft provides sample scripts tooinstall components on an HDInsight cluster.</span></span> <span data-ttu-id="ae6b9-299">Zie de volgende koppelingen voor meer voorbeeld scriptacties Hallo.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-299">See hello following links for more example script actions.</span></span>

* [<span data-ttu-id="ae6b9-300">Installeren en gebruiken van Hue op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ae6b9-300">Install and use Hue on HDInsight clusters</span></span>](hdinsight-hadoop-hue-linux.md)
* [<span data-ttu-id="ae6b9-301">Installeren en gebruiken van Solr op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ae6b9-301">Install and use Solr on HDInsight clusters</span></span>](hdinsight-hadoop-solr-install-linux.md)
* [<span data-ttu-id="ae6b9-302">Installeren en gebruiken van Giraph op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ae6b9-302">Install and use Giraph on HDInsight clusters</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* [<span data-ttu-id="ae6b9-303">Installeren of upgraden van Mono op HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="ae6b9-303">Install or upgrade Mono on HDInsight clusters</span></span>](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a><span data-ttu-id="ae6b9-304">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-304">Troubleshooting</span></span>

<span data-ttu-id="ae6b9-305">Hallo volgen fouten die optreden kunnen wanneer met behulp van scripts die u hebt ontwikkeld:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-305">hello following are errors you may encounter when using scripts you have developed:</span></span>

<span data-ttu-id="ae6b9-306">**Fout**: `$'\r': command not found`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-306">**Error**: `$'\r': command not found`.</span></span> <span data-ttu-id="ae6b9-307">Soms gevolgd door `syntax error: unexpected end of file`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-307">Sometimes followed by `syntax error: unexpected end of file`.</span></span>

<span data-ttu-id="ae6b9-308">*Oorzaak*: deze fout wordt veroorzaakt wanneer Hallo regels in een script met CRLF eindigen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-308">*Cause*: This error is caused when hello lines in a script end with CRLF.</span></span> <span data-ttu-id="ae6b9-309">UNIX-systemen verwacht alleen LF als Hallo regel beëindigen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-309">Unix systems expect only LF as hello line ending.</span></span>

<span data-ttu-id="ae6b9-310">Dit probleem treedt meestal wanneer het Hallo-script is gemaakt op een Windows-omgeving CRLF is een algemene regel die eindigt voor veel teksteditors op Windows.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-310">This problem most often occurs when hello script is authored on a Windows environment, as CRLF is a common line ending for many text editors on Windows.</span></span>

<span data-ttu-id="ae6b9-311">*Resolutie*: als het is een optie in een teksteditor, selecteert u Unix-indeling of LF voor Hallo regel beëindigen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-311">*Resolution*: If it is an option in your text editor, select Unix format or LF for hello line ending.</span></span> <span data-ttu-id="ae6b9-312">U kunt ook de volgende opdrachten op een Unix-systeem toochange Hallo CRLF tooan LF Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-312">You may also use hello following commands on a Unix system toochange hello CRLF tooan LF:</span></span>

> [!NOTE]
> <span data-ttu-id="ae6b9-313">Hallo zijn volgende opdrachten grofweg gelijk Hallo CRLF regel uitgangen tooLF moet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-313">hello following commands are roughly equivalent in that they should change hello CRLF line endings tooLF.</span></span> <span data-ttu-id="ae6b9-314">Selecteer een op basis van Hallo hulpprogramma's beschikbaar zijn op uw systeem.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-314">Select one based on hello utilities available on your system.</span></span>

| <span data-ttu-id="ae6b9-315">Opdracht</span><span class="sxs-lookup"><span data-stu-id="ae6b9-315">Command</span></span> | <span data-ttu-id="ae6b9-316">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-316">Notes</span></span> |
| --- | --- |
| `unix2dos -b INFILE` |<span data-ttu-id="ae6b9-317">het oorspronkelijke bestand Hallo back-up met een. De extensie BAK</span><span class="sxs-lookup"><span data-stu-id="ae6b9-317">hello original file is backed up with a .BAK extension</span></span> |
| `tr -d '\r' < INFILE > OUTFILE` |<span data-ttu-id="ae6b9-318">UITVOERBESTAND bevat een versie met alleen LF uitgangen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-318">OUTFILE contains a version with only LF endings</span></span> |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | <span data-ttu-id="ae6b9-319">Hallo-bestand wijzigt rechtstreeks</span><span class="sxs-lookup"><span data-stu-id="ae6b9-319">Modifies hello file directly</span></span> |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |<span data-ttu-id="ae6b9-320">UITVOERBESTAND bevat een versie met alleen LF uitgangen.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-320">OUTFILE contains a version with only LF endings.</span></span> |

<span data-ttu-id="ae6b9-321">**Fout**: `line 1: #!/usr/bin/env: No such file or directory`.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-321">**Error**: `line 1: #!/usr/bin/env: No such file or directory`.</span></span>

<span data-ttu-id="ae6b9-322">*Oorzaak*: deze fout treedt op wanneer hello script is opgeslagen als UTF-8 met een Byte Order Mark (BOM).</span><span class="sxs-lookup"><span data-stu-id="ae6b9-322">*Cause*: This error occurs when hello script was saved as UTF-8 with a Byte Order Mark (BOM).</span></span>

<span data-ttu-id="ae6b9-323">*Resolutie*: opgeslagen Hallo-bestand als ASCII of als UTF-8 zonder een stuklijst.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-323">*Resolution*: Save hello file either as ASCII, or as UTF-8 without a BOM.</span></span> <span data-ttu-id="ae6b9-324">U kunt ook de opdracht volgen op een Linux- of Unix-systeem toocreate een bestand zonder Hallo BOM Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae6b9-324">You may also use hello following command on a Linux or Unix system toocreate a file without hello BOM:</span></span>

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

<span data-ttu-id="ae6b9-325">Vervang `INFILE` met Hallo-bestand waarin Hallo stuklijst.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-325">Replace `INFILE` with hello file containing hello BOM.</span></span> <span data-ttu-id="ae6b9-326">`OUTFILE`moet u een nieuwe bestandsnaam die Hallo script zonder Hallo BOM bevat.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-326">`OUTFILE` should be a new file name, which contains hello script without hello BOM.</span></span>

## <span data-ttu-id="ae6b9-327"><a name="seeAlso"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae6b9-327"><a name="seeAlso"></a>Next steps</span></span>

* <span data-ttu-id="ae6b9-328">Meer informatie over hoe te[aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="ae6b9-328">Learn how too[Customize HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>
* <span data-ttu-id="ae6b9-329">Gebruik Hallo [HDInsight .NET SDK-naslaginformatie](https://msdn.microsoft.com/library/mt271028.aspx) toolearn meer over het maken van .NET-toepassingen die HDInsight beheren</span><span class="sxs-lookup"><span data-stu-id="ae6b9-329">Use hello [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx) toolearn more about creating .NET applications that manage HDInsight</span></span>
* <span data-ttu-id="ae6b9-330">Gebruik Hallo [HDInsight REST-API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn hoe toouse REST tooperform acties op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ae6b9-330">Use hello [HDInsight REST API](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn how toouse REST tooperform management actions on HDInsight clusters.</span></span>
