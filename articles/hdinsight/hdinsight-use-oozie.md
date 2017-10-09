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
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a>Oozie gebruiken met Hadoop toodefine en uitvoeren van een werkstroom in HDInsight
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

Meer informatie over hoe Hallo toouse Apache Oozie toodefine een werkstroom en voer de werkstroom op HDInsight. toolearn over Hallo Oozie-coördinator, Zie [op basis van tijd Hadoop Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time]. Azure Data Factory toolearn Zie [Use Pig en Hive met Data Factory][azure-data-factory-pig-hive].

Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd. Het is geïntegreerd met Hadoop-stack Hallo en Hadoop-taken voor Apache MapReduce, Apache Pig, Apache Hive en Apache Sqoop ondersteunt. Het kan ook worden de gebruikte tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn.

Hallo-werkstroom die u implementeren door Hallo-instructies in deze zelfstudie bevat twee acties:

![Werkstroomdiagram][img-workflow-diagram]

1. Een Hive-actie wordt een HiveQL-script toocount Hallo exemplaren van elk type logboek-niveau uitgevoerd in een bestand log4j. Elk bestand log4j bestaat uit een line-of velden met een [LOGBOEKNIVEAU] veld waarin Hallo-type en de ernst van hello, bijvoorbeeld:
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    Hallo Hive-scriptuitvoer is vergelijkbaar met:
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over Hive.
2. Een actie Sqoop exporteert Hallo HiveQL tooa uitvoertabel in een Azure SQL database. Zie voor meer informatie over Sqoop [Hadoop-Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?] [hdinsight-versions].
> 
> 

### <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u hebben Hallo volgende item:

* **Een werkstation met Azure PowerShell**. 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Oozie werkstroom definiëren en Hallo gerelateerde HiveQL-script
Oozie werkstromen definities worden geschreven in hPDL (een XML-proces Definition Language). Hallo werkstroom standaardbestandsnaam is *workflow.xml*. Hallo volgt Hallo werkstroombestand dat u in deze zelfstudie gebruikt.

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

Er zijn twee acties in de werkstroom Hallo gedefinieerd. Hallo start-tooaction is *RunHiveScript*. Als Hallo actie met succes wordt uitgevoerd, is de volgende actie Hallo *RunSqoopExport*.

Hallo RunHiveScript heeft meerdere variabelen. U kunt Hallo waarden doorgeven bij het verzenden van Hallo Oozie taak vanuit uw werkstation met behulp van Azure PowerShell.

<table border = "1">
<tr><th>Werkstroomvariabelen</th><th>Beschrijving</th></tr>
<tr><td>${jobTracker}</td><td>Hiermee geeft u Hallo-URL van Hallo Hadoop taak vastleggen. Gebruik <strong>jobtrackerhost:9010</strong> in HDInsight versie 3.0 en 2.1.</td></tr>
<tr><td>${nameNode}</td><td>Hiermee geeft u Hallo-URL van Hallo Hadoop naam knooppunt. Hallo bestand system standaardadres gebruiken, bijvoorbeeld <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
<tr><td>${Wachtrijnaam}</td><td>Hiermee geeft u op Hallo wachtrijnaam die Hallo taak wordt verzonden naar. Gebruik Hallo <strong>standaard</strong>.</td></tr>
</table>

<table border = "1">
<tr><th>Hive actie variabele</th><th>Beschrijving</th></tr>
<tr><td>${hiveDataFolder}</td><td>Hiermee geeft u de bronmap Hallo voor Hallo Create Table Hive-opdracht.</td></tr>
<tr><td>${hiveOutputFolder}</td><td>Hiermee geeft u de uitvoermap Hallo voor Hallo-instructie INSERT OVERSCHRIJVEN.</td></tr>
<tr><td>${hiveTableName}</td><td>Geeft de naam Hallo van Hallo Hive-tabel die verwijst naar Hallo log4j gegevensbestanden worden opgeslagen.</td></tr>
</table>

<table border = "1">
<tr><th>Sqoop actie variabele</th><th>Beschrijving</th></tr>
<tr><td>${sqlDatabaseConnectionString}</td><td>Hiermee geeft u hello Azure SQL database-verbindingsreeks.</td></tr>
<tr><td>${sqlDatabaseTableName}</td><td>Geeft aan waar Hallo gegevens worden geëxporteerd naar Azure SQL-databasetabel voor Hallo.</td></tr>
<tr><td>${hiveOutputFolder}</td><td>Hiermee geeft u Hallo uitvoermap voor Hallo instructie Hive invoegen OVERSCHRIJVEN. Dit is Hallo dezelfde map voor het exporteren van de Sqoop hello (export-dir).</td></tr>
</table>

Zie voor meer informatie over Oozie-werkstroom en het gebruik van de werkstroomacties [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight versie 2.1).

Hallo Hive actie in de werkstroom Hallo roept een scriptbestand HiveQL. Dit scriptbestand bevat drie HiveQL-instructies:

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. **Hallo DROP TABLE-instructie** verwijderingen Hallo log4j Hive-tabel als deze bestaat.
2. **Hallo CREATE TABLE-instructie** maakt een log4j Hive externe tabel die toohello locatie van Hallo log4j log-bestand verwijst. Hallo veldscheidingsteken is ",". Hallo standaard regel scheidingsteken is '\n'. Een externe Hive-tabel is gebruikte tooavoid Hallo-gegevensbestand van de oorspronkelijke locatie hello wordt verwijderd als u toorun hello Oozie werkstroom meerdere keren wilt.
3. **Hallo-instructie INSERT OVERSCHRIJVEN** telt Hallo exemplaren van elk type logboek-niveau van Hallo log4j Hive-tabel en slaat Hallo uitvoer tooa blob in Azure Storage.

Er zijn drie variabelen in Hallo script gebruikt:

* ${hiveTableName}
* ${hiveDataFolder}
* ${hiveOutputFolder}

Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime.

Zowel Hallo werkstroombestand als Hallo HiveQL bestand worden opgeslagen in een blob-container.  Hallo PowerShell-script die u later in deze zelfstudie gebruiken beide standaardopslagaccount toohello bestanden gekopieerd. 

## <a name="submit-oozie-jobs-using-powershell"></a>Met behulp van PowerShell Oozie-taken verzenden
Azure PowerShell biedt momenteel niet alle cmdlets voor het definiëren van Oozie-taken. U kunt Hallo **Invoke-RestMethod** cmdlet tooinvoke Oozie-webservices. Hallo Oozie webservices-API is een HTTP REST-API JSON. Zie voor meer informatie over Hallo Oozie web API-services, [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight versie 2.1).

Hallo PowerShell-script in deze sectie voert Hallo stappen te volgen:

1. Verbinding maken met tooAzure.
2. Maak een Azure-resourcegroep. Zie voor meer informatie [gebruik Azure PowerShell met Azure Resource Manager](../powershell-azure-resource-manager.md).
3. Een Azure SQL Database-server, een Azure SQL database en twee tabellen maken. Deze worden gebruikt door Hallo Sqoop actie in Hallo-werkstroom.
   
    Hallo-tabelnaam is *log4jLogCount*.
4. Een HDInsight-cluster gebruikt toorun Oozie-taken maken.
   
    tooexamine hello cluster, kunt u hello Azure-portal of Azure PowerShell gebruiken.
5. Kopieer bestand Hallo oozie-werkstroom en Hallo HiveQL-script bestand toohello standaardbestandssysteem.
   
    Beide bestanden worden opgeslagen in een openbare Blob-container.
   
   * Hallo HiveQL-script (useoozie.hql) tooAzure opslag (wasb:///tutorials/useoozie/useoozie.hql) kopiëren.
   * Kopieer workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
   * Bestand kopiëren Hallo-gegevens (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
6. Verzenden van een Oozie-taak.
   
    tooexamine hello OOzie taak resultaten Visual Studio of andere hulpprogramma's tooconnect toohello Azure SQL Database gebruiken.

Hier is Hallo-script.  U kunt Hallo-script uitvoeren van Windows PowerShell ISE. U hoeft alleen tooconfigure Hallo eerste 7 variabelen.

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


**Hallo toore-run-zelfstudie**

werkstroom toore-run hello, moet u Hallo volgende items verwijderen:

* Hallo Hive-scriptbestand uitvoer
* Hallo-gegevens in Hallo log4jLogsCount tabel

Hier volgt een voorbeeld PowerShell-script die u kunt gebruiken:

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

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe een Oozie toodefine werkstroom en hoe toorun een Oozie taak met behulp van PowerShell. toolearn Zie meer Hallo artikelen te volgen:

* [Tijd gebaseerde Oozie-coördinator gebruiken met HDInsight][hdinsight-oozie-coordinator-time]
* [Aan de slag met Hadoop Hive in HDInsight tooanalyze mobiele telefoon gebruiken][hdinsight-get-started]
* [Azure Blob storage gebruiken met HDInsight][hdinsight-storage]
* [HDInsight met behulp van PowerShell beheren][hdinsight-admin-powershell]
* [Uploaden van gegevens voor Hadoop-taken in HDInsight][hdinsight-upload-data]
* [Sqoop gebruiken met Hadoop in HDInsight][hdinsight-use-sqoop]
* [Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]
* [Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]
* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]

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
