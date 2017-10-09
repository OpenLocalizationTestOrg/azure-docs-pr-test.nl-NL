---
title: aaaAnalyze vluchtgegevens vertraging met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over hoe de Sqoop taak voor het uitvoeren van toouse een Windows PowerShell-script toocreate een HDInsight-cluster een Hive-taak uitvoert en Hallo cluster verwijderen.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 00e26aa9-82fb-4dbe-b87d-ffe8e39a5412
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 6ebaee65d9b270e5dc2141dd1265011d372f497d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-in-hdinsight"></a>Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight
Hive biedt een methode voor Hadoop MapReduce-taken uitgevoerd via een SQL-achtige scripttaal genaamd  *[HiveQL][hadoop-hiveql]*, die naar samenvatten, opvragen en analyseren van grote hoeveelheden gegevens kunnen worden toegepast.

> [!IMPORTANT]
> Hallo moet stappen in dit document een HDInsight op basis van Windows-cluster. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor stappen die met een cluster op basis van Linux werken [vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md).

Een van de belangrijkste voordelen van Azure HDInsight Hallo is Hallo scheiding van opslag van gegevens en rekencapaciteit. HDInsight gebruikt Azure Blob-opslag voor gegevensopslag. Een typische taak bestaat uit drie delen:

1. **Gegevens opslaan in Azure Blob-opslag.**  Bijvoorbeeld, weerbericht gegevens, sensorgegevens, weblogboeken en in dit geval vertraging vluchtgegevens worden opgeslagen in Azure Blob-opslag.
2. **Taken worden uitgevoerd.** Wanneer gegevens Hallo tooprocess is, voert u een Windows PowerShell-script (of een clienttoepassing) toocreate een HDInsight-cluster, taken uitvoeren en Hallo cluster verwijderen. Hallo taken opslaan uitvoer gegevens tooAzure Blob-opslag. Hallo uitvoergegevens wordt bewaard, zelfs nadat het Hallo-cluster is verwijderd. Op deze manier u betaalt alleen wat u hebt gebruikt.
3. **Hallo uitvoer ophalen uit Azure Blob storage**, of in deze zelfstudie Hallo gegevens tooan Azure SQL database te exporteren.

Hallo volgende diagram illustreert Hallo scenario en de structuur van deze zelfstudie Hallo:

![HDI. FlightDelays.flow][img-hdi-flightdelays-flow]

Houd er rekening mee dat Hallo getallen in Hallo diagram toohello Sectietitels overeenkomen. **M** staat voor Hallo hoofdproces. **Een** staat voor de inhoud in de bijlage Hallo Hallo.

Hallo belangrijkste deel van Hallo zelfstudie ziet u hoe toouse een Windows PowerShell-script tooperform Hallo volgende taken:

* Maak een HDInsight-cluster.
* Een Hive-taak uitvoeren op Hallo cluster toocalculate gemiddelde vertragingen op luchthavens. Hallo vertraging vluchtgegevens wordt opgeslagen in een Azure Blob storage-account.
* Voer een Sqoop taak tooexport Hallo Hive-taak uitvoer tooan Azure SQL-database.
* Hallo HDInsight-cluster verwijderen.

In de bijlagen hello, kunt u Hallo-instructies vinden voor de vertraging vluchtgegevens uploaden, maken/uploaden van een queryreeks Hive en hello Azure SQL database voorbereiden voor Hallo Sqoop taak.

> [!NOTE]
> Hallo stappen in dit document zijn specifieke tooWindows gebaseerde HDInsight-clusters. Zie voor stappen die met een cluster op basis van Linux werken [gegevens te analyseren vlucht vertraging met Hive in HDInsight (Linux)](hdinsight-analyze-flight-delay-data-linux.md)

### <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Een werkstation met Azure PowerShell**.

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.

**Bestanden die in deze zelfstudie worden gebruikt**

Deze zelfstudie wordt gebruikgemaakt van Hallo tijdige prestaties van luchtvaartmaatschappij vluchtgegevens van [onderzoek en innovatieve technologie-beheer, Bureau vervoer statistieken of RITA][rita-website].
Een kopie van Hallo gegevens zijn geüpload tooan Azure Blob storage-container met Hallo openbare Blob-machtiging.
Een gedeelte van het PowerShell-script kopieert Hallo gegevens van Hallo openbare blob-container toohello standaard blob-container van het cluster. Hallo HiveQL-script ook wordt gekopieerd toohello dezelfde Blob-container.
Als u wilt dat toolearn hoe tooget of uploadt Hallo gegevens tooyour eigenaar Storage-account en hoe toocreate of uploadt Hallo HiveQL script bestand, Zie [bijlage A](#appendix-a) en [bijlage B](#appendix-b).

Hallo bevat volgende tabel Hallo-bestanden in deze zelfstudie gebruikt:

<table border="1">
<tr><th>Bestanden</th><th>Beschrijving</th></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/flightdelays.hql</td><td>Hallo HiveQL-scriptbestand gebruikt door Hallo Hive-taak. Dit script is geüploade tooan Azure Blob storage-account met Hallo openbare toegang. <a href="#appendix-b">Bijlage B</a> instructies over het voorbereiden en het uploaden van dit bestand tooyour eigen Azure Blob storage-account heeft.</td></tr>
<tr><td>wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data</td><td>De invoergegevens voor Hallo Hive-taak. Hallo-gegevens zijn geüpload tooan Azure Blob storage-account met Hallo openbare toegang. <a href="#appendix-a">Bijlage A</a> bevat de instructies op Hallo-gegevens ophalen en uploadt Hallo gegevens tooyour eigen Azure Blob storage-account.</td></tr>
<tr><td>\tutorials\flightdelays\output</td><td>uitvoerpad Hallo voor Hallo Hive-taak. Hallo standaardcontainer wordt gebruikt voor het opslaan van Hallo uitvoergegevens.</td></tr>
<tr><td>\tutorials\flightdelays\jobstatus</td><td>Hallo Hive-taak status map op de standaardcontainer Hallo.</td></tr>
</table>

## <a name="create-cluster-and-run-hivesqoop-jobs"></a>Cluster maken en Hive/Sqoop taken uitvoeren
Hadoop-MapReduce is batchverwerking. Hallo meeste rendabele manier toorun een Hive-taak is toocreate een cluster voor Hallo taak en Hallo taak verwijderen nadat het Hallo-taak is voltooid. Hallo volgende script bevat informatie over het hele proces Hallo.
Zie voor meer informatie over het maken van een HDInsight-cluster en het uitvoeren van Hive-taken [maken Hadoop-clusters in HDInsight] [ hdinsight-provision] en [Hive gebruiken met HDInsight][hdinsight-use-hive].

**toorun hello Hive-query's met Azure PowerShell**

1. Een Azure SQL database en Hallo tabel voor Hallo Sqoop taakuitvoer maken met behulp van instructies Hallo in [bijlage C](#appendix-c).
2. Open Windows PowerShell ISE en Hallo na script uitvoeren:

    ```powershell
    $subscriptionID = "<Azure Subscription ID>"
    $nameToken = "<Enter an Alias>"

    ###########################################
    # You must configure hello follwing variables
    # for an existing Azure SQL Database
    ###########################################
    $existingSqlDatabaseServerName = "<Azure SQL Database Server>"
    $existingSqlDatabaseLogin = "<Azure SQL Database Server Login>"
    $existingSqlDatabasePassword = "<Azure SQL Database Server login password>"
    $existingSqlDatabaseName = "<Azure SQL Database name>"

    $localFolder = "E:\Tutorials\Downloads\" # A temp location for copying files.
    $azcopyPath = "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy" # depends on hello version, hello folder can be different

    ###########################################
    # (Optional) configure hello following variables
    ###########################################

    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2"

    $HDInsightClusterName = $namePrefix + "hdi"
    $httpUserName = "admin"
    $httpPassword = "<Enter hello Password>"

    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $HDInsightClusterName # use hello cluster name

    $existingSqlDatabaseTableName = "AvgDelays"
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$existingSqlDatabaseServerName.database.windows.net;user=$existingSqlDatabaseLogin@$existingSqlDatabaseServerName;password=$existingSqlDatabaseLogin;database=$existingSqlDatabaseName"

    $hqlScriptFile = "/tutorials/flightdelays/flightdelays.hql"

    $jobStatusFolder = "/tutorials/flightdelays/jobstatus"

    ###########################################
    # Login
    ###########################################
    try{
        $acct = Get-AzureRmSubscription
    }
    catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionID $subscriptionID

    ###########################################
    # Create a new HDInsight cluster
    ###########################################

    # Create ARM group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create hello default storage account
    New-AzureRmStorageAccount -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName -Location $location -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    New-AzureStorageContainer -Name $defaultBlobContainerName -Context $defaultStorageAccountContext

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
        -DefaultStorageContainer $existingDefaultBlobContainerName

    ###########################################
    # Prepare hello HiveQL script and source data
    ###########################################

    # Create hello temp location
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download hello sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous
    $blobs = Get-AzureStorageBlob -Container "flightdelay" -Context $context
    #$blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload data toodefault container

    $azcopycmd = "cmd.exe /C '$azcopyPath\azcopy.exe' /S /Source:'$localFolder' /Dest:'https://$defaultStorageAccountName.blob.core.windows.net/$defaultBlobContainerName/tutorials/flightdelays' /DestKey:$defaultStorageAccountKey"

    Invoke-Expression -Command:$azcopycmd

    ###########################################
    # Submit hello Hive job
    ###########################################
    Use-AzureRmHDInsightCluster -ClusterName $HDInsightClusterName -HttpCredential $httpCredential
    $response = Invoke-AzureRmHDInsightHiveJob `
                    -Files $hqlScriptFile `
                    -DefaultContainer $defaultBlobContainerName `
                    -DefaultStorageAccountName $defaultStorageAccountName `
                    -DefaultStorageAccountKey $defaultStorageAccountKey `
                    -StatusFolder $jobStatusFolder

    write-Host $response

    ###########################################
    # Submit hello Sqoop job
    ###########################################
    $exportDir = "wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net/tutorials/flightdelays/output"

    $sqoopDef = New-AzureRmHDInsightSqoopJobDefinition `
                    -Command "export --connect $sqlDatabaseConnectionString --table $sqlDatabaseTableName --export-dir $exportDir --fields-terminated-by \001 "
    $sqoopJob = Start-AzureRmHDInsightJob `
                    -ResourceGroupName $resourceGroupName `
                    -ClusterName $hdinsightClusterName `
                    -HttpCredential $httpCredential `
                    -JobDefinition $sqoopDef #-Debug -Verbose

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -HttpCredential $httpCredential `
        -WaitTimeoutInSeconds 3600 `
        -Job $sqoopJob.JobId

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $hdinsightClusterName `
        -HttpCredential $httpCredential `
        -DefaultContainer $existingDefaultBlobContainerName `
        -DefaultStorageAccountName $defaultStorageAccountName `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -JobId $sqoopJob.JobId `
        -DisplayOutputType StandardError

    ###########################################
    # Delete hello cluster
    ###########################################
    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $hdinsightClusterName
    ```
3. Verbinding maken met tooyour SQL database en gemiddelde vertragingen per plaats in Hallo AvgDelays tabel zien:

    ![HDI. FlightDelays.AvgDelays.Dataset][image-hdi-flightdelays-avgdelays-dataset]

- - -

## <a id="appendix-a"></a>Bijlage A - uploaden vlucht vertraging gegevens tooAzure Blob-opslag
Hallo-gegevensbestand en Hallo HiveQL-scriptbestanden uploaden (Zie [bijlage B](#appendix-b)) vereist een planning. Hallo idee is toostore Hallo-gegevensbestanden en Hallo HiveQL bestand voordat u een HDInsight-cluster en Hallo Hive-taak uitgevoerd. U hebt hiervoor twee opties:

* **Gebruik dezelfde hello Azure Storage-account dat wordt gebruikt door Hallo HDInsight-cluster als het standaardbestandssysteem Hallo.** Omdat de HDInsight-cluster Hallo Hallo toegangssleutel voor Opslagaccount, hoeft u geen toomake wijzigingen aanbrengt.
* **Gebruik een ander Azure Storage-account van Hallo standaardbestandssysteem voor HDInsight-cluster.** Als dit Hallo geval is, moet u Hallo maken deel uit van Hallo Windows PowerShell-script gevonden in wijzigen [maken HDInsight-cluster en voer Hive/Sqoop taken](#runjob) toolink Hallo Storage-account als een aanvullende Storage-account. Zie voor instructies [maken Hadoop-clusters in HDInsight][hdinsight-provision]. Hallo HDInsight-cluster, vervolgens Hallo-toegangssleutel voor opslagaccount Hallo kent.

> [!NOTE]
> Hallo Blob opslagpad voor Hallo gegevensbestand hard gecodeerd in Hallo HiveQL-scriptbestand is. U moet deze dienovereenkomstig bijwerken.

**toodownload hello vluchtgegevens**

1. Te bladeren[onderzoek en beheer-innovatieve technologie, Bureau vervoer statistieken][rita-website].
2. Selecteer op Hallo pagina Hallo volgende waarden:

    <table border="1">
    <tr><th>Naam</th><th>Waarde</th></tr>
    <tr><td>Filteren van jaar</td><td>2013 </td></tr>
    <tr><td>Periode filteren</td><td>Januari</td></tr>
    <tr><td>Velden</td><td>*Jaar*, *FlightDate*, *UniqueCarrier*, *Carrier*, *FlightNum*, *OriginAirportID*, *oorsprong*, *OriginCityName*, *OriginState*, *DestAirportID*, *Dest*, *DestCityName*, *DestState*, *DepDelayMinutes*, *ArrDelay*, *ArrDelayMinutes*, *CarrierDelay*, *WeatherDelay*,  *NASDelay*, *SecurityDelay*, *LateAircraftDelay* (alle andere velden wissen)</td></tr>
    </table>
3.Klik op **downloaden**.
4. Pak Hallo bestand toohello **C:\Tutorials\FlightDelay\2013Data** map. Elk bestand is van een CSV-bestand en ongeveer 60GB groot is.
5. De naam Hallo bestand toohello van Hallo maand die deze gegevens voor bevat. Bijvoorbeeld, Hallo gegevensbestand Hallo januari naam *January.csv*.
6. Herhaal stappen 2 en 5 toodownload een bestand voor elke Hallo 12 maanden in 2013. U moet minimaal één bestand toorun Hallo zelfstudie.

**tooupload hello vlucht vertraging gegevens tooAzure Blob-opslag**

1. Bereid Hallo parameters:

    <table border="1">
    <tr><th>Naam variabele</th><th>Opmerkingen</th></tr>
    <tr><td>$storageAccountName</td><td>Hallo waar u tooupload Hallo gegevens naar Azure Storage-account.</td></tr>
    <tr><td>$blobContainerName</td><td>Hallo waar u tooupload Hallo gegevens naar Blob-container.</td></tr>
    </table>
2. Open Azure PowerShell ISE.
3. Plak de volgende script in het scriptvenster Hallo Hallo:

    ```powershell
    [CmdletBinding()]
    Param(

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #Region - Variables
    $localFolder = "C:\Tutorials\FlightDelay\2013Data"  # hello source folder
    $destFolder = "tutorials/flightdelay/2013data"     #hello blob name prefix for hello files toobe uploaded
    #EndRegion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #Region - Copy hello file from local workstation tooAzure Blob storage
    if (test-path -Path $localFolder)
    {
        foreach ($item in Get-ChildItem -Path $localFolder){
            $fileName = "$localFolder\$item"
            $blobName = "$destFolder/$item"

            Write-Host "Copying $fileName too$blobName" -ForegroundColor Green

            Set-AzureStorageBlobContent -File $fileName -Container $blobContainerName -Blob $blobName -Context $storageContext
        }
    }
    else
    {
        Write-Host "hello source folder on hello workstation doesn't exist" -ForegroundColor Red
    }

    # List hello uploaded files on HDInsight
    Get-AzureStorageBlob -Container $blobContainerName  -Context $storageContext -Prefix $destFolder
    #EndRegion
    ```
4. Druk op **F5** toorun Hallo script.

Als u een andere methode kiest voor het uploaden van bestanden Hallo toouse, zorg Hallo bestandspad wordt flightdelay-zelfstudies-gegevens. Hallo-syntaxis voor toegang tot bestanden Hallo is:

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/tutorials/flightdelay/data

Hallo pad zelfstudies/flightdelay/gegevens is Hallo virtuele map die u hebt gemaakt toen u Hallo bestanden geüpload. Controleer of er 12 bestanden, één voor elke maand.

> [!NOTE]
> Hallo Hive query tooread vanaf de nieuwe locatie hello, moet u bijwerken.
>
> Hallo container toegang machtiging toobe openbare configureren of binden Hallo Storage account toohello HDInsight-cluster. Hallo Hive-queryreeks worden anders niet kunnen tooaccess Hallo gegevensbestanden worden opgeslagen.

- - -

## <a id="appendix-b"></a>Bijlage B - maken en uploaden van een HiveQL-script
Met Azure PowerShell, kunt u meerdere HiveQL-instructies één uitvoeren op een tijd of pakket Hallo instructie van HiveQL in een scriptbestand. Deze sectie leest u hoe toocreate HiveQL-script en uploaden Hallo tooAzure Blob-opslag script met behulp van Azure PowerShell. Hive vereist Hallo HiveQL scripts toobe opgeslagen in Azure Blob storage.

Hallo HiveQL-script voert Hallo volgende uit:

1. **Hallo delays_raw tabel**, geval Hallo tabel al bestaat.
2. **Hallo delays_raw externe Hive-tabel maken** toohello Blob-opslaglocatie met Hallo vlucht vertraging bestanden aan te wijzen. Deze query geeft aan dat de velden worden gescheiden door ',' en dat de regels worden beëindigd door '\n'. Dit is een probleem wanneer veldwaarden komma's bevatten omdat Hive kan geen onderscheid maken tussen een door komma's die een veldscheidingsteken en een die deel uitmaakt van een veldwaarde (die Hallo geval veldwaarden voor de oorsprong is\_STAD\_naam en doel\_ Plaats\_naam). tooaddress deze, Hallo query maakt TEMP kolommen toohold gegevens die onjuist is onderverdeeld in kolommen.
3. **Hallo vertragingen tabel**, geval Hallo tabel al bestaat.
4. **Hallo vertragingen tabel maken**. Is het handig tooclean up Hallo-gegevens voor verdere verwerking. Deze query maakt een nieuwe tabel *vertragingen*, uit Hallo delays_raw tabel. Opmerking Hallo TEMP kolommen (zoals eerder vermeld) worden niet gekopieerd en die Hallo **subtekenreeks** functie gebruikte tooremove aanhalingstekens Hallo gegevens is.
5. **Hallo gemiddelde weer vertraging en groepen Hallo resultaten plaatsnaam berekenen.** Dit wordt ook Hallo resultaten tooBlob opslag uitvoeren. Houd er rekening mee die query Hallo Hallo gegevens verwijderen van enkele aanhalingstekens en uitsluit rijen waar Hallo waarde voor **weather_delay** is null. Dit is nodig omdat Sqoop, die verderop in deze zelfstudie wordt gebruikt, kunnen niet worden verwerkt die waarden probleemloos standaard.

Zie voor een volledige lijst van Hallo HiveQL opdrachten [Hive Data Definition Language][hadoop-hiveql]. Elke opdracht HiveQL moet eindigen met een puntkomma.

**een scriptbestand HiveQL toocreate**

1. Bereid Hallo parameters:

    <table border="1">
    <tr><th>Naam variabele</th><th>Opmerkingen</th></tr>
    <tr><td>$storageAccountName</td><td>Hello Azure Storage-account waar u tooupload hello HiveQL-script op.</td></tr>
    <tr><td>$blobContainerName</td><td>Hallo Blob-container waar u tooupload hello HiveQL-script op.</td></tr>
    </table>
2. Open Azure PowerShell ISE.
3. Kopieer en plak de volgende script in het scriptvenster Hallo Hallo:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Blob storage variables
        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure storage account name for creating a new HDInsight cluster. If hello account doesn't exist, hello script will create one.")]
        [String]$storageAccountName,

        [Parameter(Mandatory=$True,
                    HelpMessage="Enter hello Azure blob container name for creating a new HDInsight cluster. If not specified, hello HDInsight cluster name will be used.")]
        [String]$blobContainerName
    )

    #region - Define variables
    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    # hello HiveQL script file is exported as this file before it's uploaded tooBlob storage
    $hqlLocalFileName = "e:\tutorials\flightdelay\flightdelays.hql"

    # hello HiveQL script file will be uploaded tooBlob storage as this blob name
    $hqlBlobName = "tutorials/flightdelay/flightdelays.hql"

    # These two constants are used by hello HiveQL script file
    #$srcDataFolder = "tutorials/flightdelay/data"
    $dstDataFolder = "/tutorials/flightdelay/output"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #Region - Validate user input
    Write-Host "`nValidating hello Azure Storage account and hello Blob container..." -ForegroundColor Green
    # Validate hello Storage account
    if (-not (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}))
    {
        Write-Host "hello storage account, $storageAccountName, doesn't exist." -ForegroundColor Red
        exit
    }
    else{
        $resourceGroupName = (Get-AzureRmStorageAccount|Where-Object{$_.StorageAccountName -eq $storageAccountName}).ResourceGroupName
    }

    # Validate hello container
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    if (-not (Get-AzureStorageContainer -Context $storageContext |Where-Object{$_.Name -eq $blobContainerName}))
    {
        Write-Host "hello Blob container, $blobContainerName, doesn't exist" -ForegroundColor Red
        Exit
    }
    #EngRegion

    #region - Validate hello file and file path

    # Check if a file with hello same file name already exists on hello workstation
    Write-Host "`nvalidating hello folder structure on hello workstation for saving hello HQL script file ..."  -ForegroundColor Green
    if (test-path $hqlLocalFileName){

        $isDelete = Read-Host 'hello file, ' $hqlLocalFileName ', exists.  Do you want toooverwirte it? (Y/N)'

        if ($isDelete.ToLower() -ne "y")
        {
            Exit
        }
    }

    # Create hello folder if it doesn't exist
    $folder = split-path $hqlLocalFileName
    if (-not (test-path $folder))
    {
        Write-Host "`nCreating folder, $folder ..." -ForegroundColor Green

        new-item $folder -ItemType directory
    }
    #end region

    #region - Write hello Hive script into a local file
    Write-Host "`nWriting hello Hive script into a file on your workstation ..." `
                -ForegroundColor Green

    $hqlDropDelaysRaw = "DROP TABLE delays_raw;"

    $hqlCreateDelaysRaw = "CREATE EXTERNAL TABLE delays_raw (" +
            "YEAR string, " +
            "FL_DATE string, " +
            "UNIQUE_CARRIER string, " +
            "CARRIER string, " +
            "FL_NUM string, " +
            "ORIGIN_AIRPORT_ID string, " +
            "ORIGIN string, " +
            "ORIGIN_CITY_NAME string, " +
            "ORIGIN_CITY_NAME_TEMP string, " +
            "ORIGIN_STATE_ABR string, " +
            "DEST_AIRPORT_ID string, " +
            "DEST string, " +
            "DEST_CITY_NAME string, " +
            "DEST_CITY_NAME_TEMP string, " +
            "DEST_STATE_ABR string, " +
            "DEP_DELAY_NEW float, " +
            "ARR_DELAY_NEW float, " +
            "CARRIER_DELAY float, " +
            "WEATHER_DELAY float, " +
            "NAS_DELAY float, " +
            "SECURITY_DELAY float, " +
            "LATE_AIRCRAFT_DELAY float) " +
        "ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' " +
        "LINES TERMINATED BY '\n' " +
        "STORED AS TEXTFILE " +
        "LOCATION 'wasb://flightdelay@hditutorialdata.blob.core.windows.net/2013Data';"

    $hqlDropDelays = "DROP TABLE delays;"

    $hqlCreateDelays = "CREATE TABLE delays AS " +
        "SELECT YEAR AS year, " +
            "FL_DATE AS flight_date, " +
            "substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier, " +
            "substring(CARRIER, 2, length(CARRIER) -1) AS carrier, " +
            "substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num, " +
            "ORIGIN_AIRPORT_ID AS origin_airport_id, " +
            "substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code, " +
            "substring(ORIGIN_CITY_NAME, 2) AS origin_city_name, " +
            "substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr, " +
            "DEST_AIRPORT_ID AS dest_airport_id, " +
            "substring(DEST, 2, length(DEST) -1) AS dest_airport_code, " +
            "substring(DEST_CITY_NAME,2) AS dest_city_name, " +
            "substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr, " +
            "DEP_DELAY_NEW AS dep_delay_new, " +
            "ARR_DELAY_NEW AS arr_delay_new, " +
            "CARRIER_DELAY AS carrier_delay, " +
            "WEATHER_DELAY AS weather_delay, " +
            "NAS_DELAY AS nas_delay, " +
            "SECURITY_DELAY AS security_delay, " +
            "LATE_AIRCRAFT_DELAY AS late_aircraft_delay " +
        "FROM delays_raw;"

    $hqlInsertLocal = "INSERT OVERWRITE DIRECTORY '$dstDataFolder' " +
        "SELECT regexp_replace(origin_city_name, '''', ''), " +
            "avg(weather_delay) " +
        "FROM delays " +
        "WHERE weather_delay IS NOT NULL " +
        "GROUP BY origin_city_name;"

    $hqlScript = $hqlDropDelaysRaw + $hqlCreateDelaysRaw + $hqlDropDelays + $hqlCreateDelays + $hqlInsertLocal

    $hqlScript | Out-File $hqlLocalFileName -Encoding ascii -Force
    #endregion

    #region - Upload hello Hive script toohello default Blob container
    Write-Host "`nUploading hello Hive script toohello default Blob container ..." -ForegroundColor Green

    # Create a storage context object
    $storageAccountKey = (Get-AzureRmStorageAccountKey -StorageAccountName $storageAccountName -ResourceGroupName $resourceGroupName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Upload hello file from local workstation tooBlob storage
    Set-AzureStorageBlobContent -File $hqlLocalFileName -Container $blobContainerName -Blob $hqlBlobName -Context $destContext
    #endregion

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

    Hier volgen Hallo variabelen in Hallo script gebruikt:

   * **$hqlLocalFileName** -Hallo script bestand wordt opgeslagen Hallo HiveQL-script lokaal voordat u dit uploadt tooBlob opslag. Dit is de bestandsnaam Hallo. de standaardwaarde Hallo is <u>C:\tutorials\flightdelay\flightdelays.hql</u>.
   * **$hqlBlobName** -dit is Hallo HiveQL-script blob bestandsnaam in hello Azure Blob-opslag gebruikt. de standaardwaarde Hallo is tutorials/flightdelay/flightdelays.hql. Omdat het Hallo-bestand zal tooAzure Blob-opslag rechtstreeks worden geschreven, is er niet een "/" aan Hallo begin van Hallo blob-naam. Als u tooaccess Hallo-bestand van Blob-opslag wilt, moet u tooadd een "/" aan begin Hallo Hallo-bestandsnaam.
   * **$srcDataFolder** en **$dstDataFolder** -= 'flightdelay-zelfstudies/gegevens' = 'flightdelay-zelfstudies/uitvoer'

- - -
## <a id="appendix-c"></a>Bijlage C - een Azure SQL database voorbereiden voor Hallo Sqoop taakuitvoer
**tooprepare hello SQL-database (samenvoegen dit Hello Sqoop script)**

1. Bereid Hallo parameters:

    <table border="1">
    <tr><th>Naam variabele</th><th>Opmerkingen</th></tr>
    <tr><td>$sqlDatabaseServerName</td><td>Hallo-naam van hello Azure SQL database-server. Voer niets toocreate een nieuwe server.</td></tr>
    <tr><td>$sqlDatabaseUsername</td><td>Hallo aanmeldingsnaam voor hello Azure SQL database-server. Als $sqlDatabaseServerName een bestaande server is, zijn Hallo aanmeldingsnaam en wachtwoord bij de aanmelding gebruikte tooauthenticate met Hallo-server. Ze zijn anders gebruikte toocreate een nieuwe server.</td></tr>
    <tr><td>$sqlDatabasePassword</td><td>Hallo aanmeldingswachtwoord voor hello Azure SQL database-server.</td></tr>
    <tr><td>$sqlDatabaseLocation</td><td>Deze waarde wordt alleen gebruikt als u een nieuwe Azure-database-server maakt.</td></tr>
    <tr><td>$sqlDatabaseName</td><td>Hallo SQL-database gebruikt toocreate hello AvgDelays tabel voor Hallo Sqoop taak. Leeg laat, wordt een database met de naam HDISqoop maken. Hallo tabelnaam voor Hallo Sqoop taakuitvoer is AvgDelays. </td></tr>
    </table>
2. Open Azure PowerShell ISE.
3. Kopieer en plak de volgende script in het scriptvenster Hallo Hallo:

    ```powershell
    [CmdletBinding()]
    Param(

        # Azure Resource group variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure resource group name. It will be created if it doesn't exist.")]
        [String]$resourceGroupName,

        # SQL database server variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database Server Name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseServer,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user.")]
        [String]$sqlDatabaseLogin,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello Azure SQL Database admin user password.")]
        [String]$sqlDatabasePassword,

        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello region toocreate hello Database in.")]
        [String]$sqlDatabaseLocation,   #For example, West US.

        # SQL database variables
        [Parameter(Mandatory=$True,
                HelpMessage="Enter hello database name. It will be created if it doesn't exist.")]
        [String]$sqlDatabaseName # specify hello database name if you have one created. Otherwise use "" toohave hello script create one for you.
    )

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Constants and variables

    # IP address REST service used for retrieving external IP address and creating firewall rules
    [String]$ipAddressRestService = "http://bot.whatismyipaddress.com"
    [String]$fireWallRuleName = "FlightDelay"

    # SQL database variables
    [String]$sqlDatabaseMaxSizeGB = 10

    #SQL query string for creating AvgDelays table
    [String]$sqlDatabaseTableName = "AvgDelays"
    [String]$sqlCreateAvgDelaysTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
                [origin_city_name] [nvarchar](50) NOT NULL,
                [weather_delay] float,
            CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
            (
                [origin_city_name] ASC
            )
            )"
    #endregion

    #Region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{Login-AzureRmAccount}
    #EndRegion

    #region - Create and validate Azure resouce group
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $sqlDatabaseLocation
    }

    #EndRegion

    #region - Create and validate Azure SQL database server
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServer -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $credential = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServer = (New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -SqlAdministratorCredentials $credential -Location $sqlDatabaseLocation).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServer." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-workstation" -StartIpAddress $workstationIPAddress -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -FirewallRuleName "$fireWallRuleName-Azureservices" -StartIpAddress "0.0.0.0" -EndIpAddress "0.0.0.0"
    }

    #endregion

    #region - Create and validate Azure SQL database

    try {
        Get-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName
    }
    catch {
        Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green
        New-AzureRMSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $sqlDatabaseServer -DatabaseName $sqlDatabaseName -Edition "Standard" -RequestedServiceObjectiveName "S1"
    }

    #endregion

    #region -  Execute an SQL command toocreate hello AvgDelays table

    Write-Host "`nCreating SQL Database table ..."  -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServer.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = $sqlCreateAvgDelaysTable
    $cmd.executenonquery()

    $conn.close()

    Write-host "`nEnd of hello PowerShell script" -ForegroundColor Green
    ```

   > [!NOTE]
   > Hallo-script gebruikt een representational state transfer (REST)-service, http://bot.whatismyipaddress.com, tooretrieve uw externe IP-adres. Hallo IP-adres wordt gebruikt voor het maken van een firewallregel voor uw SQL database-server.

    Hier volgen een aantal variabelen in Hallo script gebruikt:

   * **$ipAddressRestService** -Hallo standaardwaarde is http://bot.whatismyipaddress.com. Het is een openbaar IP-adres REST-service voor het ophalen van het externe IP-adres. U kunt andere services als u wilt gebruiken. Hallo externe IP-adres opgehaald via Hallo-service worden gebruikte toocreate een firewallregel voor uw Azure SQL database-server, zodat u toegang hebt tot Hallo database vanuit uw werkstation (met behulp van Windows PowerShell-script).
   * **$fireWallRuleName** -dit is de naam Hallo Hallo firewallregel voor hello Azure SQL database-server. Hallo standaardnaam is <u>FlightDelay</u>. U kunt deze desgewenst wijzigen.
   * **$sqlDatabaseMaxSizeGB** -deze waarde wordt alleen gebruikt wanneer u een nieuwe Azure SQL database-server maakt. Hallo-standaardwaarde is 10GB. 10GB is voldoende voor deze zelfstudie.
   * **$sqlDatabaseName** -deze waarde wordt alleen gebruikt wanneer u een nieuwe Azure SQL database maakt. de standaardwaarde Hallo is HDISqoop. Als u de naam wijzigt, moet u Hallo Sqoop Windows PowerShell-script dienovereenkomstig bijwerken.
4. Druk op **F5** toorun Hallo script.
5. Hallo-scriptuitvoer valideren. Zorg ervoor dat het Hallo-script is uitgevoerd.

## <a id="nextsteps"></a> Volgende stappen
Nu u begrijpt hoe tooupload een bestand tooAzure Blob-opslag, hoe toopopulate een Hive-tabel met behulp van Hallo gegevens uit Azure Blob storage, hoe toorun Hive-query's en hoe toouse Sqoop tooexport gegevens uit HDFS tooan Azure SQL database. toolearn Zie meer Hallo artikelen te volgen:

* [Aan de slag met HDInsight][hdinsight-get-started]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Oozie gebruiken met HDInsight][hdinsight-use-oozie]
* [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL
[hadoop-shell-commands]: http://hadoop.apache.org/docs/r0.18.3/hdfs_shell.html

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx

[image-hdi-flightdelays-avgdelays-dataset]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.AvgDelays.DataSet.png
[img-hdi-flightdelays-run-hive-job-output]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.RunHiveJob.Output.png
[img-hdi-flightdelays-flow]: ./media/hdinsight-analyze-flight-delay-data/HDI.FlightDelays.Flow.png
