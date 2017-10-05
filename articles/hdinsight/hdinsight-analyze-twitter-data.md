---
title: Twitter gegevens analyseren met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over het gebruik van Hive om gegevens met Hadoop in HDInsight vinden van de frequentie van de informatie over het gebruik van een bepaald woord Twitter te analyseren.
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
ms.openlocfilehash: 711d364c36c3aba699326f4a76d42891ba3219fb
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-twitter-data-using-hive-in-hdinsight"></a><span data-ttu-id="cec22-103">Twitter-gegevens met Hive in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="cec22-103">Analyze Twitter data using Hive in HDInsight</span></span>
<span data-ttu-id="cec22-104">Sociale websites zijn een van de belangrijke drijvende kracht voor big data acceptatie.</span><span class="sxs-lookup"><span data-stu-id="cec22-104">Social websites are one of the major driving forces for big-data adoption.</span></span> <span data-ttu-id="cec22-105">Openbare API's die worden geleverd door sites zoals Twitter zijn nuttig gegevensbron voor het analyseren en kennis van populaire trends.</span><span class="sxs-lookup"><span data-stu-id="cec22-105">Public APIs provided by sites like Twitter are a useful source of data for analyzing and understanding popular trends.</span></span>
<span data-ttu-id="cec22-106">In deze zelfstudie wordt u tweets verkrijgen door middel van een streaming-API Twitter en gebruik vervolgens Apache Hive in Azure HDInsight om een lijst met Twitter-gebruikers die de meeste tweets die deel uitmaakt van een bepaald woord verzonden.</span><span class="sxs-lookup"><span data-stu-id="cec22-106">In this tutorial, you will get tweets by using a Twitter streaming API, and then use Apache Hive on Azure HDInsight to get a list of Twitter users who sent the most tweets that contained a certain word.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cec22-107">De stappen in dit document moet een HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="cec22-107">The steps in this document require a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="cec22-108">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="cec22-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cec22-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cec22-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="cec22-110">Zie voor specifieke stappen voor een cluster op basis van Linux, [analyseren Twitter-gegevens met Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cec22-110">For steps specific to a Linux-based cluster, see [Analyze Twitter data using Hive in HDInsight (Linux)](hdinsight-analyze-twitter-data-linux.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cec22-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cec22-111">Prerequisites</span></span>
<span data-ttu-id="cec22-112">Voordat u met deze zelfstudie begint, moet u het volgende hebben of hebben gedaan:</span><span class="sxs-lookup"><span data-stu-id="cec22-112">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="cec22-113">**Een werkstation** met Azure PowerShell installeren en configureren.</span><span class="sxs-lookup"><span data-stu-id="cec22-113">**A workstation** with Azure PowerShell installed and configured.</span></span>

    <span data-ttu-id="cec22-114">Voor het uitvoeren van Windows PowerShell-scripts, moet u Azure PowerShell als administrator uitvoeren en het uitvoeringsbeleid instellen op *RemoteSigned*.</span><span class="sxs-lookup"><span data-stu-id="cec22-114">To execute Windows PowerShell scripts, you must run Azure PowerShell as administrator and set the execution policy to *RemoteSigned*.</span></span> <span data-ttu-id="cec22-115">Zie [Run Windows PowerShell-scripts][powershell-script].</span><span class="sxs-lookup"><span data-stu-id="cec22-115">See [Run Windows PowerShell scripts][powershell-script].</span></span>

    <span data-ttu-id="cec22-116">Voordat u Windows PowerShell-scripts uitvoert, zorg ervoor dat u bent verbonden met uw Azure-abonnement met behulp van de volgende cmdlet:</span><span class="sxs-lookup"><span data-stu-id="cec22-116">Before running Windows PowerShell scripts, make sure you are connected to your Azure subscription by using the following cmdlet:</span></span>

    ```powershell
    Login-AzureRmAccount
    ```

    <span data-ttu-id="cec22-117">Als u meerdere Azure-abonnementen hebt, gebruikt u de volgende cmdlet instellen van het huidige abonnement:</span><span class="sxs-lookup"><span data-stu-id="cec22-117">If you have multiple Azure subscriptions, use the following cmdlet to set the current subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionID <Azure Subscription ID>
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="cec22-118">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="cec22-118">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="cec22-119">In de stappen in dit document worden de nieuwe HDInsight-cmdlets gebruikt die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="cec22-119">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="cec22-120">Volg de stappen in [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) (Azure PowerShell installeren en configureren) als u de nieuwste versie van Azure PowerShell wilt installeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-120">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="cec22-121">Als u scripts hebt die moeten worden gewijzigd om ze te kunnen gebruiken met de nieuwe cmdlets die werken met Azure Resource Manager, raadpleegt u [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migreren naar op Azure Resource Manager gebaseerde hulpprogramma’s voor HDInsight-clusters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cec22-121">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

* <span data-ttu-id="cec22-122">**Een Azure HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="cec22-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="cec22-123">Zie voor instructies over het inrichten van het cluster [aan de slag met HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="cec22-123">For instructions on cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="cec22-124">Naam van het cluster moet u later in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cec22-124">You will need the cluster name later in the tutorial.</span></span>

<span data-ttu-id="cec22-125">De volgende tabel bevat de bestanden in deze zelfstudie gebruikt:</span><span class="sxs-lookup"><span data-stu-id="cec22-125">The following table lists the files used in this tutorial:</span></span>

| <span data-ttu-id="cec22-126">Bestanden</span><span class="sxs-lookup"><span data-stu-id="cec22-126">Files</span></span> | <span data-ttu-id="cec22-127">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cec22-127">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cec22-128">/tutorials/Twitter/Data/tweets.txt</span><span class="sxs-lookup"><span data-stu-id="cec22-128">/tutorials/twitter/data/tweets.txt</span></span> |<span data-ttu-id="cec22-129">De brongegevens voor de Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="cec22-129">The source data for the Hive job.</span></span> |
| <span data-ttu-id="cec22-130">/tutorials/Twitter/output</span><span class="sxs-lookup"><span data-stu-id="cec22-130">/tutorials/twitter/output</span></span> |<span data-ttu-id="cec22-131">De uitvoermap voor het Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="cec22-131">The output folder for the Hive job.</span></span> <span data-ttu-id="cec22-132">Het Hive-taak uitvoer standaardbestandsnaam is **000000_0**.</span><span class="sxs-lookup"><span data-stu-id="cec22-132">The default Hive job output file name is **000000_0**.</span></span> |
| <span data-ttu-id="cec22-133">tutorials/Twitter/Twitter.hql</span><span class="sxs-lookup"><span data-stu-id="cec22-133">tutorials/twitter/twitter.hql</span></span> |<span data-ttu-id="cec22-134">Het scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="cec22-134">The HiveQL script file.</span></span> |
| <span data-ttu-id="cec22-135">/tutorials/Twitter/JobStatus</span><span class="sxs-lookup"><span data-stu-id="cec22-135">/tutorials/twitter/jobstatus</span></span> |<span data-ttu-id="cec22-136">De status van de Hadoop-taak.</span><span class="sxs-lookup"><span data-stu-id="cec22-136">The Hadoop job status.</span></span> |

## <a name="get-twitter-feed"></a><span data-ttu-id="cec22-137">Get Twitter-feeds</span><span class="sxs-lookup"><span data-stu-id="cec22-137">Get Twitter feed</span></span>
<span data-ttu-id="cec22-138">In deze zelfstudie gebruikt u de [Twitter streaming-API's][twitter-streaming-api].</span><span class="sxs-lookup"><span data-stu-id="cec22-138">In this tutorial, you will use the [Twitter streaming APIs][twitter-streaming-api].</span></span> <span data-ttu-id="cec22-139">De specifieke Twitter streaming-API die u wilt gebruiken is [statussen-/ filter][twitter-statuses-filter].</span><span class="sxs-lookup"><span data-stu-id="cec22-139">The specific Twitter streaming API you will use is [statuses/filter][twitter-statuses-filter].</span></span>

> [!NOTE]
> <span data-ttu-id="cec22-140">Een bestand met 10.000 tweets en het Hive-scriptbestand (behandeld in de volgende sectie) zijn geüpload in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="cec22-140">A file containing 10,000 tweets and the Hive script file (covered in the next section) have been uploaded in a public Blob container.</span></span> <span data-ttu-id="cec22-141">Als u wilt de geüploade bestanden gebruiken, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="cec22-141">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="cec22-142">[Tweets gegevens](https://dev.twitter.com/docs/platform-objects/tweets) wordt opgeslagen in de notatie JSON (JavaScript Object)-indeling die een complexe geneste structuur bevat.</span><span class="sxs-lookup"><span data-stu-id="cec22-142">[Tweets data](https://dev.twitter.com/docs/platform-objects/tweets) is stored in the JavaScript Object Notation (JSON) format that contains a complex nested structure.</span></span> <span data-ttu-id="cec22-143">In plaats van een groot aantal regels code schrijven met behulp van een conventionele programmeertaal, kunt u deze geneste structuur in een Hive-tabel transformeren zodat deze kan worden doorzocht door een Structured Query Language (SQL)-taal genaamd HiveQL, zoals.</span><span class="sxs-lookup"><span data-stu-id="cec22-143">Instead of writing many lines of code by using a conventional programming language, you can transform this nested structure into a Hive table, so that it can be queried by a Structured Query Language (SQL)-like language called HiveQL.</span></span>

<span data-ttu-id="cec22-144">Twitter maakt gebruik van OAuth voor geautoriseerde toegang tot de API.</span><span class="sxs-lookup"><span data-stu-id="cec22-144">Twitter uses OAuth to provide authorized access to its API.</span></span> <span data-ttu-id="cec22-145">OAuth is een authenticatieprotocol dat Hiermee gebruikers toepassingen kunnen te handelen namens hen zonder het delen van hun wachtwoord goedkeuren.</span><span class="sxs-lookup"><span data-stu-id="cec22-145">OAuth is an authentication protocol that allows users to approve applications to act on their behalf without sharing their password.</span></span> <span data-ttu-id="cec22-146">Meer informatie kunt vinden op [oauth.net](http://oauth.net/) of in de uitstekende [basisinformatie over OAuth](http://hueniverse.com/oauth/) van Hueniverse.</span><span class="sxs-lookup"><span data-stu-id="cec22-146">More information can be found at [oauth.net](http://oauth.net/) or in the excellent [Beginner's Guide to OAuth](http://hueniverse.com/oauth/) from Hueniverse.</span></span>

<span data-ttu-id="cec22-147">De eerste stap bij het gebruik van OAuth is een nieuwe toepassing maken op de site Developer Twitter.</span><span class="sxs-lookup"><span data-stu-id="cec22-147">The first step to use OAuth is to create a new application on the Twitter Developer site.</span></span>

<span data-ttu-id="cec22-148">**Een Twitter-toepassing maken**</span><span class="sxs-lookup"><span data-stu-id="cec22-148">**To create a Twitter application**</span></span>

1. <span data-ttu-id="cec22-149">Aanmelden bij [https://apps.twitter.com/](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="cec22-149">Sign in to [https://apps.twitter.com/](https://apps.twitter.com/).</span></span> <span data-ttu-id="cec22-150">Klik op de **nu aanmelden** koppelen als u een Twitter-account niet hebt.</span><span class="sxs-lookup"><span data-stu-id="cec22-150">Click the **Sign up now** link if you don't have a Twitter account.</span></span>
2. <span data-ttu-id="cec22-151">Klik op **nieuwe App maken**.</span><span class="sxs-lookup"><span data-stu-id="cec22-151">Click **Create New App**.</span></span>
3. <span data-ttu-id="cec22-152">Voer **naam**, **beschrijving**, **Website**.</span><span class="sxs-lookup"><span data-stu-id="cec22-152">Enter **Name**, **Description**, **Website**.</span></span> <span data-ttu-id="cec22-153">U kunt maken van een URL op voor de **Website** veld.</span><span class="sxs-lookup"><span data-stu-id="cec22-153">You can make up a URL for the **Website** field.</span></span> <span data-ttu-id="cec22-154">De volgende tabel ziet u enkele voorbeeldwaarden te gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cec22-154">The following table shows some sample values to use:</span></span>

   | <span data-ttu-id="cec22-155">Veld</span><span class="sxs-lookup"><span data-stu-id="cec22-155">Field</span></span> | <span data-ttu-id="cec22-156">Waarde</span><span class="sxs-lookup"><span data-stu-id="cec22-156">Value</span></span> |
   | --- | --- |
   |  <span data-ttu-id="cec22-157">Naam</span><span class="sxs-lookup"><span data-stu-id="cec22-157">Name</span></span> |<span data-ttu-id="cec22-158">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="cec22-158">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="cec22-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cec22-159">Description</span></span> |<span data-ttu-id="cec22-160">MyHDInsightApp</span><span class="sxs-lookup"><span data-stu-id="cec22-160">MyHDInsightApp</span></span> |
   |  <span data-ttu-id="cec22-161">Website</span><span class="sxs-lookup"><span data-stu-id="cec22-161">Website</span></span> |<span data-ttu-id="cec22-162">http://www.myhdinsightapp.com</span><span class="sxs-lookup"><span data-stu-id="cec22-162">http://www.myhdinsightapp.com</span></span> |
4. <span data-ttu-id="cec22-163">Controleer **Ja, ik ga akkoord**, en klik vervolgens op **uw Twitter-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="cec22-163">Check **Yes, I agree**, and then click **Create your Twitter application**.</span></span>
5. <span data-ttu-id="cec22-164">Klik op de **machtigingen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cec22-164">Click the **Permissions** tab.</span></span> <span data-ttu-id="cec22-165">Standaard de machtiging is **alleen-lezen**.</span><span class="sxs-lookup"><span data-stu-id="cec22-165">The default permission is **Read only**.</span></span> <span data-ttu-id="cec22-166">Dit is voldoende voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="cec22-166">This is sufficient for this tutorial.</span></span>
6. <span data-ttu-id="cec22-167">Klik op de **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="cec22-167">Click the **Keys and Access Tokens** tab.</span></span>
7. <span data-ttu-id="cec22-168">Klik op **maken van mijn toegangstoken**.</span><span class="sxs-lookup"><span data-stu-id="cec22-168">Click **Create my access token**.</span></span>
8. <span data-ttu-id="cec22-169">Klik op **Test OAuth** in de rechterbovenhoek van de pagina.</span><span class="sxs-lookup"><span data-stu-id="cec22-169">Click **Test OAuth** in the upper-right corner of the page.</span></span>
9. <span data-ttu-id="cec22-170">Noteer **consumentsleutel**, **consumentgeheim**, **toegangstoken**, en **Access token geheim**.</span><span class="sxs-lookup"><span data-stu-id="cec22-170">Write down **consumer key**, **Consumer secret**, **Access token**, and **Access token secret**.</span></span> <span data-ttu-id="cec22-171">Verderop in de zelfstudie moet u de waarden.</span><span class="sxs-lookup"><span data-stu-id="cec22-171">You will need the values later in the tutorial.</span></span>

<span data-ttu-id="cec22-172">In deze zelfstudie gebruikt u Windows PowerShell om de webservice aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cec22-172">In this tutorial, you will use Windows PowerShell to make the web service call.</span></span> <span data-ttu-id="cec22-173">Zie voor een voorbeeld .NET C# [realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment].</span><span class="sxs-lookup"><span data-stu-id="cec22-173">For a .NET C# sample, see [Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment].</span></span> <span data-ttu-id="cec22-174">Het populaire hulpprogramma web service aanroepen is [ *Curl*][curl].</span><span class="sxs-lookup"><span data-stu-id="cec22-174">The other popular tool to make web service calls is [*Curl*][curl].</span></span> <span data-ttu-id="cec22-175">CURL kan worden gedownload vanaf [hier][curl-download].</span><span class="sxs-lookup"><span data-stu-id="cec22-175">Curl can be downloaded from [here][curl-download].</span></span>

> [!NOTE]
> <span data-ttu-id="cec22-176">Als u de curl-opdracht in Windows gebruikt, kunt u dubbele aanhalingstekens in plaats van enkele aanhalingstekens voor de optiewaarden.</span><span class="sxs-lookup"><span data-stu-id="cec22-176">When you use the curl command in Windows, use double quotes instead of single quotes for the option values.</span></span>

<span data-ttu-id="cec22-177">**Tweets ophalen**</span><span class="sxs-lookup"><span data-stu-id="cec22-177">**To get tweets**</span></span>

1. <span data-ttu-id="cec22-178">Open Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="cec22-178">Open the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="cec22-179">(Typ op het Windows 8 startscherm **PowerShell_ISE** en klik vervolgens op **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="cec22-179">(On the Windows 8 Start screen, type **PowerShell_ISE** and then click **Windows PowerShell ISE**.</span></span> <span data-ttu-id="cec22-180">Zie [Start Windows PowerShell in Windows 8 en Windows][powershell-start].)</span><span class="sxs-lookup"><span data-stu-id="cec22-180">See [Start Windows PowerShell on Windows 8 and Windows][powershell-start].)</span></span>
2. <span data-ttu-id="cec22-181">Het volgende script kopiëren naar het deelvenster script:</span><span class="sxs-lookup"><span data-stu-id="cec22-181">Copy the following script into the script pane:</span></span>

    ```powershell
    #region - variables and constants
    $clusterName = "<HDInsightClusterName>" # Enter the HDInsight cluster name

    # Enter the OAuth information for your Twitter application
    $oauth_consumer_key = "<TwitterAppConsumerKey>";
    $oauth_consumer_secret = "<TwitterAppConsumerSecret>";
    $oauth_token = "<TwitterAppAccessToken>";
    $oauth_token_secret = "<TwitterAppAccessTokenSecret>";

    $destBlobName = "tutorials/twitter/data/tweets.txt" # This script saves the tweets into this blob.

    $trackString = "Azure, Cloud, HDInsight" # This script gets the tweets containing these keywords.
    $track = [System.Uri]::EscapeDataString($trackString);
    $lineMax = 10000  # The script will get this number of tweets. It is about 3 minutes every 100 lines.
    #endregion

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
    Login-AzureRmAccount
    #endregion

    #region - Create a block blob object for writing tweets into Blob storage
    Write-Host "Get the default storage account name and Blob container name using the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -Name $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $storageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $containerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $storageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $containerName." -ForegroundColor Yellow

    Write-Host "Define the Azure storage connection string ..." -ForegroundColor Green
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

    #region - Write tweets to Blob storage
    Write-Host "Write to the destination blob ..." -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $destBlob.UploadFromStream($memStream)

    $sReader.close()
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="cec22-182">Stel de eerste vijf tot acht variabelen in het script:</span><span class="sxs-lookup"><span data-stu-id="cec22-182">Set the first five to eight variables in the script:</span></span>

    <span data-ttu-id="cec22-183">Variabele</span><span class="sxs-lookup"><span data-stu-id="cec22-183">Variable</span></span>|<span data-ttu-id="cec22-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cec22-184">Description</span></span>
    ---|---
    <span data-ttu-id="cec22-185">$clusterName</span><span class="sxs-lookup"><span data-stu-id="cec22-185">$clusterName</span></span>|<span data-ttu-id="cec22-186">Dit is de naam van het HDInsight-cluster waar u de toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-186">This is the name of the HDInsight cluster where you want to run the application.</span></span>
    <span data-ttu-id="cec22-187">$oauth_consumer_key</span><span class="sxs-lookup"><span data-stu-id="cec22-187">$oauth_consumer_key</span></span>|<span data-ttu-id="cec22-188">Dit is de toepassing Twitter **consumentsleutel** u opgeschreven eerder wanneer u de Twitter-toepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cec22-188">This is the Twitter application **consumer key** you wrote down earlier when you created the Twitter application.</span></span>
    <span data-ttu-id="cec22-189">$oauth_consumer_secret</span><span class="sxs-lookup"><span data-stu-id="cec22-189">$oauth_consumer_secret</span></span>|<span data-ttu-id="cec22-190">Dit is de toepassing Twitter **consumentgeheim** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="cec22-190">This is the Twitter application **consumer secret** you wrote down earlier.</span></span>
    <span data-ttu-id="cec22-191">$oauth_token</span><span class="sxs-lookup"><span data-stu-id="cec22-191">$oauth_token</span></span>|<span data-ttu-id="cec22-192">Dit is de toepassing Twitter **toegangstoken** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="cec22-192">This is the Twitter application **access token** you wrote down earlier.</span></span>
    <span data-ttu-id="cec22-193">$oauth_token_secret</span><span class="sxs-lookup"><span data-stu-id="cec22-193">$oauth_token_secret</span></span>|<span data-ttu-id="cec22-194">Dit is de toepassing Twitter **access token geheim** u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="cec22-194">This is the Twitter application **access token secret** you wrote down earlier.</span></span>
    <span data-ttu-id="cec22-195">$destBlobName</span><span class="sxs-lookup"><span data-stu-id="cec22-195">$destBlobName</span></span>|<span data-ttu-id="cec22-196">Dit is de uitvoer-blob-naam.</span><span class="sxs-lookup"><span data-stu-id="cec22-196">This is the output blob name.</span></span> <span data-ttu-id="cec22-197">De standaardwaarde is **tutorials/twitter/data/tweets.txt**.</span><span class="sxs-lookup"><span data-stu-id="cec22-197">The default value is **tutorials/twitter/data/tweets.txt**.</span></span> <span data-ttu-id="cec22-198">Als u de standaardwaarde wijzigt, moet u de Windows PowerShell-scripts worden dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="cec22-198">If you change the default value, you will need to update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="cec22-199">$trackString</span><span class="sxs-lookup"><span data-stu-id="cec22-199">$trackString</span></span>|<span data-ttu-id="cec22-200">De webservice wordt tweets die betrekking hebben op deze trefwoorden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="cec22-200">The web service will return tweets related to these keywords.</span></span> <span data-ttu-id="cec22-201">De standaardwaarde is **Azure, Cloud, HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="cec22-201">The default value is **Azure, Cloud, HDInsight**.</span></span> <span data-ttu-id="cec22-202">Als u de standaardwaarde wijzigt, wordt u de Windows PowerShell-scripts dienovereenkomstig bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="cec22-202">If you change the default value, you will update the Windows PowerShell scripts accordingly.</span></span>
    <span data-ttu-id="cec22-203">$lineMax</span><span class="sxs-lookup"><span data-stu-id="cec22-203">$lineMax</span></span>|<span data-ttu-id="cec22-204">De waarde bepaalt hoeveel tweets het script wordt gelezen.</span><span class="sxs-lookup"><span data-stu-id="cec22-204">The value determines how many tweets the script will read.</span></span> <span data-ttu-id="cec22-205">Het duurt ongeveer drie minuten 100 tweets lezen.</span><span class="sxs-lookup"><span data-stu-id="cec22-205">It takes about three minutes to read 100 tweets.</span></span> <span data-ttu-id="cec22-206">U kunt een groter aantal instellen, maar duurt het meer tijd om te downloaden.</span><span class="sxs-lookup"><span data-stu-id="cec22-206">You can set a larger number, but it will take more time to download.</span></span>

1. <span data-ttu-id="cec22-207">Druk op **F5** om het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-207">Press **F5** to run the script.</span></span> <span data-ttu-id="cec22-208">Als u problemen als tijdelijke oplossing ondervindt alle regels selecteren en druk vervolgens op **F8**.</span><span class="sxs-lookup"><span data-stu-id="cec22-208">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
2. <span data-ttu-id="cec22-209">U ziet 'Voltooi!'</span><span class="sxs-lookup"><span data-stu-id="cec22-209">You shall see "Complete!"</span></span> <span data-ttu-id="cec22-210">aan het einde van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="cec22-210">at the end of the output.</span></span> <span data-ttu-id="cec22-211">Eventuele foutberichten wordt rood weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cec22-211">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="cec22-212">U kunt het uitvoerbestand controleren als de validatieprocedure **/tutorials/twitter/data/tweets.txt**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cec22-212">As a validation procedure, you can check the output file, **/tutorials/twitter/data/tweets.txt**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="cec22-213">Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="cec22-213">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="create-hiveql-script"></a><span data-ttu-id="cec22-214">HiveQL-script maken</span><span class="sxs-lookup"><span data-stu-id="cec22-214">Create HiveQL script</span></span>
<span data-ttu-id="cec22-215">Met Azure PowerShell, kunt u meerdere HiveQL-instructies een tegelijk uitvoeren of de instructie van HiveQL in een scriptbestand van het pakket.</span><span class="sxs-lookup"><span data-stu-id="cec22-215">Using Azure PowerShell, you can run multiple HiveQL statements one at a time, or package the HiveQL statement into a script file.</span></span> <span data-ttu-id="cec22-216">In deze zelfstudie maakt u een HiveQL-script.</span><span class="sxs-lookup"><span data-stu-id="cec22-216">In this tutorial, you will create a HiveQL script.</span></span> <span data-ttu-id="cec22-217">Het scriptbestand moet worden geüpload naar Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="cec22-217">The script file must be uploaded to Azure Blob storage.</span></span> <span data-ttu-id="cec22-218">In de volgende sectie stelt uitvoeren u het scriptbestand met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cec22-218">In the next section, you will run the script file by using Azure PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="cec22-219">Het Hive-scriptbestand en een bestand met 10.000 tweets zijn geüpload in een openbare Blob-container.</span><span class="sxs-lookup"><span data-stu-id="cec22-219">The Hive script file and a file containing 10,000 tweets have been uploaded in a public Blob container.</span></span> <span data-ttu-id="cec22-220">Als u wilt de geüploade bestanden gebruiken, kunt u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="cec22-220">You can skip this section if you want to use the uploaded files.</span></span>

<span data-ttu-id="cec22-221">Het HiveQL-script wordt het volgende doen:</span><span class="sxs-lookup"><span data-stu-id="cec22-221">The HiveQL script will perform the following:</span></span>

1. <span data-ttu-id="cec22-222">**Verwijderen van de tabel tweets_raw** als de tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="cec22-222">**Drop the tweets_raw table** in case the table already exists.</span></span>
2. <span data-ttu-id="cec22-223">**De tweets_raw Hive-tabel maken**.</span><span class="sxs-lookup"><span data-stu-id="cec22-223">**Create the tweets_raw Hive table**.</span></span> <span data-ttu-id="cec22-224">Deze tijdelijke gestructureerde Hive-tabel bevat de gegevens voor verdere uitpakken, transformeren en laden (ETL) verwerking.</span><span class="sxs-lookup"><span data-stu-id="cec22-224">This temporary Hive structured table holds the data for further extract, transform, and load (ETL) processing.</span></span> <span data-ttu-id="cec22-225">Zie voor informatie over partities, [Hive-zelfstudie][apache-hive-tutorial].</span><span class="sxs-lookup"><span data-stu-id="cec22-225">For information on partitions, see [Hive tutorial][apache-hive-tutorial].</span></span>
3. <span data-ttu-id="cec22-226">**Gegevens laden** van de bronmap, /tutorials/twitter/data.</span><span class="sxs-lookup"><span data-stu-id="cec22-226">**Load data** from the source folder, /tutorials/twitter/data.</span></span> <span data-ttu-id="cec22-227">De gegevensset grote tweets in geneste JSON-indeling heeft nu is omgezet in de structuur van een tijdelijke Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="cec22-227">The large tweets dataset in nested JSON format has now been transformed into a temporary Hive table structure.</span></span>
4. <span data-ttu-id="cec22-228">**Verwijderen van de tabel tweets** als de tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="cec22-228">**Drop the tweets table** in case the table already exists.</span></span>
5. <span data-ttu-id="cec22-229">**Maken van de tabel tweets**.</span><span class="sxs-lookup"><span data-stu-id="cec22-229">**Create the tweets table**.</span></span> <span data-ttu-id="cec22-230">Voordat u kunt een query op basis van de gegevensset tweets met Hive, moet u een ander ETL-proces worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cec22-230">Before you can query against the tweets dataset by using Hive, you need to run another ETL process.</span></span> <span data-ttu-id="cec22-231">Dit proces ETL definieert een meer gedetailleerde tabelschema voor de gegevens die u hebt opgeslagen in de tabel 'twitter_raw'.</span><span class="sxs-lookup"><span data-stu-id="cec22-231">This ETL process defines a more detailed table schema for the data that you have stored in the "twitter_raw" table.</span></span>
6. <span data-ttu-id="cec22-232">**Overschrijven tabel invoegen**.</span><span class="sxs-lookup"><span data-stu-id="cec22-232">**Insert overwrite table**.</span></span> <span data-ttu-id="cec22-233">Dit complexe Hive-script wordt een reeks lang MapReduce-taken starten door het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="cec22-233">This complex Hive script will kick off a set of long MapReduce jobs by the Hadoop cluster.</span></span> <span data-ttu-id="cec22-234">Dit kan ongeveer 10 minuten duren, afhankelijk van uw gegevensset en de grootte van het cluster.</span><span class="sxs-lookup"><span data-stu-id="cec22-234">Depending on your dataset and the size of your cluster, this could take about 10 minutes.</span></span>
7. <span data-ttu-id="cec22-235">**INSERT map overschrijven**.</span><span class="sxs-lookup"><span data-stu-id="cec22-235">**Insert overwrite directory**.</span></span> <span data-ttu-id="cec22-236">Een query uitvoert en de uitvoer van de gegevensset naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="cec22-236">Run a query and output the dataset to a file.</span></span> <span data-ttu-id="cec22-237">Deze query retourneert een lijst met Twitter gebruikers afzender meeste tweets of het woord 'Azure'.</span><span class="sxs-lookup"><span data-stu-id="cec22-237">This query will return a list of Twitter users who sent most tweets that contained the word "Azure".</span></span>

<span data-ttu-id="cec22-238">**Een Hive-script maken en uploaden naar Azure**</span><span class="sxs-lookup"><span data-stu-id="cec22-238">**To create a Hive script and upload it to Azure**</span></span>

1. <span data-ttu-id="cec22-239">Open Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="cec22-239">Open Windows PowerShell ISE.</span></span>
2. <span data-ttu-id="cec22-240">Het volgende script kopiëren naar het deelvenster script:</span><span class="sxs-lookup"><span data-stu-id="cec22-240">Copy the following script into the script pane:</span></span>

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

    #region - Connect to Azure subscription
    Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }

    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #endregion

    #region - Create a block blob object for writing the Hive script file
    Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
    $myCluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $myCluster.ResourceGroup
    $defaultStorageAccountName = $myCluster.DefaultStorageAccount.Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $myCluster.DefaultStorageContainer
    Write-Host "`tThe storage account name is $defaultStorageAccountName." -ForegroundColor Yellow
    Write-Host "`tThe blob container name is $defaultBlobContainerName." -ForegroundColor Yellow

    Write-Host "Define the connection string ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=$defaultStorageAccountName;AccountKey=$defaultStorageAccountKey"

    Write-Host "Create block blob objects referencing the hql script file" -ForegroundColor Green
    $storageAccount = [Microsoft.WindowsAzure.Storage.CloudStorageAccount]::Parse($storageConnectionString)
    $storageClient = $storageAccount.CreateCloudBlobClient();
    $storageContainer = $storageClient.GetContainerReference($defaultBlobContainerName)
    $hqlScriptBlob = $storageContainer.GetBlockBlobReference($hqlScriptFile)

    Write-Host "Define a MemoryStream and a StreamWriter for writing ... " -ForegroundColor Green
    $memStream = New-Object System.IO.MemoryStream
    $writeStream = New-Object System.IO.StreamWriter $memStream
    $writeStream.Writeline($hqlStatements)
    #endregion

    #region - Write the Hive script file to Blob storage
    Write-Host "Write to the destination blob ... " -ForegroundColor Green
    $writeStream.Flush()
    $memStream.Seek(0, "Begin")
    $hqlScriptBlob.UploadFromStream($memStream)
    #endregion

    Write-Host "Completed!" -ForegroundColor Green
    ```

3. <span data-ttu-id="cec22-241">Stel de eerste twee variabelen in het script:</span><span class="sxs-lookup"><span data-stu-id="cec22-241">Set the first two variables in the script:</span></span>

   | <span data-ttu-id="cec22-242">Variabele</span><span class="sxs-lookup"><span data-stu-id="cec22-242">Variable</span></span> | <span data-ttu-id="cec22-243">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cec22-243">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="cec22-244">$clusterName</span><span class="sxs-lookup"><span data-stu-id="cec22-244">$clusterName</span></span> |<span data-ttu-id="cec22-245">Voer de naam van het HDInsight-cluster waar u de toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-245">Enter the HDInsight cluster name where you want to run the application.</span></span> |
   |  <span data-ttu-id="cec22-246">$subscriptionID</span><span class="sxs-lookup"><span data-stu-id="cec22-246">$subscriptionID</span></span> |<span data-ttu-id="cec22-247">Voer uw Azure-abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="cec22-247">Enter your Azure subscription ID.</span></span> |
   |  <span data-ttu-id="cec22-248">$sourceDataPath</span><span class="sxs-lookup"><span data-stu-id="cec22-248">$sourceDataPath</span></span> |<span data-ttu-id="cec22-249">De Azure Blob storage locatie waar u het Hive-query's de gegevens van leest.</span><span class="sxs-lookup"><span data-stu-id="cec22-249">The Azure Blob storage location where the Hive queries will read the data from.</span></span> <span data-ttu-id="cec22-250">U hoeft niet te wijzigen van deze variabele.</span><span class="sxs-lookup"><span data-stu-id="cec22-250">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="cec22-251">$outputPath</span><span class="sxs-lookup"><span data-stu-id="cec22-251">$outputPath</span></span> |<span data-ttu-id="cec22-252">De Azure Blob storage locatie waar de Hive-query wordt de resultaten.</span><span class="sxs-lookup"><span data-stu-id="cec22-252">The Azure Blob storage location where the Hive queries will output the results.</span></span> <span data-ttu-id="cec22-253">U hoeft niet te wijzigen van deze variabele.</span><span class="sxs-lookup"><span data-stu-id="cec22-253">You don't need to change this variable.</span></span> |
   |  <span data-ttu-id="cec22-254">$hqlScriptFile</span><span class="sxs-lookup"><span data-stu-id="cec22-254">$hqlScriptFile</span></span> |<span data-ttu-id="cec22-255">De locatie en de bestandsnaam van het scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="cec22-255">The location and the file name of the HiveQL script file.</span></span> <span data-ttu-id="cec22-256">U hoeft niet te wijzigen van deze variabele.</span><span class="sxs-lookup"><span data-stu-id="cec22-256">You don't need to change this variable.</span></span> |
4. <span data-ttu-id="cec22-257">Druk op **F5** om het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-257">Press **F5** to run the script.</span></span> <span data-ttu-id="cec22-258">Als u problemen als tijdelijke oplossing ondervindt alle regels selecteren en druk vervolgens op **F8**.</span><span class="sxs-lookup"><span data-stu-id="cec22-258">If you run into problems, as a workaround, select all the lines, and then press **F8**.</span></span>
5. <span data-ttu-id="cec22-259">U ziet 'Voltooi!'</span><span class="sxs-lookup"><span data-stu-id="cec22-259">You shall see "Complete!"</span></span> <span data-ttu-id="cec22-260">aan het einde van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="cec22-260">at the end of the output.</span></span> <span data-ttu-id="cec22-261">Eventuele foutberichten wordt rood weergegeven.</span><span class="sxs-lookup"><span data-stu-id="cec22-261">Any error messages will be displayed in red.</span></span>

<span data-ttu-id="cec22-262">U kunt het uitvoerbestand controleren als de validatieprocedure **/tutorials/twitter/twitter.hql**, op de Azure Blob-opslag met behulp van een Azure storage explorer of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cec22-262">As a validation procedure, you can check the output file, **/tutorials/twitter/twitter.hql**, on your Azure Blob storage by using an Azure storage explorer or Azure PowerShell.</span></span> <span data-ttu-id="cec22-263">Zie voor een Windows PowerShell-voorbeeldscript voor het weergeven van bestanden, [gebruik Blob storage met HDInsight][hdinsight-storage-powershell].</span><span class="sxs-lookup"><span data-stu-id="cec22-263">For a sample Windows PowerShell script for listing files, see [Use Blob storage with HDInsight][hdinsight-storage-powershell].</span></span>

## <a name="process-twitter-data-by-using-hive"></a><span data-ttu-id="cec22-264">Twitter-gegevens verwerken met behulp van Hive</span><span class="sxs-lookup"><span data-stu-id="cec22-264">Process Twitter data by using Hive</span></span>
<span data-ttu-id="cec22-265">U hebt al het werk voorbereiding.</span><span class="sxs-lookup"><span data-stu-id="cec22-265">You have finished all the preparation work.</span></span> <span data-ttu-id="cec22-266">U kunt nu het Hive-script aanroepen en de resultaten controleren.</span><span class="sxs-lookup"><span data-stu-id="cec22-266">Now, you can invoke the Hive script and check the results.</span></span>

### <a name="submit-a-hive-job"></a><span data-ttu-id="cec22-267">Verzenden van een Hive-taak</span><span class="sxs-lookup"><span data-stu-id="cec22-267">Submit a Hive job</span></span>
<span data-ttu-id="cec22-268">Gebruik de volgende Windows PowerShell-script de Hive-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="cec22-268">Use the following Windows PowerShell script to run the Hive script.</span></span> <span data-ttu-id="cec22-269">U moet de eerste variabele ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cec22-269">You will need to set the first variable.</span></span>

> [!NOTE]
> <span data-ttu-id="cec22-270">Instellen als u de tweets en het HiveQL-script dat u hebt geüpload in de laatste twee secties, $hqlScriptFile op ' / tutorials/twitter/twitter.hql '.</span><span class="sxs-lookup"><span data-stu-id="cec22-270">To use the tweets and the HiveQL script you uploaded in the last two sections, set $hqlScriptFile to "/tutorials/twitter/twitter.hql".</span></span> <span data-ttu-id="cec22-271">Ingesteld voor het gebruik van de waarden die voor u zijn geüpload naar een openbare blob $hqlScriptFile op 'wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql'.</span><span class="sxs-lookup"><span data-stu-id="cec22-271">To use the ones that have been uploaded to a public blob for you, set $hqlScriptFile to "wasb://twittertrend@hditutorialdata.blob.core.windows.net/twitter.hql".</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"
$httpUserName = "admin"
$httpUserPassword = "<HDInsight Cluster HTTP User Password>"

#use one of the following
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

# Create the HDInsight cluster
$pw = ConvertTo-SecureString -String $httpUserPassword -AsPlainText -Force
$httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

Use-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName -HttpCredential $httpCredential
$response = Invoke-AzureRmHDInsightHiveJob -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -DefaultContainer $defaultBlobContainerName -file $hqlScriptFile -StatusFolder $statusFolder #-OutVariable $outVariable

Write-Host "Display the standard error log ... " -ForegroundColor Green
$jobID = ($response | Select-String job_ | Select-Object -First 1) -replace ‘\s*$’ -replace ‘.*\s’
Get-AzureRmHDInsightJobOutput -ClusterName $clusterName -JobId $jobID -DefaultContainer $defaultBlobContainerName -DefaultStorageAccountName $defaultStorageAccountName -DefaultStorageAccountKey $defaultStorageAccountKey -HttpCredential $httpCredential
#endregion
```

### <a name="check-the-results"></a><span data-ttu-id="cec22-272">De resultaten controleren</span><span class="sxs-lookup"><span data-stu-id="cec22-272">Check the results</span></span>
<span data-ttu-id="cec22-273">De volgende Windows PowerShell-script gebruiken om te controleren van de uitvoer van de Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="cec22-273">Use the following Windows PowerShell script to check the Hive job output.</span></span> <span data-ttu-id="cec22-274">U moet de eerste twee variabelen worden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="cec22-274">You will need to set the first two variables.</span></span>

```powershell
#region variables and constants
$clusterName = "<Existing Azure HDInsight Cluster Name>"

$blob = "tutorials/twitter/output/000000_0" # The name of the blob to be downloaded.
#endregion

#region - Create an Azure storage context object
Write-Host "Get the default storage account name and container name based on the cluster name ..." -ForegroundColor Green
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
Write-Host "Download the blob ..." -ForegroundColor Green
cd $HOME
Get-AzureStorageBlobContent -Container $defaultBlobContainerName -Blob $blob -Context $storageContext -Force

Write-Host "Display the output ..." -ForegroundColor Green
Write-Host "==================================" -ForegroundColor Green
cat "./$blob"
Write-Host "==================================" -ForegroundColor Green
#end region
```

> [!NOTE]
> De Hive-tabel gebruikt \001 als het veldscheidingsteken. <span data-ttu-id="cec22-276">Het scheidingsteken is niet zichtbaar in de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="cec22-276">The delimiter is not visible in the output.</span></span>

<span data-ttu-id="cec22-277">Nadat de resultaten van de analyse in Azure Blob-opslag zijn geplaatst, kunt u de gegevens exporteren naar een Azure SQL database/SQL-server, de gegevens exporteren naar Excel via Power Query of verbinding maken met uw toepassing uit om de gegevens met behulp van het Hive ODBC-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="cec22-277">After the analysis results have been placed in Azure Blob storage, you can export the data to an Azure SQL database/SQL server, export the data to Excel by using Power Query, or connect your application to the data by using the Hive ODBC Driver.</span></span> <span data-ttu-id="cec22-278">Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop], [vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data], [Excel verbinding naar HDInsight met Power Query][hdinsight-power-query], en [Excel verbinding naar HDInsight met het stuurprogramma Microsoft Hive ODBC][hdinsight-hive-odbc].</span><span class="sxs-lookup"><span data-stu-id="cec22-278">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop], [Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data], [Connect Excel to HDInsight with Power Query][hdinsight-power-query], and [Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc].</span></span>

## <a name="next-steps"></a><span data-ttu-id="cec22-279">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cec22-279">Next steps</span></span>
<span data-ttu-id="cec22-280">In deze zelfstudie hebben we gezien hoe u een niet-gestructureerde JSON-gegevensset transformeren naar een gestructureerde Hive-tabel om te zoeken, verkennen en analyseren van gegevens van Twitter met behulp van HDInsight op Azure.</span><span class="sxs-lookup"><span data-stu-id="cec22-280">In this tutorial we have seen how to transform an unstructured JSON dataset into a structured Hive table to query, explore, and analyze data from Twitter by using HDInsight on Azure.</span></span> <span data-ttu-id="cec22-281">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="cec22-281">To learn more, see:</span></span>

* <span data-ttu-id="cec22-282">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="cec22-282">[Get started with HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="cec22-283">[Realtime Twitter-gevoel met HBase in HDInsight analyseren][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="cec22-283">[Analyze real-time Twitter sentiment with HBase in HDInsight][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="cec22-284">[Vertraging vluchtgegevens met HDInsight analyseren][hdinsight-analyze-flight-delay-data]</span><span class="sxs-lookup"><span data-stu-id="cec22-284">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-delay-data]</span></span>
* <span data-ttu-id="cec22-285">[Excel verbinden met HDInsight met Power Query][hdinsight-power-query]</span><span class="sxs-lookup"><span data-stu-id="cec22-285">[Connect Excel to HDInsight with Power Query][hdinsight-power-query]</span></span>
* <span data-ttu-id="cec22-286">[Excel verbinden met HDInsight met het Microsoft Hive ODBC-stuurprogramma][hdinsight-hive-odbc]</span><span class="sxs-lookup"><span data-stu-id="cec22-286">[Connect Excel to HDInsight with the Microsoft Hive ODBC Driver][hdinsight-hive-odbc]</span></span>
* <span data-ttu-id="cec22-287">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="cec22-287">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

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
