---
title: aaaInstall of Mono op HDInsight - Azure bijwerken | Microsoft Docs
description: Meer informatie over hoe toouse een specifieke versie van Mono met HDInsight-cluster. Mono is gebruikte toorun .NET-toepassingen op Linux gebaseerde HDInsight-clusters.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: hdinsightactive
ms.openlocfilehash: 1e8a8aaeff231c93a9e232379448517b326da965
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="56b65-104">Installeren of bijwerken van Mono in HDInsight</span><span class="sxs-lookup"><span data-stu-id="56b65-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="56b65-105">Meer informatie over hoe tooinstall een specifieke versie van [Mono](https://www.mono-project.com) op HDInsight 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="56b65-105">Learn how tooinstall a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="56b65-106">Mono op HDInsight 3.4 en hoger is geïnstalleerd en is gebruikte toorun .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="56b65-106">Mono is installed on HDInsight 3.4 and higher, and is used toorun .NET applications.</span></span> <span data-ttu-id="56b65-107">Zie voor informatie over het Hallo-versie van Mono opgenomen in elke versie van HDInsight, [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="56b65-107">For information on hello version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="56b65-108">tooinstall een andere versie op het cluster, gebruik Hallo scriptactie in dit document.</span><span class="sxs-lookup"><span data-stu-id="56b65-108">tooinstall a different version on your cluster, use hello script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="56b65-109">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="56b65-109">How it works</span></span>

<span data-ttu-id="56b65-110">Dit script accepteert Hallo parameter te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b65-110">This script accepts hello following parameter:</span></span>

* <span data-ttu-id="56b65-111">__Mono versienummer__: Hallo-versie van Mono tooinstall.</span><span class="sxs-lookup"><span data-stu-id="56b65-111">__Mono version number__: hello version of Mono tooinstall.</span></span> <span data-ttu-id="56b65-112">Hallo-versie moet beschikbaar zijn vanuit [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="56b65-112">hello version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="56b65-113">Hallo script installeert Hallo Mono-pakketten te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b65-113">hello script installs hello following Mono packages:</span></span>

* <span data-ttu-id="56b65-114">__Mono-voltooid__</span><span class="sxs-lookup"><span data-stu-id="56b65-114">__mono-complete__</span></span>

* <span data-ttu-id="56b65-115">__CA-certificaten-mono__</span><span class="sxs-lookup"><span data-stu-id="56b65-115">__ca-certificates-mono__</span></span>

## <a name="hello-script"></a><span data-ttu-id="56b65-116">Hallo-script</span><span class="sxs-lookup"><span data-stu-id="56b65-116">hello script</span></span>

<span data-ttu-id="56b65-117">__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="56b65-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="56b65-118">__Vereisten__:</span><span class="sxs-lookup"><span data-stu-id="56b65-118">__Requirements__:</span></span>

* <span data-ttu-id="56b65-119">Hallo script moet worden toegepast op Hallo __hoofdknooppunten__ en __worker-knooppunten__.</span><span class="sxs-lookup"><span data-stu-id="56b65-119">hello script must be applied on hello __head nodes__ and __worker nodes__.</span></span>

## <a name="toouse-hello-script"></a><span data-ttu-id="56b65-120">toouse hello script</span><span class="sxs-lookup"><span data-stu-id="56b65-120">toouse hello script</span></span>

<span data-ttu-id="56b65-121">Voor informatie over hoe toouse dit script met HDInsight, zien Hallo [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="56b65-121">For information on how toouse this script with HDInsight, see hello [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="56b65-122">U kunt gebruiken Hallo script via de hello Azure-portal, Azure PowerShell of Azure CLI Hallo.</span><span class="sxs-lookup"><span data-stu-id="56b65-122">You can use hello script through hello Azure portal, Azure PowerShell, or hello Azure CLI.</span></span>

<span data-ttu-id="56b65-123">Tijdens het volgende script actie document hello, gebruikt u Hallo URI te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b65-123">While following hello script action document, use hello following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="56b65-124">Bij het configureren van HDInsight met dit script, markeert u Hallo script als __persistente__.</span><span class="sxs-lookup"><span data-stu-id="56b65-124">When configuring HDInsight with this script, mark hello script as __Persisted__.</span></span> <span data-ttu-id="56b65-125">Deze instelling kunt HDInsight tooapply Hallo script tooworker knooppunten die zijn toegevoegd door te schalen van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="56b65-125">This setting allows HDInsight tooapply hello script tooworker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="56b65-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56b65-126">Next steps</span></span>

<span data-ttu-id="56b65-127">U hebt geleerd hoe tooupgrade of een specifieke versie van Mono installeren op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="56b65-127">You have learned how tooupgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="56b65-128">Zie voor meer informatie over het gebruik van .NET-toepassingen met Mono op HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="56b65-128">For more information on using .NET applications with Mono on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="56b65-129">.NET gebruiken voor het streamen van MapReduce in HDInsight</span><span class="sxs-lookup"><span data-stu-id="56b65-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="56b65-130">.NET met Hive en Pig in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="56b65-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="56b65-131">C#-oplossingen met Storm op HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="56b65-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="56b65-132">.NET-oplossingen migreren HDInsight op basis van tooLinux</span><span class="sxs-lookup"><span data-stu-id="56b65-132">Migrate .NET solutions tooLinux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="56b65-133">Zie voor meer informatie over het gebruik van scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="56b65-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>