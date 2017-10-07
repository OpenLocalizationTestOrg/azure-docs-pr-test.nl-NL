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
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a>Azure Data Lake Analytics beheren met Azure PowerShell
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Informatie over hoe toomanage Azure Data Lake Analytics-accounts, gegevensbronnen, taken en catalogusitems met Azure PowerShell. 

## <a name="prerequisites"></a>Vereisten

Wanneer u een Data Lake Analytics-account maakt, moet u tooknow:

* **Abonnements-ID**: hello Azure-abonnement-ID die uw Data Lake Analytics-account zich bevindt.
* **Resourcegroep**: Hallo-naam van hello Azure-resourcegroep met uw Data Lake Analytics-account.
* **Data Lake Analytics-accountnaam**: Hallo account naam mag alleen kleine letters en cijfers.
* **Data Lake Store-standaardaccount**: elk Data Lake Store Analytics-account heeft een Data Lake Store-standaardaccount. Deze accounts moeten zich in Hallo dezelfde locatie.
* **Locatie**: Hallo-locatie van uw Data Lake Analytics-account, zoals "VS-Oost 2" of andere locaties ondersteund. Ondersteunde locaties kunnen worden weergegeven op onze [pagina met prijzen](https://azure.microsoft.com/pricing/details/data-lake-analytics/).

Deze variabelen toostore deze informatie Hallo PowerShell codefragmenten in deze zelfstudie gebruiken

```powershell
$subId = "<SubscriptionId>"
$rg = "<ResourceGroupName>"
$adla = "<DataLakeAnalyticsAccountName>"
$adls = "<DataLakeStoreAccountName>"
$location = "<Location>"
```

## <a name="log-in"></a>Aanmelden

Meld u aan met een abonnements-id.

```powershell
Login-AzureRmAccount -SubscriptionId $subId
```

Meld u aan met de naam van een abonnement.

```
Login-AzureRmAccount -SubscriptionName $subname 
```

Hallo `Login-AzureRmAccount` cmdlet altijd om referenties gevraagd. U kunt voorkomen dat u met behulp van de volgende cmdlets Hallo wordt gevraagd:

```powershell
# Save login session information
Save-AzureRmProfile -Path D:\profile.json  

# Load login session information
Select-AzureRmProfile -Path D:\profile.json 
```

## <a name="managing-accounts"></a>Accounts beheren

### <a name="create-a-data-lake-analytics-account"></a>Een Data Lake Analytics-account maken

Als u nog geen hebt een [resourcegroep](../azure-resource-manager/resource-group-overview.md#resource-groups) toouse, een maken. 

```powershell
New-AzureRmResourceGroup -Name  $rg -Location $location
```

Elke Data Lake Analytics-account vereist een Data Lake Store-standaardaccount dat wordt gebruikt voor het opslaan van logboeken. U kunt een bestaand account gebruiken of een account maken. 

```powershell
New-AdlStore -ResourceGroupName $rg -Name $adls -Location $location
```

Wanneer een resourcegroep en Data Lake Store-account beschikbaar zijn, kunt u een Data Lake Analytics-account maken.

```powershell
New-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla -Location $location -DefaultDataLake $adls
```

### <a name="get-information-about-an-account"></a>Informatie ophalen over een account

Informatie ophalen over een account.

```powershell
Get-AdlAnalyticsAccount -Name $adla
```

Controleren op Hallo bestaan van een specifieke Data Lake Analytics-account. Hallo cmdlet retourneert een `True` of `False`.

```powershell
Test-AdlAnalyticsAccount -Name $adla
```

Controleren op Hallo bestaan van een specifieke Data Lake Store-account. Hallo cmdlet retourneert een `True` of `False`.

```powershell
Test-AdlStoreAccount -Name $adls
```

### <a name="listing-accounts"></a>Aanbieding-accounts

Lijst met Data Lake Analytics-accounts binnen het huidige abonnement Hallo.

```powershell
Get-AdlAnalyticsAccount
```

Lijst met Data Lake Analytics-accounts binnen een specifieke resourcegroep.

```powershell
Get-AdlAnalyticsAccount -ResourceGroupName $rg
```

## <a name="managing-firewall-rules"></a>Firewall-regels beheren

Lijst van firewallregels.

```powershell
Get-AdlAnalyticsFirewallRule -Account $adla
```

Een firewallregel toevoegen.

```powershell
$ruleName = "Allow access from on-prem server"
$startIpAddress = "<start IP address>"
$endIpAddress = "<end IP address>"

Add-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Een firewallregel wijzigen.

```powershell
Set-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName -StartIpAddress $startIpAddress -EndIpAddress $endIpAddress
```

Een firewallregel verwijderen.

```powershell
Remove-AdlAnalyticsFirewallRule -Account $adla -Name $ruleName
```



Azure-IP-adressen toestaan.

```powershell
Set-AdlAnalyticsAccount -Name $adla -AllowAzureIpState Enabled
```

```powershell
Set-AdlAnalyticsAccount -Name $adla -FirewallState Enabled
Set-AdlAnalyticsAccount -Name $adla -FirewallState Disabled
```

## <a name="managing-data-sources"></a>Gegevensbronnen beheren
Azure Data Lake Analytics ondersteunt momenteel Hallo gegevensbronnen te volgen:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

Wanneer u een Analytics-account maakt, moet u een Data Lake Store-account toobe Hallo standaardgegevensbron toewijzen. Hallo Data Lake Store-standaardaccount wordt gebruikt toostore taak metagegevens en taak controlelogboeken. Nadat u een Data Lake Analytics-account hebt gemaakt, kunt u extra Data Lake Store-accounts en/of de Storage-accounts toevoegen. 

### <a name="find-hello-default-data-lake-store-account"></a>Hallo default Data Lake Store-account vinden

```powershell
$adla_acct = Get-AdlAnalyticsAccount -Name $adla
$dataLakeStoreName = $adla_acct.DefaultDataLakeAccount
```

U kunt Hallo standaard Data Lake Store-account vinden door de lijst van gegevensbronnen Hallo filteren op Hallo `IsDefault` eigenschap:

```powershell
Get-AdlAnalyticsDataSource -Account $adla  | ? { $_.IsDefault } 
```

### <a name="add-a-data-source"></a>Een gegevensbron toevoegen

```powershell

# Add an additional Storage (Blob) account.
$AzureStorageAccountName = "<AzureStorageAccountName>"
$AzureStorageAccountKey = "<AzureStorageAccountKey>"
Add-AdlAnalyticsDataSource -Account $adla -Blob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

# Add an additional Data Lake Store account.
$AzureDataLakeStoreName = "<AzureDataLakeStoreAccountName"
Add-AdlAnalyticsDataSource -Account $adla -DataLakeStore $AzureDataLakeStoreName 
```

### <a name="list-data-sources"></a>Lijst met gegevensbronnen

```powershell
# List all hello data sources
Get-AdlAnalyticsDataSource -Name $adla

# List attached Data Lake Store accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "DataLakeStore"

# List attached Storage accounts
Get-AdlAnalyticsDataSource -Name $adla | where -Property Type -EQ "Blob"
```

## <a name="submit-u-sql-jobs"></a>U-SQL-taken verzenden

### <a name="submit-a-string-as-a-u-sql-script"></a>Verzenden van een tekenreeks als een U-SQL-script

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


### <a name="submit-a-file-as-a-u-sql-script"></a>Een bestand verzenden als een U-SQL-script

```powershell
$scriptpath = "d:\test.usql"
$script | Out-File $scriptpath 
Submit-AdlJob -AccountName $adla –ScriptPath $scriptpath -Name "Demo"
```

## <a name="list-jobs-in-an-account"></a>Lijst met taken in een account

### <a name="list-all-hello-jobs-in-hello-account"></a>Lijst van alle Hallo jobs in Hallo-account. 

Hallo uitvoer bevat Hallo actieve taken en de taken die u onlangs hebt voltooid.

```powershell
Get-AdlJob -Account $adla
```


### <a name="list-a-specific-number-of-jobs"></a>Lijst van een bepaald aantal taken

Standaard Hallo lijst met taken is gesorteerd op tijd te verzenden. Dus Hallo meest recent verzonden taken eerste worden weergegeven. Hallo ADLA account onthoudt taken gedurende 180 dagen, maar alleen Hallo eerste 500 Hallo Ge AdlJob cmdlet door standaard retourneert. Gebruik - bovenste parameter toolist een bepaald aantal taken.

```powershell
$jobs = Get-AdlJob -Account $adla -Top 10
```


### <a name="list-jobs-based-on-hello-value-of-job-property"></a>Lijst met taken op basis van het Hallo-waarde van taakeigenschap

Met behulp van Hallo `-State` parameter. U kunt deze waarden combineren:

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

Gebruik Hallo `-Result` parameter toodetect of beëindigd taken is voltooid. Deze heeft de volgende waarden:

* Geannuleerd
* Is mislukt
* Geen
* Geslaagd

``` powershell
# List Successful jobs.
Get-AdlJob -Account $adla -State Ended -Result Succeeded

# List Failed jobs.
Get-AdlJob -Account $adla -State Ended -Result Failed
```


Hallo `-Submitter` parameter kunt u bepalen wie een taak heeft ingediend.

```powershell
Get-AdlJob -Account $adla -Submitter "joe@contoso.com"
```

Hallo `-SubmittedAfter` is handig bij het filteren van tooa tijdsbereik.


```powershell
# List  jobs submitted in hello last day.
$d = [DateTime]::Now.AddDays(-1)
Get-AdlJob -Account $adla -SubmittedAfter $d

# List  jobs submitted in hello last seven day.
$d = [DateTime]::Now.AddDays(-7)
Get-AdlJob -Account $adla -SubmittedAfter $d
```

### <a name="common-scenarios-for-listing-jobs"></a>Algemene scenario's voor het weergeven van taken


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

## <a name="filtering-a-list-of-jobs"></a>Een lijst met taken filteren

Eenmaal hebt u een lijst met taken in uw huidige PowerShell-sessie. U kunt de normale PowerShell-cmdlets toofilter Hallo lijst gebruiken.

Een lijst met taken toohello taken filter verzonden in Hallo afgelopen 24 uur

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.EndTime -ge $lowerdate }
```

Filteren van een lijst met taken toohello taken die zijn beëindigd Hallo afgelopen 24 uur

```
$upperdate = Get-Date
$lowerdate = $upperdate.AddHours(-24)
$jobs | Where-Object { $_.SubmitTime -ge $lowerdate }
```

Filteren van een lijst met taken toohello taken die is gestart. Een taak kan mislukken tijdens de compilatie - en dus wordt nooit gestart. Bekijk Hallo is mislukt-taken die daadwerkelijk is gestart en vervolgens is mislukt.

```powershell
$jobs | Where-Object { $_.StartTime -ne $null }
```

### <a name="analyzing-a-list-of-jobs"></a>Een lijst met taken analyseren

Gebruik Hallo `Group-Object` tooanalyze cmdlet een lijst met taken.

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
Bij het uitvoeren van een analyse, kan het nuttig tooadd eigenschappen toohello taak objecten toomake filteren en groeperen eenvoudiger zijn. Hallo volgende fragment toont hoe tooannotate een Taakinfo met eigenschappen berekend.

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

## <a name="get-information-about-pipelines-and-recurrences"></a>Informatie ophalen over de pijplijnen en herhalingen

Gebruik Hallo `Get-AdlJobPipeline` cmdlet toosee Hallo pijplijn informatie taken eerder is verzonden.

```powershell
$pipelines = Get-AdlJobPipeline -Account $adla

$pipeline = Get-AdlJobPipeline -Account $adla -PipelineId "<pipeline ID>"
```

Gebruik Hallo `Get-AdlJobRecurrence` cmdlet toosee Hallo terugkeerpatroon informatie voor eerder ingediende taken.

```powershell
$recurrences = Get-AdlJobRecurrence -Account $adla

$recurrence = Get-AdlJobRecurrence -Account $adla -RecurrenceId "<recurrence ID>"
```

## <a name="get-information-about-a-job"></a>Informatie over een taak ophalen

### <a name="get-job-status"></a>Taakstatus ophalen

Hallo-status van een bepaalde taak ophalen.

```powershell
Get-AdlJob -AccountName $adla -JobId $job.JobId
```

### <a name="examine-hello-job-outputs"></a>Hallo taak uitvoer onderzoeken

Nadat Hallo-taak is beëindigd, moet u controleren of het uitvoerbestand Hallo bestaat door Hallo-bestanden in een map aan te bieden.

```powershell
Get-AdlStoreChildItem -Account $adls -Path "/"
```

## <a name="manage-running-jobs"></a>Actieve taken beheren

### <a name="cancel-a-job"></a>Een taak annuleren

```powershell
Stop-AdlJob -Account $adls -JobID $jobID
```

### <a name="wait-for-a-job-toofinish"></a>Wachten op een taak toofinish

In plaats van herhalende `Get-AdlAnalyticsJob` totdat een taak is voltooid, kunt u Hallo `Wait-AdlJob` cmdlet toowait voor Hallo taak tooend.

```powershell
Wait-AdlJob -Account $adla -JobId $job.JobId
```

## <a name="manage-compute-policies"></a>Compute-beleid beheren

### <a name="list-existing-compute-policies"></a>Lijst met bestaande compute-beleidsregels

Hallo `Get-AdlAnalyticsComputePolicy` cmdlet haalt de info over compute-beleid voor een Data Lake Analytics-account.

```powershell
$policies = Get-AdlAnalyticsComputePolicy -Account $adla
```

### <a name="create-a-compute-policy"></a>Een compute-beleid maken

Hallo `New-AdlAnalyticsComputePolicy` cmdlet maakt een nieuw compute-beleid voor een Data Lake Analytics-account. In dit voorbeeld sets Hallo maximale AUs beschikbaar toohello opgegeven gebruiker too50 en Hallo Minimumprioriteit prioriteit too250.

```powershell
$userObjectId = (Get-AzureRmAdUser -SearchString "garymcdaniel@contoso.com").Id

New-AdlAnalyticsComputePolicy -Account $adla -Name "GaryMcDaniel" -ObjectId $objectId -ObjectType User -MaxDegreeOfParallelismPerJob 50 -MinPriorityPerJob 250
```

## <a name="check-for-hello-existence-of-a-file"></a>Controleer op het Hallo bestaan van een bestand.

```powershell
Test-AdlStoreItem -Account $adls -Path "/data.csv"
```

## <a name="uploading-and-downloading"></a>Uploaden en downloaden

Bestand uploaden.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\data.tsv" -Destination "/data_copy.csv" 
```

Upload een hele map recursief.

```powershell
Import-AdlStoreItem -AccountName $adls -Path "c:\myData\" -Destination "/myData/" -Recurse
```

Een bestand downloaden.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "c:\data.csv"
```

Download een hele map recursief.

```powershell
Export-AdlStoreItem -AccountName $adls -Path "/" -Destination "c:\myData\" -Recurse
```

> [!NOTE]
> Als hello uploaden of downloadproces wordt onderbroken, kunt u tooresume Hallo proces proberen door actieve Hallo cmdlet opnieuw uit met Hallo ``-Resume`` vlag.

## <a name="manage-catalog-items"></a>Catalogusitems beheren

Hallo U-SQL-catalogus is toostructure gebruikte gegevens en code zodat ze kunnen worden gedeeld door de U-SQL-scripts. Hallo catalogus kunt Hallo hoogste prestaties mogelijk met gegevens in Azure Data Lake. Zie [U-SQL-catalogus gebruiken](data-lake-analytics-use-u-sql-catalog.md) voor meer informatie.

### <a name="list-items-in-hello-u-sql-catalog"></a>Lijstitems in Hallo U-SQL-catalogus

```powershell
# List U-SQL databases
Get-AdlCatalogItem -Account $adla -ItemType Database 

# List tables within a database
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database"

# List tables within a schema.
Get-AdlCatalogItem -Account $adla -ItemType Table -Path "database.schema"
```

Lijst van alle Hallo-assembly's in alle Hallo-databases in een ADLA-Account.

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

### <a name="get-details-about-a-catalog-item"></a>Informatie ophalen over een catalogusitem

```powershell
# Get details of a table
Get-AdlCatalogItem  -Account $adla -ItemType Table -Path "master.dbo.mytable"

# Test existence of a U-SQL database.
Test-AdlCatalogItem  -Account $adla -ItemType Database -Path "master"
```

### <a name="create-credentials-in-a-catalog"></a>Referenties in een catalogus maken

In een U-SQL-database, moet u een referentieobject voor een database die wordt gehost in Azure maken. U-SQL-referenties zijn momenteel Hallo enige type catalogusitem die u via PowerShell kunt maken.

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

### <a name="get-basic-information-about-an-adla-account"></a>Algemene informatie over een ADLA-account ophalen

Gegeven een accountnaam Hallo volgende code wordt er gezocht basisinformatie over Hallo-account

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

## <a name="working-with-azure"></a>Werken met Azure

### <a name="get-details-of-azurerm-errors"></a>Details van fouten AzureRm ophalen

```powershell
Resolve-AzureRmError -Last
```

### <a name="verify-if-you-are-running-as-an-administrator"></a>Controleer of als u als administrator uitvoeren

```powershell
function Test-Administrator  
{  
    $user = [Security.Principal.WindowsIdentity]::GetCurrent();
    $p = New-Object Security.Principal.WindowsPrincipal $user
    $p.IsInRole([Security.Principal.WindowsBuiltinRole]::Administrator)  
}
```

### <a name="find-a-tenantid"></a>Een TenantID vinden

Van de naam van een abonnement:

```powershell
function Get-TenantIdFromSubcriptionName( [string] $subname )
{
    $sub = (Get-AzureRmSubscription -SubscriptionName $subname)
    $sub.TenantId
}

Get-TenantIdFromSubcriptionName "ADLTrainingMS"
```

Van een abonnement-id:

```powershell
function Get-TenantIdFromSubcriptionId( [string] $subid )
{
    $sub = (Get-AzureRmSubscription -SubscriptionId $subid)
    $sub.TenantId
}

$subid = "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
Get-TenantIdFromSubcriptionId $subid
```

Van een domeinadres zoals 'contoso.com'


```powershell
function Get-TenantIdFromDomain( $domain )
{
    $url = "https://login.windows.net/" + $domain + "/.well-known/openid-configuration"
    return (Invoke-WebRequest $url|ConvertFrom-Json).token_endpoint.Split('/')[3]
}

$domain = "contoso.com"
Get-TenantIdFromDomain $domain
```

### <a name="list-all-your-subscriptions-and-tenant-ids"></a>Een lijst van al uw abonnementen en tenant-id 's

```powershell
$subs = Get-AzureRmSubscription
foreach ($sub in $subs)
{
    Write-Host $sub.Name "("  $sub.Id ")"
    Write-Host "`tTenant Id" $sub.TenantId
}
```

## <a name="create-a-data-lake-analytics-account-using-a-template"></a>Een Data Lake Analytics-account met een sjabloon maken

U kunt ook een Azure-resourcegroep sjabloon met behulp van de volgende PowerShell-script hello gebruiken:

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

Zie voor meer informatie [Implementeer een toepassing met Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md) en [Azure Resource Manager-sjablonen samenstellen](../azure-resource-manager/resource-group-authoring-templates.md).

**Van de voorbeeldsjabloon**

Opslaan van Hallo tekst als volgt een `.json` bestand en gebruik vervolgens Hallo voorafgaand aan de PowerShell-script toouse Hallo sjabloon. 

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

## <a name="next-steps"></a>Volgende stappen
* [Overzicht van Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* Aan de slag met Data Lake Analytics met [Azure-portal](data-lake-analytics-get-started-portal.md) | [Azure PowerShell](data-lake-analytics-get-started-powershell.md) | [CLI 2.0](data-lake-analytics-get-started-cli2.md)
* Azure Data Lake Analytics beheren met [Azure-portal](data-lake-analytics-manage-use-portal.md) | [Azure PowerShell](data-lake-analytics-manage-use-powershell.md) | [CLI](data-lake-analytics-manage-use-cli.md) 
