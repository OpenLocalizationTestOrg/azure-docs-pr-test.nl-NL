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
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="19a01-103">Twitter-gegevens met Hive in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="19a01-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="19a01-104">Sociale websites zijn een belangrijke drijvende dwingt Hallo voor big data.</span><span class="sxs-lookup"><span data-stu-id="19a01-104">Social websites are one of hello major driving forces for big-data adoption.</span></span> <span data-ttu-id="19a01-105">Openbare API's die worden geleverd door sites zoals Twitter zijn nuttig gegevensbron voor het analyseren en kennis van populaire trends.</span><span class="sxs-lookup"><span data-stu-id="19a01-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="19a01-106">In deze zelfstudie wordt u tweets verkrijgen door middel van een streaming-API Twitter en vervolgens met Apache Hive op Azure HDInsight tooget een lijst met Twitter-gebruikers die Hallo meeste tweets die deel uitmaakt van een bepaald woord verzonden.</span><span class="sxs-lookup"><span data-stu-id="19a01-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight tooget a list of Twitter users who sent hello most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19a01-107">Hallo moet stappen in dit document een HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="19a01-107">hello steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="19a01-108">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="19a01-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="19a01-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19a01-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="19a01-110">Zie voor stappen specifieke tooa op basis van Linux-cluster, [analyseren Twitter-gegevens met Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="19a01-110">For steps specific tooa Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="19a01-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="19a01-111">Prerequisites</span></span>
<span data-ttu-id="19a01-112">Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="19a01-112">Before you begin this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="19a01-113">**Een werkstation** met Azure PowerShell installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="19a01-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="19a01-114">tooexecute Windows PowerShell-scripts, die u moet Azure PowerShell als administrator uitvoeren en stel een uitvoeringsbeleid voor hello te*RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="19a01-114">tooexecute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set hello execution policy too*RemoteSigned*.</span></span> <span data-ttu-id="19a01-115">Zie [Run Windows PowerShell-scripts][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="19a01-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="19a01-116">Voordat u Windows PowerShell-scripts uitvoert, zorg ervoor dat u verbonden tooyour Azure-abonnement met behulp van de volgende cmdlet Hallo:</span><span class="sxs-lookup"><span data-stu-id="19a01-116">Before running Windows PowerShell scripts, make sure you are connected tooyour Azure subscription by using hello following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="19a01-117">Als u meerdere Azure-abonnementen hebt, gebruikt u Hallo cmdlet tooset Hallo huidige abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="19a01-117">If you have multiple Azure subscriptions, use hello following cmdlet tooset hello current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="19a01-118">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="19a01-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="19a01-119">Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="19a01-119">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="19a01-120">Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a01-120">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="19a01-121">Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19a01-121">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="19a01-122">**Een Azure HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="19a01-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="19a01-123">Zie voor instructies over het inrichten van het cluster [aan de slag met HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="19a01-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="19a01-124">Hallo clusternaam moet u later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="19a01-124">You will need hello cluster name later in hello tutorial.</span></span>

<span data-ttu-id="19a01-125">Hallo bevat volgende tabel Hallo-bestanden in deze zelfstudie gebruikt:</span><span class="sxs-lookup"><span data-stu-id="19a01-125">hello following table lists hello files used in this tutorial:</span></span>

| <span data-ttu-id="19a01-126">Bestanden</span><span class="sxs-lookup"><span data-stu-id="19a01-126">Files</span></span> | <span data-ttu-id="19a01-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19a01-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19a01-128">/tutorials/Twitter/Data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="19a01-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="19a01-129">Hallo brongegevens voor Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="19a01-129">hello source data for hello Hive job.</span></span> |
| <span data-ttu-id="19a01-130">/tutorials/Twitter/output</span><span class="sxs-lookup"><span data-stu-id="19a01-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="19a01-131">Hallo uitvoermap voor Hallo Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="19a01-131">hello output folder for hello Hive job.</span></span> <span data-ttu-id="19a01-132">Hallo Hive-taak uitvoer standaardbestandsnaam is **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="19a01-132">hello default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="19a01-133">tutorials/Twitter/Twitter.hql</span><span class="sxs-lookup"><span data-stu-id="19a01-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="19a01-134">Hallo HiveQL-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="19a01-134">hello HiveQL script file.</span></span> |
| <span data-ttu-id="19a01-135">/tutorials/Twitter/JobStatus</span><span class="sxs-lookup"><span data-stu-id="19a01-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="19a01-136">Hallo taakstatus Hadoop.</span><span class="sxs-lookup"><span data-stu-id="19a01-136">hello Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="19a01-137">Get Twitter-feeds</span><span class="sxs-lookup"><span data-stu-id="19a01-137">Get Twitter feed</span></span>
<span data-ttu-id="19a01-138">In deze zelfstudie gebruikt u Hallo [Twitter streaming-API's][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="19a01-138">In this tutorial, you will use hello [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="19a01-139">Hallo specifieke Twitter streaming-API die u wilt gebruiken is [statussen-/ filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="19a01-139">hello specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="19a01-140">Een bestand met 10.000 tweets en Hive-scriptbestand hello (behandeld in de volgende sectie Hallo) zijn geüpload in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="19a01-140">A file containing 10,000 tweets and hello Hive script file (covered in hello next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="19a01-141">Als u toouse Hallo geüpload bestanden wilt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="19a01-141">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="19a01-142">[Tweets gegevens](https://dev.twitter.com/docs/platform-objects/tweets) wordt opgeslagen in Hallo JSON JavaScript Object Notation ()-indeling die een complexe geneste structuur bevat.</span><span class="sxs-lookup"><span data-stu-id="19a01-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in hello JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="19a01-143">In plaats van een groot aantal regels code schrijven met behulp van een conventionele programmeertaal, kunt u deze geneste structuur in een Hive-tabel transformeren zodat deze kan worden doorzocht door een Structured Query Language (SQL)-taal genaamd HiveQL, zoals.</span><span class="sxs-lookup"><span data-stu-id="19a01-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="19a01-144">Twitter OAuth tooprovide geautoriseerde toegang tooits API gebruikt.</span><span class="sxs-lookup"><span data-stu-id="19a01-144">Twitter uses OAuth tooprovide authorized access tooits API.</span></span> <span data-ttu-id="19a01-145">OAuth is een authenticatieprotocol waarmee gebruikers tooapprove toepassingen tooact namens hen zonder het delen van hun wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="19a01-145">OAuth is an authentication protocol that allows users tooapprove applications tooact on their behalf without sharing their password.</span></span> <span data-ttu-id="19a01-146">Meer informatie kunt vinden op [oauth.net](http://oauth.net/) of in Hallo uitstekende [inleiding handleiding tooOAuth](http://hueniverse.com/oauth/) van Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="19a01-146">More information can be found at [oauth.net](http://oauth.net/) or in hello excellent [Beginner's Guide tooOAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="19a01-147">Hallo eerste stap toouse OAuth is toocreate een nieuwe toepassing op Hallo Developer Twitter-site.</span><span class="sxs-lookup"><span data-stu-id="19a01-147">hello first step toouse OAuth is toocreate a new application on hello Twitter Developer site.</span></span>

<span data-ttu-id="19a01-148">**toocreate Twitter-toepassing**</span><span class="sxs-lookup"><span data-stu-id="19a01-148">**toocreate a Twitter application**</span></span>

1. <span data-ttu-id="19a01-149">Aanmelden te[https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="19a01-149">Sign in too[https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="19a01-150">Klik op Hallo **nu aanmelden** koppelen als u een Twitter-account niet hebt.</span><span class="sxs-lookup"><span data-stu-id="19a01-150">Click hello **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="19a01-151">Klik op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="19a01-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="19a01-152">Voer **naam**, **beschrijving**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="19a01-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="19a01-153">U kunt een URL voor Hallo gezamenlijk **Website** veld.</span><span class="sxs-lookup"><span data-stu-id="19a01-153">You can make up a URL for hello **Website** field.</span></span> <span data-ttu-id="19a01-154">Hallo volgende tabel ziet u enkele waarden voorbeeld toouse:</span><span class="sxs-lookup"><span data-stu-id="19a01-154">hello following table shows some sample values toouse:</span></span>

   | <span data-ttu-id="19a01-155">Veld</span><span class="sxs-lookup"><span data-stu-id="19a01-155">Field</span></span> | <span data-ttu-id="19a01-156">Waarde</span><span class="sxs-lookup"><span data-stu-id="19a01-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="19a01-157">Naam</span><span class="sxs-lookup"><span data-stu-id="19a01-157">Name</span></span> |<span data-ttu-id="19a01-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="19a01-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="19a01-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19a01-159">Description</span></span> |<span data-ttu-id="19a01-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="19a01-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="19a01-161">Website</span><span class="sxs-lookup"><span data-stu-id="19a01-161">Website</span></span> |<span data-ttu-id="19a01-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="19a01-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="19a01-163">Controleer **Ja, ik ga akkoord**, en klik vervolgens op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="19a01-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="19a01-164">Klik op Hallo **machtigingen** tabblad Hallo standaardmachtiging **alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="19a01-164">Click hello **Permissions** tab. hello default permission is **Read only**.</span></span> <span data-ttu-id="19a01-165">Dit is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="19a01-165">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="19a01-166">Klik op Hallo **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="19a01-166">Click hello **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="19a01-167">Klik op **maken van mijn toegangstoken**.</span><span class="sxs-lookup"><span data-stu-id="19a01-167">Click **Create my access token**.</span></span>
8. <span data-ttu-id="19a01-168">Klik op **Test OAuth** in Hallo rechterbovenhoek van Hallo pagina.</span><span class="sxs-lookup"><span data-stu-id="19a01-168">Click **Test OAuth** in hello upper-right corner of hello page.</span></span>
9. <span data-ttu-id="19a01-169">Noteer **consumentsleutel**, **consumentgeheim**, **toegangstoken**, en **Access token geheim**.</span><span class="sxs-lookup"><span data-stu-id="19a01-169">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="19a01-170">Hallo-waarden moet u later in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="19a01-170">You will need hello values later in hello tutorial.</span></span>

<span data-ttu-id="19a01-171">In deze zelfstudie gebruikt u Windows PowerShell toomake Hallo webserviceaanroep.</span><span class="sxs-lookup"><span data-stu-id="19a01-171">In this tutorial, you will use Windows PowerShell toomake hello web service call.</span></span> <span data-ttu-id="19a01-172">Zie voor een voorbeeld .NET C# [realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="19a01-172">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="19a01-173">Hallo andere webserviceaanroepen toomake populaire hulpprogramma is [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="19a01-173">hello other popular tool toomake web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="19a01-174">CURL kan worden gedownload vanaf [hier][curl-download].</span><span class="sxs-lookup"><span data-stu-id="19a01-174">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="19a01-175">Als u Hallo curl-opdracht in Windows gebruikt, kunt u dubbele aanhalingstekens in plaats van enkele aanhalingstekens voor Hallo optiewaarden.</span><span class="sxs-lookup"><span data-stu-id="19a01-175">When you use hello curl command in Windows, use double quotes instead of single quotes for hello option values.</span></span>

<span data-ttu-id="19a01-176">**tooget tweets**</span><span class="sxs-lookup"><span data-stu-id="19a01-176">**tooget tweets**</span></span>

1. <span data-ttu-id="19a01-177">Open Windows PowerShell Integrated Scripting Environment (ISE) Hallo.</span><span class="sxs-lookup"><span data-stu-id="19a01-177">Open hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="19a01-178">(Typ op Hallo Windows 8 startscherm **PowerShell_ISE** en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="19a01-178">(On hello Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="19a01-179">Zie [Start Windows PowerShell in Windows 8 en Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="19a01-179">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="19a01-180">Hallo script volgen in het scriptvenster Hallo kopiëren:</span><span class="sxs-lookup"><span data-stu-id="19a01-180">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="19a01-181">Hallo eerste vijf tooeight variabelen instellen in Hallo script:</span><span class="sxs-lookup"><span data-stu-id="19a01-181">Set hello first five tooeight variables in hello script:</span></span>

    <span data-ttu-id="19a01-182">Variabele</span><span class="sxs-lookup"><span data-stu-id="19a01-182">Variable</span></span>|<span data-ttu-id="19a01-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19a01-183">Description</span></span>
    ---|---
    <span data-ttu-id="19a01-184">$clusterName</span><span class="sxs-lookup"><span data-stu-id="19a01-184">$clusterName</span></span>|<span data-ttu-id="19a01-185">Dit is de naam Hallo van Hallo HDInsight-cluster waar u toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="19a01-185">This is hello name of hello HDInsight cluster where you want toorun hello application.</span></span>
    <span data-ttu-id="19a01-186">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="19a01-186">$oauth_consumer_key</span></span>|<span data-ttu-id="19a01-187">Dit is de Twitter-toepassing hello **consumentsleutel** u opgeschreven eerder tijdens het maken van Hallo Twitter-toepassing.</span><span class="sxs-lookup"><span data-stu-id="19a01-187">This is hello Twitter application **consumer key** you wrote down earlier when you created hello Twitter application.</span></span>
    <span data-ttu-id="19a01-188">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="19a01-188">$oauth_consumer_secret</span></span>|<span data-ttu-id="19a01-189">Dit is de Twitter-toepassing hello **consumentgeheim** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="19a01-189">This is hello Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="19a01-190">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="19a01-190">$oauth_token</span></span>|<span data-ttu-id="19a01-191">Dit is de Twitter-toepassing hello **toegangstoken** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="19a01-191">This is hello Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="19a01-192">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="19a01-192">$oauth_token_secret</span></span>|<span data-ttu-id="19a01-193">Dit is de Twitter-toepassing hello **access token geheim** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="19a01-193">This is hello Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="19a01-194">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="19a01-194">$destBlobName</span></span>|<span data-ttu-id="19a01-195">Dit is Hallo uitvoer-blob-naam.</span><span class="sxs-lookup"><span data-stu-id="19a01-195">This is hello output blob name.</span></span> <span data-ttu-id="19a01-196">de standaardwaarde Hallo is **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="19a01-196">hello default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="19a01-197">Als u de standaardwaarde Hallo wijzigt, moet u Windows PowerShell-scripts voor tooupdate Hallo dienovereenkomstig.</span><span class="sxs-lookup"><span data-stu-id="19a01-197">If you change hello default value, you will need tooupdate hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="19a01-198">$trackString</span><span class="sxs-lookup"><span data-stu-id="19a01-198">$trackString</span></span>|<span data-ttu-id="19a01-199">Hallo-webservice wordt tweets gerelateerde toothese trefwoorden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19a01-199">hello web service will return tweets related toothese keywords.</span></span> <span data-ttu-id="19a01-200">de standaardwaarde Hallo is **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="19a01-200">hello default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="19a01-201">Als u de standaardwaarde Hallo wijzigt, wordt u Windows PowerShell-scripts Hallo dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="19a01-201">If you change hello default value, you will update hello Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="19a01-202">$lineMax</span><span class="sxs-lookup"><span data-stu-id="19a01-202">$lineMax</span></span>|<span data-ttu-id="19a01-203">Hallo-waarde bepaalt hoeveel tweets Hallo-script leest.</span><span class="sxs-lookup"><span data-stu-id="19a01-203">hello value determines how many tweets hello script will read.</span></span> <span data-ttu-id="19a01-204">Het duurt ongeveer drie minuten tooread 100 tweets.</span><span class="sxs-lookup"><span data-stu-id="19a01-204">It takes about three minutes tooread 100 tweets.</span></span> <span data-ttu-id="19a01-205">U kunt een groter aantal instellen, maar duurt het meer tijd toodownload.</span><span class="sxs-lookup"><span data-stu-id="19a01-205">You can set a larger number, but it will take more time toodownload.</span></span>

1. <span data-ttu-id="19a01-206">Druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="19a01-206">Press **F5** toorun hello script.</span></span> <span data-ttu-id="19a01-207">Als u problemen als tijdelijke oplossing ondervindt alle Hallo regels selecteren en druk vervolgens op **F8**.</span><span class="sxs-lookup"><span data-stu-id="19a01-207">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
2. <span data-ttu-id="19a01-208">U ziet 'Voltooi!'</span><span class="sxs-lookup"><span data-stu-id="19a01-208">You shall see "Complete!"</span></span> <span data-ttu-id="19a01-209">aan het einde van de Hallo van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="19a01-209">at hello end of hello output.</span></span> <span data-ttu-id="19a01-210">Eventuele foutberichten wordt rood weergegeven.</span><span class="sxs-lookup"><span data-stu-id="19a01-210">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="19a01-211">Als een validatieprocedure, kunt u controleren Hallo uitvoerbestand **/tutorials/twitter/data/tweets.txt**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a01-211">As a validation procedure, you can check hello output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="19a01-212">Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="19a01-212">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="19a01-213">HiveQL-script maken</span><span class="sxs-lookup"><span data-stu-id="19a01-213">Create HiveQL script</span></span>
<span data-ttu-id="19a01-214">Met Azure PowerShell, kunt u meerdere HiveQL-instructies één uitvoeren op een tijd of pakket Hallo instructie van HiveQL in een scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="19a01-214">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package hello HiveQL statement into a script file.</span></span> <span data-ttu-id="19a01-215">In deze zelfstudie maakt u een HiveQL-script.</span><span class="sxs-lookup"><span data-stu-id="19a01-215">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="19a01-216">Hallo-scriptbestand moet tooAzure geüploade Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="19a01-216">hello script file must be uploaded tooAzure Blob storage.</span></span> <span data-ttu-id="19a01-217">In de volgende sectie hello uitvoeren u Hallo-scriptbestand met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a01-217">In hello next section, you will run hello script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="19a01-218">Hallo Hive-scriptbestand en een bestand met 10.000 tweets zijn geüpload in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="19a01-218">hello Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="19a01-219">Als u toouse Hallo geüpload bestanden wilt, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="19a01-219">You can skip this section if you want toouse hello uploaded files.</span></span>

<span data-ttu-id="19a01-220">Hallo HiveQL-script voert Hallo volgende uit:</span><span class="sxs-lookup"><span data-stu-id="19a01-220">hello HiveQL script will perform hello following:</span></span>

1. <span data-ttu-id="19a01-221">**Hallo tweets_raw tabel** geval Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="19a01-221">**Drop hello tweets_raw table** in case hello table already exists.</span></span>
2. <span data-ttu-id="19a01-222">**Hallo tweets_raw Hive-tabel maken**.</span><span class="sxs-lookup"><span data-stu-id="19a01-222">**Create hello tweets_raw Hive table**.</span></span> <span data-ttu-id="19a01-223">Deze tijdelijke gestructureerde Hive-tabel bevat Hallo-gegevens voor verdere uitpakken, transformeren en laden (ETL) verwerking.</span><span class="sxs-lookup"><span data-stu-id="19a01-223">This temporary Hive structured table holds hello data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="19a01-224">Zie voor informatie over partities, [Hive-zelfstudie][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="19a01-224">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="19a01-225">**Gegevens laden** van bronmap hello, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="19a01-225">**Load data** from hello source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="19a01-226">Hallo grote tweets gegevensset in geneste JSON-indeling heeft nu is omgezet in de structuur van een tijdelijke Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="19a01-226">hello large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="19a01-227">**Verwijder Hallo tweets tabel** geval Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="19a01-227">**Drop hello tweets table** in case hello table already exists.</span></span>
5. <span data-ttu-id="19a01-228">**Hallo tweets tabel maken**.</span><span class="sxs-lookup"><span data-stu-id="19a01-228">**Create hello tweets table**.</span></span> <span data-ttu-id="19a01-229">Voordat u kunt een query op Hallo tweets gegevensset met Hive, moet u toorun een ander ETL-proces.</span><span class="sxs-lookup"><span data-stu-id="19a01-229">Before you can query against hello tweets dataset by using Hive, you need toorun another ETL process.</span></span> <span data-ttu-id="19a01-230">Dit proces ETL definieert een meer gedetailleerde tabelschema voor Hallo-gegevens die u hebt opgeslagen in Hallo 'twitter_raw' tabel.</span><span class="sxs-lookup"><span data-stu-id="19a01-230">This ETL process defines a more detailed table schema for hello data that you have stored in hello "twitter_raw" table.</span></span>
6. <span data-ttu-id="19a01-231">**Overschrijven tabel invoegen**.</span><span class="sxs-lookup"><span data-stu-id="19a01-231">**Insert overwrite table**.</span></span> <span data-ttu-id="19a01-232">Dit complexe Hive-script wordt een reeks lang MapReduce-taken starten door Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="19a01-232">This complex Hive script will kick off a set of long MapReduce jobs by hello Hadoop cluster.</span></span> <span data-ttu-id="19a01-233">Dit kan ongeveer 10 minuten duren, afhankelijk van uw gegevensset en het Hallo-grootte van het cluster.</span><span class="sxs-lookup"><span data-stu-id="19a01-233">Depending on your dataset and hello size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="19a01-234">**INSERT map overschrijven**.</span><span class="sxs-lookup"><span data-stu-id="19a01-234">**Insert overwrite directory**.</span></span> <span data-ttu-id="19a01-235">Voer een query- en uitvoer Hallo gegevensset tooa bestand.</span><span class="sxs-lookup"><span data-stu-id="19a01-235">Run a query and output hello dataset tooa file.</span></span> <span data-ttu-id="19a01-236">Deze query retourneert een lijst met Twitter-gebruikers die de meeste tweets of Hallo woord 'Azure' verzonden.</span><span class="sxs-lookup"><span data-stu-id="19a01-236">This query will return a list of Twitter users who sent most tweets that contained hello word "Azure".</span></span>

<span data-ttu-id="19a01-237">**een component toocreate script en upload het tooAzure**</span><span class="sxs-lookup"><span data-stu-id="19a01-237">**toocreate a Hive script and upload it tooAzure**</span></span>

1. <span data-ttu-id="19a01-238">Open Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="19a01-238">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="19a01-239">Hallo script volgen in het scriptvenster Hallo kopiëren:</span><span class="sxs-lookup"><span data-stu-id="19a01-239">Copy hello following script into hello script pane:</span></span>

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

3. <span data-ttu-id="19a01-240">De eerste twee variabelen Hallo in Hallo script ingesteld:</span><span class="sxs-lookup"><span data-stu-id="19a01-240">Set hello first two variables in hello script:</span></span>

   | <span data-ttu-id="19a01-241">Variabele</span><span class="sxs-lookup"><span data-stu-id="19a01-241">Variable</span></span> | <span data-ttu-id="19a01-242">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="19a01-242">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="19a01-243">$clusterName</span><span class="sxs-lookup"><span data-stu-id="19a01-243">$clusterName</span></span> |<span data-ttu-id="19a01-244">Voer naam Hallo HDInsight-cluster waar u toorun Hallo-toepassing.</span><span class="sxs-lookup"><span data-stu-id="19a01-244">Enter hello HDInsight cluster name where you want toorun hello application.</span></span> |
   |  <span data-ttu-id="19a01-245">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="19a01-245">$subscriptionID</span></span> |<span data-ttu-id="19a01-246">Voer uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="19a01-246">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="19a01-247">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="19a01-247">$sourceDataPath</span></span> |<span data-ttu-id="19a01-248">Hello Azure Blob storage locatie waar Hallo Hive-query's Hallo gegevens leest.</span><span class="sxs-lookup"><span data-stu-id="19a01-248">hello Azure Blob storage location where hello Hive queries will read hello data from.</span></span> <span data-ttu-id="19a01-249">U hoeft niet toochange deze variabele.</span><span class="sxs-lookup"><span data-stu-id="19a01-249">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="19a01-250">$outputPath</span><span class="sxs-lookup"><span data-stu-id="19a01-250">$outputPath</span></span> |<span data-ttu-id="19a01-251">Hello Azure Blob-opslaglocatie waarin Hallo Hive-query's Hallo resultaten wordt de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="19a01-251">hello Azure Blob storage location where hello Hive queries will output hello results.</span></span> <span data-ttu-id="19a01-252">U hoeft niet toochange deze variabele.</span><span class="sxs-lookup"><span data-stu-id="19a01-252">You don't need toochange this variable.</span></span> |
   |  <span data-ttu-id="19a01-253">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="19a01-253">$hqlScriptFile</span></span> |<span data-ttu-id="19a01-254">Hallo locatie en naam Hallo van Hallo HiveQL-scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="19a01-254">hello location and hello file name of hello HiveQL script file.</span></span> <span data-ttu-id="19a01-255">U hoeft niet toochange deze variabele.</span><span class="sxs-lookup"><span data-stu-id="19a01-255">You don't need toochange this variable.</span></span> |
4. <span data-ttu-id="19a01-256">Druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="19a01-256">Press **F5** toorun hello script.</span></span> <span data-ttu-id="19a01-257">Als u problemen als tijdelijke oplossing ondervindt alle Hallo regels selecteren en druk vervolgens op **F8**.</span><span class="sxs-lookup"><span data-stu-id="19a01-257">If you run into problems, as a workaround, select all hello lines, and then press **F8**.</span></span>
5. <span data-ttu-id="19a01-258">U ziet 'Voltooi!'</span><span class="sxs-lookup"><span data-stu-id="19a01-258">You shall see "Complete!"</span></span> <span data-ttu-id="19a01-259">aan het einde van de Hallo van Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="19a01-259">at hello end of hello output.</span></span> <span data-ttu-id="19a01-260">Eventuele foutberichten wordt rood weergegeven.</span><span class="sxs-lookup"><span data-stu-id="19a01-260">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="19a01-261">Als een validatieprocedure, kunt u controleren Hallo uitvoerbestand **/tutorials/twitter/twitter.hql**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a01-261">As a validation procedure, you can check hello output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="19a01-262">Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="19a01-262">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="19a01-263">Twitter-gegevens verwerken met behulp van Hive</span><span class="sxs-lookup"><span data-stu-id="19a01-263">Process Twitter data by using Hive</span></span>
<span data-ttu-id="19a01-264">U hebt al Hallo voorbereiding van het werk.</span><span class="sxs-lookup"><span data-stu-id="19a01-264">You have finished all hello preparation work.</span></span> <span data-ttu-id="19a01-265">U kunt nu aanroepen Hallo Hive-script en Hallo resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="19a01-265">Now, you can invoke hello Hive script and check hello results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="19a01-266">Verzenden van een Hive-taak</span><span class="sxs-lookup"><span data-stu-id="19a01-266">Submit a Hive job</span></span>
<span data-ttu-id="19a01-267">Hallo volgende Windows PowerShell-script toorun Hallo Hive-script gebruiken.</span><span class="sxs-lookup"><span data-stu-id="19a01-267">Use hello following Windows PowerShell script toorun hello Hive script.</span></span> <span data-ttu-id="19a01-268">U moet eerst tooset Hallo-variabele.</span><span class="sxs-lookup"><span data-stu-id="19a01-268">You will need tooset hello first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="19a01-269">toouse hello tweets en HiveQL-script die u hebt geüpload in de laatste twee secties hello, set $hqlScriptFile too"/tutorials/twitter/twitter.hql Hallo".</span><span class="sxs-lookup"><span data-stu-id="19a01-269">toouse hello tweets and hello HiveQL script you uploaded in hello last two sections, set $hqlScriptFile too"/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="19a01-270">toouse hello waarden die zijn geüpload tooa openbare blob voor u, stelt u $hqlScriptFile te'wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql'.</span><span class="sxs-lookup"><span data-stu-id="19a01-270">toouse hello ones that have been uploaded tooa public blob for you, set $hqlScriptFile too"wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

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

### <a name="check-hello-results"></a><span data-ttu-id="19a01-271">Hallo resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="19a01-271">Check hello results</span></span>
<span data-ttu-id="19a01-272">Hallo volgende Windows PowerShell-script toocheck hello taakuitvoer Hive gebruiken.</span><span class="sxs-lookup"><span data-stu-id="19a01-272">Use hello following Windows PowerShell script toocheck hello Hive job output.</span></span> <span data-ttu-id="19a01-273">U moet eerst twee tooset Hallo-variabelen.</span><span class="sxs-lookup"><span data-stu-id="19a01-273">You will need tooset hello first two variables.</span></span>

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
> Hallo Hive-tabel gebruikt \001 Hallo veldscheidingsteken. <span data-ttu-id="19a01-275">Hallo scheidingsteken is niet zichtbaar in Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="19a01-275">hello delimiter is not visible in hello output.</span></span>

<span data-ttu-id="19a01-276">Nadat de analyseresultaten Hallo in Azure Blob-opslag zijn geplaatst, kunt u Hallo gegevens tooan Azure SQL database/SQL-server exporteren, Hallo gegevens tooExcel exporteren via Power Query of uw toepassingsgegevens toohello verbinding via Hallo Hive ODBC-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="19a01-276">After hello analysis results have been placed in Azure Blob storage, you can export hello data tooan Azure SQL database/SQL server, export hello data tooExcel by using Power Query, or connect your application toohello data by using hello Hive ODBC Driver.</span></span> <span data-ttu-id="19a01-277">Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop], [vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data], [ Verbinding maken met Excel tooHDInsight met Power Query][hdinsight-power-query], en [tooHDInsight Excel verbinding maken met het stuurprogramma Microsoft Hive ODBC Hallo][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="19a01-277">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel tooHDInsight with Power Query][hdinsight-power-query], and [Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="19a01-278">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19a01-278">Next steps</span></span>
<span data-ttu-id="19a01-279">In deze zelfstudie hebben we gezien hoe tootransform een ongestructureerde gegevensset JSON in een gestructureerde Hive-tabel te tooquery verkennen en analyseren van gegevens van Twitter met behulp van HDInsight op Azure.</span><span class="sxs-lookup"><span data-stu-id="19a01-279">In this tutorial we have seen how tootransform an unstructured JSON dataset into a structured Hive table tooquery, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="19a01-280">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="19a01-280">toolearn more, see:</span></span>

* <span data-ttu-id="19a01-281">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="19a01-281">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="19a01-282">[Realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="19a01-282">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="19a01-283">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="19a01-283">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="19a01-284">[Verbinding maken met Excel tooHDInsight met Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="19a01-284">[Connect Excel tooHDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="19a01-285">[Verbinding maken met Excel tooHDInsight Hello Microsoft Hive ODBC-stuurprogramma][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="19a01-285">[Connect Excel tooHDInsight with hello Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="19a01-286">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="19a01-286">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
