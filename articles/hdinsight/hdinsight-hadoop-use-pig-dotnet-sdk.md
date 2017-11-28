---
title: Apache Pig aaaRun taken met .NET SDK voor Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse .NET SDK Hallo voor Hadoop toosubmit Pig-taken tooHadoop op HDInsight.
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="f0336-103">Hallo .NET SDK gebruiken voor Hadoop in HDInsight Pig-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="f0336-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="f0336-104">Meer informatie over hoe toouse Hallo .NET SDK voor Hadoop toosubmit Apache Pig tooHadoop in Azure HDInsight taken.</span><span class="sxs-lookup"><span data-stu-id="f0336-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="f0336-105">Hallo HDInsight .NET SDK biedt .NET-clientbibliotheken waardoor het gemakkelijker toowork met HDInsight-clusters in .NET.</span><span class="sxs-lookup"><span data-stu-id="f0336-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="f0336-106">Pig, kunt u toocreate MapReduce-bewerkingen door het modelleren van een reeks gegevenstransformaties.</span><span class="sxs-lookup"><span data-stu-id="f0336-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="f0336-107">In dit document leert u hoe toouse een basic C#-toepassing toosubmit een Pig taak tooan HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0336-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0336-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0336-108">Prerequisites</span></span>

<span data-ttu-id="f0336-109">toocomplete hello stappen in dit artikel, moet u de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0336-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="f0336-110">Een Azure HDInsight (Hadoop in HDInsight)-cluster (Windows of Linux-).</span><span class="sxs-lookup"><span data-stu-id="f0336-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f0336-111">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="f0336-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f0336-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="f0336-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="f0336-113">Visual Studio 2012, 2013 of 2015 van 2017.</span><span class="sxs-lookup"><span data-stu-id="f0336-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="f0336-114">Hallo-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="f0336-114">Create hello application</span></span>

<span data-ttu-id="f0336-115">Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET.</span><span class="sxs-lookup"><span data-stu-id="f0336-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="f0336-116">Van Hallo **bestand** menu in Visual Studio, selecteer **nieuw** en selecteer vervolgens **Project**.</span><span class="sxs-lookup"><span data-stu-id="f0336-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="f0336-117">Voor het nieuwe project hello waarden type of selecteer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="f0336-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="f0336-118">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f0336-118">Property</span></span> | <span data-ttu-id="f0336-119">Waarde</span><span class="sxs-lookup"><span data-stu-id="f0336-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="f0336-120">Category</span><span class="sxs-lookup"><span data-stu-id="f0336-120">Category</span></span> | <span data-ttu-id="f0336-121">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="f0336-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="f0336-122">Template</span><span class="sxs-lookup"><span data-stu-id="f0336-122">Template</span></span> | <span data-ttu-id="f0336-123">Console Application</span><span class="sxs-lookup"><span data-stu-id="f0336-123">Console Application</span></span> |
   | <span data-ttu-id="f0336-124">Naam</span><span class="sxs-lookup"><span data-stu-id="f0336-124">Name</span></span> | <span data-ttu-id="f0336-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="f0336-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="f0336-126">Klik op **OK** toocreate Hallo project.</span><span class="sxs-lookup"><span data-stu-id="f0336-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="f0336-127">Van Hallo **extra** selecteert u **Library Package Manager** of **Nuget Package Manager**, en selecteer vervolgens **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="f0336-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="f0336-128">tooinstall hello .NET SDK pakketten Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="f0336-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="f0336-129">Dubbelklik in Solution Explorer op **Program.cs** tooopen deze.</span><span class="sxs-lookup"><span data-stu-id="f0336-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="f0336-130">De bestaande code Hallo vervangen door de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="f0336-130">Replace hello existing code with hello following.</span></span>

    ```csharp
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;

    namespace SubmitHDInsightJobDotNet
    {
        class Program
        {
            private static HDInsightJobManagementClient _hdiJobManagementClient;

            private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
            private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
            private const string ExistingClusterUsername = "<Cluster Username>";
            private const string ExistingClusterPassword = "<Cluster User Password>";

            static void Main(string[] args)
            {
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="f0336-131">Druk op-toepassing hello toostart **F5**.</span><span class="sxs-lookup"><span data-stu-id="f0336-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="f0336-132">Druk op-toepassing hello tooexit **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="f0336-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="f0336-133">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="f0336-133">Summary</span></span>

<span data-ttu-id="f0336-134">Zoals u zien kunt, kunt u Hallo .NET SDK voor Hadoop toocreate .NET-toepassingen die bij het verzenden van Pig-taken tooan HDInsight-cluster en Hallo taakstatus controleren.</span><span class="sxs-lookup"><span data-stu-id="f0336-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0336-135">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0336-135">Next steps</span></span>

<span data-ttu-id="f0336-136">Zie voor informatie over Pig in HDInsight, [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="f0336-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="f0336-137">Zie voor meer informatie over het gebruik van Hadoop in HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="f0336-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="f0336-138">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0336-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f0336-139">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0336-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
