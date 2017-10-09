---
title: "aaaUse op basis van tijd Hadoop Oozie-coördinator in HDInsight | Microsoft Docs"
description: "Op basis van tijd Hadoop Oozie-coördinator gebruiken in HDInsight, een big data-service. Meer informatie over hoe toodefine Oozie werkstromen en coördinator, en het verzenden van taken."
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
ms.openlocfilehash: aecbb5ee94a4234d1a7768bdb6de2a33508b1e4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a><span data-ttu-id="37bd8-104">Tijd gebaseerde Oozie-coördinator gebruiken met Hadoop in HDInsight toodefine werkstromen en coördineren van taken</span><span class="sxs-lookup"><span data-stu-id="37bd8-104">Use time-based Oozie coordinator with Hadoop in HDInsight toodefine workflows and coordinate jobs</span></span>
<span data-ttu-id="37bd8-105">In dit artikel leert u hoe toodefine werkstromen en coördinator en hoe tootrigger Hallo coordinator taken, op basis van tijd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-105">In this article, you'll learn how toodefine workflows and coordinators, and how tootrigger hello coordinator jobs, based on time.</span></span> <span data-ttu-id="37bd8-106">Het is nuttig toogo via [Oozie gebruiken met HDInsight] [ hdinsight-use-oozie] voordat u dit artikel leest.</span><span class="sxs-lookup"><span data-stu-id="37bd8-106">It is helpful toogo through [Use Oozie with HDInsight][hdinsight-use-oozie] before you read this article.</span></span> <span data-ttu-id="37bd8-107">Bovendien tooOozie, u kunt ook taken plannen met behulp van Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="37bd8-107">In addition tooOozie, you can also schedule jobs using Azure Data Factory.</span></span> <span data-ttu-id="37bd8-108">Azure Data Factory toolearn Zie [Use Pig en Hive met Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="37bd8-108">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="37bd8-109">In dit artikel is een cluster met HDInsight op basis van Windows vereist.</span><span class="sxs-lookup"><span data-stu-id="37bd8-109">This article requires a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="37bd8-110">Zie voor meer informatie over het gebruik van Oozie, met inbegrip van taken op basis van tijd op een cluster op basis van Linux [Oozie gebruiken met Hadoop toodefine en een werkstroom wordt uitgevoerd op Linux gebaseerde HDInsight](hdinsight-use-oozie-linux-mac.md)</span><span class="sxs-lookup"><span data-stu-id="37bd8-110">For information on using Oozie, including time-based jobs, on a Linux-based cluster, see [Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight](hdinsight-use-oozie-linux-mac.md)</span></span>

## <a name="what-is-oozie"></a><span data-ttu-id="37bd8-111">Wat is Oozie</span><span class="sxs-lookup"><span data-stu-id="37bd8-111">What is Oozie</span></span>
<span data-ttu-id="37bd8-112">Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-112">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="37bd8-113">Het is geïntegreerd met Hadoop-stack Hallo en Hadoop-taken voor Apache MapReduce, Apache Pig, Apache Hive en Apache Sqoop ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="37bd8-113">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="37bd8-114">Het kan ook worden de gebruikte tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn.</span><span class="sxs-lookup"><span data-stu-id="37bd8-114">It can also be used tooschedule jobs that are specific tooa system, such as Java programs or shell scripts.</span></span>

<span data-ttu-id="37bd8-115">Hallo toont volgende afbeelding Hallo werkstroom die u wilt implementeren:</span><span class="sxs-lookup"><span data-stu-id="37bd8-115">hello following image shows hello workflow you will implement:</span></span>

![Werkstroomdiagram][img-workflow-diagram]

<span data-ttu-id="37bd8-117">Hallo workflow bevat twee acties:</span><span class="sxs-lookup"><span data-stu-id="37bd8-117">hello workflow contains two actions:</span></span>

1. <span data-ttu-id="37bd8-118">Een Hive-actie wordt het een HiveQL-script toocount Hallo exemplaren van elk type logboek-niveau in een logboekbestand log4j uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-118">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j log file.</span></span> <span data-ttu-id="37bd8-119">Elk logboek log4j bestaat uit een line-of velden met een [LOGBOEKNIVEAU] veld tooshow Hallo type en Hallo ernst, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="37bd8-119">Each log4j log consists of a line of fields that contains a [LOG LEVEL] field tooshow hello type and hello severity, for example:</span></span>

        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...

    <span data-ttu-id="37bd8-120">Hallo Hive-scriptuitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="37bd8-120">hello Hive script output is similar to:</span></span>

        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4

    <span data-ttu-id="37bd8-121">Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.</span><span class="sxs-lookup"><span data-stu-id="37bd8-121">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="37bd8-122">Een actie Sqoop exporteert Hallo HiveQL actie tooa uitvoertabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="37bd8-122">A Sqoop action exports hello HiveQL action output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="37bd8-123">Zie voor meer informatie over Sqoop [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="37bd8-123">For more information about Sqoop, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="37bd8-124">Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo-clusterversies geleverd door HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="37bd8-124">For supported Oozie versions on HDInsight clusters, see [What's new in hello cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
>
>

## <a name="prerequisites"></a><span data-ttu-id="37bd8-125">Vereisten</span><span class="sxs-lookup"><span data-stu-id="37bd8-125">Prerequisites</span></span>
<span data-ttu-id="37bd8-126">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="37bd8-126">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="37bd8-127">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-127">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="37bd8-128">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en verdwijnt per 1 januari 2017.</span><span class="sxs-lookup"><span data-stu-id="37bd8-128">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="37bd8-129">Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="37bd8-129">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="37bd8-130">Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37bd8-130">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="37bd8-131">Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-131">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="37bd8-132">**Een HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-132">**An HDInsight cluster**.</span></span> <span data-ttu-id="37bd8-133">Zie voor meer informatie over het maken van een HDInsight-cluster [HDInsight-clusters maken][hdinsight-provision], of [aan de slag met HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="37bd8-133">For information about creating an HDInsight cluster, see [Create HDInsight clusters][hdinsight-provision], or [Get started with HDInsight][hdinsight-get-started].</span></span> <span data-ttu-id="37bd8-134">U moet Hallo gegevens toogo Hallo-zelfstudie te volgen:</span><span class="sxs-lookup"><span data-stu-id="37bd8-134">You will need hello following data toogo through hello tutorial:</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="37bd8-135">Cluster-eigenschap</span><span class="sxs-lookup"><span data-stu-id="37bd8-135">Cluster property</span></span></th><th><span data-ttu-id="37bd8-136">Naam variabele voor Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="37bd8-136">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="37bd8-137">Waarde</span><span class="sxs-lookup"><span data-stu-id="37bd8-137">Value</span></span></th><th><span data-ttu-id="37bd8-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-138">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="37bd8-139">De naam van de HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="37bd8-139">HDInsight cluster name</span></span></td><td><span data-ttu-id="37bd8-140">$clusterName</span><span class="sxs-lookup"><span data-stu-id="37bd8-140">$clusterName</span></span></td><td></td><td><span data-ttu-id="37bd8-141">Hallo HDInsight-cluster op waarop u deze zelfstudie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-141">hello HDInsight cluster on which you will run this tutorial.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-142">Gebruikersnaam voor HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="37bd8-142">HDInsight cluster username</span></span></td><td><span data-ttu-id="37bd8-143">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="37bd8-143">$clusterUsername</span></span></td><td></td><td><span data-ttu-id="37bd8-144">gebruikersnaam voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="37bd8-144">hello HDInsight cluster user name.</span></span> </td></tr>
    <tr><td><span data-ttu-id="37bd8-145">HDInsight-cluster gebruikerswachtwoord</span><span class="sxs-lookup"><span data-stu-id="37bd8-145">HDInsight cluster user password</span></span> </td><td><span data-ttu-id="37bd8-146">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="37bd8-146">$clusterPassword</span></span></td><td></td><td><span data-ttu-id="37bd8-147">wachtwoord voor gebruiker Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="37bd8-147">hello HDInsight cluster user password.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-148">Naam van het Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="37bd8-148">Azure storage account name</span></span></td><td><span data-ttu-id="37bd8-149">$storageAccountName</span><span class="sxs-lookup"><span data-stu-id="37bd8-149">$storageAccountName</span></span></td><td></td><td><span data-ttu-id="37bd8-150">Een Azure Storage-account beschikbaar toohello HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="37bd8-150">An Azure Storage account available toohello HDInsight cluster.</span></span> <span data-ttu-id="37bd8-151">Voor deze zelfstudie gebruiken Hallo storage-standaardaccount die u hebt opgegeven tijdens het Hallo-cluster inrichten.</span><span class="sxs-lookup"><span data-stu-id="37bd8-151">For this tutorial, use hello default storage account that you specified during hello cluster provision process.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-152">Naam van een Azure Blob-container</span><span class="sxs-lookup"><span data-stu-id="37bd8-152">Azure Blob container name</span></span></td><td><span data-ttu-id="37bd8-153">$containerName</span><span class="sxs-lookup"><span data-stu-id="37bd8-153">$containerName</span></span></td><td></td><td><span data-ttu-id="37bd8-154">In dit voorbeeld gebruiken hello Azure Blob storage-container die wordt gebruikt voor Hallo standaard HDInsight-cluster-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="37bd8-154">For this example, use hello Azure Blob storage container that is used for hello default HDInsight cluster file system.</span></span> <span data-ttu-id="37bd8-155">Standaard heeft dezelfde naam als de HDInsight-cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="37bd8-155">By default, it has hello same name as hello HDInsight cluster.</span></span></td></tr>
    </table><span data-ttu-id="37bd8-156">
* **Een Azure SQL database**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-156">
* **An Azure SQL database**.</span></span> <span data-ttu-id="37bd8-157">Een firewallregel voor Hallo tooallow toegang tot SQL Database-server moet u configureren vanuit uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="37bd8-157">You must configure a firewall rule for hello SQL Database server tooallow access from your workstation.</span></span> <span data-ttu-id="37bd8-158">Zie voor instructies over het maken van een Azure SQL database en Hallo firewall configureren [aan de slag met Azure SQL database] [SQL-get-started].</span><span class="sxs-lookup"><span data-stu-id="37bd8-158">For instructions about creating an Azure SQL database and configuring hello firewall, see [Get started using Azure SQL database][sqldatabase-get-started].</span></span> <span data-ttu-id="37bd8-159">Dit artikel bevat een Windows PowerShell-script voor het maken van hello Azure SQL database-tabel die u nodig hebt voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-159">This article provides a Windows PowerShell script for creating hello Azure SQL database table that you need for this tutorial.</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="37bd8-160">SQL database-eigenschap</span><span class="sxs-lookup"><span data-stu-id="37bd8-160">SQL database property</span></span></th><th><span data-ttu-id="37bd8-161">Naam variabele voor Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="37bd8-161">Windows PowerShell variable name</span></span></th><th><span data-ttu-id="37bd8-162">Waarde</span><span class="sxs-lookup"><span data-stu-id="37bd8-162">Value</span></span></th><th><span data-ttu-id="37bd8-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-163">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="37bd8-164">SQL server-databasenaam</span><span class="sxs-lookup"><span data-stu-id="37bd8-164">SQL database server name</span></span></td><td><span data-ttu-id="37bd8-165">$sqlDatabaseServer</span><span class="sxs-lookup"><span data-stu-id="37bd8-165">$sqlDatabaseServer</span></span></td><td></td><td><span data-ttu-id="37bd8-166">Hallo SQL database-server toowhich Sqoop worden gegevens geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-166">hello SQL database server toowhich Sqoop will export data.</span></span> </td></tr>
    <tr><td><span data-ttu-id="37bd8-167">Aanmeldingsnaam voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="37bd8-167">SQL database login name</span></span></td><td><span data-ttu-id="37bd8-168">$sqlDatabaseLogin</span><span class="sxs-lookup"><span data-stu-id="37bd8-168">$sqlDatabaseLogin</span></span></td><td></td><td><span data-ttu-id="37bd8-169">Aanmeldingsnaam van de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="37bd8-169">SQL Database login name.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-170">Aanmeldingswachtwoord voor SQL-database</span><span class="sxs-lookup"><span data-stu-id="37bd8-170">SQL database login password</span></span></td><td><span data-ttu-id="37bd8-171">$sqlDatabaseLoginPassword</span><span class="sxs-lookup"><span data-stu-id="37bd8-171">$sqlDatabaseLoginPassword</span></span></td><td></td><td><span data-ttu-id="37bd8-172">Aanmeldingswachtwoord voor SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="37bd8-172">SQL Database login password.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-173">Naam van de SQL-database</span><span class="sxs-lookup"><span data-stu-id="37bd8-173">SQL database name</span></span></td><td><span data-ttu-id="37bd8-174">$sqlDatabaseName</span><span class="sxs-lookup"><span data-stu-id="37bd8-174">$sqlDatabaseName</span></span></td><td></td><td><span data-ttu-id="37bd8-175">Hello Azure SQL database toowhich Sqoop worden gegevens geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-175">hello Azure SQL database toowhich Sqoop will export data.</span></span> </td></tr>
    </table>

  > [!NOTE]
  > <span data-ttu-id="37bd8-176">Standaard wordt in een Azure SQL database verbindingen toelaat van Azure-Services, zoals Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="37bd8-176">By default an Azure SQL database allows connections from Azure Services, such as Azure HDInsight.</span></span> <span data-ttu-id="37bd8-177">Als deze firewallinstelling is uitgeschakeld, moet u het inschakelen van hello Azure-Portal.</span><span class="sxs-lookup"><span data-stu-id="37bd8-177">If this firewall setting is disabled, you must enable it from hello Azure Portal.</span></span> <span data-ttu-id="37bd8-178">Zie voor instructies over het maken van een SQL-Database en firewallregels configureren [maken en configureren van de SQL-Database][sqldatabase-get-started].</span><span class="sxs-lookup"><span data-stu-id="37bd8-178">For instruction about creating a SQL Database and configuring firewall rules, see [Create and Configure SQL Database][sqldatabase-get-started].</span></span>

> [!NOTE]
> <span data-ttu-id="37bd8-179">Hallo-waarden invullen in Hallo tabellen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-179">Fill-in hello values in hello tables.</span></span> <span data-ttu-id="37bd8-180">Dit is handig voor het doorlopen van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-180">It will be helpful for going through this tutorial.</span></span>

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="37bd8-181">Oozie werkstroom definiëren en Hallo gerelateerde HiveQL-script</span><span class="sxs-lookup"><span data-stu-id="37bd8-181">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="37bd8-182">Oozie werkstromen definities worden geschreven in hPDL (een XML-proces definition language).</span><span class="sxs-lookup"><span data-stu-id="37bd8-182">Oozie workflows definitions are written in hPDL (an XML process definition language).</span></span> <span data-ttu-id="37bd8-183">Hallo werkstroom standaardbestandsnaam is *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="37bd8-183">hello default workflow file name is *workflow.xml*.</span></span>  <span data-ttu-id="37bd8-184">U Hallo werkstroombestand lokaal opslaan en vervolgens deze toohello HDInsight-cluster implementeren met behulp van Azure PowerShell verderop in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-184">You will save hello workflow file locally, and then deploy it toohello HDInsight cluster by using Azure PowerShell later in this tutorial.</span></span>

<span data-ttu-id="37bd8-185">Hallo Hive actie in de werkstroom Hallo roept een scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="37bd8-185">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="37bd8-186">Dit scriptbestand bevat drie HiveQL-instructies:</span><span class="sxs-lookup"><span data-stu-id="37bd8-186">This script file contains three HiveQL statements:</span></span>

1. <span data-ttu-id="37bd8-187">**Hallo DROP TABLE-instructie** verwijderingen Hallo log4j Hive-tabel als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="37bd8-187">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="37bd8-188">**Hallo CREATE TABLE-instructie** maakt een log4j Hive externe tabel toohello locatie van Hallo log4j logboekbestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="37bd8-188">**hello CREATE TABLE statement** creates a log4j Hive external table, which points toohello location of hello log4j log file;</span></span>
3. <span data-ttu-id="37bd8-189">**locatie van Hallo log4j logboekbestand Hallo**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-189">**hello location of hello log4j log file**.</span></span> <span data-ttu-id="37bd8-190">Hallo veldscheidingsteken is ",".</span><span class="sxs-lookup"><span data-stu-id="37bd8-190">hello field delimiter is ",".</span></span> <span data-ttu-id="37bd8-191">Hallo standaard regel scheidingsteken is '\n'.</span><span class="sxs-lookup"><span data-stu-id="37bd8-191">hello default line delimiter is "\n".</span></span> <span data-ttu-id="37bd8-192">Een externe Hive-tabel is Hallo-gegevensbestand voor het gebruikte tooavoid wordt verwijderd uit de oorspronkelijke locatie hello, als u meerdere keren door toorun hello Oozie werkstroom wilt.</span><span class="sxs-lookup"><span data-stu-id="37bd8-192">A Hive external table is used tooavoid hello data file being removed from hello original location, in case you want toorun hello Oozie workflow multiple times.</span></span>
4. <span data-ttu-id="37bd8-193">**Hallo-instructie INSERT OVERSCHRIJVEN** telt Hallo exemplaren van elk type logboek-niveau van Hallo log4j Hive-tabel en Hallo tooan Azure Blob storage uitvoerlocatie wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-193">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and it saves hello output tooan Azure Blob storage location.</span></span>

> [!NOTE]
> <span data-ttu-id="37bd8-194">Er is een bekend probleem voor Hive-pad.</span><span class="sxs-lookup"><span data-stu-id="37bd8-194">There is a known Hive path issue.</span></span> <span data-ttu-id="37bd8-195">Voert u dit probleem is opgetreden bij het indienen van een Oozie-taak.</span><span class="sxs-lookup"><span data-stu-id="37bd8-195">You will run into this problem when submitting an Oozie job.</span></span> <span data-ttu-id="37bd8-196">Hallo instructies voor het verhelpen van Hallo probleem vindt u op Hallo TechNet-Wiki: [HDInsight Hive-fout: kan geen toorename][technetwiki-hive-error].</span><span class="sxs-lookup"><span data-stu-id="37bd8-196">hello instructions for fixing hello issue can be found on hello TechNet Wiki: [HDInsight Hive error: Unable toorename][technetwiki-hive-error].</span></span>

<span data-ttu-id="37bd8-197">**toodefine hello HiveQL-script bestand toobe aangeroepen door Hallo-werkstroom**</span><span class="sxs-lookup"><span data-stu-id="37bd8-197">**toodefine hello HiveQL script file toobe called by hello workflow**</span></span>

1. <span data-ttu-id="37bd8-198">Maak een tekstbestand met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="37bd8-198">Create a text file with hello following content:</span></span>

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    <span data-ttu-id="37bd8-199">Er zijn drie variabelen in Hallo script gebruikt:</span><span class="sxs-lookup"><span data-stu-id="37bd8-199">There are three variables used in hello script:</span></span>

   * <span data-ttu-id="37bd8-200">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="37bd8-200">${hiveTableName}</span></span>
   * <span data-ttu-id="37bd8-201">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="37bd8-201">${hiveDataFolder}</span></span>
   * <span data-ttu-id="37bd8-202">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="37bd8-202">${hiveOutputFolder}</span></span>

     <span data-ttu-id="37bd8-203">Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="37bd8-203">hello workflow definition file (workflow.xml in this tutorial) will pass these values toothis HiveQL script at run time.</span></span>
2. <span data-ttu-id="37bd8-204">Hallo bestand opslaan als **C:\Tutorials\UseOozie\useooziewf.hql** met behulp van ANSI (ASCII) codering.</span><span class="sxs-lookup"><span data-stu-id="37bd8-204">Save hello file as **C:\Tutorials\UseOozie\useooziewf.hql** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="37bd8-205">(Kladblok gebruiken als uw teksteditor deze optie niet.) Dit scriptbestand wordt geïmplementeerde toohello HDInsight-cluster worden verderop in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="37bd8-205">(Use Notepad if your text editor doesn't provide this option.) This script file will be deployed toohello HDInsight cluster later in hello tutorial.</span></span>

<span data-ttu-id="37bd8-206">**een werkstroom toodefine**</span><span class="sxs-lookup"><span data-stu-id="37bd8-206">**toodefine a workflow**</span></span>

1. <span data-ttu-id="37bd8-207">Maak een tekstbestand met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="37bd8-207">Create a text file with hello following content:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>

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

    <span data-ttu-id="37bd8-208">Er zijn twee acties in de werkstroom Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-208">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="37bd8-209">Hallo start-tooaction is *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="37bd8-209">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="37bd8-210">Als het Hallo-actie wordt uitgevoerd *OK*, is de volgende actie Hallo *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="37bd8-210">If hello action runs *OK*, hello next action is *RunSqoopExport*.</span></span>

    <span data-ttu-id="37bd8-211">Hallo RunHiveScript heeft meerdere variabelen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-211">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="37bd8-212">U doorgeven Hallo waarden bij het verzenden van Hallo Oozie taak vanuit uw werkstation met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37bd8-212">You will pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

    <span data-ttu-id="37bd8-213">Werkstroomvariabelen</span><span class="sxs-lookup"><span data-stu-id="37bd8-213">Workflow variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="37bd8-214">Werkstroomvariabelen</span><span class="sxs-lookup"><span data-stu-id="37bd8-214">Workflow variables</span></span></th><th><span data-ttu-id="37bd8-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-215">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="37bd8-216">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="37bd8-216">${jobTracker}</span></span></td><td><span data-ttu-id="37bd8-217">Geef de URL Hallo van Hallo Hadoop taak vastleggen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-217">Specify hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="37bd8-218">Gebruik <strong>jobtrackerhost:9010</strong> cluster in HDInsight versie 3.0 en 2.0.</span><span class="sxs-lookup"><span data-stu-id="37bd8-218">Use <strong>jobtrackerhost:9010</strong> on HDInsight cluster version 3.0 and 2.0.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-219">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="37bd8-219">${nameNode}</span></span></td><td><span data-ttu-id="37bd8-220">Geef de URL op Hallo van Hallo Hadoop naam knooppunt.</span><span class="sxs-lookup"><span data-stu-id="37bd8-220">Specify hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="37bd8-221">Gebruik Hallo standaard bestand system wasb: / / adres, bijvoorbeeld <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="37bd8-221">Use hello default file system wasb:// address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-222">${Wachtrijnaam}</span><span class="sxs-lookup"><span data-stu-id="37bd8-222">${queueName}</span></span></td><td><span data-ttu-id="37bd8-223">Hiermee geeft u op Hallo wachtrijnaam die taak Hallo worden verzonden naar.</span><span class="sxs-lookup"><span data-stu-id="37bd8-223">Specifies hello queue name that hello job will be submitted to.</span></span> <span data-ttu-id="37bd8-224">Gebruik <strong>standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="37bd8-224">Use <strong>default</strong>.</span></span></td></tr>
    </table>

    <span data-ttu-id="37bd8-225">Variabelen voor hive</span><span class="sxs-lookup"><span data-stu-id="37bd8-225">Hive action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="37bd8-226">Hive actie variabele</span><span class="sxs-lookup"><span data-stu-id="37bd8-226">Hive action variable</span></span></th><th><span data-ttu-id="37bd8-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-227">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="37bd8-228">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="37bd8-228">${hiveDataFolder}</span></span></td><td><span data-ttu-id="37bd8-229">Hallo bronmap voor Hallo Create Table Hive-opdracht.</span><span class="sxs-lookup"><span data-stu-id="37bd8-229">hello source directory for hello Hive Create Table command.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-230">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="37bd8-230">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="37bd8-231">Hallo uitvoermap voor Hallo-instructie INSERT OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="37bd8-231">hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-232">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="37bd8-232">${hiveTableName}</span></span></td><td><span data-ttu-id="37bd8-233">Hallo-naam van Hallo Hive-tabel die verwijst naar Hallo log4j gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-233">hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
    </table>

    <span data-ttu-id="37bd8-234">Variabelen voor de Sqoop</span><span class="sxs-lookup"><span data-stu-id="37bd8-234">Sqoop action variables</span></span>

    <table border = "1">
    <tr><th><span data-ttu-id="37bd8-235">Sqoop actie variabele</span><span class="sxs-lookup"><span data-stu-id="37bd8-235">Sqoop action variable</span></span></th><th><span data-ttu-id="37bd8-236">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-236">Description</span></span></th></tr>
    <tr><td><span data-ttu-id="37bd8-237">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="37bd8-237">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="37bd8-238">Verbindingstekenreeks van de SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="37bd8-238">SQL Database connection string.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-239">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="37bd8-239">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="37bd8-240">Hello Azure SQL database toowhere Hallo tabelgegevens worden geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-240">hello Azure SQL database table toowhere hello data will be exported.</span></span></td></tr>
    <tr><td><span data-ttu-id="37bd8-241">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="37bd8-241">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="37bd8-242">Hallo uitvoermap voor Hallo instructie Hive invoegen OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="37bd8-242">hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="37bd8-243">Dit is Hallo dezelfde map voor het exporteren van de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="37bd8-243">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
    </table>

    <span data-ttu-id="37bd8-244">Zie voor meer informatie over Oozie-werkstroom en het gebruik van de werkstroomacties Hallo [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="37bd8-244">For more information about Oozie workflow and using hello workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

1. <span data-ttu-id="37bd8-245">Hallo bestand opslaan als **C:\Tutorials\UseOozie\workflow.xml** met behulp van ANSI (ASCII) codering.</span><span class="sxs-lookup"><span data-stu-id="37bd8-245">Save hello file as **C:\Tutorials\UseOozie\workflow.xml** by using ANSI (ASCII) encoding.</span></span> <span data-ttu-id="37bd8-246">(Kladblok gebruiken als uw teksteditor deze optie niet.)</span><span class="sxs-lookup"><span data-stu-id="37bd8-246">(Use Notepad if your text editor doesn't provide this option.)</span></span>

<span data-ttu-id="37bd8-247">**toodefine coordinator**</span><span class="sxs-lookup"><span data-stu-id="37bd8-247">**toodefine coordinator**</span></span>

1. <span data-ttu-id="37bd8-248">Maak een tekstbestand met Hallo volgende inhoud:</span><span class="sxs-lookup"><span data-stu-id="37bd8-248">Create a text file with hello following content:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    <span data-ttu-id="37bd8-249">Er zijn vijf variabelen die worden gebruikt in het definitiebestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="37bd8-249">There are five variables used in hello definition file:</span></span>

   | <span data-ttu-id="37bd8-250">Variabele</span><span class="sxs-lookup"><span data-stu-id="37bd8-250">Variable</span></span> | <span data-ttu-id="37bd8-251">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="37bd8-251">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="37bd8-252">${coordFrequency}</span><span class="sxs-lookup"><span data-stu-id="37bd8-252">${coordFrequency}</span></span> |<span data-ttu-id="37bd8-253">Taak onderbreken tijd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-253">Job pause time.</span></span> <span data-ttu-id="37bd8-254">Frequentie wordt altijd uitgedrukt in minuten.</span><span class="sxs-lookup"><span data-stu-id="37bd8-254">Frequency is always expressed in minutes.</span></span> |
   | <span data-ttu-id="37bd8-255">${coordStart}</span><span class="sxs-lookup"><span data-stu-id="37bd8-255">${coordStart}</span></span> |<span data-ttu-id="37bd8-256">Begintijd van taak.</span><span class="sxs-lookup"><span data-stu-id="37bd8-256">Job start time.</span></span> |
   | <span data-ttu-id="37bd8-257">${coordEnd}</span><span class="sxs-lookup"><span data-stu-id="37bd8-257">${coordEnd}</span></span> |<span data-ttu-id="37bd8-258">Eindtijd van de taak.</span><span class="sxs-lookup"><span data-stu-id="37bd8-258">Job end time.</span></span> |
   | <span data-ttu-id="37bd8-259">${coordTimezone}</span><span class="sxs-lookup"><span data-stu-id="37bd8-259">${coordTimezone}</span></span> |<span data-ttu-id="37bd8-260">Oozie verwerkt taken in een vaste tijdzone coordinator met geen zomertijd (doorgaans weergegeven met behulp UTC).</span><span class="sxs-lookup"><span data-stu-id="37bd8-260">Oozie processes coordinator jobs in a fixed time zone with no daylight saving time (typically represented by using UTC).</span></span> <span data-ttu-id="37bd8-261">Deze tijdzone wordt verwezen als Hallo 'Oozie verwerking tijdzone."</span><span class="sxs-lookup"><span data-stu-id="37bd8-261">This time zone is referred as hello "Oozie processing timezone."</span></span> |
   | <span data-ttu-id="37bd8-262">${wfPath}</span><span class="sxs-lookup"><span data-stu-id="37bd8-262">${wfPath}</span></span> |<span data-ttu-id="37bd8-263">Hallo-pad voor Hallo workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="37bd8-263">hello path for hello workflow.xml.</span></span>  <span data-ttu-id="37bd8-264">Als bestandsnaam Hallo-werkstroom niet Hallo standaardbestandsnaam (workflow.xml), moet u deze opgeven.</span><span class="sxs-lookup"><span data-stu-id="37bd8-264">If hello workflow file name is not hello default file name (workflow.xml), you must specify it.</span></span> |
2. <span data-ttu-id="37bd8-265">Hallo bestand opslaan als **C:\Tutorials\UseOozie\coordinator.xml** met behulp van Hallo ANSI (ASCII)-codering.</span><span class="sxs-lookup"><span data-stu-id="37bd8-265">Save hello file as **C:\Tutorials\UseOozie\coordinator.xml** by using hello ANSI (ASCII) encoding.</span></span> <span data-ttu-id="37bd8-266">(Kladblok gebruiken als uw teksteditor deze optie niet.)</span><span class="sxs-lookup"><span data-stu-id="37bd8-266">(Use Notepad if your text editor doesn't provide this option.)</span></span>

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a><span data-ttu-id="37bd8-267">Hallo Oozie-project implementeert en bereid Hallo-zelfstudie</span><span class="sxs-lookup"><span data-stu-id="37bd8-267">Deploy hello Oozie project and prepare hello tutorial</span></span>
<span data-ttu-id="37bd8-268">U kunt een Azure PowerShell-script tooperform Hallo volgende wordt uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="37bd8-268">You will run an Azure PowerShell script tooperform hello following:</span></span>

* <span data-ttu-id="37bd8-269">Kopiëren Hallo HiveQL-script (useoozie.hql) tooAzure Blob-opslag, wasb:///tutorials/useoozie/useoozie.hql.</span><span class="sxs-lookup"><span data-stu-id="37bd8-269">Copy hello HiveQL script (useoozie.hql) tooAzure Blob storage, wasb:///tutorials/useoozie/useoozie.hql.</span></span>
* <span data-ttu-id="37bd8-270">Kopieer workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="37bd8-270">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
* <span data-ttu-id="37bd8-271">Kopieer coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span><span class="sxs-lookup"><span data-stu-id="37bd8-271">Copy coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.</span></span>
* <span data-ttu-id="37bd8-272">Bestand kopiëren Hallo-gegevens (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="37bd8-272">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
* <span data-ttu-id="37bd8-273">Maak een Azure SQL-databasetabel voor het opslaan van gegevens van Sqoop exporteren.</span><span class="sxs-lookup"><span data-stu-id="37bd8-273">Create an Azure SQL database table for storing Sqoop export data.</span></span> <span data-ttu-id="37bd8-274">Hallo-tabelnaam is *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="37bd8-274">hello table name is *log4jLogCount*.</span></span>

<span data-ttu-id="37bd8-275">**Inzicht in HDInsight-opslag**</span><span class="sxs-lookup"><span data-stu-id="37bd8-275">**Understand HDInsight storage**</span></span>

<span data-ttu-id="37bd8-276">HDInsight gebruikt Azure Blob-opslag voor gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="37bd8-276">HDInsight uses Azure Blob storage for data storage.</span></span> <span data-ttu-id="37bd8-277">wasb: / / is Microsoft implementatie van Hallo Hadoop distributed file system (HDFS) in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="37bd8-277">wasb:// is Microsoft's implementation of hello Hadoop distributed file system (HDFS) in Azure Blob storage.</span></span> <span data-ttu-id="37bd8-278">Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="37bd8-278">For more information, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="37bd8-279">Wanneer u een HDInsight-cluster inrichten, is een Azure Blob storage-account en een specifieke container uit dat account aangewezen als het standaardbestandssysteem hello, zoals in HDFS.</span><span class="sxs-lookup"><span data-stu-id="37bd8-279">When you provision an HDInsight cluster, an Azure Blob storage account and a specific container from that account is designated as hello default file system, like in HDFS.</span></span> <span data-ttu-id="37bd8-280">Bovendien toothis storage-account, kunt u toevoegen extra opslagaccounts van Hallo dezelfde Azure-abonnement of van verschillende Azure-abonnementen tijdens het inrichtingsproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="37bd8-280">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or from different Azure subscriptions during hello provisioning process.</span></span> <span data-ttu-id="37bd8-281">Zie voor instructies over het toevoegen van extra opslagaccounts [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="37bd8-281">For instructions about adding additional storage accounts, see [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="37bd8-282">toosimplify hello Azure PowerShell-script in deze zelfstudie gebruikt, alle bestanden worden opgeslagen in bestand Hallo-systeem standaardcontainer Hallo zich bevindt op *zelfstudies/useoozie*.</span><span class="sxs-lookup"><span data-stu-id="37bd8-282">toosimplify hello Azure PowerShell script used in this tutorial, all of hello files are stored in hello default file system container located at */tutorials/useoozie*.</span></span> <span data-ttu-id="37bd8-283">Standaard is deze container Hallo dezelfde naam als de naam van een Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="37bd8-283">By default, this container has hello same name as hello HDInsight cluster name.</span></span>
<span data-ttu-id="37bd8-284">Hallo-syntaxis is:</span><span class="sxs-lookup"><span data-stu-id="37bd8-284">hello syntax is:</span></span>

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> <span data-ttu-id="37bd8-285">Alleen Hallo *wasb: / /* syntaxis wordt ondersteund in HDInsight-cluster versie 3.0.</span><span class="sxs-lookup"><span data-stu-id="37bd8-285">Only hello *wasb://* syntax is supported in HDInsight cluster version 3.0.</span></span> <span data-ttu-id="37bd8-286">Hallo oudere *asv: / /* syntaxis wordt ondersteund in HDInsight 2.1 en 1.6-clusters, maar wordt niet ondersteund in HDInsight 3.0-clusters.</span><span class="sxs-lookup"><span data-stu-id="37bd8-286">hello older *asv://* syntax is supported in HDInsight 2.1 and 1.6 clusters, but it is not supported in HDInsight 3.0 clusters.</span></span>
>
> <span data-ttu-id="37bd8-287">Hallo wasb: / / pad is een virtueel pad.</span><span class="sxs-lookup"><span data-stu-id="37bd8-287">hello wasb:// path is a virtual path.</span></span> <span data-ttu-id="37bd8-288">Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="37bd8-288">For more information see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="37bd8-289">Een bestand dat is opgeslagen in bestand Hallo-systeem standaardcontainer toegankelijk zijn vanuit HDInsight met behulp van Hallo URI's (ik gebruik workflow.xml als voorbeeld) te volgen:</span><span class="sxs-lookup"><span data-stu-id="37bd8-289">A file that is stored in hello default file system container can be accessed from HDInsight by using any of hello following URIs (I am using workflow.xml as an example):</span></span>

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

<span data-ttu-id="37bd8-290">Als u tooaccess Hallo-bestand rechtstreeks uit Hallo storage-account wilt, wordt Hallo blob-naam voor het Hallo-bestand is:</span><span class="sxs-lookup"><span data-stu-id="37bd8-290">If you want tooaccess hello file directly from hello storage account, hello blob name for hello file is:</span></span>

    tutorials/useoozie/workflow.xml

<span data-ttu-id="37bd8-291">**De interne en externe tabellen Hive begrijpen**</span><span class="sxs-lookup"><span data-stu-id="37bd8-291">**Understand Hive internal and external tables**</span></span>

<span data-ttu-id="37bd8-292">Er zijn enkele dingen die u tooknow over Hive interne en externe tabellen nodig:</span><span class="sxs-lookup"><span data-stu-id="37bd8-292">There are a few things you need tooknow about Hive internal and external tables:</span></span>

* <span data-ttu-id="37bd8-293">Hallo CREATE TABLE opdracht maakt een interne tabel, ook wel bekend als een beheerde tabel.</span><span class="sxs-lookup"><span data-stu-id="37bd8-293">hello CREATE TABLE command creates an internal table, also known as a managed table.</span></span> <span data-ttu-id="37bd8-294">Hallo gegevensbestand moet zich in de standaardcontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="37bd8-294">hello data file must be located in hello default container.</span></span>
* <span data-ttu-id="37bd8-295">Hallo CREATE TABLE-opdracht wordt verplaatst Hallo gegevens bestand toohello/hivedatawarehouse/<TableName> map in de standaardcontainer Hallo.</span><span class="sxs-lookup"><span data-stu-id="37bd8-295">hello CREATE TABLE command moves hello data file toohello /hive/warehouse/<TableName> folder in hello default container.</span></span>
* <span data-ttu-id="37bd8-296">Hallo externe tabel maken opdracht maakt een externe tabel.</span><span class="sxs-lookup"><span data-stu-id="37bd8-296">hello CREATE EXTERNAL TABLE command creates an external table.</span></span> <span data-ttu-id="37bd8-297">Hallo-gegevensbestand kan buiten de standaardcontainer Hallo zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="37bd8-297">hello data file can be located outside hello default container.</span></span>
* <span data-ttu-id="37bd8-298">Hallo externe tabel maken opdracht verplaatst geen Hallo-gegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="37bd8-298">hello CREATE EXTERNAL TABLE command does not move hello data file.</span></span>
* <span data-ttu-id="37bd8-299">Hallo externe tabel maken opdracht toegestaan niet in alle submappen onder de Hallo-map die is opgegeven in Hallo locatie-component.</span><span class="sxs-lookup"><span data-stu-id="37bd8-299">hello CREATE EXTERNAL TABLE command doesn't allow any subfolders under hello folder that is specified in hello LOCATION clause.</span></span> <span data-ttu-id="37bd8-300">Dit is Hallo reden waarom Hallo zelfstudie een kopie van Hallo sample.log bestand wordt.</span><span class="sxs-lookup"><span data-stu-id="37bd8-300">This is hello reason why hello tutorial makes a copy of hello sample.log file.</span></span>

<span data-ttu-id="37bd8-301">Zie voor meer informatie [HDInsight: Hive interne en externe tabellen Intro][cindygross-hive-tables].</span><span class="sxs-lookup"><span data-stu-id="37bd8-301">For more information, see [HDInsight: Hive Internal and External Tables Intro][cindygross-hive-tables].</span></span>

<span data-ttu-id="37bd8-302">**tooprepare Hallo-zelfstudie**</span><span class="sxs-lookup"><span data-stu-id="37bd8-302">**tooprepare hello tutorial**</span></span>

1. <span data-ttu-id="37bd8-303">Open Hallo Windows PowerShell ISE (in Windows 8 Start welkomstscherm, typt u **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-303">Open hello Windows PowerShell ISE (in hello Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="37bd8-304">Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="37bd8-304">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="37bd8-305">Voer in het deelvenster onderaan Hallo, Hallo opdracht tooconnect tooyour Azure-abonnement na:</span><span class="sxs-lookup"><span data-stu-id="37bd8-305">In hello bottom pane, run hello following command tooconnect tooyour Azure subscription:</span></span>

    ```powershell
    Add-AzureAccount
    ```

    <span data-ttu-id="37bd8-306">U worden na vragen aan gebruiker tooenter de referenties van uw Azure-account.</span><span class="sxs-lookup"><span data-stu-id="37bd8-306">You will be prompted tooenter your Azure account credentials.</span></span> <span data-ttu-id="37bd8-307">Deze methode voor het toevoegen van een abonnementsverbinding een time-out optreedt en na 12 uur, hebt u toorun Hallo cmdlet opnieuw.</span><span class="sxs-lookup"><span data-stu-id="37bd8-307">This method of adding a subscription connection times out, and after 12 hours, you will have toorun hello cmdlet again.</span></span>

   > [!NOTE]
   > <span data-ttu-id="37bd8-308">Als er meerdere Azure-abonnementen en Hallo standaardabonnement is niet Hallo gewenste toouse, gebruikt u Hallo <strong>Select-AzureSubscription</strong> cmdlet tooselect een abonnement.</span><span class="sxs-lookup"><span data-stu-id="37bd8-308">If you have multiple Azure subscriptions and hello default subscription is not hello one you want toouse, use hello <strong>Select-AzureSubscription</strong> cmdlet tooselect a subscription.</span></span>

3. <span data-ttu-id="37bd8-309">Hallo script volgen in het scriptvenster Hallo kopiëren en stel vervolgens de eerste zes variabelen Hallo:</span><span class="sxs-lookup"><span data-stu-id="37bd8-309">Copy hello following script into hello script pane, and then set hello first six variables:</span></span>

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

    # Oozie files for hello tutorial
    $hiveQLScript = "C:\Tutorials\UseOozie\useooziewf.hql"
    $workflowDefinition = "C:\Tutorials\UseOozie\workflow.xml"
    $coordDefinition =  "C:\Tutorials\UseOozie\coordinator.xml"

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here
    ```

    <span data-ttu-id="37bd8-310">Zie voor meer beschrijvingen van de variabelen Hallo Hallo [vereisten](#prerequisites) sectie in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-310">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

4. <span data-ttu-id="37bd8-311">Hallo toohello script in het scriptvenster Hallo volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="37bd8-311">Append hello following toohello script in hello script pane:</span></span>

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
        Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green
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

        #Create hello log4jLogsCount table
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

    # make a copy of example/data/sample.log tooexample/data/log4j/sample.log
    prepareHiveDataFile;

    # create log4jlogsCount table on SQL database
    prepareSQLDatabase;
    ```

5. <span data-ttu-id="37bd8-312">Klik op **-Script uitvoeren** of druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="37bd8-312">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="37bd8-313">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="37bd8-313">hello output will be similar to:</span></span>

    ![Uitvoer van de voorbereiding van de zelfstudie][img-preparation-output]

## <a name="run-hello-oozie-project"></a><span data-ttu-id="37bd8-315">Hallo Oozie-project uitvoeren</span><span class="sxs-lookup"><span data-stu-id="37bd8-315">Run hello Oozie project</span></span>
<span data-ttu-id="37bd8-316">Azure PowerShell biedt momenteel niet alle cmdlets voor het definiëren van Oozie-taken.</span><span class="sxs-lookup"><span data-stu-id="37bd8-316">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="37bd8-317">U kunt Hallo **Invoke-RestMethod** cmdlet tooinvoke Oozie-webservices.</span><span class="sxs-lookup"><span data-stu-id="37bd8-317">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="37bd8-318">Hallo Oozie webservices-API is een HTTP REST-API JSON.</span><span class="sxs-lookup"><span data-stu-id="37bd8-318">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="37bd8-319">Zie voor meer informatie over Hallo Oozie web API-services, [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="37bd8-319">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight cluster version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight cluster version 2.1).</span></span>

<span data-ttu-id="37bd8-320">**een taak Oozie toosubmit**</span><span class="sxs-lookup"><span data-stu-id="37bd8-320">**toosubmit an Oozie job**</span></span>

1. <span data-ttu-id="37bd8-321">Open Hallo Windows PowerShell ISE (Typ in Windows 8 startscherm **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-321">Open hello Windows PowerShell ISE (in Windows 8 Start screen, type **PowerShell_ISE**, and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="37bd8-322">Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).</span><span class="sxs-lookup"><span data-stu-id="37bd8-322">For more information, see [Start Windows PowerShell on Windows 8 and Windows][powershell-start]).</span></span>
2. <span data-ttu-id="37bd8-323">Kopiëren Hallo volgende script in het scriptvenster Hallo en vervolgens set eerst veertien variabelen Hallo (echter overslaan **$storageUri**).</span><span class="sxs-lookup"><span data-stu-id="37bd8-323">Copy hello following script into hello script pane, and then set hello first fourteen variables (however, skip **$storageUri**).</span></span>

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

    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
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

    <span data-ttu-id="37bd8-324">Zie voor meer beschrijvingen van de variabelen Hallo Hallo [vereisten](#prerequisites) sectie in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="37bd8-324">For more descriptions of hello variables, see hello [Prerequisites](#prerequisites) section in this tutorial.</span></span>

    <span data-ttu-id="37bd8-325">$coordstart en $coordend zijn Hallo werkstroom begin- en eindtijd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-325">$coordstart and $coordend are hello workflow starting and ending time.</span></span> <span data-ttu-id="37bd8-326">toofind hello UTC/GMT-tijd, zoeken 'utc-tijd' op bing.com. Hallo $coordFrequency is hoe vaak in minuten die u wilt dat toorun Hallo werkstroom.</span><span class="sxs-lookup"><span data-stu-id="37bd8-326">toofind out hello UTC/GMT time, search "utc time" on bing.com. hello $coordFrequency is how often in minutes you want toorun hello workflow.</span></span>
3. <span data-ttu-id="37bd8-327">Hallo na toohello script toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-327">Append hello following toohello script.</span></span> <span data-ttu-id="37bd8-328">Dit onderdeel definieert Hallo Oozie nettolading:</span><span class="sxs-lookup"><span data-stu-id="37bd8-328">This part defines hello Oozie payload:</span></span>

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
   > <span data-ttu-id="37bd8-329">Hallo het belangrijkste verschil vergeleken toohello werkstroom-opdrachtbestand nettolading is Hallo variabele **oozie.coord.application.path**.</span><span class="sxs-lookup"><span data-stu-id="37bd8-329">hello major difference compared toohello workflow submission payload file is hello variable **oozie.coord.application.path**.</span></span> <span data-ttu-id="37bd8-330">Wanneer u een werkstroomtaak indient, gebruikt u **oozie.wf.application.path** in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="37bd8-330">When you submit a workflow job, you use **oozie.wf.application.path** instead.</span></span>

4. <span data-ttu-id="37bd8-331">Hallo na toohello script toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-331">Append hello following toohello script.</span></span> <span data-ttu-id="37bd8-332">Dit deel controleert de status van Hallo Oozie web service:</span><span class="sxs-lookup"><span data-stu-id="37bd8-332">This part checks hello Oozie web service status:</span></span>

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
            Write-Host "Oozie server status is $oozieServerSatus...cannot submit Oozie jobs. Check hello server status and re-run hello job."
            exit 1
        }
    }
    ```

5. <span data-ttu-id="37bd8-333">Hallo na toohello script toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-333">Append hello following toohello script.</span></span> <span data-ttu-id="37bd8-334">Dit onderdeel maakt een taak Oozie:</span><span class="sxs-lookup"><span data-stu-id="37bd8-334">This part creates an Oozie job:</span></span>

    ```powershell
    function createOozieJob()
    {
        # create Oozie job
        Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
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
   > <span data-ttu-id="37bd8-335">Wanneer u een werkstroomtaak verzendt, moet u een andere web service aanroep toostart Hallo taak maken nadat Hallo-taak is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="37bd8-335">When you submit a workflow job, you must make another web service call toostart hello job after hello job is created.</span></span> <span data-ttu-id="37bd8-336">In dit geval wordt Hallo coordinator taak geactiveerd door tijd.</span><span class="sxs-lookup"><span data-stu-id="37bd8-336">In this case, hello coordinator job is triggered by time.</span></span> <span data-ttu-id="37bd8-337">Hallo-taak wordt automatisch gestart.</span><span class="sxs-lookup"><span data-stu-id="37bd8-337">hello job will start automatically.</span></span>

6. <span data-ttu-id="37bd8-338">Hallo na toohello script toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-338">Append hello following toohello script.</span></span> <span data-ttu-id="37bd8-339">Dit onderdeel controleert de status van de taak Oozie Hallo:</span><span class="sxs-lookup"><span data-stu-id="37bd8-339">This part checks hello Oozie job status:</span></span>

    ```powershell
    function checkOozieJobStatus($oozieJobId)
    {
        # get job status
        Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

        Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
        $clusterUriGetJobStatus = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $creds
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")

        while($JobStatus -notmatch "SUCCEEDED|KILLED")
        {
            Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
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

7. <span data-ttu-id="37bd8-340">(Optioneel) Hallo na toohello script toevoegen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-340">(Optional) Append hello following toohello script.</span></span>

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
        Write-Host "Killing hello Oozie job $oozieJobId..." -ForegroundColor Green
        $clusterUriStartJob = "https://$clusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=kill" #Valid values for hello 'action' parameter are 'start', 'suspend', 'resume', 'kill', 'dryrun', 'rerun', and 'change'.
        $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $creds | Format-Table -HideTableHeaders -debug
    }
    ```

8. <span data-ttu-id="37bd8-341">Hallo na toohello script toevoegen:</span><span class="sxs-lookup"><span data-stu-id="37bd8-341">Append hello following toohello script:</span></span>

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    <span data-ttu-id="37bd8-342">Hallo # tekens verwijderen als u wilt dat toorun Hallo extra functies.</span><span class="sxs-lookup"><span data-stu-id="37bd8-342">Remove hello # signs if you want toorun hello additional functions.</span></span>
9. <span data-ttu-id="37bd8-343">Als uw HDinsight-cluster versie 2.1 is vervangen door "https://$clusterName.azurehdinsight.net:443/oozie/v2/' met 'https://$clusterName.azurehdinsight.net:443/oozie/v1/'.</span><span class="sxs-lookup"><span data-stu-id="37bd8-343">If your HDinsight cluster is version 2.1, replace "https://$clusterName.azurehdinsight.net:443/oozie/v2/" with "https://$clusterName.azurehdinsight.net:443/oozie/v1/".</span></span> <span data-ttu-id="37bd8-344">HDInsight-cluster versie 2.1 komt niet ondersteunt versie 2 van het Hallo-webservices.</span><span class="sxs-lookup"><span data-stu-id="37bd8-344">HDInsight cluster version 2.1 does not supports version 2 of hello web services.</span></span>
10. <span data-ttu-id="37bd8-345">Klik op **-Script uitvoeren** of druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="37bd8-345">Click **Run Script** or press **F5** toorun hello script.</span></span> <span data-ttu-id="37bd8-346">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="37bd8-346">hello output will be similar to:</span></span>

     ![Zelfstudie voor uitvoer van de werkstroom uitvoeren][img-runworkflow-output]
11. <span data-ttu-id="37bd8-348">Verbinding maken met SQL-Database toosee Hallo geëxporteerd gegevens tooyour.</span><span class="sxs-lookup"><span data-stu-id="37bd8-348">Connect tooyour SQL Database toosee hello exported data.</span></span>

<span data-ttu-id="37bd8-349">**toocheck hello taak foutenlogboek**</span><span class="sxs-lookup"><span data-stu-id="37bd8-349">**toocheck hello job error log**</span></span>

<span data-ttu-id="37bd8-350">tootroubleshoot een werkstroom, Hallo Oozie-logboekbestand kan worden gevonden op C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log van Hallo cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="37bd8-350">tootroubleshoot a workflow, hello Oozie log file can be found at C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log from hello cluster headnode.</span></span> <span data-ttu-id="37bd8-351">Zie voor informatie over RDP, [beheer van HDInsight-clusters met behulp van Azure-portal Hallo][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="37bd8-351">For information on RDP, see [Administering HDInsight clusters using hello Azure portal][hdinsight-admin-portal].</span></span>

<span data-ttu-id="37bd8-352">**toorerun Hallo-zelfstudie**</span><span class="sxs-lookup"><span data-stu-id="37bd8-352">**toorerun hello tutorial**</span></span>

<span data-ttu-id="37bd8-353">toorerun hello werkstroom, moet u Hallo volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="37bd8-353">toorerun hello workflow, you must perform hello following tasks:</span></span>

* <span data-ttu-id="37bd8-354">Hallo Hive-scriptbestand uitvoer verwijderen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-354">Delete hello Hive script output file.</span></span>
* <span data-ttu-id="37bd8-355">Hallo-gegevens in Hallo log4jLogsCount tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="37bd8-355">Delete hello data in hello log4jLogsCount table.</span></span>

<span data-ttu-id="37bd8-356">Hier volgt een voorbeeld van een Windows PowerShell script die u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="37bd8-356">Here is a sample Windows PowerShell script that you can use:</span></span>

```powershell
$storageAccountName = "<AzureStorageAccountName>"
$containerName = "<ContainerName>"

#SQL database variables
$sqlDatabaseServer = "<SQLDatabaseServerName>"
$sqlDatabaseLogin = "<SQLDatabaseLoginName>"
$sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>"
$sqlDatabaseName = "<SQLDatabaseName>"
$sqlDatabaseTableName = "log4jLogsCount"

Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
$storageaccountkey = get-azurestoragekey $storageAccountName | %{$_.Primary}
$destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey
Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $containerName

Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
$conn = New-Object System.Data.SqlClient.SqlConnection
$conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabaseLoginPassword;Encrypt=true;Trusted_Connection=false;"
$conn.open()
$cmd = New-Object System.Data.SqlClient.SqlCommand
$cmd.connection = $conn
$cmd.commandtext = "delete from $sqlDatabaseTableName"
$cmd.executenonquery()

$conn.close()
```

## <a name="next-steps"></a><span data-ttu-id="37bd8-357">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="37bd8-357">Next steps</span></span>
<span data-ttu-id="37bd8-358">In deze zelfstudie hebt u geleerd hoe toodefine een werkstroom Oozie en Oozie-coördinator en hoe toorun Oozie-coördinator taak met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="37bd8-358">In this tutorial, you learned how toodefine an Oozie workflow and an Oozie coordinator, and how toorun an Oozie coordinator job by using Azure PowerShell.</span></span> <span data-ttu-id="37bd8-359">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="37bd8-359">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="37bd8-360">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="37bd8-360">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="37bd8-361">[Azure Blob storage gebruiken met HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="37bd8-361">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="37bd8-362">[HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="37bd8-362">[Administer HDInsight by using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="37bd8-363">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="37bd8-363">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="37bd8-364">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="37bd8-364">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="37bd8-365">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="37bd8-365">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="37bd8-366">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="37bd8-366">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="37bd8-367">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="37bd8-367">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-java-mapreduce]</span></span>

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
