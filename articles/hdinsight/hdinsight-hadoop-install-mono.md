---
title: Installeren of bijwerken van Mono op HDInsight - Azure | Microsoft Docs
description: Informatie over het gebruik van een specifieke versie van Mono met HDInsight-cluster. Mono wordt gebruikt voor het uitvoeren van .NET-toepassingen op Linux gebaseerde HDInsight-clusters.
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
ms.openlocfilehash: fd284542e1de65f323f1e3a092689f847e025be6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="install-or-update-mono-on-hdinsight"></a><span data-ttu-id="adf8f-104">Installeren of bijwerken van Mono in HDInsight</span><span class="sxs-lookup"><span data-stu-id="adf8f-104">Install or update Mono on HDInsight</span></span>

<span data-ttu-id="adf8f-105">Informatie over het installeren van een specifieke versie van [Mono](https://www.mono-project.com) op HDInsight 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="adf8f-105">Learn how to install a specific version of [Mono](https://www.mono-project.com) on HDInsight 3.4 or higher.</span></span>

<span data-ttu-id="adf8f-106">Mono op HDInsight 3.4 en hoger is geïnstalleerd en wordt gebruikt voor het uitvoeren van .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="adf8f-106">Mono is installed on HDInsight 3.4 and higher, and is used to run .NET applications.</span></span> <span data-ttu-id="adf8f-107">Zie voor informatie over de versie van Mono opgenomen in elke versie van HDInsight, [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="adf8f-107">For information on the version of Mono included with each HDInsight version, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="adf8f-108">Gebruik voor het installeren van een andere versie op het cluster, de scriptactie in dit document.</span><span class="sxs-lookup"><span data-stu-id="adf8f-108">To install a different version on your cluster, use the script action in this document.</span></span> 

## <a name="how-it-works"></a><span data-ttu-id="adf8f-109">Hoe werkt het?</span><span class="sxs-lookup"><span data-stu-id="adf8f-109">How it works</span></span>

<span data-ttu-id="adf8f-110">Dit script accepteert de volgende parameter:</span><span class="sxs-lookup"><span data-stu-id="adf8f-110">This script accepts the following parameter:</span></span>

* <span data-ttu-id="adf8f-111">__Mono versienummer__: de versie van Mono te installeren.</span><span class="sxs-lookup"><span data-stu-id="adf8f-111">__Mono version number__: The version of Mono to install.</span></span> <span data-ttu-id="adf8f-112">De versie moet beschikbaar zijn vanuit [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span><span class="sxs-lookup"><span data-stu-id="adf8f-112">The version must be available from [https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/](https://download.mono-project.com/repo/debian/dists/wheezy/snapshots/).</span></span>

<span data-ttu-id="adf8f-113">Het script wordt geïnstalleerd voor de volgende Mono-pakketten:</span><span class="sxs-lookup"><span data-stu-id="adf8f-113">The script installs the following Mono packages:</span></span>

* <span data-ttu-id="adf8f-114">__Mono-voltooid__</span><span class="sxs-lookup"><span data-stu-id="adf8f-114">__mono-complete__</span></span>

* <span data-ttu-id="adf8f-115">__CA-certificaten-mono__</span><span class="sxs-lookup"><span data-stu-id="adf8f-115">__ca-certificates-mono__</span></span>

## <a name="the-script"></a><span data-ttu-id="adf8f-116">Het script</span><span class="sxs-lookup"><span data-stu-id="adf8f-116">The script</span></span>

<span data-ttu-id="adf8f-117">__Locatie script__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span><span class="sxs-lookup"><span data-stu-id="adf8f-117">__Script location__: [https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash](https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash)</span></span>

<span data-ttu-id="adf8f-118">__Vereisten__:</span><span class="sxs-lookup"><span data-stu-id="adf8f-118">__Requirements__:</span></span>

* <span data-ttu-id="adf8f-119">Het script moet worden toegepast op de __hoofdknooppunten__ en __worker-knooppunten__.</span><span class="sxs-lookup"><span data-stu-id="adf8f-119">The script must be applied on the __head nodes__ and __worker nodes__.</span></span>

## <a name="to-use-the-script"></a><span data-ttu-id="adf8f-120">Het script gebruiken</span><span class="sxs-lookup"><span data-stu-id="adf8f-120">To use the script</span></span>

<span data-ttu-id="adf8f-121">Zie voor meer informatie over het gebruik van dit script met HDInsight de [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span><span class="sxs-lookup"><span data-stu-id="adf8f-121">For information on how to use this script with HDInsight, see the [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md#apply-a-script-action-to-a-running-cluster) document.</span></span> <span data-ttu-id="adf8f-122">U kunt het script via de Azure-portal, Azure PowerShell of Azure CLI gebruiken.</span><span class="sxs-lookup"><span data-stu-id="adf8f-122">You can use the script through the Azure portal, Azure PowerShell, or the Azure CLI.</span></span>

<span data-ttu-id="adf8f-123">Tijdens het script actie document te volgen, gebruikt u de volgende URI:</span><span class="sxs-lookup"><span data-stu-id="adf8f-123">While following the script action document, use the following URI:</span></span>

    https://hdiconfigactions.blob.core.windows.net/install-mono/install-mono.bash

> [!NOTE]
> <span data-ttu-id="adf8f-124">Bij het configureren van HDInsight met dit script, markeert u het script als __persistente__.</span><span class="sxs-lookup"><span data-stu-id="adf8f-124">When configuring HDInsight with this script, mark the script as __Persisted__.</span></span> <span data-ttu-id="adf8f-125">Deze instelling kunt HDInsight het script op de worker-knooppunten die zijn toegevoegd door te schalen bewerkingen toepassen.</span><span class="sxs-lookup"><span data-stu-id="adf8f-125">This setting allows HDInsight to apply the script to worker nodes added through scaling operations.</span></span>


## <a name="next-steps"></a><span data-ttu-id="adf8f-126">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="adf8f-126">Next steps</span></span>

<span data-ttu-id="adf8f-127">U hebt geleerd hoe u wilt upgraden of installeren van een specifieke versie van Mono op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="adf8f-127">You have learned how to upgrade or install a specific version of Mono on HDInsight.</span></span> <span data-ttu-id="adf8f-128">Zie de volgende documenten voor meer informatie over het gebruik van .NET-toepassingen met Mono op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="adf8f-128">For more information on using .NET applications with Mono on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="adf8f-129">.NET gebruiken voor het streamen van MapReduce in HDInsight</span><span class="sxs-lookup"><span data-stu-id="adf8f-129">Use .NET for streaming MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)
* [<span data-ttu-id="adf8f-130">.NET met Hive en Pig in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="adf8f-130">Use .NET with Hive and Pig on HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)
* [<span data-ttu-id="adf8f-131">C#-oplossingen met Storm op HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="adf8f-131">Develop C# solutions with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="adf8f-132">.NET-oplossingen migreren naar HDInsight op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="adf8f-132">Migrate .NET solutions to Linux-based HDInsight</span></span>](hdinsight-hadoop-migrate-dotnet-to-linux.md)

<span data-ttu-id="adf8f-133">Zie voor meer informatie over het gebruik van scriptacties [aanpassen Linux gebaseerde HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md)</span><span class="sxs-lookup"><span data-stu-id="adf8f-133">For more information on using script actions, see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md)</span></span>