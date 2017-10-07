---
title: aaaRun Sqoop taken met behulp van .NET- en HDInsight - Azure | Microsoft Docs
description: Informatie over hoe toouse HDInsight .NET SDK toorun Sqoop importeren en exporteren tussen een Hadoop-cluster en een Azure SQL database.
keywords: sqoop taak
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Met .NET SDK voor Hadoop in HDInsight Sqoop-taken uitvoeren
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Informatie over hoe toouse HDInsight .NET SDK toorun Sqoop taken in HDInsight tooimport en exporteren tussen een HDInsight-cluster en Azure SQL database of SQL Server-database.

> [!NOTE]
> Hallo stappen in dit artikel kunnen worden gebruikt met ofwel een Windows- of Linux gebaseerde HDInsight-cluster; deze stappen werken echter alleen vanaf een Windows-client. Hallo tabselector op Hallo boven aan dit artikel toochoose andere methoden gebruiken.
> 
> 

### <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een Hadoop-cluster in HDInsight**. Zie [cluster en SQL-database maken](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>Sqoop gebruiken op HDInsight-clusters met .NET SDK
Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET. In deze sectie maakt u een C#-console toepassing tooexport hello hivesampletable toohello SQL-Database tabel die u eerder in deze zelfstudie hebt gemaakt.

## <a name="submit-a-sqoop-job"></a>Verzenden van een taak Sqoop

1. Maak een C#-consoletoepassing in Visual Studio.
2. Voer uit Hallo Visual Studio Package Manager-Console, Hallo Nuget opdracht tooimport Hallo-pakket te volgen.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Hallo na de code in het bestand Program.cs hello gebruiken:
   
        using System.Collections.Generic;
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
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. Druk op **F5** toorun Hallo programma. 

## <a name="limitations"></a>Beperkingen
* Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.
* Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen uitvoert.

## <a name="next-steps"></a>Volgende stappen
Nu u hebt geleerd hoe toouse Sqoop. toolearn meer, Zie:

* [Oozie gebruiken met HDInsight](hdinsight-use-oozie.md): Sqoop gebruiken in een werkstroom Oozie in te grijpen.
* [Vertraging vluchtgegevens met HDInsight analyseren](hdinsight-analyze-flight-delay-data.md): tooanalyze vlucht Hive gebruiken gegevens uit te stellen en vervolgens Sqoop tooexport tooan Azure SQL database te gebruiken.
* [Uploaden van gegevens tooHDInsight](hdinsight-upload-data.md): vinden van andere methoden voor het uploaden van gegevens tooHDInsight/Azure Blob-opslag.

