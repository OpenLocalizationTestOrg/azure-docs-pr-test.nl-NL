---
title: Sqoop taken met behulp van .NET- en HDInsight - Azure uitvoeren | Microsoft Docs
description: Informatie over het gebruik van HDInsight .NET SDK voor het uitvoeren van Sqoop importeren en exporteren tussen een Hadoop-cluster en een Azure SQL database.
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="46d23-104">Met .NET SDK voor Hadoop in HDInsight Sqoop-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="46d23-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="46d23-105">Informatie over het gebruik van HDInsight .NET SDK Sqoop taken uitvoeren in HDInsight om te importeren en exporteren tussen een HDInsight-cluster en Azure SQL database of SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="46d23-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="46d23-106">De stappen in dit artikel kunnen worden gebruikt met ofwel een Windows- of Linux gebaseerde HDInsight-cluster; deze stappen werken echter alleen vanaf een Windows-client.</span><span class="sxs-lookup"><span data-stu-id="46d23-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="46d23-107">Gebruik de tabselector boven aan dit artikel om andere methoden.</span><span class="sxs-lookup"><span data-stu-id="46d23-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="46d23-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="46d23-108">Prerequisites</span></span>
<span data-ttu-id="46d23-109">Voordat u met deze zelfstudie begint, moet u beschikken over de volgende items:</span><span class="sxs-lookup"><span data-stu-id="46d23-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="46d23-110">**Een Hadoop-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="46d23-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="46d23-111">Zie [cluster en SQL-database maken](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="46d23-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="46d23-112">Sqoop gebruiken op HDInsight-clusters met .NET SDK</span><span class="sxs-lookup"><span data-stu-id="46d23-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="46d23-113">De HDInsight .NET SDK biedt clientbibliotheken .NET, waardoor het makkelijker wordt om te werken met HDInsight-clusters in .NET.</span><span class="sxs-lookup"><span data-stu-id="46d23-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="46d23-114">In deze sectie maakt u een C#-consoletoepassing de hivesampletable exporteren naar de SQL-databasetabel die u eerder in deze zelfstudie hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="46d23-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="46d23-115">Verzenden van een taak Sqoop</span><span class="sxs-lookup"><span data-stu-id="46d23-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="46d23-116">Maak een C#-consoletoepassing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="46d23-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="46d23-117">Voer de volgende Nuget-opdracht voor het importeren van het pakket van Visual Studio Package Manager-Console.</span><span class="sxs-lookup"><span data-stu-id="46d23-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="46d23-118">Gebruik de volgende code in het bestand Program.cs:</span><span class="sxs-lookup"><span data-stu-id="46d23-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="46d23-119">Druk op **F5** het programma uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="46d23-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="46d23-120">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="46d23-120">Limitations</span></span>
* <span data-ttu-id="46d23-121">Bulksgewijs export - met Linux gebaseerde HDInsight, de Sqoop-connector gebruikt voor het exporteren van gegevens naar Microsoft SQL Server of Azure SQL Database biedt momenteel geen ondersteuning voor bulksgewijs invoegen.</span><span class="sxs-lookup"><span data-stu-id="46d23-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="46d23-122">Batchverwerking - met HDInsight op basis van Linux, wanneer u de `-batch` bij het uitvoeren van invoeg-switch, Sqoop meerdere invoegen in plaats van de bewerkingen insert batchverwerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="46d23-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="46d23-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="46d23-123">Next steps</span></span>
<span data-ttu-id="46d23-124">Nu hebt u geleerd hoe Sqoop gebruiken.</span><span class="sxs-lookup"><span data-stu-id="46d23-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="46d23-125">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="46d23-125">To learn more, see:</span></span>

* <span data-ttu-id="46d23-126">[Oozie gebruiken met HDInsight](hdinsight-use-oozie.md): Sqoop gebruiken in een werkstroom Oozie in te grijpen.</span><span class="sxs-lookup"><span data-stu-id="46d23-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="46d23-127">[Vertraging vluchtgegevens met HDInsight analyseren](hdinsight-analyze-flight-delay-data.md): Hive gebruiken voor het analyseren van vlucht gegevens uit te stellen en vervolgens Sqoop gebruiken om gegevens te exporteren naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="46d23-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="46d23-128">[Gegevens uploaden naar HDInsight](hdinsight-upload-data.md): vinden van andere methoden voor het uploaden van gegevens naar HDInsight/Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="46d23-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

