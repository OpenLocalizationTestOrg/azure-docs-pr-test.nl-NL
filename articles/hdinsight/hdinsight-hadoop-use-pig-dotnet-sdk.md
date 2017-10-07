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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Hallo .NET SDK gebruiken voor Hadoop in HDInsight Pig-taken uitvoeren

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Meer informatie over hoe toouse Hallo .NET SDK voor Hadoop toosubmit Apache Pig tooHadoop in Azure HDInsight taken.

Hallo HDInsight .NET SDK biedt .NET-clientbibliotheken waardoor het gemakkelijker toowork met HDInsight-clusters in .NET. Pig, kunt u toocreate MapReduce-bewerkingen door het modelleren van een reeks gegevenstransformaties. In dit document leert u hoe toouse een basic C#-toepassing toosubmit een Pig taak tooan HDInsight-cluster.

## <a name="prerequisites"></a>Vereisten

toocomplete hello stappen in dit artikel, moet u de volgende Hallo.

* Een Azure HDInsight (Hadoop in HDInsight)-cluster (Windows of Linux-).

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Visual Studio 2012, 2013 of 2015 van 2017.

## <a name="create-hello-application"></a>Hallo-toepassing maken

Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET.

1. Van Hallo **bestand** menu in Visual Studio, selecteer **nieuw** en selecteer vervolgens **Project**.

2. Voor het nieuwe project hello waarden type of selecteer Hallo volgende:

   | Eigenschap | Waarde |
   | ------ | ------ |
   | Category | Templates/Visual C#/Windows |
   | Template | Console Application |
   | Naam | SubmitPigJob |

3. Klik op **OK** toocreate Hallo project.

4. Van Hallo **extra** selecteert u **Library Package Manager** of **Nuget Package Manager**, en selecteer vervolgens **Package Manager Console**.

5. tooinstall hello .NET SDK pakketten Hallo volgende opdracht gebruiken:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. Dubbelklik in Solution Explorer op **Program.cs** tooopen deze. De bestaande code Hallo vervangen door de volgende Hallo.

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

7. Druk op-toepassing hello toostart **F5**.

8. Druk op-toepassing hello tooexit **ENTER**.

## <a name="summary"></a>Samenvatting

Zoals u zien kunt, kunt u Hallo .NET SDK voor Hadoop toocreate .NET-toepassingen die bij het verzenden van Pig-taken tooan HDInsight-cluster en Hallo taakstatus controleren.

## <a name="next-steps"></a>Volgende stappen

Zie voor informatie over Pig in HDInsight, [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).

Zie voor meer informatie over het gebruik van Hadoop in HDInsight Hallo documenten te volgen:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
