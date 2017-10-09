---
title: aaaUse .NET met Hadoop MapReduce op Linux gebaseerde HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse .NET-toepassingen voor streaming MapReduce op Linux gebaseerde HDInsight.
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
ms.openlocfilehash: 5a4e6dc1b4dafa8cc40780e3371fa4b8ba3e3d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-toolinux-based-hdinsight"></a><span data-ttu-id="385da-103">Migreren van .NET-oplossingen voor HDInsight op basis van Windows HDInsight op basis van tooLinux</span><span class="sxs-lookup"><span data-stu-id="385da-103">Migrate .NET solutions for Windows-based HDInsight tooLinux-based HDInsight</span></span>

<span data-ttu-id="385da-104">Linux gebaseerde HDInsight-clusters gebruik [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="385da-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="385da-105">Mono kunt u toouse .NET onderdelen zoals MapReduce-toepassingen met HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="385da-105">Mono allows you toouse .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="385da-106">In dit document wordt meer informatie over hoe toomigrate .NET oplossingen voor Windows gebaseerde HDInsight-clusters toowork met Mono op Linux gebaseerde HDInsight gemaakt.</span><span class="sxs-lookup"><span data-stu-id="385da-106">In this document, learn how toomigrate .NET solutions created for Windows-based HDInsight clusters toowork with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="385da-107">Mono compatibiliteit met .NET</span><span class="sxs-lookup"><span data-stu-id="385da-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="385da-108">Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="385da-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="385da-109">Zie voor meer informatie over Hallo-versie van Mono opgenomen met HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="385da-109">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="385da-110">tooinstall een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="385da-110">tooinstall a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="385da-111">Zie voor gedetailleerde informatie over de compatibiliteit tussen Mono en .NET Hallo [Mono compatibiliteit (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span><span class="sxs-lookup"><span data-stu-id="385da-111">For detailed information on compatibility between Mono and .NET, see hello [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="385da-112">Hallo SCP.NET framework is compatibel met Mono.</span><span class="sxs-lookup"><span data-stu-id="385da-112">hello SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="385da-113">Zie voor meer informatie over het gebruik van SCP.NET met Mono [Gebruik Visual Studio toodevelop C#-topologieën voor Apache Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="385da-113">For more information on using SCP.NET with Mono, see [Use Visual Studio toodevelop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="385da-114">Analyse van geautomatiseerde draagbaarheid</span><span class="sxs-lookup"><span data-stu-id="385da-114">Automated portability analysis</span></span>

<span data-ttu-id="385da-115">Hallo [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) gebruikte toogenerate een rapport van compatibiliteitsproblemen tussen de toepassing en Mono kan zijn.</span><span class="sxs-lookup"><span data-stu-id="385da-115">hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used toogenerate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="385da-116">Volgende stappen tooconfigure Hallo analyzer toocheck Hallo uw toepassing voor Mono draagbaarheid gebruiken:</span><span class="sxs-lookup"><span data-stu-id="385da-116">Use hello following steps tooconfigure hello analyzer toocheck your application for Mono portability:</span></span>

1. <span data-ttu-id="385da-117">Hallo installeren [.NET draagbaarheid Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="385da-117">Install hello [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="385da-118">Selecteer Hallo-versie van Visual Studio toouse tijdens de installatie.</span><span class="sxs-lookup"><span data-stu-id="385da-118">During installation, select hello version of Visual Studio toouse.</span></span>

2. <span data-ttu-id="385da-119">Selecteer in Visual Studio 2015 __analyseren__ > __draagbaarheid Analyzer instellingen__, en zorg ervoor dat __4.5__ Hallo is ingecheckt __Mono__  sectie.</span><span class="sxs-lookup"><span data-stu-id="385da-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in hello __Mono__ section.</span></span>

    ![4.5 Mono sectie voor Hallo analyzer instellingen ingecheckt](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="385da-121">Selecteer __OK__ toosave Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="385da-121">Select __OK__ toosave hello configuration.</span></span>

3. <span data-ttu-id="385da-122">Selecteer __analyseren__ > __analyseren Assembly draagbaarheid__.</span><span class="sxs-lookup"><span data-stu-id="385da-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="385da-123">Selecteer Hallo-assembly die uw oplossing bevat, en selecteer vervolgens __Open__ toobegin analyse.</span><span class="sxs-lookup"><span data-stu-id="385da-123">Select hello assembly that contains your solution, and then select __Open__ toobegin analysis.</span></span>

4. <span data-ttu-id="385da-124">Zodra de analyse is voltooid, selecteert u __analyseren__ > __analyserapporten weergeven__.</span><span class="sxs-lookup"><span data-stu-id="385da-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="385da-125">In __draagbaarheid analyseresultaten__, selecteer __rapport openen__ tooopen een rapport.</span><span class="sxs-lookup"><span data-stu-id="385da-125">In __Portability Analysis Results__, select __Open report__ tooopen a report.</span></span>

    ![Draagbaarheid analyzer resultaten dialoogvenster](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="385da-127">Hallo analyzer kan geen catch elk probleem met uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="385da-127">hello analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="385da-128">Bijvoorbeeld, een bestandspad van `c:\temp\file.txt` wordt beschouwd als OK omdat Mono wordt uitgevoerd op Windows en Hallo pad ongeldig in deze context is.</span><span class="sxs-lookup"><span data-stu-id="385da-128">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and hello path is valid in that context.</span></span> <span data-ttu-id="385da-129">Hallo-pad is echter niet geldig voor een Linux-platform.</span><span class="sxs-lookup"><span data-stu-id="385da-129">However, hello path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="385da-130">Handmatige draagbaarheid analyse</span><span class="sxs-lookup"><span data-stu-id="385da-130">Manual portability analysis</span></span>

<span data-ttu-id="385da-131">Voer een handmatige controle van uw code met Hallo informatie in Hallo [toepassing draagbaarheid (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span><span class="sxs-lookup"><span data-stu-id="385da-131">Perform a manual audit of your code using hello information in hello [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="385da-132">Wijzigen en maken</span><span class="sxs-lookup"><span data-stu-id="385da-132">Modify and build</span></span>

<span data-ttu-id="385da-133">U kunt Visual Studio-toobuild toouse blijven uw .NET-oplossingen voor HDInsight.</span><span class="sxs-lookup"><span data-stu-id="385da-133">You can continue toouse Visual Studio toobuild your .NET solutions for HDInsight.</span></span> <span data-ttu-id="385da-134">Echter, moet u ervoor zorgen dat Hallo-project is geconfigureerde toouse .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="385da-134">However, you must ensure that hello project is configured toouse .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="385da-135">Implementeren en testen</span><span class="sxs-lookup"><span data-stu-id="385da-135">Deploy and test</span></span>

<span data-ttu-id="385da-136">Als u uw oplossing met behulp van Hallo aanbevelingen van Hallo .NET draagbaarheid Analyzer of van een handmatige analyse hebt gewijzigd, moet u het testen met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="385da-136">Once you have modified your solution using hello recommendations from hello .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="385da-137">Hallo-oplossing op een Linux gebaseerde HDInsight-cluster te testen, waarschijnlijk subtiele problemen die toobe gecorrigeerd moeten.</span><span class="sxs-lookup"><span data-stu-id="385da-137">Testing hello solution on a Linux-based HDInsight cluster may reveal subtle problems that need toobe corrected.</span></span> <span data-ttu-id="385da-138">Het is raadzaam dat u aanvullende logboekregistratie inschakelen in uw toepassing bij het testen.</span><span class="sxs-lookup"><span data-stu-id="385da-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="385da-139">Zie voor meer informatie over de toegang tot logboeken Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="385da-139">For more information on accessing logs, see hello following documents:</span></span>

* [<span data-ttu-id="385da-140">Toegang tot YARN-toepassingslogboeken in een HDInsight-cluster op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="385da-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="385da-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="385da-141">Next steps</span></span>

* [<span data-ttu-id="385da-142">Gebruik C# met MapReduce in HDInsight</span><span class="sxs-lookup"><span data-stu-id="385da-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="385da-143">Gebruik van de gebruiker gedefinieerde functies C# met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="385da-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="385da-144">C#-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="385da-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)