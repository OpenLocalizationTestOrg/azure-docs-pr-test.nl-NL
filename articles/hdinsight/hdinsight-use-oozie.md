---
title: aaaUse Hadoop Oozie in HDInsight | Microsoft Docs
description: Hadoop Oozie in HDInsight, een big data-service gebruiken. Meer informatie over hoe toodefine een Oozie-werkstroom en het verzenden van een Oozie-taak.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="ec718-104">Oozie gebruiken met Hadoop toodefine en uitvoeren van een werkstroom in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ec718-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="ec718-105">Meer informatie over hoe Hallo toouse Apache Oozie toodefine een werkstroom en voer de werkstroom op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ec718-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="ec718-106">toolearn over Hallo Oozie-coördinator, Zie [op basis van tijd Hadoop Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="ec718-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="ec718-107">Azure Data Factory toolearn Zie [Use Pig en Hive met Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="ec718-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="ec718-108">Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="ec718-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="ec718-109">Het is geïntegreerd met Hadoop-stack Hallo en Hadoop-taken voor Apache MapReduce, Apache Pig, Apache Hive en Apache Sqoop ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="ec718-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="ec718-110">Het kan ook worden de gebruikte tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn.</span><span class="sxs-lookup"><span data-stu-id="ec718-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="ec718-111">Hallo-werkstroom die u implementeren door Hallo-instructies in deze zelfstudie bevat twee acties:</span><span class="sxs-lookup"><span data-stu-id="ec718-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Werkstroomdiagram][img-workflow-diagram]

1. <span data-ttu-id="ec718-113">Een Hive-actie wordt een HiveQL-script toocount Hallo exemplaren van elk type logboek-niveau uitgevoerd in een bestand log4j.</span><span class="sxs-lookup"><span data-stu-id="ec718-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="ec718-114">Elk bestand log4j bestaat uit een line-of velden met een [LOGBOEKNIVEAU] veld waarin Hallo-type en de ernst van hello, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ec718-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="ec718-115">Hallo Hive-scriptuitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="ec718-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="ec718-116">Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.</span><span class="sxs-lookup"><span data-stu-id="ec718-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="ec718-117">Een actie Sqoop exporteert Hallo HiveQL tooa uitvoertabel in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="ec718-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="ec718-118">Zie voor meer informatie over Sqoop [Hadoop-Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="ec718-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="ec718-119">Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="ec718-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="ec718-120">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec718-120">Prerequisites</span></span>
<span data-ttu-id="ec718-121">Voordat u deze zelfstudie begint, moet u hebben Hallo volgende item:</span><span class="sxs-lookup"><span data-stu-id="ec718-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="ec718-122">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ec718-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="ec718-123">Oozie werkstroom definiëren en Hallo gerelateerde HiveQL-script</span><span class="sxs-lookup"><span data-stu-id="ec718-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="ec718-124">Oozie werkstromen definities worden geschreven in hPDL (een XML-proces Definition Language).</span><span class="sxs-lookup"><span data-stu-id="ec718-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="ec718-125">Hallo werkstroom standaardbestandsnaam is *workflow.xml*.</span><span class="sxs-lookup"><span data-stu-id="ec718-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="ec718-126">Hallo volgt Hallo werkstroombestand dat u in deze zelfstudie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ec718-126">hello following is hello workflow file you use in this tutorial.</span></span>

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

<span data-ttu-id="ec718-127">Er zijn twee acties in de werkstroom Hallo gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="ec718-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="ec718-128">Hallo start-tooaction is *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="ec718-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="ec718-129">Als Hallo actie met succes wordt uitgevoerd, is de volgende actie Hallo *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="ec718-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="ec718-130">Hallo RunHiveScript heeft meerdere variabelen.</span><span class="sxs-lookup"><span data-stu-id="ec718-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="ec718-131">U kunt Hallo waarden doorgeven bij het verzenden van Hallo Oozie taak vanuit uw werkstation met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec718-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="ec718-132">Werkstroomvariabelen</span><span class="sxs-lookup"><span data-stu-id="ec718-132">Workflow variables</span></span></th><th><span data-ttu-id="ec718-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ec718-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="ec718-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="ec718-134">${jobTracker}</span></span></td><td><span data-ttu-id="ec718-135">Hiermee geeft u Hallo-URL van Hallo Hadoop taak vastleggen.</span><span class="sxs-lookup"><span data-stu-id="ec718-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="ec718-136">Gebruik <strong>jobtrackerhost:9010</strong> in HDInsight versie 3.0 en 2.1.</span><span class="sxs-lookup"><span data-stu-id="ec718-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="ec718-137">${nameNode}</span></span></td><td><span data-ttu-id="ec718-138">Hiermee geeft u Hallo-URL van Hallo Hadoop naam knooppunt.</span><span class="sxs-lookup"><span data-stu-id="ec718-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="ec718-139">Hallo bestand system standaardadres gebruiken, bijvoorbeeld <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</span><span class="sxs-lookup"><span data-stu-id="ec718-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-140">${Wachtrijnaam}</span><span class="sxs-lookup"><span data-stu-id="ec718-140">${queueName}</span></span></td><td><span data-ttu-id="ec718-141">Hiermee geeft u op Hallo wachtrijnaam die Hallo taak wordt verzonden naar.</span><span class="sxs-lookup"><span data-stu-id="ec718-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="ec718-142">Gebruik Hallo <strong>standaard</strong>.</span><span class="sxs-lookup"><span data-stu-id="ec718-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="ec718-143">Hive actie variabele</span><span class="sxs-lookup"><span data-stu-id="ec718-143">Hive action variable</span></span></th><th><span data-ttu-id="ec718-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ec718-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="ec718-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="ec718-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="ec718-146">Hiermee geeft u de bronmap Hallo voor Hallo Create Table Hive-opdracht.</span><span class="sxs-lookup"><span data-stu-id="ec718-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="ec718-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="ec718-148">Hiermee geeft u de uitvoermap Hallo voor Hallo-instructie INSERT OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="ec718-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="ec718-149">${hiveTableName}</span></span></td><td><span data-ttu-id="ec718-150">Geeft de naam Hallo van Hallo Hive-tabel die verwijst naar Hallo log4j gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="ec718-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="ec718-151">Sqoop actie variabele</span><span class="sxs-lookup"><span data-stu-id="ec718-151">Sqoop action variable</span></span></th><th><span data-ttu-id="ec718-152">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ec718-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="ec718-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="ec718-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="ec718-154">Hiermee geeft u hello Azure SQL database-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="ec718-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="ec718-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="ec718-156">Geeft aan waar Hallo gegevens worden geëxporteerd naar Azure SQL-databasetabel voor Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec718-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="ec718-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="ec718-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="ec718-158">Hiermee geeft u Hallo uitvoermap voor Hallo instructie Hive invoegen OVERSCHRIJVEN.</span><span class="sxs-lookup"><span data-stu-id="ec718-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="ec718-159">Dit is Hallo dezelfde map voor het exporteren van de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="ec718-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="ec718-160">Zie voor meer informatie over Oozie-werkstroom en het gebruik van de werkstroomacties [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="ec718-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="ec718-161">Hallo Hive actie in de werkstroom Hallo roept een scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="ec718-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="ec718-162">Dit scriptbestand bevat drie HiveQL-instructies:</span><span class="sxs-lookup"><span data-stu-id="ec718-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="ec718-163">**Hallo DROP TABLE-instructie** verwijderingen Hallo log4j Hive-tabel als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="ec718-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="ec718-164">**Hallo CREATE TABLE-instructie** maakt een log4j Hive externe tabel die toohello locatie van Hallo log4j log-bestand verwijst.</span><span class="sxs-lookup"><span data-stu-id="ec718-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="ec718-165">Hallo veldscheidingsteken is ",".</span><span class="sxs-lookup"><span data-stu-id="ec718-165">hello field delimiter is ",".</span></span> <span data-ttu-id="ec718-166">Hallo standaard regel scheidingsteken is '\n'.</span><span class="sxs-lookup"><span data-stu-id="ec718-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="ec718-167">Een externe Hive-tabel is gebruikte tooavoid Hallo-gegevensbestand van de oorspronkelijke locatie hello wordt verwijderd als u toorun hello Oozie werkstroom meerdere keren wilt.</span><span class="sxs-lookup"><span data-stu-id="ec718-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="ec718-168">**Hallo-instructie INSERT OVERSCHRIJVEN** telt Hallo exemplaren van elk type logboek-niveau van Hallo log4j Hive-tabel en slaat Hallo uitvoer tooa blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="ec718-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="ec718-169">Er zijn drie variabelen in Hallo script gebruikt:</span><span class="sxs-lookup"><span data-stu-id="ec718-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="ec718-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="ec718-170">${hiveTableName}</span></span>
* <span data-ttu-id="ec718-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="ec718-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="ec718-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="ec718-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="ec718-173">Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="ec718-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="ec718-174">Zowel Hallo werkstroombestand als Hallo HiveQL bestand worden opgeslagen in een blob-container.</span><span class="sxs-lookup"><span data-stu-id="ec718-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="ec718-175">Hallo PowerShell-script die u later in deze zelfstudie gebruiken beide standaardopslagaccount toohello bestanden gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="ec718-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="ec718-176">Met behulp van PowerShell Oozie-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="ec718-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="ec718-177">Azure PowerShell biedt momenteel niet alle cmdlets voor het definiëren van Oozie-taken.</span><span class="sxs-lookup"><span data-stu-id="ec718-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="ec718-178">U kunt Hallo **Invoke-RestMethod** cmdlet tooinvoke Oozie-webservices.</span><span class="sxs-lookup"><span data-stu-id="ec718-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="ec718-179">Hallo Oozie webservices-API is een HTTP REST-API JSON.</span><span class="sxs-lookup"><span data-stu-id="ec718-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="ec718-180">Zie voor meer informatie over Hallo Oozie web API-services, [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight versie 2.1).</span><span class="sxs-lookup"><span data-stu-id="ec718-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="ec718-181">Hallo PowerShell-script in deze sectie voert Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec718-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="ec718-182">Verbinding maken met tooAzure.</span><span class="sxs-lookup"><span data-stu-id="ec718-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="ec718-183">Maak een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ec718-183">Create an Azure resource group.</span></span> <span data-ttu-id="ec718-184">Zie voor meer informatie [gebruik Azure PowerShell met Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="ec718-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="ec718-185">Een Azure SQL Database-server, een Azure SQL database en twee tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="ec718-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="ec718-186">Deze worden gebruikt door Hallo Sqoop actie in Hallo-werkstroom.</span><span class="sxs-lookup"><span data-stu-id="ec718-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="ec718-187">Hallo-tabelnaam is *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="ec718-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="ec718-188">Een HDInsight-cluster gebruikt toorun Oozie-taken maken.</span><span class="sxs-lookup"><span data-stu-id="ec718-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="ec718-189">tooexamine hello cluster, kunt u hello Azure-portal of Azure PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec718-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="ec718-190">Kopieer bestand Hallo oozie-werkstroom en Hallo HiveQL-script bestand toohello standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="ec718-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="ec718-191">Beide bestanden worden opgeslagen in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="ec718-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="ec718-192">Hallo HiveQL-script (useoozie.hql) tooAzure opslag (wasb:///tutorials/useoozie/useoozie.hql) kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ec718-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="ec718-193">Kopieer workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="ec718-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="ec718-194">Bestand kopiëren Hallo-gegevens (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="ec718-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="ec718-195">Verzenden van een Oozie-taak.</span><span class="sxs-lookup"><span data-stu-id="ec718-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="ec718-196">tooexamine hello OOzie taak resultaten Visual Studio of andere hulpprogramma's tooconnect toohello Azure SQL Database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec718-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="ec718-197">Hier is Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="ec718-197">Here is hello script.</span></span>  <span data-ttu-id="ec718-198">U kunt Hallo-script uitvoeren van Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="ec718-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="ec718-199">U hoeft alleen tooconfigure Hallo eerste 7 variabelen.</span><span class="sxs-lookup"><span data-stu-id="ec718-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

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
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="ec718-200">**Hallo toore-run-zelfstudie**</span><span class="sxs-lookup"><span data-stu-id="ec718-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="ec718-201">werkstroom toore-run hello, moet u Hallo volgende items verwijderen:</span><span class="sxs-lookup"><span data-stu-id="ec718-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="ec718-202">Hallo Hive-scriptbestand uitvoer</span><span class="sxs-lookup"><span data-stu-id="ec718-202">hello Hive script output file</span></span>
* <span data-ttu-id="ec718-203">Hallo-gegevens in Hallo log4jLogsCount tabel</span><span class="sxs-lookup"><span data-stu-id="ec718-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="ec718-204">Hier volgt een voorbeeld PowerShell-script die u kunt gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ec718-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="ec718-205">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ec718-205">Next steps</span></span>
<span data-ttu-id="ec718-206">In deze zelfstudie hebt u geleerd hoe een Oozie toodefine werkstroom en hoe toorun een Oozie taak met behulp van PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ec718-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="ec718-207">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ec718-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="ec718-208">[Tijd gebaseerde Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="ec718-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="ec718-209">[Aan de slag met Hadoop Hive in HDInsight tooanalyze mobiele telefoon gebruiken][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="ec718-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="ec718-210">[Azure Blob storage gebruiken met HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="ec718-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="ec718-211">[HDInsight met behulp van PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="ec718-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="ec718-212">[Uploaden van gegevens voor Hadoop-taken in HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ec718-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ec718-213">[Sqoop gebruiken met Hadoop in HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="ec718-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="ec718-214">[Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ec718-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="ec718-215">[Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ec718-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ec718-216">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ec718-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png  
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
