---
title: "aaaApache Storm-topologieën met Visual Studio en C# - Azure HDInsight | Microsoft Docs"
description: "Meer informatie over hoe toocreate Storm-topologieën in C#. Een eenvoudige word-count-topologie in Visual Studio maakt met behulp van Hallo Hadoop-hulpprogramma's voor Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7a6b3-104">C#-topologieën ontwikkelen voor Apache Storm met behulp van Hallo Data Lake tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a6b3-104">Develop C# topologies for Apache Storm by using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7a6b3-105">Meer informatie over hoe toocreate een C# Storm-topologie met behulp van hello Azure Data Lake (Hadoop) tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-105">Learn how toocreate a C# Storm topology by using hello Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="7a6b3-106">Dit document wordt uitgelegd Hallo-proces voor het maken van een Storm-project in Visual Studio, lokaal te testen en implementeren van tooan Apache Storm op Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-106">This document walks through hello process of creating a Storm project in Visual Studio, testing it locally, and deploying it tooan Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="7a6b3-107">U leert ook hoe toocreate hybride topologieën die werken met C# en Java-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-107">You also learn how toocreate hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="7a6b3-108">Hoewel Hallo stappen in dit document, is afhankelijk van een Windows-ontwikkelomgeving met Visual Studio, zijn gecompileerd Hallo-project ingediende tooeither een Linux- of Windows gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-108">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooeither a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="7a6b3-109">Op basis van Linux-clusters die zijn gemaakt na 28 oktober 2016 ondersteunen alleen SCP.NET topologieën.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="7a6b3-110">toouse een C#-topologie met een cluster op basis van Linux, moet u Hallo Microsoft.SCP.Net.SDK NuGet-pakket gebruikt door uw project tooversion 0.10.0.6 of hoger bijwerken.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-110">toouse a C# topology with a Linux-based cluster, you must update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or later.</span></span> <span data-ttu-id="7a6b3-111">Hallo-versie van het Hallo-pakket moet ook overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-111">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="7a6b3-112">HDInsight-versie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-112">HDInsight version</span></span> | <span data-ttu-id="7a6b3-113">Storm-versie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-113">Storm version</span></span> | <span data-ttu-id="7a6b3-114">SCP.NET versie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-114">SCP.NET version</span></span> | <span data-ttu-id="7a6b3-115">Standaard Mono-versie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="7a6b3-116">3.3</span><span class="sxs-lookup"><span data-stu-id="7a6b3-116">3.3</span></span> |<span data-ttu-id="7a6b3-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-117">0.10.x</span></span> |<span data-ttu-id="7a6b3-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-118">0.10.x.x</span></span></br><span data-ttu-id="7a6b3-119">(alleen op HDInsight op basis van Windows)</span><span class="sxs-lookup"><span data-stu-id="7a6b3-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="7a6b3-120">N.v.t.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-120">NA</span></span> |
| <span data-ttu-id="7a6b3-121">3.4</span><span class="sxs-lookup"><span data-stu-id="7a6b3-121">3.4</span></span> | <span data-ttu-id="7a6b3-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-122">0.10.0.x</span></span> | <span data-ttu-id="7a6b3-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-123">0.10.0.x</span></span> | <span data-ttu-id="7a6b3-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="7a6b3-124">3.2.8</span></span> |
| <span data-ttu-id="7a6b3-125">3,5</span><span class="sxs-lookup"><span data-stu-id="7a6b3-125">3.5</span></span> | <span data-ttu-id="7a6b3-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-126">1.0.2.x</span></span> | <span data-ttu-id="7a6b3-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-127">1.0.0.x</span></span> | <span data-ttu-id="7a6b3-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="7a6b3-128">4.2.1</span></span> |
| <span data-ttu-id="7a6b3-129">3.6</span><span class="sxs-lookup"><span data-stu-id="7a6b3-129">3.6</span></span> | <span data-ttu-id="7a6b3-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-130">1.1.0.x</span></span> | <span data-ttu-id="7a6b3-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="7a6b3-131">1.0.0.x</span></span> | <span data-ttu-id="7a6b3-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="7a6b3-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="7a6b3-133">C#-topologieën op Linux gebaseerde clusters moeten gebruiken, .NET 4.5 en het gebruik van Mono toorun op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="7a6b3-134">Controleer [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) voor potentiële compatibiliteitsproblemen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="7a6b3-135">Visual Studio installeren</span><span class="sxs-lookup"><span data-stu-id="7a6b3-135">Install Visual Studio</span></span>

<span data-ttu-id="7a6b3-136">U kunt de C#-topologieën met SCP.NET ontwikkelen met behulp van een van de volgende versies van Visual Studio Hallo:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-136">You can develop C# topologies with SCP.NET by using one of hello following versions of Visual Studio:</span></span>

* <span data-ttu-id="7a6b3-137">Visual Studio 2012 met [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="7a6b3-137">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

* <span data-ttu-id="7a6b3-138">Visual Studio 2013 met [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) of [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="7a6b3-138">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="7a6b3-139">Visual Studio 2015 of [Visual Studio 2015-Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="7a6b3-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="7a6b3-140">Visual Studio 2017 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="7a6b3-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="7a6b3-141">Installatie van Data Lake tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7a6b3-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="7a6b3-142">tooinstall Data Lake tools voor Visual Studio, Hallo stappen in [aan de slag met Data Lake tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-142">tooinstall Data Lake tools for Visual Studio, follow hello steps in [Get started using Data Lake tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="7a6b3-143">Java installeren</span><span class="sxs-lookup"><span data-stu-id="7a6b3-143">Install Java</span></span>

<span data-ttu-id="7a6b3-144">Wanneer u een Storm-topologie vanuit Visual Studio indient, genereert SCP.NET een zip-bestand dat Hallo topologie en afhankelijkheden bevat.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains hello topology and dependencies.</span></span> <span data-ttu-id="7a6b3-145">Java gebruikte toocreate is deze zip-bestanden, omdat deze gebruikmaakt van een indeling die is beter geschikt voor clusters op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-145">Java is used toocreate these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="7a6b3-146">Hallo Java Developer Kit (JDK) 7 of hoger installeren op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-146">Install hello Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="7a6b3-147">U kunt krijgen Hallo Oracle JDK van [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-147">You can get hello Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="7a6b3-148">U kunt ook [andere Java-distributies](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="7a6b3-149">Hallo `JAVA_HOME` omgeving variabele moet punt toohello directory met Java.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-149">hello `JAVA_HOME` environment variable must point toohello directory that contains Java.</span></span>

3. <span data-ttu-id="7a6b3-150">Hallo `PATH` omgevingsvariabele vergezeld Hallo `%JAVA_HOME%\bin` directory.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-150">hello `PATH` environment variable must include hello `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="7a6b3-151">Hallo volgende C#-console toepassing tooverify Java en Hallo JDK juist zijn geïnstalleerd, kunt u gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-151">You can use hello following C# console application tooverify that Java and hello JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="7a6b3-152">Storm-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-152">Storm templates</span></span>

<span data-ttu-id="7a6b3-153">Hallo Data Lake tools voor Visual Studio bieden Hallo sjablonen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-153">hello Data Lake tools for Visual Studio provide hello following templates:</span></span>

| <span data-ttu-id="7a6b3-154">Projecttype</span><span class="sxs-lookup"><span data-stu-id="7a6b3-154">Project type</span></span> | <span data-ttu-id="7a6b3-155">Demonstreert</span><span class="sxs-lookup"><span data-stu-id="7a6b3-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="7a6b3-156">Storm-toepassing</span><span class="sxs-lookup"><span data-stu-id="7a6b3-156">Storm Application</span></span> |<span data-ttu-id="7a6b3-157">Een leeg Storm-topologie-project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="7a6b3-158">Storm Azure SQL Writer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7a6b3-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="7a6b3-159">Hoe toowrite tooAzure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-159">How toowrite tooAzure SQL Database.</span></span> |
| <span data-ttu-id="7a6b3-160">Voorbeeld van storm Azure Cosmos DB lezer</span><span class="sxs-lookup"><span data-stu-id="7a6b3-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="7a6b3-161">Hoe tooread uit Azure Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-161">How tooread from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="7a6b3-162">Storm Azure Cosmos DB Writer voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7a6b3-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="7a6b3-163">Hoe toowrite tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-163">How toowrite tooAzure Cosmos DB.</span></span> |
| <span data-ttu-id="7a6b3-164">Voorbeeld van storm EventHub-lezer</span><span class="sxs-lookup"><span data-stu-id="7a6b3-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="7a6b3-165">Hoe tooread uit Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-165">How tooread from Azure Event Hubs.</span></span> |
| <span data-ttu-id="7a6b3-166">Voorbeeld van storm EventHub-schrijver</span><span class="sxs-lookup"><span data-stu-id="7a6b3-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="7a6b3-167">Hoe toowrite tooAzure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-167">How toowrite tooAzure Event Hubs.</span></span> |
| <span data-ttu-id="7a6b3-168">Voorbeeld van storm-HBase-lezer</span><span class="sxs-lookup"><span data-stu-id="7a6b3-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="7a6b3-169">Hoe tooread van HBase op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-169">How tooread from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="7a6b3-170">Voorbeeld van storm-HBase-schrijver</span><span class="sxs-lookup"><span data-stu-id="7a6b3-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="7a6b3-171">Hoe toowrite tooHBase op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-171">How toowrite tooHBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="7a6b3-172">Storm hybride voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7a6b3-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="7a6b3-173">Hoe toouse een Java-component.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-173">How toouse a Java component.</span></span> |
| <span data-ttu-id="7a6b3-174">Storm-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="7a6b3-174">Storm Sample</span></span> |<span data-ttu-id="7a6b3-175">Een basic word-count-topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="7a6b3-176">Niet alle sjablonen, werken met HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-176">Not all templates will work with Linux-based HDInsight.</span></span> <span data-ttu-id="7a6b3-177">Nuget-pakketten die worden gebruikt door Hallo sjablonen zijn mogelijk niet compatibel met Mono.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-177">Nuget packages used by hello templates may not be compatible with Mono.</span></span> <span data-ttu-id="7a6b3-178">Controleer Hallo [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) documenteren en gebruik Hallo [.NET draagbaarheid Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potentiële problemen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-178">Check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use hello [.NET Portability Analyzer](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify potential problems.</span></span>

<span data-ttu-id="7a6b3-179">In Hallo stappen in dit document gebruikt u Hallo basic Storm-toepassing project type toocreate een topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-179">In hello steps in this document, you use hello basic Storm Application project type toocreate a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="7a6b3-180">Opmerkingen bij de HBase-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-180">HBase templates notes</span></span>

<span data-ttu-id="7a6b3-181">Hallo HBase lezer en writer sjablonen gebruiken Hallo HBase REST API, niet Hallo HBase Java API, toocommunicate met een HBase op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-181">hello HBase reader and writer templates use hello HBase REST API, not hello HBase Java API, toocommunicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="7a6b3-182">Opmerkingen bij de EventHub-sjablonen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a6b3-183">Hallo Java gebaseerde EventHub spout onderdeel van Hallo EventHub lezer sjabloon niet met Storm op HDInsight versie 3.5 of hoger werken mogelijk.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-183">hello Java-based EventHub spout component included with hello EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="7a6b3-184">Een bijgewerkte versie van dit onderdeel is beschikbaar op [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="7a6b3-185">Zie voor een topologie die gebruikmaakt van dit onderdeel en werkt met Storm op HDInsight 3.5, [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="7a6b3-186">Maak een C#-topologie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-186">Create a C# topology</span></span>

1. <span data-ttu-id="7a6b3-187">Open Visual Studio, selecteer **bestand** > **nieuw**, en selecteer vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="7a6b3-188">Van Hallo **nieuw Project** venster Vouw **geïnstalleerde** > **sjablonen**, en selecteer **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-188">From hello **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="7a6b3-189">Selecteer in de lijst met sjablonen Hallo **Storm-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-189">From hello list of templates, select **Storm Application**.</span></span> <span data-ttu-id="7a6b3-190">Voer Hallo onderaan welkomstscherm in **WordCount** als naam van de toepassing hello Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-190">At hello bottom of hello screen, enter **WordCount** as hello name of hello application.</span></span>

    ![Schermopname van nieuw Project-venster](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="7a6b3-192">Nadat u Hallo-project hebt gemaakt, hebt u Hallo volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-192">After you have created hello project, you should have hello following files:</span></span>

   * <span data-ttu-id="7a6b3-193">**Program.cs**: dit bestand definieert het Hallo-topologie voor uw project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-193">**Program.cs**: This file defines hello topology for your project.</span></span> <span data-ttu-id="7a6b3-194">Standaard wordt een standaard-topologie die uit één spout en één bolt bestaat gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="7a6b3-195">**Spout.cs**: een voorbeeld spout die willekeurige getallen verzendt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="7a6b3-196">**Bolt.cs**: een voorbeeld-bolt die een aantal van de getallen die worden verzonden door Hallo spout houdt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by hello spout.</span></span>

     <span data-ttu-id="7a6b3-197">Wanneer u Hallo-project maakt, NuGet downloads laatste Hallo [SCP.NET pakket](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-197">When you create hello project, NuGet downloads hello latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a><span data-ttu-id="7a6b3-198">Implementeer Hallo spout</span><span class="sxs-lookup"><span data-stu-id="7a6b3-198">Implement hello spout</span></span>

1. <span data-ttu-id="7a6b3-199">Open **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-199">Open **Spout.cs**.</span></span> <span data-ttu-id="7a6b3-200">Spouts zijn gebruikte tooread gegevens in een topologie van een externe bron.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-200">Spouts are used tooread data in a topology from an external source.</span></span> <span data-ttu-id="7a6b3-201">hoofdonderdelen voor een spout Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-201">hello main components for a spout are:</span></span>

   * <span data-ttu-id="7a6b3-202">**NextTuple**: door Storm wordt aangeroepen wanneer de Hallo spout tooemit nieuwe tuples is toegestaan.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-202">**NextTuple**: Called by Storm when hello spout is allowed tooemit new tuples.</span></span>

   * <span data-ttu-id="7a6b3-203">**ACK** (alleen voor transactionele topologie): bevestigingen geïnitieerd door de andere onderdelen in Hallo-topologie voor verzonden van Hallo spout tuples worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in hello topology for tuples sent from hello spout.</span></span> <span data-ttu-id="7a6b3-204">Een tuple zijn bevestigd, kunt Hallo spout weten dat deze is verwerkt door downstream-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-204">Acknowledging a tuple lets hello spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="7a6b3-205">**Mislukken** (alleen voor transactionele topologie): tuples die zijn mislukt-verwerking van andere onderdelen in de topologie Hallo verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in hello topology.</span></span> <span data-ttu-id="7a6b3-206">Implementatie van een methode is mislukt, kunt u toore-tuple Hallo verzenden zodat deze opnieuw kan worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-206">Implementing a Fail method allows you toore-emit hello tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="7a6b3-207">Vervang de inhoud Hallo Hallo **Spout** klasse met de volgende tekst hello.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-207">Replace hello contents of hello **Spout** class with hello following text.</span></span> <span data-ttu-id="7a6b3-208">Deze spout verzendt willekeurig een zin in Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-208">This spout randomly emits a sentence into hello topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a><span data-ttu-id="7a6b3-209">Hallo bolts implementeren</span><span class="sxs-lookup"><span data-stu-id="7a6b3-209">Implement hello bolts</span></span>

1. <span data-ttu-id="7a6b3-210">Verwijder bestaande Hallo **Bolt.cs** bestand uit Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-210">Delete hello existing **Bolt.cs** file from hello project.</span></span>

2. <span data-ttu-id="7a6b3-211">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **toevoegen** > **nieuw item**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-211">In **Solution Explorer**, right-click hello project, and select **Add** > **New item**.</span></span> <span data-ttu-id="7a6b3-212">Selecteer in de lijst Hallo **Storm Bolt**, en voer **Splitter.cs** als Hallo-naam.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-212">From hello list, select **Storm Bolt**, and enter **Splitter.cs** as hello name.</span></span> <span data-ttu-id="7a6b3-213">Herhaal dit proces toocreate met de naam een tweede bolt **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-213">Repeat this process toocreate a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="7a6b3-214">**Splitter.cs**: implementeert een bolt die zinnen splitst in afzonderlijke woorden en verzendt een nieuwe reeks woorden.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-214">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="7a6b3-215">**Counter.cs**: implementeert een bolt die elk woord telt en verzendt een nieuwe reeks woorden en Hallo telling voor elk woord.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-215">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and hello count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="7a6b3-216">Deze bolts lezen en schrijven toostreams, maar u kunt ook een bolt toocommunicate met bronnen zoals een database of service.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-216">These bolts read and write toostreams, but you can also use a bolt toocommunicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="7a6b3-217">Open **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-217">Open **Splitter.cs**.</span></span> <span data-ttu-id="7a6b3-218">Slechts één methode heeft standaard: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-218">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="7a6b3-219">Hallo Execute-methode wordt aangeroepen wanneer Hallo bolt een tuple voor verwerking ontvangt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-219">hello Execute method is called when hello bolt receives a tuple for processing.</span></span> <span data-ttu-id="7a6b3-220">Hier vindt u binnenkomende tuples verwerken en verzenden van uitgaande tuples.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-220">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="7a6b3-221">Vervang de inhoud Hallo Hallo **splitser** klasse Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-221">Replace hello contents of hello **Splitter** class with hello following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. <span data-ttu-id="7a6b3-222">Open **Counter.cs**, en vervang Hallo klasse inhoud door Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-222">Open **Counter.cs**, and replace hello class contents with hello following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a><span data-ttu-id="7a6b3-223">Hallo-topologie definiëren</span><span class="sxs-lookup"><span data-stu-id="7a6b3-223">Define hello topology</span></span>

<span data-ttu-id="7a6b3-224">Spouts en bolts worden gerangschikt in een grafiek, waarmee wordt gedefinieerd hoe Hallo gegevens tussen onderdelen loopt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-224">Spouts and bolts are arranged in a graph, which defines how hello data flows between components.</span></span> <span data-ttu-id="7a6b3-225">Voor deze topologie is Hallo grafiek als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-225">For this topology, hello graph is as follows:</span></span>

![Diagram van hoe onderdelen worden gerangschikt](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="7a6b3-227">Zinnen van Hallo spout worden verzonden en gedistribueerde tooinstances van Hallo splitser bolt zijn.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-227">Sentences are emitted from hello spout, and are distributed tooinstances of hello Splitter bolt.</span></span> <span data-ttu-id="7a6b3-228">Hallo zinnen Hallo splitser bolt opgesplitst in woorden die gedistribueerd toohello teller bolt zijn.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-228">hello Splitter bolt breaks hello sentences into words, which are distributed toohello Counter bolt.</span></span>

<span data-ttu-id="7a6b3-229">Omdat het aantal woorden is die lokaal zijn opgeslagen in een exemplaar van prestatiemeteritem hello, willen we zeker van te zijn dat specifieke woorden toohello vloeien toomake hetzelfde exemplaar van prestatiemeteritem bolt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-229">Because word count is held locally in hello Counter instance, we want toomake sure that specific words flow toohello same Counter bolt instance.</span></span> <span data-ttu-id="7a6b3-230">Elk exemplaar houdt van specifieke woorden.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-230">Each instance keeps track of specific words.</span></span> <span data-ttu-id="7a6b3-231">Aangezien Hallo splitser bolt geen status onderhoudt, het echt maakt niet uit welke instantie van de splitser Hallo ontvangt welke zin.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-231">Since hello Splitter bolt maintains no state, it really doesn't matter which instance of hello splitter receives which sentence.</span></span>

<span data-ttu-id="7a6b3-232">Open **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-232">Open **Program.cs**.</span></span> <span data-ttu-id="7a6b3-233">Hallo belangrijke methode is **GetTopologyBuilder**, tooStorm die is gebruikt toodefine Hallo-topologie die is verzonden.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-233">hello important method is **GetTopologyBuilder**, which is used toodefine hello topology that is submitted tooStorm.</span></span> <span data-ttu-id="7a6b3-234">Vervang de inhoud Hallo van **GetTopologyBuilder** Hello na code tooimplement Hallo topologie eerder beschreven:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-234">Replace hello contents of **GetTopologyBuilder** with hello following code tooimplement hello topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a><span data-ttu-id="7a6b3-235">Hallo-topologie verzenden</span><span class="sxs-lookup"><span data-stu-id="7a6b3-235">Submit hello topology</span></span>

1. <span data-ttu-id="7a6b3-236">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-236">In **Solution Explorer**, right-click hello project, and select **Submit tooStorm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a6b3-237">Als u wordt gevraagd, voert u Hallo referenties voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-237">If prompted, enter hello credentials for your Azure subscription.</span></span> <span data-ttu-id="7a6b3-238">Als u meer dan één abonnement hebt, meld u aan toohello een bestand met uw Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-238">If you have more than one subscription, sign in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="7a6b3-239">Selecteer uw Storm op HDInsight-cluster in Hallo **Storm-Cluster** vervolgkeuzelijst en selecteer vervolgens **indienen**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-239">Select your Storm on HDInsight cluster from hello **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="7a6b3-240">U kunt controleren als Hallo verzending is voltooid met Hallo **uitvoer** venster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-240">You can monitor if hello submission is successful by using hello **Output** window.</span></span>

3. <span data-ttu-id="7a6b3-241">Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën** voor Hallo cluster moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-241">When hello topology has been successfully submitted, hello **Storm Topologies** for hello cluster should appear.</span></span> <span data-ttu-id="7a6b3-242">Selecteer Hallo **WordCount** topologie van Hallo lijst tooview informatie over het Hallo-topologie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-242">Select hello **WordCount** topology from hello list tooview information about hello running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a6b3-243">U kunt ook weergeven **Storm-topologieën** van **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-243">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="7a6b3-244">Vouw **Azure** > **HDInsight**, met de rechtermuisknop op een Storm op HDInsight-cluster en selecteer vervolgens **weergave Storm-topologieën**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-244">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="7a6b3-245">tooview informatie over Hallo-onderdelen in Hallo-topologie, dubbelklik op Hallo-component in Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-245">tooview information about hello components in hello topology, double-click hello component in hello diagram.</span></span>

4. <span data-ttu-id="7a6b3-246">Van Hallo **Topology Summary** weergeven, klikt u op **Kill** toostop Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-246">From hello **Topology Summary** view, click **Kill** toostop hello topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a6b3-247">Storm-topologieën blijven toorun totdat ze worden gedeactiveerd of Hallo-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-247">Storm topologies continue toorun until they are deactivated, or hello cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="7a6b3-248">Transactionele-topologie</span><span class="sxs-lookup"><span data-stu-id="7a6b3-248">Transactional topology</span></span>

<span data-ttu-id="7a6b3-249">Hallo vorige topologie is niet-transactionele.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-249">hello previous topology is non-transactional.</span></span> <span data-ttu-id="7a6b3-250">Hallo-onderdelen in de topologie Hallo functionaliteit tooreplaying berichten niet geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-250">hello components in hello topology do not implement functionality tooreplaying messages.</span></span> <span data-ttu-id="7a6b3-251">Voor een voorbeeld van een transactionele topologie, maak een project en selecteer **Storm voorbeeld** als Hallo projecttype.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-251">For an example of a transactional topology, create a project and select **Storm Sample** as hello project type.</span></span>

<span data-ttu-id="7a6b3-252">Transactionele topologieën implementeren Hallo toosupport replay van gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-252">Transactional topologies implement hello following toosupport replay of data:</span></span>

* <span data-ttu-id="7a6b3-253">**Metagegevens opslaan in cache**: Hallo spout moet slaan metagegevens over Hallo gegevens verzonden, zodat Hallo gegevens kunnen worden opgehaald en opnieuw verzonden als er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-253">**Metadata caching**: hello spout must store metadata about hello data emitted, so that hello data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="7a6b3-254">Omdat het Hallo-gegevens die door Hallo voorbeeld klein is, wordt in een woordenlijst om replaydetectie Hallo onbewerkte gegevens voor elke tuple opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-254">Because hello data emitted by hello sample is small, hello raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="7a6b3-255">**ACK**: elke bolt in Hallo topologie kunt aanroepen `this.ctx.Ack(tuple)` tooacknowledge dat deze is een tuple verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-255">**Ack**: Each bolt in hello topology can call `this.ctx.Ack(tuple)` tooacknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="7a6b3-256">Wanneer alle bolts bevestigd Hallo tuple hebt, Hallo `Ack` hello spout methode wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-256">When all bolts have acked hello tuple, hello `Ack` method of hello spout is invoked.</span></span> <span data-ttu-id="7a6b3-257">Hallo `Ack` methode kunnen Hallo spout tooremove gegevens om replaydetectie in cache is opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-257">hello `Ack` method allows hello spout tooremove data that was cached for replay.</span></span>

* <span data-ttu-id="7a6b3-258">**Mislukken**: elke bolt kunt aanroepen `this.ctx.Fail(tuple)` tooindicate die verwerking is mislukt voor een tuple.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-258">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` tooindicate that processing has failed for a tuple.</span></span> <span data-ttu-id="7a6b3-259">Hallo fout doorgegeven toohello `Fail` methode van Hallo spout, waarbij Hallo-tuple kan worden cookies met behulp van metagegevens in cache.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-259">hello failure propagates toohello `Fail` method of hello spout, where hello tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="7a6b3-260">**Sequentiëren ID**: bij het genereren van een tuple een unieke reeks-ID kan worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-260">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="7a6b3-261">Deze waarde identificeert Hallo tuple voor de verwerking van opnieuw afspelen (Ack en mislukken).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-261">This value identifies hello tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="7a6b3-262">Bijvoorbeeld, Hallo spout in Hallo **Storm voorbeeld** Hallo volgende wordt gebruikt bij het genereren van gegevens:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-262">For example, hello spout in hello **Storm Sample** project uses hello following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="7a6b3-263">Deze code verzendt een tuple met een zin toohello standaard-stream met Hallo reeks id-waarde is opgenomen in **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-263">This code emits a tuple that contains a sentence toohello default stream, with hello sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="7a6b3-264">In dit voorbeeld **lastSeqId** voor elke tuple verzonden wordt verhoogd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-264">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="7a6b3-265">Zoals wordt beschreven in Hallo **Storm voorbeeld** project, of een onderdeel is transactionele kan worden ingesteld tijdens runtime, op basis van configuratie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-265">As demonstrated in hello **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="7a6b3-266">Hybride topologie met C# en Java</span><span class="sxs-lookup"><span data-stu-id="7a6b3-266">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="7a6b3-267">U kunt ook Data Lake tools voor Visual Studio toocreate hybride topologieën, waarin bepaalde onderdelen zijn C# en anderen Java zijn.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-267">You can also use Data Lake tools for Visual Studio toocreate hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="7a6b3-268">Voor een voorbeeld van een hybride-topologie, maak een project en selecteer **Storm hybride voorbeeld**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-268">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="7a6b3-269">Dit Voorbeeldtype demonstreert Hallo volgende concepten:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-269">This sample type demonstrates hello following concepts:</span></span>

* <span data-ttu-id="7a6b3-270">**Java-spout** en **C# bolt**: gedefinieerd in **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-270">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="7a6b3-271">Een transactionele versie is gedefinieerd in **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-271">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="7a6b3-272">**C# spout** en **Java bolt**: gedefinieerd in **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-272">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="7a6b3-273">Een transactionele versie is gedefinieerd in **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-273">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="7a6b3-274">Deze versie wordt ook getoond hoe toouse Clojure code uit een tekstbestand als een Java-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-274">This version also demonstrates how toouse Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="7a6b3-275">tooswitch hello topologie die wordt gebruikt wanneer het Hallo-project wordt ingediend, verplaatst Hallo `[Active(true)]` instructie toohello topologie toouse, voordat het wordt ingediend toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-275">tooswitch hello topology that is used when hello project is submitted, simply move hello `[Active(true)]` statement toohello topology you want toouse, before submitting it toohello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7a6b3-276">Alle Hallo Java-bestanden die vereist zijn worden geleverd als onderdeel van dit project in Hallo **JavaDependency** map.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-276">All hello Java files that are required are provided as part of this project in hello **JavaDependency** folder.</span></span>

<span data-ttu-id="7a6b3-277">Overweeg Hallo volgende wanneer u maken en verzenden van een hybride-topologie:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-277">Consider hello following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="7a6b3-278">U moet gebruiken **JavaComponentConstructor** toocreate een exemplaar van Hallo Java-klasse voor een spout of bolt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-278">You must use **JavaComponentConstructor** toocreate an instance of hello Java class for a spout or bolt.</span></span>

* <span data-ttu-id="7a6b3-279">U moet gebruiken **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON tooserialize gegevens van of naar Java-onderdelen van Java-objecten.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-279">You should use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooserialize data into or out of Java components from Java objects tooJSON.</span></span>

* <span data-ttu-id="7a6b3-280">Bij het indienen van Hallo topologie toohello server, moet u Hallo **aanvullende configuraties** optie toospecify hello **Java bestandspaden**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-280">When submitting hello topology toohello server, you must use hello **Additional configurations** option toospecify hello **Java File paths**.</span></span> <span data-ttu-id="7a6b3-281">Hallo-pad opgegeven moet Hallo directory met Hallo JAR-bestanden die uw Java-klassen bevatten.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-281">hello path specified should be hello directory that contains hello JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="7a6b3-282">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="7a6b3-282">Azure Event Hubs</span></span>

<span data-ttu-id="7a6b3-283">SCP.NET versie 0.9.4.203 introduceert een nieuwe klasse en de methode specifiek voor het werken met Hallo Event Hub spout (een Java-spout die uit Event Hubs lezen).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-283">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with hello Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="7a6b3-284">Wanneer u een topologie maakt die gebruikmaakt van een Event Hub spout, gebruik Hallo volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-284">When you create a topology that uses an Event Hub spout, use hello following methods:</span></span>

* <span data-ttu-id="7a6b3-285">**EventHubSpoutConfig** klasse: maakt een object dat het Hallo-configuratie voor Hallo spout onderdeel bevat.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-285">**EventHubSpoutConfig** class: Creates an object that contains hello configuration for hello spout component.</span></span>

* <span data-ttu-id="7a6b3-286">**TopologyBuilder.SetEventHubSpout** methode: Hallo Event Hub spout onderdeel toohello topologie worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-286">**TopologyBuilder.SetEventHubSpout** method: Adds hello Event Hub spout component toohello topology.</span></span>

> [!NOTE]
> <span data-ttu-id="7a6b3-287">U moet nog steeds gebruiken Hallo **CustomizedInteropJSONSerializer** tooserialize gegevens geproduceerd door Hallo spout.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-287">You must still use hello **CustomizedInteropJSONSerializer** tooserialize data produced by hello spout.</span></span>

## <span data-ttu-id="7a6b3-288"><a id="configurationmanager"></a>Configuration Manager gebruiken</span><span class="sxs-lookup"><span data-stu-id="7a6b3-288"><a id="configurationmanager"></a>Use ConfigurationManager</span></span>

<span data-ttu-id="7a6b3-289">Gebruik geen **ConfigurationManager** tooretrieve configuratiewaarden van Bolts en spout onderdelen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-289">Don't use **ConfigurationManager** tooretrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="7a6b3-290">In dat geval kan een uitzondering voor een null-aanwijzer veroorzaken.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-290">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="7a6b3-291">In plaats daarvan wordt Hallo-configuratie voor uw project in Hallo Storm-topologie doorgegeven als een sleutel-waardepaar in de context van Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-291">Instead, hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="7a6b3-292">Elk onderdeel dat is afhankelijk van de configuratiewaarden moet deze worden opgehaald van Hallo context tijdens de initialisatie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-292">Each component that relies on configuration values must retrieve them from hello context during initialization.</span></span>

<span data-ttu-id="7a6b3-293">Hallo volgende code laat zien hoe tooretrieve deze waarden:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-293">hello following code demonstrates how tooretrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="7a6b3-294">Als u een `Get` methode tooreturn een instantie van het onderdeel, moet u ervoor zorgen dat dit wordt doorgegeven beide Hallo `Context` en `Dictionary<string, Object>` parameters toohello constructor.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-294">If you use a `Get` method tooreturn an instance of your component, you must ensure that it passes both hello `Context` and `Dictionary<string, Object>` parameters toohello constructor.</span></span> <span data-ttu-id="7a6b3-295">Hallo volgende voorbeeld is een eenvoudige `Get` methode die deze waarden correct is geslaagd:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-295">hello following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a><span data-ttu-id="7a6b3-296">Hoe tooupdate SCP.NET</span><span class="sxs-lookup"><span data-stu-id="7a6b3-296">How tooupdate SCP.NET</span></span>

<span data-ttu-id="7a6b3-297">Recente versies van SCP.NET ondersteuning pakketupgrade via NuGet.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-297">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="7a6b3-298">Wanneer een nieuwe update beschikbaar is, ontvangt u een upgrade melding.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-298">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="7a6b3-299">toomanually selectievakje voor een upgrade als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-299">toomanually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="7a6b3-300">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-300">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="7a6b3-301">Selecteer in het Hallo-Pakketbeheer **Updates**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-301">From hello package manager, select **Updates**.</span></span> <span data-ttu-id="7a6b3-302">Als een update beschikbaar is, wordt het weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-302">If an update is available, it is listed.</span></span> <span data-ttu-id="7a6b3-303">Klik op **Update** voor Hallo pakket tooinstall deze.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-303">Click **Update** for hello package tooinstall it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a6b3-304">Als uw project is gemaakt met een eerdere versie van SCP.NET die NuGet niet gebruikt, moet u de volgende stappen tooupdate tooa nieuwere versie Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-304">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform hello following steps tooupdate tooa newer version:</span></span>
>
> 1. <span data-ttu-id="7a6b3-305">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-305">In **Solution Explorer**, right-click hello project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="7a6b3-306">Met behulp van Hallo **Search** veld, zoeken en vervolgens toevoegt, **Microsoft.SCP.Net.SDK** toohello project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-306">Using hello **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** toohello project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="7a6b3-307">Algemene problemen met topologieën</span><span class="sxs-lookup"><span data-stu-id="7a6b3-307">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="7a6b3-308">Null-aanwijzer uitzonderingen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-308">Null pointer exceptions</span></span>

<span data-ttu-id="7a6b3-309">Wanneer u van een C#-topologie met een Linux gebaseerde HDInsight-cluster gebruikmaakt, Bolts en onderdelen die gebruikmaken van spout **ConfigurationManager** tooread configuratie-instellingen tijdens runtime kunnen null-aanwijzer uitzonderingen retourneren.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-309">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** tooread configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="7a6b3-310">Hallo-configuratie voor uw project is doorgegeven aan Hallo Storm-topologie als een sleutel-waardepaar in de context van Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-310">hello configuration for your project is passed into hello Storm topology as a key and value pair in hello topology context.</span></span> <span data-ttu-id="7a6b3-311">Het kan worden opgehaald uit Hallo dictionary-object dat wordt doorgegeven tooyour onderdelen wanneer deze worden geïnitialiseerd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-311">It can be retrieved from hello dictionary object that is passed tooyour components when they are initialized.</span></span>

<span data-ttu-id="7a6b3-312">Zie voor meer informatie, Hallo [ConfigurationManager](#configurationmanager) gedeelte van dit document.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-312">For more information, see hello [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="7a6b3-313">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="7a6b3-313">System.TypeLoadException</span></span>

<span data-ttu-id="7a6b3-314">Wanneer u van een C#-topologie met een Linux gebaseerde HDInsight-cluster gebruikmaakt, kunnen Hallo volgende fout optreden:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-314">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter hello following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="7a6b3-315">Deze fout treedt op wanneer u een binair bestand dat niet compatibel met Hallo van .NET-versies die ondersteuning biedt voor Mono gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-315">This error occurs when you use a binary that is not compatible with hello version of .NET that Mono supports.</span></span>

<span data-ttu-id="7a6b3-316">Zorg ervoor dat uw project maakt gebruik van binaire bestanden voor .NET 4.5 compiled Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-316">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="7a6b3-317">Een topologie lokaal testen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-317">Test a topology locally</span></span>

<span data-ttu-id="7a6b3-318">Hoewel het eenvoudig toodeploy een topologie tooa cluster, in sommige gevallen moet u een topologie lokaal tootest.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-318">Although it is easy toodeploy a topology tooa cluster, in some cases, you may need tootest a topology locally.</span></span> <span data-ttu-id="7a6b3-319">Gebruik Hallo toorun stappen te volgen en Hallo voorbeeldtopologie testen in deze zelfstudie lokaal in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-319">Use hello following steps toorun and test hello example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="7a6b3-320">Lokale testen werkt alleen voor basic, C#-topologieën voor alleen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-320">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="7a6b3-321">U de lokale testen voor hybride topologieën of topologieën met meerdere streams niet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-321">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="7a6b3-322">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-322">In **Solution Explorer**, right-click hello project, and select **Properties**.</span></span> <span data-ttu-id="7a6b3-323">Wijzig in de Projecteigenschappen hello, Hallo **type uitvoer** te**consoletoepassing**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-323">In hello project properties, change hello **Output type** too**Console Application**.</span></span>

    ![Schermafbeelding van de Projecteigenschappen met uitvoertype gemarkeerd](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="7a6b3-325">Houd er rekening mee toochange Hallo **type uitvoer** back te maken**Class Library** voordat u Hallo topologie tooa cluster implementeert.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-325">Remember toochange hello **Output type** back too**Class Library** before you deploy hello topology tooa cluster.</span></span>

2. <span data-ttu-id="7a6b3-326">In **Solution Explorer**, met de rechtermuisknop op het Hallo-project en selecteer vervolgens **toevoegen** > **Nieuw Item**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-326">In **Solution Explorer**, right-click hello project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="7a6b3-327">Selecteer **klasse**, en voer **LocalTest.cs** als Hallo klassenaam.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-327">Select **Class**, and enter **LocalTest.cs** as hello class name.</span></span> <span data-ttu-id="7a6b3-328">Tot slot op **toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-328">Finally, click **Add**.</span></span>

3. <span data-ttu-id="7a6b3-329">Open **LocalTest.cs**, en voeg de volgende Hallo **met** instructie Hallo boven:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-329">Open **LocalTest.cs**, and add hello following **using** statement at hello top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="7a6b3-330">Gebruik Hallo volgende code als inhoud Hallo Hallo **LocalTest** klasse:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-330">Use hello following code as hello contents of hello **LocalTest** class:</span></span>

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="7a6b3-331">Een ogenblik tooread via Hallo codeopmerkingen in beslag nemen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-331">Take a moment tooread through hello code comments.</span></span> <span data-ttu-id="7a6b3-332">Deze code gebruikt **LocalContext** toorun Hallo onderdelen in het Hallo-ontwikkelomgeving en zich blijft voordoen Hallo gegevensstroom tussen onderdelen tootext bestanden op de lokale schijf Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-332">This code uses **LocalContext** toorun hello components in hello development environment, and it persists hello data stream between components tootext files on hello local drive.</span></span>

1. <span data-ttu-id="7a6b3-333">Open **Program.cs**, en Voeg na toohello hello **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-333">Open **Program.cs**, and add hello following toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="7a6b3-334">Hallo wijzigingen opslaan en klik vervolgens op **F5** of selecteer **Debug** > **foutopsporing starten** toostart Hallo project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-334">Save hello changes, and then click **F5** or select **Debug** > **Start Debugging** toostart hello project.</span></span> <span data-ttu-id="7a6b3-335">Een consolevenster moet worden weergegeven en meld u aan status als Hallo tests uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-335">A console window should appear, and log status as hello tests progress.</span></span> <span data-ttu-id="7a6b3-336">Wanneer **Tests voltooid** wordt weergegeven, drukt u op een sleutel tooclose Hallo-venster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-336">When **Tests finished** appears, press any key tooclose hello window.</span></span>

3. <span data-ttu-id="7a6b3-337">Gebruik **Windows Verkenner** toolocate Hallo directory met uw project.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-337">Use **Windows Explorer** toolocate hello directory that contains your project.</span></span> <span data-ttu-id="7a6b3-338">Bijvoorbeeld: **C:\Users\<gebruikersnaam > \Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-338">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="7a6b3-339">Open in deze map **Bin**, en klik vervolgens op **Debug**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-339">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="7a6b3-340">U ziet Hallo tekstbestanden die zijn geproduceerd als Hallo tests uitgevoerd: sentences.txt counter.txt en splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-340">You should see hello text files that were produced when hello tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="7a6b3-341">Open elk tekstbestand en Hallo gegevens controleren.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-341">Open each text file and inspect hello data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7a6b3-342">Tekenreeksgegevens zich blijft voordoen als een matrix met decimale waarden in deze bestanden.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-342">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="7a6b3-343">Bijvoorbeeld: \[[97,103,111]] in Hallo **splitter.txt** bestand is Hallo word *en*.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-343">For example, \[[97,103,111]] in hello **splitter.txt** file is hello word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="7a6b3-344">Ervoor tooset Hallo worden **projecttype** back-te**Class Library** voordat u implementeert tooa Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-344">Be sure tooset hello **Project type** back too**Class Library** before deploying tooa Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="7a6b3-345">Logboekgegevens</span><span class="sxs-lookup"><span data-stu-id="7a6b3-345">Log information</span></span>

<span data-ttu-id="7a6b3-346">U kunt eenvoudig gegevens van de onderdelen van uw topologie vastleggen met behulp van `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-346">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="7a6b3-347">Hallo volgende wordt bijvoorbeeld een informatieve logboekvermelding gemaakt:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-347">For example, hello following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="7a6b3-348">Logboekgegevens kan bekeken worden vanuit Hallo **Hadoop-serviceaccount voor aanmelden**, die is gevonden **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-348">Logged information can be viewed from hello **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="7a6b3-349">Vouw Hallo-vermelding voor uw Storm op HDInsight-cluster uit en vouw vervolgens **Hadoop-serviceaccount voor aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-349">Expand hello entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="7a6b3-350">Ten slotte Hallo log-bestand tooview selecteren.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-350">Finally, select hello log file tooview.</span></span>

> [!NOTE]
> <span data-ttu-id="7a6b3-351">Hallo-logboeken worden opgeslagen in hello Azure storage-account dat wordt gebruikt door het cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-351">hello logs are stored in hello Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="7a6b3-352">tooview hello Logboeken in Visual Studio, moet u in Azure-abonnement dat eigenaar is van het opslagaccount Hallo toohello ondertekenen.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-352">tooview hello logs in Visual Studio, you must sign in toohello Azure subscription that owns hello storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="7a6b3-353">Fout-informatie weergeven</span><span class="sxs-lookup"><span data-stu-id="7a6b3-353">View error information</span></span>

<span data-ttu-id="7a6b3-354">tooview fouten die zijn opgetreden in een actieve topologie gebruik Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-354">tooview errors that have occurred in a running topology, use hello following steps:</span></span>

1. <span data-ttu-id="7a6b3-355">Van **Server Explorer**, met de rechtermuisknop op Hallo Storm op HDInsight-cluster en selecteert u **weergave Storm-topologieën**.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-355">From **Server Explorer**, right-click hello Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="7a6b3-356">Voor Hallo **Spout** en **Bolts**, Hallo **laatste fout** kolom bevat informatie over de laatste fout Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-356">For hello **Spout** and **Bolts**, hello **Last Error** column contains information on hello last error.</span></span>

3. <span data-ttu-id="7a6b3-357">Selecteer Hallo **Spout Id** of **Bolt Id** voor Hallo-onderdeel met een fout weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-357">Select hello **Spout Id** or **Bolt Id** for hello component that has an error listed.</span></span> <span data-ttu-id="7a6b3-358">Op de detailpagina Hallo die wordt weergegeven, extra fout informatie wordt weergegeven in Hallo **fouten** sectie Hallo Hallo pagina onderaan in.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-358">On hello details page that is displayed, additional error information is listed in hello **Errors** section at hello bottom of hello page.</span></span>

4. <span data-ttu-id="7a6b3-359">tooobtain meer informatie, selecteer een **poort** van Hallo **Executor** sectie van de pagina hello, toosee Hallo Storm worker logboek voor Hallo laatste paar minuten.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-359">tooobtain more information, select a **Port** from hello **Executors** section of hello page, toosee hello Storm worker log for hello last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="7a6b3-360">Fouten verzonden topologieën</span><span class="sxs-lookup"><span data-stu-id="7a6b3-360">Errors submitting topologies</span></span>

<span data-ttu-id="7a6b3-361">Als er een topologie-tooHDInsight verzenden fouten optreden, kunt u Logboeken vinden voor Hallo serveronderdelen dat de verzending van de topologie op uw HDInsight-cluster te verwerken.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-361">If you encounter errors submitting a topology tooHDInsight, you can find logs for hello server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="7a6b3-362">tooretrieve deze zich aanmeldt, gebruik Hallo volgende opdracht uit vanaf een opdrachtregel:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-362">tooretrieve these logs, use hello following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="7a6b3-363">Vervang __sshuser__ Hello SSH gebruikersaccount voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-363">Replace __sshuser__ with hello SSH user account for hello cluster.</span></span> <span data-ttu-id="7a6b3-364">Vervang __clustername__ met de naam van de HDInsight-cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-364">Replace __clustername__ with hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="7a6b3-365">Voor meer informatie over het gebruik van `scp` en `ssh` met HDInsight, raadpleegt u [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-365">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="7a6b3-366">Voorbeelden kunnen om meerdere redenen mislukken:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-366">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="7a6b3-367">JDK is niet geïnstalleerd of is niet in het Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-367">JDK is not installed or is not in hello path.</span></span>
* <span data-ttu-id="7a6b3-368">Vereiste Java-afhankelijkheden zijn niet opgenomen in Hallo verzending.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-368">Required Java dependencies are not included in hello submission.</span></span>
* <span data-ttu-id="7a6b3-369">Niet-compatibele afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-369">Incompatible dependencies.</span></span>
* <span data-ttu-id="7a6b3-370">Dubbele namen van de topologie.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-370">Duplicate topology names.</span></span>

<span data-ttu-id="7a6b3-371">Als hello `hdinsight-scpwebapi.out` logboek bevat een `FileNotFoundException`, dit wordt mogelijk veroorzaakt door Hallo volgende voorwaarden:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-371">If hello `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by hello following conditions:</span></span>

* <span data-ttu-id="7a6b3-372">Hallo JDK is niet in Hallo-pad op Hallo-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-372">hello JDK is not in hello path on hello development environment.</span></span> <span data-ttu-id="7a6b3-373">Controleer of deze Hallo JDK in Hallo ontwikkelomgeving en die is geïnstalleerd `%JAVA_HOME%/bin` Hallo-pad.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-373">Verify that hello JDK is installed in hello development environment, and that `%JAVA_HOME%/bin` is in hello path.</span></span>
* <span data-ttu-id="7a6b3-374">Ontbreekt er een Java-afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-374">You are missing a Java dependency.</span></span> <span data-ttu-id="7a6b3-375">Zorg ervoor dat u alle vereiste JAR-bestanden als onderdeel van de verzending van hello opneemt.</span><span class="sxs-lookup"><span data-stu-id="7a6b3-375">Make sure you are including any required .jar files as part of hello submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a6b3-376">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7a6b3-376">Next steps</span></span>

<span data-ttu-id="7a6b3-377">Zie voor een voorbeeld van het verwerken van gegevens uit Event Hubs, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-377">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="7a6b3-378">Zie voor een voorbeeld van een C#-topologie die stroomgegevens in meerdere streams splitst [C# Storm-voorbeeld](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-378">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="7a6b3-379">toodiscover meer informatie over het maken van C#-topologieën, Zie [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="7a6b3-379">toodiscover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="7a6b3-380">Zie voor meer manieren toowork met HDInsight en meer Storm op HDInsight voorbeelden Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="7a6b3-380">For more ways toowork with HDInsight and more Storm on HDInsight samples, see hello following documents:</span></span>

<span data-ttu-id="7a6b3-381">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="7a6b3-381">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="7a6b3-382">Programmeerhandleiding voor SCP</span><span class="sxs-lookup"><span data-stu-id="7a6b3-382">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="7a6b3-383">**Apache Storm op HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7a6b3-383">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="7a6b3-384">Implementeren en bewaken topologieën met Apache Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-384">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="7a6b3-385">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-385">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="7a6b3-386">**Apache Hadoop in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7a6b3-386">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="7a6b3-387">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-387">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7a6b3-388">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-388">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7a6b3-389">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-389">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7a6b3-390">**Apache HBase in HDInsight**</span><span class="sxs-lookup"><span data-stu-id="7a6b3-390">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="7a6b3-391">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7a6b3-391">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
