---
title: aaaAnalyze Twitter-gegevens met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hive tooanalyze Twitter-gegevens op Hadoop in HDInsight toofind Hallo frequentie van de informatie over het gebruik van een bepaald woord.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 78e4ea33-9714-424d-ac07-3d60ecaebf2e
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 40c0a1afbc1fff10c070d22a99cd9d32d42f230a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a>Twitter-gegevens met Hive in HDInsight analyseren
Sociale websites zijn een belangrijke drijvende dwingt Hallo voor big data. Openbare API's die worden geleverd door sites zoals Twitter zijn nuttig gegevensbron voor het analyseren en kennis van populaire trends.
In deze zelfstudie wordt u tweets verkrijgen door middel van een streaming-API Twitter en vervolgens met Apache Hive op Azure HDInsight tooget een lijst met Twitter-gebruikers die Hallo meeste tweets die deel uitmaakt van een bepaald woord verzonden.

> [!IMPORTANT]
> Hallo moet stappen in dit document een HDInsight op basis van Windows-cluster. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie. Zie voor stappen specifieke tooa op basis van Linux-cluster, [analyseren Twitter-gegevens met Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een werkstation** met Azure PowerShell installeren en configureren.

    tooexecute Windows PowerShell-scripts, die u moet Azure PowerShell als administrator uitvoeren en stel een uitvoeringsbeleid voor hello te*RemoteSigned*. Zie [Run Windows PowerShell-scripts][powershell-script].

    Voordat u Windows PowerShell-scripts uitvoert, zorg ervoor dat u verbonden tooyour Azure-abonnement met behulp van de volgende cmdlet Hallo:

    ```powershell
    Login-AzureRmAccount
    ```

    Als u meerdere Azure-abonnementen hebt, gebruikt u Hallo cmdlet tooset Hallo huidige abonnement te volgen:

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.

* **Een Azure HDInsight-cluster**. Zie voor instructies over het inrichten van het cluster [aan de slag met HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision]. Hallo clusternaam moet u later in de zelfstudie Hallo.

Hallo bevat volgende tabel Hallo-bestanden in deze zelfstudie gebruikt:

| Bestanden | Beschrijving |
| --- | --- |
| /tutorials/Twitter/Data/tweets.txt |Hallo brongegevens voor Hallo Hive-taak. |
| /tutorials/Twitter/output |Hallo uitvoermap voor Hallo Hive-taak. Hallo Hive-taak uitvoer standaardbestandsnaam is **000000_0**. |
| tutorials/Twitter/Twitter.hql |Hallo HiveQL-scriptbestand. |
| /tutorials/Twitter/JobStatus |Hallo taakstatus Hadoop. |

## <a name="get-twitter-feed"></a>Get Twitter-feeds
In deze zelfstudie gebruikt u Hallo [Twitter streaming-API's][twitter-streaming-api]. Hallo specifieke Twitter streaming-API die u wilt gebruiken is [statussen-/ filter][twitter-statuses-filter].

> [!NOTE]
> Een bestand met 10.000 tweets en Hive-scriptbestand hello (behandeld in de volgende sectie Hallo) zijn geüpload in een openbare Blob-container. Als u toouse Hallo geüpload bestanden wilt, kunt u deze sectie overslaan.

[Tweets gegevens](https://dev.twitter.com/docs/platform-objects/tweets) wordt opgeslagen in Hallo JSON JavaScript Object Notation ()-indeling die een complexe geneste structuur bevat. In plaats van een groot aantal regels code schrijven met behulp van een conventionele programmeertaal, kunt u deze geneste structuur in een Hive-tabel transformeren zodat deze kan worden doorzocht door een Structured Query Language (SQL)-taal genaamd HiveQL, zoals.

Twitter OAuth tooprovide geautoriseerde toegang tooits API gebruikt. OAuth is een authenticatieprotocol waarmee gebruikers tooapprove toepassingen tooact namens hen zonder het delen van hun wachtwoord. Meer informatie kunt vinden op [oauth.net](http://oauth.net/) of in Hallo uitstekende [inleiding handleiding tooOAuth](http://hueniverse.com/oauth/) van Hueniverse.

Hallo eerste stap toouse OAuth is toocreate een nieuwe toepassing op Hallo Developer Twitter-site.

**toocreate Twitter-toepassing**

1. Aanmelden te[https://apps.twitter.com/](https://apps.twitter.com/). Klik op Hallo **nu aanmelden** koppelen als u een Twitter-account niet hebt.
2. Klik op **nieuwe App maken**.
3. Voer **naam**, **beschrijving**, **Website**. U kunt een URL voor Hallo gezamenlijk **Website** veld. Hallo volgende tabel ziet u enkele waarden voorbeeld toouse:

   | Veld | Waarde |
   | --- | --- |
   |  Naam |MyHDInsightApp |
   |  Beschrijving |MyHDInsightApp |
   |  Website |http://www.myhdinsightapp.com |
4. Controleer **Ja, ik ga akkoord**, en klik vervolgens op **uw Twitter-toepassing maken**.
5. Klik op Hallo **machtigingen** tabblad Hallo standaardmachtiging **alleen-lezen**. Dit is voldoende voor deze zelfstudie.
6. Klik op Hallo **sleutels en toegangstokens** tabblad.
7. Klik op **maken van mijn toegangstoken**.
8. Klik op **Test OAuth** in Hallo rechterbovenhoek van Hallo pagina.
9. Noteer **consumentsleutel**, **consumentgeheim**, **toegangstoken**, en **Access token geheim**. Hallo-waarden moet u later in de zelfstudie Hallo.

In deze zelfstudie gebruikt u Windows PowerShell toomake Hallo webserviceaanroep. Zie voor een voorbeeld .NET C# [realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment]. Hallo andere webserviceaanroepen toomake populaire hulpprogramma is [ *Curl*][curl]. CURL kan worden gedownload vanaf [hier][curl-download].

> [!NOTE]
> Als u Hallo curl-opdracht in Windows gebruikt, kunt u dubbele aanhalingstekens in plaats van enkele aanhalingstekens voor Hallo optiewaarden.

**tooget tweets**

1. Open Windows PowerShell Integrated Scripting Environment (ISE) Hallo. (Typ op Hallo Windows 8 startscherm **PowerShell_ISE** en klik vervolgens op **Windows PowerShell ISE**. Zie [Start Windows PowerShell in Windows 8 en Windows][powershell-start].)
2. Hallo script volgen in het scriptvenster Hallo kopiëren:

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter hello HDInsight cluster name

    # Enter hello OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves hello tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets hello tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # hello script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get hello default storage account name and Blob container name using hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define hello Azure storage connection string ..." -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$storageAccountName;AccountKey=$storageAccountKey"
    Write-Host "`tThe connection string is $storageConnectionString." -ForegroundColor Yellow

    Write-Host "Create block blob object ..." -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($containerName)
    $destBlob = $storageContainer.GetBlockBlobReference($destBlobName)
    #end region

    # region - Format OAuth strings
    Write-Host "Format oauth strings ..." -ForegroundColor Green
    $oauth_nonce = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes([System.DateTime]::Now.Ticks.ToString()));
    $ts = [System.DateTime]::UtcNow - [System.DateTime]::ParseExact("01/01/1970", "dd/MM/yyyy", $null)
    $oauth_timestamp = [System.Convert]::ToInt64($ts.TotalSeconds).ToString();

    $signature = "POST&";
    $signature += [System.Uri]::EscapeDataString("https://stream.twitter.com/1.1/statuses/filter.json") + "&";
    $signature += [System.Uri]::EscapeDataString("oauth_consumer_key=" + $oauth_consumer_key + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_nonce=" + $oauth_nonce + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_signature_method=HMAC-SHA1&");
    $signature += [System.Uri]::EscapeDataString("oauth_timestamp=" + $oauth_timestamp + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_token=" + $oauth_token + "&");
    $signature += [System.Uri]::EscapeDataString("oauth_version=1.0&");
    $signature += [System.Uri]::EscapeDataString("track=" + $track);

    $signature_key = [System.Uri]::EscapeDataString($oauth_consumer_secret) + "&" + [System.Uri]::EscapeDataString($oauth_token_secret);

    $hmacsha1 = new-object System.Security.Cryptography.HMACSHA1;
    $hmacsha1.Key = [System.Text.Encoding]::ASCII.GetBytes($signature_key);
    $oauth_signature = [System.Convert]::ToBase64String($hmacsha1.ComputeHash([System.Text.Encoding]::ASCII.GetBytes($signature)));

    $oauth_authorization = 'OAuth ';
    $oauth_authorization += 'oauth_consumer_key="' + [System.Uri]::EscapeDataString($oauth_consumer_key) + '",';
    $oauth_authorization += 'oauth_nonce="' + [System.Uri]::EscapeDataString($oauth_nonce) + '",';
    $oauth_authorization += 'oauth_signature="' + [System.Uri]::EscapeDataString($oauth_signature) + '",';
    $oauth_authorization += 'oauth_signature_method="HMAC-SHA1",'
    $oauth_authorization += 'oauth_timestamp="' + [System.Uri]::EscapeDataString($oauth_timestamp) + '",'
    $oauth_authorization += 'oauth_token="' + [System.Uri]::EscapeDataString($oauth_token) + '",';
    $oauth_authorization += 'oauth_version="1.0"';

    $post_body = [System.Text.Encoding]::ASCII.GetBytes("track=" + $track);
    #endregion

    #region - Read tweets
    Write-Host "Create HTTP web request ..." -ForegroundColor Green
    [System.Net.HttpWebRequest] $request = [System.Net.WebRequest]::Create("https://stream.twitter.com/1.1/statuses/filter.json");
    $request.Method = "POST";
    $request.Headers.Add("Authorization", $oauth_authorization);
    $request.ContentType = "application/x-www-form-urlencoded";
    $body = $request.GetRequestStream();

    $body.write($post_body, 0, $post_body.length);
    $body.flush();
    $body.close();
    $response = $request.GetResponse() ;

    Write-Host "Start stream reading ..." -ForegroundColor Green

    Write-Host "Define a MemoryStream and a StreamWriter for writing ..." -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream

    $sReader = New-Object System.IO.StreamReader($response.GetResponseStream())

    $inrec = $sReader.ReadLine()
    $count = 0
    while (($inrec -ne $null) -and ($count -le $lineMax))
    {
        if ($inrec -ne "")
        {
            Write-Host "`n`t $count tweets received." -ForegroundColor Yellow

            $writeStream.WriteLine($inrec)
            $count ++
        }

        $inrec=$sReader.ReadLine()
    }
    #endregion

    #region - Write tweets tooBlob storage
    Write-Host "Write toohello destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. Hallo eerste vijf tooeight variabelen instellen in Hallo script:

    Variabele|Beschrijving
    ---|---
    $clusterName|Dit is de naam Hallo van Hallo HDInsight-cluster waar u toorun Hallo-toepassing.
    $oauth_consumer_key|Dit is de Twitter-toepassing hello **consumentsleutel** u opgeschreven eerder tijdens het maken van Hallo Twitter-toepassing.
    $oauth_consumer_secret|Dit is de Twitter-toepassing hello **consumentgeheim** u eerder hebt genoteerd.
    $oauth_token|Dit is de Twitter-toepassing hello **toegangstoken** u eerder hebt genoteerd.
    $oauth_token_secret|Dit is de Twitter-toepassing hello **access token geheim** u eerder hebt genoteerd.
    $destBlobName|Dit is Hallo uitvoer-blob-naam. de standaardwaarde Hallo is **tutorials/twitter/data/tweets.txt**. Als u de standaardwaarde Hallo wijzigt, moet u Windows PowerShell-scripts voor tooupdate Hallo dienovereenkomstig.
    $trackString|Hallo-webservice wordt tweets gerelateerde toothese trefwoorden geretourneerd. de standaardwaarde Hallo is **Azure, Cloud, HDInsight**. Als u de standaardwaarde Hallo wijzigt, wordt u Windows PowerShell-scripts Hallo dienovereenkomstig bijgewerkt.
    $lineMax|Hallo-waarde bepaalt hoeveel tweets Hallo-script leest. Het duurt ongeveer drie minuten tooread 100 tweets. U kunt een groter aantal instellen, maar duurt het meer tijd toodownload.

1. Druk op **F5** toorun Hallo script. Als u problemen als tijdelijke oplossing ondervindt alle Hallo regels selecteren en druk vervolgens op **F8**.
2. U ziet 'Voltooi!' aan het einde van de Hallo van Hallo uitvoer. Eventuele foutberichten wordt rood weergegeven.

Als een validatieprocedure, kunt u controleren Hallo uitvoerbestand **/tutorials/twitter/data/tweets.txt**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell. Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].

## <a name="create-hiveql-script"></a>HiveQL-script maken
Met Azure PowerShell, kunt u meerdere HiveQL-instructies één uitvoeren op een tijd of pakket Hallo instructie van HiveQL in een scriptbestand. In deze zelfstudie maakt u een HiveQL-script. Hallo-scriptbestand moet tooAzure geüploade Blob-opslag. In de volgende sectie hello uitvoeren u Hallo-scriptbestand met behulp van Azure PowerShell.

> [!NOTE]
> Hallo Hive-scriptbestand en een bestand met 10.000 tweets zijn geüpload in een openbare Blob-container. Als u toouse Hallo geüpload bestanden wilt, kunt u deze sectie overslaan.

Hallo HiveQL-script voert Hallo volgende uit:

1. **Hallo tweets_raw tabel** geval Hallo tabel al bestaat.
2. **Hallo tweets_raw Hive-tabel maken**. Deze tijdelijke gestructureerde Hive-tabel bevat Hallo-gegevens voor verdere uitpakken, transformeren en laden (ETL) verwerking. Zie voor informatie over partities, [Hive-zelfstudie][apache-hive-tutorial].
3. **Gegevens laden** van bronmap hello, /tutorials/twitter/data. Hallo grote tweets gegevensset in geneste JSON-indeling heeft nu is omgezet in de structuur van een tijdelijke Hive-tabel.
4. **Verwijder Hallo tweets tabel** geval Hallo tabel al bestaat.
5. **Hallo tweets tabel maken**. Voordat u kunt een query op Hallo tweets gegevensset met Hive, moet u toorun een ander ETL-proces. Dit proces ETL definieert een meer gedetailleerde tabelschema voor Hallo-gegevens die u hebt opgeslagen in Hallo 'twitter_raw' tabel.
6. **Overschrijven tabel invoegen**. Dit complexe Hive-script wordt een reeks lang MapReduce-taken starten door Hallo Hadoop-cluster. Dit kan ongeveer 10 minuten duren, afhankelijk van uw gegevensset en het Hallo-grootte van het cluster.
7. **INSERT map overschrijven**. Voer een query- en uitvoer Hallo gegevensset tooa bestand. Deze query retourneert een lijst met Twitter-gebruikers die de meeste tweets of Hallo woord 'Azure' verzonden.

**een component toocreate script en upload het tooAzure**

1. Open Windows PowerShell ISE.
2. Hallo script volgen in het scriptvenster Hallo kopiëren:

    ```powershell
    #region - variables and constants
    $clusterName = "<Existing HDInsight Cluster Name>" # Enter your HDInsight cluster name
    $subscriptionID = "<Azure Subscription ID>"

    $sourceDataPath = "/tutorials/twitter/data"
    $outputPath = "/tutorials/twitter/output"
    $hqlScriptFile = "tutorials/twitter/twitter.hql"

    $hqlStatements = @"
    set hive.exec.dynamic.partition = true;
    set hive.exec.dynamic.partition.mode = nonstrict;

    DROP TABLE tweets_raw;
    CREATE EXTERNAL TABLE tweets_raw (
        json_response STRING
    )
    STORED AS TEXTFILE LOCATION '$sourceDataPath';

    DROP TABLE tweets;
    CREATE TABLE tweets
    (
        id BIGINT,
        created_at STRING,
        created_at_date STRING,
        created_at_year STRING,
        created_at_month STRING,
        created_at_day STRING,
        created_at_time STRING,
        in_reply_to_user_id_str STRING,
        text STRING,
        contributors STRING,
        retweeted STRING,
        truncated STRING,
        coordinates STRING,
        source STRING,
        retweet_count INT,
        url STRING,
        hashtags array<STRING>,
        user_mentions array<STRING>,
        first_hashtag STRING,
        first_user_mention STRING,
        screen_name STRING,
        name STRING,
        followers_count INT,
        listed_count INT,
        friends_count INT,
        lang STRING,
        user_location STRING,
        time_zone STRING,
        profile_image_url STRING,
        json_response STRING
    );

    FROM tweets_raw
    INSERT OVERWRITE TABLE tweets
    SELECT
        cast(get_json_object(json_response, '$.id_str') as BIGINT),
        get_json_object(json_response, '$.created_at'),
        concat(substr (get_json_object(json_response, '$.created_at'),1,10),' ',
        substr (get_json_object(json_response, '$.created_at'),27,4)),
        substr (get_json_object(json_response, '$.created_at'),27,4),
        case substr (get_json_object(json_response, '$.created_at'),5,3)
            when "Jan" then "01"
            when "Feb" then "02"
            when "Mar" then "03"
            when "Apr" then "04"
            when "May" then "05"
            when "Jun" then "06"
            when "Jul" then "07"
            when "Aug" then "08"
            when "Sep" then "09"
            when "Oct" then "10"
            when "Nov" then "11"
            when "Dec" then "12" end,
        substr (get_json_object(json_response, '$.created_at'),9,2),
        substr (get_json_object(json_response, '$.created_at'),12,8),
        get_json_object(json_response, '$.in_reply_to_user_id_str'),
        get_json_object(json_response, '$.text'),
        get_json_object(json_response, '$.contributors'),
        get_json_object(json_response, '$.retweeted'),
        get_json_object(json_response, '$.truncated'),
        get_json_object(json_response, '$.coordinates'),
        get_json_object(json_response, '$.source'),
        cast (get_json_object(json_response, '$.retweet_count') as INT),
        get_json_object(json_response, '$.entities.display_url'),
        array(
            trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[1].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[2].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[3].text'))),
            trim(lower(get_json_object(json_response, '$.entities.hashtags[4].text')))),
        array(
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[1].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[2].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[3].screen_name'))),
            trim(lower(get_json_object(json_response, '$.entities.user_mentions[4].screen_name')))),
        trim(lower(get_json_object(json_response, '$.entities.hashtags[0].text'))),
        trim(lower(get_json_object(json_response, '$.entities.user_mentions[0].screen_name'))),
        get_json_object(json_response, '$.user.screen_name'),
        get_json_object(json_response, '$.user.name'),
        cast (get_json_object(json_response, '$.user.followers_count') as INT),
        cast (get_json_object(json_response, '$.user.listed_count') as INT),
        cast (get_json_object(json_response, '$.user.friends_count') as INT),
        get_json_object(json_response, '$.user.lang'),
        get_json_object(json_response, '$.user.location'),
        get_json_object(json_response, '$.user.time_zone'),
        get_json_object(json_response, '$.user.profile_image_url'),
        json_response
    WHERE (length(json_response) > 500);

    INSERT OVERWRITE DIRECTORY '$outputPath'
    SELECT name, screen_name, count(1) as cc
        FROM tweets
        WHERE text like "%Azure%"
        GROUP BY name,screen_name
        ORDER BY cc DESC LIMIT 10;
    "@
    #endregion

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing hello Hive script file
    Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define hello connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing hello hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write hello Hive script file tooBlob storage
    Write-Host "Write toohello destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. De eerste twee variabelen Hallo in Hallo script ingesteld:

   | Variabele | Beschrijving |
   | --- | --- |
   |  $clusterName |Voer naam Hallo HDInsight-cluster waar u toorun Hallo-toepassing. |
   |  $subscriptionID |Voer uw Azure-abonnement-ID. |
   |  $sourceDataPath |Hello Azure Blob storage locatie waar Hallo Hive-query's Hallo gegevens leest. U hoeft niet toochange deze variabele. |
   |  $outputPath |Hello Azure Blob-opslaglocatie waarin Hallo Hive-query's Hallo resultaten wordt de uitvoer. U hoeft niet toochange deze variabele. |
   |  $hqlScriptFile |Hallo locatie en naam Hallo van Hallo HiveQL-scriptbestand. U hoeft niet toochange deze variabele. |
4. Druk op **F5** toorun Hallo script. Als u problemen als tijdelijke oplossing ondervindt alle Hallo regels selecteren en druk vervolgens op **F8**.
5. U ziet 'Voltooi!' aan het einde van de Hallo van Hallo uitvoer. Eventuele foutberichten wordt rood weergegeven.

Als een validatieprocedure, kunt u controleren Hallo uitvoerbestand **/tutorials/twitter/twitter.hql**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell. Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].

## <a name="process-twitter-data-by-using-hive"></a>Twitter-gegevens verwerken met behulp van Hive
U hebt al Hallo voorbereiding van het werk. U kunt nu aanroepen Hallo Hive-script en Hallo resultaten controleren.

### <a name="submit-a-hive-job"></a>Verzenden van een Hive-taak
Hallo volgende Windows PowerShell-script toorun Hallo Hive-script gebruiken. U moet eerst tooset Hallo-variabele.

> [!NOTE]
> toouse hello tweets en HiveQL-script die u hebt geüpload in de laatste twee secties hello, set $hqlScriptFile too"/tutorials/twitter/twitter.hql Hallo". toouse hello waarden die zijn geüpload tooa openbare blob voor u, stelt u $hqlScriptFile te'wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql'.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of hello following
$hqlScriptFile = "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql"
$hqlScriptFile = "/tutorials/twitter/twitter.hql"

$statusFolder = "/tutorials/twitter/jobstatus"
#endregion

$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value

$defaultBlobContainerName = $myCluster.DefaultStorageContainer

#region - Invoke Hive
Write-Host "Invoke Hive ... " -ForegroundColor Green

# Create hello HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display hello standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-hello-results"></a>Hallo resultaten controleren
Hallo volgende Windows PowerShell-script toocheck hello taakuitvoer Hive gebruiken. U moet eerst twee tooset Hallo-variabelen.

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # hello name of hello blob toobe downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get hello default storage account name and container name based on hello cluster name ..." -ForegroundColor Green
$myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroupName = $myCluster.ResourceGroup
$defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
$defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
$defaultBlobContainerName = $myCluster.DefaultStorageContainer

Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

Write-Host "Create a context object ... " -ForegroundColor Green
$storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
#endregion

#region - Download blob and display blob
Write-Host "Download hello blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display hello output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> Hallo Hive-tabel gebruikt \001 Hallo veldscheidingsteken. Hallo scheidingsteken is niet zichtbaar in Hallo uitvoer.

Nadat de analyseresultaten Hallo in Azure Blob-opslag zijn geplaatst, kunt u Hallo gegevens tooan Azure SQL database/SQL-server exporteren, Hallo gegevens tooExcel exporteren via Power Query of uw toepassingsgegevens toohello verbinding via Hallo Hive ODBC-stuurprogramma. Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop], [vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data], [ Verbinding maken met Excel tooHDInsight met Power Query][hdinsight-power-query], en [tooHDInsight Excel verbinding maken met het stuurprogramma Microsoft Hive ODBC Hallo][hdinsight-hive-odbc].

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebben we gezien hoe tootransform een ongestructureerde gegevensset JSON in een gestructureerde Hive-tabel te tooquery verkennen en analyseren van gegevens van Twitter met behulp van HDInsight op Azure. toolearn meer, Zie:

* [Aan de slag met HDInsight][hdinsight-get-started]
* [Realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment]
* [Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data]
* [Verbinding maken met Excel tooHDInsight met Power Query][hdinsight-power-query]
* [Verbinding maken met Excel tooHDInsight Hello Microsoft Hive ODBC-stuurprogramma][hdinsight-hive-odbc]
* [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[apache-hive-tutorial]: https://cwiki.apache.org/confluence/display/Hive/Tutorial

[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176961.aspx

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]:hdinsight-hadoop-use-blob-storage.md#access-blobs-using-azure-powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-odbc-driver.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
