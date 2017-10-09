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
# <a name="use-time-based-oozie-coordinator-with-hadoop-in-hdinsight-toodefine-workflows-and-coordinate-jobs"></a>Tijd gebaseerde Oozie-coördinator gebruiken met Hadoop in HDInsight toodefine werkstromen en coördineren van taken
In dit artikel leert u hoe toodefine werkstromen en coördinator en hoe tootrigger Hallo coordinator taken, op basis van tijd. Het is nuttig toogo via [Oozie gebruiken met HDInsight] [ hdinsight-use-oozie] voordat u dit artikel leest. Bovendien tooOozie, u kunt ook taken plannen met behulp van Azure Data Factory. Azure Data Factory toolearn Zie [Use Pig en Hive met Data Factory](../data-factory/data-factory-data-transformation-activities.md).

> [!NOTE]
> In dit artikel is een cluster met HDInsight op basis van Windows vereist. Zie voor meer informatie over het gebruik van Oozie, met inbegrip van taken op basis van tijd op een cluster op basis van Linux [Oozie gebruiken met Hadoop toodefine en een werkstroom wordt uitgevoerd op Linux gebaseerde HDInsight](hdinsight-use-oozie-linux-mac.md)

## <a name="what-is-oozie"></a>Wat is Oozie
Apache Oozie is een werkstroom/coördinatie systeem waarmee Hadoop-taken worden beheerd. Het is geïntegreerd met Hadoop-stack Hallo en Hadoop-taken voor Apache MapReduce, Apache Pig, Apache Hive en Apache Sqoop ondersteunt. Het kan ook worden de gebruikte tooschedule taken die specifieke tooa systeem, zoals Java-programma's of shell-scripts zijn.

Hallo toont volgende afbeelding Hallo werkstroom die u wilt implementeren:

![Werkstroomdiagram][img-workflow-diagram]

Hallo workflow bevat twee acties:

1. Een Hive-actie wordt het een HiveQL-script toocount Hallo exemplaren van elk type logboek-niveau in een logboekbestand log4j uitgevoerd. Elk logboek log4j bestaat uit een line-of velden met een [LOGBOEKNIVEAU] veld tooshow Hallo type en Hallo ernst, bijvoorbeeld:

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
2. Een actie Sqoop exporteert Hallo HiveQL actie tooa uitvoertabel in een Azure SQL database. Zie voor meer informatie over Sqoop [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].

> [!NOTE]
> Zie voor ondersteunde versies van de Oozie op HDInsight-clusters, [wat is er nieuw in Hallo-clusterversies geleverd door HDInsight?] [hdinsight-versions].
>
>

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een werkstation met Azure PowerShell**.

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en verdwijnt per 1 januari 2017. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.

* **Een HDInsight-cluster**. Zie voor meer informatie over het maken van een HDInsight-cluster [HDInsight-clusters maken][hdinsight-provision], of [aan de slag met HDInsight][hdinsight-get-started]. U moet Hallo gegevens toogo Hallo-zelfstudie te volgen:

    <table border = "1">
    <tr><th>Cluster-eigenschap</th><th>Naam variabele voor Windows PowerShell</th><th>Waarde</th><th>Beschrijving</th></tr>
    <tr><td>De naam van de HDInsight-cluster</td><td>$clusterName</td><td></td><td>Hallo HDInsight-cluster op waarop u deze zelfstudie wordt uitgevoerd.</td></tr>
    <tr><td>Gebruikersnaam voor HDInsight-cluster</td><td>$clusterUsername</td><td></td><td>gebruikersnaam voor Hallo HDInsight-cluster. </td></tr>
    <tr><td>HDInsight-cluster gebruikerswachtwoord </td><td>$clusterPassword</td><td></td><td>wachtwoord voor gebruiker Hallo HDInsight-cluster.</td></tr>
    <tr><td>Naam van het Azure-opslagaccount</td><td>$storageAccountName</td><td></td><td>Een Azure Storage-account beschikbaar toohello HDInsight-cluster. Voor deze zelfstudie gebruiken Hallo storage-standaardaccount die u hebt opgegeven tijdens het Hallo-cluster inrichten.</td></tr>
    <tr><td>Naam van een Azure Blob-container</td><td>$containerName</td><td></td><td>In dit voorbeeld gebruiken hello Azure Blob storage-container die wordt gebruikt voor Hallo standaard HDInsight-cluster-bestandssysteem. Standaard heeft dezelfde naam als de HDInsight-cluster Hallo Hallo.</td></tr>
    </table>
* **Een Azure SQL database**. Een firewallregel voor Hallo tooallow toegang tot SQL Database-server moet u configureren vanuit uw werkstation. Zie voor instructies over het maken van een Azure SQL database en Hallo firewall configureren [aan de slag met Azure SQL database] [SQL-get-started]. Dit artikel bevat een Windows PowerShell-script voor het maken van hello Azure SQL database-tabel die u nodig hebt voor deze zelfstudie.

    <table border = "1">
    <tr><th>SQL database-eigenschap</th><th>Naam variabele voor Windows PowerShell</th><th>Waarde</th><th>Beschrijving</th></tr>
    <tr><td>SQL server-databasenaam</td><td>$sqlDatabaseServer</td><td></td><td>Hallo SQL database-server toowhich Sqoop worden gegevens geëxporteerd. </td></tr>
    <tr><td>Aanmeldingsnaam voor SQL-database</td><td>$sqlDatabaseLogin</td><td></td><td>Aanmeldingsnaam van de SQL-Database.</td></tr>
    <tr><td>Aanmeldingswachtwoord voor SQL-database</td><td>$sqlDatabaseLoginPassword</td><td></td><td>Aanmeldingswachtwoord voor SQL-Database.</td></tr>
    <tr><td>Naam van de SQL-database</td><td>$sqlDatabaseName</td><td></td><td>Hello Azure SQL database toowhich Sqoop worden gegevens geëxporteerd. </td></tr>
    </table>

  > [!NOTE]
  > Standaard wordt in een Azure SQL database verbindingen toelaat van Azure-Services, zoals Azure HDInsight. Als deze firewallinstelling is uitgeschakeld, moet u het inschakelen van hello Azure-Portal. Zie voor instructies over het maken van een SQL-Database en firewallregels configureren [maken en configureren van de SQL-Database][sqldatabase-get-started].

> [!NOTE]
> Hallo-waarden invullen in Hallo tabellen. Dit is handig voor het doorlopen van deze zelfstudie.

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a>Oozie werkstroom definiëren en Hallo gerelateerde HiveQL-script
Oozie werkstromen definities worden geschreven in hPDL (een XML-proces definition language). Hallo werkstroom standaardbestandsnaam is *workflow.xml*.  U Hallo werkstroombestand lokaal opslaan en vervolgens deze toohello HDInsight-cluster implementeren met behulp van Azure PowerShell verderop in deze zelfstudie.

Hallo Hive actie in de werkstroom Hallo roept een scriptbestand HiveQL. Dit scriptbestand bevat drie HiveQL-instructies:

1. **Hallo DROP TABLE-instructie** verwijderingen Hallo log4j Hive-tabel als deze bestaat.
2. **Hallo CREATE TABLE-instructie** maakt een log4j Hive externe tabel toohello locatie van Hallo log4j logboekbestand verwijst.
3. **locatie van Hallo log4j logboekbestand Hallo**. Hallo veldscheidingsteken is ",". Hallo standaard regel scheidingsteken is '\n'. Een externe Hive-tabel is Hallo-gegevensbestand voor het gebruikte tooavoid wordt verwijderd uit de oorspronkelijke locatie hello, als u meerdere keren door toorun hello Oozie werkstroom wilt.
4. **Hallo-instructie INSERT OVERSCHRIJVEN** telt Hallo exemplaren van elk type logboek-niveau van Hallo log4j Hive-tabel en Hallo tooan Azure Blob storage uitvoerlocatie wordt opgeslagen.

> [!NOTE]
> Er is een bekend probleem voor Hive-pad. Voert u dit probleem is opgetreden bij het indienen van een Oozie-taak. Hallo instructies voor het verhelpen van Hallo probleem vindt u op Hallo TechNet-Wiki: [HDInsight Hive-fout: kan geen toorename][technetwiki-hive-error].

**toodefine hello HiveQL-script bestand toobe aangeroepen door Hallo-werkstroom**

1. Maak een tekstbestand met Hallo volgende inhoud:

        DROP TABLE ${hiveTableName};
        CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
        INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

    Er zijn drie variabelen in Hallo script gebruikt:

   * ${hiveTableName}
   * ${hiveDataFolder}
   * ${hiveOutputFolder}

     Hallo werkstroom-definitiebestand (workflow.xml in deze zelfstudie) geeft deze waarden toothis HiveQL-script tijdens runtime.
2. Hallo bestand opslaan als **C:\Tutorials\UseOozie\useooziewf.hql** met behulp van ANSI (ASCII) codering. (Kladblok gebruiken als uw teksteditor deze optie niet.) Dit scriptbestand wordt geïmplementeerde toohello HDInsight-cluster worden verderop in de zelfstudie Hallo.

**een werkstroom toodefine**

1. Maak een tekstbestand met Hallo volgende inhoud:

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

    Er zijn twee acties in de werkstroom Hallo gedefinieerd. Hallo start-tooaction is *RunHiveScript*. Als het Hallo-actie wordt uitgevoerd *OK*, is de volgende actie Hallo *RunSqoopExport*.

    Hallo RunHiveScript heeft meerdere variabelen. U doorgeven Hallo waarden bij het verzenden van Hallo Oozie taak vanuit uw werkstation met behulp van Azure PowerShell.

    Werkstroomvariabelen

    <table border = "1">
    <tr><th>Werkstroomvariabelen</th><th>Beschrijving</th></tr>
    <tr><td>${jobTracker}</td><td>Geef de URL Hallo van Hallo Hadoop taak vastleggen. Gebruik <strong>jobtrackerhost:9010</strong> cluster in HDInsight versie 3.0 en 2.0.</td></tr>
    <tr><td>${nameNode}</td><td>Geef de URL op Hallo van Hallo Hadoop naam knooppunt. Gebruik Hallo standaard bestand system wasb: / / adres, bijvoorbeeld <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. blob.core.windows.net</i>.</td></tr>
    <tr><td>${Wachtrijnaam}</td><td>Hiermee geeft u op Hallo wachtrijnaam die taak Hallo worden verzonden naar. Gebruik <strong>standaard</strong>.</td></tr>
    </table>

    Variabelen voor hive

    <table border = "1">
    <tr><th>Hive actie variabele</th><th>Beschrijving</th></tr>
    <tr><td>${hiveDataFolder}</td><td>Hallo bronmap voor Hallo Create Table Hive-opdracht.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Hallo uitvoermap voor Hallo-instructie INSERT OVERSCHRIJVEN.</td></tr>
    <tr><td>${hiveTableName}</td><td>Hallo-naam van Hallo Hive-tabel die verwijst naar Hallo log4j gegevensbestanden worden opgeslagen.</td></tr>
    </table>

    Variabelen voor de Sqoop

    <table border = "1">
    <tr><th>Sqoop actie variabele</th><th>Beschrijving</th></tr>
    <tr><td>${sqlDatabaseConnectionString}</td><td>Verbindingstekenreeks van de SQL-Database.</td></tr>
    <tr><td>${sqlDatabaseTableName}</td><td>Hello Azure SQL database toowhere Hallo tabelgegevens worden geëxporteerd.</td></tr>
    <tr><td>${hiveOutputFolder}</td><td>Hallo uitvoermap voor Hallo instructie Hive invoegen OVERSCHRIJVEN. Dit is Hallo dezelfde map voor het exporteren van de Sqoop hello (export-dir).</td></tr>
    </table>

    Zie voor meer informatie over Oozie-werkstroom en het gebruik van de werkstroomacties Hallo [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).

1. Hallo bestand opslaan als **C:\Tutorials\UseOozie\workflow.xml** met behulp van ANSI (ASCII) codering. (Kladblok gebruiken als uw teksteditor deze optie niet.)

**toodefine coordinator**

1. Maak een tekstbestand met Hallo volgende inhoud:

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
            <workflow>
                <app-path>${wfPath}</app-path>
            </workflow>
        </action>
    </coordinator-app>
    ```

    Er zijn vijf variabelen die worden gebruikt in het definitiebestand Hallo:

   | Variabele | Beschrijving |
   | --- | --- |
   | ${coordFrequency} |Taak onderbreken tijd. Frequentie wordt altijd uitgedrukt in minuten. |
   | ${coordStart} |Begintijd van taak. |
   | ${coordEnd} |Eindtijd van de taak. |
   | ${coordTimezone} |Oozie verwerkt taken in een vaste tijdzone coordinator met geen zomertijd (doorgaans weergegeven met behulp UTC). Deze tijdzone wordt verwezen als Hallo 'Oozie verwerking tijdzone." |
   | ${wfPath} |Hallo-pad voor Hallo workflow.xml.  Als bestandsnaam Hallo-werkstroom niet Hallo standaardbestandsnaam (workflow.xml), moet u deze opgeven. |
2. Hallo bestand opslaan als **C:\Tutorials\UseOozie\coordinator.xml** met behulp van Hallo ANSI (ASCII)-codering. (Kladblok gebruiken als uw teksteditor deze optie niet.)

## <a name="deploy-hello-oozie-project-and-prepare-hello-tutorial"></a>Hallo Oozie-project implementeert en bereid Hallo-zelfstudie
U kunt een Azure PowerShell-script tooperform Hallo volgende wordt uitgevoerd:

* Kopiëren Hallo HiveQL-script (useoozie.hql) tooAzure Blob-opslag, wasb:///tutorials/useoozie/useoozie.hql.
* Kopieer workflow.xml toowasb:///tutorials/useoozie/workflow.xml.
* Kopieer coordinator.xml toowasb:///tutorials/useoozie/coordinator.xml.
* Bestand kopiëren Hallo-gegevens (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.
* Maak een Azure SQL-databasetabel voor het opslaan van gegevens van Sqoop exporteren. Hallo-tabelnaam is *log4jLogCount*.

**Inzicht in HDInsight-opslag**

HDInsight gebruikt Azure Blob-opslag voor gegevensopslag. wasb: / / is Microsoft implementatie van Hallo Hadoop distributed file system (HDFS) in Azure Blob-opslag. Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].

Wanneer u een HDInsight-cluster inrichten, is een Azure Blob storage-account en een specifieke container uit dat account aangewezen als het standaardbestandssysteem hello, zoals in HDFS. Bovendien toothis storage-account, kunt u toevoegen extra opslagaccounts van Hallo dezelfde Azure-abonnement of van verschillende Azure-abonnementen tijdens het inrichtingsproces Hallo. Zie voor instructies over het toevoegen van extra opslagaccounts [HDInsight-clusters inrichten][hdinsight-provision]. toosimplify hello Azure PowerShell-script in deze zelfstudie gebruikt, alle bestanden worden opgeslagen in bestand Hallo-systeem standaardcontainer Hallo zich bevindt op *zelfstudies/useoozie*. Standaard is deze container Hallo dezelfde naam als de naam van een Hallo HDInsight-cluster.
Hallo-syntaxis is:

    wasb[s]://<ContainerName>@<StorageAccountName>.blob.core.windows.net/<path>/<filename>

> [!NOTE]
> Alleen Hallo *wasb: / /* syntaxis wordt ondersteund in HDInsight-cluster versie 3.0. Hallo oudere *asv: / /* syntaxis wordt ondersteund in HDInsight 2.1 en 1.6-clusters, maar wordt niet ondersteund in HDInsight 3.0-clusters.
>
> Hallo wasb: / / pad is een virtueel pad. Zie voor meer informatie [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].

Een bestand dat is opgeslagen in bestand Hallo-systeem standaardcontainer toegankelijk zijn vanuit HDInsight met behulp van Hallo URI's (ik gebruik workflow.xml als voorbeeld) te volgen:

    wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/workflow.xml
    wasb:///tutorials/useoozie/workflow.xml
    /tutorials/useoozie/workflow.xml

Als u tooaccess Hallo-bestand rechtstreeks uit Hallo storage-account wilt, wordt Hallo blob-naam voor het Hallo-bestand is:

    tutorials/useoozie/workflow.xml

**De interne en externe tabellen Hive begrijpen**

Er zijn enkele dingen die u tooknow over Hive interne en externe tabellen nodig:

* Hallo CREATE TABLE opdracht maakt een interne tabel, ook wel bekend als een beheerde tabel. Hallo gegevensbestand moet zich in de standaardcontainer Hallo.
* Hallo CREATE TABLE-opdracht wordt verplaatst Hallo gegevens bestand toohello/hivedatawarehouse/<TableName> map in de standaardcontainer Hallo.
* Hallo externe tabel maken opdracht maakt een externe tabel. Hallo-gegevensbestand kan buiten de standaardcontainer Hallo zich bevinden.
* Hallo externe tabel maken opdracht verplaatst geen Hallo-gegevensbestand.
* Hallo externe tabel maken opdracht toegestaan niet in alle submappen onder de Hallo-map die is opgegeven in Hallo locatie-component. Dit is Hallo reden waarom Hallo zelfstudie een kopie van Hallo sample.log bestand wordt.

Zie voor meer informatie [HDInsight: Hive interne en externe tabellen Intro][cindygross-hive-tables].

**tooprepare Hallo-zelfstudie**

1. Open Hallo Windows PowerShell ISE (in Windows 8 Start welkomstscherm, typt u **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**. Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).
2. Voer in het deelvenster onderaan Hallo, Hallo opdracht tooconnect tooyour Azure-abonnement na:

    ```powershell
    Add-AzureAccount
    ```

    U worden na vragen aan gebruiker tooenter de referenties van uw Azure-account. Deze methode voor het toevoegen van een abonnementsverbinding een time-out optreedt en na 12 uur, hebt u toorun Hallo cmdlet opnieuw.

   > [!NOTE]
   > Als er meerdere Azure-abonnementen en Hallo standaardabonnement is niet Hallo gewenste toouse, gebruikt u Hallo <strong>Select-AzureSubscription</strong> cmdlet tooselect een abonnement.

3. Hallo script volgen in het scriptvenster Hallo kopiëren en stel vervolgens de eerste zes variabelen Hallo:

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

    Zie voor meer beschrijvingen van de variabelen Hallo Hallo [vereisten](#prerequisites) sectie in deze zelfstudie.

4. Hallo toohello script in het scriptvenster Hallo volgende toevoegen:

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

5. Klik op **-Script uitvoeren** of druk op **F5** toorun Hallo script. Hallo-uitvoer is vergelijkbaar met:

    ![Uitvoer van de voorbereiding van de zelfstudie][img-preparation-output]

## <a name="run-hello-oozie-project"></a>Hallo Oozie-project uitvoeren
Azure PowerShell biedt momenteel niet alle cmdlets voor het definiëren van Oozie-taken. U kunt Hallo **Invoke-RestMethod** cmdlet tooinvoke Oozie-webservices. Hallo Oozie webservices-API is een HTTP REST-API JSON. Zie voor meer informatie over Hallo Oozie web API-services, [Apache Oozie 4.0 documentatie] [ apache-oozie-400] (voor HDInsight-cluster versie 3.0) of [Apache Oozie 3.3.2 documentatie] [ apache-oozie-332] (voor HDInsight-cluster versie 2.1).

**een taak Oozie toosubmit**

1. Open Hallo Windows PowerShell ISE (Typ in Windows 8 startscherm **PowerShell_ISE**, en klik vervolgens op **Windows PowerShell ISE**. Zie voor meer informatie [Start Windows PowerShell in Windows 8 en Windows][powershell-start]).
2. Kopiëren Hallo volgende script in het scriptvenster Hallo en vervolgens set eerst veertien variabelen Hallo (echter overslaan **$storageUri**).

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

    Zie voor meer beschrijvingen van de variabelen Hallo Hallo [vereisten](#prerequisites) sectie in deze zelfstudie.

    $coordstart en $coordend zijn Hallo werkstroom begin- en eindtijd. toofind hello UTC/GMT-tijd, zoeken 'utc-tijd' op bing.com. Hallo $coordFrequency is hoe vaak in minuten die u wilt dat toorun Hallo werkstroom.
3. Hallo na toohello script toevoegen. Dit onderdeel definieert Hallo Oozie nettolading:

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
   > Hallo het belangrijkste verschil vergeleken toohello werkstroom-opdrachtbestand nettolading is Hallo variabele **oozie.coord.application.path**. Wanneer u een werkstroomtaak indient, gebruikt u **oozie.wf.application.path** in plaats daarvan.

4. Hallo na toohello script toevoegen. Dit deel controleert de status van Hallo Oozie web service:

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

5. Hallo na toohello script toevoegen. Dit onderdeel maakt een taak Oozie:

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
   > Wanneer u een werkstroomtaak verzendt, moet u een andere web service aanroep toostart Hallo taak maken nadat Hallo-taak is gemaakt. In dit geval wordt Hallo coordinator taak geactiveerd door tijd. Hallo-taak wordt automatisch gestart.

6. Hallo na toohello script toevoegen. Dit onderdeel controleert de status van de taak Oozie Hallo:

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

7. (Optioneel) Hallo na toohello script toevoegen.

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

8. Hallo na toohello script toevoegen:

    ```powershell
    checkOozieServerStatus
    # listOozieJobs
    $oozieJobId = createOozieJob($oozieJobId)
    checkOozieJobStatus($oozieJobId)
    # ShowOozieJobLog($oozieJobId)
    # killOozieJob($oozieJobId)
    ```

    Hallo # tekens verwijderen als u wilt dat toorun Hallo extra functies.
9. Als uw HDinsight-cluster versie 2.1 is vervangen door "https://$clusterName.azurehdinsight.net:443/oozie/v2/' met 'https://$clusterName.azurehdinsight.net:443/oozie/v1/'. HDInsight-cluster versie 2.1 komt niet ondersteunt versie 2 van het Hallo-webservices.
10. Klik op **-Script uitvoeren** of druk op **F5** toorun Hallo script. Hallo-uitvoer is vergelijkbaar met:

     ![Zelfstudie voor uitvoer van de werkstroom uitvoeren][img-runworkflow-output]
11. Verbinding maken met SQL-Database toosee Hallo geëxporteerd gegevens tooyour.

**toocheck hello taak foutenlogboek**

tootroubleshoot een werkstroom, Hallo Oozie-logboekbestand kan worden gevonden op C:\apps\dist\oozie-3.3.2.1.3.2.0-05\oozie-win-distro\logs\Oozie.log van Hallo cluster headnode. Zie voor informatie over RDP, [beheer van HDInsight-clusters met behulp van Azure-portal Hallo][hdinsight-admin-portal].

**toorerun Hallo-zelfstudie**

toorerun hello werkstroom, moet u Hallo volgende taken uitvoeren:

* Hallo Hive-scriptbestand uitvoer verwijderen.
* Hallo-gegevens in Hallo log4jLogsCount tabel verwijderen.

Hier volgt een voorbeeld van een Windows PowerShell script die u kunt gebruiken:

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

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toodefine een werkstroom Oozie en Oozie-coördinator en hoe toorun Oozie-coördinator taak met behulp van Azure PowerShell. toolearn Zie meer Hallo artikelen te volgen:

* [Aan de slag met HDInsight][hdinsight-get-started]
* [Azure Blob storage gebruiken met HDInsight][hdinsight-storage]
* [HDInsight met behulp van Azure PowerShell beheren][hdinsight-admin-powershell]
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-java-mapreduce]

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
