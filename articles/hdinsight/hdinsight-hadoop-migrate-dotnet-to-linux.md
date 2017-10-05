---
title: .NET gebruiken met Hadoop-MapReduce op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Informatie over het gebruik van .NET-toepassingen voor streaming MapReduce op Linux gebaseerde HDInsight.
services: hdinsight
documentationCenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 6ad188fb752474ff5c7d8a3fb9d609eefe8c7a9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="76fd8-103">Migreren van .NET-oplossingen voor HDInsight op Linux gebaseerde HDInsight op basis van Windows</span><span class="sxs-lookup"><span data-stu-id="76fd8-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="76fd8-104">Linux gebaseerde HDInsight-clusters gebruik [Mono (https://mono-project.com)](https://mono-project.com) .NET-toepassingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="76fd8-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="76fd8-105">Mono kunt u .NET-componenten zoals MapReduce-toepassingen gebruiken met HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="76fd8-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="76fd8-106">Informatie over het migreren van .NET-oplossingen voor Windows gebaseerde HDInsight-clusters werkt met Mono op Linux gebaseerde HDInsight gemaakt in dit document.</span><span class="sxs-lookup"><span data-stu-id="76fd8-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="76fd8-107">Mono compatibiliteit met .NET</span><span class="sxs-lookup"><span data-stu-id="76fd8-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="76fd8-108">Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="76fd8-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="76fd8-109">Zie voor meer informatie over de versie van Mono opgenomen met HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="76fd8-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="76fd8-110">Zie het installeren van een specifieke versie van Mono de [installeren of bijwerken van Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="76fd8-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="76fd8-111">Zie voor gedetailleerde informatie over de compatibiliteit tussen Mono en .NET de [Mono compatibiliteit (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span><span class="sxs-lookup"><span data-stu-id="76fd8-111">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76fd8-112">Het framework SCP.NET is compatibel met Mono.</span><span class="sxs-lookup"><span data-stu-id="76fd8-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="76fd8-113">Zie voor meer informatie over het gebruik van SCP.NET met Mono [Gebruik Visual Studio C#-topologieën ontwikkelen voor Apache Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="76fd8-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="76fd8-114">Analyse van geautomatiseerde draagbaarheid</span><span class="sxs-lookup"><span data-stu-id="76fd8-114">Automated portability analysis</span></span>

<span data-ttu-id="76fd8-115">De [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) kan worden gebruikt om een rapport van compatibiliteitsproblemen tussen de toepassing en Mono te genereren.</span><span class="sxs-lookup"><span data-stu-id="76fd8-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="76fd8-116">Gebruik de volgende stappen voor het configureren van de analyzer om te controleren van uw toepassing voor Mono draagbaarheid:</span><span class="sxs-lookup"><span data-stu-id="76fd8-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="76fd8-117">Installeer de [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="76fd8-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="76fd8-118">Selecteer de versie van Visual Studio te gebruiken tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="76fd8-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="76fd8-119">Selecteer in Visual Studio 2015 __analyseren__ > __draagbaarheid Analyzer instellingen__, en zorg ervoor dat __4.5__ is ingeschakeld de __Mono__ sectie.</span><span class="sxs-lookup"><span data-stu-id="76fd8-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 Mono sectie voor de instellingen analyzer ingecheckt](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="76fd8-121">Selecteer __OK__ aan de configuratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="76fd8-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="76fd8-122">Selecteer __analyseren__ > __analyseren Assembly draagbaarheid__.</span><span class="sxs-lookup"><span data-stu-id="76fd8-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="76fd8-123">Selecteer de assembly waarin uw oplossing en selecteer vervolgens __Open__ om te beginnen met de analyse.</span><span class="sxs-lookup"><span data-stu-id="76fd8-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="76fd8-124">Zodra de analyse is voltooid, selecteert u __analyseren__ > __analyserapporten weergeven__.</span><span class="sxs-lookup"><span data-stu-id="76fd8-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="76fd8-125">In __draagbaarheid analyseresultaten__, selecteer __rapport openen__ om een rapport te openen.</span><span class="sxs-lookup"><span data-stu-id="76fd8-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Draagbaarheid analyzer resultaten dialoogvenster](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="76fd8-127">De analyzer kan geen catch elk probleem met uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="76fd8-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="76fd8-128">Bijvoorbeeld, een bestandspad van `c:\temp\file.txt` wordt beschouwd als OK omdat Mono wordt uitgevoerd op Windows en het pad ongeldig in deze context is.</span><span class="sxs-lookup"><span data-stu-id="76fd8-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="76fd8-129">Het pad is echter niet geldig voor een Linux-platform.</span><span class="sxs-lookup"><span data-stu-id="76fd8-129">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="76fd8-130">Handmatige draagbaarheid analyse</span><span class="sxs-lookup"><span data-stu-id="76fd8-130">Manual portability analysis</span></span>

<span data-ttu-id="76fd8-131">Voer een handmatige controle van uw code met de informatie in de [toepassing draagbaarheid (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span><span class="sxs-lookup"><span data-stu-id="76fd8-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="76fd8-132">Wijzigen en maken</span><span class="sxs-lookup"><span data-stu-id="76fd8-132">Modify and build</span></span>

<span data-ttu-id="76fd8-133">U kunt blijven gebruiken van Visual Studio voor het bouwen van uw .NET-oplossingen voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76fd8-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="76fd8-134">Echter, moet u ervoor zorgen dat het project is geconfigureerd voor gebruik van .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="76fd8-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="76fd8-135">Implementeren en testen</span><span class="sxs-lookup"><span data-stu-id="76fd8-135">Deploy and test</span></span>

<span data-ttu-id="76fd8-136">Als u uw oplossing met behulp van de aanbevelingen van de .NET draagbaarheid Analyzer of van een handmatige analyse hebt gewijzigd, moet u het testen met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="76fd8-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="76fd8-137">Testen van de oplossing op een Linux gebaseerde HDInsight-cluster kan subtiele problemen onthullen die moeten worden gecorrigeerd.</span><span class="sxs-lookup"><span data-stu-id="76fd8-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="76fd8-138">Het is raadzaam dat u aanvullende logboekregistratie inschakelen in uw toepassing bij het testen.</span><span class="sxs-lookup"><span data-stu-id="76fd8-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="76fd8-139">Zie de volgende documenten voor meer informatie over de toegang tot logboeken:</span><span class="sxs-lookup"><span data-stu-id="76fd8-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="76fd8-140">Toegang tot YARN-toepassingslogboeken in een HDInsight-cluster op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="76fd8-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="76fd8-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="76fd8-141">Next steps</span></span>

* [<span data-ttu-id="76fd8-142">Gebruik C# met MapReduce in HDInsight</span><span class="sxs-lookup"><span data-stu-id="76fd8-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="76fd8-143">Gebruik van de gebruiker gedefinieerde functies C# met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="76fd8-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="76fd8-144">C#-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="76fd8-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)