---
title: Azure Data Lake Analytics met Azure PowerShell aaaManage | Microsoft Docs
description: 'Meer informatie over hoe toomanage Data Lake Analytics-accounts, gegevensbronnen, taken, en catalogusitems. '
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/23/2017
ms.author: mahi
ms.openlocfilehash: 5954f0efb7d5a9778727edfccae83aec046343bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="3b859-103">Azure Data Lake Analytics beheren met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b859-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="3b859-104">Informatie over hoe toomanage Azure Data Lake Analytics-accounts, gegevensbronnen, taken en catalogusitems met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b859-104">Learn how toomanage Azure Data Lake Analytics accounts, data sources, jobs, and catalog items using Azure PowerShell.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="3b859-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3b859-105">Prerequisites</span></span>

<span data-ttu-id="3b859-106">Wanneer u een Data Lake Analytics-account maakt, moet u tooknow:</span><span class="sxs-lookup"><span data-stu-id="3b859-106">When creating a Data Lake Analytics account, you need tooknow:</span></span>

* <span data-ttu-id="3b859-107">**Abonnements-ID**: hello Azure-abonnement-ID die uw Data Lake Analytics-account zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="3b859-107">**Subscription ID**: hello Azure subscription ID under which your Data Lake Analytics account resides.</span></span>
* <span data-ttu-id="3b859-108">**Resourcegroep**: Hallo-naam van hello Azure-resourcegroep met uw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-108">**Resource group**: hello name of hello Azure resource group that contains your Data Lake Analytics account.</span></span>
* <span data-ttu-id="3b859-109">**Data Lake Analytics-accountnaam**: Hallo account naam mag alleen kleine letters en cijfers.</span><span class="sxs-lookup"><span data-stu-id="3b859-109">**Data Lake Analytics account name**: hello account name must only contain lowercase letters and numbers.</span></span>
* <span data-ttu-id="3b859-110">**Data Lake Store-standaardaccount**: elk Data Lake Store Analytics-account heeft een Data Lake Store-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="3b859-110">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span> <span data-ttu-id="3b859-111">Deze accounts moeten zich in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="3b859-111">These accounts must be in hello same location.</span></span>
* <span data-ttu-id="3b859-112">**Locatie**: Hallo-locatie van uw Data Lake Analytics-account, zoals "VS-Oost 2" of andere locaties ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3b859-112">**Location**: hello location of your Data Lake Analytics account, such as "East US 2" or other supported locations.</span></span> <span data-ttu-id="3b859-113">Ondersteunde locaties kunnen worden weergegeven op onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3b859-113">Supported locations can be seen on our [pricing page](https://azure.microsoft.com/pricing/details/data-lake-analytics/).</span></span>

<span data-ttu-id="3b859-114">Deze variabelen toostore deze informatie Hallo PowerShell codefragmenten in deze zelfstudie gebruiken</span><span class="sxs-lookup"><span data-stu-id="3b859-114">hello PowerShell snippets in this tutorial use these variables toostore this information</span></span>

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a><span data-ttu-id="3b859-115">Aanmelden</span><span class="sxs-lookup"><span data-stu-id="3b859-115">Log in</span></span>

<span data-ttu-id="3b859-116">Meld u aan met een abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="3b859-116">Log in using a subscription id.</span></span>

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

<span data-ttu-id="3b859-117">Meld u aan met de naam van een abonnement.</span><span class="sxs-lookup"><span data-stu-id="3b859-117">Log in using a subscription name.</span></span>

```
Login-AzureRmAccount -SubscriptionName $subname 
```

<span data-ttu-id="3b859-118">Hallo `Login-AzureRmAccount` cmdlet altijd om referenties gevraagd.</span><span class="sxs-lookup"><span data-stu-id="3b859-118">hello `Login-AzureRmAccount` cmdlet  always prompts for credentials.</span></span> <span data-ttu-id="3b859-119">U kunt voorkomen dat u met behulp van de volgende cmdlets Hallo wordt gevraagd:</span><span class="sxs-lookup"><span data-stu-id="3b859-119">You can avoid being prompted by using hello following cmdlets:</span></span>

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a><span data-ttu-id="3b859-120">Accounts beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-120">Managing accounts</span></span>

### <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="3b859-121">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="3b859-121">Create a Data Lake Analytics account</span></span>

<span data-ttu-id="3b859-122">Als u nog geen hebt een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, een maken.</span><span class="sxs-lookup"><span data-stu-id="3b859-122">If you don't already have a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, create one.</span></span> 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

<span data-ttu-id="3b859-123">Elke Data Lake Analytics-account vereist een Data Lake Store-standaardaccount dat wordt gebruikt voor het opslaan van logboeken.</span><span class="sxs-lookup"><span data-stu-id="3b859-123">Every Data Lake Analytics account requires a default Data Lake Store account that it uses for storing logs.</span></span> <span data-ttu-id="3b859-124">U kunt een bestaand account gebruiken of een account maken.</span><span class="sxs-lookup"><span data-stu-id="3b859-124">You can reuse an existing account or create an account.</span></span> 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

<span data-ttu-id="3b859-125">Wanneer een resourcegroep en Data Lake Store-account beschikbaar zijn, kunt u een Data Lake Analytics-account maken.</span><span class="sxs-lookup"><span data-stu-id="3b859-125">Once a Resource Group and Data Lake Store account is available, create a Data Lake Analytics account.</span></span>

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a><span data-ttu-id="3b859-126">Informatie ophalen over een account</span><span class="sxs-lookup"><span data-stu-id="3b859-126">Get information about an account</span></span>

<span data-ttu-id="3b859-127">Informatie ophalen over een account.</span><span class="sxs-lookup"><span data-stu-id="3b859-127">Get details about an account.</span></span>

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="3b859-128">Controleren op Hallo bestaan van een specifieke Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-128">Check hello existence of a specific Data Lake Analytics account.</span></span> <span data-ttu-id="3b859-129">Hallo cmdlet retourneert een `True` of `False`.</span><span class="sxs-lookup"><span data-stu-id="3b859-129">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

<span data-ttu-id="3b859-130">Controleren op Hallo bestaan van een specifieke Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-130">Check hello existence of a specific Data Lake Store account.</span></span> <span data-ttu-id="3b859-131">Hallo cmdlet retourneert een `True` of `False`.</span><span class="sxs-lookup"><span data-stu-id="3b859-131">hello cmdlet returns either `True` or `False`.</span></span>

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a><span data-ttu-id="3b859-132">Aanbieding-accounts</span><span class="sxs-lookup"><span data-stu-id="3b859-132">Listing accounts</span></span>

<span data-ttu-id="3b859-133">Lijst met Data Lake Analytics-accounts binnen het huidige abonnement Hallo.</span><span class="sxs-lookup"><span data-stu-id="3b859-133">List Data Lake Analytics accounts within hello current subscription.</span></span>

```powershell
Get-AdlAnalyticsAccount
```

<span data-ttu-id="3b859-134">Lijst met Data Lake Analytics-accounts binnen een specifieke resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3b859-134">List Data Lake Analytics accounts within a specific resource group.</span></span>

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a><span data-ttu-id="3b859-135">Firewall-regels beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-135">Managing firewall rules</span></span>

<span data-ttu-id="3b859-136">Lijst van firewallregels.</span><span class="sxs-lookup"><span data-stu-id="3b859-136">List firewall rules.</span></span>

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

<span data-ttu-id="3b859-137">Een firewallregel toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3b859-137">Add a firewall rule.</span></span>

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="3b859-138">Een firewallregel wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3b859-138">Change a firewall rule.</span></span>

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

<span data-ttu-id="3b859-139">Een firewallregel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="3b859-139">Remove a firewall rule.</span></span>

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



<span data-ttu-id="3b859-140">Azure-IP-adressen toestaan.</span><span class="sxs-lookup"><span data-stu-id="3b859-140">Allow Azure IP addresses.</span></span>

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a><span data-ttu-id="3b859-141">Gegevensbronnen beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-141">Managing data sources</span></span>
<span data-ttu-id="3b859-142">Azure Data Lake Analytics ondersteunt momenteel Hallo gegevensbronnen te volgen:</span><span class="sxs-lookup"><span data-stu-id="3b859-142">Azure Data Lake Analytics currently supports hello following data sources:</span></span>

* [<span data-ttu-id="3b859-143">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3b859-143">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="3b859-144">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3b859-144">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="3b859-145">Wanneer u een Analytics-account maakt, moet u een Data Lake Store-account toobe Hallo standaardgegevensbron toewijzen.</span><span class="sxs-lookup"><span data-stu-id="3b859-145">When you create an Analytics account, you must designate a Data Lake Store account toobe hello default data source.</span></span> <span data-ttu-id="3b859-146">Hallo Data Lake Store-standaardaccount wordt gebruikt toostore taak metagegevens en taak controlelogboeken.</span><span class="sxs-lookup"><span data-stu-id="3b859-146">hello default Data Lake Store account is used toostore job metadata and job audit logs.</span></span> <span data-ttu-id="3b859-147">Nadat u een Data Lake Analytics-account hebt gemaakt, kunt u extra Data Lake Store-accounts en/of de Storage-accounts toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3b859-147">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Storage accounts.</span></span> 

### <a name="find-hello-default-data-lake-store-account"></a><span data-ttu-id="3b859-148">Hallo default Data Lake Store-account vinden</span><span class="sxs-lookup"><span data-stu-id="3b859-148">Find hello default Data Lake Store account</span></span>

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

<span data-ttu-id="3b859-149">U kunt Hallo standaard Data Lake Store-account vinden door de lijst van gegevensbronnen Hallo filteren op Hallo `IsDefault` eigenschap:</span><span class="sxs-lookup"><span data-stu-id="3b859-149">You can find hello default Data Lake Store account by filtering hello list of datasources by hello `IsDefault` property:</span></span>

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a><span data-ttu-id="3b859-150">Een gegevensbron toevoegen</span><span class="sxs-lookup"><span data-stu-id="3b859-150">Add a data source</span></span>

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a><span data-ttu-id="3b859-151">Lijst met gegevensbronnen</span><span class="sxs-lookup"><span data-stu-id="3b859-151">List data sources</span></span>

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="3b859-152">U-SQL-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="3b859-152">Submit U-SQL jobs</span></span>

### <a name="submit-a-string-as-a-u-sql-script"></a><span data-ttu-id="3b859-153">Verzenden van een tekenreeks als een U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="3b859-153">Submit a string as a U-SQL script</span></span>

```powershell
$script = @"
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"@

$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 

Submit-AdlJob -AccountName $adla -Script $script -Name "Demo"
```


### <a name="submit-a-file-as-a-u-sql-script"></a><span data-ttu-id="3b859-154">Een bestand verzenden als een U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="3b859-154">Submit a file as a U-SQL script</span></span>

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a><span data-ttu-id="3b859-155">Lijst met taken in een account</span><span class="sxs-lookup"><span data-stu-id="3b859-155">List jobs in an account</span></span>

### <a name="list-all-hello-jobs-in-hello-account"></a><span data-ttu-id="3b859-156">Lijst van alle Hallo jobs in Hallo-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-156">List all hello jobs in hello account.</span></span> 

<span data-ttu-id="3b859-157">Hallo uitvoer bevat Hallo actieve taken en de taken die u onlangs hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="3b859-157">hello output includes hello currently running jobs and those jobs that have recently completed.</span></span>

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a><span data-ttu-id="3b859-158">Lijst van een bepaald aantal taken</span><span class="sxs-lookup"><span data-stu-id="3b859-158">List a specific number of jobs</span></span>

<span data-ttu-id="3b859-159">Standaard Hallo lijst met taken is gesorteerd op tijd te verzenden.</span><span class="sxs-lookup"><span data-stu-id="3b859-159">By default hello list of jobs is sorted on submit time.</span></span> <span data-ttu-id="3b859-160">Dus Hallo meest recent verzonden taken eerste worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3b859-160">So hello most recently submitted jobs appear first.</span></span> <span data-ttu-id="3b859-161">Hallo ADLA account onthoudt taken gedurende 180 dagen, maar alleen Hallo eerste 500 Hallo Ge AdlJob cmdlet door standaard retourneert.</span><span class="sxs-lookup"><span data-stu-id="3b859-161">By default, hello ADLA account remembers jobs for 180 days, but hello Ge-AdlJob  cmdlet by default returns only hello first 500.</span></span> <span data-ttu-id="3b859-162">Gebruik - bovenste parameter toolist een bepaald aantal taken.</span><span class="sxs-lookup"><span data-stu-id="3b859-162">Use -Top parameter toolist a specific number of jobs.</span></span>

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a><span data-ttu-id="3b859-163">Lijst met taken op basis van het Hallo-waarde van taakeigenschap</span><span class="sxs-lookup"><span data-stu-id="3b859-163">List jobs based on hello value of job property</span></span>

<span data-ttu-id="3b859-164">Met behulp van Hallo `-State` parameter.</span><span class="sxs-lookup"><span data-stu-id="3b859-164">Using hello `-State` parameter.</span></span> <span data-ttu-id="3b859-165">U kunt deze waarden combineren:</span><span class="sxs-lookup"><span data-stu-id="3b859-165">You can combine any of these values:</span></span>

* `Accepted`
* `Compiling`
* `Ended`
* `New`
* `Paused`
* `Queued`
* `Running`
* `Scheduling`
* `Start`

```powershell
# List hello running jobs
Get-AdlJob -Account $adla -State Running

# List hello jobs that have completed
Get-AdlJob -Account $adla -State Ended

# List hello jobs that have not started yet
Get-AdlJob -Account $adla -State Accepted,Compiling,New,Paused,Scheduling,Start
```

<span data-ttu-id="3b859-166">Gebruik Hallo `-Result` parameter toodetect of beëindigd taken is voltooid.</span><span class="sxs-lookup"><span data-stu-id="3b859-166">Use hello `-Result` parameter toodetect whether ended jobs completed successfully.</span></span> <span data-ttu-id="3b859-167">Deze heeft de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="3b859-167">It has these values:</span></span>

* <span data-ttu-id="3b859-168">Geannuleerd</span><span class="sxs-lookup"><span data-stu-id="3b859-168">Cancelled</span></span>
* <span data-ttu-id="3b859-169">Is mislukt</span><span class="sxs-lookup"><span data-stu-id="3b859-169">Failed</span></span>
* <span data-ttu-id="3b859-170">Geen</span><span class="sxs-lookup"><span data-stu-id="3b859-170">None</span></span>
* <span data-ttu-id="3b859-171">Geslaagd</span><span class="sxs-lookup"><span data-stu-id="3b859-171">Succeeded</span></span>

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


<span data-ttu-id="3b859-172">Hallo `-Submitter` parameter kunt u bepalen wie een taak heeft ingediend.</span><span class="sxs-lookup"><span data-stu-id="3b859-172">hello `-Submitter` parameter helps you identify who submitted a job.</span></span>

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

<span data-ttu-id="3b859-173">Hallo `-SubmittedAfter` is handig bij het filteren van tooa tijdsbereik.</span><span class="sxs-lookup"><span data-stu-id="3b859-173">hello `-SubmittedAfter` is useful in filtering tooa time range.</span></span>


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a><span data-ttu-id="3b859-174">Algemene scenario's voor het weergeven van taken</span><span class="sxs-lookup"><span data-stu-id="3b859-174">Common scenarios for listing jobs</span></span>


```
# List jobs submitted in hello last five days and that successfully completed.
$d = (Get-Date).AddDays(-5)
Get-AdlJob -Account $adla -SubmittedAfter $d -State Ended -Result Succeeded

# List all failed jobs submitted by "joe@contoso.com" within hello past seven days.
Get-AdlJob -Account $adla `
    -Submitter "joe@contoso.com" `
    -SubmittedAfter (Get-Date).AddDays(-7) `
    -Result Failed
```

## <a name="filtering-a-list-of-jobs"></a><span data-ttu-id="3b859-175">Een lijst met taken filteren</span><span class="sxs-lookup"><span data-stu-id="3b859-175">Filtering a list of jobs</span></span>

<span data-ttu-id="3b859-176">Eenmaal hebt u een lijst met taken in uw huidige PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="3b859-176">Once you have a list of jobs in your current PowerShell session.</span></span> <span data-ttu-id="3b859-177">U kunt de normale PowerShell-cmdlets toofilter Hallo lijst gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3b859-177">You can use normal PowerShell cmdlets toofilter hello list.</span></span>

<span data-ttu-id="3b859-178">Een lijst met taken toohello taken filter verzonden in Hallo afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="3b859-178">Filter a list of jobs toohello jobs submitted in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

<span data-ttu-id="3b859-179">Filteren van een lijst met taken toohello taken die zijn beëindigd Hallo afgelopen 24 uur</span><span class="sxs-lookup"><span data-stu-id="3b859-179">Filter a list of jobs toohello jobs that ended in hello last 24 hours</span></span>

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

<span data-ttu-id="3b859-180">Filteren van een lijst met taken toohello taken die is gestart.</span><span class="sxs-lookup"><span data-stu-id="3b859-180">Filter a list of jobs toohello jobs that started running.</span></span> <span data-ttu-id="3b859-181">Een taak kan mislukken tijdens de compilatie - en dus wordt nooit gestart.</span><span class="sxs-lookup"><span data-stu-id="3b859-181">A job might fail at compile time - and so it never starts.</span></span> <span data-ttu-id="3b859-182">Bekijk Hallo is mislukt-taken die daadwerkelijk is gestart en vervolgens is mislukt.</span><span class="sxs-lookup"><span data-stu-id="3b859-182">Let's look at hello failed jobs that actually started running and then failed.</span></span>

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a><span data-ttu-id="3b859-183">Een lijst met taken analyseren</span><span class="sxs-lookup"><span data-stu-id="3b859-183">Analyzing a list of jobs</span></span>

<span data-ttu-id="3b859-184">Gebruik Hallo `Group-Object` tooanalyze cmdlet een lijst met taken.</span><span class="sxs-lookup"><span data-stu-id="3b859-184">Use hello `Group-Object` cmdlet tooanalyze a list of jobs.</span></span>

```
# Count hello number of jobs by Submitter
$jobs | Group-Object Submitter | Select -Property Count,Name

# Count hello number of jobs by Result
$jobs | Group-Object Result | Select -Property Count,Name

# Count hello number of jobs by State
$jobs | Group-Object State | Select -Property Count,Name

#  Count hello number of jobs by DegreeOfParallelism
$jobs | Group-Object DegreeOfParallelism | Select -Property Count,Name
```
<span data-ttu-id="3b859-185">Bij het uitvoeren van een analyse, kan het nuttig tooadd eigenschappen toohello taak objecten toomake filteren en groeperen eenvoudiger zijn.</span><span class="sxs-lookup"><span data-stu-id="3b859-185">When performing an analysis, it can be useful tooadd properties toohello Job objects toomake filtering and grouping simpler.</span></span> <span data-ttu-id="3b859-186">Hallo volgende fragment toont hoe tooannotate een Taakinfo met eigenschappen berekend.</span><span class="sxs-lookup"><span data-stu-id="3b859-186">hello following  snippet shows how tooannotate a JobInfo with calculated properties.</span></span>

```
function annotate_job( $j )
{
    $dic1 = @{
        Label='AUHours';
        Expression={ ($_.DegreeOfParallelism * ($_.EndTime-$_.StartTime).TotalHours)}}
    $dic2 = @{
        Label='DurationSeconds';
        Expression={ ($_.EndTime-$_.StartTime).TotalSeconds}}
    $dic3 = @{
        Label='DidRun';
        Expression={ ($_.StartTime -ne $null)}}

    $j2 = $j | select *, $dic1, $dic2, $dic3
    $j2
}

$jobs = Get-AdlJob -Account $adla -Top 10
$jobs = $jobs | %{ annotate_job( $_ ) }
```

## <a name="get-information-about-pipelines-and-recurrences"></a><span data-ttu-id="3b859-187">Informatie ophalen over de pijplijnen en herhalingen</span><span class="sxs-lookup"><span data-stu-id="3b859-187">Get information about pipelines and recurrences</span></span>

<span data-ttu-id="3b859-188">Gebruik Hallo `Get-AdlJobPipeline` cmdlet toosee Hallo pijplijn informatie taken eerder is verzonden.</span><span class="sxs-lookup"><span data-stu-id="3b859-188">Use hello `Get-AdlJobPipeline` cmdlet toosee hello pipeline information previously submitted jobs.</span></span>

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

<span data-ttu-id="3b859-189">Gebruik Hallo `Get-AdlJobRecurrence` cmdlet toosee Hallo terugkeerpatroon informatie voor eerder ingediende taken.</span><span class="sxs-lookup"><span data-stu-id="3b859-189">Use hello `Get-AdlJobRecurrence` cmdlet toosee hello recurrence information for previously submitted jobs.</span></span>

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a><span data-ttu-id="3b859-190">Informatie over een taak ophalen</span><span class="sxs-lookup"><span data-stu-id="3b859-190">Get information about a job</span></span>

### <a name="get-job-status"></a><span data-ttu-id="3b859-191">Taakstatus ophalen</span><span class="sxs-lookup"><span data-stu-id="3b859-191">Get job status</span></span>

<span data-ttu-id="3b859-192">Hallo-status van een bepaalde taak ophalen.</span><span class="sxs-lookup"><span data-stu-id="3b859-192">Get hello status of a specific job.</span></span>

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a><span data-ttu-id="3b859-193">Hallo taak uitvoer onderzoeken</span><span class="sxs-lookup"><span data-stu-id="3b859-193">Examine hello job outputs</span></span>

<span data-ttu-id="3b859-194">Nadat Hallo-taak is beëindigd, moet u controleren of het uitvoerbestand Hallo bestaat door Hallo-bestanden in een map aan te bieden.</span><span class="sxs-lookup"><span data-stu-id="3b859-194">After hello job has ended, check if hello output file exists by listing hello files in a folder.</span></span>

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a><span data-ttu-id="3b859-195">Actieve taken beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-195">Manage running jobs</span></span>

### <a name="cancel-a-job"></a><span data-ttu-id="3b859-196">Een taak annuleren</span><span class="sxs-lookup"><span data-stu-id="3b859-196">Cancel a job</span></span>

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a><span data-ttu-id="3b859-197">Wachten op een taak toofinish</span><span class="sxs-lookup"><span data-stu-id="3b859-197">Wait for a job toofinish</span></span>

<span data-ttu-id="3b859-198">In plaats van herhalende `Get-AdlAnalyticsJob` totdat een taak is voltooid, kunt u Hallo `Wait-AdlJob` cmdlet toowait voor Hallo taak tooend.</span><span class="sxs-lookup"><span data-stu-id="3b859-198">Instead of repeating `Get-AdlAnalyticsJob` until a job finishes, you can use hello `Wait-AdlJob` cmdlet toowait for hello job tooend.</span></span>

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a><span data-ttu-id="3b859-199">Compute-beleid beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-199">Manage compute policies</span></span>

### <a name="list-existing-compute-policies"></a><span data-ttu-id="3b859-200">Lijst met bestaande compute-beleidsregels</span><span class="sxs-lookup"><span data-stu-id="3b859-200">List existing compute policies</span></span>

<span data-ttu-id="3b859-201">Hallo `Get-AdlAnalyticsComputePolicy` cmdlet haalt de info over compute-beleid voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-201">hello `Get-AdlAnalyticsComputePolicy` cmdlet retrieves info about compute policies for a Data Lake Analytics account.</span></span>

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a><span data-ttu-id="3b859-202">Een compute-beleid maken</span><span class="sxs-lookup"><span data-stu-id="3b859-202">Create a compute policy</span></span>

<span data-ttu-id="3b859-203">Hallo `New-AdlAnalyticsComputePolicy` cmdlet maakt een nieuw compute-beleid voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="3b859-203">hello `New-AdlAnalyticsComputePolicy` cmdlet creates a new compute policy for a Data Lake Analytics account.</span></span> <span data-ttu-id="3b859-204">In dit voorbeeld sets Hallo maximale AUs beschikbaar toohello opgegeven gebruiker too50 en Hallo Minimumprioriteit prioriteit too250.</span><span class="sxs-lookup"><span data-stu-id="3b859-204">This example sets  hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a><span data-ttu-id="3b859-205">Controleer op het Hallo bestaan van een bestand.</span><span class="sxs-lookup"><span data-stu-id="3b859-205">Check for hello existence of a file.</span></span>

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a><span data-ttu-id="3b859-206">Uploaden en downloaden</span><span class="sxs-lookup"><span data-stu-id="3b859-206">Uploading and downloading</span></span>

<span data-ttu-id="3b859-207">Bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="3b859-207">Upload a file.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

<span data-ttu-id="3b859-208">Upload een hele map recursief.</span><span class="sxs-lookup"><span data-stu-id="3b859-208">Upload an entire folder recursively.</span></span>

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

<span data-ttu-id="3b859-209">Een bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="3b859-209">Download a file.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

<span data-ttu-id="3b859-210">Download een hele map recursief.</span><span class="sxs-lookup"><span data-stu-id="3b859-210">Download an entire folder recursively.</span></span>

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> <span data-ttu-id="3b859-211">Als hello uploaden of downloadproces wordt onderbroken, kunt u tooresume Hallo proces proberen door actieve Hallo cmdlet opnieuw uit met Hallo ``-Resume`` vlag.</span><span class="sxs-lookup"><span data-stu-id="3b859-211">If hello upload or download process is interrupted, you can attempt tooresume hello process by running hello cmdlet again with hello ``-Resume`` flag.</span></span>

## <a name="manage-catalog-items"></a><span data-ttu-id="3b859-212">Catalogusitems beheren</span><span class="sxs-lookup"><span data-stu-id="3b859-212">Manage catalog items</span></span>

<span data-ttu-id="3b859-213">Hallo U-SQL-catalogus is toostructure gebruikte gegevens en code zodat ze kunnen worden gedeeld door de U-SQL-scripts.</span><span class="sxs-lookup"><span data-stu-id="3b859-213">hello U-SQL catalog is used toostructure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="3b859-214">Hallo catalogus kunt Hallo hoogste prestaties mogelijk met gegevens in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3b859-214">hello catalog enables hello highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="3b859-215">Zie [U-SQL-catalogus gebruiken](data-lake-analytics-use-u-sql-catalog.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3b859-215">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-items-in-hello-u-sql-catalog"></a><span data-ttu-id="3b859-216">Lijstitems in Hallo U-SQL-catalogus</span><span class="sxs-lookup"><span data-stu-id="3b859-216">List items in hello U-SQL catalog</span></span>

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

<span data-ttu-id="3b859-217">Lijst van alle Hallo-assembly's in alle Hallo-databases in een ADLA-Account.</span><span class="sxs-lookup"><span data-stu-id="3b859-217">List all hello assemblies in all hello databases in an ADLA Account.</span></span>

```powershell
$dbs = Get-AdlCatalogItem -Account $adla -ItemType Database

foreach ($db in $dbs)
{
    $asms = Get-AdlCatalogItem -Account $adla -ItemType Assembly -Path $db.Name

    foreach ($asm in $asms)
    {
        $asmname = "[" + $db.Name + "].[" + $asm.Name + "]"
        Write-Host $asmname
    }
}
```

### <a name="get-details-about-a-catalog-item"></a><span data-ttu-id="3b859-218">Informatie ophalen over een catalogusitem</span><span class="sxs-lookup"><span data-stu-id="3b859-218">Get details about a catalog item</span></span>

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a><span data-ttu-id="3b859-219">Referenties in een catalogus maken</span><span class="sxs-lookup"><span data-stu-id="3b859-219">Create credentials in a catalog</span></span>

<span data-ttu-id="3b859-220">In een U-SQL-database, moet u een referentieobject voor een database die wordt gehost in Azure maken.</span><span class="sxs-lookup"><span data-stu-id="3b859-220">Within a U-SQL database, create a credential object for a database hosted in Azure.</span></span> <span data-ttu-id="3b859-221">U-SQL-referenties zijn momenteel Hallo enige type catalogusitem die u via PowerShell kunt maken.</span><span class="sxs-lookup"><span data-stu-id="3b859-221">Currently, U-SQL credentials are hello only type of catalog item that you can create through PowerShell.</span></span>

```powershell
$dbName = "master"
$credentialName = "ContosoDbCreds"
$dbUri = "https://contoso.database.windows.net:8080"

New-AdlCatalogCredential -AccountName $adla `
          -DatabaseName $db `
          -CredentialName $credentialName `
          -Credential (Get-Credential) `
          -Uri $dbUri
```

### <a name="get-basic-information-about-an-adla-account"></a><span data-ttu-id="3b859-222">Algemene informatie over een ADLA-account ophalen</span><span class="sxs-lookup"><span data-stu-id="3b859-222">Get basic information about an ADLA account</span></span>

<span data-ttu-id="3b859-223">Gegeven een accountnaam Hallo volgende code wordt er gezocht basisinformatie over Hallo-account</span><span class="sxs-lookup"><span data-stu-id="3b859-223">Given an account name, hello following code looks up basic information about hello account</span></span>

```
$adla_acct = Get-AdlAnalyticsAccount -Name "saveenrdemoadla"
$adla_name = $adla_acct.Name
$adla_subid = $adla_acct.Id.Split("/")[2]
$adla_sub = Get-AzureRmSubscription -SubscriptionId $adla_subid
$adla_subname = $adla_sub.Name
$adla_defadls_datasource = Get-AdlAnalyticsDataSource -Account $adla_name  | ? { $_.IsDefault } 
$adla_defadlsname = $adla_defadls_datasource.Name

Write-Host "ADLA Account Name" $adla_name
Write-Host "Subscription Id" $adla_subid
Write-Host "Subscription Name" $adla_subname
Write-Host "Defautl ADLS Store" $adla_defadlsname
Write-Host 

Write-Host '$subname' " = ""$adla_subname"" "
Write-Host '$subid' " = ""$adla_subid"" "
Write-Host '$adla' " = ""$adla_name"" "
Write-Host '$adls' " = ""$adla_defadlsname"" "
```

## <a name="working-with-azure"></a><span data-ttu-id="3b859-224">Werken met Azure</span><span class="sxs-lookup"><span data-stu-id="3b859-224">Working with Azure</span></span>

### <a name="get-details-of-azurerm-errors"></a><span data-ttu-id="3b859-225">Details van fouten AzureRm ophalen</span><span class="sxs-lookup"><span data-stu-id="3b859-225">Get details of AzureRm errors</span></span>

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a><span data-ttu-id="3b859-226">Controleer of als u als administrator uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3b859-226">Verify if you are running as an administrator</span></span>

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a><span data-ttu-id="3b859-227">Een TenantID vinden</span><span class="sxs-lookup"><span data-stu-id="3b859-227">Find a TenantID</span></span>

<span data-ttu-id="3b859-228">Van de naam van een abonnement:</span><span class="sxs-lookup"><span data-stu-id="3b859-228">From a subscription name:</span></span>

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

<span data-ttu-id="3b859-229">Van een abonnement-id:</span><span class="sxs-lookup"><span data-stu-id="3b859-229">From a subscription id:</span></span>

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

<span data-ttu-id="3b859-230">Van een domeinadres zoals 'contoso.com'</span><span class="sxs-lookup"><span data-stu-id="3b859-230">From a domain address such as "contoso.com"</span></span>


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a><span data-ttu-id="3b859-231">Een lijst van al uw abonnementen en tenant-id 's</span><span class="sxs-lookup"><span data-stu-id="3b859-231">List all your subscriptions and tenant ids</span></span>

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a><span data-ttu-id="3b859-232">Een Data Lake Analytics-account met een sjabloon maken</span><span class="sxs-lookup"><span data-stu-id="3b859-232">Create a Data Lake Analytics account using a template</span></span>

<span data-ttu-id="3b859-233">U kunt ook een Azure-resourcegroep sjabloon met behulp van de volgende PowerShell-script hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="3b859-233">You can also use an Azure Resource Group template using hello following  PowerShell script:</span></span>

```powershell
$subId = "<Your Azure Subscription ID>"

$rg = "<New Azure Resource Group Name>"
$location = "<Location (such as East US 2)>"
$adls = "<New Data Lake Store Account Name>"
$adla = "<New Data Lake Analytics Account Name>"

$deploymentName = "MyDataLakeAnalyticsDeployment"
$armTemplateFile = "<LocalFolderPath>\azuredeploy.json"  # update hello JSON template path 

# Log in tooAzure
Login-AzureRmAccount -SubscriptionId $subId

# Create hello resource group
New-AzureRmResourceGroup -Name $rg -Location $location

# Create hello Data Lake Analytics account with hello default Data Lake Store account.
$parameters = @{"adlAnalyticsName"=$adla; "adlStoreName"=$adls}
New-AzureRmResourceGroupDeployment -Name $deploymentName -ResourceGroupName $rg -TemplateFile $armTemplateFile -TemplateParameterObject $parameters 
```

<span data-ttu-id="3b859-234">Zie voor meer informatie [Implementeer een toepassing met Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md) en [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3b859-234">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="3b859-235">**Van de voorbeeldsjabloon**</span><span class="sxs-lookup"><span data-stu-id="3b859-235">**Example template**</span></span>

<span data-ttu-id="3b859-236">Opslaan van Hallo tekst als volgt een `.json` bestand en gebruik vervolgens Hallo voorafgaand aan de PowerShell-script toouse Hallo sjabloon.</span><span class="sxs-lookup"><span data-stu-id="3b859-236">Save hello following text as a `.json` file, and then use hello preceding PowerShell script toouse hello template.</span></span> 

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adlAnalyticsName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Analytics account toocreate."
      }
    },
    "adlStoreName": {
      "type": "string",
      "metadata": {
        "description": "hello name of hello Data Lake Store account toocreate."
      }
    }
  },
  "resources": [
    {
      "name": "[parameters('adlStoreName')]",
      "type": "Microsoft.DataLakeStore/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ ],
      "tags": { }
    },
    {
      "name": "[parameters('adlAnalyticsName')]",
      "type": "Microsoft.DataLakeAnalytics/accounts",
      "location": "East US 2",
      "apiVersion": "2015-10-01-preview",
      "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
      "tags": { },
      "properties": {
        "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
        "dataLakeStoreAccounts": [
          { "name": "[parameters('adlStoreName')]" }
        ]
      }
    }
  ],
  "outputs": {
    "adlAnalyticsAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
    },
    "adlStoreAccount": {
      "type": "object",
      "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="3b859-237">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3b859-237">Next steps</span></span>
* [<span data-ttu-id="3b859-238">Overzicht van Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3b859-238">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* <span data-ttu-id="3b859-239">Aan de slag met Data Lake Analytics met [Azure-portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span><span class="sxs-lookup"><span data-stu-id="3b859-239">Get started with Data Lake Analytics using [Azure portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)</span></span>
* <span data-ttu-id="3b859-240">Azure Data Lake Analytics beheren met [Azure-portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span><span class="sxs-lookup"><span data-stu-id="3b859-240">Manage Azure Data Lake Analytics using [Azure portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md)</span></span> 
