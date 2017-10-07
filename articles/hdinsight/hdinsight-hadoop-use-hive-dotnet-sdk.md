---
title: aaaRun Hive-query's met behulp van HDInsight-SDK voor .NET - Azure | Microsoft Docs
description: Meer informatie over hoe toosubmit Hadoop tooAzure HDInsight Hadoop met HDInsight .NET SDK taken.
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Uitvoeren van Hive-query's met HDInsight .NET SDK
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Meer informatie over hoe toosubmit Hive query's met HDInsight .NET SDK. U schrijft een C#-programma toosubmit een Hive-query voor het aanbieden van Hive-tabellen en Hallo resultaten weer te geven.

> [!NOTE]
> Hallo stappen in dit artikel moeten worden uitgevoerd vanuit een Windows-client. Gebruik Hallo tabselector weergegeven op de voorgrond Hallo van Hallo artikel voor informatie over het gebruik van een Linux-, OS X- of Unix-client toowork met Hive.
> 
> 

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende items Hallo hebben:

* **Een Hadoop-cluster in HDInsight**. Zie [aan de slag met Hadoop op basis van Linux in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Indienen van Hive-query's met HDInsight .NET SDK
Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET. 

**tooSubmit taken**

1. Maak een C#-consoletoepassing in Visual Studio.
2. Voer vanuit Hallo Nuget Package Manager-Console, Hallo volgende opdracht:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Hallo volgende code gebruiken:

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
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
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. Druk op **F5** toorun Hallo-toepassing.

Hallo-uitvoer van de toepassing hello zijn vergelijkbaar met:

![Uitvoer van HDInsight Hadoop Hive-taak](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd toocreate met verschillende manieren een HDInsight-cluster. toolearn Zie meer Hallo artikelen te volgen:

* [Aan de slag met Azure HDInsight][hdinsight-get-started]
* [Hadoop-clusters maken in HDInsight][hdinsight-provision]
* [Hadoop-clusters in HDInsight beheren met behulp van hello Azure-portal](hdinsight-administer-use-management-portal.md)
* [HDInsight-SDK voor .NET-verwijzing](https://msdn.microsoft.com/library/mt271028.aspx)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop-mac-linux.md)
* [Toepassingen zonder interactieve verificatie voor .NET HDInsight maken](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


