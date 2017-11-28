---
title: "Op basis van tijd Hadoop Oozie-coördinator gebruiken in HDInsight | Microsoft Docs"
description: "Op basis van tijd Hadoop Oozie-coördinator gebruiken in HDInsight, een big data-service. Informatie over het definiëren van Oozie-werkstromen en coördinator en verzenden van taken."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00c3a395-d51a-44ff-af2d-1f116c4b1c83
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 600a70c74a16e2601a874f804ac2e8382c8bfa90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-to-define-workflows-and-coordinate-jobs"></a><span data-ttu-id="d2b7b-104">Tijd gebaseerde Oozie-coördinator gebruiken met Hadoop in HDInsight voor het definiëren van werkstromen en coördineren van taken</span><span class="sxs-lookup"><span data-stu-id="d2b7b-104">Use time-based Oozie coordinator with Hadoop in HDInsight to define workflows and coordinate jobs</span></span>
<span data-ttu-id="d2b7b-105">In dit artikel leert u hoe u werkstromen en coördinator definiëren en het activeren van de coördinator-taken op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-105">In this article, you'll learn how to define workflows and coordinators, and how to trigger the coordinator jobs, based on time.</span></span> <span data-ttu-id="d2b7b-106">Is het handig om te gaan via [Oozie gebruiken met HDInsight] [ hdinsight-use-oozie] voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-106">It is helpful to go through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="d2b7b-107">Naast Oozie, kunt u ook taken met behulp van Azure Data Factory plannen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-107">In addition to Oozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="d2b7b-108">Zie voor meer informatie over Azure Data Factory, [Use Pig en Hive met Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-108">To learn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d2b7b-109">In dit artikel is een cluster met HDInsight op basis van Windows vereist.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="d2b7b-110">Zie voor meer informatie over het gebruik van Oozie, met inbegrip van taken op basis van tijd op een cluster op basis van Linux [Oozie gebruiken met Hadoop om te definiëren en uitvoeren van een werkstroom op Linux gebaseerde HDInsight](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="d2b7b-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="d2b7b-111">Wat is Oozie</span><span class="sxs-lookup"><span data-stu-id="d2b7b-111">What is Oozie</span></span>
<span data-ttu-id="d2b7b-112">Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="d2b7b-113">Het is geïntegreerd met de Hadoop-stack en Hadoop-taken voor Apache MapReduce, Apache Pig, Apache Hive en Apache Sqoop ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-113">It is integrated with the Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="d2b7b-114">Het kan ook worden gebruikt voor het plannen van taken die specifiek voor een systeem, zoals Java-programma's of shell-scripts zijn.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-114">It can also be used to schedule jobs that are specific to a system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="d2b7b-115">De volgende afbeelding ziet u de werkstroom die u wilt implementeren:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-115">The following image shows the workflow you will implement:</span></span>

![Werkstroomdiagram][img-workflow-diagram]

<span data-ttu-id="d2b7b-117">De workflow bevat twee acties:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-117">The workflow contains two actions:</span></span>

1. <span data-ttu-id="d2b7b-118">Een Hive-actie wordt een HiveQL-script voor het tellen van elk type logboek-niveau in een logboekbestand log4j uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-118">A Hive action runs a HiveQL script to count the occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="d2b7b-119">Elk logboek log4j bestaat uit een line-of velden met een veld [LOGBOEKNIVEAU] als u wilt weergeven van het type en de ernst, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field to show the type and the severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="d2b7b-120">De uitvoer van de Hive-script is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-120">The Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="d2b7b-121">Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="d2b7b-122">Een actie Sqoop exporteert u de uitvoer van de actie HiveQL naar een tabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-122">A Sqoop action exports the HiveQL action output to a table in an Azure SQL database.</span></span> <span data-ttu-id="d2b7b-123">Zie voor meer informatie over Sqoop [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="d2b7b-124">Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in de clusterversies geleverd door HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-124">For supported Oozie versions on HDInsight clusters, see [What's new in the cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="d2b7b-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d2b7b-125">Prerequisites</span></span>
<span data-ttu-id="d2b7b-126">Voordat u met deze zelfstudie begint, moet u het volgende hebben of hebben gedaan:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-126">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="d2b7b-127">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d2b7b-128">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en verdwijnt per 1 januari 2017.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="d2b7b-129">In de stappen in dit document worden de nieuwe HDInsight-cmdlets gebruikt die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-129">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="d2b7b-130">Volg de stappen in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Azure PowerShell installeren en configureren) als u de nieuwste versie van Azure PowerShell wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-130">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="d2b7b-131">Als u scripts hebt die moeten worden gewijzigd om ze te kunnen gebruiken met de nieuwe cmdlets die werken met Azure Resource Manager, raadpleegt u [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migreren naar op Azure Resource Manager gebaseerde hulpprogramma’s voor HDInsight-clusters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-131">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="d2b7b-132">**Een HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="d2b7b-133">Zie voor meer informatie over het maken van een HDInsight-cluster [HDInsight-clusters maken][hdinsight-provision], of [aan de slag met HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="d2b7b-134">U moet de volgende gegevens om de zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-134">You will need the following data to go through the tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d2b7b-135">Cluster-eigenschap</span><span class="sxs-lookup"><span data-stu-id="d2b7b-135">Cluster property</span></span></th><th><span data-ttu-id="d2b7b-136">Naam variabele voor Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2b7b-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="d2b7b-137">Waarde</span><span class="sxs-lookup"><span data-stu-id="d2b7b-137">Value</span></span></th><th><span data-ttu-id="d2b7b-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d2b7b-139">De naam van de HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="d2b7b-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="d2b7b-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="d2b7b-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="d2b7b-141">Het HDInsight-cluster op waarop u deze zelfstudie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-141">The HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-142">Gebruikersnaam voor HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="d2b7b-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="d2b7b-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="d2b7b-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="d2b7b-144">De naam van de gebruiker in de HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-144">The HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="d2b7b-145">HDInsight-cluster gebruikerswachtwoord</span><span class="sxs-lookup"><span data-stu-id="d2b7b-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="d2b7b-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="d2b7b-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="d2b7b-147">Het wachtwoord van de gebruiker in de HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-147">The HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-148">Naam van het Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="d2b7b-148">Azure storage account name</span></span></td><td><span data-ttu-id="d2b7b-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="d2b7b-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="d2b7b-150">Een Azure Storage-account beschikbaar is voor het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-150">An Azure Storage account available to the HDInsight cluster.</span></span> <span data-ttu-id="d2b7b-151">Gebruik het standaardopslagaccount die u hebt opgegeven tijdens het inrichten van het cluster voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-151">For this tutorial, use the default storage account that you specified during the cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-152">Naam van een Azure Blob-container</span><span class="sxs-lookup"><span data-stu-id="d2b7b-152">Azure Blob container name</span></span></td><td><span data-ttu-id="d2b7b-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="d2b7b-153">$containerName</span></span></td><td></td><td><span data-ttu-id="d2b7b-154">Voor dit voorbeeld gebruikt u de Azure Blob storage-container die wordt gebruikt voor het standaardbestandssysteem HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-154">For this example, use the Azure Blob storage container that is used for the default HDInsight cluster file system.</span></span> <span data-ttu-id="d2b7b-155">Standaard is deze dezelfde naam als het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-155">By default, it has the same name as the HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="d2b7b-156">
* **Een Azure SQL database**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="d2b7b-157">U moet een firewallregel voor de SQL-databaseserver toegang toestaan via uw werkstation configureren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-157">You must configure a firewall rule for the SQL Database server to allow access from your workstation.</span></span> <span data-ttu-id="d2b7b-158">Zie voor instructies over het maken van een Azure SQL database en de firewall configureren [aan de slag met Azure SQL database] [SQL-get-started].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-158">For instructions about creating an Azure SQL database and configuring the firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="d2b7b-159">Dit artikel vindt een Windows PowerShell-script voor het maken van de Azure SQL database-tabel die u nodig hebt voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-159">This article provides a Windows PowerShell script for creating the Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d2b7b-160">SQL database-eigenschap</span><span class="sxs-lookup"><span data-stu-id="d2b7b-160">SQL database property</span></span></th><th><span data-ttu-id="d2b7b-161">Naam variabele voor Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2b7b-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="d2b7b-162">Waarde</span><span class="sxs-lookup"><span data-stu-id="d2b7b-162">Value</span></span></th><th><span data-ttu-id="d2b7b-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d2b7b-164">SQL server-databasenaam</span><span class="sxs-lookup"><span data-stu-id="d2b7b-164">SQL database server name</span></span></td><td><span data-ttu-id="d2b7b-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="d2b7b-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="d2b7b-166">De SQL-databaseserver waarnaar Sqoop gegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-166">The SQL database server to which Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="d2b7b-167">Aanmeldingsnaam voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="d2b7b-167">SQL database login name</span></span></td><td><span data-ttu-id="d2b7b-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="d2b7b-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="d2b7b-169">Aanmeldingsnaam van de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-170">Aanmeldingswachtwoord voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="d2b7b-170">SQL database login password</span></span></td><td><span data-ttu-id="d2b7b-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="d2b7b-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="d2b7b-172">Aanmeldingswachtwoord voor SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-173">Naam van de SQL-database</span><span class="sxs-lookup"><span data-stu-id="d2b7b-173">SQL database name</span></span></td><td><span data-ttu-id="d2b7b-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="d2b7b-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="d2b7b-175">De Azure SQL database waarnaar Sqoop gegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-175">The Azure SQL database to which Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="d2b7b-176">Standaard wordt in een Azure SQL database verbindingen toelaat van Azure-Services, zoals Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="d2b7b-177">Als deze firewallinstelling is uitgeschakeld, moet u het inschakelen van de Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-177">If this firewall setting is disabled, you must enable it from the Azure Portal.</span></span> <span data-ttu-id="d2b7b-178">Zie voor instructies over het maken van een SQL-Database en firewallregels configureren [maken en configureren van de SQL-Database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="d2b7b-179">Invullen de waarden in de tabellen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-179">Fill-in the values in the tables.</span></span> <span data-ttu-id="d2b7b-180">Dit is handig voor het doorlopen van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-the-related-hiveql-script"></a><span data-ttu-id="d2b7b-181">Oozie-werkstroom en het bijbehorende HiveQL-script definiëren</span><span class="sxs-lookup"><span data-stu-id="d2b7b-181">Define Oozie workflow and the related HiveQL script</span></span>
<span data-ttu-id="d2b7b-182">Oozie werkstromen definities worden geschreven in hPDL (een XML-proces definition language).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="d2b7b-183">De standaardnaam van de werkstroom is *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-183">The default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="d2b7b-184">U een bestand van de werkstroom lokaal opslaan en vervolgens naar het HDInsight-cluster implementeren met behulp van Azure PowerShell verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-184">You will save the workflow file locally, and then deploy it to the HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="d2b7b-185">De Hive-bewerking in de werkstroom aangeroepen door een scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-185">The Hive action in the workflow calls a HiveQL script file.</span></span> <span data-ttu-id="d2b7b-186">Dit scriptbestand bevat drie HiveQL-instructies:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="d2b7b-187">**De instructie DROP TABLE** de log4j Hive-tabel wordt verwijderd als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-187">**The DROP TABLE statement** deletes the log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="d2b7b-188">**De instructie CREATE TABLE** maakt een log4j Hive externe tabel naar de locatie van het logboekbestand log4j verwijst;</span><span class="sxs-lookup"><span data-stu-id="d2b7b-188">**The CREATE TABLE statement** creates a log4j Hive external table, which points to the location of the log4j log file;</span></span>
3. <span data-ttu-id="d2b7b-189">**De locatie van het logboekbestand log4j**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-189">**The location of the log4j log file**.</span></span> <span data-ttu-id="d2b7b-190">Het veldscheidingsteken is ",".</span><span class="sxs-lookup"><span data-stu-id="d2b7b-190">The field delimiter is ",".</span></span> <span data-ttu-id="d2b7b-191">Het scheidingsteken voor regel is '\n'.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-191">The default line delimiter is "\n".</span></span> <span data-ttu-id="d2b7b-192">Een externe Hive-tabel wordt om te voorkomen dat het bestand wordt verwijderd uit de oorspronkelijke locatie, als u wilt uitvoeren van de werkstroom Oozie meerdere keren gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-192">A Hive external table is used to avoid the data file being removed from the original location, in case you want to run the Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="d2b7b-193">**De instructie INSERT OVERSCHRIJVEN** telt het aantal instanties van elk type logboek-niveau van de log4j Hive-tabel en de uitvoer wordt opgeslagen naar een Azure Blob storage-locatie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-193">**The INSERT OVERWRITE statement** counts the occurrences of each log-level type from the log4j Hive table, and it saves the output to an Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b7b-194">Er is een bekend probleem voor Hive-pad.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-194">There is a known Hive path issue.</span></span> <span data-ttu-id="d2b7b-195">Voert u dit probleem is opgetreden bij het indienen van een Oozie-taak.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="d2b7b-196">De instructies voor het verhelpen van het probleem kunnen u vinden op de TechNet-Wiki: [HDInsight Hive-fout: kan de naam van][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-196">The instructions for fixing the issue can be found on the TechNet Wiki: [HDInsight Hive error: Unable to rename][technetwiki-hive-error].</span></span>

<span data-ttu-id="d2b7b-197">**Het scriptbestand HiveQL moet worden aangeroepen door de werkstroom definiëren**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-197">**To define the HiveQL script file to be called by the workflow**</span></span>

1. <span data-ttu-id="d2b7b-198">Maak een tekstbestand met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-198">Create a text file with the following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="d2b7b-199">Er zijn drie variabelen die worden gebruikt in het script:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-199">There are three variables used in the script:</span></span>

   * <span data-ttu-id="d2b7b-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-200">${hiveTableName}</span></span>
   * <span data-ttu-id="d2b7b-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="d2b7b-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="d2b7b-203">De werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden aan dit HiveQL-script tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-203">The workflow definition file (workflow.xml in this tutorial) will pass these values to this HiveQL script at run time.</span></span>
2. <span data-ttu-id="d2b7b-204">Sla het bestand als **C:\Tutorials\UseOozie\useooziewf.hql** met behulp van ANSI (ASCII) codering.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-204">Save the file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d2b7b-205">(Kladblok gebruiken als uw teksteditor deze optie niet.) Dit scriptbestand wordt verderop in de zelfstudie voor het HDInsight-cluster worden geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed to the HDInsight cluster later in the tutorial.</span></span>

<span data-ttu-id="d2b7b-206">**Voor het definiëren van een werkstroom**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-206">**To define a workflow**</span></span>

1. <span data-ttu-id="d2b7b-207">Maak een tekstbestand met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-207">Create a text file with the following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>

        <action name="RunHiveScript">
            <hive xmlns="uri:oozie:hive-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.job.queue.name</name>
                        <value>${queueName}</value>
                    </property>
                </configuration>
                <script>${hiveScript}</script>
                <param>hiveTableName=${hiveTableName}</param>
                <param>hiveDataFolder=${hiveDataFolder}</param>
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
            </hive>
            <ok to="RunSqoopExport"/>
            <error to="fail"/>
        </action>

        <action name="RunSqoopExport">
            <sqoop xmlns="uri:oozie:sqoop-action:0.2">
                <job-tracker>${jobTracker}</job-tracker>
                <name-node>${nameNode}</name-node>
                <configuration>
                    <property>
                        <name>mapred.compress.map.output</name>
                        <value>true</value>
                    </property>
                </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="d2b7b-208">Er zijn twee acties die zijn gedefinieerd in de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-208">There are two actions defined in the workflow.</span></span> <span data-ttu-id="d2b7b-209">De actie start voor *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-209">The start-to action is *RunHiveScript*.</span></span> <span data-ttu-id="d2b7b-210">Als u de actie uitvoert *OK*, is de volgende actie *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-210">If the action runs *OK*, the next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="d2b7b-211">De RunHiveScript heeft meerdere variabelen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-211">The RunHiveScript has several variables.</span></span> <span data-ttu-id="d2b7b-212">U geeft de waarden bij het verzenden van de taak Oozie vanuit uw werkstation met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-212">You will pass the values when you submit the Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="d2b7b-213">Werkstroomvariabelen</span><span class="sxs-lookup"><span data-stu-id="d2b7b-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d2b7b-214">Werkstroomvariabelen</span><span class="sxs-lookup"><span data-stu-id="d2b7b-214">Workflow variables</span></span></th><th><span data-ttu-id="d2b7b-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d2b7b-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-216">${jobTracker}</span></span></td><td><span data-ttu-id="d2b7b-217">Geef de URL van de taak Hadoop vastleggen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-217">Specify the URL of the Hadoop job tracker.</span></span> <span data-ttu-id="d2b7b-218">Gebruik <strong>jobtrackerhost:9010</strong> cluster in HDInsight versie 3.0 en 2.0.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-219">${nameNode}</span></span></td><td><span data-ttu-id="d2b7b-220">Geef de URL van het knooppunt Hadoop-naam.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-220">Specify the URL of the Hadoop name node.</span></span> <span data-ttu-id="d2b7b-221">Gebruik van de standaard bestand system wasb: / / adres, bijvoorbeeld <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-221">Use the default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-222">${Wachtrijnaam}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-222">${queueName}</span></span></td><td><span data-ttu-id="d2b7b-223">Hiermee geeft u de naam van de wachtrij die de taak te worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-223">Specifies the queue name that the job will be submitted to.</span></span> <span data-ttu-id="d2b7b-224">Gebruik <strong>standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="d2b7b-225">Variabelen voor hive</span><span class="sxs-lookup"><span data-stu-id="d2b7b-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d2b7b-226">Hive actie variabele</span><span class="sxs-lookup"><span data-stu-id="d2b7b-226">Hive action variable</span></span></th><th><span data-ttu-id="d2b7b-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d2b7b-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="d2b7b-229">De bronmap voor de opdracht Create Table Hive.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-229">The source directory for the Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="d2b7b-231">De uitvoermap voor de instructie INSERT OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-231">The output folder for the INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-232">${hiveTableName}</span></span></td><td><span data-ttu-id="d2b7b-233">De naam van de Hive-tabel die verwijst naar de gegevensbestanden log4j.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-233">The name of the Hive table that references the log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="d2b7b-234">Variabelen voor de Sqoop</span><span class="sxs-lookup"><span data-stu-id="d2b7b-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="d2b7b-235">Sqoop actie variabele</span><span class="sxs-lookup"><span data-stu-id="d2b7b-235">Sqoop action variable</span></span></th><th><span data-ttu-id="d2b7b-236">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="d2b7b-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="d2b7b-238">Verbindingstekenreeks van de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="d2b7b-240">De Azure SQL-databasetabel aan waar de gegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-240">The Azure SQL database table to where the data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="d2b7b-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="d2b7b-242">De uitvoermap voor de instructie Hive invoegen OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-242">The output folder for the Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="d2b7b-243">Dit is dezelfde map voor het exporteren van Sqoop (export-dir).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-243">This is the same folder for the Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="d2b7b-244">Zie voor meer informatie over Oozie-werkstroom en het gebruik van de werkstroomacties [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie ] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-244">For more information about Oozie workflow and using the workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="d2b7b-245">Sla het bestand als **C:\Tutorials\UseOozie\workflow.xml** met behulp van ANSI (ASCII) codering.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-245">Save the file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d2b7b-246">(Kladblok gebruiken als uw teksteditor deze optie niet.)</span><span class="sxs-lookup"><span data-stu-id="d2b7b-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="d2b7b-247">**Coördinator definiëren**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-247">**To define coordinator**</span></span>

1. <span data-ttu-id="d2b7b-248">Maak een tekstbestand met de volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-248">Create a text file with the following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="d2b7b-249">Er zijn vijf variabelen die worden gebruikt in het definitiebestand:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-249">There are five variables used in the definition file:</span></span>

   | <span data-ttu-id="d2b7b-250">Variabele</span><span class="sxs-lookup"><span data-stu-id="d2b7b-250">Variable</span></span> | <span data-ttu-id="d2b7b-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d2b7b-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="d2b7b-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-252">${coordFrequency}</span></span> |<span data-ttu-id="d2b7b-253">Taak onderbreken tijd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-253">Job pause time.</span></span> <span data-ttu-id="d2b7b-254">Frequentie wordt altijd uitgedrukt in minuten.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="d2b7b-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-255">${coordStart}</span></span> |<span data-ttu-id="d2b7b-256">Begintijd van taak.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-256">Job start time.</span></span> |
   | <span data-ttu-id="d2b7b-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-257">${coordEnd}</span></span> |<span data-ttu-id="d2b7b-258">Eindtijd van de taak.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-258">Job end time.</span></span> |
   | <span data-ttu-id="d2b7b-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-259">${coordTimezone}</span></span> |<span data-ttu-id="d2b7b-260">Oozie verwerkt taken in een vaste tijdzone coordinator met geen zomertijd (doorgaans weergegeven met behulp UTC).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="d2b7b-261">Deze tijdzone wordt verwezen als de "Oozie verwerking tijdzone."</span><span class="sxs-lookup"><span data-stu-id="d2b7b-261">This time zone is referred as the "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="d2b7b-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="d2b7b-262">${wfPath}</span></span> |<span data-ttu-id="d2b7b-263">Het pad voor de workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-263">The path for the workflow.xml.</span></span>  <span data-ttu-id="d2b7b-264">Als de naam van de werkstroom is niet de standaardnaam (workflow.xml), moet u deze opgeven.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-264">If the workflow file name is not the default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="d2b7b-265">Sla het bestand als **C:\Tutorials\UseOozie\coordinator.xml** met behulp van de ANSI (ASCII)-codering.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-265">Save the file as **C:\Tutorials\UseOozie\coordinator.xml** by using the ANSI (ASCII) encoding.</span></span> <span data-ttu-id="d2b7b-266">(Kladblok gebruiken als uw teksteditor deze optie niet.)</span><span class="sxs-lookup"><span data-stu-id="d2b7b-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-the-oozie-project-and-prepare-the-tutorial"></a><span data-ttu-id="d2b7b-267">Het project Oozie implementeren en voorbereiden van de zelfstudie</span><span class="sxs-lookup"><span data-stu-id="d2b7b-267">Deploy the Oozie project and prepare the tutorial</span></span>
<span data-ttu-id="d2b7b-268">U kunt een Azure PowerShell-script voor het uitvoeren van de volgende wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-268">You will run an Azure PowerShell script to perform the following:</span></span>

* <span data-ttu-id="d2b7b-269">Kopieer het HiveQL-script (useoozie.hql) naar Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-269">Copy the HiveQL script (useoozie.hql) to Azure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="d2b7b-270">Kopieer workflow.xml naar wasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-270">Copy workflow.xml to wasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="d2b7b-271">Kopieer coordinator.xml naar wasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-271">Copy coordinator.xml to wasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="d2b7b-272">Kopieer het bestand (/ example/data/sample.log) naar wasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-272">Copy the data file (/example/data/sample.log) to wasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="d2b7b-273">Maak een Azure SQL-databasetabel voor het opslaan van gegevens van Sqoop exporteren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="d2b7b-274">De tabelnaam van de is *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-274">The table name is *log4jLogCount*.</span></span>

<span data-ttu-id="d2b7b-275">**Inzicht in HDInsight-opslag**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="d2b7b-276">HDInsight gebruikt Azure Blob-opslag voor gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="d2b7b-277">wasb: / / is Microsoft implementatie van het Hadoop distributed file system (HDFS) in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-277">wasb:// is Microsoft's implementation of the Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="d2b7b-278">Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d2b7b-279">Wanneer u een HDInsight-cluster inrichten, is een Azure Blob storage-account en een specifieke container uit dat account aangewezen als het standaardbestandssysteem zoals in HDFS.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as the default file system, like in HDFS.</span></span> <span data-ttu-id="d2b7b-280">Naast dit opslagaccount, kunt u toevoegen extra opslagaccounts van dezelfde Azure-abonnement of van verschillende Azure-abonnementen tijdens het inrichtingsproces.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-280">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or from different Azure subscriptions during the provisioning process.</span></span> <span data-ttu-id="d2b7b-281">Zie voor instructies over het toevoegen van extra opslagaccounts [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="d2b7b-282">Om te vereenvoudigen de Azure PowerShell-script in deze zelfstudie gebruikt, worden alle bestanden opgeslagen in de systeemcontainer van de standaard-bestand zich bevindt op *zelfstudies/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-282">To simplify the Azure PowerShell script used in this tutorial, all of the files are stored in the default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="d2b7b-283">Deze container heeft dezelfde naam als de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-283">By default, this container has the same name as the HDInsight cluster name.</span></span>
<span data-ttu-id="d2b7b-284">De syntaxis is:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-284">The syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="d2b7b-285">Alleen de *wasb: / /* syntaxis wordt ondersteund in HDInsight-cluster versie 3.0.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-285">Only the *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="d2b7b-286">De oudere *asv: / /* syntaxis wordt ondersteund in HDInsight 2.1 en 1.6-clusters, maar wordt niet ondersteund in HDInsight 3.0-clusters.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-286">The older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="d2b7b-287">De wasb: / / pad is een virtueel pad.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-287">The wasb:// path is a virtual path.</span></span> <span data-ttu-id="d2b7b-288">Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="d2b7b-289">Een bestand dat is opgeslagen in de container met standaard toegankelijk zijn vanuit HDInsight met behulp van de volgende URI's (ik gebruik workflow.xml als voorbeeld):</span><span class="sxs-lookup"><span data-stu-id="d2b7b-289">A file that is stored in the default file system container can be accessed from HDInsight by using any of the following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="d2b7b-290">Als u toegang tot het bestand rechtstreeks vanuit het opslagaccount wilt, wordt de blob-naam voor het bestand is:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-290">If you want to access the file directly from the storage account, the blob name for the file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="d2b7b-291">**De interne en externe tabellen Hive begrijpen**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="d2b7b-292">Er zijn een aantal dingen die u wilt weten over Hive interne en externe tabellen:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-292">There are a few things you need to know about Hive internal and external tables:</span></span>

* <span data-ttu-id="d2b7b-293">De opdracht CREATE TABLE maakt u een interne tabel, ook wel bekend als een beheerde tabel.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-293">The CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="d2b7b-294">De gegevensbestand moet zich in de standaard-container.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-294">The data file must be located in the default container.</span></span>
* <span data-ttu-id="d2b7b-295">De opdracht CREATE TABLE het bestand verplaatst naar de/hive/datawarehouse/<TableName> map in de standaard-container.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-295">The CREATE TABLE command moves the data file to the /hive/warehouse/<TableName> folder in the default container.</span></span>
* <span data-ttu-id="d2b7b-296">De externe tabel maken opdracht maakt u een externe tabel.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-296">The CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="d2b7b-297">Het gegevensbestand kan buiten de standaardcontainer zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-297">The data file can be located outside the default container.</span></span>
* <span data-ttu-id="d2b7b-298">De externe tabel maken-opdracht verplaatst niet het bestand.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-298">The CREATE EXTERNAL TABLE command does not move the data file.</span></span>
* <span data-ttu-id="d2b7b-299">De externe tabel maken-opdracht toegestaan niet in alle submappen onder de map die is opgegeven in de component locatie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-299">The CREATE EXTERNAL TABLE command doesn't allow any subfolders under the folder that is specified in the LOCATION clause.</span></span> <span data-ttu-id="d2b7b-300">Dit is de reden waarom de zelfstudie een kopie van het bestand sample.log wordt.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-300">This is the reason why the tutorial makes a copy of the sample.log file.</span></span>

<span data-ttu-id="d2b7b-301">Zie voor meer informatie [HDInsight: Hive interne en externe tabellen Intro][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="d2b7b-302">**Voorbereiden van de zelfstudie**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-302">**To prepare the tutorial**</span></span>

1. <span data-ttu-id="d2b7b-303">Open de Windows PowerShell ISE (Typ in het Windows 8 startscherm **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-303">Open the Windows PowerShell ISE (in the Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="d2b7b-304">Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="d2b7b-305">Voer de volgende opdracht verbinding maken met uw Azure-abonnement in het deelvenster onderaan:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-305">In the bottom pane, run the following command to connect to your Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="d2b7b-306">U wordt gevraagd de referenties van uw Azure-account in te voeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-306">You will be prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="d2b7b-307">Deze methode voor het toevoegen van een abonnementsverbinding een time-out optreedt en na 12 uur, heeft u de cmdlet opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-307">This method of adding a subscription connection times out, and after 12 hours, you will have to run the cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d2b7b-308">Als u meerdere Azure-abonnementen hebt en het standaardabonnement niet de versie die u wilt gebruiken is, gebruiken de <strong>Select-AzureSubscription</strong> cmdlet om een abonnement te selecteren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-308">If you have multiple Azure subscriptions and the default subscription is not the one you want to use, use the <strong>Select-AzureSubscription</strong> cmdlet to select a subscription.</span></span>

3. <span data-ttu-id="d2b7b-309">Kopieer het volgende script in het scriptvenster en stel op de eerste zes variabelen:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-309">Copy the following script into the script pane, and then set the first six variables:</span></span>

    ```powershell
    # WASB variables
    $storageAccountName = "<StorageAccountName>"
    $containerName = "<BlobStorageContainerName>"

    # SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    # Oozie files for the tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing the Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use the long path here
    ```

    <span data-ttu-id="d2b7b-310">Zie voor meer beschrijvingen van de variabelen de [vereisten](#prerequisites) sectie in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-310">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="d2b7b-311">De volgende toevoegen aan het script in het scriptvenster:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-311">Append the following to the script in the script pane:</span></span>

    ```powershell
    # Create a storage context object
    $storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

    function uploadOozieFiles()
    {
        Write-Host "Copy HiveQL script, workflow definition and coordinator definition ..." -ForegroundColor Green
        Set-AzureStorageBlobContent -File $hiveQLScript -Container $containerName -Blob "$destFolder/useooziewf.hql" -Context $destContext
        Set-AzureStorageBlobContent -File $workflowDefinition -Container $containerName -Blob "$destFolder/workflow.xml" -Context $destContext
        Set-AzureStorageBlobContent -File $coordDefinition -Container $containerName -Blob "$destFolder/coordinator.xml" -Context $destContext
    }

    function prepareHiveDataFile()
    {
        Write-Host "Make a copy of the sample.log file ... " -ForegroundColor Green
        Start-CopyAzureStorageBlob -SrcContainer $containerName -SrcBlob "example/data/sample.log" -Context $destContext -DestContainer $containerName -destBlob "$destFolder/data/sample.log" -DestContext $destContext
    }

    function prepareSQLDatabase()
    {
        # SQL query string for creating log4jLogsCount table
        $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [Level] [nvarchar](10) NOT NULL,
                [Total] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
            [Level] ASC
            )
            )"

        #Create the log4jLogsCount table
        Write-Host "Create Log4jLogsCount table ..." -ForegroundColor Green
        $conn = New-Object System.Data.SqlClient.SqlConnection
        $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
        $conn.open()
        $cmd = New-Object System.Data.SqlClient.SqlCommand
        $cmd.connection = $conn
        $cmd.commandtext = $cmdCreateLog4jCountTable
        $cmd.executenonquery()

        $conn.close()
    }

    # upload workflow.xml, coordinator.xml, and ooziewf.hql
    uploadOozieFiles;

    # make a copy of example/data/sample.log to example/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="d2b7b-312">Klik op **-Script uitvoeren** of druk op **F5** het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-312">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="d2b7b-313">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-313">The output will be similar to:</span></span>

    ![Uitvoer van de voorbereiding van de zelfstudie][img-preparation-output]

## <a name="run-the-oozie-project"></a><span data-ttu-id="d2b7b-315">Voer het Oozie-project</span><span class="sxs-lookup"><span data-stu-id="d2b7b-315">Run the Oozie project</span></span>
<span data-ttu-id="d2b7b-316">Azure PowerShell biedt momenteel niet alle cmdlets voor het definiëren van Oozie-taken.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="d2b7b-317">U kunt de **Invoke-RestMethod** cmdlet Oozie-webservices aanroepen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-317">You can use the **Invoke-RestMethod** cmdlet to invoke Oozie web services.</span></span> <span data-ttu-id="d2b7b-318">De Oozie-webservices-API is een HTTP REST-API JSON.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-318">The Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="d2b7b-319">Zie voor meer informatie over de webservices Oozie API [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-319">For more information about the Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="d2b7b-320">**Een taak Oozie verzenden**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-320">**To submit an Oozie job**</span></span>

1. <span data-ttu-id="d2b7b-321">Open de Windows PowerShell ISE (Typ in Windows 8 startscherm **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-321">Open the Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="d2b7b-322">Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="d2b7b-323">Kopieer het volgende script in het scriptvenster en stel de eerst veertien variabelen (echter overslaan **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="d2b7b-323">Copy the following script into the script pane, and then set the first fourteen variables (however, skip **$storageUri**).</span></span>

    ```powershell
    #HDInsight cluster variables
    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterUserPassword>"

    #Azure Blob storage (WASB) variables
    $storageAccountName = "<StorageAccountName>"
    $storageContainerName = "<BlobContainerName>"
    $storageUri="wasb://$storageContainerName@$storageAccountName.blob.core.windows.net"

    #Azure SQL database variables
    $sqlDatabaseServer = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabaseLoginPassword = "<SQLDatabaseloginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"

    #Oozie WF/coordinator variables
    $coordStart = "2014-03-21T13:45Z"
    $coordEnd = "2014-03-21T13:45Z"
    $coordFrequency = "1440"    # in minutes, 24h x 60m = 1440m
    $coordTimezone = "UTC"    #UTC/GMT

    $oozieWFPath="$storageUri/tutorials/useoozie"  # The default name is workflow.xml. And you don't need to specify the file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServer.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServer;password=$sqlDatabaseLoginPassword;database=$sqlDatabaseName"
    $sqlDatabaseTableName = "log4jLogsCount"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)
    ```

    <span data-ttu-id="d2b7b-324">Zie voor meer beschrijvingen van de variabelen de [vereisten](#prerequisites) sectie in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-324">For more descriptions of the variables, see the [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="d2b7b-325">$coordstart en $coordend zijn de werkstroom begin- en eindtijd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-325">$coordstart and $coordend are the workflow starting and ending time.</span></span> <span data-ttu-id="d2b7b-326">Zoek voor meer informatie over de UTC/GMT-tijd, 'utc-tijd' op bing.com. De $coordFrequency is hoe vaak in minuten die u wilt uitvoeren van de werkstroom.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-326">To find out the UTC/GMT time, search "utc time" on bing.com. The $coordFrequency is how often in minutes you want to run the workflow.</span></span>
3. <span data-ttu-id="d2b7b-327">De volgende toevoegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-327">Append the following to the script.</span></span> <span data-ttu-id="d2b7b-328">Dit onderdeel wordt de nettolading van de Oozie gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-328">This part defines the Oozie payload:</span></span>

    ```powershell
    #OoziePayload used for Oozie web service submission
    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
            <name>nameNode</name>
            <value>$storageUrI</value>
        </property>

        <property>
            <name>jobTracker</name>
            <value>jobtrackerhost:9010</value>
        </property>

        <property>
            <name>queueName</name>
            <value>default</value>
        </property>

        <property>
            <name>oozie.use.system.libpath</name>
            <value>true</value>
        </property>

        <property>
            <name>oozie.coord.application.path</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>wfPath</name>
            <value>$oozieWFPath</value>
        </property>

        <property>
            <name>coordStart</name>
            <value>$coordStart</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>$coordEnd</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>$coordFrequency</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>$coordTimezone</value>
        </property>

        <property>
            <name>hiveScript</name>
            <value>$hiveScript</value>
        </property>

        <property>
            <name>hiveTableName</name>
            <value>$hiveTableName</value>
        </property>

        <property>
            <name>hiveDataFolder</name>
            <value>$hiveDataFolder</value>
        </property>

        <property>
            <name>hiveOutputFolder</name>
            <value>$hiveOutputFolder</value>
        </property>

        <property>
            <name>sqlDatabaseConnectionString</name>
            <value>&quot;$sqlDatabaseConnectionString&quot;</value>
        </property>

        <property>
            <name>sqlDatabaseTableName</name>
            <value>$SQLDatabaseTableName</value>
        </property>

        <property>
            <name>user.name</name>
            <value>admin</value>
        </property>

    </configuration>
    "@
    ```

   > [!NOTE]
   > <span data-ttu-id="d2b7b-329">Het belangrijkste verschil in vergelijking met het bestand van de werkstroom verzending van de nettolading van de variabele is **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-329">The major difference compared to the workflow submission payload file is the variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="d2b7b-330">Wanneer u een werkstroomtaak indient, gebruikt u **oozie.wf.application.path** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="d2b7b-331">De volgende toevoegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-331">Append the following to the script.</span></span> <span data-ttu-id="d2b7b-332">Dit onderdeel controleert de status van de Oozie-web-service:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-332">This part checks the Oozie web service status:</span></span>

    ```powershell
    function checkOozieServerStatus()
    {
        Write-Host "Checking Oozie server status..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/admin/status"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds -OutVariable $OozieServerStatus

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieServerSatus = $jsonResponse[0].("systemMode")
        Write-Host "Oozie server status is $oozieServerSatus..."

        if($oozieServerSatus -notmatch "NORMAL")
        {
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check the server status and re-run the job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="d2b7b-333">De volgende toevoegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-333">Append the following to the script.</span></span> <span data-ttu-id="d2b7b-334">Dit onderdeel maakt een taak Oozie:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending the following Payload to the cluster:" -ForegroundColor Green
        Write-Host "`n--------`n$OoziePayload`n--------"
        $clusterUriCreateJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $creds -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName -debug -Verbose

        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $oozieJobId = $jsonResponse[0].("id")
        Write-Host "Oozie job id is $oozieJobId..."

        return $oozieJobId
    }
    ```

   > [!NOTE]
   > <span data-ttu-id="d2b7b-335">Wanneer u een werkstroomtaak verzendt, moet u een andere webservice aanroepen van de taak starten nadat de taak is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-335">When you submit a workflow job, you must make another web service call to start the job after the job is created.</span></span> <span data-ttu-id="d2b7b-336">In dit geval wordt de coördinator-taak geactiveerd door tijd.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-336">In this case, the coordinator job is triggered by time.</span></span> <span data-ttu-id="d2b7b-337">De taak wordt automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-337">The job will start automatically.</span></span>

6. <span data-ttu-id="d2b7b-338">De volgende toevoegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-338">Append the following to the script.</span></span> <span data-ttu-id="d2b7b-339">Dit onderdeel controleert de status van de taak Oozie:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-339">This part checks the Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until the job metadata is populated in the Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for the job to complete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for the job to complete..."
            Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
            $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
            $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
            $JobStatus = $jsonResponse[0].("status")
        }

        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!"
        if($JobStatus -notmatch "SUCCEEDED")
        {
            Write-Host "Check logs at http://headnode0:9014/cluster for detais."
            exit -1
        }
    }
    ```

7. <span data-ttu-id="d2b7b-340">(Optioneel) De volgende toevoegen aan het script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-340">(Optional) Append the following to the script.</span></span>

    ```powershell
    function listOozieJobs()
    {
        Write-Host "Listing Oozie jobs..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/jobs"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds

        write-host "Job ID                                   App Name        Status      Started                         Ended"
        write-host "----------------------------------------------------------------------------------------------------------------------------------"
        foreach($job in $response.workflows)
        {
            Write-Host $job.id "`t" $job.appName "`t" $job.status "`t" $job.startTime "`t" $job.endTime
        }
    }

    function ShowOozieJobLog($oozieJobId)
    {
        Write-Host "Showing Oozie job info..." -ForegroundColor Green
        $clusterUriStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/$oozieJobId" + "?show=log"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $creds
        write-host $response
    }

    function killOozieJob($oozieJobId)
    {
        Write-Host "Killing the Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for the 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="d2b7b-341">De volgende toevoegen aan het script:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-341">Append the following to the script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="d2b7b-342">De tekens # verwijderen als u wilt de aanvullende functies uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-342">Remove the # signs if you want to run the additional functions.</span></span>
9. <span data-ttu-id="d2b7b-343">Als uw HDinsight-cluster versie 2.1 is vervangen door "https://$clusterName.azurehdinsight.net:443/oozie/v2/' met 'https://$clusterName.azurehdinsight.net:443/oozie/v1/'.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="d2b7b-344">HDInsight-cluster versie 2.1 komt niet ondersteunt versie 2 van de webservices.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-344">HDInsight cluster version 2.1 does not supports version 2 of the web services.</span></span>
10. <span data-ttu-id="d2b7b-345">Klik op **-Script uitvoeren** of druk op **F5** het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-345">Click **Run Script** or press **F5** to run the script.</span></span> <span data-ttu-id="d2b7b-346">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-346">The output will be similar to:</span></span>

     ![Zelfstudie voor uitvoer van de werkstroom uitvoeren][img-runworkflow-output]
11. <span data-ttu-id="d2b7b-348">Verbinding maken met uw SQL-Database om de geëxporteerde gegevens te bekijken.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-348">Connect to your SQL Database to see the exported data.</span></span>

<span data-ttu-id="d2b7b-349">**Controleer het foutenlogboek van de taak**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-349">**To check the job error log**</span></span>

<span data-ttu-id="d2b7b-350">Voor het oplossen van een werkstroom kan het logboekbestand Oozie worden gevonden op C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log van de cluster-headnode.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-350">To troubleshoot a workflow, the Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from the cluster headnode.</span></span> <span data-ttu-id="d2b7b-351">Zie voor informatie over RDP, [beheer van HDInsight-clusters met de Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="d2b7b-351">For information on RDP, see [Administering HDInsight clusters using the Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="d2b7b-352">**Opnieuw uitvoeren van de zelfstudie**</span><span class="sxs-lookup"><span data-stu-id="d2b7b-352">**To rerun the tutorial**</span></span>

<span data-ttu-id="d2b7b-353">Als u wilt herhalen van de werkstroom, moet u de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-353">To rerun the workflow, you must perform the following tasks:</span></span>

* <span data-ttu-id="d2b7b-354">Verwijder het uitvoerbestand voor Hive-script.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-354">Delete the Hive script output file.</span></span>
* <span data-ttu-id="d2b7b-355">De gegevens in de tabel log4jLogsCount verwijderen.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-355">Delete the data in the log4jLogsCount table.</span></span>

<span data-ttu-id="d2b7b-356">Hier volgt een voorbeeld van een Windows PowerShell script die u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete the Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all the records from the log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="d2b7b-357">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d2b7b-357">Next steps</span></span>
<span data-ttu-id="d2b7b-358">In deze zelfstudie hebt u geleerd hoe u een werkstroom Oozie en Oozie-coördinator definiëren en hoe u een Oozie-coördinator-taak uitvoert met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2b7b-358">In this tutorial, you learned how to define an Oozie workflow and an Oozie coordinator, and how to run an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="d2b7b-359">Zie voor meer informatie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="d2b7b-359">To learn more, see the following articles:</span></span>

* <span data-ttu-id="d2b7b-360">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="d2b7b-361">[Azure Blob storage gebruiken met HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="d2b7b-362">[HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="d2b7b-363">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-363">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="d2b7b-364">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="d2b7b-365">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d2b7b-366">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d2b7b-367">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="d2b7b-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-develop-java-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md

[sqldatabase-get-started]: ../sql-database/sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie-coordinator-time/HDI.UseOozie.RunCoord.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
