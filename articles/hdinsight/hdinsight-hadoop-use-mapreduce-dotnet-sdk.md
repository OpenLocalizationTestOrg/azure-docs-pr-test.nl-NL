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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Met HDInsight .NET SDK MapReduce-taken uitvoeren
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Meer informatie over hoe toosubmit MapReduce taken met HDInsight .NET SDK. HDInsight clusters worden geleverd met een jar-bestand met voorbeelden van MapReduce. Hallo jar-bestand is */example/jars/hadoop-mapreduce-examples.jar*.  Een van de voorbeelden Hallo *wordcount*. U een C#-console toepassing toosubmit een taak wordcount ontwikkelen.  Hallo taak leest Hallo */example/data/gutenberg/davinci.txt* bestands- en uitvoer Hallo u resultaten te*/example/data/davinciwordcount*.  Als u toorerun Hallo toepassing wilt, moet u de uitvoermap Hallo opschonen.

> [!NOTE]
> Hallo stappen in dit artikel moeten worden uitgevoerd vanuit een Windows-client. Gebruik Hallo tabselector weergegeven op de voorgrond Hallo van Hallo artikel voor informatie over het gebruik van een Linux-, OS X- of Unix-client toowork met Hive.
> 
> 

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende items Hallo hebben:

* **Een Hadoop-cluster in HDInsight**. Zie [aan de slag met Hadoop op basis van Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Verzenden van MapReduce-taken met HDInsight .NET SDK
Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET. 

**tooSubmit taken**

1. Maak een C#-consoletoepassing in Visual Studio.
2. Voer vanuit Hallo Nuget Package Manager-Console, Hallo volgende opdracht:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Hallo volgende code gebruiken:
   
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
4. Druk op **F5** toorun Hallo-toepassing.

toorun hello taak opnieuw, moet u Hallo taak uitvoer mapnaam op in de steekproef hello, is het '/ data-voorbeeld/davinciwordcount'.

Wanneer Hallo-taak voltooid is, afgedrukt Hallo toepassing hello inhoud van het uitvoerbestand Hallo 'onderdeel-r-00000'.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd toocreate met verschillende manieren een HDInsight-cluster. toolearn Zie meer Hallo artikelen te volgen:

* Zie voor het indienen van een Hive-taak [uitvoeren Hive-query's met HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Zie voor het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* Zie voor het beheer van HDInsight-clusters, [beheren Hadoop-clusters in HDInsight](hdinsight-administer-use-portal-linux.md).
* Zie voor het leren Hallo HDInsight .NET SDK, [HDInsight .NET SDK-naslaginformatie](https://msdn.microsoft.com/library/mt271028.aspx).
* Voor niet-interactieve tooAzure worden geverifieerd, Zie [niet-interactieve verificatie .NET HDInsight-toepassingen maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

