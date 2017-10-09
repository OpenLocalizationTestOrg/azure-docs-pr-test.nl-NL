---
title: aaaSubmit MapReduce-taken met behulp van HDInsight-SDK voor .NET - Azure | Microsoft Docs
description: Meer informatie over hoe toosubmit MapReduce tooAzure HDInsight Hadoop met HDInsight .NET SDK taken.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="2dead-103">Met HDInsight .NET SDK MapReduce-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2dead-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="2dead-104">Meer informatie over hoe toosubmit MapReduce taken met HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2dead-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="2dead-105">HDInsight clusters worden geleverd met een jar-bestand met voorbeelden van MapReduce.</span><span class="sxs-lookup"><span data-stu-id="2dead-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="2dead-106">Hallo jar-bestand is */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="2dead-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="2dead-107">Een van de voorbeelden Hallo *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="2dead-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="2dead-108">U een C#-console toepassing toosubmit een taak wordcount ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="2dead-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="2dead-109">Hallo taak leest Hallo */example/data/gutenberg/davinci.txt* bestands- en uitvoer Hallo u resultaten te*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="2dead-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="2dead-110">Als u toorerun Hallo toepassing wilt, moet u de uitvoermap Hallo opschonen.</span><span class="sxs-lookup"><span data-stu-id="2dead-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="2dead-111">Hallo stappen in dit artikel moeten worden uitgevoerd vanuit een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="2dead-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="2dead-112">Gebruik Hallo tabselector weergegeven op de voorgrond Hallo van Hallo artikel voor informatie over het gebruik van een Linux-, OS X- of Unix-client toowork met Hive.</span><span class="sxs-lookup"><span data-stu-id="2dead-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2dead-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="2dead-113">Prerequisites</span></span>
<span data-ttu-id="2dead-114">Voordat u dit artikel, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="2dead-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="2dead-115">**Een Hadoop-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="2dead-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="2dead-116">Zie [aan de slag met Hadoop op basis van Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2dead-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="2dead-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="2dead-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="2dead-118">Verzenden van MapReduce-taken met HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2dead-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="2dead-119">Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET.</span><span class="sxs-lookup"><span data-stu-id="2dead-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="2dead-120">**tooSubmit taken**</span><span class="sxs-lookup"><span data-stu-id="2dead-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="2dead-121">Maak een C#-consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2dead-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="2dead-122">Voer vanuit Hallo Nuget Package Manager-Console, Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="2dead-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="2dead-123">Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="2dead-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="2dead-124">Druk op **F5** toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="2dead-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="2dead-125">toorun hello taak opnieuw, moet u Hallo taak uitvoer mapnaam op in de steekproef hello, is het '/ data-voorbeeld/davinciwordcount'.</span><span class="sxs-lookup"><span data-stu-id="2dead-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="2dead-126">Wanneer Hallo-taak voltooid is, afgedrukt Hallo toepassing hello inhoud van het uitvoerbestand Hallo 'onderdeel-r-00000'.</span><span class="sxs-lookup"><span data-stu-id="2dead-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="2dead-127">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2dead-127">Next steps</span></span>
<span data-ttu-id="2dead-128">In dit artikel hebt u geleerd toocreate met verschillende manieren een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="2dead-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="2dead-129">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="2dead-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="2dead-130">Zie voor het indienen van een Hive-taak [uitvoeren Hive-query's met HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="2dead-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="2dead-131">Zie voor het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="2dead-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="2dead-132">Zie voor het beheer van HDInsight-clusters, [beheren Hadoop-clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2dead-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="2dead-133">Zie voor het leren Hallo HDInsight .NET SDK, [HDInsight .NET SDK-naslaginformatie](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="2dead-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="2dead-134">Voor niet-interactieve tooAzure worden geverifieerd, Zie [niet-interactieve verificatie .NET HDInsight-toepassingen maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="2dead-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

