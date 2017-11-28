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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="df447-104">Met .NET SDK voor Hadoop in HDInsight Sqoop-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="df447-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="df447-105">Informatie over hoe toouse HDInsight .NET SDK toorun Sqoop taken in HDInsight tooimport en exporteren tussen een HDInsight-cluster en Azure SQL database of SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="df447-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="df447-106">Hallo stappen in dit artikel kunnen worden gebruikt met ofwel een Windows- of Linux gebaseerde HDInsight-cluster; deze stappen werken echter alleen vanaf een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="df447-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="df447-107">Hallo tabselector op Hallo boven aan dit artikel toochoose andere methoden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df447-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="df447-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="df447-108">Prerequisites</span></span>
<span data-ttu-id="df447-109">Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="df447-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="df447-110">**Een Hadoop-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="df447-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="df447-111">Zie [cluster en SQL-database maken](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="df447-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="df447-112">Sqoop gebruiken op HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="df447-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="df447-113">Hallo HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het gemakkelijker toowork met HDInsight-clusters in .NET.</span><span class="sxs-lookup"><span data-stu-id="df447-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="df447-114">In deze sectie maakt u een C#-console toepassing tooexport hello hivesampletable toohello SQL-Database tabel die u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="df447-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="df447-115">Verzenden van een taak Sqoop</span><span class="sxs-lookup"><span data-stu-id="df447-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="df447-116">Maak een C#-consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="df447-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="df447-117">Voer uit Hallo Visual Studio Package Manager-Console, Hallo Nuget opdracht tooimport Hallo-pakket te volgen.</span><span class="sxs-lookup"><span data-stu-id="df447-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="df447-118">Hallo na de code in het bestand Program.cs hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="df447-118">Use hello following code in hello Program.cs file:</span></span>
   
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
4. <span data-ttu-id="df447-119">Druk op **F5** toorun Hallo programma.</span><span class="sxs-lookup"><span data-stu-id="df447-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="df447-120">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="df447-120">Limitations</span></span>
* <span data-ttu-id="df447-121">Bulk-export - met Linux gebaseerde HDInsight, Hallo Sqoop connector die wordt gebruikt tooexport gegevens tooMicrosoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="df447-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="df447-122">Batchverwerking - met HDInsight op basis van Linux bij gebruik van Hallo `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van batchverwerking Hallo insert-bewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="df447-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="df447-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="df447-123">Next steps</span></span>
<span data-ttu-id="df447-124">Nu u hebt geleerd hoe toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="df447-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="df447-125">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="df447-125">toolearn more, see:</span></span>

* <span data-ttu-id="df447-126">[Oozie gebruiken met HDInsight](hdinsight-use-oozie.md): Sqoop gebruiken in een werkstroom Oozie in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="df447-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="df447-127">[Vertraging vluchtgegevens met HDInsight analyseren](hdinsight-analyze-flight-delay-data.md): tooanalyze vlucht Hive gebruiken gegevens uit te stellen en vervolgens Sqoop tooexport tooan Azure SQL database te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="df447-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="df447-128">[Uploaden van gegevens tooHDInsight](hdinsight-upload-data.md): vinden van andere methoden voor het uploaden van gegevens tooHDInsight/Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="df447-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

